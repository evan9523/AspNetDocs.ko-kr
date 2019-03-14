---
title: ASP.NET Core에서 개발 앱 암호의 안전한 저장소
author: rick-anderson
description: 저장 하 고 ASP.NET Core 앱을 개발 하는 동안 앱 암호 '로 중요 한 정보를 검색 하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 01/31/2019
uid: security/app-secrets
ms.openlocfilehash: eaa2e9d1ba98d391a29a9ff55872d062df016b87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030150"
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="c118f-103">ASP.NET Core에서 개발 앱 암호의 안전한 저장소</span><span class="sxs-lookup"><span data-stu-id="c118f-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="c118f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="c118f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="c118f-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="c118f-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="c118f-106">이 문서에 저장 하 고 ASP.NET Core 앱을 개발 하는 동안 중요 한 데이터를 검색 하는 기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-106">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="c118f-107">소스 코드에서 암호 또는 기타 중요 한 데이터를 저장 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c118f-107">Never store passwords or other sensitive data in source code.</span></span> <span data-ttu-id="c118f-108">프로덕션 비밀을 사용할 수 없습니다 개발 또는 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-108">Production secrets shouldn't be used for development or test.</span></span> <span data-ttu-id="c118f-109">[Azure Key Vault 구성 제공자](xref:security/key-vault-configuration)로 Azure 테스트 및 프로덕션 암호를 저장하고 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-109">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="c118f-110">환경 변수</span><span class="sxs-lookup"><span data-stu-id="c118f-110">Environment variables</span></span>

<span data-ttu-id="c118f-111">환경 변수는 로컬 구성 파일 또는 코드에서의 앱 비밀 저장소를 방지 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-111">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="c118f-112">환경 변수는 모든 이전에 지정한 구성 원본에 대 한 구성 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-112">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="c118f-113">호출 하 여 환경 변수 값을 읽는 구성 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) 에 `Startup` 생성자:</span><span class="sxs-lookup"><span data-stu-id="c118f-113">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=8)]

::: moniker-end

<span data-ttu-id="c118f-114">ASP.NET Core 웹 앱을는 것이 좋습니다 **개별 사용자 계정** 보안이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-114">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="c118f-115">프로젝트의 기본 데이터베이스 연결 문자열을 있기 *appsettings.json* 키를 사용 하 여 파일 `DefaultConnection`합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-115">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="c118f-116">기본 연결 문자열은 사용자 모드에서 실행 되는 암호가 필요 하며 LocalDB입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-116">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="c118f-117">앱 배포 하는 동안는 `DefaultConnection` 환경 변수의 값을 사용 하 여 키 값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-117">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="c118f-118">환경 변수는 중요 한 자격 증명을 사용 하 여 전체 연결 문자열을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-118">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="c118f-119">환경 변수는 암호화 되지 않은 일반 텍스트에 일반적으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-119">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="c118f-120">컴퓨터 또는 프로세스가 손상 된 경우 환경 변수는 신뢰할 수 없는 당사자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-120">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="c118f-121">사용자 암호의 공개 되지 않도록 추가 조치가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-121">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="c118f-122">암호 관리자</span><span class="sxs-lookup"><span data-stu-id="c118f-122">Secret Manager</span></span>

<span data-ttu-id="c118f-123">암호 관리자 도구는 ASP.NET Core 프로젝트를 개발 하는 동안 중요 한 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-123">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="c118f-124">이 컨텍스트에서 중요 한 데이터의 일부는 앱 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-124">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="c118f-125">앱 암호는 별도 프로젝트 트리 위치에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-125">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="c118f-126">앱 암호를 특정 프로젝트와 연결 된 또는 여러 프로젝트 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-126">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="c118f-127">앱 암호를 소스 제어에 체크 인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-127">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="c118f-128">암호 관리자 도구는 저장 된 비밀을 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 간주 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-128">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="c118f-129">개발 목적 으로만입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-129">It's for development purposes only.</span></span> <span data-ttu-id="c118f-130">키와 값은 사용자 프로필 디렉터리에는 JSON 구성 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-130">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="c118f-131">암호 관리자 도구 작동 원리</span><span class="sxs-lookup"><span data-stu-id="c118f-131">How the Secret Manager tool works</span></span>

<span data-ttu-id="c118f-132">암호 관리자 도구를 같은 값을 저장 하는 위치와 방법을 구현 세부 정보를 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-132">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="c118f-133">이러한 구현 세부 정보를 알 필요 없이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-133">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="c118f-134">값은 로컬 컴퓨터의 시스템 보호 된 사용자 프로필 폴더에 JSON 구성 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-134">The values are stored in a JSON configuration file in a system-protected user profile folder on the local machine:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="c118f-135">Windows</span><span class="sxs-lookup"><span data-stu-id="c118f-135">Windows</span></span>](#tab/windows)

<span data-ttu-id="c118f-136">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="c118f-136">File system path:</span></span>

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[<span data-ttu-id="c118f-137">macOS</span><span class="sxs-lookup"><span data-stu-id="c118f-137">macOS</span></span>](#tab/macos)

<span data-ttu-id="c118f-138">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="c118f-138">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[<span data-ttu-id="c118f-139">Linux</span><span class="sxs-lookup"><span data-stu-id="c118f-139">Linux</span></span>](#tab/linux)

<span data-ttu-id="c118f-140">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="c118f-140">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

<span data-ttu-id="c118f-141">앞의 파일 경로, 대체 `<user_secrets_id>` 사용 하 여 합니다 `UserSecretsId` 에 지정 된 값을 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-141">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="c118f-142">위치 또는 암호 관리자 도구를 사용 하 여 저장 된 데이터의 형식에 의존 하는 코드를 작성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c118f-142">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="c118f-143">이러한 구현 세부 정보를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-143">These implementation details may change.</span></span> <span data-ttu-id="c118f-144">예를 들어, 비밀 값을 암호화 되지 않습니다 하지만 나중에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-144">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"

## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="c118f-145">암호 관리자 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-145">Install the Secret Manager tool</span></span>

<span data-ttu-id="c118f-146">암호 관리자 도구는.NET Core SDK 2.1.300에서에서.NET Core CLI와 함께 번들로 묶은 이상.</span><span class="sxs-lookup"><span data-stu-id="c118f-146">The Secret Manager tool is bundled with the .NET Core CLI in .NET Core SDK 2.1.300 or later.</span></span> <span data-ttu-id="c118f-147">.NET Core SDK 2.1.300 이전 버전의 경우 도구 설치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-147">For .NET Core SDK versions before 2.1.300, tool installation is necessary.</span></span>

> [!TIP]
> <span data-ttu-id="c118f-148">실행 `dotnet --version` 명령 셸을 설치 된.NET Core SDK 버전 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-148">Run `dotnet --version` from a command shell to see the installed .NET Core SDK version number.</span></span>

<span data-ttu-id="c118f-149">사용 중인.NET Core SDK 도구를 포함 하는 경우 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-149">A warning is displayed if the .NET Core SDK being used includes the tool:</span></span>

```console
The tool 'Microsoft.Extensions.SecretManager.Tools' is now included in the .NET Core SDK. Information on resolving this warning is available at (https://aka.ms/dotnetclitools-in-box).
```

<span data-ttu-id="c118f-150">설치 합니다 [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 프로젝트에 NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="c118f-150">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project.</span></span> <span data-ttu-id="c118f-151">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c118f-151">For example:</span></span>

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=15-16)]

<span data-ttu-id="c118f-152">도구 설치를 확인 하려면 명령 셸에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-152">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="c118f-153">암호 관리자 도구 샘플 사용법, 옵션 및 명령 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-153">The Secret Manager tool displays sample usage, options, and command help:</span></span>

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> <span data-ttu-id="c118f-154">동일한 디렉터리에 있어야 합니다 *.csproj* 파일에 정의 된 도구를 실행 하는 *.csproj* 파일의 `DotNetCliToolReference` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-154">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>

::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="c118f-155">암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-155">Set a secret</span></span>

<span data-ttu-id="c118f-156">암호 관리자 도구는 사용자 프로필에 저장 된 프로젝트 관련 구성 설정에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-156">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="c118f-157">사용자 암호를 사용 하려면 정의 `UserSecretsId` 내의 요소를 `PropertyGroup` 의 합니다 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-157">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="c118f-158">변수의 `UserSecretsId` 는 임의적 이지만 프로젝트에 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-158">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="c118f-159">개발자는 일반적으로 GUID를 생성할는 `UserSecretsId`합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-159">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

> [!TIP]
> <span data-ttu-id="c118f-160">Visual Studio에서 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 암호 관리** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-160">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="c118f-161">이 제스처 추가 `UserSecretsId` 에 채워진 GUID를 사용 하 여 요소를 *.csproj* 파일.</span><span class="sxs-lookup"><span data-stu-id="c118f-161">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="c118f-162">Visual Studio가 열립니다는 *secrets.json* 파일을 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="c118f-162">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="c118f-163">내용을 바꿉니다 *secrets.json* 저장할 키-값 쌍을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-163">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="c118f-164">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c118f-164">For example:</span></span>
> ```json
> {
>   "Movies": {
>     "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true",
>     "ServiceApiKey": "12345"
>   }
> }
> ```
> <span data-ttu-id="c118f-165">JSON 구조를 통해 수정 후 결합 됩니다 `dotnet user-secrets remove` 또는 `dotnet user-secrets set`합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-165">The JSON structure is flattened after modifications via `dotnet user-secrets remove` or `dotnet user-secrets set`.</span></span> <span data-ttu-id="c118f-166">예를 들어, 실행 중인 `dotnet user-secrets remove "Movies:ConnectionString"` 축소는 `Movies` 개체 리터럴.</span><span class="sxs-lookup"><span data-stu-id="c118f-166">For example, running `dotnet user-secrets remove "Movies:ConnectionString"` collapses the `Movies` object literal.</span></span> <span data-ttu-id="c118f-167">수정된 된 파일에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-167">The modified file resembles the following:</span></span>
> ```json
> {
>   "Movies:ServiceApiKey": "12345"
> }
> ```

<span data-ttu-id="c118f-168">키 및 해당 값으로 구성 된 앱 암호를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-168">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="c118f-169">암호는 프로젝트와 연결 된 `UserSecretsId` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-169">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="c118f-170">예를 들어 있는 디렉터리에서 다음 명령을 실행 합니다 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-170">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="c118f-171">앞의 예제에서 콜론 나타냅니다 `Movies` 는 개체를 사용 하 여 리터럴는 `ServiceApiKey` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-171">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="c118f-172">암호 관리자 도구는 너무 다른 디렉터리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-172">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="c118f-173">사용 합니다 `--project` 는 파일 시스템 경로 제공 하는 옵션을 *.csproj* 파일이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-173">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="c118f-174">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c118f-174">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="c118f-175">여러 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-175">Set multiple secrets</span></span>

<span data-ttu-id="c118f-176">JSON에 파이프 하 여 비밀의 일괄 처리를 설정할 수 있습니다는 `set` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-176">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="c118f-177">다음 예제에서는 *input.json* 파일의 내용으로 파이프 되는 `set` 명령.</span><span class="sxs-lookup"><span data-stu-id="c118f-177">In the following example, the *input.json* file's contents are piped to the `set` command.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="c118f-178">Windows</span><span class="sxs-lookup"><span data-stu-id="c118f-178">Windows</span></span>](#tab/windows)

<span data-ttu-id="c118f-179">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-179">Open a command shell, and execute the following command:</span></span>

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[<span data-ttu-id="c118f-180">macOS</span><span class="sxs-lookup"><span data-stu-id="c118f-180">macOS</span></span>](#tab/macos)

<span data-ttu-id="c118f-181">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-181">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[<span data-ttu-id="c118f-182">Linux</span><span class="sxs-lookup"><span data-stu-id="c118f-182">Linux</span></span>](#tab/linux)

<span data-ttu-id="c118f-183">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-183">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a><span data-ttu-id="c118f-184">비밀에 액세스</span><span class="sxs-lookup"><span data-stu-id="c118f-184">Access a secret</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="c118f-185">합니다 [ASP.NET Core 구성 API](xref:fundamentals/configuration/index) 암호 관리자 암호에 대 한 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-185">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="c118f-186">프로젝트가.NET Framework를 대상으로 하는 경우 설치 합니다 [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="c118f-186">If your project targets the .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="c118f-187">ASP.NET Core 2.0 이상에서는 사용자 비밀 구성 소스는 자동으로 추가 개발 모드에서 프로젝트를 호출 하는 경우 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 미리 구성 된 기본값을 사용 하 여 호스트의 새 인스턴스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-187">In ASP.NET Core 2.0 or later, the user secrets configuration source is automatically added in development mode when the project calls <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> to initialize a new instance of the host with preconfigured defaults.</span></span> <span data-ttu-id="c118f-188">`CreateDefaultBuilder` 호출 <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> 때 합니다 <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName> 는 <xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span><span class="sxs-lookup"><span data-stu-id="c118f-188">`CreateDefaultBuilder` calls <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> when the <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName> is <xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]

<span data-ttu-id="c118f-189">때 `CreateDefaultBuilder` 되지 호출 하 여 사용자 비밀 구성 소스를 명시적으로 추가 호출 <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> 에 `Startup` 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-189">When `CreateDefaultBuilder` isn't called, add the user secrets configuration source explicitly by calling <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> in the `Startup` constructor.</span></span> <span data-ttu-id="c118f-190">호출 `AddUserSecrets` 만 앱에서에서 실행 될 때 개발 환경에서는 다음 예제에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="c118f-190">Call `AddUserSecrets` only when the app runs in the Development environment, as shown in the following example:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="c118f-191">합니다 [ASP.NET Core 구성 API](xref:fundamentals/configuration/index) 암호 관리자 암호에 대 한 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-191">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="c118f-192">설치 합니다 [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="c118f-192">Install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="c118f-193">호출 하 여 사용자 비밀 구성 소스를 추가 [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) 에 `Startup` 생성자:</span><span class="sxs-lookup"><span data-stu-id="c118f-193">Add the user secrets configuration source with a call to [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

<span data-ttu-id="c118f-194">사용자 암호를 통해 검색할 수는 `Configuration` API:</span><span class="sxs-lookup"><span data-stu-id="c118f-194">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=26)]

::: moniker-end

## <a name="map-secrets-to-a-poco"></a><span data-ttu-id="c118f-195">POCO에 비밀을 맵</span><span class="sxs-lookup"><span data-stu-id="c118f-195">Map secrets to a POCO</span></span>

<span data-ttu-id="c118f-196">전체 개체 리터럴에 POCO (속성을 사용 하 여 간단한.NET 클래스)에 매핑하는 관련된 속성을 집계 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-196">Mapping an entire object literal to a POCO (a simple .NET class with properties) is useful for aggregating related properties.</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="c118f-197">이전 암호를 POCO에 매핑할을 사용 합니다 `Configuration` API [graph 바인딩 개체](xref:fundamentals/configuration/index#bind-to-an-object-graph) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-197">To map the preceding secrets to a POCO, use the `Configuration` API's [object graph binding](xref:fundamentals/configuration/index#bind-to-an-object-graph) feature.</span></span> <span data-ttu-id="c118f-198">다음 코드를 사용자 지정 바인딩할 `MovieSettings` POCO 및 액세스는 `ServiceApiKey` 속성 값:</span><span class="sxs-lookup"><span data-stu-id="c118f-198">The following code binds to a custom `MovieSettings` POCO and accesses the `ServiceApiKey` property value:</span></span>

::: moniker range=">= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

::: moniker range="= aspnetcore-1.0"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

<span data-ttu-id="c118f-199">합니다 `Movies:ConnectionString` 하 고 `Movies:ServiceApiKey` 비밀의 각 속성에 매핑됩니다. `MovieSettings`:</span><span class="sxs-lookup"><span data-stu-id="c118f-199">The `Movies:ConnectionString` and `Movies:ServiceApiKey` secrets are mapped to the respective properties in `MovieSettings`:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Models/MovieSettings.cs?name=snippet_MovieSettingsClass)]

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="c118f-200">암호를 사용 하 여 문자열 대체</span><span class="sxs-lookup"><span data-stu-id="c118f-200">String replacement with secrets</span></span>

<span data-ttu-id="c118f-201">암호를 일반 텍스트로 저장 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-201">Storing passwords in plain text is insecure.</span></span> <span data-ttu-id="c118f-202">데이터베이스 연결 문자열에 저장 하는 예를 들어 *appsettings.json* 지정된 된 사용자에 대 한 암호를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-202">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="c118f-203">보다 안전한 방법은 암호로 암호를 저장 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-203">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="c118f-204">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c118f-204">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="c118f-205">제거 된 `Password` 연결 문자열에서 키-값 쌍 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-205">Remove the `Password` key-value pair from the connection string in *appsettings.json*.</span></span> <span data-ttu-id="c118f-206">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c118f-206">For example:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="c118f-207">암호의 값에 설정할 수는 [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) 개체의 [암호](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) 연결 문자열을 완료 하는 속성:</span><span class="sxs-lookup"><span data-stu-id="c118f-207">The secret's value can be set on a [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) object's [Password](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) property to complete the connection string:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-17)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=26-29)]

::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="c118f-208">암호 나열</span><span class="sxs-lookup"><span data-stu-id="c118f-208">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="c118f-209">디렉터리에서 다음 명령을 실행 합니다 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-209">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="c118f-210">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-210">The following output appears:</span></span>

```console
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
Movies:ServiceApiKey = 12345
```

<span data-ttu-id="c118f-211">키 이름에 콜론 앞의 예제에서 내에서 개체 계층 구조를 나타냅니다 *secrets.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-211">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="c118f-212">단일 암호를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-212">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="c118f-213">디렉터리에서 다음 명령을 실행 합니다 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-213">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="c118f-214">앱의 *secrets.json* 와 연결 된 키-값 쌍을 제거 하려면 파일을 수정한는 `MoviesConnectionString` 키:</span><span class="sxs-lookup"><span data-stu-id="c118f-214">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="c118f-215">실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-215">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="c118f-216">모든 암호를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-216">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="c118f-217">디렉터리에서 다음 명령을 실행 합니다 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-217">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="c118f-218">앱에 대 한 모든 사용자 암호에서 삭제 합니다 *secrets.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="c118f-218">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="c118f-219">실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c118f-219">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="c118f-220">추가 자료</span><span class="sxs-lookup"><span data-stu-id="c118f-220">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>
