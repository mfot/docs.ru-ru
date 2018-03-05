---
title: "Анализатор .NET API"
description: "Узнайте, как анализатор .NET API помогает выявлять устаревшие интерфейсы API и проблемы с совместимостью платформ."
author: oliag
ms.author: mairaw
ms.date: 01/30/2018
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.openlocfilehash: 81ab7e32b2af6048d822243226f1054ebd1ca419
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="net-api-analyzer"></a><span data-ttu-id="c623c-103">Анализатор .NET API</span><span class="sxs-lookup"><span data-stu-id="c623c-103">.NET API analyzer</span></span>

<span data-ttu-id="c623c-104">Анализатор API .NET, созданный на платформе Roslyn, выявляет риски совместимости для API на языке C# на разных платформах, а также отслеживает вызовы устаревших интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="c623c-104">The .NET API Analyzer is a Roslyn analyzer that discovers potential compatibility risks for C# APIs on different platforms and detects calls to deprecated APIs.</span></span> <span data-ttu-id="c623c-105">Разработчики C# могут применять его на любом этапе разработки.</span><span class="sxs-lookup"><span data-stu-id="c623c-105">It can be useful for all C# developers at any stage of development.</span></span>

<span data-ttu-id="c623c-106">Анализатор API поставляется в виде пакета NuGet [Microsoft.DotNet.Analyzers.Compatibility](https://www.nuget.org/packages/Microsoft.DotNet.Analyzers.Compatibility/).</span><span class="sxs-lookup"><span data-stu-id="c623c-106">API Analyzer comes as a NuGet package [Microsoft.DotNet.Analyzers.Compatibility](https://www.nuget.org/packages/Microsoft.DotNet.Analyzers.Compatibility/).</span></span> <span data-ttu-id="c623c-107">Как только вы добавите в проект ссылку на анализатор, он автоматически начнет отслеживать код и извещать о проблемах с использованием API.</span><span class="sxs-lookup"><span data-stu-id="c623c-107">After you reference it in a project, it automatically monitors the code and indicates problematic API usage.</span></span> <span data-ttu-id="c623c-108">Щелкнув значок лампочки, вы получите предложения по возможным мерам для исправления ситуации.</span><span class="sxs-lookup"><span data-stu-id="c623c-108">You can also get suggestions on possible fixes by clicking on the light bulb.</span></span> <span data-ttu-id="c623c-109">Также в раскрывающееся меню есть пункт для скрытия предупреждений.</span><span class="sxs-lookup"><span data-stu-id="c623c-109">The drop-down menu includes an option to suppress the warnings.</span></span>

> [!NOTE]
> <span data-ttu-id="c623c-110">Анализатор .NET API пока доступен в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c623c-110">The .NET API analyzer is still a pre-release version.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c623c-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c623c-111">Prerequisites</span></span>

* <span data-ttu-id="c623c-112">Visual Studio 2017 или Visual Studio для Mac (любые версии).</span><span class="sxs-lookup"><span data-stu-id="c623c-112">Visual Studio 2017 or Visual Studio for Mac (all versions).</span></span>

## <a name="discovering-deprecated-apis"></a><span data-ttu-id="c623c-113">Обнаружение устаревших API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="c623c-113">Discovering deprecated APIs</span></span>

### <a name="what-are-deprecated-apis"></a><span data-ttu-id="c623c-114">Что такое устаревшие API-интерфейсы?</span><span class="sxs-lookup"><span data-stu-id="c623c-114">What are deprecated APIs?</span></span>

<span data-ttu-id="c623c-115">Семейство .NET включает несколько крупных программных продуктов, которые постоянно обновляются, чтобы лучше соответствовать потребностям клиентов.</span><span class="sxs-lookup"><span data-stu-id="c623c-115">The .NET family is a set of large products that are constantly upgraded to better serve customer needs.</span></span> <span data-ttu-id="c623c-116">Вполне логично, что некоторые API устаревают и заменяются новыми.</span><span class="sxs-lookup"><span data-stu-id="c623c-116">It's natural to deprecate some APIs and replace them with new ones.</span></span> <span data-ttu-id="c623c-117">API считается устаревшим, если существует более современный вариант.</span><span class="sxs-lookup"><span data-stu-id="c623c-117">An API is considered deprecated when a better alternative exists.</span></span> <span data-ttu-id="c623c-118">Атрибут <xref:System.ObsoleteAttribute> в API оповещает о том, что этот интерфейс устарел и его не следует использовать.</span><span class="sxs-lookup"><span data-stu-id="c623c-118">One way to inform that an API is deprecated and shouldn't be used is to mark it with the <xref:System.ObsoleteAttribute> attribute.</span></span> <span data-ttu-id="c623c-119">У этого подхода есть недостаток — для всех устаревших API применяется только один диагностический идентификатор ([CS0612](../../csharp/misc/cs0612.md) в C#).</span><span class="sxs-lookup"><span data-stu-id="c623c-119">The disadvantage of this approach is that there is only one diagnostic ID for all obsolete APIs (for C#, [CS0612](../../csharp/misc/cs0612.md)).</span></span> <span data-ttu-id="c623c-120">Это означает следующее.</span><span class="sxs-lookup"><span data-stu-id="c623c-120">This means that:</span></span>
- <span data-ttu-id="c623c-121">Нет возможности создать отдельные документы для каждого случая.</span><span class="sxs-lookup"><span data-stu-id="c623c-121">It's impossible to have dedicated documents for each case.</span></span>
- <span data-ttu-id="c623c-122">Нет возможности отключить предупреждения определенной категории.</span><span class="sxs-lookup"><span data-stu-id="c623c-122">It's impossible to suppress certain category of warnings.</span></span> <span data-ttu-id="c623c-123">Вы сможете только отключить все предупреждения или разрешить все сразу.</span><span class="sxs-lookup"><span data-stu-id="c623c-123">You can suppress either all or none of them.</span></span>
- <span data-ttu-id="c623c-124">Чтобы известить пользователей об устаревании интерфейсов, необходимо обновить используемую сборку или целевой пакет.</span><span class="sxs-lookup"><span data-stu-id="c623c-124">To inform users of a new deprecation, a referenced assembly or targeting package has to be updated.</span></span>

<span data-ttu-id="c623c-125">Анализатор API применяет коды ошибок с индексом DE (Deprecation Error, ошибка устаревания), характерные для конкретных API-интерфейсов, чтобы управлять отображением индивидуальных предупреждений.</span><span class="sxs-lookup"><span data-stu-id="c623c-125">The API Analyzer uses API-specific error codes that begin with DE (which stands for Deprecation Error), which allows control over the display of individual warnings.</span></span> <span data-ttu-id="c623c-126">Устаревшие API, обнаруживаемые анализатором, определяются в репозитории [dotnet/platform-compat](https://github.com/dotnet/platform-compat).</span><span class="sxs-lookup"><span data-stu-id="c623c-126">The deprecated APIs identified by the analyzer are defined in the [dotnet/platform-compat](https://github.com/dotnet/platform-compat) repo.</span></span>

### <a name="using-the-api-analyzer"></a><span data-ttu-id="c623c-127">Использование анализатора API</span><span class="sxs-lookup"><span data-stu-id="c623c-127">Using the API Analyzer</span></span>

<span data-ttu-id="c623c-128">Если в коде используется устаревший API-интерфейс, например <xref:System.Net.WebClient>, анализатор API выделяет его зеленой волнистой линией.</span><span class="sxs-lookup"><span data-stu-id="c623c-128">When a deprecated API, such as <xref:System.Net.WebClient>, is used in a code, API Analyzer highlights it with a green squiggly line.</span></span> <span data-ttu-id="c623c-129">Когда вы наведете указатель мыши на вызов этого API, отобразится значок лампочки со сведениями об устаревании API, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c623c-129">When you hover over the API call, a light bulb is displayed with information about the API deprecation, as in the following example:</span></span>

![Снимок экрана API-интерфейса WebClient с зеленой волнистой линией и лампочкой слева](media/api-analyzer/green-squiggle.jpg)

<span data-ttu-id="c623c-131">Окно **Список ошибок** содержит предупреждения с уникальным идентификатором для каждого устаревшего API-интерфейса, как показано в следующем примере (`DE004`):</span><span class="sxs-lookup"><span data-stu-id="c623c-131">The **Error List** window contains warnings with a unique ID per deprecated API, as shown in the following example (`DE004`):</span></span> 

![Снимок экрана с окном списка ошибок, где отображаются идентификатор и описание предупреждения](media/api-analyzer/warnings.jpg)

<span data-ttu-id="c623c-133">Щелкнув этот идентификатор, вы перейдите на веб-страницу с подробными сведениями о том, почему этот API-интерфейс устарел и какие альтернативы рекомендуется использовать.</span><span class="sxs-lookup"><span data-stu-id="c623c-133">By clicking on the ID, you go to a webpage with detailed information about why the API was deprecated and suggestions regarding alternative APIs that can be used.</span></span>

<span data-ttu-id="c623c-134">Вы можете скрыть любое предупреждение, щелкнув подсвеченный элемент правой кнопкой мыши и выбрав пункт **Скрыть \<идентификатор диагностики>**.</span><span class="sxs-lookup"><span data-stu-id="c623c-134">Any warnings can be suppressed by right-clicking on the highlighted member and selecting **Suppress \<diagnostic ID>**.</span></span> <span data-ttu-id="c623c-135">Есть два способа скрыть предупреждения:</span><span class="sxs-lookup"><span data-stu-id="c623c-135">There are two ways to suppress warnings:</span></span> 

* <span data-ttu-id="c623c-136">[локально (в исходном коде)](#suppressing-warnings-locally);</span><span class="sxs-lookup"><span data-stu-id="c623c-136">[locally (in source)](#suppressing-warnings-locally)</span></span>
* <span data-ttu-id="c623c-137">[глобально (в соответствующем файле)](#suppressing-warnings-globally) — мы рекомендуем использовать этот вариант.</span><span class="sxs-lookup"><span data-stu-id="c623c-137">[globally (in a suppression file)](#suppressing-warnings-globally) - recommended</span></span>

### <a name="suppressing-warnings-locally"></a><span data-ttu-id="c623c-138">Локальное скрытие предупреждений</span><span class="sxs-lookup"><span data-stu-id="c623c-138">Suppressing warnings locally</span></span>

<span data-ttu-id="c623c-139">Чтобы скрыть предупреждения локально, щелкните нужный элемент правой кнопкой мыши и выберите **Быстрые действия и рефакторинг** > **Скрыть *идентификатор диагностики*\<идентификатор диагностики>** > **в исходном коде**.</span><span class="sxs-lookup"><span data-stu-id="c623c-139">To suppress warnings locally, right-click on the member you want to suppress warnings for and then select **Quick Actions and Refactorings** > **Suppress *diagnostic ID*\<diagnostic ID>** > **in Source**.</span></span> <span data-ttu-id="c623c-140">Это действие добавляет в ваш исходный код директиву препроцессора [#pragma](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md) для определенной области. ![Снимок экрана с фрагментом кода, для которого #pragma отключает предупреждение](media/api-analyzer/suppress-in-source.jpg)</span><span class="sxs-lookup"><span data-stu-id="c623c-140">The [#pragma](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md) warning preprocessor directive is added to your source code in the scope defined: !["Screenshot of code framed with #pragma warning disable"](media/api-analyzer/suppress-in-source.jpg)</span></span>

### <a name="suppressing-warnings-globally"></a><span data-ttu-id="c623c-141">Глобальное скрытие предупреждений</span><span class="sxs-lookup"><span data-stu-id="c623c-141">Suppressing warnings globally</span></span>

<span data-ttu-id="c623c-142">Чтобы скрыть предупреждения глобально, щелкните нужный элемент правой кнопкой мыши и выберите **Быстрые действия и рефакторинг** > **Скрыть *идентификатор диагностики* \<идентификатор диагностики >** > **в файле с предупреждениями**.</span><span class="sxs-lookup"><span data-stu-id="c623c-142">To suppress warnings globally, right-click on the member you want to suppress warnings for and then select **Quick Actions and Refactorings** > **Suppress *diagnostic ID*\<diagnostic ID>** > **in Suppression File**.</span></span>

![Снимок экрана API-интерфейса WebClient с зеленой волнистой линией и лампочкой слева](media/api-analyzer/suppress-in-sup-file.jpg)

<span data-ttu-id="c623c-144">Когда вы настроите скрытие в первый раз, в проект будет добавлен файл *GlobalSuppressions.cs*.</span><span class="sxs-lookup"><span data-stu-id="c623c-144">A *GlobalSuppressions.cs* file is added to your project after the first suppression.</span></span> <span data-ttu-id="c623c-145">В этом файле сохраняются все новые операции глобального скрытия.</span><span class="sxs-lookup"><span data-stu-id="c623c-145">New global suppressions are appended to this file.</span></span>

![Снимок экрана API-интерфейса WebClient с зеленой волнистой линией и лампочкой слева](media/api-analyzer/suppression-file.jpg)

<span data-ttu-id="c623c-147">Мы рекомендуем использовать глобальное скрытие, чтобы гарантировать единообразие в применении API-интерфейсов в проектах.</span><span class="sxs-lookup"><span data-stu-id="c623c-147">Global suppression is the recommended way to ensure consistency of API usage across projects.</span></span>

## <a name="discovering-cross-platform-issues"></a><span data-ttu-id="c623c-148">Обнаружение проблем с межплатформенным взаимодействием</span><span class="sxs-lookup"><span data-stu-id="c623c-148">Discovering cross-platform issues</span></span>

<span data-ttu-id="c623c-149">Помимо устаревших API-интерфейсов анализатор определяет все API-интерфейсы, не поддерживающие кроссплатформенность.</span><span class="sxs-lookup"><span data-stu-id="c623c-149">Similar to deprecated APIs, the analyzer identifies all APIs that are not cross-platform.</span></span> <span data-ttu-id="c623c-150">Например, <xref:System.Console.WindowWidth?displayProperty=nameWithType> работает только в Windows, но не в Linux или macOS.</span><span class="sxs-lookup"><span data-stu-id="c623c-150">For example, <xref:System.Console.WindowWidth?displayProperty=nameWithType> works on Windows but not on Linux and macOS.</span></span> <span data-ttu-id="c623c-151">Идентификатор диагностики отображается в окне **Список ошибок**.</span><span class="sxs-lookup"><span data-stu-id="c623c-151">The diagnostic ID is shown in the **Error List** window.</span></span> <span data-ttu-id="c623c-152">Чтобы скрыть это предупреждение, щелкните его правой кнопкой мыши и выберите пункт **Быстрые действия и рефакторинг**.</span><span class="sxs-lookup"><span data-stu-id="c623c-152">You can suppress that warning by right-clicking and selecting **Quick Actions and Refactorings**.</span></span> <span data-ttu-id="c623c-153">В отличие от ситуации с устареванием, когда у вас есть два варианта (продолжать использование конкретного устаревшего элемента, скрыв предупреждение, или отказаться от его использования), здесь вы можете сразу отключить все предупреждения о тех платформах, для которых не предназначено ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="c623c-153">Unlike deprecation cases where you have two options (either keep using the deprecated member and suppress warnings or not use it at all), here if you're developing your code only for certain platforms, you can suppress all warnings for all other platforms you don't plan to run your code on.</span></span> <span data-ttu-id="c623c-154">Для этого откройте файл проекта, добавьте в него свойство `PlatformCompatIgnore` и перечислите в нем все платформы, которые следует игнорировать.</span><span class="sxs-lookup"><span data-stu-id="c623c-154">To do so, you just need to edit your project file and add the `PlatformCompatIgnore` property that lists all platforms to be ignored.</span></span> <span data-ttu-id="c623c-155">Допустимые значения: `Linux`, `MacOSX` и (или) `Windows`.</span><span class="sxs-lookup"><span data-stu-id="c623c-155">The accepted values are: `Linux`, `MacOSX`, and `Windows`.</span></span>

```xml
<PropertyGroup>
    <PlatformCompatIgnore>Linux;MacOS</PlatformCompatIgnore>
</PropertyGroup>
```

<span data-ttu-id="c623c-156">Если код предназначен для нескольких платформ, но вы хотите воспользоваться преимуществами некоторого API, который поддерживается не всеми этими платформами, вы можете отделить часть кода с помощью инструкции `if` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c623c-156">If your code targets multiple platforms and you want to take advantage of an API not supported on some of them, you can guard that part of the code with an `if` statement:</span></span>

```csharp
if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
{
     var w = Console.WindowWidth;
     // More code
}
```

<span data-ttu-id="c623c-157">Также вы можете выполнять условную компиляцию кода для целевой платформы и (или) операционной системы, но пока только [вручную](../frameworks.md#how-to-specify-target-frameworks).</span><span class="sxs-lookup"><span data-stu-id="c623c-157">You can also conditionally compile per target framework/operating system, but you currently need to do that [manually](../frameworks.md#how-to-specify-target-frameworks).</span></span>

## <a name="supported-diagnostics"></a><span data-ttu-id="c623c-158">Поддерживаемые проверки</span><span class="sxs-lookup"><span data-stu-id="c623c-158">Supported diagnostics</span></span>

<span data-ttu-id="c623c-159">Сейчас анализатор обрабатывает следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="c623c-159">Currently, the analyzer handles the following cases:</span></span>

* <span data-ttu-id="c623c-160">Использование API .NET Standard, которые создают исключение <xref:System.PlatformNotSupportedException> (PC001).</span><span class="sxs-lookup"><span data-stu-id="c623c-160">Usage of a .NET Standard API that throws <xref:System.PlatformNotSupportedException> (PC001).</span></span>
* <span data-ttu-id="c623c-161">Использование API .NET Standard, которые не поддерживаются платформой .NET Framework 4.6.1 (PC002).</span><span class="sxs-lookup"><span data-stu-id="c623c-161">Usage of a .NET Standard API that isn't available on the .NET Framework 4.6.1 (PC002).</span></span>
* <span data-ttu-id="c623c-162">Использование собственных API, которые не существуют в универсальной платформе Windows (PC003).</span><span class="sxs-lookup"><span data-stu-id="c623c-162">Usage of a native API that doesn’t exist in UWP (PC003).</span></span>
* <span data-ttu-id="c623c-163">Использование API, которые помечены как устаревшие (DEXXXX).</span><span class="sxs-lookup"><span data-stu-id="c623c-163">Usage of an API that is marked as deprecated (DEXXXX).</span></span>

## <a name="ci-machine"></a><span data-ttu-id="c623c-164">Компьютер CI</span><span class="sxs-lookup"><span data-stu-id="c623c-164">CI machine</span></span>

<span data-ttu-id="c623c-165">Все эти диагностические действия доступны не только в среде IDE, но и в командной строке при сборке проекта, в том числе для сервера CI.</span><span class="sxs-lookup"><span data-stu-id="c623c-165">All these diagnostics are available not only in the IDE, but also on the command line as part of building your project, which includes the CI server.</span></span>

## <a name="configuration"></a><span data-ttu-id="c623c-166">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="c623c-166">Configuration</span></span>

<span data-ttu-id="c623c-167">Пользователь может выбрать режим поведения для каждой проверки: предупреждения, ошибки, предложения или отключено.</span><span class="sxs-lookup"><span data-stu-id="c623c-167">The user decides how the diagnostics should be treated: as warnings, errors, suggestions, or to be turned off.</span></span> <span data-ttu-id="c623c-168">Например, архитектор проекта может решить, что проблемы с совместимостью следует рассматривать как ошибки, для вызовов некоторых устаревших API формировать предупреждения, а остальные проверки выполнять только в режиме рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="c623c-168">For example, as an architect, you can decide that compatibility issues should be treated as errors, calls to some deprecated APIs generate warnings, while others only generate suggestions.</span></span> <span data-ttu-id="c623c-169">Вы можете настроить это поведение отдельно для каждого идентификатора диагностики и каждого проекта.</span><span class="sxs-lookup"><span data-stu-id="c623c-169">You can configure this separately by diagnostic ID and by project.</span></span> <span data-ttu-id="c623c-170">Для этого найдите в **обозревателе решений** узел **Зависимости** для нужного проекта.</span><span class="sxs-lookup"><span data-stu-id="c623c-170">To do so in **Solution Explorer**, navigate to the **Dependencies** node under your project.</span></span> <span data-ttu-id="c623c-171">Разверните узлы **Зависимости** > **Анализаторы** > **Microsoft.DotNet.Analyzers.Compatibility**.</span><span class="sxs-lookup"><span data-stu-id="c623c-171">Expand the nodes **Dependencies** > **Analyzers** > **Microsoft.DotNet.Analyzers.Compatibility**.</span></span> <span data-ttu-id="c623c-172">Щелкните правой кнопкой мыши идентификатор диагностики, щелкните действие **Установить серьезность набора правил** и выберите нужный вариант.</span><span class="sxs-lookup"><span data-stu-id="c623c-172">Right click on the diagnostic ID, select **Set Rule Set Severity** and pick the desired option.</span></span>

![Снимок экрана с обозревателем решений и всплывающим диалоговым окном для выбора серьезности набор правил](media/api-analyzer/disable-notifications.jpg)

## <a name="see-also"></a><span data-ttu-id="c623c-174">См. также</span><span class="sxs-lookup"><span data-stu-id="c623c-174">See also</span></span>

* <span data-ttu-id="c623c-175">Запись блога [Знакомство с API анализатора](https://blogs.msdn.microsoft.com/dotnet/2017/10/31/introducing-api-analyzer/).</span><span class="sxs-lookup"><span data-stu-id="c623c-175">[Introducing API Analyzer](https://blogs.msdn.microsoft.com/dotnet/2017/10/31/introducing-api-analyzer/) blog post.</span></span>
* <span data-ttu-id="c623c-176">Демонстрационное видео [об анализаторе API](https://youtu.be/eeBEahYXGd0) на YouTube.</span><span class="sxs-lookup"><span data-stu-id="c623c-176">[API Analyzer](https://youtu.be/eeBEahYXGd0) demo video on YouTube.</span></span>