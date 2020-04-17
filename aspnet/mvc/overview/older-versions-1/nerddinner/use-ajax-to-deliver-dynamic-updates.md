---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX를 사용하여 동적 업데이트를 제공 | 마이크로 소프트 문서
author: rick-anderson
description: 10단계는 로그인한 사용자가 저녁 식사에 참석하는 데 관심이 있는 RSVP에 대한 지원을 구현하며, 저녁 식사 세부 사항에 통합된 Ajax 기반 접근 방식을 사용하여...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541249"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="959f0-103">AJAX를 사용하여 동적 업데이트 제공</span><span class="sxs-lookup"><span data-stu-id="959f0-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="959f0-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="959f0-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="959f0-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="959f0-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="959f0-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 10단계입니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="959f0-107">10단계는 저녁 식사 세부 정보 페이지에 통합된 Ajax 기반 접근 방식을 사용하여 로그인한 사용자가 저녁 식사에 참석하는 데 관심이 있는 RSVP에 대한 지원을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="959f0-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="959f0-109">얼간이 디너 단계 10: AJAX RSVPs 허용 허용</span><span class="sxs-lookup"><span data-stu-id="959f0-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="959f0-110">이제 로그인한 사용자에 대한 지원을 RSVP에 지원하여 저녁 식사에 참석하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="959f0-111">저녁 식사 세부 정보 페이지에 통합된 AJAX 기반 접근 방식을 사용하여 이 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="959f0-112">사용자가 RSVP인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="959f0-113">사용자는 */Dinners/Details/[id] URL을*방문하여 특정 저녁 식사에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="959f0-114">Details() 작업 메서드는 다음과 같이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="959f0-115">RSVP 지원을 구현하는 첫 번째 단계는 Dinner 개체에 "IsUserRegistered(사용자 이름)" 도우미 메서드를 추가하는 것입니다(이전에 빌드한 Dinner.cs 부분 클래스 내에서).</span><span class="sxs-lookup"><span data-stu-id="959f0-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="959f0-116">이 도우미 메서드는 사용자가 현재 Dinner에 대 한 RSVP'd 인지 여부에 따라 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="959f0-117">그런 다음 Details.aspx 보기 템플릿에 다음 코드를 추가하여 사용자가 이벤트에 등록되었는지 여부를 나타내는 적절한 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="959f0-118">이제 사용자가 저녁 식사를 방문하면 이 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="959f0-119">그리고 그들은 저녁 식사를 방문 할 때 그들은 아래 메시지가 표시됩니다 에 대한 등록되지 않습니다 :</span><span class="sxs-lookup"><span data-stu-id="959f0-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="959f0-120">레지스터 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="959f0-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="959f0-121">이제 세부 정보 페이지에서 저녁 식사를 위해 사용자가 RSVP에 사용할 수 있도록 하는 데 필요한 기능을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="959f0-122">이를 구현하기 위해 \Controllers 디렉토리를 마우스 오른쪽 단추로 클릭하고 컨트롤러 추가&gt;메뉴 명령을 선택하여 새 "RSVPController" 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="959f0-123">우리는 인수로 Dinner에 대한 ID를 취하는 새로운 RSVPController 클래스 내에서 "등록"작업 메서드를 구현하고, 적절한 Dinner 개체를 검색하고, 로그인 한 사용자가 현재 등록 한 사용자 목록에 있는지 확인하고 RSVP 개체를 추가하지 않는 지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="959f0-124">작업 메서드의 출력으로 간단한 문자열을 반환 하는 방법을 위에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="959f0-125">보기 템플릿 내에 이 메시지를 포함시킬 수 있지만 너무 작기 때문에 컨트롤러 기본 클래스에서 Content() 도우미 메서드를 사용하고 위와 같은 문자열 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="959f0-126">AJAX를 사용하여 RSVPForEvent 작업 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="959f0-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="959f0-127">AJAX를 사용하여 세부 정보 보기에서 등록 작업 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="959f0-128">이를 구현하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="959f0-129">먼저 두 개의 스크립트 라이브러리 참조를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="959f0-130">첫 번째 라이브러리는 AJAX 클라이언트 측 스크립트 라이브러리의 핵심 ASP.NET 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="959f0-131">이 파일은 약 24k 크기 (압축)이며 핵심 클라이언트 측 AJAX 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="959f0-132">두 번째 라이브러리에는 ASP.NET MVC의 기본 제공 AJAX 도우미 메서드와 통합되는 유틸리티 함수가 포함되어 있습니다(곧 사용하겠습니다).</span><span class="sxs-lookup"><span data-stu-id="959f0-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="959f0-133">그런 다음 앞에서 추가한 뷰 템플릿 코드를 업데이트하여 "이 이벤트에 등록되지 않았습니다" 메시지를 보내는 대신 푸시할 때 RSVPForEvent 작업 메서드를 호출하는 AJAX 호출을 수행하는 링크를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="959f0-134">위에서 사용하는 Ajax.ActionLink() 도우미 메서드는 ASP.NET MVC에 기본 제공되며 표준 탐색을 수행하는 대신 링크를 클릭할 때 작업 메서드를 호출하는 것을 제외하고는 Html.ActionLink() 도우미 메서드와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="959f0-135">위에서는 "RSVP" 컨트롤러에서 "등록" 작업 메서드를 호출하고 DinnerID를 "id" 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="959f0-136">우리가 전달하는 마지막 AjaxOptions 매개 변수는 작업 메서드에서 반환 된 콘텐츠를 &lt;가져&gt; 와서 ID가 "rsvpmsg"인 페이지의 HTML div 요소를 업데이트하려는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="959f0-137">이제 사용자가 저녁 식사를 탐색할 때 아직 등록되지 않은 경우 RSVP에 대한 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="959f0-138">"이 이벤트에 대한 RSVP" 링크를 클릭하면 RSVP 컨트롤러의 레지스터 작업 메서드에 대한 AJAX 호출을 수행하며 완료되면 다음과 같은 업데이트된 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="959f0-139">이 AJAX 호출을 할 때 관련된 네트워크 대역폭과 트래픽은 정말 가볍습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="959f0-140">사용자가 "이 이벤트에 대한 RSVP" 링크를 클릭하면 와이어에서 아래와 같이 보이는 */Dinners/Register/1* URL에 대한 작은 HTTP POST 네트워크 요청이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="959f0-141">그리고 우리의 등록 작업 방법의 응답은 단순히 :</span><span class="sxs-lookup"><span data-stu-id="959f0-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="959f0-142">이 경량 호출은 빠르며 느린 네트워크에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="959f0-143">j쿼리 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="959f0-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="959f0-144">구현한 AJAX 기능은 매우 빠르게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="959f0-145">그러나 때로는 사용자가 RSVP 링크가 새 텍스트로 대체되었음을 알 수 없을 정도로 빠르게 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="959f0-146">결과를 좀 더 분명하게 하기 위해 업데이트 메시지에 주의를 끌기 위해 간단한 애니메이션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="959f0-147">기본 ASP.NET MVC 프로젝트 템플릿에는 microsoft에서 지원하는 훌륭한 (그리고 매우 인기 있는) 오픈 소스 자바스크립트 라이브러리인 jQuery가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="959f0-148">jQuery는 좋은 HTML DOM 선택 및 효과 라이브러리를 포함하여 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="959f0-149">jQuery를 사용하려면 먼저 스크립트 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="959f0-150">사이트 내의 다양한 위치에서 jQuery를 사용할 예정이므로 모든 페이지가 사용할 수 있도록 Site.master 마스터 페이지 파일 내에 스크립트 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="959f0-151">*팁: VS 2008 SP1용 자바스크립트 인텔리센스 핫픽스를 설치하여 자바스크립트 파일(jQuery 포함)에 대한 풍부한 인텔리센스 지원을 지원했는지 확인합니다. 다음 에서 다운로드할 수 있습니다.http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="959f0-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="959f0-152">JQuery를 사용하여 작성된 코드는 CSS 선택기에서 하나 이상의 HTML 요소를 검색하는 글로벌 "$()" JavaScript 메서드를 사용하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="959f0-153">예를 들어 *$("#rsvpmsg")는* rsvpmsg의 ID가 있는 HTML 요소를 선택하고 *$(".something")는* "무언가" CSS 클래스 이름을 가진 모든 요소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="959f0-154">또한 다음과 같은 선택기 쿼리를 사용하여 "확인된 모든 라디오 단추 반환"과 같은 고급 *쿼리를 작성할@type@checked*수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="959f0-155">요소를 선택한 후에는 메서드를 호출하여 숨기는 것과 같은 작업을 수행할 수 *#rsvpmsg 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="959f0-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="959f0-156">RSVP 시나리오의 경우 "rsvpmsg" div를 &lt;&gt; 선택하고 텍스트 콘텐츠의 크기를 애니메이션하는 "AnimateRSVPMessage"라는 간단한 자바스크립트 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="959f0-157">아래 코드는 텍스트를 작게 시작한 다음 400밀리초 기간 동안 증가하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="959f0-158">그런 다음 AjaX 호출이 성공적으로 완료된 후 Ajax.ActionLink(Ajax.ActionLink() 도우미 메서드에 이름을 전달하여 호출할 자바스크립트 함수를 와이어업할 수 있습니다(AjaxOptions "OnSuccess" 이벤트 속성 사용).</span><span class="sxs-lookup"><span data-stu-id="959f0-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="959f0-159">이제 "이 이벤트에 대한 RSVP" 링크를 클릭하고 AJAX 호출이 성공적으로 완료되면 다시 전송된 콘텐츠 메시지가 애니메이션화되고 커집니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="959f0-160">AjaxOptions 개체는 "OnSuccess" 이벤트를 제공하는 것 외에도 OnBegin, OnFailure 및 OnComplete 이벤트를 노출합니다(다양한 다른 속성 및 유용한 옵션과 함께).</span><span class="sxs-lookup"><span data-stu-id="959f0-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="959f0-161">정리 - RSVP 부분 뷰리팩터링</span><span class="sxs-lookup"><span data-stu-id="959f0-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="959f0-162">우리의 세부 정보 보기 템플릿은 조금 길어지기 시작하여 초과 근무는 이해하기가 조금 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="959f0-163">코드 가독성을 향상시키기 위해 세부 정보 페이지의 모든 RSVP 보기 코드를 캡슐화하는 부분 보기(RSVPStatus.ascx)를 만들어 마무리해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="959f0-164">\View\Dinners 폴더를 마우스 오른쪽 단추로 클릭한 다음 추가&gt;보기 메뉴 명령을 선택하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="959f0-165">우리는 그것의 강력한 형식의 ViewModel로 Dinner 개체를 걸릴 거 야.</span><span class="sxs-lookup"><span data-stu-id="959f0-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="959f0-166">그런 다음 Details.aspx 보기에서 RSVP 콘텐츠를 복사/붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="959f0-167">일단 우리가 그, 또 다른 부분 보기를 만들 수 있습니다-EditAndDeleteLinks.ascx-우리의 편집 및 링크 보기 보기 코드를 캡슐화.</span><span class="sxs-lookup"><span data-stu-id="959f0-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="959f0-168">또한 Dinner 개체를 강력한 형식의 ViewModel로 가져 와서 Details.aspx 보기에서 편집 및 삭제 논리를 복사/붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="959f0-169">그런 다음 세부 정보 보기 템플릿을 사용하여 아래쪽에 두 개의 Html.RenderPartial() 메서드 호출만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="959f0-170">이렇게 하면 코드를 읽고 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="959f0-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="959f0-171">Next Step</span></span>

<span data-ttu-id="959f0-172">이제 AJAX를 더욱 사용하고 응용 프로그램에 대화형 매핑 지원을 추가하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="959f0-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="959f0-173">[이전](secure-applications-using-authentication-and-authorization.md)
> [다음](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="959f0-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
