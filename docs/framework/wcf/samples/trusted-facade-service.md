---
title: "Доверенная фасадная служба"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c34d1a8f-e45e-440b-a201-d143abdbac38
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 8c0d1d0473a821510ee70e386058a2b3249221dd
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="trusted-facade-service"></a>Доверенная фасадная служба
В этом образце сценария показано, как передать информацию удостоверения вызывающей стороны от одной службы к другой с помощью инфраструктуры безопасности [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] .  
  
 Обычно разработчики обеспечивают предоставление функциональных возможностей службы в открытую сеть через "фасадную" службу. Фасадная служба обычно размещается в демилитаризованной зоне (также называемой промежуточной подсетью или DMZ) и взаимодействует с серверной службой, реализующей бизнес-логику и имеющей доступ к внутренним данным. Коммуникационный канал между фасадной службой и серверной службой проходит через брандмауэр, и обычно он используется только для одной цели.  
  
 Код в этом образце состоит из следующих компонентов:  
  
-   Клиентская часть калькулятора  
  
-   Фасадная служба калькулятора  
  
-   Серверная служба калькулятора  
  
 Фасадная служба проверяет запрос и подлинность вызывающей стороны. После успешного выполнения этих проверок она передает запрос серверной службе по управляемому коммуникационному каналу из демилитаризованной зоны во внутреннюю сеть. В передаваемый запрос фасадная служба добавляет удостоверение вызывающей стороны, чтобы серверная служба могла использовать его при обработке. Это удостоверение передается с помощью маркера безопасности `Username` в заголовке сообщения `Security` . В данном образце для передачи этой информации и ее извлечения из заголовка [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] используется инфраструктура безопасности `Security` .  
  
> [!IMPORTANT]
>  Серверная служба доверяет результатам проверки подлинности вызывающей стороны, выполненной фасадной службой. Поэтому серверная служба не выполняет проверку подлинности повторно. Она использует удостоверение, предоставленное фасадной службой в переданном запросе. Это отношение доверия требует, чтобы серверная служба проверяла подлинность фасадной службы, чтобы убедиться, что сообщение передано из надежного источника (в данном случае - от фасадной службы).  
  
## <a name="implementation"></a>Реализация  
 В этом образце используются два пути обмена данными: между клиентом и фасадной службой и между фасадной службой и серверной службой.  
  
### <a name="communication-path-between-client-and-faade-service"></a>Путь обмена данными между клиентом и фасадной службой  
 На пути обмена данными между клиентом и фасадной службой используется привязка `wsHttpBinding` и тип учетных данных клиента `UserName` . Это означает, что фасадная служба проверяет подлинность клиента по имени пользователя и паролю, а клиент проверяет подлинность фасадной службы с помощью сертификата X.509. Конфигурация привязки выглядит следующим образом.  
  
```xml  
<bindings>  
  <wsHttpBinding>  
    <binding name="Binding1">  
      <security mode="Message">  
        <message clientCredentialType="UserName"/>  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 Фасадная служба проверяет подлинность вызывающей стороны с помощью пользовательской реализации класса `UserNamePasswordValidator` . Для простоты примера проверка подлинности проверяет только соответствие имени пользователя представленному паролю. На практике проверка подлинности пользователя обычно выполняется с помощью Active Directory или пользовательского поставщика членства ASP.NET. Код, реализующий проверку подлинности, находится в файле `FacadeService.cs` .  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // check that username matches password  
        if (null == userName || userName != password)  
        {  
            Console.WriteLine("Invalid username or password");  
            throw new SecurityTokenValidationException(  
                       "Invalid username or password");  
        }  
    }  
}  
```  
  
 Пользовательский модуль проверки настроен для использования в рамках поведения `serviceCredentials` в файле конфигурации фасадной службы. Это поведение также используется для настройки сертификата X.509 службы.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="FacadeServiceBehavior">  
      <!--The serviceCredentials behavior allows you to define -->  
      <!--a service certificate. -->  
      <!--A service certificate is used by the service to  -->  
      <!--authenticate itself to its clients and to provide  -->  
      <!--message protection. -->  
      <!--This configuration references the "localhost"  -->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate   
               findValue="localhost"   
               storeLocation="LocalMachine"   
               storeName="My"   
               x509FindType="FindBySubjectName" />  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
            customUserNamePasswordValidatorType=  
           "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,  
            FacadeService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
### <a name="communication-path-between-faade-service-and-backend-service"></a>Путь обмена данными между фасадной службой и серверной службой  
 На пути обмена данными между фасадной службой и серверной службой используется привязка `customBinding` , включающая в себя несколько элементов привязки. Эта привязка выполняет две задачи. Она проверяет подлинность фасадной службы и серверной службы, обеспечивая безопасность связи и надежность источника данных. Кроме того, она передает удостоверение изначальной вызывающей стороны в маркере безопасности `Username` . В этом случае серверной службе передается только имя пользователя изначальной вызывающей стороны (пароль не указывается в сообщении). Это обуславливается тем, что серверная служба доверяет фасадной службе проверку подлинности вызывающей стороны, выполняемую перед отправкой запроса. Поскольку серверная служба проверяет подлинность фасадной службы, она доверяет информации, содержащейся в переданном от нее запросе.  
  
 Ниже приведена конфигурация привязки для этого пути обмена данными.  
  
```xml  
<bindings>  
  <customBinding>  
    <binding name="ClientBinding">  
      <security authenticationMode="UserNameOverTransport"/>  
      <windowsStreamSecurity/>  
      <tcpTransport/>  
    </binding>  
  </customBinding>  
</bindings>  
```  
  
 [ \<Безопасности >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) берет на себя передачу имени пользователя изначальной вызывающей стороны и извлечение элемента привязки. [ \<Windowsstreamsecurity инициирует >](../../../../docs/framework/configure-apps/file-schema/wcf/windowsstreamsecurity.md) и [ \<tcpTransport >](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) обеспечения проверки подлинности фасадной и серверной служб, а также защиту сообщений.  
  
 Для передачи запроса необходимо реализовать в фасадной службе возможность передачи имени пользователя изначальной вызывающей стороны, чтобы инфраструктура безопасности [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] могла добавить его в передаваемое сообщение. Фасадная служба предоставляет имя пользователя изначальной вызывающей стороны в виде значения свойства `ClientCredentials` экземпляра клиентского прокси-класса, используемого для обмена информацией между фасадной и серверной службами.  
  
 В следующем примере кода показана реализация метода `GetCallerIdentity` фасадной службы. В прочих методах используются аналогичные принципы.  
  
```  
public string GetCallerIdentity()  
{  
    CalculatorClient client = new CalculatorClient();  
    client.ClientCredentials.UserName.UserName = ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    string result = client.GetCallerIdentity();  
    client.Close();  
    return result;  
}  
```  
  
 Как показано в предыдущем примере кода, в свойстве `ClientCredentials` не задается пароль (в нем содержится только имя пользователя). Инфраструктура безопасности[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] в этом случае создает токен безопасности без пароля, что и требуется в этом сценарии.  
  
 В серверной службе должна быть проверена подлинность информации, содержащейся в маркере безопасности. По умолчанию инфраструктура безопасности [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] пытается сопоставить пользователя с учетной записью Windows, используя предоставленный пароль. В данном случае пароль не предоставляется, и серверной службе не требуется проверять имя пользователя, поскольку эта процедура уже выполнена фасадной службой. Для реализации этой функции в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]предоставляется пользовательский класс `UserNamePasswordValidator` , обеспечивающий принудительное требование о том, чтобы в маркере было указано имя пользователя, и не выполняющий дополнительную проверку подлинности.  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // Ignore the password because it is empty,   
        // we trust the facade service to authenticate the client.  
        // Accept the username information here so that the   
        // application gets access to it.  
        if (null == userName)  
        {  
            Console.WriteLine("Invalid username");  
            throw new   
             SecurityTokenValidationException("Invalid username");  
        }  
    }  
}  
```  
  
 Пользовательский модуль проверки настроен для использования в рамках поведения `serviceCredentials` в файле конфигурации фасадной службы.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="BackendServiceBehavior">  
      <serviceCredentials>  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
           customUserNamePasswordValidatorType=  
          "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,   
           BackendService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Для извлечения имени пользователя и информации об учетной записи доверенной фасадной службы в серверной службе реализован класс `ServiceSecurityContext` . В следующем примере кода показана реализация метода `GetCallerIdentity` .  
  
```  
public string GetCallerIdentity()  
{  
    // Facade service is authenticated using Windows authentication.  
    //Its identity is accessible.  
    // On ServiceSecurityContext.Current.WindowsIdentity.  
    string facadeServiceIdentityName =   
          ServiceSecurityContext.Current.WindowsIdentity.Name;  
  
    // The client name is transmitted using Username authentication on   
    //the message level without the password  
    // using a supporting encrypted UserNameToken.  
    // Claims extracted from this supporting token are available in   
    // ServiceSecurityContext.Current.AuthorizationContext.ClaimSets   
    // collection.  
    string clientName = null;  
    foreach (ClaimSet claimSet in   
        ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
    {  
        foreach (Claim claim in claimSet)  
        {  
            if (claim.ClaimType == ClaimTypes.Name &&   
                                   claim.Right == Rights.Identity)  
            {  
                clientName = (string)claim.Resource;  
                break;  
            }  
        }  
    }  
    if (clientName == null)  
    {  
        // In case there was no UserNameToken attached to the request.  
        // In the real world implementation the service should reject   
        // this request.  
        return "Anonymous caller via " + facadeServiceIdentityName;  
    }  
  
    return clientName + " via " + facadeServiceIdentityName;  
}  
```  
  
 Информация об учетной записи фасадной службы извлекается с помощью свойства `ServiceSecurityContext.Current.WindowsIdentity` . Для доступа к информации об изначальной вызывающей стороне серверная служба использует свойство `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` . Она выполняет поиск утверждения `Identity` , принадлежащего к типу `Name`. Это утверждение автоматически создается инфраструктурой безопасности [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] из информации, содержащейся в маркере безопасности `Username` .  
  
## <a name="running-the-sample"></a>Выполнение образца  
 При выполнении примера запросы и ответы операций отображаются в окне консоли клиента. Чтобы закрыть клиент, нажмите клавишу ВВОД в окне клиента. Можно нажать клавишу ВВОД в окнах консолей фасадной и серверной служб, чтобы закрыть их.  
  
```  
Username authentication required.  
Provide a valid machine or domain ac  
   Enter username:  
user  
   Enter password:  
****  
user via MyMachine\testaccount  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 В состав образца сценария, где используется доверенная фасадная служба, входит пакетный файл Setup.bat, позволяющий настроить для сервера соответствующий сертификат для запуска фасадной службы, необходимый для проверки ее подлинности клиентом. Подробные сведения см. в описании процедуры настройки в конце этого раздела.  
  
 Ниже приводится краткое описание различных разделов пакетного файла.  
  
-   Создание сертификата сервера.  
  
     Следующие строки из файла Setup.bat создают используемый в дальнейшем сертификат сервера.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     В переменной `%SERVER_NAME%` указывается имя сервера. Значение по умолчанию - localhost. Сертификат хранится в хранилище LocalMachine.  
  
-   Установка сертификата фасадной службы в хранилище доверенных сертификатов клиента.  
  
     Следующая строка копирует сертификат фасадной службы в хранилище доверенных лиц клиента. Этот шаг является обязательным, поскольку сертификаты, созданные с помощью программы Makecert.exe, не получают неявного доверия со стороны клиентской системы. Если уже имеется сертификат, имеющий доверенный корневой сертификат клиента, например сертификат, выпущенный корпорацией Майкрософт, выполнять этот шаг по добавлению сертификата сервера в хранилище сертификатов клиента не требуется.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1.  Убедитесь, что вы выполнили [выполняемая однократно процедура настройки для образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Чтобы создать выпуск решения на языке C# или Visual Basic .NET, следуйте инструкциям в разделе [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
#### <a name="to-run-the-sample-on-the-same-machine"></a>Запуск образца на том же компьютере  
  
1.  Убедитесь, что путь включает папку, в которой хранится файл Makecert.exe.  
  
2.  Запустите файл Setup.bat из папки установки примера. При этом устанавливаются все сертификаты, необходимые для выполнения образца.  
  
3.  Запустите программу BackendService.exe из каталога \BackendService\bin в отдельном окне консоли.  
  
4.  Запустите программу FacadeService.exe из каталога \FacadeService\bin в отдельном окне консоли.  
  
5.  Запустите программу Client.exe из каталога \client\bin. Действия клиента отображаются в консольном приложении клиента.  
  
6.  Если клиенту и службе не удается взаимодействовать, см. раздел [советы по устранению неполадок](http://msdn.microsoft.com/library/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### <a name="to-clean-up-after-the-sample"></a>Очистка после образца  
  
1.  После завершения работы примера запустите в папке примеров файл Cleanup.bat.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Примеры Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все примеры [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\TrustedFacade`  
  
## <a name="see-also"></a>См. также
