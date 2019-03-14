---
title: Azure App Service에 ASP.NET Core 앱 배포
author: guardrex
description: 이 문서에는 Azure 호스트 및 배포 리소스의 링크가 포함됩니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: host-and-deploy/azure-apps/index
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a>Azure App Service에 ASP.NET Core 앱 배포

[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.

## <a name="useful-resources"></a>유용한 리소스

Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다. ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.

[Azure에서 ASP.NET Core 웹앱 만들기](/azure/app-service/app-service-web-get-started-dotnet)  
Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.

[App Service on Linux에서 ASP.NET Core 앱 만들기](/azure/app-service/containers/quickstart-dotnetcore)  
명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.

다음 문서는 ASP.NET Core 설명서에 제공됩니다.

<xref:tutorials/publish-to-azure-webapp-using-vs>  
Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.

<xref:host-and-deploy/azure-apps/azure-continuous-deployment>  
Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.

[Azure Pipelines를 사용하여 첫 번째 파이프라인 만들기](/azure/devops/pipelines/get-started-yaml)  
ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.

[Azure Web App 샌드박스](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.

## <a name="application-configuration"></a>애플리케이션 구성

### <a name="platform"></a>플랫폼

::: moniker range=">= aspnetcore-2.2"

64비트(x64) 및 32비트(x86) 앱은 Azure App Service에 있습니다. App Service에서 사용 가능한 [.NET Core SDK](/dotnet/core/sdk)는 32비트이지만 [Kudu](https://github.com/projectkudu/kudu/wiki) 콘솔 또는 [Visual Studio 게시 프로필이나 CLI 명령을 사용하는 MSDeploy](xref:host-and-deploy/visual-studio-publish-profiles)를 통해 64비트 앱을 배포할 수 있습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

원시 종속 항목을 지원하는 앱의 경우 32비트(x86) 앱의 런타임이 Azure App Service에 있습니다. App Service에서 사용 가능한 [.NET Core SDK](/dotnet/core/sdk)는 32비트입니다.

::: moniker-end

### <a name="packages"></a>패키지

Azure App Service에 배포된 앱에 대한 자동 로깅 기능을 제공하려면 다음 NuGet 패키지를 포함합니다.

* [Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 강화 통합을 제공합니다. 추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.
* [Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.
* [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.

이전의 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 없습니다. .NET Framework를 대상으로 하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 앱은 앱 프로젝트 파일의 개별 패키지를 명시적으로 참조해야 합니다.

## <a name="override-app-configuration-using-the-azure-portal"></a>Azure Portal을 사용하여 앱 구성 재정의

Azure Portal의 앱 설정을 사용하면 앱의 환경 변수를 설정할 수 있습니다. 환경 변수는 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)가 사용할 수 있습니다.

Azure Portal에서 앱 설정을 만들거나 수정하고**저장** 단추를 선택하면 Azure 앱이 다시 시작됩니다. 서비스를 다시 시작한 후에 환경 변수를 앱에서 사용할 수 있습니다.

앱이 [웹 호스트](xref:fundamentals/host/web-host)를 사용하고 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 사용하여 호스트를 빌드하는 경우 호스트를 구성하는 환경 변수는 `ASPNETCORE_` 접두사를 사용합니다. 자세한 내용은 <xref:fundamentals/host/web-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.

앱이 [일반 호스트](xref:fundamentals/host/generic-host)를 사용하는 경우에는 기본적으로 환경 변수가 앱 구성으로 로드되지 않으며 개발자가 구성 공급자를 추가해야 합니다. 개발자가 구성 공급자를 추가할 때 환경 변수 접두사를 결정합니다. 자세한 내용은 <xref:fundamentals/host/generic-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다. 추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

## <a name="monitoring-and-logging"></a>모니터링 및 로깅

App Service에 배포된 ASP.NET Core 앱은 자동으로 App Service 확장인 **ASP.NET Core 로깅 확장**을 받습니다. 이 확장은 Azure 로깅을 사용하도록 설정합니다.

모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.

[방법: Azure App Service에서 앱 모니터링](/azure/app-service/web-sites-monitor)  
앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.

[Azure App Service에서 웹앱에 대한 진단 로깅 사용](/azure/app-service/web-sites-enable-diagnostic-log)  
HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.

<xref:fundamentals/error-handling>  
ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.

<xref:host-and-deploy/azure-apps/troubleshoot>  
ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.

<xref:host-and-deploy/azure-iis-errors-reference>  
Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.

## <a name="data-protection-key-ring-and-deployment-slots"></a>데이터 보호 키 링 및 배포 슬롯

[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다. 이 폴더는 네트워크 스토리지에서 지원하고, 앱을 호스트하는 모든 머신에서 동기화됩니다. 저장된 키는 보호되지 않습니다. 이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다. 준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.

배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다. ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다. 이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다. 슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.

* Azure Blob Storage
* Azure Key Vault
* SQL 저장소
* Redis Cache

자세한 내용은 <xref:security/data-protection/implementation/key-storage-providers>을 참조하세요.

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a>Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포

다음 방법 중 하나를 사용합니다.

* [미리 보기 사이트 확장을 설치](#install-the-preview-site-extension)합니다.
* [자체 포함된 앱을 배포](#deploy-the-app-self-contained)합니다.
* [Web Apps for Containers에서 Docker를 사용](#use-docker-with-web-apps-for-containers)합니다.

### <a name="install-the-preview-site-extension"></a>미리 보기 사이트 확장 설치

미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.

1. Azure Portal에서 App Service로 이동합니다.
1. 웹앱을 선택합니다.
1. 검색 상자에 "ex"를 입력하여 "확장"으로 필터링하거나 관리 도구 목록을 아래로 스크롤합니다.
1. **확장**을 선택합니다.
1. **추가**를 선택합니다.
1. 목록에서 **ASP.NET Core {X.Y}({x64|x86}) 런타임** 확장을 선택합니다. 여기서 `{X.Y}`는 ASP.NET Core 미리 보기 버전이며 `{x64|x86}`은 플랫폼을 지정합니다.
1. **확인**을 선택하여 적합한 조건을 적용합니다.
1. 확장을 설치하려면 **확인**을 선택합니다.

작업이 완료되면 최신.NET Core 미리 보기가 설치됩니다. 설치를 확인합니다.

1. **고급 도구**를 선택합니다.
1. **고급 도구**에서 **Go**를 선택합니다.
1. **디버그 콘솔** > **PowerShell** 메뉴 항목을 선택합니다.
1. PowerShell 프롬프트에서 다음 명령을 실행합니다. 명령에서 `{X.Y}`를 ASP.NET Core 런타임 버전으로 대체하고, `{PLATFORM}`을 플랫폼으로 대체합니다.

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.{PLATFORM}\
   ```
   x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.

> [!NOTE]
> A 시리즈 컴퓨팅 또는 더 나은 호스트 계층에서 호스트되는 앱이 필요한 경우 Azure Portal의 앱 설정에서 App Services 앱의 플랫폼 아키텍처(x86/x64)를 설정합니다. 앱이 in-process 모드에서 실행되고 플랫폼 아키텍처가 64비트(x64)에 대해 구성되는 경우 ASP.NET Core 모듈은 64비트 미리 보기 런타임을 사용합니다(있는 경우). **ASP.NET Core {X.Y}(x64) 런타임** 확장을 설치합니다.
>
> x64 미리 보기 런타임을 설치한 후에 Kudu PowerShell 명령 창에서 다음 명령을 실행하여 설치를 확인합니다. 명령에서 `{X.Y}`에 대한 ASP.NET Core 런타임 버전을 대체합니다.
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.x64\
> ```
> x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.

> [!NOTE]
> **ASP.NET Core 확장**을 사용하면 Azure 로깅을 사용하는 등 Azure App Services에서 ASP.NET Core에 대한 추가 기능을 사용할 수 있습니다. Visual Studio에서 배포할 경우 확장은 자동으로 설치됩니다. 확장이 설치되지 않은 경우 앱에서 설치합니다.

**ARM 템플릿에서 미리 보기 사이트 확장 사용**

ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다. 예를 들어:

[!code-json[](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a>자체 포함된 앱 배포

미리 보기 런타임을 대상으로 하는 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)는 배포 시 미리 보기 런타임을 전달합니다.

자체 포함된 앱을 배포하는 경우:

* Azure App Service의 사이트에는 [미리 보기 사이트 확장](#install-the-preview-site-extension)이 필요하지 않습니다.
* 앱은 [FDD(프레임워크 종속 배포)](/dotnet/core/deploying#framework-dependent-deployments-fdd)에 대해 게시할 때와 다른 접근 방식으로 공개해야 합니다.

#### <a name="publish-from-visual-studio"></a>Visual Studio에서 게시

1. Visual Studio 도구 모음에서 **빌드** > **{애플리케이션 이름} 게시**를 선택합니다.
1. **공개 대상 선택** 대화 상자에서 **App Service**가 선택되어 있는지 확인합니다.
1. **고급**을 선택합니다. **게시** 대화 상자가 열립니다.
1. **게시** 대화 상자에서:
   * **릴리스** 구성이 선택되었는지 확인합니다.
   * **배포 모드** 드롭다운 목록을 열고 **자체 포함**을 선택합니다.
   * **대상 런타임** 드롭다운 목록에서 대상 런타임을 선택합니다. 기본값은 `win-x86`입니다.
   * 배포 시 추가 파일을 제거해야 하는 경우 **파일 게시 옵션**을 열고 대상에서 추가 파일을 제거하는 확인란을 선택합니다.
   * **저장**을 선택합니다.
1. 게시 마법사의 나머지 프롬프트를 따라 새 사이트를 작성하거나 기존 사이트를 업데이트합니다.

#### <a name="publish-using-command-line-interface-cli-tools"></a>CLI(명령줄 인터페이스) 도구를 사용하여 게시합니다.

1. 프로젝트 파일에서 하나 이상의 [RID(런타임 ID)](/dotnet/core/rid-catalog)를 지정합니다. 단일 RID에 `<RuntimeIdentifier>`(단수)을 사용하거나, `<RuntimeIdentifiers>`(복수)를 사용하여 세미콜론으로 구분된 RID 목록을 제공합니다. 다음 예제에서는 `win-x86` RID가 지정됩니다.

   ```xml
   <PropertyGroup>
     <TargetFramework>netcoreapp2.1</TargetFramework>
     <RuntimeIdentifier>win-x86</RuntimeIdentifier>
   </PropertyGroup>
   ```
1. 명령 셸에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 사용하여 호스트의 런타임에 대한 릴리스 구성에 있는 앱을 게시합니다. 다음 예제에서 앱은 `win-x86` RID에 게시됩니다. `--runtime` 옵션에 제공된 RID를 프로젝트 파일의 `<RuntimeIdentifier>`(또는 `<RuntimeIdentifiers>`) 속성에 제공해야 합니다.

   ```console
   dotnet publish --configuration Release --runtime win-x86
   ```
1. *bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* 디렉터리의 콘텐츠를 App Service의 사이트로 이동합니다.

### <a name="use-docker-with-web-apps-for-containers"></a>Web Apps for Containers에서 Docker 사용

[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 미리 보기 Docker 이미지가 포함됩니다. 이미지는 기본 이미지로 사용할 수 있습니다. 이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.

## <a name="protocol-settings-https"></a>프로토콜 설정(HTTPS)

보안 프로토콜 바인딩을 사용하면 HTTPS를 통한 요청에 응답할 때 사용할 인증서를 지정할 수 있습니다. 바인딩을 위해서는 특정 호스트 이름에 대해 발행된 유효한 개인 인증서(*.pfx*)가 필요합니다. 자세한 내용은 [자습서: 기존 사용자 지정 SSL 인증서를 Azure Web Apps에 바인딩](/azure/app-service/app-service-web-tutorial-custom-ssl)을 참조하세요.

## <a name="transform-webconfig"></a>web.config 변환

게시할 때 *web.config*를 변환해야 하는 경우(예: 구성, 프로필 또는 환경을 기반으로 환경 변수 설정) <xref:host-and-deploy/iis/transform-webconfig>를 참조하세요.

## <a name="additional-resources"></a>추가 자료

* [Web Apps 개요(5분 개요 비디오)](/azure/app-service/app-service-web-overview)
* [Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 동영상)](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 동영상)](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [Azure App Service 진단 개요](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다. 다음 항목은 기본 IIS 기술과 관련이 있습니다.

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [Microsoft TechNet 라이브러리: Windows Server](/windows-server/windows-server-versions)
