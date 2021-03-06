---
title: "Сведения о развертывании (Entity Framework)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a847a22-4eb8-4565-b18b-453bbca070db
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: d38f90822746c08d576879ab35fa0984e439640b
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="deployment-considerations-entity-framework"></a>Сведения о развертывании (Entity Framework)
В этом разделе представлены сведения о развертывании приложений, использующих для доступа к данным платформу ADO.NET Entity Framework. Дополнительные сведения о платформе Entity Framework см. в разделе [Приступая к работе](../../../../../docs/framework/data/adonet/ef/getting-started.md).  
  
 Платформа Entity Framework предоставляет набор средств, интегрирующихся в среду Visual Studio и облегчающих разработку в ней. Дополнительные сведения см. в разделе [ADO.NET Entity Data Model Tools](http://msdn.microsoft.com/library/91076853-0881-421b-837a-f582f36be527). В этом разделе не описано использование специальных технологий для развертывания приложений, созданных на базе Entity Framework.  
  
 Среда Visual Studio предоставляет функции распространения и развертывания приложений, например функцию развертывания ClickOnce. Дополнительные сведения см. в разделе [развертывание приложений и компонентов](/visualstudio/deployment/deploying-applications-services-and-components) в документации по Visual Studio.  
  
 При развертывании приложения, использующего платформу Entity Framework, следует принимать во внимание следующие соображения.  
  
-   Entity Framework является компонентом платформы .NET Framework, начиная с .NET Framework 3.5 с пакетом обновления 1 (SP1). При развертывании приложения, использующего платформу Entity Framework, необходимо убедиться, что установлена платформа .NET Framework 3.5 с пакетом обновления 1 (SP1) или более поздняя версия.  
  
-   При создании концептуальной модели с использованием мастера модели EDM в файле конфигурации приложения создается строка подключения. Файлы модели и сопоставления могут быть внедрены в качестве ресурсов приложения или скопированы в выходной каталог. По умолчанию эти файлы развертываются в качестве внедренных ресурсов приложения. Свойство `Metadata Artifact Processing` файла конструктора сущностей используется для выбора одного из этих параметров. Дополнительные сведения см. в разделе [как: копирование модели и сопоставления файлов в выходной каталог](http://msdn.microsoft.com/library/e2c9820f-1705-457e-9fdb-8b289f3179b4).  
  
-   Убедитесь, что сведения о модели и сопоставлениях, выраженные на языке определения концептуальных схем (язык CSDL), языке определения схемы хранения (язык SSDL) и языке определения сопоставлений (язык MSL) развернуты совместно с приложением и находятся в каталоге, заданном в строке соединения. Дополнительные сведения см. в статье [Connection Strings](../../../../../docs/framework/data/adonet/ef/connection-strings.md) (Строки подключения).  
  
-   Если производится внедрение сведений о модели и сопоставлениях в качестве ресурсов приложения, то приложение нужно перекомпилировать и повторно разворачивать каждый раз при обновлении концептуальной модели.  
  
-   Поскольку Entity Framework является компонентом платформы .NET Framework, она может распространяться вместе с приложением в соответствии с условиями лицензионного соглашения для платформы .NET Framework.  
  
## <a name="see-also"></a>См. также  
 [ADO.NET Entity Framework](../../../../../docs/framework/data/adonet/ef/index.md)  
 [Вопросы разработки и развертывания](../../../../../docs/framework/data/adonet/ef/development-and-deployment-considerations.md)
