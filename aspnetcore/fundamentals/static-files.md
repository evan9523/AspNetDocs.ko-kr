---
title: ASP.NET Core의 고정 파일
author: rick-anderson
description: ASP.NET Core 웹앱에서 정적 파일을 제공 및 보호하고 정적 파일 호스팅 미들웨어 동작을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: fundamentals/static-files
ms.openlocfilehash: e6bda5dd60c62c7bdbfa81f34c14cfcd07e8d700
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042160"
---
# <a name="static-files-in-aspnet-core"></a>ASP.NET Core의 고정 파일

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Scott Addie](https://twitter.com/Scott_Addie)

HTML, CSS, 이미지 및 JavaScript와 같은 정적 파일은 ASP.NET Core 앱이 클라이언트에 직접 제공하는 자산입니다. 일부 구성은 이러한 파일을 제공하는 데 필수적입니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="serve-static-files"></a>정적 파일 제공

정적 파일은 프로젝트의 웹 루트 디렉터리 내에 저장됩니다. 기본 디렉터리는 *\<content_root>/wwwroot*이지만, [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) 메서드를 통해 변경할 수 있습니다. 자세한 정보는 [콘텐츠 루트](xref:fundamentals/index#content-root) 및 [웹 루트](xref:fundamentals/index#web-root)를 참조하세요.

앱의 웹 호스트에서 콘텐츠 루트 디렉터리를 인식하도록 해야 합니다.

::: moniker range=">= aspnetcore-2.0"

`WebHost.CreateDefaultBuilder` 메서드는 콘텐츠 루트를 현재 디렉터리로 설정합니다.

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

`Program.Main` 내부에 있는 [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_)를 호출하여 콘텐츠 루트를 현재 디렉터리로 설정합니다.

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

::: moniker-end

정적 파일은 웹 루트를 기준으로 하는 경로를 통해 액세스할 수 있습니다. 예를 들어 **웹 애플리케이션** 프로젝트 템플릿에는 *wwwroot* 폴더 내에 여러 폴더를 포함합니다.

* **wwwroot**
  * **css**
  * **images**
  * **js**

*images* 하위 폴더에 있는 파일에 액세스하기 위한 URI 형식은 *http://\<server_address>/images/\<image_file_name>* 입니다. 예: *http://localhost:9189/images/banner3.svg*.

::: moniker range=">= aspnetcore-2.1"

.NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 패키지를 프로젝트에 추가합니다. .NET Core를 대상으로 하는 경우 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 이 패키지가 포함됩니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

.NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 패키지를 프로젝트에 추가합니다. .NET Core를 대상으로 하는 경우는 [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)가 이 패키지를 포함합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 패키지를 프로젝트에 추가합니다.

::: moniker-end

정적 파일을 제공할 수 있도록 [미들웨어](xref:fundamentals/middleware/index)를 구성합니다.

### <a name="serve-files-inside-of-web-root"></a>웹 루트 내부에 있는 파일을 제공합니다

`Startup.Configure` 내부에 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드를 호출합니다.

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

매개 변수가 없는 `UseStaticFiles` 메서드 오버로드는 웹 루트에 있는 파일을 제공 가능으로 표시합니다. 다음 표시는 *wwwroot/images/banner1.svg*를 참조합니다.

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

위의 코드에서 물결표 문자 `~/`는 webroot를 가리킵니다. 자세한 내용은 [웹 루트](xref:fundamentals/index#web-root)를 참조하세요.

### <a name="serve-files-outside-of-web-root"></a>웹 루트 외부에 있는 파일을 제공합니다

제공할 정적 파일이 웹 루트 외부에 있는 디렉터리 계층 구조를 고려합니다.

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*

요청은 정적 파일 미들웨어를 다음과 같이 구성하여 *banner1.svg* 파일에 액세스할 수 있습니다.

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

위의 코드에서 *MyStaticFiles* 디렉터리 계층 구조가 *StaticFiles* URI 세그먼트를 통해 공개적으로 노출됩니다. *http://\<server_address>/StaticFiles/images/banner1.svg*에 대한 요청은 *banner1.svg* 파일을 제공합니다.

다음 표시는 *MyStaticFiles/images/banner1.svg*를 참조합니다.

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a>HTTP 응답 헤더 설정

[StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) 개체는 HTTP 응답 헤더를 설정하는 데 사용할 수 있습니다. 웹 루트에서 제공되는 정적 파일을 구성하는 것 외에도 다음 코드는 `Cache-Control` 헤더를 설정합니다.

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) 메서드는 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 패키지에 있습니다.

개발 환경에서 파일은 10분(600초) 동안 공개적으로 캐시할 수 있습니다.

![추가된 캐시 제어 헤더를 보여 주는 응답 헤더](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a>정적 파일 권한 부여

정적 파일 미들웨어는 권한 부여 검사를 제공하지 않습니다. *wwwroot* 아래의 항목을 비롯한 제공되는 모든 파일은 공개적으로 사용할 수 있습니다. 권한 부여를 기준으로 파일을 제공하려면 다음을 수행합니다.

* *wwwroot* 외부의 항목 및 정적 파일 미들웨어에 액세스할 수 있는 모든 디렉터리를 저장합니다.
* 권한 부여가 적용되는 동작 메서드를 통해 제공합니다. [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) 개체를 반환합니다.

  [!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a>디렉터리 검색 사용

디렉터리 검색을 사용하면 웹앱 사용자가 지정된 디렉터리 내 디렉터리 목록 및 파일을 볼 수 있습니다. 기본적으로 디렉터리 검색은 보안상의 이유로 비활성화되어 있습니다([고려할 사항](#considerations) 참조). `Startup.Configure`에서 [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) 메서드를 호출하여 디렉터리 검색을 사용하도록 설정합니다.

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

`Startup.ConfigureServices`에서 [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 메서드를 호출하여 필요한 서비스를 추가합니다.

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

위의 코드를 통해 각 파일 및 폴더에 대한 링크가 있는 URL *http://\<server_address>/MyImages*를 사용하여 *wwwroot/images* 폴더의 디렉터리 검색을 사용할 수 있습니다.

![디렉터리 검색](static-files/_static/dir-browse.png)

검색을 활성화하는 경우 보안 위험에 대한 [고려할 사항](#considerations)을 참조하세요.

다음 예제에서 두 `UseStaticFiles` 호출을 참고하세요. 첫 번째 호출은 *wwwroot* 폴더에서 정적 파일 제공을 사용하도록 설정합니다. 두 번째 호출은 URL *http://\<server_address>/MyImages*를 사용하여 *wwwroot/images* 폴더의 디렉터리 검색을 활성화합니다.

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a>기본 문서 제공

기본 홈페이지를 설정하면 방문자가 사이트를 방문할 때 논리적 시작점을 제공합니다. URI를 정규화하는 사용자 없이 기본 페이지를 제공하려면 `Startup.Configure`에서 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드를 호출합니다.

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> `UseStaticFiles`가 기본 파일을 제공하기 전에 `UseDefaultFiles`를 먼저 호출해야 합니다. `UseDefaultFiles`는 파일을 실제로 제공하지 않는 URL 재작성기입니다. 파일을 제공하도록 `UseStaticFiles`를 통해 정적 파일 미들웨어를 활성화합니다.

`UseDefaultFiles`를 사용하여 다음에 대한 폴더 검색을 요청합니다.

* *default.htm*
* *default.html*
* *index.htm*
* *index.html*

목록에서 첫 번째 파일이 마치 요청이 정규화된 URI인 것처럼 제공됩니다. 브라우저 URL이 요청된 URI를 계속 반영합니다.

다음 코드는 기본 파일 이름을 *mydefault.html*로 변경합니다.

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a>UseFileServer

[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_)는 `UseStaticFiles`, `UseDefaultFiles` 및 `UseDirectoryBrowser`의 기능을 결합합니다.

다음 코드는 정적 파일의 제공 및 기본 파일을 활성화합니다. 디렉터리 검색 기능이 활성화되지 않았습니다.

```csharp
app.UseFileServer();
```

다음 코드는 매개 변수가 없는 오버로드에서 디렉터리 검색을 활성화하여 빌드합니다.

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

다음 디렉터리 계층 구조를 고려합니다.

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*
  * *default.html*

다음 코드는 정적 파일, 기본 파일 및 `MyStaticFiles`의 디렉터리 검색을 활성화합니다.

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

`EnableDirectoryBrowsing` 속성 값이 `true`인 경우 `AddDirectoryBrowser`를 호출해야 합니다.

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

URL은 파일 계층 구조 및 이전 코드를 사용하여 다음과 같이 확인합니다.

| URI            |                             응답  |
| ------- | ------|
| *http://\<server_address>/StaticFiles/images/banner1.svg*    |      MyStaticFiles/images/banner1.svg |
| *http://\<server_address>/StaticFiles*             |     MyStaticFiles/default.html |

*MyStaticFiles* 디렉터리에 기본 이름이 지정된 파일이 없는 경우 *http://\<server_address>/StaticFiles*는 클릭 가능한 링크와 함께 디렉터리 목록을 반환합니다.

![정적 파일 목록](static-files/_static/db2.png)

> [!NOTE]
> `UseDefaultFiles` 및 `UseDirectoryBrowser`는 후행 슬래시가 없는 URL *http://\<server_address>/StaticFiles*를 사용하여 *http://\<server_address>/StaticFiles/* 로의 클라이언트 쪽 리디렉션을 트리거합니다. 후행 슬래시 추가를 확인하세요. 문서 내에서 상대 URL은 후행 슬래시가 없는 잘못된 것으로 간주됩니다.

## <a name="fileextensioncontenttypeprovider"></a>FileExtensionContentTypeProvider

[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) 클래스는 MIME 콘텐츠 형식에 대한 파일 확장명 매핑 역할을 수행하는 `Mappings` 속성을 포함합니다. 다음 샘플에서는 여러 파일 확장명이 알려진 MIME 형식에 등록됩니다. *.rtf* 확장은 대체되며 *.mp4*는 제거됩니다.

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

[MIME 콘텐츠 형식](http://www.iana.org/assignments/media-types/media-types.xhtml)을 참조하세요.

## <a name="non-standard-content-types"></a>비표준 콘텐츠 형식

정적 파일 미들웨어는 거의 400가지의 알려진 파일 콘텐츠 형식을 이해합니다. 사용자가 알 수 없는 파일 형식의 파일을 요청하는 경우 정적 파일 미들웨어가 해당 요청을 파이프라인의 다음 미들웨어로 전달합니다. 요청을 처리한 미들웨어가 없으면 ‘404 찾을 수 없음’ 응답이 반환됩니다. 디렉터리 찾아보기가 사용 가능한 경우 파일에 대한 링크가 디렉터리 목록에 표시됩니다.

다음 코드는 알 수 없는 형식 제공을 사용하도록 설정하고 알 수 없는 파일을 이미지로 렌더링합니다.

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

위의 코드를 사용하면 알 수 없는 콘텐츠 형식인 파일에 대한 요청은 이미지로 반환됩니다.

> [!WARNING]
> [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes)를 사용하도록 설정하면 보안 위험이 발생합니다. 기본적으로 비활성화되어 있으며 사용은 권장되지 않습니다. [FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider)는 비표준 확장명을 가진 파일을 제공하는 것보다 안전한 대체 방법을 제공합니다.

### <a name="considerations"></a>고려 사항

> [!WARNING]
> `UseDirectoryBrowser` 및 `UseStaticFiles`는 비밀 정보를 누출 할 수 있습니다. 프로덕션 환경에서 디렉터리 검색을 비활성화하는 것이 좋습니다. `UseStaticFiles` 또는 `UseDirectoryBrowser`를 통해 어떤 디렉터리가 활성화되었는지 주의 깊게 검토합니다. 전체 디렉터리와 해당 하위 디렉터리는 공개적으로 액세스할 수 있습니다. *\<content_root>/wwwroot*와 같이 전용 디렉터리에 공개적으로 제공하는 데 적합한 파일을 저장합니다. MVC 뷰, Razor 페이지(2.x에만 해당), 구성 파일 등으로 이러한 파일을 구분합니다.

* `UseDirectoryBrowser` 및 `UseStaticFiles`로 노출된 콘텐츠에 대한 URL은 대/소문자 구분 및 기본 파일 시스템의 문자 제한이 적용됩니다. 예를 들어 Windows는 대/소문자를 구분하지 않는 반면 macOS 및 Linux는 그렇지 않습니다.

* IIS에서 호스팅되는 ASP.NET Core 앱은 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 사용하여 정적 파일 요청을 비롯한 모든 요청을 앱에 전달합니다. IIS 정적 파일 처리기는 사용되지 않습니다. 모듈에서 처리하기 전에는 요청을 처리할 수 없습니다.

* 서버 또는 웹 사이트 수준에서 IIS 정적 파일 처리기를 제거하려면 IIS 관리자에서 다음 단계를 완료합니다.
    1. **모듈** 기능으로 이동합니다.
    1. 목록에서 **StaticFileModule**을 선택합니다.
    1. **동작** 사이드바에서 **제거**를 클릭합니다.

> [!WARNING]
> IIS 정적 파일 처리기가 사용되도록 설정된 경우 **및** ASP.NET Core 모듈이 올바르게 구성된 경우, 정적 파일이 제공됩니다. 이는 예를 들어 *web.config* 파일이 배포되지 않는 경우에 발생합니다.

* 코드 파일(*.cs* 및 *.cshtml* 포함)을 앱 프로젝트의 웹 루트 외부에 배치합니다. 따라서 논리적 분리가 앱의 클라이언트 쪽 콘텐츠 및 서버 기반 코드 사이에 만들어집니다. 그러면 서버 쪽 코드가 유출되지 않습니다.

## <a name="additional-resources"></a>추가 자료

* [미들웨어](xref:fundamentals/middleware/index)
* [ASP.NET Core 소개](xref:index)
