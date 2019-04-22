---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 개별 계정 및 ASP.NET Web API 2.2에서에서 로컬 로그인을 사용 하 여 Web API 보안 유지 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 OAuth2를 사용 하 여 멤버 자격 데이터베이스에 대해 인증 하는 웹 API를 보호 하는 방법을 보여 줍니다. 자습서는 Visual Studio 201에 사용 되는 소프트웨어 버전 중...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 29c3670ad7ab93acb0be878e5bd961d0ea446eee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59396234"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a><span data-ttu-id="26f61-104">개별 계정 및 ASP.NET Web API 2.2에서에서 로컬 로그인을 사용 하 여 Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="26f61-104">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>

<span data-ttu-id="26f61-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="26f61-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="26f61-106">샘플 앱 다운로드</span><span class="sxs-lookup"><span data-stu-id="26f61-106">Download Sample App</span></span>](https://github.com/MikeWasson/LocalAccountsApp)

> <span data-ttu-id="26f61-107">이 항목에서는 OAuth2를 사용 하 여 멤버 자격 데이터베이스에 대해 인증 하는 웹 API를 보호 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-107">This topic shows how to secure a web API using OAuth2 to authenticate against a membership database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="26f61-108">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="26f61-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="26f61-109">Visual Studio 2013 업데이트 3</span><span class="sxs-lookup"><span data-stu-id="26f61-109">Visual Studio 2013 Update 3</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="26f61-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="26f61-110">Web API 2.2</span></span>](../releases/whats-new-in-aspnet-web-api-22.md)
> - [<span data-ttu-id="26f61-111">ASP.NET Identity 2.1</span><span class="sxs-lookup"><span data-stu-id="26f61-111">ASP.NET Identity 2.1</span></span>](../../../identity/index.md)


<span data-ttu-id="26f61-112">Visual Studio 2013에서 Web API 프로젝트 템플릿을 사용 하면 인증에 대 한 세 가지 옵션:</span><span class="sxs-lookup"><span data-stu-id="26f61-112">In Visual Studio 2013, the Web API project template gives you three options for authentication:</span></span>

- <span data-ttu-id="26f61-113">**개별 계정입니다.**</span><span class="sxs-lookup"><span data-stu-id="26f61-113">**Individual accounts.**</span></span> <span data-ttu-id="26f61-114">멤버 자격 데이터베이스를 사용 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-114">The app uses a membership database.</span></span>
- <span data-ttu-id="26f61-115">**조직 계정입니다.**</span><span class="sxs-lookup"><span data-stu-id="26f61-115">**Organizational accounts.**</span></span> <span data-ttu-id="26f61-116">사용자가 Azure Active Directory, Office 365 또는 온-프레미스 Active Directory 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-116">Users sign in with their Azure Active Directory, Office 365, or on-premise Active Directory credentials.</span></span>
- <span data-ttu-id="26f61-117">**Windows 인증입니다.**</span><span class="sxs-lookup"><span data-stu-id="26f61-117">**Windows authentication.**</span></span> <span data-ttu-id="26f61-118">이 옵션은 인트라넷 응용 프로그램의 경우 이며 Windows Authentication IIS 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-118">This option is intended for Intranet applications, and uses the Windows Authentication IIS module.</span></span>

<span data-ttu-id="26f61-119">이러한 옵션에 대 한 자세한 내용은 참조 하세요. [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-119">For more details about these options, see [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).</span></span>

<span data-ttu-id="26f61-120">개별 계정에 로그인 할 두 가지 방법으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-120">Individual accounts provide two ways for a user to log in:</span></span>

- <span data-ttu-id="26f61-121">**로컬 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-121">**Local login**.</span></span> <span data-ttu-id="26f61-122">사용자 이름과 암호를 입력 합니다. 사이트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-122">The user registers at the site, entering a username and password.</span></span> <span data-ttu-id="26f61-123">응용 프로그램 멤버 자격 데이터베스에서 암호 해시를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-123">The app stores the password hash in the membership database.</span></span> <span data-ttu-id="26f61-124">사용자가 로그인 할 때 ASP.NET Id 시스템에 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-124">When the user logs in, the ASP.NET Identity system verifies the password.</span></span>
- <span data-ttu-id="26f61-125">**소셜 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-125">**Social login**.</span></span> <span data-ttu-id="26f61-126">사용자는 Facebook, Microsoft, Google 등 외부 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-126">The user signs in with an external service, such as Facebook, Microsoft, or Google.</span></span> <span data-ttu-id="26f61-127">여전히 앱 사용자에 대 한 항목이 멤버 자격 데이터베이스를 만들지만 모든 자격 증명을 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-127">The app still creates an entry for the user in the membership database, but does not store any credentials.</span></span> <span data-ttu-id="26f61-128">사용자는 외부 서비스에 로그인 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-128">The user authenticates by signing into the external service.</span></span>

<span data-ttu-id="26f61-129">이 문서에서는 로컬 로그인 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-129">This article looks at the local login scenario.</span></span> <span data-ttu-id="26f61-130">로컬 및 소셜 로그인에 대 한 Web API는 요청을 인증 OAuth2를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-130">For both local and social login, Web API uses OAuth2 to authenticate requests.</span></span> <span data-ttu-id="26f61-131">그러나 자격 증명 흐름은 로컬 및 소셜 로그인에 대 한 다양 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-131">However, the credential flows are different for local and social login.</span></span>

<span data-ttu-id="26f61-132">이 문서에서는 사용자가 로그인 하 고 웹 API에 인증 된 AJAX 호출을 보낼 수 있는 간단한 앱을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-132">In this article, I'll demonstrate a simple app that lets the user log in and send authenticated AJAX calls to a web API.</span></span> <span data-ttu-id="26f61-133">샘플 코드를 다운로드할 수 있습니다 [여기](https://github.com/MikeWasson/LocalAccountsApp)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-133">You can download the sample code [here](https://github.com/MikeWasson/LocalAccountsApp).</span></span> <span data-ttu-id="26f61-134">추가 정보에는 Visual Studio에서 처음부터 샘플을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-134">The readme describes how to create the sample from scratch in Visual Studio.</span></span>

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

<span data-ttu-id="26f61-135">샘플 앱은 데이터 바인딩 및 jQuery AJAX 요청을 보내는 Knockout.js를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-135">The sample app uses Knockout.js for data-binding and jQuery for sending AJAX requests.</span></span> <span data-ttu-id="26f61-136">이 문서에 대 한 Knockout.js를 알 필요가 없습니다 있습니까 AJAX 호출에 집중 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-136">I'll be focusing on the AJAX calls, so you don't need to know Knockout.js for this article.</span></span>

<span data-ttu-id="26f61-137">이 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-137">Along the way, I'll describe:</span></span>

- <span data-ttu-id="26f61-138">클라이언트 쪽에서 어떤 앱에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-138">What the app is doing on the client side.</span></span>
- <span data-ttu-id="26f61-139">서버에서 일어나 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-139">What's happening on the server.</span></span>
- <span data-ttu-id="26f61-140">중간에 HTTP 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-140">The HTTP traffic in the middle.</span></span>

<span data-ttu-id="26f61-141">먼저 몇 가지 OAuth2 용어를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-141">First, we need to define some OAuth2 terminology.</span></span>

- <span data-ttu-id="26f61-142">*리소스*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-142">*Resource*.</span></span> <span data-ttu-id="26f61-143">보호할 수 있는 데이터의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-143">Some piece of data that can be protected.</span></span>
- <span data-ttu-id="26f61-144">*리소스 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-144">*Resource server*.</span></span> <span data-ttu-id="26f61-145">리소스를 호스팅하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-145">The server that hosts the resource.</span></span>
- <span data-ttu-id="26f61-146">*리소스 소유자*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-146">*Resource owner*.</span></span> <span data-ttu-id="26f61-147">리소스에 액세스 권한을 부여할 수 있는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="26f61-147">The entity that can grant permission to access a resource.</span></span> <span data-ttu-id="26f61-148">(일반적으로 사용자입니다.)</span><span class="sxs-lookup"><span data-stu-id="26f61-148">(Typically the user.)</span></span>
- <span data-ttu-id="26f61-149">*클라이언트*: 리소스에 액세스 하려고 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-149">*Client*: The app that wants access to the resource.</span></span> <span data-ttu-id="26f61-150">이 문서에서는 클라이언트는 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-150">In this article, the client is a web browser.</span></span>
- <span data-ttu-id="26f61-151">*액세스 토큰*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-151">*Access token*.</span></span> <span data-ttu-id="26f61-152">리소스에 대 한 액세스 권한을 부여 하는 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-152">A token that grants access to a resource.</span></span>
- <span data-ttu-id="26f61-153">*전달자 토큰*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-153">*Bearer token*.</span></span> <span data-ttu-id="26f61-154">토큰을 사용할 수 있습니다 누구나 속성을 사용 하 여 액세스 토큰에 특정 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-154">A particular type of access token, with the property that anyone can use the token.</span></span> <span data-ttu-id="26f61-155">즉, 클라이언트는 암호화 키 또는 전달자 토큰 사용 하 여 다른 암호 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-155">In other words, a client doesn't need a cryptographic key or other secret to use a bearer token.</span></span> <span data-ttu-id="26f61-156">이런 이유로 전달자 토큰을 https만 사용 해야 하 고 비교적 짧은 만료 시간을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-156">For that reason, bearer tokens should only be used over a HTTPS, and should have relatively short expiration times.</span></span>
- <span data-ttu-id="26f61-157">*권한 부여 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-157">*Authorization server*.</span></span> <span data-ttu-id="26f61-158">액세스 토큰을 제공 하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-158">A server that gives out access tokens.</span></span>

<span data-ttu-id="26f61-159">응용 프로그램 권한 부여 서버와 리소스 서버 모두로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-159">An application can act as both authorization server and resource server.</span></span> <span data-ttu-id="26f61-160">Web API 프로젝트 템플릿은이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-160">The Web API project template follows this pattern.</span></span>

## <a name="local-login-credential-flow"></a><span data-ttu-id="26f61-161">로컬 로그인 자격 증명 흐름</span><span class="sxs-lookup"><span data-stu-id="26f61-161">Local Login Credential Flow</span></span>

<span data-ttu-id="26f61-162">로컬 로그인에 대 한 웹 API에 사용 합니다 [리소스 소유자 암호 흐름](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) OAuth2에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-162">For local login, Web API uses the [resource owner password flow](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) defined in OAuth2.</span></span>

1. <span data-ttu-id="26f61-163">사용자가 클라이언트에 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-163">The user enters a name and password into the client.</span></span>
2. <span data-ttu-id="26f61-164">클라이언트가 권한 부여 서버에 이러한 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-164">The client sends these credentials to the authorization server.</span></span>
3. <span data-ttu-id="26f61-165">권한 부여 서버는 자격 증명을 인증 하 고 액세스 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-165">The authorization server authenticates the credentials and returns an access token.</span></span>
4. <span data-ttu-id="26f61-166">보호 된 리소스에 액세스 하려면 클라이언트는 HTTP 요청의 인증 헤더에 액세스 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-166">To access a protected resource, the client includes the access token in the Authorization header of the HTTP request.</span></span>

![](individual-accounts-in-web-api/_static/image3.png)

<span data-ttu-id="26f61-167">선택 하면 **개별 계정** Web API 프로젝트 템플릿에서 프로젝트에 사용자 자격 증명의 유효성을 검사 하 고 토큰을 발급 하는 권한 부여 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-167">When you select **Individual accounts** in the Web API project template, the project includes an authorization server that validates user credentials and issues tokens.</span></span> <span data-ttu-id="26f61-168">다음 다이어그램에서는 Web API 구성 요소를 기준으로 동일한 자격 증명 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-168">The following diagram shows the same credential flow in terms of Web API components.</span></span>

![](individual-accounts-in-web-api/_static/image4.png)

<span data-ttu-id="26f61-169">이 시나리오에서는 Web API 컨트롤러 리소스 서버로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-169">In this scenario, Web API controllers act as resource servers.</span></span> <span data-ttu-id="26f61-170">인증 필터를 액세스 토큰의 유효성을 검사 하며 **[Authorize]** 특성 리소스를 보호 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-170">An authentication filter validates access tokens, and the **[Authorize]** attribute is used to protect a resource.</span></span> <span data-ttu-id="26f61-171">컨트롤러 또는 작업에 하는 경우는 **[Authorize]** 특성을 컨트롤러에 대 한 모든 요청 또는 작업을 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-171">When a controller or action has the **[Authorize]** attribute, all requests to that controller or action must be authenticated.</span></span> <span data-ttu-id="26f61-172">이 고, 그렇지 권한 부여가 거부 하 고 Web API를 401 (권한 없음된) 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-172">Otherwise, authorization is denied, and Web API returns a 401 (Unauthorized) error.</span></span>

<span data-ttu-id="26f61-173">권한 부여 서버와 둘 다 호출 인증 필터를 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) OAuth2의 세부 정보를 처리 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-173">The authorization server and the authentication filter both call into an [OWIN middleware](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) component that handles the details of OAuth2.</span></span> <span data-ttu-id="26f61-174">이 자습서의 뒷부분에서 자세히의 설계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-174">I'll describe the design in more detail later in this tutorial.</span></span>

## <a name="sending-an-unauthorized-request"></a><span data-ttu-id="26f61-175">권한이 없는 요청을 전송</span><span class="sxs-lookup"><span data-stu-id="26f61-175">Sending an Unauthorized Request</span></span>

<span data-ttu-id="26f61-176">시작 하려면 앱을 실행 하 고 클릭 합니다 **API 호출** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-176">To get started, run the app and click the **Call API** button.</span></span> <span data-ttu-id="26f61-177">요청이 완료 되 면 오류 메시지가 나타납니다 합니다 **결과** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-177">When the request completes, you should see an error message in the **Result** box.</span></span> <span data-ttu-id="26f61-178">이것은 요청에는 액세스 토큰을 포함 하지 않으므로 요청이 인증 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-178">That's because the request does not contain an access token, so the request is unauthorized.</span></span>

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

<span data-ttu-id="26f61-179">합니다 **API 호출** 단추 AJAX 요청을 보냅니다 ~/api/값이 Web API 컨트롤러 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-179">The **Call API** button sends an AJAX request to ~/api/values, which invokes a Web API controller action.</span></span> <span data-ttu-id="26f61-180">AJAX 요청을 보내는 JavaScript 코드의 섹션을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-180">Here is the section of JavaScript code that sends the AJAX request.</span></span> <span data-ttu-id="26f61-181">샘플 앱에서 JavaScript 앱 코드를 모두에 Scripts\app.js 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-181">In the sample app, all of the JavaScript app code is located in the Scripts\app.js file.</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

<span data-ttu-id="26f61-182">사용자가 로그인 될 때까지 전달자 토큰이 없습니다 및 따라서 없는 권한 부여 요청의 헤더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-182">Until the user logs in, there is no bearer token, and therefore no Authorization header in the request.</span></span> <span data-ttu-id="26f61-183">그러면 401 오류를 반환 하는 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-183">This causes the request to return a 401 error.</span></span>

<span data-ttu-id="26f61-184">다음은 HTTP 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-184">Here is the HTTP request.</span></span> <span data-ttu-id="26f61-185">(사용한 [Fiddler](http://www.telerik.com/fiddler) HTTP 트래픽을 캡처할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="26f61-185">(I used [Fiddler](http://www.telerik.com/fiddler) to capture the HTTP traffic.)</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

<span data-ttu-id="26f61-186">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="26f61-186">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

<span data-ttu-id="26f61-187">전달자를 설정 하는 문제를 사용 하 여 응답 Www-authenticate 헤더에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-187">Notice that the response includes a Www-Authenticate header with the challenge set to Bearer.</span></span> <span data-ttu-id="26f61-188">서버 전달자 토큰에서 예상 하는 것이 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-188">That indicates the server expects a bearer token.</span></span>

## <a name="register-a-user"></a><span data-ttu-id="26f61-189">사용자 등록</span><span class="sxs-lookup"><span data-stu-id="26f61-189">Register a User</span></span>

<span data-ttu-id="26f61-190">에 **등록** 섹션 앱의 전자 메일 및 암호를 입력 하 고 클릭 합니다 **등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-190">In the **Register** section of the app, enter an email and password, and click the **Register** button.</span></span>

<span data-ttu-id="26f61-191">이 샘플에 대 한 유효한 전자 메일 주소를 사용할 필요는 없지만 실제 앱 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-191">You don't need to use a valid email address for this sample, but a real app would confirm the address.</span></span> <span data-ttu-id="26f61-192">(참조 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) 암호를 사용 하 여 "Password1!"와 같이 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-192">(See [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) For the password, use something like "Password1!", with an upper case letter, lower case letter, number, and non-alpha-numeric character.</span></span> <span data-ttu-id="26f61-193">클라이언트 쪽 유효성 검사 아웃 두었습니다 간단히 유지 하기 위해 앱 암호 형식에 문제가 있으면 400 (잘못 된 요청) 오류가 발생을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-193">To keep the app simple, I left out client-side validation, so if there is a problem with the password format, you'll get a 400 (Bad Request) error.</span></span>

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

<span data-ttu-id="26f61-194">합니다 **등록** 단추 ~/api/Account/Register에 POST 요청이 전송 /입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-194">The **Register** button sends a POST request to ~/api/Account/Register/.</span></span> <span data-ttu-id="26f61-195">요청 본문에는 이름 및 암호를 보유 하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-195">The request body is a JSON object that holds the name and password.</span></span> <span data-ttu-id="26f61-196">요청을 보내는 JavaScript 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-196">Here is the JavaScript code that sends the request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

<span data-ttu-id="26f61-197">HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="26f61-197">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

<span data-ttu-id="26f61-198">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="26f61-198">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

<span data-ttu-id="26f61-199">이 요청을 처리 합니다 `AccountController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-199">This request is handled by the `AccountController` class.</span></span> <span data-ttu-id="26f61-200">내부적으로 `AccountController` ASP.NET Id를 사용 하 여 멤버 자격 데이터베이스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-200">Internally, `AccountController` uses ASP.NET Identity to manage the membership database.</span></span>

<span data-ttu-id="26f61-201">Visual Studio에서 앱을 로컬로 실행 하는 경우 사용자 계정은 AspNetUsers 테이블에서 LocalDB에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-201">If you run the app locally from Visual Studio, user accounts are stored in LocalDB, in the AspNetUsers table.</span></span> <span data-ttu-id="26f61-202">Visual Studio에서 테이블을 보려면 클릭 합니다 **보기** 메뉴에서 **서버 탐색기**를 차례로 확장 **데이터 연결**.</span><span class="sxs-lookup"><span data-stu-id="26f61-202">To view the tables in Visual Studio, click the **View** menu, select **Server Explorer**, then expand **Data Connections**.</span></span>

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a><span data-ttu-id="26f61-203">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="26f61-203">Get an Access Token</span></span>

<span data-ttu-id="26f61-204">지금까지 우리가 수행 하지 않은 모든 OAuth 있지만 이제 살펴보겠습니다 OAuth 권한 부여 서버 작업에 대 한 액세스 토큰을 요청할 때.</span><span class="sxs-lookup"><span data-stu-id="26f61-204">So far we have not done any OAuth, but now we'll see the OAuth authorization server in action, when we request an access token.</span></span> <span data-ttu-id="26f61-205">에 **로그인** 메일과 암호를 입력 하 고 클릭 하는 샘플 앱의 영역 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-205">In the **Log In** area of the sample app, enter the email and password and click **Log In**.</span></span>

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

<span data-ttu-id="26f61-206">합니다 **로그인** 단추 토큰 끝점에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-206">The **Log In** button sends a request to the token endpoint.</span></span> <span data-ttu-id="26f61-207">다음 양식 url로 인코딩된 데이터를 포함 하는 요청 본문:</span><span class="sxs-lookup"><span data-stu-id="26f61-207">The body of the request contains the following form-url-encoded data:</span></span>

- <span data-ttu-id="26f61-208">grant\_type: "password"</span><span class="sxs-lookup"><span data-stu-id="26f61-208">grant\_type: "password"</span></span>
- <span data-ttu-id="26f61-209">사용자 이름: &lt;사용자의 전자 메일&gt;</span><span class="sxs-lookup"><span data-stu-id="26f61-209">username: &lt;the user's email&gt;</span></span>
- <span data-ttu-id="26f61-210">password: &lt;password&gt;</span><span class="sxs-lookup"><span data-stu-id="26f61-210">password: &lt;password&gt;</span></span>

<span data-ttu-id="26f61-211">AJAX 요청을 보내는 JavaScript 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-211">Here is the JavaScript code that sends the AJAX request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

<span data-ttu-id="26f61-212">요청이 성공 하는 경우 권한 부여 서버는 응답 본문에 액세스 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-212">If the request succeeds, the authorization server returns an access token in the response body.</span></span> <span data-ttu-id="26f61-213">토큰 API에 요청을 보낼 때 나중에 사용할 세션 저장소에 저장 된 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-213">Notice that we store the token in session storage, to use later when sending requests to the API.</span></span> <span data-ttu-id="26f61-214">일부 형태의 인증 (예: 쿠키 기반 인증)와 달리 브라우저 포함 되지 않습니다 자동으로 액세스 토큰은 후속 요청에서.</span><span class="sxs-lookup"><span data-stu-id="26f61-214">Unlike some forms of authentication (such as cookie-based authentication), the browser will not automatically include the access token in subsequent requests.</span></span> <span data-ttu-id="26f61-215">응용 프로그램이 있으므로 명시적으로 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-215">The application must do so explicitly.</span></span> <span data-ttu-id="26f61-216">좋은 것을 제한 하므로 [CSRF 취약점으로 인 한](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-216">That's a good thing, because it limits [CSRF vulnerabilities](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="26f61-217">HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="26f61-217">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

<span data-ttu-id="26f61-218">요청에 사용자의 자격 증명을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-218">You can see that the request contains the user's credentials.</span></span> <span data-ttu-id="26f61-219">있습니다 *해야* HTTPS를 사용 하 여 전송 계층 보안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-219">You *must* use HTTPS to provide transport layer security.</span></span>

<span data-ttu-id="26f61-220">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="26f61-220">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

<span data-ttu-id="26f61-221">가독성을 위해 JSON을 들여쓰기 있습니까 고 매우 긴 액세스 토큰을 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-221">For readability, I indented the JSON and truncated the access token, which is a quite long.</span></span>

<span data-ttu-id="26f61-222">합니다 `access_token`, `token_type`, 및 `expires_in` 속성은 OAuth2 사양에서 정의 됩니다. 다른 속성 (`userName`, `.issued`, 및 `.expires`)는 정보 제공을 위해서만 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-222">The `access_token`, `token_type`, and `expires_in` properties are defined by the OAuth2 spec. The other properties (`userName`, `.issued`, and `.expires`) are just for informational purposes.</span></span> <span data-ttu-id="26f61-223">이러한 추가 속성을 추가 하는 코드를 찾을 수 있습니다는 `TokenEndpoint` 메서드를 /Providers/ApplicationOAuthProvider.cs 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-223">You can find the code that adds those additional properties in the `TokenEndpoint` method, in the /Providers/ApplicationOAuthProvider.cs file.</span></span>

## <a name="send-an-authenticated-request"></a><span data-ttu-id="26f61-224">인증 된 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="26f61-224">Send an Authenticated Request</span></span>

<span data-ttu-id="26f61-225">전달자 토큰을 만들었으므로 API에 인증 된 요청을 가능 했습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-225">Now that we have a bearer token, we can make an authenticated request to the API.</span></span> <span data-ttu-id="26f61-226">이 요청에 Authorization 헤더를 설정 하 여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-226">This is done by setting the Authorization header in the request.</span></span> <span data-ttu-id="26f61-227">클릭 합니다 **API 호출** 하려면 단추를 다시 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="26f61-227">Click the **Call API** button again to see this.</span></span>

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

<span data-ttu-id="26f61-228">HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="26f61-228">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

<span data-ttu-id="26f61-229">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="26f61-229">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a><span data-ttu-id="26f61-230">로그 아웃</span><span class="sxs-lookup"><span data-stu-id="26f61-230">Log Out</span></span>

<span data-ttu-id="26f61-231">브라우저는 자격 증명이 나 액세스 토큰을 캐시 하지 않습니다, 때문에 로그 아웃 토큰을 세션 저장소에서 제거 하 여 "무시"의 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-231">Because the browser does not cache the credentials or the access token, logging out is simply a matter of "forgetting" the token, by removing it from session storage:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a><span data-ttu-id="26f61-232">개별 계정을 프로젝트 템플릿 이해</span><span class="sxs-lookup"><span data-stu-id="26f61-232">Understanding the Individual Accounts Project Template</span></span>

<span data-ttu-id="26f61-233">선택 하면 **개별 계정** 프로젝트는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-233">When you select **Individual Accounts** in the ASP.NET Web Application project template, the project includes:</span></span>

- <span data-ttu-id="26f61-234">OAuth2 권한 부여 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-234">An OAuth2 authorization server.</span></span>
- <span data-ttu-id="26f61-235">사용자 계정 관리에 대 한 Web API 끝점</span><span class="sxs-lookup"><span data-stu-id="26f61-235">A Web API endpoint for managing user accounts</span></span>
- <span data-ttu-id="26f61-236">사용자 계정을 저장 하는 것에 대 한 EF 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-236">An EF model for storing user accounts.</span></span>

<span data-ttu-id="26f61-237">이러한 기능을 구현 하는 기본 응용 프로그램 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-237">Here are the main application classes that implement these features:</span></span>

- <span data-ttu-id="26f61-238">`AccountController`.</span><span class="sxs-lookup"><span data-stu-id="26f61-238">`AccountController`.</span></span> <span data-ttu-id="26f61-239">사용자 계정을 관리 하기 위한 Web API 끝점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-239">Provides a Web API endpoint for managing user accounts.</span></span> <span data-ttu-id="26f61-240">`Register` 작업은이 자습서에서 사용 하는 유일한 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-240">The `Register` action is the only one that we used in this tutorial.</span></span> <span data-ttu-id="26f61-241">클래스의 다른 메서드는 암호 재설정, 소셜 로그인 및 기타 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-241">Other methods on the class support password reset, social logins, and other functionality.</span></span>
- <span data-ttu-id="26f61-242">`ApplicationUser`/Models/IdentityModels.cs에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-242">`ApplicationUser`, defined in /Models/IdentityModels.cs.</span></span> <span data-ttu-id="26f61-243">이 클래스는 멤버 자격 데이터베이스에서 사용자 계정에 대 한 EF 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-243">This class is the EF model for user accounts in the membership database.</span></span>
- <span data-ttu-id="26f61-244">`ApplicationUserManager`/App에 정의 된\_이 클래스에서 파생 됩니다 Start/IdentityConfig.cs [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) 암호 등을 확인 하는 새 사용자 만들기와 같은 사용자 계정에서 작업을 수행 하 고 자동으로 유지 데이터베이스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-244">`ApplicationUserManager`, defined in /App\_Start/IdentityConfig.cs This class derives from [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) and performs operations on user accounts, such as creating a new user, verifying passwords, and so forth, and automatically persists changes to the database.</span></span>
- <span data-ttu-id="26f61-245">`ApplicationOAuthProvider`.</span><span class="sxs-lookup"><span data-stu-id="26f61-245">`ApplicationOAuthProvider`.</span></span> <span data-ttu-id="26f61-246">이 개체는 OWIN 미들웨어를 크롤링합니다 및 미들웨어에서 발생 하는 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-246">This object plugs into the OWIN middleware, and processes events raised by the middleware.</span></span> <span data-ttu-id="26f61-247">파생 되므로 [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-247">It derives from [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).</span></span>

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a><span data-ttu-id="26f61-248">권한 부여 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-248">Configuring the Authorization Server</span></span>

<span data-ttu-id="26f61-249">StartupAuth.cs, 다음 코드는 OAuth2 권한 부여 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-249">In StartupAuth.cs, the following code configures the OAuth2 authorization server.</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

<span data-ttu-id="26f61-250">`TokenEndpointPath` 속성에는 권한 부여 서버 끝점 URL 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-250">The `TokenEndpointPath` property is the URL path to the authorization server endpoint.</span></span> <span data-ttu-id="26f61-251">URL는 전달자 토큰을 가져오기 위해 해당 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-251">That's the URL that app uses to get the bearer tokens.</span></span>

<span data-ttu-id="26f61-252">`Provider` 속성은 OWIN 미들웨어에 연결 하 고 미들웨어에서 발생 하는 이벤트를 처리 하는 공급자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-252">The `Provider` property specifies a provider that plugs into the OWIN middleware, and processes events raised by the middleware.</span></span>

<span data-ttu-id="26f61-253">앱 토큰을 가져오려면 하려고 할 때의 기본 흐름을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-253">Here is the basic flow when the app wants to get a token:</span></span>

1. <span data-ttu-id="26f61-254">앱의 요청을 보내 액세스 토큰을 가져오려면 ~ n /입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-254">To get an access token, the app sends a request to ~/Token.</span></span>
2. <span data-ttu-id="26f61-255">OAuth 미들웨어 호출 `GrantResourceOwnerCredentials` 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-255">The OAuth middleware calls `GrantResourceOwnerCredentials` on the provider.</span></span>
3. <span data-ttu-id="26f61-256">공급자 호출을 `ApplicationUserManager` 클레임 id를 만들고 자격 증명의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-256">The provider calls the `ApplicationUserManager` to validate the credentials and create a claims identity.</span></span>
4. <span data-ttu-id="26f61-257">작업에 성공 하면 공급자는 토큰을 생성 하는 데 사용 되는 인증 티켓을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-257">If that succeeds, the provider creates an authentication ticket, which is used to generate the token.</span></span>

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

<span data-ttu-id="26f61-258">OAuth 미들웨어는 사용자 계정에 대 한 아무것도 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-258">The OAuth middleware doesn't know anything about the user accounts.</span></span> <span data-ttu-id="26f61-259">공급자는 미들웨어 및 ASP.NET Id 간에 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-259">The provider communicates between the middleware and ASP.NET Identity.</span></span> <span data-ttu-id="26f61-260">권한 부여 서버를 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [OWIN OAuth 2.0 권한 부여 서버](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-260">For more information about implementing the authorization server, see [OWIN OAuth 2.0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).</span></span>

### <a name="configuring-web-api-to-use-bearer-tokens"></a><span data-ttu-id="26f61-261">전달자 토큰을 사용 하도록 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="26f61-261">Configuring Web API to use Bearer Tokens</span></span>

<span data-ttu-id="26f61-262">에 `WebApiConfig.Register` 메서드를 다음 코드에서는 Web API 파이프라인에 대 한 인증을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-262">In the `WebApiConfig.Register` method, the following code sets up authentication for the Web API pipeline:</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

<span data-ttu-id="26f61-263">합니다 **HostAuthenticationFilter** 클래스를 사용 하면 전달자 토큰을 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-263">The **HostAuthenticationFilter** class enables authentication using bearer tokens.</span></span>

<span data-ttu-id="26f61-264">합니다 **SuppressDefaultHostAuthentication** 메서드 Web API 요청에는 IIS 또는 OWIN 미들웨어에서 Web API 파이프라인에 도달 하기 전에 발생 하는 인증을 무시 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-264">The **SuppressDefaultHostAuthentication** method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="26f61-265">이런 방식으로 웹 API만 전달자 토큰을 사용 하 여 인증을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-265">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="26f61-266">특히, 앱의 MVC 부분이 폼 인증 쿠키에 자격 증명을 저장 하는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-266">In particular, the MVC portion of your app might use forms authentication, which stores credentials in a cookie.</span></span> <span data-ttu-id="26f61-267">쿠키 기반 인증 CSRF 공격을 방지 하기 위해 위조 방지 토큰을 사용을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-267">Cookie-based authentication requires the use of anti-forgery tokens, to prevent CSRF attacks.</span></span> <span data-ttu-id="26f61-268">웹 Api에 대 한 문제가 위조 방지 토큰을 클라이언트로 보낼 웹 API에 대 한 편리한 방법이 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-268">That's a problem for web APIs, because there is no convenient way for the web API to send the anti-forgery token to the client.</span></span> <span data-ttu-id="26f61-269">(이 문제에 자세한 배경 정보를 참조 하세요 [Web API에서 CSRF 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md).) 호출 **SuppressDefaultHostAuthentication** Web API를 쿠키에 저장 된 자격 증명에서 CSRF 공격에 취약 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-269">(For more background on this issue, see [Preventing CSRF Attacks in Web API](preventing-cross-site-request-forgery-csrf-attacks.md).) Calling **SuppressDefaultHostAuthentication** ensures that Web API is not vulnerable to CSRF attacks from credentials stored in cookies.</span></span>


<span data-ttu-id="26f61-270">클라이언트가 보호 된 리소스를 요청 하면 Web API 파이프라인에서 어떻게 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-270">When the client requests a protected resource, here is what happens in the Web API pipeline:</span></span>

1. <span data-ttu-id="26f61-271">합니다 **HostAuthentication** 토큰 유효성 검사에 OAuth 미들웨어를 호출 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-271">The **HostAuthentication** filter calls the OAuth middleware to validate the token.</span></span>
2. <span data-ttu-id="26f61-272">미들웨어는 토큰 클레임 id를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-272">The middleware converts the token into a claims identity.</span></span>
3. <span data-ttu-id="26f61-273">이 시점에서 요청은 *인증* 있지만 *권한이*합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-273">At this point, the request is *authenticated* but not *authorized*.</span></span>
4. <span data-ttu-id="26f61-274">클레임 id를 검사 하는 권한 부여 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-274">The authorization filter examines the claims identity.</span></span> <span data-ttu-id="26f61-275">클레임에는 해당 리소스에 대 한 사용자의 권한 부여를 요청 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-275">If the claims authorize the user for that resource, the request is authorized.</span></span> <span data-ttu-id="26f61-276">기본적으로 **[Authorize]** 특성은 인증 된 모든 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-276">By default, the **[Authorize]** attribute will authorize any request that is authenticated.</span></span> <span data-ttu-id="26f61-277">그러나 다른 클레임 하거나 역할에서 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-277">However, you can authorize by role or by other claims.</span></span> <span data-ttu-id="26f61-278">자세한 내용은 [인증 및 권한 부여 Web API에서](authentication-and-authorization-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-278">For more information, see [Authentication and Authorization in Web API](authentication-and-authorization-in-aspnet-web-api.md).</span></span>
5. <span data-ttu-id="26f61-279">이전 단계에 성공한 경우 컨트롤러는 보호 된 리소스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-279">If the previous steps are successful, the controller returns the protected resource.</span></span> <span data-ttu-id="26f61-280">그렇지 않으면 클라이언트를 401 (권한 없음된) 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-280">Otherwise, the client receives a 401 (Unauthorized) error.</span></span>

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a><span data-ttu-id="26f61-281">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="26f61-281">Additional Resources</span></span>

- [<span data-ttu-id="26f61-282">ASP.NET Id</span><span class="sxs-lookup"><span data-stu-id="26f61-282">ASP.NET Identity</span></span>](../../../identity/index.md)
- <span data-ttu-id="26f61-283">[VS2013 RC에 대 한 SPA 템플릿의 보안 기능을 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-283">[Understanding Security Features in the SPA Template for VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx).</span></span> <span data-ttu-id="26f61-284">Sun Hongye에서 MSDN 블로그 게시물.</span><span class="sxs-lookup"><span data-stu-id="26f61-284">MSDN blog post by Hongye Sun.</span></span>
- <span data-ttu-id="26f61-285">[웹 API 개별 계정 템플릿-파트 2 분석: 로컬 계정](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-285">[Dissecting the Web API Individual Accounts Template–Part 2: Local Accounts](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/).</span></span> <span data-ttu-id="26f61-286">Dominick Baier 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-286">Blog post by Dominick Baier.</span></span>
- <span data-ttu-id="26f61-287">[인증 및 OWIN 사용 하 여 웹 API를 호스팅할](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-287">[Host authentication and Web API with OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/).</span></span> <span data-ttu-id="26f61-288">적절 한 설명은 `SuppressDefaultHostAuthentication` 및 `HostAuthenticationFilter` Brock Allen 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-288">A good explanation of `SuppressDefaultHostAuthentication` and `HostAuthenticationFilter` by Brock Allen.</span></span>
- <span data-ttu-id="26f61-289">[VS 2013 템플릿에서 ASP.NET Id에서 프로필 정보를 사용자 지정](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-289">[Customizing profile information in ASP.NET Identity in VS 2013 templates](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx).</span></span> <span data-ttu-id="26f61-290">Pranav rastogi MSDN 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-290">MSDN blog post by Pranav Rastogi.</span></span>
- <span data-ttu-id="26f61-291">[UserManager 클래스 ASP.NET Id에 대 한 요청 수명 관리 당](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-291">[Per request lifetime management for UserManager class in ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).</span></span> <span data-ttu-id="26f61-292">Suhas Joshi의 좋은 설명 MSDN 블로그 게시물을 `UserManager` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="26f61-292">MSDN blog post by Suhas Joshi, with a good explanation of the `UserManager` class.</span></span>
