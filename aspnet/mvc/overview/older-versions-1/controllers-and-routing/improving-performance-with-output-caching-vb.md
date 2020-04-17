---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 출력 캐싱(VB)으로 성능 향상 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 출력 캐싱을 활용하여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 알아봅니다. 당신은 ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: e18d4c5132d4dccc97f1465e7885c9c47a0edab1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542692"
---
# <a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="282e5-104">출력 캐싱을 통한 성능 향상(VB)</span><span class="sxs-lookup"><span data-stu-id="282e5-104">Improving Performance with Output Caching (VB)</span></span>

<span data-ttu-id="282e5-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="282e5-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="282e5-106">이 자습서에서는 출력 캐싱을 활용하여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="282e5-107">컨트롤러 작업에서 반환된 결과를 캐시하여 새 사용자가 작업을 호출할 때마다 동일한 콘텐츠를 만들 필요가 없도록 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="282e5-108">이 자습서의 목표는 출력 캐시를 활용하여 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="282e5-109">출력 캐시를 사용하면 컨트롤러 작업에서 반환되는 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="282e5-110">이렇게 하면 동일한 컨트롤러 작업이 호출될 때마다 동일한 콘텐츠를 생성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="282e5-111">예를 들어 ASP.NET MVC 응용 프로그램이 Index라는 보기의 데이터베이스 레코드 목록을 표시한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="282e5-112">일반적으로 사용자가 Index 뷰를 반환하는 컨트롤러 작업을 호출할 때마다 데이터베이스 쿼리를 실행하여 데이터베이스 레코드 집합을 데이터베이스에서 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="282e5-113">반면에 출력 캐시를 활용하면 사용자가 동일한 컨트롤러 작업을 호출할 때마다 데이터베이스 쿼리를 실행하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="282e5-114">컨트롤러 작업에서 재생성되는 대신 캐시에서 뷰를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="282e5-115">캐싱을 사용하면 서버에서 중복 작업을 수행하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="282e5-116">출력 캐싱 사용</span><span class="sxs-lookup"><span data-stu-id="282e5-116">Enabling Output Caching</span></span>

<span data-ttu-id="282e5-117">개별 컨트롤러 작업 또는 &lt;전체&gt; 컨트롤러 클래스에 OutputCache 특성을 추가하여 출력 캐싱을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="282e5-118">예를 들어 목록 1의 컨트롤러는 Index()라는 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="282e5-119">Index() 작업의 출력은 10초 동안 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="282e5-120">**목록 1 – 컨트롤러\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="282e5-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

<span data-ttu-id="282e5-121">ASP.NET MVC의 베타 버전에서는 출력 캐싱이 와 같은 [http://www.MySite.com/](http://www.mysite.com/)URL에 대해 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="282e5-122">대신 에 대한 [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)URL을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>

<span data-ttu-id="282e5-123">목록 1에서 Index() 작업의 출력은 10초 동안 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="282e5-124">원하는 경우 훨씬 더 긴 캐시 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="282e5-125">예를 들어 컨트롤러 작업의 출력을 하루 동안 캐시하려는 경우 86400초(60초 \* 60분 \* 24시간)의 캐시 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="282e5-126">지정한 시간 동안 콘텐츠가 캐시된다는 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="282e5-127">메모리 리소스가 부족해지면 캐시가 자동으로 콘텐츠를 제거하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="282e5-128">목록 1의 홈 컨트롤러는 목록 2의 인덱스 보기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="282e5-129">이 보기에 대해 특별한 것은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-129">There is nothing special about this view.</span></span> <span data-ttu-id="282e5-130">색인 보기에는 단순히 현재 시간이 표시됩니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="282e5-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="282e5-131">**목록 2 – 보기\홈\인덱스.aspx**</span><span class="sxs-lookup"><span data-stu-id="282e5-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="282e5-132">**그림 1 – 캐시된 인덱스 보기**</span><span class="sxs-lookup"><span data-stu-id="282e5-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="282e5-134">브라우저의 주소 표시줄에 URL /Home/Index를 입력하고 브라우저에서 새로 고침/다시로드 버튼을 반복적으로 눌러 Index() 작업을 여러 번 호출하면 인덱스 보기에 표시되는 시간이 10초 동안 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="282e5-135">뷰가 캐시되므로 동시에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="282e5-136">응용 프로그램을 방문하는 모든 사람에게 동일한 보기가 캐시된다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="282e5-137">Index() 작업을 호출하는 모든 사용자는 인덱스 보기의 캐시된 버전과 동일한 캐시된 버전을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="282e5-138">즉, 인덱스 보기를 제공하기 위해 웹 서버가 수행해야 하는 작업량이 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="282e5-139">목록 2의 보기는 정말 간단한 일을하는 일이.</span><span class="sxs-lookup"><span data-stu-id="282e5-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="282e5-140">뷰에 현재 시간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-140">The view just displays the current time.</span></span> <span data-ttu-id="282e5-141">그러나 데이터베이스 레코드 집합을 표시하는 뷰를 쉽게 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="282e5-142">이 경우 뷰를 반환하는 컨트롤러 작업이 호출될 때마다 데이터베이스 레코드 집합을 데이터베이스에서 검색할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="282e5-143">캐싱을 사용하면 웹 서버와 데이터베이스 서버가 모두 수행해야 하는 작업량을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="282e5-144">MVC 보기에서 &lt;페이지 %@&gt; OutputCache % 지시문을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="282e5-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="282e5-145">이 지시문은 Web Forms 세계에서 흘러넘치며 ASP.NET MVC 응용 프로그램에서 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="282e5-146">콘텐츠가 캐시되는 위치</span><span class="sxs-lookup"><span data-stu-id="282e5-146">Where Content is Cached</span></span>

<span data-ttu-id="282e5-147">기본적으로 OutputCache&gt; 특성을 &lt;사용하면 콘텐츠가 웹 서버, 프록시 서버 및 웹 브라우저의 세 위치에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="282e5-148">&lt;OutputCache&gt; 특성의 위치 속성을 수정하여 콘텐츠가 캐시되는 위치를 정확하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="282e5-149">위치 속성을 다음 값 중 하나로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="282e5-150">· 어떤</span><span class="sxs-lookup"><span data-stu-id="282e5-150">· Any</span></span>
> 
> <span data-ttu-id="282e5-151">· 클라이언트</span><span class="sxs-lookup"><span data-stu-id="282e5-151">· Client</span></span>
> 
> <span data-ttu-id="282e5-152">· 다운스트림</span><span class="sxs-lookup"><span data-stu-id="282e5-152">· Downstream</span></span>
> 
> <span data-ttu-id="282e5-153">· 서버</span><span class="sxs-lookup"><span data-stu-id="282e5-153">· Server</span></span>
> 
> <span data-ttu-id="282e5-154">· 없음</span><span class="sxs-lookup"><span data-stu-id="282e5-154">· None</span></span>
> 
> <span data-ttu-id="282e5-155">· 서버앤클라이언트</span><span class="sxs-lookup"><span data-stu-id="282e5-155">· ServerAndClient</span></span>

<span data-ttu-id="282e5-156">기본적으로 Location 속성에는 Any 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="282e5-157">그러나 브라우저에서만 캐시하거나 서버에서만 캐시하려는 상황이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="282e5-158">예를 들어 각 사용자에 대해 개인 설정된 정보를 캐싱하는 경우 서버의 정보를 캐시해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="282e5-159">다른 사용자에게 다른 정보를 표시하는 경우 클라이언트에서만 정보를 캐시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="282e5-160">예를 들어 목록 3의 컨트롤러는 현재 사용자 이름을 반환하는 GetName() 이라는 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="282e5-161">잭이 웹 사이트에 로그인하여 GetName() 작업을 호출하면 작업이 "Hi Jack"문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="282e5-162">그 후 Jill이 웹 사이트에 로그인하여 GetName() 작업을 호출하면 "Hi Jack"이라는 문자열도 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="282e5-163">Jack이 처음에 컨트롤러 작업을 호출한 후 모든 사용자에 대해 문자열이 웹 서버에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="282e5-164">**목록 3 – 컨트롤러\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="282e5-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="282e5-165">대부분의 경우 목록 3의 컨트롤러가 원하는 방식으로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="282e5-166">Jill에 "Hi Jack"이라는 메시지를 표시하고 싶지 는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="282e5-167">서버 캐시에서 개인 설정된 콘텐츠를 캐시해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="282e5-168">그러나 성능을 향상시키기 위해 브라우저 캐시에서 개인 설정된 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="282e5-169">브라우저에서 콘텐츠를 캐시하고 사용자가 동일한 컨트롤러 작업을 여러 번 호출하면 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="282e5-170">목록 4의 수정된 컨트롤러는 GetName() 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="282e5-171">그러나 콘텐츠는 서버가 아닌 브라우저에서만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="282e5-172">이렇게 하면 여러 사용자가 GetName() 메서드를 호출할 때 각 사용자는 다른 사용자의 사용자 이름이 아닌 자신의 사용자 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="282e5-173">**목록 4 – 컨트롤러\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="282e5-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="282e5-174">목록 4의 &lt;&gt; OutputCache 특성에는 ValueCacheLocation.Client값으로 설정된 위치 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="282e5-175">OutputCache &lt;&gt; 특성에는 NoStore 속성도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="282e5-176">NoStore 속성은 프록시 서버와 브라우저에 캐시된 콘텐츠의 영구 복사본을 저장하지 않도록 알리는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="282e5-177">출력 캐시 변경</span><span class="sxs-lookup"><span data-stu-id="282e5-177">Varying the Output Cache</span></span>

<span data-ttu-id="282e5-178">경우에 따라 동일한 콘텐츠의 다른 캐시 된 버전을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="282e5-179">예를 들어 마스터/세부 정보 페이지를 만드는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="282e5-180">마스터 페이지에는 영화 제목 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="282e5-181">제목을 클릭하면 선택한 동영상에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="282e5-182">세부 정보 페이지를 캐시하면 클릭한 동영상에 관계없이 동일한 동영상에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="282e5-183">첫 번째 사용자가 선택한 첫 번째 동영상이 모든 향후 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="282e5-184">&lt;OutputCache&gt; 특성의 VaryByParam 속성을 이용하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="282e5-185">이 속성을 사용하면 양식 매개 변수 또는 쿼리 문자열 매개 변수가 다를 때 동일한 콘텐츠의 다른 캐시된 버전을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="282e5-186">예를 들어 목록 5의 컨트롤러는 Master() 및 Details()라는 두 개의 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="282e5-187">마스터() 작업은 동영상 제목 목록을 반환하고 세부 정보() 작업은 선택한 동영상에 대한 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="282e5-188">**목록 5 – 컨트롤러\영화Controller.vb**</span><span class="sxs-lookup"><span data-stu-id="282e5-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="282e5-189">마스터() 작업에는 값이 "none"인 VaryByParam 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="282e5-190">Master() 작업이 호출되면 동일한 캐시된 버전의 마스터 뷰가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="282e5-191">모든 양식 매개 변수 또는 쿼리 문자열 매개 변수는 무시됩니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="282e5-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="282e5-192">**그림 2 – /영화/마스터 보기**</span><span class="sxs-lookup"><span data-stu-id="282e5-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="282e5-194">**그림 3 – /영화/세부 정보 보기**</span><span class="sxs-lookup"><span data-stu-id="282e5-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="282e5-196">세부 정보() 작업에는 값 "Id"가 있는 VaryByParam 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="282e5-197">Id 매개 변수의 다른 값이 컨트롤러 작업에 전달되면 세부 정보 보기의 다른 캐시된 버전이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="282e5-198">VarByParam 속성을 사용하면 캐싱이 더 많아지고 더 적지 않다는 것을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="282e5-199">세부 정보 보기의 다른 캐시된 버전이 Id 매개 변수의 각 다른 버전에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="282e5-200">[바바이파라임] 속성을 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="282e5-201">\*= 양식 또는 쿼리 문자열 매개 변수가 다를 때마다 다른 캐시된 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="282e5-202">없음 = 다른 캐시된 버전을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="282e5-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="282e5-203">세미콜론 매개 변수 목록 = 목록의 양식 또는 쿼리 문자열 매개 변수가 다를 때마다 다른 캐시된 버전 만들기</span><span class="sxs-lookup"><span data-stu-id="282e5-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

#### <a name="creating-a-cache-profile"></a><span data-ttu-id="282e5-204">캐시 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="282e5-204">Creating a Cache Profile</span></span>

<span data-ttu-id="282e5-205">&lt;OutputCache&gt; 특성의 속성을 수정하여 출력 캐시 속성을 구성하는 대신 웹 구성(web.config) 파일에서 캐시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="282e5-206">웹 구성 파일에 캐시 프로필을 만들면 몇 가지 중요한 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="282e5-207">먼저 웹 구성 파일에서 출력 캐싱을 구성하여 컨트롤러 작업이 한 중앙 위치에서 콘텐츠를 캐시하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="282e5-208">하나의 캐시 프로필을 만들고 프로파일을 여러 컨트롤러 또는 컨트롤러 작업에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="282e5-209">둘째, 응용 프로그램을 다시 컴파일하지 않고 웹 구성 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="282e5-210">프로덕션에 이미 배포된 응용 프로그램에 대해 캐싱을 사용하지 않도록 설정해야 하는 경우 웹 구성 파일에 정의된 캐시 프로필을 수정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="282e5-211">웹 구성 파일에 대한 모든 변경 내용이 자동으로 감지되고 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="282e5-212">예를 들어 &lt;목록&gt; 6의 웹 구성 섹션은 Cache1Hour라는 캐시 프로필을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="282e5-213">캐싱 &lt;&gt; 섹션은 웹 &lt;구성 파일의 system.web&gt; 섹션내에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="282e5-214">**목록 6 – web.config에 대 한 캐싱 섹션**</span><span class="sxs-lookup"><span data-stu-id="282e5-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="282e5-215">목록 7의 컨트롤러는 &lt;Cache1Hour 프로필을 OutputCache&gt; 특성을 사용하여 컨트롤러 작업에 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="282e5-216">**목록 7 – 컨트롤러\프로필Controller.vb**</span><span class="sxs-lookup"><span data-stu-id="282e5-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="282e5-217">목록 7의 컨트롤러가 노출한 Index() 작업을 호출하면 동일한 시간이 1시간 동안 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="282e5-218">요약</span><span class="sxs-lookup"><span data-stu-id="282e5-218">Summary</span></span>

<span data-ttu-id="282e5-219">출력 캐싱은 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시키는 매우 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="282e5-220">이 자습서에서는 OutputCache &lt;&gt; 특성을 사용하여 컨트롤러 작업의 출력을 캐시하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="282e5-221">또한 기간 및 VaryByParam 속성과 같은 &lt;OutputCache&gt; 특성의 속성을 수정하여 콘텐츠가 캐시되는 방법을 수정하는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="282e5-222">마지막으로 웹 구성 파일에서 캐시 프로필을 정의하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="282e5-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="282e5-223">[이전](understanding-action-filters-vb.md)
> [다음](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="282e5-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
