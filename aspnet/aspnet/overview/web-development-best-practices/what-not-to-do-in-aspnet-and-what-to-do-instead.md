---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET에서 안 되 고 대신 | Microsoft Docs
author: Rick-Anderson
description: 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다. 무엇을 해야 이러한 공용을 방지 하기 위한 권장 사항을 제공 하는 중...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65118176"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="7657b-104">ASP.NET에서 하지 말아야 하는 일과 해야 하는 일</span><span class="sxs-lookup"><span data-stu-id="7657b-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="7657b-105">이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="7657b-106">이러한 일반적인 실수를 방지 하려면 수행 해야 하는 것에 대 한 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="7657b-107">기반이 되는 [프레젠테이션](http://vimeo.com/68390507) 하 여 **Damian Edwards** 노르웨이 개발자 회의에서.</span><span class="sxs-lookup"><span data-stu-id="7657b-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="7657b-108">고지 사항</span><span class="sxs-lookup"><span data-stu-id="7657b-108">Disclaimer</span></span>

<span data-ttu-id="7657b-109">이 항목에서는 없습니다 완전 한 가이드로 안전 하 고 효율적인 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="7657b-110">이 항목에서 설명 하지는 보안 및 성능에 대 한 모범 사례를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="7657b-111">만.NET 클래스 및 프로세스와 관련 된 일반적인 실수를 방지 하는 방법을 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="7657b-112">개요</span><span class="sxs-lookup"><span data-stu-id="7657b-112">Overview</span></span>

<span data-ttu-id="7657b-113">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="7657b-114">표준 준수</span><span class="sxs-lookup"><span data-stu-id="7657b-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="7657b-115">컨트롤 어댑터</span><span class="sxs-lookup"><span data-stu-id="7657b-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="7657b-116">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="7657b-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="7657b-117">페이지 및 컨트롤 콜백을</span><span class="sxs-lookup"><span data-stu-id="7657b-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="7657b-118">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="7657b-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="7657b-119">보안</span><span class="sxs-lookup"><span data-stu-id="7657b-119">Security</span></span>](#security)

    - [<span data-ttu-id="7657b-120">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7657b-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="7657b-121">쿠키 없는 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="7657b-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="7657b-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="7657b-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="7657b-123">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="7657b-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="7657b-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="7657b-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="7657b-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="7657b-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="7657b-126">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="7657b-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="7657b-127">PreSendRequestHeaders 및 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="7657b-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="7657b-128">Web Forms 사용 하 여 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="7657b-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="7657b-129">실행 후 제거 작업</span><span class="sxs-lookup"><span data-stu-id="7657b-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="7657b-130">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="7657b-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="7657b-131">Response.Redirect 및 Response.End</span><span class="sxs-lookup"><span data-stu-id="7657b-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="7657b-132">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="7657b-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="7657b-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="7657b-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="7657b-134">긴 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="7657b-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="7657b-135">표준 준수</span><span class="sxs-lookup"><span data-stu-id="7657b-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="7657b-136">컨트롤 어댑터</span><span class="sxs-lookup"><span data-stu-id="7657b-136">Control adapters</span></span>

<span data-ttu-id="7657b-137">권장 사항: 적응형 렌더링에 대 한 컨트롤 어댑터를 사용 하 여 중지 하 고 대신 표준 규격 HTML 및 CSS 미디어 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="7657b-138">컨트롤 어댑터는 다양 한 장치 및 환경에 대 한 사용자 지정 된 프레젠테이션 코드를 렌더링 하는.NET 2.0에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="7657b-139">이제이 적응형 렌더링 CSS 및 HTML을 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="7657b-140">컨트롤 어댑터 사용을 중지 하 고 기존 어댑터를 모두 CSS 및 HTML을 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="7657b-141">자세한 내용은 [미디어 쿼리에](http://www.w3.org/TR/css3-mediaqueries/) 고 [방법: ASP.NET Web forms에 모바일 페이지 추가 / MVC 응용 프로그램](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="7657b-142">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="7657b-142">Style properties on controls</span></span>

<span data-ttu-id="7657b-143">권장 사항: 컨트롤 태그에 스타일 값을 설정 합니다. 중지 하 고 대신 CSS 스타일 시트에서 형식 지정 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="7657b-144">웹 서버 컨트롤에는 수십 개의 인라인 스타일 속성을 설정 하는 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="7657b-145">예를 들어, ForeColor 속성을 컨트롤에 대 한 텍스트의 색을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="7657b-146">CSS 스타일 시트를 통해 더 효율적으로이 동일한 효과 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="7657b-147">스타일 시트를 사용 하 여 스타일 값을 중앙 집중화 하 고 응용 프로그램 전체에서 이러한 값을 설정 하지 마십시오 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="7657b-148">다음 예제에서는 빨간색 집합 텍스트 CSS 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="7657b-149">다음 예제에는 CSS 클래스를 동적으로 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="7657b-150">페이지 및 컨트롤 콜백</span><span class="sxs-lookup"><span data-stu-id="7657b-150">Page and control callbacks</span></span>

<span data-ttu-id="7657b-151">권장 사항: 페이지 및 컨트롤 콜백을 사용 하 여 중지 하 고 대신 다음 중 하나를 사용 합니다. AJAX, UpdatePanel, MVC 동작 메서드, 웹 API 또는 SignalR 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="7657b-152">이전 버전의 ASP.NET 페이지 및 컨트롤의 콜백 메서드를 사용 전체 페이지를 새로 고치지 않고 웹 페이지의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="7657b-153">이제을 통해 부분 페이지 업데이트를 수행할 수 있습니다 [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)합니다 [MVC](../../../mvc/index.md)를 [Web API](../../../web-api/index.md) 또는 [SignalR](../../../signalr/index.md).</span><span class="sxs-lookup"><span data-stu-id="7657b-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="7657b-154">라우팅 및 친숙 한 Url을 사용 하 여 문제가 발생할 수 있으므로 콜백 메서드를 사용 하 여 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="7657b-155">기본적으로 컨트롤에 콜백 메서드를 사용 하지 마십시오 있지만 컨트롤에서이 기능을 사용 하도록 설정한 경우에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="7657b-156">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="7657b-156">Browser capability detection</span></span>

<span data-ttu-id="7657b-157">권장 사항: 정적 브라우저 기능 감지를 사용 하 여 중지 하 고 대신 동적 기능 감지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="7657b-158">이전 버전의 ASP.NET에서는 각 브라우저에 대해 지원 되는 기능의 XML 파일에 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="7657b-159">정적 조회를 통해 검색 기능이 가장 좋은 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="7657b-160">이제 검색할 수 있습니다 동적으로 브라우저에서 같은 기능 검색 프레임 워크를 사용 하 여 지 원하는 기능 [Modernizr](http://modernizr.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="7657b-161">기능 검색 메서드 또는 속성을 사용 하려고 하 고 브라우저에 원하는 결과 생성 하는 경우 참조를 확인 하 여 지원을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="7657b-162">기본적으로 Modernizr 웹 응용 프로그램 템플릿에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="7657b-163">보안</span><span class="sxs-lookup"><span data-stu-id="7657b-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="7657b-164">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7657b-164">Request validation</span></span>

<span data-ttu-id="7657b-165">권장 사항: 사용자 입력의 유효성을 검사 하 고 사용자의 출력을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="7657b-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="7657b-166">요청 유효성 검사에는 각 요청을 검사 하 고 인식 된 위협이 발견 된 경우 요청을 중지 하는 ASP.NET의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="7657b-167">사이트 간 스크립팅 공격 으로부터 응용 프로그램을 보호 하는 것에 대 한 요청 유효성 검사에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="7657b-168">대신, 사용자의 모든 입력의 유효성을 검사 하 고 출력을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="7657b-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="7657b-169">일부 제한 된 경우에 정규식을 사용 하 여 입력의 유효성을 검사 하지만 유효성을 검사 해야 하는 더 복잡 한 경우에서 사용자 입력 값과 일치 하는 경우를 결정 하는.NET 클래스를 사용 하 여 허용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="7657b-170">다음 예제에서는 Uri 클래스의 정적 메서드를 사용 하 여 사용자가 제공 된 Uri의 유효한 지 여부를 결정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="7657b-171">그러나 Uri를 충분히 확인 하는 경우에 확인 해야 지정 되도록 `http` 또는 `https`합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="7657b-172">다음 예제에서는 인스턴스 메서드를 사용 하 여 Uri가 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="7657b-173">사용자 입력을 포함 하 여 SQL 쿼리에서 또는 HTML로 사용자 입력을 렌더링 하기 전에 악성 코드가 포함 되지 않도록 하려면 값을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="7657b-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="7657b-174">HTML을 수 있습니다 사용 하 여 태그의 값을 인코딩하는 &lt;%: %&gt; 아래와 같이 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="7657b-175">HTML Razor 구문에서를 사용 하 여 인코딩하 @ 아래 표시 된 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="7657b-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="7657b-176">다음 예제에 나와 있는 어떻게 HTML로 인코딩 코드 숨김에 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="7657b-177">SQL 명령에 대 한 값을 안전 하 게 인코딩 명령 매개 변수 같은 사용 합니다 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="7657b-178">쿠키 없는 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="7657b-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="7657b-179">권장 사항: 쿠키를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="7657b-180">쿼리 문자열의 인증 정보를 전달 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="7657b-181">따라서 응용 프로그램 인증을 포함 하는 경우에 쿠키를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="7657b-182">중요 한 정보를 저장 하는 쿠키가, 경우에 쿠키에 SSL을 필요로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="7657b-183">다음 예제에서는 폼 인증에서는 SSL을 통해 전송 되는 쿠키를 해야 하는 Web.config 파일에서 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="7657b-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="7657b-184">EnableViewStateMac</span></span>

<span data-ttu-id="7657b-185">권장 사항: False로 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7657b-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="7657b-186">기본적으로 EnableViewStateMac 설정을 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="7657b-187">응용 프로그램 뷰 상태에 사용 하지 않는 경우에 EnableViewStateMac를 false로 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7657b-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="7657b-188">이 값을 false로 설정 하 게 응용 프로그램 사이트 간 스크립팅에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="7657b-189">ASP.NET 4.5.2부터 런타임에서 적용 **EnableViewStateMac = true**합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="7657b-190">False로 설정 하는 경우에 런타임은이 값을 무시 하 고 true로 설정 된 값으로 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="7657b-191">자세한 내용은 [ASP.NET 4.5.2 및 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="7657b-192">다음 예제에서는 EnableViewStateMac true로 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="7657b-193">실제로이 값을 기본적으로 true 이기 때문에 true로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="7657b-194">그러나 설정한 경우이 false로 아무 페이지에서 응용 프로그램에서이 값을 즉시 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="7657b-195">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="7657b-195">Medium trust</span></span>

<span data-ttu-id="7657b-196">권장 사항: 종속 되지 않는 보통 신뢰 (또는 다른 신뢰 수준) 보안 경계로 서입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="7657b-197">부분 신뢰 응용 프로그램을 적절 하 게 보호 하지 않습니다 하 고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="7657b-198">대신 완전 신뢰를 사용 하 고 별도 응용 프로그램 풀에서 신뢰할 수 없는 응용 프로그램을 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="7657b-199">또한 각 응용 프로그램 풀을 고유 id를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="7657b-200">자세한 내용은 [부분 신뢰 ASP.NET 응용 프로그램 격리를 보장 하지 않습니다](https://support.microsoft.com/kb/2698981)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="7657b-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="7657b-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="7657b-202">권장 사항: 보안 설정 안 &lt;appSettings&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="7657b-203">AppSettings 요소는 보안 업데이트에 필요한 많은 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="7657b-204">하지 변경 하거나 이러한 값을 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-204">You should not change or disable these values.</span></span> <span data-ttu-id="7657b-205">업데이트를 배포할 때 이러한 값을 사용 하지 않도록 해야, 즉시 다시 사용 하도록 설정 배포를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="7657b-206">자세한 내용은 참조 하세요 [ASP.NET appSettings 요소](https://msdn.microsoft.com/library/hh975440.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="7657b-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="7657b-207">UrlPathEncode</span></span>

<span data-ttu-id="7657b-208">권장 사항: 사용 하 여 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="7657b-209">UrlPathEncode 메서드는 매우 구체적인 브라우저 호환성 문제를 해결 하려면.NET Framework에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="7657b-210">URL을 적절 하 게 암호화 하지 않습니다 하 고 응용 프로그램에서 사이트 간 스크립팅 보호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="7657b-211">되지 응용 프로그램에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-211">You should never use it in your application.</span></span> <span data-ttu-id="7657b-212">대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="7657b-213">다음 예제에서는 인코딩된 URL 하이퍼링크 컨트롤에 대 한 쿼리 문자열 매개 변수로 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="7657b-214">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="7657b-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="7657b-215">PreSendRequestHeaders 및 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="7657b-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="7657b-216">권장 사항: 관리 되는 모듈을 사용 하 여 이러한 이벤트를 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7657b-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="7657b-217">대신, 필요한 작업을 수행 하는 네이티브 IIS 모듈을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="7657b-218">참조 [네이티브 코드 HTTP 모듈을 만드는](https://msdn.microsoft.com/library/ms693629.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="7657b-219">사용할 수는 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) 하 고 [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) 네이티브 IIS 모듈을 사용 하 여 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="7657b-220">사용 하지 마세요 `PreSendRequestHeaders` 하 고 `PreSendRequestContent` 구현 하는 관리 되는 모듈을 사용 하 여 `IHttpModule`입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="7657b-221">이러한 속성을 설정 하면 비동기 요청을 사용 하 여 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="7657b-222">애플리케이션 요청 라우팅 (ARR) 및 websocket의 조합을 w3wp 충돌을 일으킬 수 있는 액세스 위반 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="7657b-223">예를 들어 iiscore! W3_CONTEXT_BASE::GetIsLastNotification + 68 iiscore.dll에서 액세스 위반 예외 (0xC0000005) 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="7657b-224">Web forms 사용 하 여 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="7657b-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="7657b-225">권장 사항: Web Forms 페이지 수명 주기 이벤트에 대 한 void 메서드 비동기 쓰기를 방지 하 고 대신 [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) 비동기 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="7657b-226">페이지 이벤트를 표시 하는 시점 **비동기** 하 고 **void**, 비동기 코드는 완료 된 시기를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="7657b-227">완료를 추적할 수 있는 방식으로 비동기 코드를 실행 하려면 Page.RegisterAsyncTask를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="7657b-228">단추는 다음 예제에서는 비동기 코드를 포함 하는 처리기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="7657b-229">이 예에서는 권장 아닌 비동기 작업의 간단한 예제로만 제공 하는 문자열 값을 비동기적으로 읽는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="7657b-230">비동기 작업을 사용 하는 경우 Http 런타임 대상 프레임 워크로 설정 4.5 (또는 그 이상)의 Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="7657b-231">대상 프레임 워크를 설정을 4.5으로 설정 하면 새 동기화 컨텍스트에서.NET 4.5에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="7657b-232">이 값은 기본적으로 Visual Studio에서 새 프로젝트에서 설정 되지만 되지 설정 기존 프로젝트를 사용 하 여 작업 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7657b-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="7657b-233">실행 후 제거 작업</span><span class="sxs-lookup"><span data-stu-id="7657b-233">Fire-and-forget work</span></span>

<span data-ttu-id="7657b-234">권장 사항: Asp.net 요청을 처리할 때 (이러한 ThreadPool.QueueUserWorkItem 메서드 호출 또는 반복적으로 대리자를 호출 하는 타이머를 만드는) 실행 후 제거 작업을 시작 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7657b-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="7657b-235">응용 프로그램에 ASP.NET에서 실행 되는 실행 후 제거 작업을 하는 경우 응용 프로그램 동기화를 가져올 수 있습니다. 언제 든 지 응용 프로그램 도메인을 제거할 수 없습니다. 즉, 진행 중인 프로세스는 더 이상 응용 프로그램의 현재 상태를 일치 시킬 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="7657b-236">이 유형의 ASP.NET 외부에서 작업을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="7657b-237">진행 중인 작업을 수행 하는 데 Azure의 웹 작업, Windows 서비스 또는 작업자 역할을 사용 하 고 다른 프로세스에서 해당 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="7657b-238">Asp.net이 작업을 수행 해야 하는 경우 라는 Nuget 패키지를 추가할 수 있습니다 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="7657b-239">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="7657b-239">Request entity body</span></span>

<span data-ttu-id="7657b-240">권장 사항: 처리기의 이벤트를 실행 하기 전에 Request.Form 또는 Request.InputStream 읽기를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="7657b-241">가능한 한 빨리 Request.Form 또는 Request.InputStream에서 읽는 것은 동안 처리기의 실행 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7657b-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="7657b-242">Mvc에서 컨트롤러는 처리기 이며 실행 이벤트 동작 메서드를 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7657b-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="7657b-243">Web Forms 페이지 처리기 이며 Page.Init 이벤트가 발생할 때 실행 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="7657b-244">이전 실행 이벤트 요청 엔터티 본문을 읽는 경우 요청을 처리 하는 방해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="7657b-245">를 실행 하기 전에 요청 엔터티 본문을 읽는 해야 하는 경우 하나를 사용 [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) 하거나 [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="7657b-246">GetBufferlessInputStream를 사용 하는 경우 요청에서 원시는 스트림을 가져오려면 하 고 전체 요청을 처리 하는 것에 대 한 책임을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="7657b-247">GetBufferlessInputStream를 호출한 후 Request.Form 및 Request.InputStream은 사용할 수 없습니다 ASP.NET에서 채우지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="7657b-248">GetBufferedInputStream를 사용 하는 경우 요청에서 스트림의 복사본을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="7657b-249">ASP.NET 다른 복사본을 채우므로 Request.Form 및 Request.InputStream 요청에서 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="7657b-250">Response.Redirect 및 Response.End</span><span class="sxs-lookup"><span data-stu-id="7657b-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="7657b-251">권장 사항: 호출한 후 스레드가 처리 하는 방법을의 차이점에 유의 [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="7657b-252">합니다 [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) 메서드 Response.End 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="7657b-253">동기 프로세스에서 Request.Redirect를 호출 하면 현재 스레드가 즉시 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="7657b-254">그러나 비동기 프로세스에서 Response.Redirect를 호출를 중단 하지 않습니다 현재 스레드에서 코드 실행 요청에 대해 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="7657b-255">비동기 프로세스에서 코드 실행을 중지 하려면 메서드에서 작업을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="7657b-256">MVC 프로젝트에서 Response.Redirect를 호출 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="7657b-257">된 RedirectResult 대신 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="7657b-258">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="7657b-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="7657b-259">권장 사항: EnableViewState, 대신 ViewStateMode를 사용 하는 컨트롤 보기 상태를 사용 하는 세부적인 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="7657b-260">EnableViewState Page 지시문에서 false로 설정한 경우 뷰 상태 페이지 내에서 모든 컨트롤에 대해 비활성화 되 고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="7657b-261">페이지에만 특정 컨트롤에 대 한 뷰 상태를 사용 하려는 경우 페이지에 대 한 ViewStateMode 사용 안 함으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="7657b-262">그런 다음 실제로 뷰 상태를 해야 하는 컨트롤만에 ViewStateMode Enabled로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="7657b-263">만 필요로 하는 컨트롤의 뷰 상태를 사용 하 여 웹 페이지에 대 한 보기 상태의 크기를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="7657b-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="7657b-264">SqlMembershipProvider</span></span>

<span data-ttu-id="7657b-265">권장 사항: 범용 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="7657b-266">현재 프로젝트 템플릿에서 SqlMembershipProvider 바뀌었습니다 [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)를 NuGet 패키지로 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="7657b-267">SqlMembershipProvider 템플릿의 이전 버전을 사용 하 여 빌드된 프로젝트를 사용 하는 경우 Universal Providers를 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="7657b-268">Universal Providers Entity Framework에서 지원 되는 모든 데이터베이스를 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="7657b-269">자세한 내용은 [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="7657b-270">장기 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="7657b-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="7657b-271">권장 사항: 사용 하 여 [Websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) 하거나 [SignalR](../../../signalr/index.md) 연결 된 클라이언트 및 사용 하 여 비동기 I/O 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="7657b-272">장기 실행 요청 웹 응용 프로그램에서 예기치 않은 결과 및 성능 저하를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="7657b-273">요청에 대 한 기본 제한 시간 설정은 110 초입니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="7657b-274">를 사용 하는 장기 실행 요청을 사용 하 여 세션 상태를 사용 하는 경우 ASP.NET 세션 개체에 대 한 잠금을 110 초 후에 출시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="7657b-275">그러나 잠금이 해제 되 고 작업을 성공적으로 완료 되지 않을 수 하는 경우 세션 개체에 대 한 작업 중 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="7657b-276">첫 번째 요청이 실행 되는 동안 사용자의 두 번째 요청을 차단 된 경우 두 번째 요청 일관성이 없는 상태에서 세션 개체를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="7657b-277">응용 프로그램 차단 (또는 동기) I/O 작업에 포함 된 경우 응용 프로그램 응답 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="7657b-278">성능 향상을 위해.NET Framework의 비동기 I/O 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="7657b-279">또한 서버에 연결 하는 클라이언트에 대 한 Websocket 또는 SignalR를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="7657b-280">이러한 기능은 효율적으로 장기 실행 요청을 처리 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7657b-280">These features are designed to efficiently handle long-running requests.</span></span>
