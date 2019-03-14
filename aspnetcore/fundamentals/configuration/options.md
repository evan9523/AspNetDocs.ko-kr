---
title: ASP.NET Core의 옵션 패턴
author: guardrex
description: 옵션 패턴을 사용하여 ASP.NET Core 앱에서 관련된 설정 그룹을 나타내는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: fundamentals/configuration/options
ms.openlocfilehash: 9566ed75375bdfaa9d6d8bf898b9fb2054356017
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065220"
---
# <a name="options-pattern-in-aspnet-core"></a>ASP.NET Core의 옵션 패턴

[Luke Latham](https://github.com/guardrex)으로

::: moniker range="<= aspnetcore-1.1"

이 항목의 1.1 버전을 얻으려면 [ASP.NET Core의 옵션 패턴(버전 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Options_1.1.pdf)을 다운로드하세요.

::: moniker-end

옵션 패턴은 클래스를 사용하여 관련 설정 그룹을 나타냅니다. [구성 설정](xref:fundamentals/configuration/index)이 시나리오에 따라 별도 클래스로 격리된 경우 앱은 두 가지 중요한 소프트웨어 엔지니어링 원칙을 따릅니다.

* [ISP(Interface Segregation Principle, 인터페이스 분리 원칙) 또는 캡슐화](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation) &ndash; 구성 설정에 종속된 시나리오(클래스)는 사용하는 구성 설정에 의해서만 결정됩니다.
* [관심사의 분리](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) &ndash; 앱의 다른 부분에 대한 설정은 다른 설정에 종속되거나 연결되지 않습니다.

옵션은 구성 데이터의 유효성을 검사하는 메커니즘도 제공합니다. 자세한 내용은 [옵션 유효성 검사](#options-validation) 섹션을 참조하세요.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>전제 조건

[Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)를 참조하거나 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) 패키지에 패키지 참조를 추가합니다.

## <a name="options-interfaces"></a>옵션 인터페이스

<xref:Microsoft.Extensions.Options.IOptionsMonitor`1>는 옵션을 검색하고 `TOptions` 인스턴스에 대한 옵션 알림을 관리하는 데 사용됩니다. <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>에서는 다음 시나리오를 지원합니다.

* 변경 알림
* [명명된 옵션](#named-options-support-with-iconfigurenamedoptions)
* [다시 로드할 수 있는 구성](#reload-configuration-data-with-ioptionssnapshot)
* 선택적 옵션 무효화(<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>)

[사후 구성](#options-post-configuration) 시나리오에서는 모든 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 구성이 수행된 후 옵션을 설정하거나 변경할 수 있습니다.

<xref:Microsoft.Extensions.Options.IOptionsFactory`1>는 새로운 옵션 인스턴스를 만듭니다. 단일 <xref:Microsoft.Extensions.Options.IOptionsFactory`1.Create*> 메서드가 있습니다. 기본 구현에서는 등록된 모든 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 및 <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1>를 사용하며 먼저 구성을 모두 실행한 다음, 사후 구성을 수행합니다. <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>와 <xref:Microsoft.Extensions.Options.IConfigureOptions`1>를 구별하며 적절한 인터페이스만 호출합니다.

<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>는 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>에서 `TOptions` 인스턴스를 캐시하는 데 사용됩니다. <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>는 모니터의 옵션 인스턴스를 무효화하므로 값이 다시 계산됩니다(<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryRemove*>). <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryAdd*>를 사용하여 값을 수동으로 도입할 수 있습니다. 모든 명명된 인스턴스를 필요에 따라 다시 만들어야 하는 경우 <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.Clear*> 메서드가 사용됩니다.

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1>은 모든 요청에서 옵션을 다시 계산해야 하는 시나리오에서 유용합니다. 자세한 내용은 [IOptionsSnapshot을 사용하여 구성 데이터 다시 로드](#reload-configuration-data-with-ioptionssnapshot)를 참조하세요.

<xref:Microsoft.Extensions.Options.IOptions`1>를 사용하여 옵션을 지원할 수 있습니다. 그러나 <xref:Microsoft.Extensions.Options.IOptions`1>는 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>의 이전 시나리오를 지원하지 않습니다. <xref:Microsoft.Extensions.Options.IOptions`1> 인터페이스를 이미 사용하고 있으며 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>에서 제공하는 시나리오가 필요하지 않은 기존 프레임워크 및 라이브러리에서는 <xref:Microsoft.Extensions.Options.IOptions`1>를 계속 사용할 수 있습니다.

## <a name="general-options-configuration"></a>일반 옵션 구성

일반 옵션 구성은 샘플 앱에 예제 &num;1로 설명되어 있습니다.

옵션 클래스는 매개 변수가 없는 public 생성자를 사용하는 비추상이어야 합니다. 다음 클래스 `MyOptions`에는 `Option1` 및 `Option2`의 두 가지 속성이 있습니다. 기본 값 설정은 선택 사항이지만, 다음 예제의 클래스 생성자는 `Option1`의 기본값을 설정합니다. `Option2`에는 직접 속성을 초기화하여 설정된 기본값이 있습니다(*Models/MyOptions.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptions.cs?name=snippet1)]

`MyOptions` 클래스가 <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure*>를 통해 서비스 컨테이너에 추가되고 구성에 바인딩됩니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example1)]

다음 페이지 모델은 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>를 통해 [생성자 종속성 삽입](xref:mvc/controllers/dependency-injection)을 사용하여 설정에 액세스합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example1)]

샘플의 *appsettings.json* 파일은 `option1` 및 `option2`에 대한 값을 지정합니다.

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=2-3)]

앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> 사용자 지정 <xref:System.Configuration.ConfigurationBuilder>를 사용하여 설정 파일에서 옵션 구성을 로드하는 경우 기본 경로가 올바르게 설정되었는지 확인합니다.
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 통해 설정 파일에서 옵션 구성을 로드하는 경우에는 명시적으로 기본 경로를 설정하지 않아도 됩니다.

## <a name="configure-simple-options-with-a-delegate"></a>대리자로 간단한 옵션 구성

대리자를 사용한 간단한 옵션 구성은 샘플 앱에 예제 &num;2로 설명되어 있습니다.

대리자를 사용하여 옵션 값을 설정합니다. 샘플 앱에서는 `MyOptionsWithDelegateConfig` 클래스(*Models/MyOptionsWithDelegateConfig.cs*)를 사용합니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

다음 코드에서 두 번째 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 서비스가 서비스 컨테이너에 추가됩니다. `MyOptionsWithDelegateConfig`를 통해 바인딩을 구성하는 데 대리자를 사용합니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example2)]

여러 구성 공급자를 추가할 수 있습니다. 구성 공급자는 NuGet 패키지에서 사용할 수 있으며 등록된 순서대로 적용됩니다. 자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.

<xref:Microsoft.Extensions.Options.IConfigureOptions`1.Configure*>를 호출할 때마다 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 서비스가 서비스 컨테이너에 추가됩니다. 위의 예제에서는 `Option1` 및 `Option2`의 값은 모두 *appsettings.json*에서 지정되지만, `Option1` 및 `Option2`의 값은 구성된 대리자에 의해 재정의됩니다.

둘 이상의 구성 서비스를 활성화한 경우 마지막 지정된 구성 소스가 *wins*를 지정했으며 구성 값을 설정합니다. 앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>하위 옵션 구성

하위 옵션 구성은 샘플 앱에 예제 &num;3으로 설명되어 있습니다.

앱은 앱의 특정 시나리오 그룹(클래스)과 관련된 옵션 클래스를 만들어야 합니다. 구성 값을 필요로 하는 앱의 일부는 사용하는 구성 값에 액세스할 수 있어야 합니다.

옵션을 구성에 바인딩하는 경우 옵션 형식의 각 속성은 `property[:sub-property:]` 양식의 구성 키에 바인딩됩니다. 예를 들어 `MyOptions.Option1` 속성은 키 `Option1`에 바인딩되어 *appsettings.json*의 `option1` 속성에서 읽습니다.

다음 코드에서 세 번째 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 서비스가 서비스 컨테이너에 추가됩니다. 이 코드는 `MySubOptions`를 *appsettings.json* 파일의 `subsection` 섹션에 바인딩합니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example3)]

`GetSection` 확장 메서드에는 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 패키지가 필요합니다. 앱이 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)를 사용하는 경우 패키지가 자동으로 포함됩니다.

샘플의 *appsettings.json* 파일은 `suboption1` 및 `suboption2`에 대한 키로 `subsection` 멤버를 정의합니다.

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=4-7)]

`MySubOptions` 클래스는 `SubOption1` 및 `SubOption2` 속성을 정의하여 옵션 값을 유지합니다(*Models/MySubOptions.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MySubOptions.cs?name=snippet1)]

페이지 모델의 `OnGet` 메서드는 옵션 값이 포함된 문자열을 반환합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example3)]

앱을 실행할 때 `OnGet` 메서드는 하위 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>직접 보기 주입 또는 보기 모델에 의해 제공되는 옵션

직접 보기 삽입 또는 보기 모델에 의해 제공되는 옵션은 샘플 앱에 예제 &num;4로 설명되어 있습니다.

옵션은 뷰 모델 또는 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>를 보기에 직접 주입하여 제공할 수 있습니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example4)]

샘플 앱은 `@inject` 지시문을 사용하여 `IOptionsMonitor<MyOptions>`를 삽입하는 방법을 보여 줍니다.

[!code-cshtml[](options/samples/2.x/OptionsSample/Pages/Index.cshtml?range=1-10&highlight=4)]

앱을 실행하면 옵션 값이 렌더링된 페이지에 표시됩니다.

![옵션 값 옵션 1: value1_from_json 및 옵션 2: -1은 모델에서 로드되며 보기에 주입됩니다.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>IOptionsSnapshot을 사용하여 구성 데이터 다시 로드

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1>을 사용하여 구성 데이터를 다시 로드하는 방법은 샘플 앱에 예제 &num;5로 설명되어 있습니다.

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1>은 최소한의 처리 오버헤드로 옵션 다시 로드를 지원합니다.

옵션은 요청의 수명 동안 액세스되고 캐시될 때 요청당 한 번 계산됩니다.

다음 예제에는 *appsettings.json*이 변경된 후 새 <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1>을 만드는 방법이 설명되어 있습니다(*Pages/Index.cshtml.cs*). 서버에 대한 여러 요청은 파일이 변경되고 구성이 다시 로드될 때까지 *appsettings.json* 파일에서 제공하는 상수 값을 반환합니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example5)]

다음 이미지에는 *appsettings.json* 파일에서 로드된 초기 `option1` 및 `option2` 값이 나와 있습니다.

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

*appsettings.json* 파일의 값을 `value1_from_json UPDATED` 및 `200`으로 변경합니다. *appsettings.json* 파일을 저장합니다. 옵션 값이 업데이트되었음을 확인하려면 브라우저를 새로 고칩니다.

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>IConfigureNamedOptions로 명명된 옵션 지원

<xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>로 명명된 옵션 지원은 샘플 앱에 예제 &num;6으로 설명되어 있습니다.

앱은 *명명된 옵션* 지원을 통해 명명된 옵션 구성들을 구분할 수 있습니다. 샘플 앱에서 명명된 옵션은 [OptionsServiceCollectionExtensions.Configure](xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure*)를 사용하여 선언됩니다. 이 메서드는 [ConfigureNamedOptions\<TOptions>.Configure](xref:Microsoft.Extensions.Options.ConfigureNamedOptions`1.Configure*) 확장 메서드를 호출합니다.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example6)]

샘플 앱은 <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1.Get*>을 사용하여 명명된 옵션에 액세스합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example6)]

샘플 앱을 실행하면 명명된 옵션이 반환됩니다.

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

`named_options_1` 값은 *appsettings.json* 파일에서 로드되는 구성에서 제공됩니다. `named_options_2` 값은 다음에서 제공됩니다.

* `Option1`에 대한 `ConfigureServices`의 `named_options_2` 대리자.
* `MyOptions` 클래스에서 제공되는 `Option2`에 대한 기본값.

## <a name="configure-all-options-with-the-configureall-method"></a>ConfigureAll 메서드를 사용하여 모든 옵션 구성

<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*> 메서드를 사용하여 모든 옵션 인스턴스를 구성합니다. 다음 코드는 공통 값을 사용하는 모든 구성 인스턴스에 대해 `Option1`을 구성합니다. 다음 코드를 `Startup.ConfigureServices` 메서드에 직접 추가합니다.

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

코드를 추가한 후 샘플 앱을 실행하면 다음과 같은 결과가 생성됩니다.

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> 모든 옵션은 명명된 인스턴스입니다. 기존 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 인스턴스는 `Options.DefaultName` 인스턴스를 대상 지정하는 것으로 처리됩니다(즉, `string.Empty`). 또한 <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>는 <xref:Microsoft.Extensions.Options.IConfigureOptions`1>를 구현합니다. <xref:Microsoft.Extensions.Options.IOptionsFactory`1>의 기본 구현에는 각 옵션을 적절하게 사용하기 위한 논리가 있습니다. `null` 명명된 옵션은 특정 명명된 인스턴스 대신 모든 명명된 인스턴스를 대상으로 지정하는 데 사용됩니다(<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*> 및 <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*>에서 이 규칙을 사용함).

## <a name="optionsbuilder-api"></a>OptionsBuilder API

<xref:Microsoft.Extensions.Options.OptionsBuilder`1>는 `TOptions` 인스턴스를 구성하는 데 사용됩니다. `OptionsBuilder`는 `AddOptions<TOptions>(string optionsName)` 호출에 대한 단일 매개 변수이므로 모든 후속 호출에 나타나는 대신 명명된 옵션 생성을 간소화합니다. 옵션 유효성 검사 및 서비스 종속성을 허용하는 `ConfigureOptions` 오버로드는 `OptionsBuilder`를 통해서만 사용할 수 있습니다.

```csharp
// Options.DefaultName = "" is used.
services.AddOptions<MyOptions>().Configure(o => o.Property = "default");

services.AddOptions<MyOptions>("optionalName")
    .Configure(o => o.Property = "named");
```

## <a name="use-di-services-to-configure-options"></a>DI 서비스를 사용하여 옵션 구성

다음과 같은 두 가지 방법으로 옵션을 구성하는 동안 종속성 주입을 통해 다른 서비스에 액세스할 수 있습니다.

* [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1)에서 구성 대리자를 [구성](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*)에 전달합니다. [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1)는 최대 5개의 서비스를 사용하여 옵션을 구성할 수 있는 [구성](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*)의 오버로드를 제공합니다.

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<Service1, Service2, Service3, Service4, Service5>(
          (o, s, s2, s3, s4, s5) => 
              o.Property = DoSomethingWith(s, s2, s3, s4, s5));
  ```

* <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 또는 <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>를 구현하는 고유의 형식을 만들고 형식을 서비스로 등록합니다.

서비스를 만드는 것이 더 복잡하기 때문에 구성 대리자를 [구성](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*)에 전달하는 것이 좋습니다. 고유의 형식을 만드는 것은 [구성](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*)을 사용할 때 프레임워크가 수행하는 것과 동일합니다. [구성](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*)을 호출하면 지정된 일반 서비스 유형을 허용하는 생성자가 있는 일시적인 제네릭 <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>가 등록됩니다. 

::: moniker range=">= aspnetcore-2.2"

## <a name="options-validation"></a>옵션 유효성 검사

옵션 유효성 검사를 사용하면 옵션이 구성될 때 옵션의 유효성을 검사할 수 있습니다. 옵션이 유효하면 `true`를 반환하고 옵션이 유효하지 않으면 `false`를 반환하는 유효성 검사 메서드로 `Validate`를 호출합니다.

```csharp
// Registration
services.AddOptions<MyOptions>("optionalOptionsName")
    .Configure(o => { }) // Configure the options
    .Validate(o => YourValidationShouldReturnTrueIfValid(o), 
        "custom error");

// Consumption
var monitor = services.BuildServiceProvider()
    .GetService<IOptionsMonitor<MyOptions>>();
  
try
{
    var options = monitor.Get("optionalOptionsName");
}
catch (OptionsValidationException e) 
{
   // e.OptionsName returns "optionalOptionsName"
   // e.OptionsType returns typeof(MyOptions)
   // e.Failures returns a list of errors, which would contain 
   //     "custom error"
}
```

위의 예제에서는 명명된 옵션 인스턴스를 `optionalOptionsName`으로 설정합니다. 기본 옵션 인스턴스는 `Options.DefaultName`입니다.

유효성 검사는 옵션 인스턴스가 만들어지면 실행됩니다. 옵션 인스턴스는 처음 액세스되면 유효성 검사를 통과하도록 보장됩니다.

> [!IMPORTANT]
> 옵션 유효성 검사는 옵션이 처음 구성되고 유효성이 검사된 후 옵션 수정에 대해 보호하지 않습니다.

`Validate` 메서드는 `Func<TOptions, bool>`을 허용합니다. 유효성 검사를 완전히 사용자 지정하려면 다음을 허용하는 `IValidateOptions<TOptions>`를 구현합니다.

* 여러 옵션 형식의 유효성 검사: `class ValidateTwo : IValidateOptions<Option1>, IValidationOptions<Option2>`
* 다른 옵션 형식에 의존하는 유효성 검사: `public DependsOnAnotherOptionValidator(IOptionsMonitor<AnotherOption> options)`

`IValidateOptions`는 다음의 유효성을 검사합니다.

* 특정 명명된 옵션 인스턴스.
* `name`이 `null`인 경우 모든 옵션.

인터페이스의 구현에서 `ValidateOptionsResult`를 반환합니다.

```csharp
public interface IValidateOptions<TOptions> where TOptions : class
{
    ValidateOptionsResult Validate(string name, TOptions options);
}
```

데이터 주석 기반 유효성 검사는 `OptionsBuilder<TOptions>`에 대해 `ValidateDataAnnotations` 메서드를 호출하여 [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) 패키지에서 사용할 수 있습니다. `Microsoft.Extensions.Options.DataAnnotations`는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.2 이상)에 포함되어 있습니다.

```csharp
private class AnnotatedOptions
{
    [Required]
    public string Required { get; set; }

    [StringLength(5, ErrorMessage = "Too long.")]
    public string StringLength { get; set; }

    [Range(-5, 5, ErrorMessage = "Out of range.")]
    public int IntRange { get; set; }
}

[Fact]
public void CanValidateDataAnnotations()
{
    var services = new ServiceCollection();
    services.AddOptions<AnnotatedOptions>()
        .Configure(o =>
        {
            o.StringLength = "111111";
            o.IntRange = 10;
            o.Custom = "nowhere";
        })
        .ValidateDataAnnotations();

    var sp = services.BuildServiceProvider();

    var error = Assert.Throws<OptionsValidationException>(() => 
        sp.GetRequiredService<IOptionsMonitor<AnnotatedOptions>>().Value);
    ValidateFailure<AnnotatedOptions>(error, Options.DefaultName, 1,
        "DataAnnotation validation failed for members Required " +
            "with the error 'The Required field is required.'.",
        "DataAnnotation validation failed for members StringLength " +
            "with the error 'Too long.'.",
        "DataAnnotation validation failed for members IntRange " +
            "with the error 'Out of range.'.");
}
```

즉시 유효성 검사(시작 시 빠른 실패)는 향후 릴리스에서 고려 중입니다.

::: moniker-end

## <a name="options-post-configuration"></a>옵션 사후 구성

<xref:Microsoft.Extensions.Options.IPostConfigureOptions`1>를 사용하여 사후 구성을 설정합니다. 사후 구성은 모든 <xref:Microsoft.Extensions.Options.IConfigureOptions`1> 구성이 수행된 후에 실행됩니다.

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<xref:Microsoft.Extensions.Options.IPostConfigureOptions`1.PostConfigure*>를 사용하여 명명된 옵션을 사후 구성할 수 있습니다.

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

모든 구성 인스턴스를 사후 구성하려면 <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*>을 사용합니다.

```csharp
services.PostConfigureAll<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="accessing-options-during-startup"></a>시작하는 동안 옵션 액세스

`Configure` 메서드가 실행되기 전에 서비스가 빌드되므로 `Startup.Configure`에서 <xref:Microsoft.Extensions.Options.IOptions`1> 및 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>를 사용할 수 있습니다.

```csharp
public void Configure(IApplicationBuilder app, IOptionsMonitor<MyOptions> optionsAccessor)
{
    var option1 = optionsAccessor.CurrentValue.Option1;
}
```

`Startup.ConfigureServices`에서는 <xref:Microsoft.Extensions.Options.IOptions`1> 또는 <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>를 사용하지 마세요. 서비스 등록의 순서 지정으로 인해 일관성 없는 옵션 상태가 있을 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/configuration/index>
