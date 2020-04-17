---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 권한 부여 서버 | 마이크로 소프트 문서
author: hongyes
description: 이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법을 안내합니다. 이것은 단지 outlin 고급 자습서입니다 ...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540414"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="1c849-104">OWIN OAuth 2.0 권한 부여 서버</span><span class="sxs-lookup"><span data-stu-id="1c849-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="1c849-105">[홍예선과](https://github.com/hongyes) [프라부라즈 티아가라잔](https://github.com/Praburaj)</span><span class="sxs-lookup"><span data-stu-id="1c849-105">by [Hongye Sun](https://github.com/hongyes) and [Praburaj Thiagarajan](https://github.com/Praburaj)</span></span>

> <span data-ttu-id="1c849-106">이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="1c849-107">OWIN OAuth 2.0 권한 부여 서버를 만드는 단계만 간략하게 설명하는 고급 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="1c849-108">이것은 단계별 튜토리얼이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="1c849-109">[샘플 코드를 다운로드합니다.](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)</span><span class="sxs-lookup"><span data-stu-id="1c849-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
>
> > [!NOTE]
> > <span data-ttu-id="1c849-110">이 개요는 보안 프로덕션 앱을 만드는 데 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="1c849-111">이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법에 대한 개요만 제공하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="1c849-112">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1c849-112">Software versions</span></span>
>
> | <span data-ttu-id="1c849-113">**튜토리얼에 표시**</span><span class="sxs-lookup"><span data-stu-id="1c849-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="1c849-114">**또한 와 함께 작동**</span><span class="sxs-lookup"><span data-stu-id="1c849-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="1c849-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1c849-115">Windows 8.1</span></span> | <span data-ttu-id="1c849-116">윈도우 8, 윈도우 7</span><span class="sxs-lookup"><span data-stu-id="1c849-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="1c849-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1c849-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | <span data-ttu-id="1c849-118">[비주얼 스튜디오 2013 데스크탑 익스프레스](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span><span class="sxs-lookup"><span data-stu-id="1c849-118">[Visual Studio 2013 Express for Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span></span> <span data-ttu-id="1c849-119">최신 업데이트와 Visual Studio 2012 가 작동해야하지만, 튜토리얼은 그것으로 테스트되지 않은, 일부 메뉴 선택 및 대화 상자는 다르다.</span><span class="sxs-lookup"><span data-stu-id="1c849-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="1c849-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1c849-120">.NET 4.5</span></span> |  |
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="1c849-121">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="1c849-121">Questions and Comments</span></span>
>
> <span data-ttu-id="1c849-122">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [GitHub에 카타나 프로젝트에서](https://github.com/aspnet/AspNetKatana/)게시 할 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="1c849-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="1c849-123">자습서 자체에 대한 질문과 의견은 페이지 하단의 주석 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="1c849-124">[OAuth 2.0 프레임워크를](http://tools.ietf.org/html/rfc6749) 사용하면 타사 앱에서 HTTP 서비스에 대한 제한된 액세스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="1c849-125">클라이언트는 리소스 소유자의 자격 증명을 사용하여 보호된 리소스에 액세스하는 대신 특정 범위, 수명 및 기타 액세스 특성을 나타내는 문자열인 액세스 토큰을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="1c849-126">액세스 토큰은 리소스 소유자의 승인을 받은 권한 부여 서버에서 타사 클라이언트에 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="1c849-127">이 자습서는 다음을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-127">This tutorial will cover:</span></span>

- <span data-ttu-id="1c849-128">네 가지 권한 부여 권한 부여 유형 및 새로 고침 토큰을 지원하기 위해 권한 부여 서버를 만드는 방법:</span><span class="sxs-lookup"><span data-stu-id="1c849-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="1c849-129">권한 부여 코드 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-129">Authorization code grant</span></span>
    - <span data-ttu-id="1c849-130">암시적 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-130">Implicit Grant</span></span>
    - <span data-ttu-id="1c849-131">리소스 소유자 암호 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="1c849-132">클라이언트 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-132">Client Credentials Grant</span></span>
- <span data-ttu-id="1c849-133">액세스 토큰으로 보호되는 리소스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="1c849-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="1c849-134">OAuth 2.0 클라이언트 만들기.</span><span class="sxs-lookup"><span data-stu-id="1c849-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="1c849-135">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1c849-135">Prerequisites</span></span>

- <span data-ttu-id="1c849-136">[비주얼 스튜디오 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) 또는 무료 [비주얼 스튜디오 익스프레스 2013,](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)페이지 상단의 **소프트웨어 버전에** 표시된 대로.</span><span class="sxs-lookup"><span data-stu-id="1c849-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="1c849-137">OWIN에 익숙합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-137">Familiarity with OWIN.</span></span> <span data-ttu-id="1c849-138">[카타나 프로젝트 시작하기와](https://msdn.microsoft.com/magazine/dn451439.aspx) [OWIN 및 카타나에서](index.md)새로운 사항 확인</span><span class="sxs-lookup"><span data-stu-id="1c849-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="1c849-139">[역할,](http://tools.ietf.org/html/rfc6749#section-1.1) [프로토콜 흐름](http://tools.ietf.org/html/rfc6749#section-1.2)및 [권한 부여 부여를](http://tools.ietf.org/html/rfc6749#section-1.3)포함한 [OAuth](http://tools.ietf.org/html/rfc6749) 용어에 대한 친숙도.</span><span class="sxs-lookup"><span data-stu-id="1c849-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="1c849-140">[OAuth 2.0 소개는](http://tools.ietf.org/html/rfc6749#section-1) 좋은 소개를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="1c849-141">권한 부여 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="1c849-141">Create an Authorization Server</span></span>

<span data-ttu-id="1c849-142">이 자습서에서는 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 및 ASP.NET MVC를 사용하여 권한 부여 서버를 만드는 방법을 대략 스케치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="1c849-143">이 자습서에는 각 단계가 포함되어 있지 않으므로 완료된 샘플에 대한 다운로드를 곧 제공할 수 있기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="1c849-144">먼저 *AuthorizationServer라는* 빈 웹 앱을 만들고 다음 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="1c849-145">마이크로소프트.아스프넷.Mvc</span><span class="sxs-lookup"><span data-stu-id="1c849-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="1c849-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="1c849-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="1c849-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="1c849-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="1c849-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="1c849-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="1c849-149">마이크로 소프트.Owin.Security.Google (또는 마이크로 소프트.Owin.Security.Facebook과 같은 다른 소셜 로그인 패키지)</span><span class="sxs-lookup"><span data-stu-id="1c849-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="1c849-150">*시작이라는*프로젝트 루트 폴더 아래에 [OWIN 시작 클래스를](owin-startup-class-detection.md) 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="1c849-151">*앱\_시작* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="1c849-152">*앱\_시작* 폴더를 선택하고 Shift+Alt+A를 사용하여 권한 *부여 서버\앱\_시작\Startup.Auth.cs* 파일의 다운로드버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="1c849-153">위의 코드는 계정 관리를 위해 권한 부여 서버 자체에서 사용되는 쿠키 및 Google 인증에 응용 프로그램 / 외부 로그인을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="1c849-154">`UseOAuthAuthorizationServer` 확장 방법은 권한 부여 서버를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="1c849-155">설정 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-155">The setup options are:</span></span>

- <span data-ttu-id="1c849-156">`AuthorizeEndpointPath`: 클라이언트 응용 프로그램이 사용자가 토큰 또는 코드를 발급하는 데 동의를 얻기 위해 사용자 에이전트를 리디렉션하는 요청 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="1c849-157">예를 들어`/Authorize`선행 슬래시로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="1c849-158">`TokenEndpointPath`: 요청 경로 클라이언트 응용 프로그램이 액세스 토큰을 얻기 위해 직접 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="1c849-159">"/토큰"과 같은 선행 슬래시로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="1c849-160">클라이언트가 [클라이언트\_보안](http://tools.ietf.org/html/rfc6749#appendix-A.2)을 발급하는 경우 이 끝점에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="1c849-161">`ApplicationCanDisplayErrors`: 웹 `true` 응용 프로그램이 엔드포인트에서 클라이언트 유효성 검사 오류에 `/Authorize` 대한 사용자 지정 오류 페이지를 생성하려는 경우로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="1c849-162">이는 브라우저가 클라이언트 응용 프로그램으로 다시 리디렉션되지 않는 경우(예: `client_id` 올바르지 `redirect_uri` 않은 경우에만)에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="1c849-163">끝점은 `/Authorize` "oauth"를 볼 것으로 예상해야 합니다. 오류", "오스. 오류 설명", "oauth" ErrorUri" 속성이 OWIN 환경에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c849-164">그렇지 않은 경우 권한 부여 서버는 오류 세부 정보가 있는 기본 오류 페이지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="1c849-165">`AllowInsecureHttp`: TRUE는 HTTP URI 주소에 권한을 부여하고 토큰 요청이 `redirect_uri` HTTP URI 주소에 도착할 수 있도록 허용하고 들어오는 요청 매개 변수에 HTTP URI 주소를 가질 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1c849-166">보안 - 개발 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-166">Security - This is for development only.</span></span>
- <span data-ttu-id="1c849-167">`Provider`: 권한 부여 서버 미들웨어에서 발생하는 이벤트를 처리하기 위해 응용 프로그램에서 제공하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="1c849-168">응용 프로그램은 인터페이스를 완전히 구현하거나 이 서버가 지원하는 OAuth 흐름에 필요한 대리자를 `OAuthAuthorizationServerProvider` 인스턴스를 만들고 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="1c849-169">`AuthorizationCodeProvider`: 클라이언트 응용 프로그램으로 돌아가는 일회용 권한 부여 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="1c849-170">OAuth 서버가 보안을 유지하려면 응용 프로그램이 `AuthorizationCodeProvider` `OnCreate/OnCreateAsync` 이벤트에서 생성된 토큰이 에 대한 호출 한 `OnReceive/OnReceiveAsync`번만 유효한 것으로 간주되는 인스턴스를 제공해야 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="1c849-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="1c849-171">`RefreshTokenProvider`: 필요할 때 새 액세스 토큰을 생성하는 데 사용할 수 있는 새로 고침 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="1c849-172">부여 서버가 제공되지 않으면 끝점에서 새로 `/Token` 고침 토큰이 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="1c849-173">계정 관리</span><span class="sxs-lookup"><span data-stu-id="1c849-173">Account Management</span></span>

<span data-ttu-id="1c849-174">OAuth는 사용자 계정 정보를 관리하는 위치 나 방법을 신경 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="1c849-175">그것은 ASP.NET 그것을 담당하는 [정체성입니다.](../../../identity/index.md)</span><span class="sxs-lookup"><span data-stu-id="1c849-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="1c849-176">이 자습서에서는 계정 관리 코드를 단순화 하 고 사용자가 OWIN 쿠키 미들웨어를 사용 하 여 로그인할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="1c849-177">다음은 다음의 단순화된 샘플 `AccountController`코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="1c849-178">`ValidateClientRedirectUri`은 등록된 리디렉션 URL을 사용하여 클라이언트의 유효성을 검사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="1c849-179">`ValidateClientAuthentication`기본 구성표 헤더와 폼 본문을 확인하여 클라이언트의 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="1c849-180">로그인 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="1c849-181">지금 IETF의 OAuth 2 [권한 부여 코드 부여](http://tools.ietf.org/html/rfc6749#section-4.1) 섹션을 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span>

<span data-ttu-id="1c849-182">**공급자(아래** 표)는 [OAuth권한 부여 서버옵션입니다.](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx) 모든 OAuth `OAuthAuthorizationServerProvider`서버 이벤트를 포함하는 형식의 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span>

| <span data-ttu-id="1c849-183">권한 부여 코드 부여 섹션의 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="1c849-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="1c849-184">샘플 다운로드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="1c849-185">(A) 클라이언트는 리소스 소유자의 사용자 에이전트를 권한 부여 끝점으로 지시하여 흐름을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="1c849-186">클라이언트에는 클라이언트 식별자, 요청된 범위, 로컬 상태 및 권한 부여 서버가 액세스가 부여되거나 거부되면 사용자 에이전트를 다시 보내는 리디렉션 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="1c849-187">공급자.일치 엔드 포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여 Endpoint</span><span class="sxs-lookup"><span data-stu-id="1c849-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="1c849-188">(B) 권한 부여 서버는 사용자 에이전트를 통해 리소스 소유자를 인증하고 리소스 소유자가 클라이언트의 액세스 요청을 부여하거나 거부하는지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="1c849-189">**사용자에게 액세스&gt; 권한을 부여하는 경우 &lt;** 공급자.매치엔드포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여Endpoint 권한 코드 제공.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="1c849-190">(C) 리소스 소유자가 액세스 권한을 부여한다고 가정하면 권한 부여 서버는 앞에서 제공한 리디렉션 URI(요청 또는 클라이언트 등록 중)를 사용하여 사용자 에이전트를 클라이언트로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="1c849-191">...</span><span class="sxs-lookup"><span data-stu-id="1c849-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="1c849-192">(D) 클라이언트는 이전 단계에서 받은 권한 부여 코드를 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="1c849-193">요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="1c849-194">클라이언트에는 확인을 위한 권한 부여 코드를 가져오는 데 사용되는 리디렉션 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="1c849-195">provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 인증 코드코드.ReceiveAsync 공급자.ValidateTokenRequest 공급자.토큰엔드포인트 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="1c849-196">권한 부여 `AuthorizationCodeProvider.CreateAsync` 코드의 생성 및 유효성 검사를 제어하기 `ReceiveAsync` 위한 샘플 구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="1c849-197">위의 코드는 메모리 내 동시 사전을 사용하여 코드 및 ID 티켓을 저장하고 코드를 받은 후 ID를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="1c849-198">실제 응용 프로그램에서는 영구 데이터 저장소로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="1c849-199">권한 부여 끝점은 리소스 소유자가 클라이언트에 대한 액세스 권한을 부여하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="1c849-200">일반적으로 사용자가 단추를 클릭하고 권한 부여를 확인할 수 있도록 사용자 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="1c849-201">OWIN OAuth 미들웨어를 사용하면 응용 프로그램 코드가 권한 부여 끝점을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="1c849-202">샘플 앱에서는 이를 처리하기 위해 호출된 `OAuthController` MVC 컨트롤러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="1c849-203">다음은 샘플 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="1c849-204">이 `Authorize` 작업은 사용자가 권한 부여 서버에 로그인했는지 먼저 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="1c849-205">그렇지 않은 경우 인증 미들웨어는 호출자에게 "응용 프로그램" 쿠키를 사용하여 인증하도록 하고 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="1c849-206">(위의 강조 표시된 코드를 참조하십시오.) 사용자가 로그인한 경우 아래와 같이 권한 부여 보기가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="1c849-207">권한 **부여** 단추를 선택하면 `Authorize` 작업이 새 "Bearer" ID를 만들고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="1c849-208">권한 부여 서버가 베어러 토큰을 생성하고 JSON 페이로드를 사용하여 클라이언트로 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span>

### <a name="implicit-grant"></a><span data-ttu-id="1c849-209">암시적 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-209">Implicit Grant</span></span>

<span data-ttu-id="1c849-210">지금 IETF의 OAuth 2 [암시적 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="1c849-211">그림 4에 표시된 [암시적 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="1c849-212">암시적 부여 섹션의 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="1c849-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="1c849-213">샘플 다운로드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="1c849-214">(A) 클라이언트는 리소스 소유자의 사용자 에이전트를 권한 부여 끝점으로 지시하여 흐름을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="1c849-215">클라이언트에는 클라이언트 식별자, 요청된 범위, 로컬 상태 및 권한 부여 서버가 액세스가 부여되거나 거부되면 사용자 에이전트를 다시 보내는 리디렉션 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="1c849-216">공급자.일치 엔드 포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여 Endpoint</span><span class="sxs-lookup"><span data-stu-id="1c849-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="1c849-217">(B) 권한 부여 서버는 사용자 에이전트를 통해 리소스 소유자를 인증하고 리소스 소유자가 클라이언트의 액세스 요청을 부여하거나 거부하는지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="1c849-218">**사용자에게 액세스&gt; 권한을 부여하는 경우 &lt;** 공급자.매치엔드포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여Endpoint 권한 코드 제공.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="1c849-219">(C) 리소스 소유자가 액세스 권한을 부여한다고 가정하면 권한 부여 서버는 앞에서 제공한 리디렉션 URI(요청 또는 클라이언트 등록 중)를 사용하여 사용자 에이전트를 클라이언트로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="1c849-220">...</span><span class="sxs-lookup"><span data-stu-id="1c849-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="1c849-221">(D) 클라이언트는 이전 단계에서 받은 권한 부여 코드를 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="1c849-222">요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="1c849-223">클라이언트에는 확인을 위한 권한 부여 코드를 가져오는 데 사용되는 리디렉션 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="1c849-224">권한 부여 코드 부여에`OAuthController.Authorize` 대한 권한 부여 끝점(작업)을 이미 구현했기 때문에 암시적 흐름도 자동으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="1c849-225">참고: `Provider.ValidateClientRedirectUri` 리디렉션 URL을 사용하여 클라이언트 ID의 유효성을 검사하는 데 사용되며, 이 URL은 암시적 권한 부여 흐름이 악의적인[클라이언트(중간자](https://www.owasp.org/index.php/Man-in-the-middle_attack)공격)에게 액세스 토큰을 보내지 않도록 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="1c849-226">리소스 소유자 암호 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="1c849-227">지금 IETF의 OAuth 2 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="1c849-228">그림 5에 표시된 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="1c849-229">리소스 소유자 암호 자격 증명 부여 섹션에서 단계 흐름</span><span class="sxs-lookup"><span data-stu-id="1c849-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="1c849-230">샘플 다운로드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="1c849-231">(A) 리소스 소유자는 클라이언트에 사용자 이름과 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="1c849-232">(B) 클라이언트는 리소스 소유자로부터 받은 자격 증명을 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="1c849-233">요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="1c849-234">provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 공급자.유효성 검사토큰 요청 공급자.GrantResource소유자 자격 증명 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="1c849-235">(C) 권한 부여 서버는 클라이언트를 인증하고 리소스 소유자 자격 증명의 유효성을 검사하며, 유효한 경우 액세스 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="1c849-236">다음은 `Provider.GrantResourceOwnerCredentials`샘플 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="1c849-237">위의 코드는 자습서의 이 섹션을 설명하기 위한 것이며 보안 또는 프로덕션 앱에서 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="1c849-238">리소스 소유자 자격 증명을 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="1c849-239">모든 자격 증명이 유효하다고 가정하고 새 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="1c849-240">새 ID는 액세스 토큰을 생성하고 토큰을 새로 고치는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="1c849-241">코드를 사용자 고유의 보안 계정 관리 코드로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="1c849-242">클라이언트 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="1c849-242">Client Credentials Grant</span></span>

<span data-ttu-id="1c849-243">지금 IETF의 OAuth 2 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="1c849-244">그림 6에 표시된 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="1c849-245">클라이언트 자격 증명 부여 섹션의 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="1c849-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="1c849-246">샘플 다운로드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="1c849-247">(A) 클라이언트는 권한 부여 서버로 인증하고 토큰 끝점에서 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="1c849-248">provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 공급자.유효성 검사 토큰 요청 공급자.GrantClientcredentials 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="1c849-249">(B) 권한 부여 서버는 클라이언트를 인증하고 유효한 경우 액세스 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="1c849-250">다음은 `Provider.GrantClientCredentials`샘플 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="1c849-251">위의 코드는 자습서의 이 섹션을 설명하기 위한 것이며 보안 또는 프로덕션 앱에서 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="1c849-252">코드를 사용자 고유의 보안 클라이언트 관리 코드로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="1c849-253">토큰 새로 고침</span><span class="sxs-lookup"><span data-stu-id="1c849-253">Refresh Token</span></span>

<span data-ttu-id="1c849-254">지금 IETF의 OAuth 2 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="1c849-255">그림 2에 표시된 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="1c849-256">클라이언트 자격 증명 부여 섹션의 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="1c849-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="1c849-257">샘플 다운로드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="1c849-258">(G) 클라이언트는 권한 부여 서버로 인증하고 새로 고침 토큰을 표시하여 새 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="1c849-259">클라이언트 인증 요구 사항은 클라이언트 유형 및 권한 부여 서버 정책을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="1c849-260">provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 새로 고침 토큰 공급자.ReceiveAsync 공급자.유효성 검사 토큰 공급자.GrantRefreshToken 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="1c849-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="1c849-261">(H) 권한 부여 서버는 클라이언트를 인증하고 새로 고침 토큰의 유효성을 검사하며, 유효한 경우 새 액세스 토큰(및 선택적으로 새 새로 고침 토큰)을 발행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="1c849-262">다음은 `Provider.GrantRefreshToken`샘플 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="1c849-263">액세스 토큰으로 보호되는 리소스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="1c849-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="1c849-264">빈 웹 앱 프로젝트를 만들고 프로젝트에 다음 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="1c849-265">마이크로소프트.아스프넷.웹Api.오윈</span><span class="sxs-lookup"><span data-stu-id="1c849-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="1c849-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="1c849-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="1c849-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="1c849-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="1c849-268">시작 클래스를 만들고 인증 및 웹 API를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="1c849-269">샘플 다운로드에서 *권한 부여 서버\리소스 서버\Startup.cs를* 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="1c849-270">샘플 다운로드에서 *권한 부여\_서버\리소스 서버\앱 시작\Startup.Auth.cs를* 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="1c849-271">샘플 다운로드에서 *권한 부여\_서버\리소스 서버\앱 시작\Startup.WebApi.cs를* 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="1c849-272">`UseCors`메서드를 사용하면 모든 도메인에 대한 CORS가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="1c849-273">`UseOAuthBearerAuthentication`메서드는 요청의 권한 부여 헤더에서 베어러 토큰을 수신하고 유효성을 검사하는 OAuth 베어러 토큰 인증 미들웨어를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="1c849-274">`Config.SuppressDefaultHostAuthenticaiton`앱에서 기본 호스트 인증 보안 주체를 표시하므로 이 호출 후 모든 요청이 익명으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="1c849-275">`HostAuthenticationFilter`지정된 인증 유형에 대해서만 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="1c849-276">이 경우 베어러 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="1c849-277">인증된 ID를 보여 주기 위해 현재 사용자의 클레임을 출력하는 ApiController를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="1c849-278">권한 부여 서버와 리소스 서버가 동일한 컴퓨터에 없는 경우 OAuth 미들웨어는 다른 컴퓨터 키를 사용하여 베어러 액세스 토큰을 암호화하고 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="1c849-279">두 프로젝트 간에 동일한 개인 키를 공유하기 `machinekey` 위해 두 *web.config* 파일에 동일한 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="1c849-280">OAuth 2.0 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="1c849-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="1c849-281">우리는 클라이언트 코드를 단순화하기 위해 [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="1c849-282">권한 부여 코드 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1c849-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="1c849-283">이 클라이언트는 MVC 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-283">This client is an MVC application.</span></span> <span data-ttu-id="1c849-284">백 엔드에서 액세스 토큰을 얻기 위해 권한 부여 코드 부여 흐름을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="1c849-285">아래와 같이 단일 페이지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="1c849-286">**권한 부여** 단추는 브라우저를 권한 부여 서버로 리디렉션하여 리소스 소유자에게 이 클라이언트에 대한 액세스 권한을 부여하도록 알립니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="1c849-287">**새로 고침** 단추는 현재 새로 고침 토큰을 사용하여 새 액세스 토큰및 새로 고침 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="1c849-288">**보호된 리소스 API 액세스** 단추는 리소스 서버를 호출하여 현재 사용자의 클레임 데이터를 얻고 페이지에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="1c849-289">다음은 클라이언트의 `HomeController` 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="1c849-290">`DotNetOpenAuth`기본적으로 SSL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="1c849-291">데모에서 HTTP를 사용하므로 구성 파일에 다음 설정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="1c849-292">보안 - 프로덕션 앱에서 SSL을 사용하지 않도록 설정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1c849-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="1c849-293">이제 로그인 자격 증명이 유선에서 일반 텍스트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="1c849-294">위의 코드는 로컬 샘플 디버깅 및 탐색용입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="1c849-295">암시적 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1c849-295">Implicit Grant Client</span></span>

<span data-ttu-id="1c849-296">이 클라이언트는 자바 스크립트를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="1c849-297">새 창을 열고 권한 부여 서버의 권한 부여 끝점으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="1c849-298">URL 조각이 다시 리디렉션될 때 URL 조각에서 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="1c849-299">다음 이미지는 이 프로세스를 보여 주며 다음과 같은 프로세스를 보여 주며 다음과 같은 프로세스를 보여 주며 다음과</span><span class="sxs-lookup"><span data-stu-id="1c849-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="1c849-300">클라이언트는 홈 페이지용 페이지와 콜백용 페이지의 두 페이지가 있어야 합니다. 다음은 *Index.cshtml* 파일에 있는 자바스크립트 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="1c849-301">*SignIn.cshtml* 파일의 콜백 처리 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="1c849-302">가장 좋은 방법은 자바스크립트를 외부 파일로 이동하고 Razor 태그와 함께 포함하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="1c849-303">이 샘플을 단순하게 유지하기 위해 결합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="1c849-304">리소스 소유자 암호 자격 증명 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1c849-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="1c849-305">콘솔 앱을 사용하여 이 클라이언트를 데모합니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="1c849-306">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="1c849-307">클라이언트 자격 증명 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1c849-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="1c849-308">리소스 소유자 암호 자격 증명 부여와 유사하게 콘솔 앱 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c849-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
