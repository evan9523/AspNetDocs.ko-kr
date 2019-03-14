---
title: ASP.NET Core 2.1의 새로운 기능
author: isaac2004
description: ASP.NET Core 2.1의 새로운 기능에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: aspnetcore-2.1
ms.openlocfilehash: 8299af819f86d3d2371650ce3d87deb817f0feb8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058490"
---
# <a name="whats-new-in-aspnet-core-21"></a><span data-ttu-id="2fe84-103">ASP.NET Core 2.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="2fe84-103">What's new in ASP.NET Core 2.1</span></span>

<span data-ttu-id="2fe84-104">이 아티클에서는 ASP.NET Core 2.1의 가장 큰 변경 내용을 중점적으로 설명하고 관련 문서의 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-104">This article highlights the most significant changes in ASP.NET Core 2.1, with links to relevant documentation.</span></span>

## <a name="signalr"></a><span data-ttu-id="2fe84-105">SignalR</span><span class="sxs-lookup"><span data-stu-id="2fe84-105">SignalR</span></span>

<span data-ttu-id="2fe84-106">SignalR은 ASP.NET Core 2.1에서 다시 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-106">SignalR has been rewritten for ASP.NET Core 2.1.</span></span> <span data-ttu-id="2fe84-107">ASP.NET Core SignalR에는 여러 향상된 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-107">ASP.NET Core SignalR includes a number of improvements:</span></span>

* <span data-ttu-id="2fe84-108">간소화된 스케일 아웃 모델</span><span class="sxs-lookup"><span data-stu-id="2fe84-108">A simplified scale-out model.</span></span>
* <span data-ttu-id="2fe84-109">JQuery에 종속되지 않는 새 JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fe84-109">A new JavaScript client with no jQuery dependency.</span></span>
* <span data-ttu-id="2fe84-110">MessagePack에 기반한 새로운 초소형 이진 프로토콜</span><span class="sxs-lookup"><span data-stu-id="2fe84-110">A new compact binary protocol based on MessagePack.</span></span>
* <span data-ttu-id="2fe84-111">사용자 지정 프로토콜에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="2fe84-111">Support for custom protocols.</span></span>
* <span data-ttu-id="2fe84-112">새 스트리밍 응답 모델</span><span class="sxs-lookup"><span data-stu-id="2fe84-112">A new streaming response model.</span></span>
* <span data-ttu-id="2fe84-113">기본 Websocket에 기반한 클라이언트에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="2fe84-113">Support for clients based on bare WebSockets.</span></span>

<span data-ttu-id="2fe84-114">자세한 내용은 [ASP.NET Core SignalR](xref:signalr/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-114">For more information, see [ASP.NET Core SignalR](xref:signalr/index).</span></span>

## <a name="razor-class-libraries"></a><span data-ttu-id="2fe84-115">Razor 클래스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="2fe84-115">Razor class libraries</span></span>

<span data-ttu-id="2fe84-116">ASP.NET Core 2.1을 통해 Razor 기반 UI를 빌드하고 라이브러리에 포함하고 여러 프로젝트 간에 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-116">ASP.NET Core 2.1 makes it easier to build and include Razor-based UI in a library and share it across multiple projects.</span></span> <span data-ttu-id="2fe84-117">새로운 Razor SDK를 사용하면 NuGet 패키지에 포함될 수 있는 클래스 라이브러리 프로젝트에 Razor 파일을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-117">The new Razor SDK enables building Razor files into a class library project that can be packaged into a NuGet package.</span></span> <span data-ttu-id="2fe84-118">라이브러리의 보기 및 페이지는 자동으로 검색되고 앱에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-118">Views and pages in libraries are automatically discovered and can be overridden by the app.</span></span> <span data-ttu-id="2fe84-119">Razor 컴파일을 빌드에 통합하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-119">By integrating Razor compilation into the build:</span></span>

* <span data-ttu-id="2fe84-120">앱 시작 시간이 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-120">The app startup time is significantly faster.</span></span>
* <span data-ttu-id="2fe84-121">런타임 시 Razor 보기 및 페이지에 대한 빠른 업데이트는 반복적인 개발 워크플로의 일부분으로사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-121">Fast updates to Razor views and pages at runtime are still available as part of an iterative development workflow.</span></span>

<span data-ttu-id="2fe84-122">자세한 내용은 [Razor 클래스 라이브러리 프로젝트를 사용하여 재사용 가능한 UI 만들기](xref:razor-pages/ui-class)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-122">For more information, see [Create reusable UI using the Razor Class Library project](xref:razor-pages/ui-class).</span></span>

## <a name="identity-ui-library--scaffolding"></a><span data-ttu-id="2fe84-123">ID UI 라이브러리 및 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="2fe84-123">Identity UI library & scaffolding</span></span>

<span data-ttu-id="2fe84-124">ASP.NET Core 2.1에서는 [ASP.NET Core ID](xref:security/authentication/identity)를 [Razor 클래스 라이브러리](xref:razor-pages/ui-class)로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-124">ASP.NET Core 2.1 provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span> <span data-ttu-id="2fe84-125">ID가 포함되는 앱은 선택적으로 ID RCL(Razor 클래스 라이브러리)에 포함된 소스 코드를 추가하기 위헤 새 ID 스캐폴더를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-125">Apps that include Identity can apply the new Identity scaffolder to selectively add the source code contained in the Identity Razor Class Library (RCL).</span></span> <span data-ttu-id="2fe84-126">코드를 수정하고 동작을 변경할 수 있도록 소스 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-126">You might want to generate source code so you can modify the code and change the behavior.</span></span> <span data-ttu-id="2fe84-127">예를 들어 등록에 사용된 코드를 생성하도록 스캐폴더를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-127">For example, you could instruct the scaffolder to generate the code used in registration.</span></span> <span data-ttu-id="2fe84-128">생성된 코드는 ID RCL의 동일한 코드보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-128">Generated code takes precedence over the same code in the Identity RCL.</span></span>

<span data-ttu-id="2fe84-129">인증을 포함하지 **않는** 앱은 RCL ID 패키지를 추가하기 위해 ID 스캐폴더를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-129">Apps that do **not** include authentication can apply the Identity scaffolder to add the RCL Identity package.</span></span> <span data-ttu-id="2fe84-130">선택한 ID 코드의 옵션이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-130">You have the option of selecting Identity code to be generated.</span></span>

<span data-ttu-id="2fe84-131">자세한 내용은 [ASP.NET Core 프로젝트에서 ID 스캐폴드](xref:security/authentication/scaffold-identity)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-131">For more information, see [Scaffold Identity in ASP.NET Core projects](xref:security/authentication/scaffold-identity).</span></span>

## <a name="https"></a><span data-ttu-id="2fe84-132">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2fe84-132">HTTPS</span></span>

<span data-ttu-id="2fe84-133">보안 및 개인 정보에 더 중점을 두어 웹앱에서 HTTPS를 활성화하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-133">With the increased focus on security and privacy, enabling HTTPS for web apps is important.</span></span> <span data-ttu-id="2fe84-134">웹에서 HTTPS를 점점 더 많이 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-134">HTTPS enforcement is becoming increasingly strict on the web.</span></span> <span data-ttu-id="2fe84-135">HTTPS를 사용하지 않는 사이트는 안전하지 않은 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-135">Sites that don’t use HTTPS are considered insecure.</span></span> <span data-ttu-id="2fe84-136">브라우저(Chromium, Mozilla)는 보안 컨텍스트에서 웹 기능을 사용하도록 강제 적용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-136">Browsers (Chromium, Mozilla) are starting to enforce that web features must be used from a secure context.</span></span> <span data-ttu-id="2fe84-137">[GDPR](xref:security/gdpr)은 사용자의 개인 정보를 보호하기 위해 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-137">[GDPR](xref:security/gdpr) requires the use of HTTPS to protect user privacy.</span></span> <span data-ttu-id="2fe84-138">프로덕션에서 HTTPS를 사용하는 것이 중요한 반면 개발에서 HTTPS를 사용하면 배포의 문제(예: 안전하지 않은 링크)를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-138">While using HTTPS in production is critical, using HTTPS in development can help prevent issues in deployment (for example, insecure links).</span></span> <span data-ttu-id="2fe84-139">ASP.NET Core 2.1에는 개발에서 HTTPS를 쉽게 사용하고 프로덕션에서 HTTPS를 쉽게 구성하는 다양한 향상된 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-139">ASP.NET Core 2.1 includes a number of improvements that make it easier to use HTTPS in development and to configure HTTPS in production.</span></span> <span data-ttu-id="2fe84-140">자세한 내용은 [HTTPS 적용](xref:security/enforcing-ssl)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-140">For more information, see [Enforce HTTPS](xref:security/enforcing-ssl).</span></span>

### <a name="on-by-default"></a><span data-ttu-id="2fe84-141">기본적으로 설정</span><span class="sxs-lookup"><span data-stu-id="2fe84-141">On by default</span></span>

<span data-ttu-id="2fe84-142">보안 웹 사이트 개발을 위해 HTTPS는 이제 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-142">To facilitate secure website development, HTTPS  is now enabled by default.</span></span> <span data-ttu-id="2fe84-143">2.1부터는 Kestrel이 로컬 개발 인증서가 제공되는 경우 `https://localhost:5001`을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-143">Starting in 2.1, Kestrel listens on `https://localhost:5001` when a local development certificate is present.</span></span> <span data-ttu-id="2fe84-144">개발 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-144">A development certificate is created:</span></span>

* <span data-ttu-id="2fe84-145">처음에 SDK를 사용하면 .NET Core SDK 첫 실행 환경의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-145">As part of the .NET Core SDK first-run experience, when you use the SDK for the first time.</span></span>
* <span data-ttu-id="2fe84-146">수동으로 새 `dev-certs` 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-146">Manually using the new `dev-certs` tool.</span></span>

<span data-ttu-id="2fe84-147">인증서를 신뢰하려면 `dotnet dev-certs https --trust`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-147">Run `dotnet dev-certs https --trust` to trust the certificate.</span></span>

### <a name="https-redirection-and-enforcement"></a><span data-ttu-id="2fe84-148">HTTPS 리디렉션 및 적용</span><span class="sxs-lookup"><span data-stu-id="2fe84-148">HTTPS redirection and enforcement</span></span>

<span data-ttu-id="2fe84-149">웹앱은 일반적으로 HTTP 및 HTTPS를 모두 수신 대기해야 하지만 그런 다음, 모든 HTTP 트래픽을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-149">Web apps typically need to listen on both HTTP and HTTPS, but then redirect all HTTP traffic to HTTPS.</span></span> <span data-ttu-id="2fe84-150">2.1에서는 구성 또는 바인딩된 서버 포트의 유무에 따라 지능적으로 리디렉션되는 특수한 HTTPS 리디렉션 미들웨어가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-150">In 2.1, specialized HTTPS redirection middleware that intelligently redirects based on the presence of configuration or bound server ports has been introduced.</span></span>

<span data-ttu-id="2fe84-151">HTTPS는 [HSTS(HTTP 엄격한 전송 보안 프로토콜)](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts)를 사용하여 더 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-151">Use of HTTPS can be further enforced using [HTTP Strict Transport Security Protocol (HSTS)](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts).</span></span> <span data-ttu-id="2fe84-152">HSTS는 항상 HTTPS를 통해 사이트에 액세스하도록 브라우저에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-152">HSTS instructs browsers to always access the site via HTTPS.</span></span> <span data-ttu-id="2fe84-153">ASP.NET Core 2.1은 최대 기간, 하위 도메인 및 HSTS 미리 로드 목록에 대한 몇 가지 옵션을 지원하는 HSTS 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-153">ASP.NET Core 2.1 adds HSTS middleware that supports options for max age, subdomains, and the HSTS preload list.</span></span>

### <a name="configuration-for-production"></a><span data-ttu-id="2fe84-154">프로덕션에 대한 구성</span><span class="sxs-lookup"><span data-stu-id="2fe84-154">Configuration for production</span></span>

<span data-ttu-id="2fe84-155">프로덕션 내에 HTTPS가 명시적으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-155">In production, HTTPS must be explicitly configured.</span></span> <span data-ttu-id="2fe84-156">2.1에서는 Kestrel에 HTTPS를 구성하는 기본 구성 스키마가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-156">In 2.1, default configuration schema for configuring HTTPS for Kestrel has been added.</span></span> <span data-ttu-id="2fe84-157">다음을 사용하도록 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-157">Apps can be configured to use:</span></span>

* <span data-ttu-id="2fe84-158">URL을 포함하는 여러 엔드포인트.</span><span class="sxs-lookup"><span data-stu-id="2fe84-158">Multiple endpoints including the URLs.</span></span> <span data-ttu-id="2fe84-159">자세한 내용은 [Kestrel 웹 서버 구현: 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-159">For more information, see [Kestrel web server implementation: Endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>
* <span data-ttu-id="2fe84-160">디스크의 파일 또는 인증서 저장소에서 HTTPS에 사용할 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-160">The certificate to use for HTTPS either from a file on disk or from a certificate store.</span></span>

## <a name="gdpr"></a><span data-ttu-id="2fe84-161">GDPR</span><span class="sxs-lookup"><span data-stu-id="2fe84-161">GDPR</span></span>

<span data-ttu-id="2fe84-162">ASP.NET Core에서는 [EU GDPR(일반 데이터 보호 규정)](https://www.eugdpr.org/) 요구 사항의 일부를 충족하는 API 및 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-162">ASP.NET Core provides APIs and templates to help meet some of the [EU General Data Protection Regulation (GDPR)](https://www.eugdpr.org/) requirements.</span></span> <span data-ttu-id="2fe84-163">자세한 내용은 [ASP.NET Core에서 GDPR 지원](xref:security/gdpr)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-163">For more information, see [GDPR support in ASP.NET Core](xref:security/gdpr).</span></span> <span data-ttu-id="2fe84-164">[샘플 앱](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample)에서는 ASP.NET Core 2.1 템플릿에 추가된 대부분의 GDPR 확장점 및 API를 사용하고 테스트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-164">A [sample app](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) shows how to use and lets you test most of the GDPR extension points and APIs added to the ASP.NET Core 2.1 templates.</span></span>

## <a name="integration-tests"></a><span data-ttu-id="2fe84-165">통합 테스트</span><span class="sxs-lookup"><span data-stu-id="2fe84-165">Integration tests</span></span>

<span data-ttu-id="2fe84-166">테스트 생성 및 실행을 간소화하는 새 패키지가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-166">A new package is introduced that streamlines test creation and execution.</span></span> <span data-ttu-id="2fe84-167">[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing/) 패키지는 다음과 같은 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-167">The [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing/) package handles the following tasks:</span></span>

* <span data-ttu-id="2fe84-168">종속성 파일(*\*.deps*)을 테스트된 앱에서 테스트 프로젝트의 *bin* 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-168">Copies the dependency file (*\*.deps*) from the tested app into the test project's *bin* folder.</span></span>
* <span data-ttu-id="2fe84-169">테스트를 실행하면 고정 파일 및 페이지/보기를 찾을 수 있도록 루트 콘텐츠를 테스트된 앱의 프로젝트 루트로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-169">Sets the content root to the tested app's project root so that static files and pages/views are found when the tests are executed.</span></span>
* <span data-ttu-id="2fe84-170">[TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)를 사용하여 테스트된 앱의 부트스트랩을 간소화하기 위해 [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-170">Provides the [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) class to streamline bootstrapping the tested app with [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver).</span></span>

<span data-ttu-id="2fe84-171">다음 테스트는 [xUnit](https://xunit.github.io/)를 사용하여 성공 상태 코드 및 올바른 콘텐츠 형식 헤더의 인덱스 페이지가 로드되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-171">The following test uses [xUnit](https://xunit.github.io/) to check that the Index page loads with a success status code and with the correct Content-Type header:</span></span>

```csharp
public class BasicTests
    : IClassFixture<WebApplicationFactory<RazorPagesProject.Startup>>
{
    private readonly HttpClient _client;

    public BasicTests(WebApplicationFactory<RazorPagesProject.Startup> factory)
    {
        _client = factory.CreateClient();
    }

    [Fact]
    public async Task GetHomePage()
    {
        // Act
        var response = await _client.GetAsync("/");

        // Assert
        response.EnsureSuccessStatusCode(); // Status Code 200-299
        Assert.Equal("text/html; charset=utf-8",
            response.Content.Headers.ContentType.ToString());
    }
}
```

<span data-ttu-id="2fe84-172">자세한 내용은 [통합 테스트](xref:test/integration-tests) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-172">For more information, see the [Integration tests](xref:test/integration-tests) topic.</span></span>

## <a name="apicontroller-actionresultt"></a><span data-ttu-id="2fe84-173">[ApiController], ActionResult\<T></span><span class="sxs-lookup"><span data-stu-id="2fe84-173">[ApiController], ActionResult\<T></span></span>

<span data-ttu-id="2fe84-174">ASP.NET Core 2.1은 쉽게 명확하고 설명이 포함된 웹 API를 빌드할 수 있는 새 프로그래밍 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-174">ASP.NET Core 2.1 adds new programming conventions that make it easier to build clean and descriptive web APIs.</span></span> <span data-ttu-id="2fe84-175">`ActionResult<T>`를 추가하여 앱이 응답 또는 다른 작업 결과를 반환할 수 있도록 추가된 새 형식(IActionResult와 유사)이지만 응답 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-175">`ActionResult<T>` is a new type added to allow an app to return either a response type or any other action result (similar to IActionResult), while still indicating the response type.</span></span> <span data-ttu-id="2fe84-176">`[ApiController]` 특성은 Web API 특정 규칙 및 동작에 옵트인하는 방법으로도 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-176">The `[ApiController]` attribute has also been added as the way to opt in to Web API-specific conventions and behaviors.</span></span>

<span data-ttu-id="2fe84-177">자세한 내용은 [ASP.NET Core를 사용하여 Web API 빌드](xref:web-api/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-177">For more information, see [Build Web APIs with ASP.NET Core](xref:web-api/index).</span></span>

## <a name="ihttpclientfactory"></a><span data-ttu-id="2fe84-178">IHttpClientFactory</span><span class="sxs-lookup"><span data-stu-id="2fe84-178">IHttpClientFactory</span></span>

<span data-ttu-id="2fe84-179">ASP.NET Core 2.1에는 앱에서 `HttpClient`의 인스턴스를 쉽게 구성하고 사용할 수 있는 새로운 `IHttpClientFactory` 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-179">ASP.NET Core 2.1 includes a new `IHttpClientFactory` service that makes it easier to configure and consume instances of `HttpClient` in apps.</span></span> <span data-ttu-id="2fe84-180">`HttpClient`에는 나가는 HTTP 요청을 위해 함께 연결될 수 있는 처리기 위임이라는 개념이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-180">`HttpClient` already has the concept of delegating handlers that could be linked together for outgoing HTTP requests.</span></span> <span data-ttu-id="2fe84-181">팩터리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-181">The factory:</span></span>

* <span data-ttu-id="2fe84-182">보다 직관적인 명명 클라이언트별 `HttpClient` 인스턴스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-182">Makes registering of instances of `HttpClient` per named client more intuitive.</span></span>
* <span data-ttu-id="2fe84-183">Polly 정책을 다시 시도, CircuitBreakers 등에 사용할 수 있는 Polly 처리기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-183">Implements a Polly handler that allows Polly policies to be used for Retry, CircuitBreakers, etc.</span></span>

<span data-ttu-id="2fe84-184">자세한 내용은 [HTTP 요청 시작](xref:fundamentals/http-requests)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-184">For more information, see [Initiate HTTP Requests](xref:fundamentals/http-requests).</span></span>

## <a name="kestrel-transport-configuration"></a><span data-ttu-id="2fe84-185">Kestrel 전송 구성</span><span class="sxs-lookup"><span data-stu-id="2fe84-185">Kestrel transport configuration</span></span>

<span data-ttu-id="2fe84-186">ASP.NET Core 2.1 릴리스에서 Kestrel의 기본 전송은 더 이상 Libuv에 기반하지 않으며 대신 관리 소켓에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-186">With the release of ASP.NET Core 2.1, Kestrel's default transport is no longer based on Libuv but instead based on managed sockets.</span></span> <span data-ttu-id="2fe84-187">자세한 내용은 [Kestrel 웹 서버 구현: 전송 구성](xref:fundamentals/servers/kestrel#transport-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-187">For more information, see [Kestrel web server implementation: Transport configuration](xref:fundamentals/servers/kestrel#transport-configuration).</span></span>

## <a name="generic-host-builder"></a><span data-ttu-id="2fe84-188">제네릭 호스트 작성기</span><span class="sxs-lookup"><span data-stu-id="2fe84-188">Generic host builder</span></span>

<span data-ttu-id="2fe84-189">제네릭 호스트 작성기(`HostBuilder`)가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-189">The Generic Host Builder (`HostBuilder`) has been introduced.</span></span> <span data-ttu-id="2fe84-190">HTTP 요청(메시징, 백그라운드 작업 등)을 처리하지 않는 앱에 작성기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-190">This builder can be used for apps that don't process HTTP requests (Messaging, background tasks, etc.).</span></span>

<span data-ttu-id="2fe84-191">자세한 내용은 [.NET 제네릭 호스트](xref:fundamentals/host/generic-host)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-191">For more information, see [.NET Generic Host](xref:fundamentals/host/generic-host).</span></span>

## <a name="updated-spa-templates"></a><span data-ttu-id="2fe84-192">업데이트된 SPA 템플릿</span><span class="sxs-lookup"><span data-stu-id="2fe84-192">Updated SPA templates</span></span>

<span data-ttu-id="2fe84-193">표준 프로젝트 구조를 사용하고 각 프레임워크에 대한 시스템을 빌드하도록 Angular, React 및 React with Redux에 대한 단일 페이지 애플리케이션 템플릿을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-193">The Single Page Application templates for Angular, React, and React with Redux are updated to use the standard project structures and build systems for each framework.</span></span>

<span data-ttu-id="2fe84-194">Angular 템플릿은 Angular CLI에 기반하고 React 템플릿은 create-react-app에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-194">The Angular template is based on the Angular CLI, and the React templates are based on create-react-app.</span></span>

<span data-ttu-id="2fe84-195">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-195">For more information, see:</span></span>

* <xref:spa/angular>
* <xref:spa/react>
* <xref:spa/react-with-redux>

## <a name="razor-pages-search-for-razor-assets"></a><span data-ttu-id="2fe84-196">Razor 자산에 대한 Razor Pages 검색</span><span class="sxs-lookup"><span data-stu-id="2fe84-196">Razor Pages search for Razor assets</span></span>

<span data-ttu-id="2fe84-197">2.1에서는 나열된 순서로 다음 디렉터리에 있는 Razor 자산(예: 레이아웃 및 부분)에 대한 Razor Pages 검색은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-197">In 2.1, Razor Pages search for Razor assets (such as layouts and partials) in the following directories in the listed order:</span></span>

1. <span data-ttu-id="2fe84-198">현재 Pages 폴더</span><span class="sxs-lookup"><span data-stu-id="2fe84-198">Current Pages folder.</span></span>
1. <span data-ttu-id="2fe84-199">*/Pages/Shared/*</span><span class="sxs-lookup"><span data-stu-id="2fe84-199">*/Pages/Shared/*</span></span>
1. <span data-ttu-id="2fe84-200">*/Views/Shared/*</span><span class="sxs-lookup"><span data-stu-id="2fe84-200">*/Views/Shared/*</span></span>

## <a name="razor-pages-in-an-area"></a><span data-ttu-id="2fe84-201">영역의 Razor Pages</span><span class="sxs-lookup"><span data-stu-id="2fe84-201">Razor Pages in an area</span></span>

<span data-ttu-id="2fe84-202">이제 Razor Pages는 [영역](xref:mvc/controllers/areas)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-202">Razor Pages now support [areas](xref:mvc/controllers/areas).</span></span> <span data-ttu-id="2fe84-203">영역의 예제를 보려면 개별 사용자 계정을 사용하여 새 Razor Pages 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-203">To see an example of areas, create a new Razor Pages web app with individual user accounts.</span></span> <span data-ttu-id="2fe84-204">개별 사용자 계정을 사용하는 Razor Pages 웹앱에는 */Areas/Identity/Pages*가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-204">A Razor Pages web app with individual user accounts includes */Areas/Identity/Pages*.</span></span>

## <a name="mvc-compatibility-version"></a><span data-ttu-id="2fe84-205">MVC 호환성 버전</span><span class="sxs-lookup"><span data-stu-id="2fe84-205">MVC compatibility version</span></span>

<span data-ttu-id="2fe84-206"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 메서드를 사용하면 ASP.NET Core MVC 2.1 이상에서 도입된 주요 동작 변경 내용을 앱이 옵트인(opt-in) 또는 옵트아웃(opt-out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe84-206">The <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET Core MVC 2.1 or later.</span></span>

<span data-ttu-id="2fe84-207">자세한 내용은 <xref:mvc/compatibility-version>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-207">For more information, see <xref:mvc/compatibility-version>.</span></span>

## <a name="migrate-from-20-to-21"></a><span data-ttu-id="2fe84-208">2.0에서 2.1로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2fe84-208">Migrate from 2.0 to 2.1</span></span>

<span data-ttu-id="2fe84-209">[ASP.NET Core 2.0에서 2.1로 마이그레이션](xref:migration/20_21)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-209">See [Migrate from ASP.NET Core 2.0 to 2.1](xref:migration/20_21).</span></span>

## <a name="additional-information"></a><span data-ttu-id="2fe84-210">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2fe84-210">Additional information</span></span>

<span data-ttu-id="2fe84-211">전체 변경 내용 목록을 보려면 [ASP.NET Core 2.1 릴리스 정보](https://github.com/aspnet/Home/releases/tag/2.1.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe84-211">For the complete list of changes, see the [ASP.NET Core 2.1 Release Notes](https://github.com/aspnet/Home/releases/tag/2.1.0).</span></span>
