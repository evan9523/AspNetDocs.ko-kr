---
title: ASP.NET Core 앱 배포용 Visual Studio 게시 프로필
author: rick-anderson
description: Visual Studio에서 게시 프로필을 만들고 다양한 대상에 대한 ASP.NET Core 앱 배포를 관리하는 데 사용하는 방법에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/22/2019
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: e1e8f99be18d6f395a146bda805f71c46cd0346d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058620"
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a>ASP.NET Core 앱 배포용 Visual Studio 게시 프로필

작성자: [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="<= aspnetcore-1.1"

이 항목 1.1 버전의 경우 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필(버전 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/VS_Publish_Profiles_1.1.pdf)을 다운로드합니다.

::: moniker-end

이 문서에서는 Visual Studio 2017 이상을 사용하여 게시 프로필을 만들고 사용하는 방법에 초점을 맞춥니다. Visual Studio로 만들어진 게시 프로필은 MSBuild 및 Visual Studio에서 실행할 수 있습니다. Azure에 게시에 관한 지침은 [Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)를 참조하세요.

다음 프로젝트 파일은 `dotnet new mvc` 명령을 사용하여 만들어졌습니다.

::: moniker range=">= aspnetcore-2.2"

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.2</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>
```

::: moniker-end

`<Project>` 요소의 `Sdk` 특성은 다음 작업을 수행합니다.

* 시작 시 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props*에서 속성 파일을 가져옵니다.
* 종료 시 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets*에서 대상 파일을 가져옵니다.

`MSBuildSDKsPath`의 기본 위치(Visual Studio 2017 Enterprise 사용)는 *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* 폴더입니다.

`Microsoft.NET.Sdk.Web` SDK는 다음에 따라 달라집니다.

* *Microsoft.NET.Sdk.Web.ProjectSystem*
* *Microsoft.NET.Sdk.Publish*

이러한 항목은 다음 속성 및 대상을 가져옵니다.

* *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props*
* *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets*
* *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props*
* *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets*

게시 대상은 사용된 게시 방법에 따라 올바른 대상 집합을 가져옵니다.

MSBuild 또는 Visual Studio가 프로젝트를 로드하면 다음 높은 수준의 작업이 수행됩니다.

* 프로젝트 빌드
* 게시할 파일 계산
* 대상에 파일 게시

## <a name="compute-project-items"></a>프로젝트 항목 계산

프로젝트가 로드되면 프로젝트 항목(파일)이 계산됩니다. `item type` 특성에 따라 파일 처리 방법이 결정됩니다. 기본적으로 *.cs* 파일은 `Compile` 항목 목록에 포함됩니다. `Compile` 항목 목록의 파일이 컴파일됩니다.

`Content` 항목 목록에는 빌드 출력 이외에 게시될 파일이 포함됩니다. 기본적으로 패턴 `wwwroot/**`와 일치하는 파일은 `Content` 항목에 포함됩니다. [와일드카드 사용 패턴](https://gruntjs.com/configuring-tasks#globbing-patterns)인 `wwwroot/\*\*`는 *wwwroot* **및** 하위 폴더에서 모든 파일을 일치시킵니다. 게시 목록에 파일을 명시적으로 추가하려면 [포함 파일](#include-files)에 표시된 대로 *.csproj* 파일에서 직접 파일을 추가합니다.

Visual Studio에서 **게시** 단추를 선택하거나 명령줄에서 게시할 경우:

* 속성/항목이 계산됩니다(빌드하는 데 필요한 파일).
* **Visual Studio 전용**: NuGet 패키지가 복원됩니다. (CLI에서 사용자가 명시적으로 복원해야 합니다.)
* 프로젝트가 빌드됩니다.
* 게시 항목이 계산됩니다(게시하는 데 필요한 파일).
* 프로젝트가 게시됩니다(계산된 파일이 게시 대상에 복사됨).

ASP.NET Core 프로젝트가 프로젝트 파일의 `Microsoft.NET.Sdk.Web`을 참조하면 *app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다. 파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.

## <a name="basic-command-line-publishing"></a>기본 명령줄 게시

명령줄 게시는 모든 .NET Core 지원 플랫폼에 적용되며 Visual Studio가 필요하지 않습니다. 아래 샘플에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령은 *.csproj* 파일이 포함된 프로젝트 디렉터리에서 실행됩니다. 프로젝트 폴더에 없는 경우 프로젝트 파일 경로를 명시적으로 전달합니다. 예를 들어:

```console
dotnet publish C:\Webs\Web1
```

다음 명령을 실행하여 웹앱을 만들고 게시합니다.

```console
dotnet new mvc
dotnet publish
```

[dotnet publish](/dotnet/core/tools/dotnet-publish) 명령은 다음과 유사한 출력 결과를 표시합니다.

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

기본 게시 폴더는 `bin\$(Configuration)\netcoreapp<version>\publish`입니다. `$(Configuration)`의 기본값은 *Debug*입니다. 앞의 예제에서 `<TargetFramework>`는 `netcoreapp2.0`입니다.

`dotnet publish -h`는 게시에 대한 도움말 정보를 표시합니다.

다음 명령은 `Release` 빌드 및 게시 디렉터리를 지정합니다.

```console
dotnet publish -c Release -o C:\MyWebs\test
```

[dotnet publish](/dotnet/core/tools/dotnet-publish) 명령은 `Publish` 대상을 호출하는 MSBuild를 호출합니다. `dotnet publish` 및 MSBuild에 전달된 모든 매개 변수. `-c` 매개 변수는 `Configuration` MSBuild 속성에 매핑됩니다. `-o` 매개 변수는 `OutputPath`에 매핑됩니다.

다음 형식 중 하나를 사용하여 MSBuild 속성을 전달할 수 있습니다.

* `p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

다음 명령은 `Release` 빌드를 네트워크 공유에 게시합니다.

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

네트워크 공유는 슬래시(*//r8/*)를 사용하여 지정하고 모든 .NET Core 지원 플랫폼에서 작동합니다.

배포할 게시된 앱이 실행되고 있지 않은지 확인합니다. 앱이 실행 중이면 *publish* 폴더의 파일이 잠겨 있습니다. 잠긴 파일을 복사할 수 없으므로 배포를 수행할 수 없습니다.

## <a name="publish-profiles"></a>게시 프로필

이 섹션에서는 Visual Studio 2017 이상을 사용하여 게시 프로필을 만듭니다. 프로필이 만들어지면 Visual Studio 또는 명령줄에서 게시할 수 있습니다.

게시 프로필을 사용하면 게시 프로세스를 간소화할 수 있고 제한 없이 프로필을 사용할 수 있습니다. 다음 경로 중 하나를 선택하여 Visual Studio에서 게시 프로필을 만듭니다.

* 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.
* **빌드** 메뉴에서 **게시 {PROJECT NAME}** 를 선택합니다.

앱 기능 페이지의 **게시** 탭이 표시됩니다. 프로젝트에 게시 프로필이 없으면 다음 페이지가 표시됩니다.

![앱 기능 페이지의 게시 탭](visual-studio-publish-profiles/_static/az.png)

**폴더**를 선택할 경우 게시된 자산을 저장할 폴더 경로를 지정합니다. 기본 폴더는 *bin\Release\PublishOutput*입니다. **프로필 만들기** 단추를 클릭하여 완료합니다.

게시 프로필이 만들어지면 **게시** 탭이 변경됩니다. 새로 만들어진 프로필이 드롭다운 목록에 표시됩니다. **새 프로필 만들기**를 클릭하여 또 다른 새 프로필을 만듭니다.

![FolderProfile을 표시하는 앱 기능 페이지의 게시 탭](visual-studio-publish-profiles/_static/create_new.png)

게시 마법사는 다음 게시 대상을 지원합니다.

* Azure App Service
* Azure Virtual Machines
* IIS, FTP 등(웹 서버의 경우)
* 폴더
* 프로필 가져오기

자세한 내용은 [내게 적합한 게시 옵션](/visualstudio/ide/not-in-toc/web-publish-options)을 참조하세요.

Visual Studio를 사용하여 게시 프로필을 만들면 *Properties/PublishProfiles/{PROFILE NAME}.pubxml* MSBuild 파일이 만들어집니다. 이 *.pubxml* 파일은 MSBuild 파일이고 게시 구성 설정을 포함합니다. 이 파일을 변경하여 빌드 및 게시 프로세스를 사용자 지정할 수 있습니다. 게시 프로세스에서 이 파일을 읽습니다. `<LastUsedBuildConfiguration>`은 전역 속성이고 빌드에서 가져온 파일에 포함되면 안 되므로 특별합니다. 자세한 내용은 [MSBuild: 구성 속성을 설정하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)을 참조하세요.

Azure 대상에 게시하는 경우 *.pubxml* 파일에는 Azure 구독 식별자가 포함됩니다. 대상 유형을 사용할 경우 이 파일을 소스 제어에 추가하지 않는 것이 좋습니다. Azure 이외 대상에 게시하는 경우 *.pubxml* 파일을 체크 인해도 안전합니다.

중요 정보(예: 게시 암호)는 사용자/컴퓨터 수준별로 암호화됩니다. 이 정보는 *Properties/PublishProfiles/{PROFILE NAME}.pubxml.user* 파일에 저장됩니다. 중요 정보가 저장될 수 있는 파일이므로 소스 제어에 체크 인하면 안 됩니다.

ASP.NET Core에서 웹앱을 게시하는 방법에 대한 개요는 [호스트 및 배포](xref:host-and-deploy/index)를 참조하세요. ASP.NET Core 앱을 게시하는 데 필요한 MSBuild 작업 및 대상은 https://github.com/aspnet/websdk의 오픈 소스입니다.

`dotnet publish`는 MSDeploy 폴더와 [Kudu](https://github.com/projectkudu/kudu/wiki) 게시 프로필을 사용할 수 있습니다.

폴더(플랫폼 간에 작동):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>
```

MSDeploy(MSDeploy가 플랫폼 간이 아니기 때문에 현재 Windows에서만 작동):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

MSDeploy 패키지(MSDeploy가 플랫폼 간이 아니기 때문에 현재 Windows에서만 작동):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

위 샘플에서 `deployonbuild`를 `dotnet publish`에 전달하지 **마세요**.

자세한 내용은 [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)를 참조하세요.

`dotnet publish`는 모든 플랫폼에서 Azure에 게시하기 위해 Kudu API를 지원합니다. Visual Studio 게시는 Kudu API를 지원하지만 플랫폼 간 Azure에 게시에 대해 WebSDK에 의해 지원됩니다.

다음 콘텐츠와 함께 *Properties/PublishProfiles* 폴더에 게시 프로필을 추가합니다.

```xml
<Project>
  <PropertyGroup>
    <PublishProtocol>Kudu</PublishProtocol>
    <PublishSiteName>nodewebapp</PublishSiteName>
    <UserName>username</UserName>
    <Password>password</Password>
  </PropertyGroup>
</Project>
```

다음 명령을 실행하면 게시 콘텐츠가 압축되고 Kudu API를 사용하여 Azure에 게시됩니다.

```console
dotnet publish /p:PublishProfile=Azure /p:Configuration=Release
```

게시 프로필을 사용할 경우 다음 MSBuild 속성을 설정합니다.

* `DeployOnBuild=true`
* `PublishProfile={PUBLISH PROFILE}`

*FolderProfile*이라는 프로필을 사용하여 게시할 경우 다음 명령 중 하나를 실행할 수 있습니다.

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

[dotnet build](/dotnet/core/tools/dotnet-build)를 호출하면 이 명령은 `msbuild`를 호출하여 빌드 및 게시 프로세스를 실행합니다. 폴더 프로필을 전달할 경우 `dotnet build` 또는 `msbuild` 호출은 동일합니다. Windows에서 MSBuild를 직접 호출하면 MSBuild의 .NET Framework 버전이 사용됩니다. MSDeploy는 현재 게시를 위해 Windows 컴퓨터로 제한됩니다. 폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고 MSBuild는 폴더가 아닌 프로필에서 MSDeploy를 사용합니다. 폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고(MSDeploy 사용) Windows 플랫폼에서 실행될 경우에도 오류가 발생합니다. 폴더가 아닌 프로필을 사용하여 게시하려면 MSBuild를 직접 호출합니다.

다음 폴더 게시 프로필은 Visual Studio를 사용하여 만들어졌고 네트워크 공유에 게시됩니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework>netcoreapp1.1</PublishFramework>
    <ProjectGuid>c30c453c-312e-40c4-aec9-394a145dee0b</ProjectGuid>
    <publishUrl>\\r8\Release\AdminWeb</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
</Project>
```

`<LastUsedBuildConfiguration>`은 `Release`로 설정됩니다. Visual Studio에서 게시할 경우 `<LastUsedBuildConfiguration>` 구성 속성 값은 게시 프로세스가 시작될 때의 값을 사용하여 설정됩니다. `<LastUsedBuildConfiguration>` 구성 속성은 특별하고 가져온 MSBuild 파일에서 재정의되면 안 됩니다. 이 속성은 명령줄에서 재정의할 수 있습니다.

.NET Core CLI 사용:

```console
dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

MSBuild 사용:

```console
msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a>명령줄에서 MSDeploy 엔드포인트에 게시

다음 예제에서는 *AzureWebApp*라는 Visual Studio에서 만든 ASP.NET Core 웹앱을 사용합니다. Azure 게시 프로필이 Visual Studio에 추가되었습니다. 프로필을 만드는 방법에 대한 자세한 내용은 [게시 프로필](#publish-profiles) 섹션을 참조하세요.

게시 프로필을 사용하여 앱을 배포하려면 Visual Studio **개발자 명령 프롬프트**에서 `msbuild` 명령을 실행합니다. 명령 프롬프트는 Windows 작업 표시줄의 **시작** 메뉴에 있는 *Visual Studio* 폴더에서 사용할 수 있습니다. 쉽게 액세스할 수 있도록 Visual Studio의 **도구** 메뉴에 명령 프롬프트를 추가할 수 있습니다. 자세한 내용은 [Visual Studio용 개발자 명령 프롬프트](/dotnet/framework/tools/developer-command-prompt-for-vs#run-the-command-prompt-from-inside-visual-studio)를 참조하세요.

MSBuild는 다음 명령 구문을 사용합니다.

```console
msbuild {PATH} 
    /p:DeployOnBuild=true 
    /p:PublishProfile={PROFILE} 
    /p:Username={USERNAME} 
    /p:Password={PASSWORD}
```

* {PATH} &ndash; 앱의 프로젝트 파일 경로입니다.
* {PROFILE} &ndash; 게시 프로필의 이름입니다.
* {USERNAME} &ndash; MSDeploy 사용자 이름입니다. {USERNAME}은 게시 프로필에서 찾을 수 있습니다.
* {PASSWORD} &ndash; MSDeploy 암호입니다. *{PROFILE}.PublishSettings* 파일에서 {PASSWORD}를 가져옵니다. 다음 위치에서 *.PublishSettings* 파일을 다운로드합니다.
  * 솔루션 탐색기: **보기** > **클라우드 탐색기**를 선택합니다. Azure 구독으로 연결합니다. **App Services**를 엽니다. 앱을 마우스 오른쪽 단추로 클릭합니다. **게시 프로필 다운로드**를 선택합니다.
  * Azure Portal: 웹앱의 **개요** 패널에서 **게시 프로필 가져오기**를 선택합니다.

다음 예제에서는 *AzureWebApp - 웹 배포*라는 게시 프로필을 사용합니다.

```console
msbuild "AzureWebApp.csproj" 
    /p:DeployOnBuild=true 
    /p:PublishProfile="AzureWebApp - Web Deploy" 
    /p:Username="$AzureWebApp" 
    /p:Password=".........."
```

게시 프로필은 Windows 명령 프롬프트에서 .NET Core CLI [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild) 명령과 함께 사용할 수도 있습니다.

```console
dotnet msbuild "AzureWebApp.csproj"
    /p:DeployOnBuild=true 
    /p:PublishProfile="AzureWebApp - Web Deploy" 
    /p:Username="$AzureWebApp" 
    /p:Password=".........."
```

> [!NOTE]
> [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild) 명령은 플랫폼 간 사용할 수 있으며 macOS 및 Linux에서 ASP.NET Core 앱을 컴파일할 수 있습니다. 그러나 macOS 및 Linux의 MSBuild는 Azure 또는 다른 MSDeploy 앤드포인트에 앱을 배포할 수 없습니다. MSDeploy는 Windows에서만 사용할 수 있습니다.

## <a name="set-the-environment"></a>환경 변수를 설정합니다.

`<EnvironmentName>` 속성을 게시 프로필(*.pubxml*) 또는 프로젝트 파일에 포함하여 앱의 [환경](xref:fundamentals/environments)을 설정합니다.

```xml
<PropertyGroup>
  <EnvironmentName>Development</EnvironmentName>
</PropertyGroup>
```

*web.config* 변환(예: 구성, 프로필 또는 환경에 따라 환경 변수 설정)이 필요한 경우 <xref:host-and-deploy/iis/transform-webconfig>을 참조하세요.

## <a name="exclude-files"></a>파일 제외

ASP.NET Core 웹앱을 게시할 경우 *wwwroot* 폴더의 빌드 아티팩트 및 콘텐츠가 포함됩니다. `msbuild`는 [와일드카드 사용 패턴](https://gruntjs.com/configuring-tasks#globbing-patterns)을 지원합니다. 예를 들어 다음 `<Content>` 요소는 *wwwroot/content* 폴더와 모든 하위 폴더에서 모든 텍스트(*.txt*) 파일을 제외합니다.

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

앞의 태그는 게시 프로필 또는 *.csproj* 파일에 추가될 수 있습니다. *.csproj* 파일에 추가된 규칙은 프로젝트의 모든 게시 프로필에 추가됩니다.

다음 `<MsDeploySkipRules>` 요소는 *wwwroot/content* 폴더에서 모든 파일을 제외합니다.

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

`<MsDeploySkipRules>`는 배포 사이트에서 ‘건너뛰기’ 대상을 삭제하지 않습니다. `<Content>` 대상 파일 및 폴더는 배포 사이트에서 삭제됩니다. 예를 들어 배포된 웹앱에 다음 파일이 포함되었다고 가정합니다.

* *Views/Home/About1.cshtml*
* *Views/Home/About2.cshtml*
* *Views/Home/About3.cshtml*

다음 `<MsDeploySkipRules>` 요소가 추가되면 해당 파일은 배포 사이트에서 삭제되지 않습니다.

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

앞의 `<MsDeploySkipRules>` 요소는 ‘건너뛴’ 파일이 배포되지 않도록 합니다. 해당 파일은 배포된 후에 삭제되지 않습니다.

다음 `<Content>` 요소는 배포 사이트에서 대상 파일을 삭제합니다.

```xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

앞의 `<Content>` 요소와 함께 명령줄 배포를 사용하면 다음 출력이 생성됩니다.

```console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="include-files"></a>포함 파일

다음 태그는 게시 사이트의 *wwwroot/images* 폴더에 대한 프로젝트 디렉터리 외부에 *images* 폴더를 포함합니다.

```xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

태그는 *.csproj* 파일 또는 게시 프로필에 추가될 수 있습니다. 태그가 *.csproj* 파일에 추가되면 프로젝트의 각 게시 프로필에 포함됩니다.

다음 강조 표시된 태그는 방법을 표시합니다.

* 프로젝트 외부에서 *wwwroot* 폴더로 파일을 복사합니다.
* *wwwroot\Content* 폴더를 제외합니다.
* *Views\Home\About2.cshtml*을 제외합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework />
    <ProjectGuid>afa9f185-7ce0-4935-9da1-ab676229d68a</ProjectGuid>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
  <ItemGroup>
    <ResolvedFileToPublish Include="..\ReadMe2.MD">
      <RelativePath>wwwroot\ReadMe2.MD</RelativePath>
    </ResolvedFileToPublish>

    <Content Update="wwwroot\Content\**\*" CopyToPublishDirectory="Never" />
    <Content Update="Views\Home\About2.cshtml" CopyToPublishDirectory="Never" />

  </ItemGroup>
</Project>
```

더 많은 배포 샘플을 보려면 [WebSDK Readme](https://github.com/aspnet/websdk)(WebSDK 추가 정보)를 참조하세요.

## <a name="run-a-target-before-or-after-publishing"></a>게시 이전 또는 이후 대상 실행

기본 제공 `BeforePublish` 및 `AfterPublish` 대상은 게시 대상 이전 또는 이후에 대상을 실행합니다. 다음 요소를 게시 프로필에 추가하여 게시 이전 및 이후에 콘솔 메시지를 기록합니다.

```xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="publish-to-a-server-using-an-untrusted-certificate"></a>신뢰할 수 없는 인증서를 사용하여 서버에 게시

`True` 값을 사용하는 `<AllowUntrustedCertificate>` 속성을 게시 프로필에 추가합니다.

```xml
<PropertyGroup>
  <AllowUntrustedCertificate>True</AllowUntrustedCertificate>
</PropertyGroup>
```

## <a name="the-kudu-service"></a>Kudu 서비스

Azure App Service 웹앱 배포에 있는 파일을 보려면 [Kudu 서비스](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)를 사용합니다. `scm` 토큰을 웹앱 이름에 추가합니다. 예를 들어:

| URL                                    | 결과       |
| -------------------------------------- | ------------ |
| `http://mysite.azurewebsites.net/`     | 웹앱      |
| `http://mysite.scm.azurewebsites.net/` | Kudu 서비스 |

[디버그 콘솔](https://github.com/projectkudu/kudu/wiki/Kudu-console) 메뉴 항목을 선택하여 파일을 표시, 편집, 삭제 또는 추가합니다.

## <a name="additional-resources"></a>추가 자료

* [웹 배포](https://www.iis.net/downloads/microsoft/web-deploy)(MSDeploy)는 IIS 서버에 대한 웹앱 및 웹 사이트 배포를 간소화합니다.
* [https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): 배포에 대한 파일 문제 및 요청 기능.
* [Visual Studio에서 Azure VM에 ASP.NET 웹앱 게시](/azure/virtual-machines/windows/publish-web-app-from-visual-studio)
* <xref:host-and-deploy/iis/transform-webconfig>
