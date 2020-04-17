---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 캐시된 페이지(VB)에 동적 콘텐츠 추가 | 마이크로 소프트 문서
author: rick-anderson
description: 동일한 페이지에서 동적 및 캐시된 콘텐츠를 혼합하는 방법을 알아봅니다. 포스트 캐시 대체를 사용하면 배너 광고와 같은 동적 콘텐츠를 표시 할 수 있습니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542263"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a><span data-ttu-id="1a681-104">캐시된 페이지에 동적 콘텐츠 추가(VB)</span><span class="sxs-lookup"><span data-stu-id="1a681-104">Adding Dynamic Content to a Cached Page (VB)</span></span>

<span data-ttu-id="1a681-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1a681-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1a681-106">동일한 페이지에서 동적 및 캐시된 콘텐츠를 혼합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="1a681-107">캐시 후 대체를 사용하면 출력 캐시된 페이지 내에 배너 광고 또는 뉴스 항목과 같은 동적 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="1a681-108">출력 캐싱을 활용하면 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="1a681-109">페이지를 요청할 때마다 페이지를 다시 생성하는 대신 페이지를 한 번 생성하고 여러 사용자를 위해 메모리에 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="1a681-110">그러나 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-110">But there is a problem.</span></span> <span data-ttu-id="1a681-111">페이지에 동적 콘텐츠를 표시해야 하는 경우 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="1a681-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="1a681-112">예를 들어 페이지에 배너 광고를 표시한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="1a681-113">모든 사용자가 동일한 광고를 볼 수 있도록 배너 광고를 캐시하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="1a681-114">당신은 그런 식으로 돈을 벌수 없을 것입니다!</span><span class="sxs-lookup"><span data-stu-id="1a681-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="1a681-115">다행히도 쉬운 해결책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="1a681-116">*포스트 캐시 대체라는*ASP.NET 프레임워크의 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="1a681-117">캐시 후 대체를 사용하면 메모리에 캐시된 페이지에서 동적 콘텐츠를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="1a681-118">일반적으로 &lt;OutputCache&gt; 특성을 사용하여 페이지를 캐시할 때 페이지는 서버와 클라이언트(웹 브라우저)에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-118">Normally, when you output cache a page by using the &lt;OutputCache&gt; attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="1a681-119">사후 캐시 대체를 사용하면 페이지는 서버에서만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="1a681-120">사후 캐시 대체 사용</span><span class="sxs-lookup"><span data-stu-id="1a681-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="1a681-121">사후 캐시 대체를 사용하려면 두 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="1a681-122">먼저 캐시된 페이지에 표시할 동적 콘텐츠를 나타내는 문자열을 반환하는 메서드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="1a681-123">그런 다음 HttpResponse.WriteSubstitution() 메서드를 호출하여 동적 콘텐츠를 페이지에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="1a681-124">예를 들어 캐시된 페이지에 다른 뉴스 항목을 임의로 표시하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="1a681-125">목록 1의 클래스는 세 개의 뉴스 항목 목록에서 하나의 뉴스 항목을 임의로 반환하는 RenderNews()라는 단일 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="1a681-126">**목록 1 – 모델\뉴스.vb**</span><span class="sxs-lookup"><span data-stu-id="1a681-126">**Listing 1 – Models\News.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

<span data-ttu-id="1a681-127">사후 캐시 대체를 활용하려면 HttpResponse.WriteSubstitution() 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="1a681-128">WriteSubstitution() 메서드는 캐시된 페이지의 영역을 동적 콘텐츠로 대체하도록 코드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="1a681-129">WriteSubitution() 메서드는 목록 2의 보기에 임의의 뉴스 항목을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="1a681-130">**목록 2 – 보기\홈\인덱스.aspx**</span><span class="sxs-lookup"><span data-stu-id="1a681-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

<span data-ttu-id="1a681-131">RenderNews 메서드는 WriteSubitution() 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="1a681-132">RenderNews 메서드가 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-132">Notice that the RenderNews method is not called.</span></span> <span data-ttu-id="1a681-133">대신 메서드에 대 한 참조는 AddressOf 연산자의 도움으로 WriteSubitution()에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-133">Instead a reference to the method is passed to WriteSubstitution() with the help of the AddressOf operator.</span></span>

<span data-ttu-id="1a681-134">인덱스 보기가 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-134">The Index view is cached.</span></span> <span data-ttu-id="1a681-135">보기는 목록 3의 컨트롤러에 의해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="1a681-136">Index() 작업은 &lt;Index 보기를 60초&gt; 동안 캐시하도록 하는 OutputCache 특성으로 장식되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-136">Notice that the Index() action is decorated with an &lt;OutputCache&gt; attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="1a681-137">**목록 3 – 컨트롤러\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="1a681-137">**Listing 3 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

<span data-ttu-id="1a681-138">인덱스 보기가 캐시되어 있더라도 인덱스 페이지를 요청할 때 다른 임의의 뉴스 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="1a681-139">색인 페이지를 요청하면 페이지에 표시되는 시간이 60초 동안 변경되지 않습니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1a681-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="1a681-140">시간이 변경되지 않는다는 사실은 페이지가 캐시되었음을 증명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="1a681-141">그러나 WriteSubitution() 메서드에 의해 주입된 콘텐츠(임의의 뉴스 항목)는 각 요청에 따라 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="1a681-142">**그림 1 - 캐시된 페이지에 동적 뉴스 항목 주입**</span><span class="sxs-lookup"><span data-stu-id="1a681-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="1a681-144">도우미 메서드에서 사후 캐시 대체 사용</span><span class="sxs-lookup"><span data-stu-id="1a681-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="1a681-145">포스트 캐시 대체를 활용하는 더 쉬운 방법은 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드에 대한 호출을 캡슐화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="1a681-146">이 방법은 목록 4의 도우미 메서드에 의해 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="1a681-147">**목록 4 – 도우미\AdHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="1a681-147">**Listing 4 – Helpers\AdHelper.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

<span data-ttu-id="1a681-148">목록 4에는 렌더배너() 및 렌더배너내부()의 두 가지 방법을 노출하는 시각적 기본 모듈이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-148">Listing 4 contains a Visual Basic module that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="1a681-149">RenderBanner() 메서드는 실제 도우미 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="1a681-150">이 메서드는 표준 ASP.NET MVC HtmlHelper 클래스를 확장하여 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="1a681-151">렌더배너() 메서드는 렌더배너내부() 메서드를 WriteSubstitution() 메서드에 전달하는 HttpResponse.WriteSubstitution() 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="1a681-152">렌더배너내부() 메서드는 전용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="1a681-153">이 메서드는 도우미 메서드로 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="1a681-154">RenderBannerInternal() 메서드는 세 개의 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 임의로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="1a681-155">목록 5의 수정된 인덱스 보기는 RenderBanner() 도우미 메서드를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="1a681-156">MvcApplication1.helpers 네임스페이스를 가져오기 위해 뷰 상단에 추가 &lt;%@ 가져오기 %&gt; 지시문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="1a681-157">이 네임스페이스를 가져오지 않으면 RenderBanner() 메서드가 Html 속성에 메서드로 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="1a681-158">**목록 5 – 보기\홈\Index.aspx (렌더 배너() 방법)**</span><span class="sxs-lookup"><span data-stu-id="1a681-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

<span data-ttu-id="1a681-159">목록 5의 보기에 의해 렌더링된 페이지를 요청하면 각 요청과 함께 다른 배너 광고가 표시됩니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="1a681-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="1a681-160">페이지는 캐시되지만 배너 보급 알림은 RenderBanner() 도우미 메서드에 의해 동적으로 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="1a681-161">**그림 2 - 임의 배너 광고를 표시하는 인덱스 보기**</span><span class="sxs-lookup"><span data-stu-id="1a681-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="1a681-163">요약</span><span class="sxs-lookup"><span data-stu-id="1a681-163">Summary</span></span>

<span data-ttu-id="1a681-164">이 자습서에서는 캐시된 페이지에서 콘텐츠를 동적으로 업데이트하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="1a681-165">HttpResponse.WriteSubstitution() 메서드를 사용하여 캐시된 페이지에 동적 콘텐츠를 삽입할 수 있도록 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="1a681-166">HTML 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="1a681-167">가능하면 캐싱을 활용하여 웹 응용 프로그램의 성능에 극적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="1a681-168">이 자습서에서 설명한 대로 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 캐싱을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a681-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1a681-169">[이전](improving-performance-with-output-caching-vb.md)
> [다음](creating-a-controller-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1a681-169">[Previous](improving-performance-with-output-caching-vb.md)
[Next](creating-a-controller-vb.md)</span></span>
