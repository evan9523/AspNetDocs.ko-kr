---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 이해 (C#) | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서의 목표는 작업 필터를 설명하는 것입니다. 작업 필터는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542185"
---
# <a name="understanding-action-filters-c"></a><span data-ttu-id="4dbe2-104">작업 필터 이해(C#)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-104">Understanding Action Filters (C#)</span></span>

<span data-ttu-id="4dbe2-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4dbe2-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4dbe2-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="4dbe2-107">이 자습서의 목표는 작업 필터를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="4dbe2-108">작업 필터는 작업이 실행되는 방식을 수정하는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="4dbe2-109">작업 필터 이해</span><span class="sxs-lookup"><span data-stu-id="4dbe2-109">Understanding Action Filters</span></span>

<span data-ttu-id="4dbe2-110">이 자습서의 목표는 작업 필터를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="4dbe2-111">작업 필터는 작업이 실행되는 방식을 수정하는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="4dbe2-112">ASP.NET MVC 프레임워크에는 다음과 같은 몇 가지 작업 필터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="4dbe2-113">OutputCache - 이 작업 필터는 지정된 시간 동안 컨트롤러 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="4dbe2-114">HandleError - 이 작업 필터는 컨트롤러 작업이 실행될 때 발생하는 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="4dbe2-115">권한 부여 - 이 작업 필터를 사용하면 특정 사용자 또는 역할에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="4dbe2-116">사용자 지정 작업 필터를 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="4dbe2-117">예를 들어 사용자 지정 인증 시스템을 구현하기 위해 사용자 지정 작업 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="4dbe2-118">또는 컨트롤러 작업에서 반환되는 뷰 데이터를 수정하는 작업 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="4dbe2-119">이 자습서에서는 처음부터 작업 필터를 빌드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="4dbe2-120">작업 처리의 여러 단계를 Visual Studio 출력 창에 기록하는 로그 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="4dbe2-121">작업 필터 사용</span><span class="sxs-lookup"><span data-stu-id="4dbe2-121">Using an Action Filter</span></span>

<span data-ttu-id="4dbe2-122">작업 필터는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-122">An action filter is an attribute.</span></span> <span data-ttu-id="4dbe2-123">대부분의 작업 필터를 개별 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="4dbe2-124">예를 들어 목록 1의 데이터 컨트롤러는 `Index()` 현재 시간을 반환하는 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="4dbe2-125">이 작업은 `OutputCache` 작업 필터로 장식됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="4dbe2-126">이 필터를 사용하면 작업에서 반환되는 값이 10초 동안 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="4dbe2-127">**리스팅 1 –`Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="4dbe2-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="4dbe2-128">URL /Data/Index를 `Index()` 브라우저의 주소 표시줄에 입력하고 새로 고침 단추를 여러 번 누르면 10초 동안 동일한 시간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="4dbe2-129">`Index()` 작업의 출력은 10초 동안 캐시됩니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="4dbe2-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="4dbe2-130">[![캐시된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="4dbe2-131">**그림 01**: 캐시 된 시간[(전체 크기 이미지를 보려면 클릭)](understanding-action-filters-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>

<span data-ttu-id="4dbe2-132">목록 1에서 작업 필터인 `OutputCache` 단일 작업 필터가 `Index()` 메서드에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="4dbe2-133">필요한 경우 동일한 작업에 여러 작업 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="4dbe2-134">예를 들어 `OutputCache` 동일한 작업에 및 `HandleError` 작업 필터를 모두 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="4dbe2-135">목록 1에서 `OutputCache` 작업 필터가 `Index()` 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="4dbe2-136">이 특성을 `DataController` 클래스 자체에 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="4dbe2-137">이 경우 컨트롤러에서 노출된 모든 작업에서 반환되는 결과는 10초 동안 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="4dbe2-138">다양한 유형의 필터</span><span class="sxs-lookup"><span data-stu-id="4dbe2-138">The Different Types of Filters</span></span>

<span data-ttu-id="4dbe2-139">ASP.NET MVC 프레임워크는 다음과 같은 네 가지 유형의 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="4dbe2-140">권한 부여 필터 - `IAuthorizationFilter` 특성을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="4dbe2-141">작업 필터 - 특성을 `IActionFilter` 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="4dbe2-142">결과 필터 - 특성을 `IResultFilter` 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="4dbe2-143">예외 필터 - 특성을 `IExceptionFilter` 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="4dbe2-144">필터는 위에 나열된 순서대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="4dbe2-145">예를 들어 권한 부여 필터는 항상 작업 필터 앞에 실행되고 예외 필터는 다른 모든 유형의 필터 후에 항상 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="4dbe2-146">권한 부여 필터는 컨트롤러 작업에 대한 인증 및 권한 부여를 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="4dbe2-147">예를 들어 권한 부여 필터는 권한 부여 필터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="4dbe2-148">작업 필터에는 컨트롤러 작업이 실행되기 전과 후에 실행되는 논리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="4dbe2-149">예를 들어 작업 필터를 사용하여 컨트롤러 작업이 반환하는 뷰 데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="4dbe2-150">결과 필터에는 뷰 결과가 실행되기 전과 후에 실행되는 논리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="4dbe2-151">예를 들어 뷰가 브라우저에 렌더링되기 직전에 뷰 결과를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="4dbe2-152">예외 필터는 실행할 마지막 필터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="4dbe2-153">예외 필터를 사용하여 컨트롤러 작업 또는 컨트롤러 작업 결과에서 발생하는 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="4dbe2-154">예외 필터를 사용하여 오류를 기록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="4dbe2-155">각 필터 유형은 특정 순서로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="4dbe2-156">동일한 유형의 필터가 실행되는 순서를 제어하려면 필터의 Order 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="4dbe2-157">모든 작업 필터의 기본 클래스는 `System.Web.Mvc.FilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="4dbe2-158">`IAuthorizationFilter`특정 유형의 필터를 구현하려면 기본 Filter 클래스에서 상속되고 하나 이상의 을 `IActionFilter`구현하는 클래스를 `IResultFilter` `IExceptionFilter` 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="4dbe2-159">기본 작업필터특성 클래스</span><span class="sxs-lookup"><span data-stu-id="4dbe2-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="4dbe2-160">사용자 지정 작업 필터를 보다 쉽게 구현할 수 있도록 ASP.NET MVC 프레임워크에는 기본 `ActionFilterAttribute` 클래스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="4dbe2-161">이 클래스는 `IActionFilter` 클래스와 `IResultFilter` 인터페이스를 모두 구현하고 `Filter` 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="4dbe2-162">여기서 용어는 완전히 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="4dbe2-163">기술적으로 ActionFilterAttribute 클래스에서 상속하는 클래스는 작업 필터와 결과 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="4dbe2-164">그러나 느슨한 의미에서 단어 작업 필터는 ASP.NET MVC 프레임워크의 모든 유형의 필터를 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="4dbe2-165">기본 `ActionFilterAttribute` 클래스에는 재정의할 수 있는 다음 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="4dbe2-166">OnAction실행 - 컨트롤러 작업이 실행되기 전에 이 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="4dbe2-167">OnActionExecuted - 컨트롤러 작업이 실행된 후 이 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="4dbe2-168">OnResult 실행 - 컨트롤러 작업 결과가 실행되기 전에 이 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="4dbe2-169">OnResultExecuted - 컨트롤러 작업 결과가 실행된 후 이 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="4dbe2-170">다음 섹션에서는 이러한 각 다른 메서드를 구현하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="4dbe2-171">로그 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="4dbe2-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="4dbe2-172">사용자 지정 작업 필터를 빌드하는 방법을 설명하기 위해 컨트롤러 작업을 처리하는 단계를 Visual Studio 출력 창에 기록하는 사용자 지정 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="4dbe2-173">우리는 `LogActionFilter` 리스팅 2에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="4dbe2-174">**리스팅 2 –`ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="4dbe2-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="4dbe2-175">목록 2에서 `OnActionExecuting()`에서 `OnActionExecuted()` `OnResultExecuting()`" `OnResultExecuted()` 및 메서드는 `Log()` 모두 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="4dbe2-176">메서드의 이름과 현재 경로 데이터가 `Log()` 메서드에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="4dbe2-177">메서드는 `Log()` Visual Studio 출력 창에 메시지를 씁니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="4dbe2-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="4dbe2-178">[![비주얼 스튜디오 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="4dbe2-179">**그림 02**: 비주얼 스튜디오 출력 창에 쓰기[(전체 크기 이미지를 보려면 클릭)](understanding-action-filters-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>

<span data-ttu-id="4dbe2-180">목록 3의 홈 컨트롤러는 전체 컨트롤러 클래스에 로그 작업 필터를 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="4dbe2-181">홈 컨트롤러에서 노출되는 작업이 호출될 때마다 `Index()` 메서드 또는 `About()` 메서드 - 작업 처리 단계는 Visual Studio 출력 창에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="4dbe2-182">**리스팅 3 –`Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="4dbe2-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="4dbe2-183">요약</span><span class="sxs-lookup"><span data-stu-id="4dbe2-183">Summary</span></span>

<span data-ttu-id="4dbe2-184">이 자습서에서는 MVC 작업 필터를 ASP.NET 소개했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="4dbe2-185">권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터의 네 가지 유형의 필터에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="4dbe2-186">기본 `ActionFilterAttribute` 클래스에 대해서도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="4dbe2-187">마지막으로 간단한 작업 필터를 구현하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="4dbe2-188">컨트롤러 작업을 처리하는 단계를 Visual Studio 출력 창에 기록하는 로그 작업 필터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4dbe2-189">[이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
