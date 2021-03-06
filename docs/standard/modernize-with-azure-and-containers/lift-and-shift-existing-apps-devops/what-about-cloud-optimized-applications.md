---
title: "Как насчет оптимизированную для облачных приложений?"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Как насчет оптимизированную для облачных приложений?"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/26/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: adcb9d2352022cc94238296562b3eb7677bdf20b
ms.sourcegitcommit: c3957fdb990060559d73cca44ab3e2c7b4d049c0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2018
---
# <a name="what-about-cloud-optimized-applications"></a>Как насчет оптимизированную для облачных приложений?

Несмотря на то, что оптимизированными для облака и [облако в собственном коде](https://www.gartner.com/doc/3738117/comparing-leading-cloudnative-application-platforms) приложения не является основной задачей данного руководства полезно иметь представление об этом уровне зрелости модернизацию и чтобы отличать его от DevOps готовую для облачных.

Рис. 4-3 помещает оптимизированную для облачных приложений в уровнями зрелости модернизацию приложения:

![Позиционирование оптимизированную для облачных приложений](./media/image3.png)

> **Рис. 4-3.** Позиционирование оптимизированную для облачных приложений

Уровень зрелости модернизацию оптимизированными для облака обычно требуется новые системы разработки. Перемещение уровень оптимизированными для облака обычно определяется необходимого при модернизации приложений, насколько возможно, для снижения затрат и повышения гибкости и конкурируют преимущества. Эти задачи выполняются посредством максимального использования облачных PaaS. Это означает, что не только с помощью служб PaaS, как DBaaS, CaaS и хранилище службы (STaaS), а также путем переноса приложений и служб в PaaS вычислений платформы как службы приложений Azure, или orchestrators.

Этот тип модернизацию обычно требует рефакторинга или написание нового кода, который оптимизирован для облачных платформах PaaS (как для службы приложений Azure). Он может потребоваться даже архитектуры специально для облачной среде, особенно в том случае, если вы переходите к моделям собственный облачных приложений, основанных на микрослужбами. Это ключ, по сравнению с DevOps готовую для облачных, требующий не изменять архитектуру и новый код не отличительный признак.

В некоторых более сложных случаях можно создать [облако в собственном коде](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications) приложений на основе архитектуры микрослужбами, которым может развиваться с гибкость и масштабировать ограничений, которые будет трудно добиться в объединенный архитектуры для развернуть в локальной среде.

Рис. 4-4 показывает тип приложений, которые можно развернуть при использовании модели оптимизированными для облака. У вас есть два основных вариантов — современный веб-приложений и приложений облако в собственном коде.

> ![Типы приложений на уровне оптимизированными для облака](./media/image4.png)
>
> **Рис. 4-4.** Типы приложений на уровне оптимизированными для облака

Основные современных веб-приложений и облако в собственном коде приложения можно расширить, добавив другими службами, такими как искусственный интеллект (AI), машинное обучение (ML) и IoT. Можно использовать любой из этих служб для расширения любого из возможных подходов, оптимизированными для облака.

Фундаментальное различие в приложениях на уровне оптимизированными для облака — в архитектуре приложения. [Облако в собственном коде](https://www.gartner.com/doc/3738117/comparing-leading-cloudnative-application-platforms) приложения, по определению, приложениями, которые основаны на микрослужбами. Облако в собственном коде приложения требуют специальных архитектур, технологий и платформ, по сравнению с монолитные веб-приложения или традиционные N-уровневого приложения.

Создание новых приложений, которые не используют микрослужбами также имеет смысл. Существует множество сценариев новые и по-прежнему современных, в которых подход на основе микрослужбами может превысить вашим потребностям. В некоторых случаях может просто хотите создать проще монолитные веб-приложения или добавление недетализированного служб в N-уровневого приложения. В таких случаях можно выполнять полностью использовать возможности облака PaaS возможности, такие как те, предлагаемые службой приложения Azure. Вы по-прежнему сократить обслуживания работу до предела.

Кроме того так как создавать новый код в оптимизированную для облачных сценариев (для всего приложения или для частичного подсистем), при создании нового кода следует использовать более новые версии .NET ([.NET Core](../../../core/index.md) и [ASP.NET Core](/aspnet/core/), в частности). Это особенно важно, если так, как .NET Core — это платформа компактного и быстрого создания микрослужбами и контейнеры. Вы сможете получить небольшой объем памяти и быстрый запуск в контейнерах, и приложения будут повышению производительности. Такой подход вполне соответствует с различными требованиями к микрослужбами и контейнеры, и вы получаете преимущества кросс платформенных framework настоящее может запустить то же приложение на Mac (Mac для сред разработки), Windows Server и Linux.

## <a name="cloud-native-applications-with-cloud-optimized-applications"></a>Облако в собственном коде приложения с приложениями, оптимизированными для облака

[Облако в собственном коде](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications) — более расширенные или зрелой состояние больших и критически важных приложений. Облако в собственном коде приложений обычно требуют архитектуры и проектирования, созданные с нуля, а не модернизация существующих приложений. Ключевое различие между приложением облако в собственном коде и проще, оптимизированными для облака веб-приложения развернут PaaS является рекомендацию, чтобы использовать архитектурах микрослужбами подход облако в собственном коде. Оптимизированную для облачных приложений также может быть монолитные веб-приложения и N-уровневого приложения, развернутые облачные службы PaaS, например службы приложений Azure.

[12-фактора приложения](https://12factor.net/) (коллекция шаблонов, которые тесно связаны с подходами микрослужбами) также считается обязательным для [облако в собственном коде](https://www.gartner.com/doc/3738117/comparing-leading-cloudnative-application-platforms) архитектур приложений.

[Облаке собственный Foundation вычислений (CNCF)](https://www.cncf.io/) является основной активатором принципов облако в собственном коде. Корпорация Майкрософт [членом CNCF](https://azure.microsoft.com/blog/announcing-cncf/).

Пример определения и Дополнительные сведения о характеристиках собственный облачных приложений, см. в статье Gartner [как спроектировать и разработать собственный облачных приложений](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications). Руководство корпорации Майкрософт о том, как реализовать приложение облако в собственном коде см. в разделе [микрослужбами .NET: архитектура для приложений .NET в контейнерах](https://aka.ms/microservicesebook).

Наиболее важным вопросом при переносе всего приложения для [облако в собственном коде](https://www.gartner.com/doc/3738117/comparing-leading-cloudnative-application-platforms) модель является, необходимо повторно сконструировать для микрослужбами-архитектурой. Это требует значительных вложений в разработку из-за больших рефакторинга процесс. Этот параметр обычно выбирается для критически важных приложений, требующих новые уровни масштабируемости и гибкости долгосрочной. Однако можно начать перемещение сторону облако в собственном коде, добавив микрослужбами для всего несколько новых сценариев и в конечном итоге рефакторинга приложения полностью как микрослужбами. Это инкрементальный подход, который в наибольшей степени подходит для некоторых сценариев.

## <a name="what-about-microservices"></a>Как насчет микрослужбами? 

Важно понимать микрослужбами и принципы их работы, если вы принимаете собственный облачных приложений для вашей организации.

Архитектура микрослужбами — усовершенствованный подход, который можно использовать для приложений, которые создаются с нуля, либо когда развивать существующие приложения (локальные или облачные приложения готовы к использованию DevOps) к собственный облачных приложений. Можно запустить, добавив несколько микрослужбами в существующие приложения, чтобы узнать о новых парадигм микрослужбами. Но очевидно, архитектор и кода, особенно для этого типа архитектурный подход.

Однако микрослужбами не являются обязательными для любых новых или современных приложений. Микрослужбами не «bullet magic», и они не лучший способ создания каждого приложения. Как и при использовании микрослужбами зависит от типа приложения, которое необходимо создать.

Архитектура микрослужбами становится предпочтительным подходом для распределенных и больших или сложных критически важных приложений, основанных на несколько независимых подсистемах в виде автономной службы. В микрослужбами архитектуры построен набор служб, которые могут быть независимо друг от друга разработки, тестирования, с версиями, развертывания и масштабирования приложения. Это может быть любой связанные, автономные базы данных на микрослужбы.

Подробное рассмотрение архитектуры микрослужбами, который можно реализовать с помощью .NET Core. в разделе загружаемые PDF электронной книги [микрослужбами .NET: архитектура для приложений .NET в контейнерах](https://aka.ms/microservicesebook). Руководство также доступно [online](../../microservices-architecture/index.md).

Но даже в случаях, в которых микрослужбами предоставляют мощные возможности независимых развертывания, границы строгого подсистемы и разнообразие технологии-они также создают много новых задач. Проблемы связаны с разработки распределенных приложений, например фрагментации и независимых моделях данных; Достижение устойчивым обмен данными между микрослужбами; потребность в окончательной согласованности; и сложности. Микрослужбами ввести более высокий уровень сложности, по сравнению с традиционными приложениями монолитные.

Из-за сложности архитектуры микрослужбами только конкретных сценариев и некоторые типы приложений, подходят для приложений на основе микрослужбу. К ним относятся больших и сложных приложений с несколькими развивается подсистем. В таких случаях стоит инвестиции в более сложных архитектура программного обеспечения для повысить долгосрочной гибкость и эффективность обслуживания приложения. Но для более сложных сценариев рекомендуется продолжать работу с подход монолитные приложения или проще N-уровневые приближается.

Последнее замечание, несмотря на риск повторяющихся о трудностях, из которых не следует рассмотреть использование микрослужбами в приложениях как «файловый или nothing вообще*.*» Можно расширить и развивать существующие монолитные приложения путем добавления новых, небольших сценариев, основанных на микрослужбами. Нет необходимости начинать с нуля, чтобы приступить к работе с микрослужбами архитектурного подхода. На самом деле мы рекомендуем развитие с помощью существующего монолитные или N-уровневого приложения путем добавления новых сценариев. В конце концов можно разбить приложение в автономные компоненты или микрослужбами. Вы можете запустить развивается монолитные приложения в направлении микрослужбами, шаг за шагом.

## <a name="when-to-use-azure-app-service-for-modernizing-existing-net-apps"></a>Когда использовать службу приложений Azure для модернизация существующих приложений .NET

Когда вы модернизировать существующие веб-приложения ASP.NET на уровне зрелости, оптимизированными для облака, так как веб-приложений, разработанных с помощью .NET Framework, основных зависимостей, в Windows и, скорее всего, Internet Information Server (IIS). Можно использовать и развертывать приложения на основе Windows и на базе IIS либо путем непосредственного развертывания для [службе приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) или по первому containerizing приложения с помощью контейнеров Windows. Если containerizing, развертывание приложений либо к контейнерам Windows размещает (на основе виртуальных Машин) или кластера, поддерживающих эту технологию контейнеров Windows Azure Service Fabric.

При использовании контейнеров Windows, вы получаете все преимущества создание контейнеров. Повышают гибкость в доставки и развертывания приложения и сократить трения для среды проблемах (промежуточного хранения, разработки и тестирования, производство). В следующих разделах мы более подробно о преимуществах, которые можно получить с помощью контейнеров.

На момент написания данного руководства, в службе приложений Azure не поддерживает контейнеры Windows. Он поддерживает контейнеры для Linux. Поэтому может иметь следующий вопрос, «Как сделать выбор между службы приложений Azure и контейнеров Windows?»

По сути Если службе приложений Azure работает для приложения и нет ни один сервер пользовательских зависимостей блокировки путь для использования службы приложений, необходимо перенести существующее веб-приложение для .NET для служб приложений. Это простой, наиболее эффективный способ поддержания приложения. В Azure приложение также будет иметь простой путь обслуживания из-за преимуществ от инфраструктуры PaaS, такие как DBaaS, CaaS и STaaS.

Тем не менее если приложение имеет сервера или пользовательских зависимостей, которые не поддерживаются в службе приложений Azure, может потребоваться рассмотреть варианты, основанные на доступ к контейнерам Windows. Сервер или пользовательских зависимостей примеры стороннего программного обеспечения или MSI-файл, который должен быть установлен на сервере, но которые не поддерживаются в службе приложений Azure. Еще один пример — другие конфигурации сервера, который не поддерживается в службе приложений Azure, как с помощью сборок в глобальный кэш сборок (GAC) или COM-компоненты COM +. Благодаря образы контейнеров Windows можно включить пользовательские зависимостей в ту же «единицу развертывания.»

Кроме того можно переработать области приложения, которые не поддерживаются службой приложений Azure. В зависимости от объема работы рефакторинг требуется, необходимо тщательно оценить, выполнен ли, имеет смысл.

### <a name="benefits-of-moving-to-azure-app-service"></a>Преимущества перехода на службе приложений Azure

Служба приложений Azure — это полностью управляемая PaaS, которое позволяет легко создавать веб-приложений, которые архивируются бизнес-процессов. При использовании службы приложений, можно избежать затрат инфраструктуры управления, связанных с обновление и обслуживание веб приложения в локальной среде. В частности Вырезать оборудования и стоимости лицензирования веб приложения в локальной среде выполнения.

Если веб-приложения подходит для миграции на службы приложений Azure, главным преимуществом является короткого времени, затрачиваемого на перемещение приложения. Службы приложений предлагает очень легко среду, в которой приступить к работе.

Служба приложений Azure отлично подходит для большинства веб-приложений, так как он является простейшим PaaS в Azure, можно использовать для запуска веб-приложений. Развертывание и управление ими интегрированы в платформу и сайты быстро масштабирования для обработки трафика высокой нагрузки диспетчера трафика и балансировки нагрузки встроенных обеспечения высокого уровня доступности.

Даже наблюдение за веб-приложения является простой через Azure Application Insights. Application Insights поставляется бесплатно с службы приложений и не требует написания специальных кода в приложении. Просто запустить веб-приложения в службе приложений, и вы сможете получить привлекательные система мониторинга, без дополнительных действий.

В службе приложений много приложений с открытым исходным кодом можно использовать также непосредственно из коллекции веб-приложений Azure (например WordPress или Umbraco), или можно создать новый сайт с помощью framework и средств по своему усмотрению, такие как ASP.NET. Компонент веб-заданий для приложения службы позволяет легко добавить фоновое задание обработки для веб-приложения служб приложений.

Следующие ключевые преимущества Миграция веб-приложения с помощью функции веб-приложениях службы приложений Azure.

-   Автоматическое масштабирование для удовлетворения спроса при большой загрузке и сократить затраты на скрытый периоды.

-   Автоматическое создание резервных копий для защиты изменений и данных.

-   Высокий уровень доступности и устойчивости на платформе Azure PaaS.

-   Слоты развертывания для разработки и промежуточные среды, а также для тестирования нескольких устройств сайтов.

-   Балансировка нагрузки и защиты распределенных отказ в обслуживании (DDoS).

-   Управление трафиком для направления пользователей на ближайший географической развертывания.

Хотя службы приложений может быть лучшим вариантом для нового веб-приложений, однако для существующих приложений службы приложений может оказаться лучшим вариантом только в том случае, если поддерживается зависимостей приложения в службе приложений.

### <a name="additional-resources"></a>Дополнительные ресурсы

-   **Анализ совместимости для службы приложений Azure**  
[https://www.migratetoazure.net/Resources](https://www.migratetoazure.net/Resources)


### <a name="benefits-of-moving-to-windows-containers"></a>Преимущества перехода к контейнерам Windows

Основным преимуществом использования контейнеров Windows, является более надежным и улучшенный режим развертывания, по сравнению с не контейнерных приложений. Кроме того приложения эффективно модернизированный с контейнерами и делает ваше приложение готово для многих платформ и облака, которые поддерживают контейнеров Windows. В следующих разделах более подробно рассматриваются преимущества перехода к контейнерам Windows.

Среды основной вычислений в Azure (общедоступная, начиная с mid 2017 г.), поддерживающие контейнеры Windows, Azure Service Fabric и базовые контейнеры Windows узлов (2016 виртуальных машин Windows Server). Эти среды являются сценариев основной инфраструктуры, описанные в этом руководстве.

Также можно развернуть контейнеры Windows на другие orchestrators как Kubernetes помощью Docker Swarm и контроллера домена/OS. В настоящее время (раннее попадают 2017 г.), эти платформы находитесь в режиме предварительного просмотра в службе контейнера Azure с использованием контейнеров Windows.

>[!div class="step-by-step"]
[Назад](microsoft-technologies-in-cloud-devops-ready-applications.md)
[Вперед](how-to-deploy-existing-net-apps-to-azure-app-service.md)
