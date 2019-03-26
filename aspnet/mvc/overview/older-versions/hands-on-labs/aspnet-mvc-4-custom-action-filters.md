---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC는 작업 메서드가 호출 되기 전후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: 4c8628cc289610e287c0a3bc3c8a4c7a833c9fde
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423418"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="4074e-104">ASP.NET MVC 4 사용자 지정 작업 필터</span><span class="sxs-lookup"><span data-stu-id="4074e-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="4074e-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="4074e-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4074e-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="4074e-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4074e-107">ASP.NET MVC는 작업 메서드가 호출 되기 전후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="4074e-108">작업 필터는 컨트롤러의 작업 메서드에 사전 작업 및 작업 이후의 동작을 추가 하는 선언적 방법을 제공 하는 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="4074e-109">이 실습 랩에서 MvcMusicStore 컨트롤러의 요청을 catch 하 고 솔루션을 데이터베이스 테이블에는 사이트의 활동 로그에 사용자 지정 작업 필터 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="4074e-110">모든 컨트롤러 또는 동작을 주입 하 여 로깅 필터를 추가 하려면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="4074e-111">마지막으로, 방문자 목록을 보여 주는 로그 보기를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="4074e-112">이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="4074e-113">사용 하지 않은 경우 **ASP.NET MVC** 이전 좋습니다 이동해 **ASP.NET MVC 4 기본 사항** 실습 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="4074e-114">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4074e-115">이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 사용자 지정 작업 필터](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="4074e-116">목표</span><span class="sxs-lookup"><span data-stu-id="4074e-116">Objectives</span></span>

<span data-ttu-id="4074e-117">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="4074e-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="4074e-118">필터링 기능을 확장 하는 사용자 지정 작업 필터 특성 만들기</span><span class="sxs-lookup"><span data-stu-id="4074e-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="4074e-119">특정 수준에 주입 하 여 사용자 지정 필터 특성 적용</span><span class="sxs-lookup"><span data-stu-id="4074e-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="4074e-120">사용자 지정 작업 필터를 전역으로 등록</span><span class="sxs-lookup"><span data-stu-id="4074e-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4074e-121">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4074e-121">Prerequisites</span></span>

<span data-ttu-id="4074e-122">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4074e-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="4074e-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4074e-124">설정</span><span class="sxs-lookup"><span data-stu-id="4074e-124">Setup</span></span>

<span data-ttu-id="4074e-125">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="4074e-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="4074e-126">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4074e-127">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4074e-128">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c: 코드 조각을 사용 하 여](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4074e-129">연습</span><span class="sxs-lookup"><span data-stu-id="4074e-129">Exercises</span></span>

<span data-ttu-id="4074e-130">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="4074e-131">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="4074e-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="4074e-132">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="4074e-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="4074e-133">이 랩을 완료 하는 시간을 예상 합니다. **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="4074e-134">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4074e-135">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="4074e-136">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="4074e-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="4074e-137">이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="4074e-138">해당 목적을 위해 선택한 컨트롤러의 모든 활동을 기록 하는 MusicStore 사이트로 로깅 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="4074e-139">필터를 확장 합니다 **ActionFilterAttributeClass** 시키고 **OnActionExecuting** 메서드를 각 요청을 catch 하 고 다음 로깅 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="4074e-140">HTTP 요청에 대 한 컨텍스트 정보를 실행 하는 메서드, 결과 및 매개 변수에서 제공 합니다 ASP.NET MVC **ActionExecutingContext** 클래스 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="4074e-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="4074e-141">ASP.NET MVC 4 기본 필터 공급자는 사용자 지정 필터를 만들지 않고도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="4074e-142">ASP.NET MVC 4는 다음과 같은 유형의 필터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="4074e-143">**권한 부여** 그러면 인증 수행 또는 요청의 속성 유효성 검사 등의 작업 메서드를 실행할 것인지에 대 한 보안 결정을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="4074e-144">**작업** 작업 메서드 실행을 래핑하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="4074e-145">이 필터는 작업 메서드에 추가 데이터를 제공, 반환 값 검사 또는 작업 메서드 실행을 취소 하는 등의 추가적인 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="4074e-146">**결과** ActionResult 개체의 실행을 래핑하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="4074e-147">이 필터는 결과 HTTP 응답을 수정 하는 등의 추가 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="4074e-148">**예외** 어딘가에 메서드에서 예외를 throw 작업, 권한 부여 필터를 사용 하 여 시작 하 고 결과의 실행을 사용 하 여 종료 처리 되지 않은 예외가 발생 하는 경우를 실행 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="4074e-149">예외 필터는 로깅 또는 오류 페이지 표시 등의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="4074e-150">필터 공급자에 대 한 자세한 내용은이 MSDN 링크를 참조 하세요. ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4074e-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="4074e-151">MVC Music Store 응용 프로그램 로깅 기능에 대 한</span><span class="sxs-lookup"><span data-stu-id="4074e-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="4074e-152">이 Music Store 솔루션에 사이트 로깅에 대 한 새 데이터 모델 테이블이 **ActionLog**, 다음 필드를 사용 하 여: 요청, 호출 동작, 클라이언트 IP 및 타임 스탬프를 수신 하는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="4074e-153">![데이터 모델입니다. ActionLog 테이블입니다. ](aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델입니다. ActionLog 테이블입니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="4074e-154">*데이터 모델-ActionLog 테이블*</span><span class="sxs-lookup"><span data-stu-id="4074e-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="4074e-155">솔루션에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 **MvcMusicStores/보기/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="4074e-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="4074e-156">![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="4074e-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="4074e-157">*작업 로그 보기*</span><span class="sxs-lookup"><span data-stu-id="4074e-157">*Action Log view*</span></span>

<span data-ttu-id="4074e-158">이 구조를 사용 하 여 모든 작업 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행에 집중 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="4074e-159">작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="4074e-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="4074e-160">이 태스크에서 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="4074e-161">ASP.NET MVC를 확장 하면 해당 용도로 **ActionFilterAttribute** 클래스 및 인터페이스를 구현 하 **IActionFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="4074e-162">합니다 **ActionFilterAttribute** 모든 특성 필터에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="4074e-163">컨트롤러 작업의 실행 전과 후에 특정 논리를 실행 하려면 다음 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="4074e-164">**OnActionExecuting**(ActionExecutingContext filterContext): 메서드는 작업 바로 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="4074e-165">**OnActionExecuted**(ActionExecutedContext filterContext): 동작 메서드가 호출 된 후 및 하기 전에 결과 (이전 보기 렌더링) 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="4074e-166">**OnResultExecuting**(ResultExecutingContext filterContext): 결과 직전 (이전 보기 렌더링) 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="4074e-167">**OnResultExecuted**(ResultExecutedContext filterContext): (뷰를 렌더링할) 후 결과 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="4074e-168">이러한 방법 중 하나를 파생 클래스로 재정의 함으로써 필터링 사용자 고유의 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>


1. <span data-ttu-id="4074e-169">엽니다는 **시작할** 솔루션에 있는 **\Source\Ex01-LoggingActions\Begin** 폴더.</span><span class="sxs-lookup"><span data-stu-id="4074e-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="4074e-170">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="4074e-171">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4074e-172">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4074e-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4074e-173">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4074e-174">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4074e-175">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4074e-176">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4074e-177">자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4074e-178">에 새 C# 클래스를 추가 합니다 **필터** 폴더 하 고 이름을 *CustomActionFilter.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="4074e-179">이 폴더는 모든 사용자 지정 필터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="4074e-180">오픈 **CustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 하 고 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4074e-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="4074e-181">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="4074e-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="4074e-182">상속 된 **CustomActionFilter** 에서 클래스 **ActionFilterAttribute** 한 다음 **CustomActionFilter** 클래스 구현 **IActionFilter** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="4074e-183">확인 **CustomActionFilter** 메서드를 재정의 하는 클래스 **OnActionExecuting** 필터의 실행을 기록 하는 데 필요한 논리가 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="4074e-184">이렇게 하려면 다음 강조 표시 된 코드를 추가 **CustomActionFilter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="4074e-185">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="4074e-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="4074e-186">**OnActionExecuting** 메서드를 사용 하 여 **Entity Framework** 새 ActionLog 레지스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="4074e-187">만들고 새 엔터티 인스턴스 컨텍스트 정보로 채웁니다 **filterContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="4074e-188">에 대 한 자세한 내용은 **ControllerContext** 에서 클래스 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="4074e-189">작업 2-코드 인터셉터 저장소 컨트롤러 클래스에 삽입</span><span class="sxs-lookup"><span data-stu-id="4074e-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="4074e-190">이 작업에서 모든 컨트롤러 클래스 및 기록 될 컨트롤러 작업에 삽입 하 여 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="4074e-191">이 연습에서는 저장소 컨트롤러 클래스에 로그를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="4074e-192">메서드 **OnActionExecuting** 에서 **ActionLogFilterAttribute** 삽입 된 요소를 호출할 때 사용자 지정 필터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="4074e-193">특정 컨트롤러 메서드를 가로챌 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="4074e-194">열기는 **StoreController** 에 **MvcMusicStore\Controllers** 에 대 한 참조를 추가 합니다 **필터** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4074e-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="4074e-195">사용자 지정 필터를 삽입할 **CustomActionFilter** 로 **StoreController** 클래스를 추가 하 여 **[CustomActionFilter]** 특성 클래스 선언 전 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="4074e-196">필터는 컨트롤러 클래스에 주입 됩니다을 하는 경우 모든 작업 삽입도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="4074e-197">일련의 작업에 대해서만 필터를 적용 하려는 있다면 삽입할 **[CustomActionFilter]** 중 각각에:</span><span class="sxs-lookup"><span data-stu-id="4074e-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4074e-198">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4074e-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="4074e-199">이 태스크에서는 로깅 필터 작동 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="4074e-200">응용 프로그램을 시작 되며 스토어 방문 및 로그인된 활동 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="4074e-201">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4074e-202">이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 보려면:</span><span class="sxs-lookup"><span data-stu-id="4074e-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="4074e-203">![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image3.png "페이지 작업 전에 추적 상태를 기록 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4074e-204">*페이지 작업 하기 전에 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="4074e-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="4074e-205">기본적으로 메뉴에 대 한 기존 장르를 검색 하는 경우 생성 되는 하나의 항목이 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="4074e-206">간단히 하기 위해 정리 될 예정 된 **ActionLog** 각 특정 작업의 확인의 로그만 표시 됩니다 있도록 응용 프로그램이 실행 될 때마다 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="4074e-207">다음 코드를 제거 해야 하는 **세션\_시작** 메서드 (에 **Global.asax** 클래스) 저장소 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하기 위해 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="4074e-208">중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="4074e-209">이동할 **/ActionLog** 경우 로그 빈 키를 눌러 **F5** 페이지를 새로 고칠 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="4074e-210">에 방문 추적 된를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="4074e-211">![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "활동 로그를 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4074e-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4074e-212">*활동 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4074e-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="4074e-213">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="4074e-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="4074e-214">이 연습에서 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 필터 둘 모두를 실행할 수 있는 특정 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="4074e-215">그런 다음 필터를 전역으로 등록 하는 코드를 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="4074e-216">필터 실행 순서를 정의할 때 고려해 야 할 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="4074e-217">예를 들어 주문 속성 및 필터 범위:</span><span class="sxs-lookup"><span data-stu-id="4074e-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="4074e-218">정의할 수 있습니다는 **범위** 각 필터에 대 한 예를 들어, 있습니다 수 범위 내에서 실행 하는 모든 작업 필터는 **컨트롤러 범위**, 및에서 실행 하려면 모든 권한 부여 필터 **전역 범위** .</span><span class="sxs-lookup"><span data-stu-id="4074e-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="4074e-219">범위 정의 된 실행 순서는 경우</span><span class="sxs-lookup"><span data-stu-id="4074e-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="4074e-220">또한 각 작업 필터에는 실행 순서는 필터의 범위를 결정 하는 데 사용 되는 순서 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="4074e-221">사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은이 MSDN 문서를 참조 하세요. ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span><span class="sxs-lookup"><span data-stu-id="4074e-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="4074e-222">작업 1: 새 사용자 지정 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="4074e-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="4074e-223">이 태스크에서는 만들려는 StoreController 클래스에 삽입 하려면 새 사용자 지정 작업 필터를 필터의 실행 순서를 관리 하는 방법을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="4074e-224">엽니다는 **시작할** 솔루션에 있는 **\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더.</span><span class="sxs-lookup"><span data-stu-id="4074e-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="4074e-225">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="4074e-226">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4074e-227">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="4074e-228">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4074e-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="4074e-229">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4074e-230">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4074e-231">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4074e-232">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="4074e-233">자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4074e-234">에 새 C# 클래스를 추가 합니다 **필터** 폴더 이름을 *MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="4074e-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="4074e-235">오픈 **MyNewCustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 하며 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4074e-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="4074e-236">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="4074e-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="4074e-237">기본 클래스 선언을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="4074e-238">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="4074e-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="4074e-239">이 사용자 지정 작업 필터는 이전 연습에서 만든 것 보다 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="4074e-240">주요 차이점은 있는지 합니다 *&quot;다른 이름으로 기록&quot;* 필터 등록 로그를 식별 하는이 새 클래스의이 이름을 사용 하 여 업데이트 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="4074e-241">작업 2: 새 코드 인터셉터를 StoreController 클래스에 삽입</span><span class="sxs-lookup"><span data-stu-id="4074e-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="4074e-242">이 태스크에서는 StoreController 클래스에 새 사용자 지정 필터를 추가 하 고 필터 둘 모두 어떻게 함께 작동을 확인 하려면 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="4074e-243">엽니다는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 하 고 새 사용자 지정 필터 삽입 **MyNewCustomActionFilter** 에  **StoreController** 과 같은 클래스는 다음 코드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="4074e-244">이제 이러한 두 사용자 지정 작업 필터의 작동 방식을 확인 하기 위해 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="4074e-245">이 작업을 수행 하려면 키를 누릅니다 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="4074e-246">이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="4074e-247">![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image5.png "페이지 작업 전에 추적 상태를 기록 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4074e-248">*페이지 작업 하기 전에 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="4074e-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="4074e-249">중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="4074e-250">이 시간 확인 에 방문 두 번 추적 된:에 추가한 각 사용자 지정 작업 필터에 대 한 합니다 **StorageController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="4074e-251">![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "활동 로그를 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4074e-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4074e-252">*활동 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4074e-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="4074e-253">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="4074e-254">작업 3: 필터 순서 관리</span><span class="sxs-lookup"><span data-stu-id="4074e-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="4074e-255">이 작업 순서 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="4074e-256">열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 지정 합니다 **순서** 속성 필터 둘 모두에 같은 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="4074e-257">이제 필터의 순서 속성의 값에 따라 실행 되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="4074e-258">필터의 가장 작은 값을 사용 하 여 볼 수 있습니다 (**CustomActionFilter**)이 실행 되는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="4074e-259">키를 눌러 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="4074e-260">이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="4074e-261">![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image7.png "페이지 작업 전에 추적 상태를 기록 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4074e-262">*페이지 작업 하기 전에 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="4074e-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="4074e-263">중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="4074e-264">이 이번에 따라 방문 된 추적 되는 필터의 순서 값으로 정렬 된 것을 확인 합니다. **CustomActionFilter** 로그의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="4074e-265">![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "활동 로그를 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4074e-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4074e-266">*활동 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4074e-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="4074e-267">이제 필터의 순서 값을 업데이트 한 로깅 순서가 변경 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="4074e-268">에 **StoreController** 클래스, 아래와 같은 필터의 순서 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="4074e-269">키를 눌러 응용 프로그램을 다시 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="4074e-270">중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="4074e-271">이 이번에는 로그 여 만들어졌는지 확인 **MyNewCustomActionFilter** 필터 첫 번째로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="4074e-272">![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "활동 로그를 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4074e-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4074e-273">*활동 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4074e-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="4074e-274">작업 4: 전역 필터 등록</span><span class="sxs-lookup"><span data-stu-id="4074e-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="4074e-275">이 태스크에서는 새 필터를 등록 하는 솔루션 업데이트 됩니다 (**MyNewCustomActionFilter**) 글로벌 필터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="4074e-276">이 작업을 수행 하 여 이전 태스크와 같이 StoreController 것 뿐만 아니라 응용 프로그램에서 실행 되는 모든 작업으로 트리거할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="4074e-277">**StoreController** 클래스를 제거할 **[MyNewCustomActionFilter]** 특성과 order 속성에서 **[CustomActionFilter]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="4074e-278">이 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="4074e-279">오픈 **Global.asax** 찾아서 파일을 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="4074e-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="4074e-280">때마다 응용 프로그램 시작 알림 전역 필터를 등록 하는 호출 하 여 **RegisterGlobalFilters** 내에서 메서드 **FilterConfig** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="4074e-281">![Global.asax의 전역 필터 등록](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global.asax의 전역 필터 등록")</span><span class="sxs-lookup"><span data-stu-id="4074e-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="4074e-282">*Global.asax의 전역 필터 등록*</span><span class="sxs-lookup"><span data-stu-id="4074e-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="4074e-283">오픈 **등록 합니다** 내에 파일이 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="4074e-284">System.Web.Mvc;를 사용 하 여에 대 한 참조를 추가 합니다. MvcMusicStore.Filters;를 사용 하 여 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="4074e-285">업데이트 **RegisterGlobalFilters** 메서드를 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="4074e-286">이렇게 하려면 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="4074e-287">**F5**를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="4074e-288">중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="4074e-289">이제 확인 **[MyNewCustomActionFilter]** 너무 HomeController ActionLogController에 삽입 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="4074e-290">![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "활동 로그를 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4074e-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4074e-291">*전역 작업 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4074e-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="4074e-292">또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 [부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4074e-293">요약</span><span class="sxs-lookup"><span data-stu-id="4074e-293">Summary</span></span>

<span data-ttu-id="4074e-294">이 실습을 완료 하 여 사용자 지정 작업을 실행 하는 작업 필터를 확장 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="4074e-295">또한 페이지 컨트롤러에 필터를 주입 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="4074e-296">다음 개념 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-296">The following concepts were used:</span></span>

- <span data-ttu-id="4074e-297">ASP.NET MVC ActionFilterAttribute 클래스를 사용 하 여 사용자 지정 작업 필터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4074e-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="4074e-298">ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4074e-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="4074e-299">필터 순서 속성을 사용 하 여 순서를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4074e-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="4074e-300">필터를 전역으로 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4074e-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4074e-301">부록 a: Express 2012 for Web Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="4074e-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4074e-302">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4074e-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4074e-303">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4074e-304">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4074e-305">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4074e-306">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-306">Click on **Install Now**.</span></span> <span data-ttu-id="4074e-307">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4074e-308">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4074e-309">![Visual Studio Express를 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4074e-310">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4074e-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4074e-311">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="4074e-313">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="4074e-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4074e-314">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-314">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="4074e-316">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="4074e-316">*Installation progress*</span></span>
6. <span data-ttu-id="4074e-317">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-317">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="4074e-319">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="4074e-319">*Installation completed*</span></span>
7. <span data-ttu-id="4074e-320">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4074e-321">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="4074e-323">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="4074e-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4074e-324">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="4074e-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="4074e-325">이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="4074e-326">작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4074e-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="4074e-327">로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4074e-328">Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="4074e-329">등록할 수 있습니다 [여기](https://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="4074e-330">![Windows Azure 포털에 로그온](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure 포털에 로그온")</span><span class="sxs-lookup"><span data-stu-id="4074e-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="4074e-331">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="4074e-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="4074e-332">클릭 **새로 만들기** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="4074e-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="4074e-333">![새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="4074e-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="4074e-334">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="4074e-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="4074e-335">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="4074e-336">선택한 **빨리 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="4074e-337">새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4074e-338">Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트.</span><span class="sxs-lookup"><span data-stu-id="4074e-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="4074e-339">빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="4074e-340">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="4074e-341">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="4074e-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="4074e-342">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="4074e-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="4074e-343">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="4074e-344">웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="4074e-345">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="4074e-346">![새 웹 사이트를 찾아](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4074e-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="4074e-347">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="4074e-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="4074e-348">![실행 중인 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image21.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="4074e-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="4074e-349">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="4074e-349">*Web site running*</span></span>
6. <span data-ttu-id="4074e-350">포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="4074e-351">![웹 사이트 관리 페이지를 열어](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="4074e-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="4074e-352">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="4074e-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="4074e-353">**대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="4074e-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4074e-354">합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="4074e-355">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="4074e-356">**Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="4074e-357">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image23.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="4074e-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="4074e-358">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="4074e-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="4074e-359">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="4074e-360">추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="4074e-361">![게시 프로필 파일을 저장](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="4074e-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="4074e-362">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="4074e-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="4074e-363">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="4074e-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="4074e-364">응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="4074e-365">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="4074e-366">응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="4074e-367">Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="4074e-368">만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="4074e-369">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="4074e-370">만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="4074e-371">![SQL Database 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="4074e-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="4074e-372">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="4074e-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="4074e-373">다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="4074e-374">이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="4074e-376">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="4074e-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="4074e-377">한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="4074e-379">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="4074e-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4074e-380">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="4074e-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="4074e-381">ASP.NET MVC 4 솔루션 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="4074e-382">에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="4074e-383">![응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="4074e-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="4074e-384">*웹 사이트를 게시합니다.*</span><span class="sxs-lookup"><span data-stu-id="4074e-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="4074e-385">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="4074e-386">![게시 프로필 가져오기](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="4074e-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="4074e-387">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="4074e-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="4074e-388">클릭 **연결의 유효성을 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-388">Click **Validate Connection**.</span></span> <span data-ttu-id="4074e-389">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4074e-390">연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="4074e-391">![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="4074e-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="4074e-392">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="4074e-392">*Validating connection*</span></span>
4. <span data-ttu-id="4074e-393">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="4074e-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="4074e-394">![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="4074e-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="4074e-395">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="4074e-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="4074e-396">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="4074e-397">에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="4074e-398">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="4074e-399">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="4074e-400">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-400">Type a new database name.</span></span>

     <span data-ttu-id="4074e-401">![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="4074e-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="4074e-402">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="4074e-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="4074e-403">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-403">Then click **OK**.</span></span> <span data-ttu-id="4074e-404">데이터베이스를 만들라는 메시지가 나오면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="4074e-405">![데이터베이스를 만드는](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="4074e-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="4074e-406">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="4074e-406">*Creating the database*</span></span>
7. <span data-ttu-id="4074e-407">기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="4074e-408">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-408">Then click **Next**.</span></span>

    <span data-ttu-id="4074e-409">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="4074e-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="4074e-410">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="4074e-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="4074e-411">에 **미리 보기** 페이지에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="4074e-412">![웹 응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="4074e-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="4074e-413">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="4074e-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="4074e-414">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="4074e-415">부록 c: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="4074e-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="4074e-416">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4074e-417">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4074e-418">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-custom-action-filters/_static/image37.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="4074e-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4074e-419">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="4074e-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4074e-420">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="4074e-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4074e-421">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4074e-422">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4074e-423">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4074e-424">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="4074e-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4074e-425">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4074e-426">![코드 조각 이름을 입력](aspnet-mvc-4-custom-action-filters/_static/image38.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="4074e-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4074e-427">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="4074e-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="4074e-428">![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="4074e-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4074e-429">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="4074e-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4074e-430">![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-custom-action-filters/_static/image40.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="4074e-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4074e-431">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="4074e-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4074e-432">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4074e-433">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4074e-434">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4074e-435">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4074e-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4074e-436">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="4074e-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4074e-437">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="4074e-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4074e-438">![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-custom-action-filters/_static/image42.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="4074e-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4074e-439">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="4074e-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
