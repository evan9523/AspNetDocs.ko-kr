---
title: ASP.NET Core에서 여러 환경 사용
author: rick-anderson
description: ASP.NET Core 앱의 여러 환경에서 앱 동작을 제어하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 01/22/2019
uid: fundamentals/environments
ms.openlocfilehash: 39e1b48481832a6d76de605b37410fe2e16dcd88
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035580"
---
# <a name="use-multiple-environments-in-aspnet-core"></a>ASP.NET Core에서 여러 환경 사용

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core는 환경 변수를 사용하여 런타임 환경에 따라 앱 동작을 구성합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="environments"></a>환경

ASP.NET Core는 앱 시작 시 환경 변수 `ASPNETCORE_ENVIRONMENT`를 읽고 [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)에 값을 저장합니다. `ASPNETCORE_ENVIRONMENT`를 임의의 값으로 설정할 수 있지만 [세 개의 값](/dotnet/api/microsoft.aspnetcore.hosting.environmentname)은 프레임워크에서 지원됩니다. [개발](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [스테이징](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging) 및 [프로덕션](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production). `ASPNETCORE_ENVIRONMENT`가 설정되지 않은 경우 기본값은 `Production`입니다.

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet)]

위의 코드는:

* `ASPNETCORE_ENVIRONMENT`이 `Development`로 설정된 경우 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage)를 호출합니다.
* `ASPNETCORE_ENVIRONMENT`의 값이 다음 중 하나로 설정된 경우 [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler)를 호출합니다.

    * `Staging`
    * `Production`
    * `Staging_2`

[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)는 `IHostingEnvironment.EnvironmentName`의 값을 사용하여 요소에 표시를 포함하거나 제외합니다.

[!code-cshtml[](environments/sample-snapshot/EnvironmentsSample/Pages/About.cshtml)]

Windows와 macOS에서 환경 변수 및 값은 대/소문자를 구분하지 않습니다. Linux 환경 변수 및 값은 기본적으로 **대/소문자를 구분**합니다.

### <a name="development"></a>개발

개발 환경은 프로덕션에서 노출해서는 안 되는 기능을 활성화할 수 있습니다. 예를 들어 ASP.NET Core 템플릿은 개발 환경에서 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page)를 활성화합니다.

로컬 컴퓨터 개발을 위한 환경은 프로젝트의 *Properties\launchSettings.json* 파일에서 설정할 수 있습니다. *launchSettings.json*의 환경 값은 시스템 환경에서 설정된 값을 재정의합니다.

다음 JSON에는 *launchSettings.json* 파일의 세 가지 프로필이 표시되어 있습니다.

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:54339/",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      }
    },
    "EnvironmentsSample": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:54340/"
    },
    "Kestrel Staging": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:51997/"
    }
  }
}
```

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> *launchSettings.json*의 `applicationUrl` 속성은 서버 URL의 목록을 지정할 수 있습니다. 목록의 URL 사이에 세미콜론을 사용합니다.
>
> ```json
> "EnvironmentsSample": {
>    "commandName": "Project",
>    "launchBrowser": true,
>    "applicationUrl": "https://localhost:5001;http://localhost:5000",
>    "environmentVariables": {
>      "ASPNETCORE_ENVIRONMENT": "Development"
>    }
> }
> ```

::: moniker-end

[dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 앱을 시작하면 `"commandName": "Project"`를 포함한 첫 번째 프로필이 사용됩니다. `commandName`의 값은 시작할 웹 서버를 지정합니다. `commandName`은 다음 중 하나일 수 있습니다.

* `IISExpress`
* `IIS`
* `Project`(Kestrel 시작)

앱이 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작하는 경우:

* 가능한 경우 *launchSettings.json*을 읽습니다. *launchSettings.json*의 `environmentVariables` 설정은 환경 변수를 재정의합니다.
* 호스팅 환경이 표시됩니다.

다음 출력은 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작되는 앱을 보여 줍니다.

```bash
PS C:\Websites\EnvironmentsSample> dotnet run
Using launch settings from C:\Websites\EnvironmentsSample\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Websites\EnvironmentsSample
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

Visual Studio 프로젝트 속성 **Debug** 탭은 *launchSettings.json* 파일을 편집할 수 있는 GUI를 제공합니다.

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

웹 서버가 다시 시작되기 전에는 프로젝트 프로필의 변경 내용이 적용되지 않을 수 있습니다. 해당 환경에 대한 변경 내용을 감지하려면 Kestrel을 다시 시작해야 합니다.

> [!WARNING]
> *launchSettings.json*은 암호를 저장하지 않아야 합니다. [암호 관리자 도구](xref:security/app-secrets)를 사용하여 로컬 개발에 대한 암호를 저장할 수 있습니다.

[Visual Studio Code](https://code.visualstudio.com/)를 사용하는 경우 환경 변수는 *.vscode/launch.json* 파일에서 설정할 수 있습니다. 다음 예제에서는 환경을 `Development`로 설정합니다.

```json
{
   "version": "0.2.0",
   "configurations": [
        {
            "name": ".NET Core Launch (web)",

            ... additional VS Code configuration settings ...

            "env": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    ]
}
```

*Properties/launchSettings.json*과 같은 방식으로 `dotnet run`을 사용하여 앱을 시작할 때 프로젝트의 *.vscode/launch.json* 파일은 읽히지 않습니다. *launchSettings.json* 파일이 없는 개발 환경에서 앱을 시작할 때는 `dotnet run` 명령에 대한 환경 변수 또는 명령줄 인수로 환경을 설정합니다.

### <a name="production"></a>프로덕션

프로덕션 환경은 보안, 성능 및 앱 견고성을 최대화하도록 구성되어야 합니다. 개발과 다른 몇 가지 일반적인 설정은 다음과 같습니다.

* 캐싱.
* 클라이언트 쪽 리소스가 번들로 제공되고, 축소되며, 잠재적으로 CDN에서 처리됩니다.
* 진단 오류 페이지를 사용하지 않습니다.
* 친숙한 오류 페이지를 사용하도록 설정합니다.
* 프로덕션 로깅 및 모니터링을 사용합니다. 예: [Application Insights](/azure/application-insights/app-insights-asp-net-core).

## <a name="set-the-environment"></a>환경 변수를 설정합니다.

테스트를 위해 특정 환경을 설정하는 것이 유용합니다. 환경을 설정하지 않으면 대부분의 디버깅 기능을 사용하지 않는 `Production`으로 기본값이 지정됩니다. 환경 설정에 대한 메서드는 운영 체제에 따라 다릅니다.

### <a name="azure-app-service"></a>Azure App Service

[Azure App Service](https://azure.microsoft.com/services/app-service/)에서 환경을 설정하려면 다음 단계를 수행합니다.

1. **App Services** 블레이드에서 앱을 선택합니다.
1. **SETTINGS** 그룹에서 **애플리케이션 설정** 블레이드를 선택합니다.
1. **애플리케이션 설정** 영역에서 **새 설정 추가**를 선택합니다.
1. **이름 입력**의 경우, `ASPNETCORE_ENVIRONMENT`를 제공합니다. **값 입력**의 경우 환경을 제공합니다(예: `Staging`).
1. 배포 슬롯을 교환할 때 환경 설정을 현재 슬롯으로 유지하려면 **슬롯 설정** 확인란을 선택합니다. 자세한 내용은 [Azure 설명서: 교환된 설정은? ](/azure/app-service/web-sites-staged-publishing)를 참조하세요.
1. 블레이드 상단에서 **저장**을 선택합니다.

Azure App Service는 Azure Portal에서 앱 설정(환경 변수)이 추가, 변경 또는 삭제된 후 앱을 자동으로 다시 시작합니다.

### <a name="windows"></a>Windows

현재 세션에 `ASPNETCORE_ENVIRONMENT`를 설정하려면 앱이 [dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 시작할 때 다음 명령이 사용됩니다.

**명령 프롬프트**

```console
set ASPNETCORE_ENVIRONMENT=Development
```

**PowerShell**

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

이러한 명령은 현재 창에만 적용됩니다. 창이 닫히면 `ASPNETCORE_ENVIRONMENT` 설정이 기본 설정 또는 컴퓨터 값으로 되돌아갑니다.

Windows에서 전역적으로 값을 설정하려면 다음 방법 중 하나를 사용합니다.

* **제어판** > **시스템** > **고급 시스템 설정**을 열고 `ASPNETCORE_ENVIRONMENT` 값을 추가하거나 편집합니다.

  ![시스템 고급 속성](environments/_static/systemsetting_environment.png)

  ![ASPNET Core 환경 변수](environments/_static/windows_aspnetcore_environment.png)

* 관리 명령 프롬프트를 열고 `setx` 명령을 사용하거나 관리 PowerShell 명령 프롬프트를 열고 `[Environment]::SetEnvironmentVariable`을 사용합니다.

  **명령 프롬프트**

  ```console
  setx ASPNETCORE_ENVIRONMENT Development /M
  ```

  `/M` 스위치는 시스템 수준에서 환경 변수를 설정함을 나타냅니다. `/M` 스위치를 사용하지 않으면 환경 변수가 사용자 계정으로 설정됩니다.

  **PowerShell**

  ```powershell
  [Environment]::SetEnvironmentVariable("ASPNETCORE_ENVIRONMENT", "Development", "Machine")
  ```

  `Machine` 옵션 값은 시스템 수준에서 환경 변수를 설정함을 나타냅니다. 옵션 값이 `User`로 변경되면 환경 변수가 사용자 계정으로 설정됩니다.

`ASPNETCORE_ENVIRONMENT` 환경 변수를 전역적으로 설정하면 값이 설정된 후 열리는 모든 명령 창에서 `dotnet run`에 대해 적용됩니다.

**web.config**

*web.config*를 사용하여 `ASPNETCORE_ENVIRONMENT`환경 변수를 설정하려면 <xref:host-and-deploy/aspnet-core-module#setting-environment-variables>의 *환경 변수 설정* 섹션을 참조하세요. `ASPNETCORE_ENVIRONMENT` 환경 변수를 *web.config*로 설정하면 해당 값이 시스템 수준의 설정을 재정의합니다.

::: moniker range=">= aspnetcore-2.2"

**프로젝트 파일 또는 게시 프로필**

**Windows IIS 배포의 경우:** `<EnvironmentName>` 속성을 게시 프로필(*.pubxml*) 또는 프로젝트 파일에 포함합니다. 이 방법은 프로젝트가 게시될 때 *web.config*에 환경을 설정합니다.

```xml
<PropertyGroup>
  <EnvironmentName>Development</EnvironmentName>
</PropertyGroup>
```

::: moniker-end

**IIS 애플리케이션 풀마다**

격리된 애플리케이션 풀에서 실행되는(IIS 10.0 이상에서 지원됨) 앱에 대한 `ASPNETCORE_ENVIRONMENT` 환경 변수를 설정하려면, [ 환경 변수 &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요. `ASPNETCORE_ENVIRONMENT` 환경 변수를 앱 풀에 대해 설정하면 해당 값이 시스템 수준의 설정을 재정의합니다.

> [!IMPORTANT]
> IIS에서 앱을 호스팅하고 `ASPNETCORE_ENVIRONMENT` 환경 변수를 추가 또는 변경할 때 다음 방법 중 하나를 사용하여 앱에서 선택한 새 값을 가져옵니다.
>
> * 명령 프롬프트에서 `net stop was /y` 다음에 `net start w3svc`를 실행합니다.
> * 서버를 다시 시작합니다.

### <a name="macos"></a>macOS

macOS에 대한 현재 환경 설정은 앱을 실행할 때 인라인으로 수행할 수 있습니다.

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

또는 앱을 실행하기 전에 `export`를 사용하여 환경을 설정합니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

컴퓨터 수준 환경 변수는 *.bashrc* 또는 *.bash_profile* 파일에서 설정됩니다. 임의의 텍스트 편집기를 사용하여 파일을 편집합니다. 다음 명령문을 추가합니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a>Linux

Linux 배포의 경우 세션 기반 변수 설정에 대한 명령 프롬프트에서 `export` 명령 또는 컴퓨터 수준 환경 설정에 대한 *bash_profile* 파일을 사용합니다.

### <a name="configuration-by-environment"></a>환경별 구성

환경별 구성을 로드하려면 다음을 권장합니다.

* *appsettings* 파일(*appsettings.&lt;<Environment>&gt;.json) [구성: 파일 구성 공급자](xref:fundamentals/configuration/index#file-configuration-provider)를 참조하세요.
* 환경 변수(앱이 호스팅되는 각 시스템에서 설정) [구성: 파일 구성 공급자](xref:fundamentals/configuration/index#file-configuration-provider) 및 [개발에서 앱 비밀의 안전한 스토리지: 환경 변수](xref:security/app-secrets#environment-variables)를 참조하세요.
* 비밀 관리자(개발 환경에만 해당) <xref:security/app-secrets>을 참조하세요.

## <a name="environment-based-startup-class-and-methods"></a>환경에 따른 시작 클래스 및 메서드

### <a name="startup-class-conventions"></a>시작 클래스 규칙

ASP.NET Core 앱이 시작되면 [시작 클래스](xref:fundamentals/startup)가 앱을 부트스트랩합니다. 앱은 다양한 환경(예: `StartupDevelopment`)에 대한 별도의 `Startup` 클래스를 정의할 수 있으며 적절한 `Startup` 클래스는 런타임에 선택됩니다. 해당 이름 접미사가 현재 환경과 일치하는 클래스에 우선 순위가 부여됩니다. 일치하는 `Startup{EnvironmentName}` 클래스를 찾을 수 없으면 `Startup` 클래스가 사용됩니다.

환경 기반 `Startup` 클래스를 구현하려면 사용 중인 각 환경에 대한 `Startup{EnvironmentName}` 클래스와 폴백 `Startup` 클래스를 만듭니다.

```csharp
// Startup class to use in the Development environment
public class StartupDevelopment
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}

// Startup class to use in the Production environment
public class StartupProduction
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}

// Fallback Startup class
// Selected if the environment doesn't match a Startup{EnvironmentName} class
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        ...
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        ...
    }
}
```

어셈블리 이름을 허용하는 [UseStartup(IWebHostBuilder, String)](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usestartup) 오버로드를 사용합니다.

::: moniker range=">= aspnetcore-2.1"

```csharp
public static void Main(string[] args)
{
    CreateWebHostBuilder(args).Build().Run();
}

public static IWebHostBuilder CreateWebHostBuilder(string[] args)
{
    var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

    return WebHost.CreateDefaultBuilder(args)
        .UseStartup(assemblyName);
}
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
public static void Main(string[] args)
{
    CreateWebHost(args).Run();
}

public static IWebHost CreateWebHost(string[] args)
{
    var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

    return WebHost.CreateDefaultBuilder(args)
        .UseStartup(assemblyName)
        .Build();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var assemblyName = typeof(Startup).GetTypeInfo().Assembly.FullName;

        var host = new WebHostBuilder()
            .UseStartup(assemblyName)
            .Build();

        host.Run();
    }
}
```

::: moniker-end

### <a name="startup-method-conventions"></a>시작 메서드 규칙

[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices)는 `Configure<EnvironmentName>` 및 `Configure<EnvironmentName>Services` 양식의 환경 특정 버전을 지원합니다.

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet_all&highlight=15,51)]

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/startup>
* <xref:fundamentals/configuration/index>
* [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)
