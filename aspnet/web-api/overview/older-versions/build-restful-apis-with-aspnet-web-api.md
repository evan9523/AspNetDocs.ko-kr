---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API-ASP.NET 사용 하 여 RESTful Api 빌드 4.x
author: rick-anderson
description: '실습: 웹 API를 사용 하 여 asp.net에서 4.x를 연락처 관리자 응용 프로그램에 대 한 간단한 REST API를 빌드하 합니다.'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3ba7f2d186e6f0837a32f69f964cec19fe625953
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59391483"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="519e7-103">ASP.NET Web API 사용 하 여 RESTful Api 빌드</span><span class="sxs-lookup"><span data-stu-id="519e7-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="519e7-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="519e7-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="519e7-105">실습: 웹 API를 사용 하 여 asp.net에서 4.x를 연락처 관리자 응용 프로그램에 대 한 간단한 REST API를 빌드하 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="519e7-106">또한 API를 사용 하려면 클라이언트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="519e7-107">최근 몇 년 동안에서 HTTP HTML 페이지를 제공 하는 동안만 아님을 지우기 되었습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="519e7-108">와 같은 몇 가지 간단한 개념 및 몇 가지 동사 (GET, POST 등)을 사용 하는 웹 Api를 빌드하기 위한 강력한 플랫폼 이기도 *Uri* 하 고 *헤더*합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="519e7-109">ASP.NET Web API는 HTTP 프로그래밍을 단순화 하는 구성 요소 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="519e7-110">ASP.NET MVC 런타임은 기반 하기 때문에 Web API http 전송 하위 수준 세부 정보를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="519e7-111">동시에, Web API는 자연스럽 게 HTTP 프로그래밍 모델을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="519e7-112">사실, Web API의 한 가지 목표를 *되지* 실제로 http를 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="519e7-113">결과적으로, 웹 API는 유연 하 고 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="519e7-114">REST 아키텍처 스타일은 아니지만 분명 HTTP에 대 한 올바른 접근 방법 HTTP-활용할 수 있는 효과적인 방법을 것으로 입증 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="519e7-115">대화 상대 관리자는 나열, 추가 및 다른 연락처를 제거 하기 위한 RESTful를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="519e7-116">이 랩에서 HTTP REST에 대 한 기본적인 지식이 필요 하 고 HTML, JavaScript 및 jQuery의 기본 작동 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="519e7-117">ASP.NET 웹 사이트에서 ASP.NET Web API 프레임 워크에 전용 영역이 [ https://asp.net/web-api ](https://asp.net/web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="519e7-118">이 사이트는 계속 최신 정보, 샘플 및 웹 API와 관련 된 뉴스 따라서 확인 자주 제공 거의 모든 장치 또는 개발 프레임 워크를 사용할 수 있는 사용자 지정 Web Api를 만드는 아트를 철저히 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="519e7-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="519e7-119">ASP.NET Web API, ASP.NET MVC 4 비슷합니다에 사용할 수 있는 종속성 주입 프레임 워크의 몇 가지 매우 쉽게 사용할 수 있도록 컨트롤러에서 서비스 계층을 구분 하는 측면에서 유연</span><span class="sxs-lookup"><span data-stu-id="519e7-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="519e7-120">Msdn에서 다운로드할 수 있는 ASP.NET Web API 프로젝트에서 종속성 주입을 위한 Ninject를 사용 하는 방법을 보여 주는 좋은 샘플 있기 [여기](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="519e7-121">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="519e7-122">목표</span><span class="sxs-lookup"><span data-stu-id="519e7-122">Objectives</span></span>

<span data-ttu-id="519e7-123">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="519e7-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="519e7-124">RESTful 웹 API를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="519e7-125">HTML 클라이언트에서 API 호출</span><span class="sxs-lookup"><span data-stu-id="519e7-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="519e7-126">전제 조건</span><span class="sxs-lookup"><span data-stu-id="519e7-126">Prerequisites</span></span>

<span data-ttu-id="519e7-127">다음는이 실습을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="519e7-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 B](#AppendixB) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="519e7-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="519e7-129">설정</span><span class="sxs-lookup"><span data-stu-id="519e7-129">Setup</span></span>

<span data-ttu-id="519e7-130">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="519e7-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="519e7-131">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="519e7-132">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="519e7-133">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 a: 코드 조각을 사용 하 여](#AppendixA)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="519e7-134">연습</span><span class="sxs-lookup"><span data-stu-id="519e7-134">Exercises</span></span>

<span data-ttu-id="519e7-135">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="519e7-136">연습 1: 읽기 전용으로 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="519e7-137">연습 2: 읽기/쓰기 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="519e7-138">연습 3: HTML 클라이언트에서 Web API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="519e7-139">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="519e7-140">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="519e7-141">이 랩을 완료 하는 시간을 예상 합니다. **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="519e7-142">연습 1: 읽기 전용으로 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="519e7-143">이 연습에서는 연락처 관리자에 대 한 읽기 전용으로 GET 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="519e7-144">작업 1-API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="519e7-145">이 태스크에서는 새 ASP.NET 웹 프로젝트 템플릿은 웹 API 웹 응용 프로그램을 만들려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="519e7-146">실행할 **Visual Studio 2012 Express for Web**,이 이동 작업을 수행 하 **시작** 유형과 **VS Express for Web** 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="519e7-147">**파일** 메뉴에서 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="519e7-148">선택 된 **Visual C# | 웹** 프로젝트 형식을 프로젝트 유형 트리 보기에서 다음을 선택 합니다 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식.</span><span class="sxs-lookup"><span data-stu-id="519e7-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="519e7-149">프로젝트의 설정 **이름** 하 *ContactManager* 및 **솔루션 이름** 에 *시작*를 클릭 **확인**.</span><span class="sxs-lookup"><span data-stu-id="519e7-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="519e7-150">![새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기](build-restful-apis-with-aspnet-web-api/_static/image1.png "새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="519e7-151">*새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="519e7-152">ASP.NET MVC 4 프로젝트 형식 대화 상자에서 선택 합니다 **Web API** 형식 프로젝션 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="519e7-153">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-153">Click **OK**.</span></span>

    <span data-ttu-id="519e7-154">![Web API 프로젝트 형식 지정](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API 프로젝트 형식 지정")</span><span class="sxs-lookup"><span data-stu-id="519e7-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="519e7-155">*Web API 프로젝트 형식 지정*</span><span class="sxs-lookup"><span data-stu-id="519e7-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="519e7-156">작업 2-연락처 관리자 API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="519e7-157">이 태스크에서는 API 메서드 상주할 컨트롤러 클래스를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="519e7-158">라는 파일을 삭제 **ValuesController.cs** 내 **컨트롤러** 프로젝트에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="519e7-159">마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에서 프로젝트를 마우스 **추가 | 컨트롤러** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="519e7-160">![프로젝트에 새 컨트롤러를 추가](build-restful-apis-with-aspnet-web-api/_static/image3.png "프로젝트에 새 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="519e7-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="519e7-161">*프로젝트에 새 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="519e7-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="519e7-162">에 **컨트롤러 추가** 대화 상자가 나타나면 선택 **빈 API 컨트롤러** 템플릿 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="519e7-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="519e7-163">컨트롤러 클래스의 이름을 **contact ¡© Controller**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="519e7-164">클릭 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="519e7-164">Then, click **Add.**</span></span>

    <span data-ttu-id="519e7-165">![컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면](build-restful-apis-with-aspnet-web-api/_static/image4.png "컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면")</span><span class="sxs-lookup"><span data-stu-id="519e7-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="519e7-166">*컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면*</span><span class="sxs-lookup"><span data-stu-id="519e7-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="519e7-167">다음 코드를 추가 합니다 **contact ¡© Controller**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="519e7-168">(코드 조각- *웹 API 랩-Ex01-Get API 메서드*)</span><span class="sxs-lookup"><span data-stu-id="519e7-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="519e7-169">키를 눌러 **F5** 응용 프로그램을 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="519e7-170">Web API 프로젝트에 대 한 기본 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="519e7-171">![ASP.NET Web API 응용 프로그램의 기본 홈페이지](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 응용 프로그램의 기본 홈 페이지")</span><span class="sxs-lookup"><span data-stu-id="519e7-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="519e7-172">*ASP.NET Web API 응용 프로그램의 기본 홈 페이지*</span><span class="sxs-lookup"><span data-stu-id="519e7-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="519e7-173">키를 눌러 Internet Explorer 창에서 합니다 **F12** 키를 합니다 **개발자 도구** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="519e7-174">클릭는 **네트워크** 탭을 클릭 합니다 **캡처 시작** 단추 창에 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="519e7-175">![네트워크 탭을 열고 시작 네트워크 캡처](build-restful-apis-with-aspnet-web-api/_static/image6.png "네트워크 탭을 열고 시작 네트워크 캡처")</span><span class="sxs-lookup"><span data-stu-id="519e7-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="519e7-176">*네트워크 탭을 열고 네트워크 캡처를 시작 합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="519e7-177">사용 하 여 브라우저의 주소 표시줄에서 URL을 추가 **/api/contact** 및 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="519e7-178">전송 정보를 네트워크 캡처 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="519e7-179">응답의 MIME 형식이 보면 **application/json**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="519e7-180">이 방법의 기본 출력 형식은 JSON 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="519e7-181">![네트워크 보기에서 Web API 요청의 출력을 보는](build-restful-apis-with-aspnet-web-api/_static/image7.png "네트워크 보기에서 Web API 요청 결과 보기")</span><span class="sxs-lookup"><span data-stu-id="519e7-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="519e7-182">*네트워크 보기에서 Web API 요청 결과 보기*</span><span class="sxs-lookup"><span data-stu-id="519e7-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-183">이 시점에서 Internet Explorer 10의 기본 동작을 저장 하거나 웹 API 호출에서 결과 스트림을 열지 사용자가 원하는 경우 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="519e7-184">출력에는 Web API URL 호출의 JSON 결과 포함 하는 텍스트 파일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="519e7-185">개발자 도구 창을 통해 응답의 콘텐츠를 볼 수 있도록 대화 상자를 취소 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="519e7-186">클릭 합니다 **자세한 보기로 이동** 이 API 호출의 응답에 대 한 자세한 내용을 보려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="519e7-187">![자세히 보기를 전환할](build-restful-apis-with-aspnet-web-api/_static/image8.png "세부 정보 보기로 전환")</span><span class="sxs-lookup"><span data-stu-id="519e7-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="519e7-188">*자세한 보기로 전환*</span><span class="sxs-lookup"><span data-stu-id="519e7-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="519e7-189">클릭 합니다 **응답 본문** 실제 JSON 응답 텍스트를 보려면 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="519e7-190">![네트워크 모니터에서 텍스트를 출력 JSON을 보는](build-restful-apis-with-aspnet-web-api/_static/image9.png "네트워크 모니터에서 텍스트를 출력 JSON 보기")</span><span class="sxs-lookup"><span data-stu-id="519e7-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="519e7-191">*네트워크 모니터에서 JSON 출력 텍스트 보기*</span><span class="sxs-lookup"><span data-stu-id="519e7-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="519e7-192">작업 3-연락처 모델을 만드는 고 Contact Controller 보강</span><span class="sxs-lookup"><span data-stu-id="519e7-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="519e7-193">이 태스크에서는 API 메서드 상주할 컨트롤러 클래스를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="519e7-194">마우스 오른쪽 단추로 클릭 합니다 **모델** 선택한 폴더 **추가 | 클래스...**  상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="519e7-195">![웹 응용 프로그램에 새 모델 추가](build-restful-apis-with-aspnet-web-api/_static/image10.png "웹 응용 프로그램에 새 모델 추가")</span><span class="sxs-lookup"><span data-stu-id="519e7-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="519e7-196">*웹 응용 프로그램에 새 모델 추가*</span><span class="sxs-lookup"><span data-stu-id="519e7-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="519e7-197">에 **새 항목 추가** 대화 상자에서 새 파일 이름 **Contact.cs** 를 클릭 하 고 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="519e7-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="519e7-198">![새 연락처 클래스 파일을 만드는](build-restful-apis-with-aspnet-web-api/_static/image11.png "새 연락처 클래스 파일 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="519e7-199">*새 연락처 클래스 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="519e7-200">다음 강조 표시 된 코드를 추가 합니다 **연락처** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="519e7-201">(코드 조각- *웹 API 랩-Ex01-연락처 클래스*)</span><span class="sxs-lookup"><span data-stu-id="519e7-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="519e7-202">에 **contact ¡© Controller** 클래스, 단어를 선택 **문자열** 의 메서드 정의에 **가져오기** 메서드와 해당 단어 입력 *연락처*합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="519e7-203">단어를 입력, 표시기 단어의 시작 부분에 표시 됩니다 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="519e7-204">중 하나를 길게 누른 합니다 **Ctrl** 키 및 마침표 (.) 키를 누르거나 마우스를 사용 하 여 코드 편집기 자동으로 맞게 지원 대화 상자를 열려면 아이콘을 클릭 합니다 **사용 하 여** 모델에 대 한 지시문 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![네임 스페이스 선언에 대 한 Intellisense 지원을 사용 하 여](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="519e7-206">*네임 스페이스 선언에 대 한 Intellisense 지원을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="519e7-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="519e7-207">코드를 수정 합니다 **가져올** 메서드 담당자 모델 인스턴스 배열을 반환 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="519e7-208">(코드 조각- *웹 API 랩-Ex01-연락처 목록을 반환*)</span><span class="sxs-lookup"><span data-stu-id="519e7-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="519e7-209">키를 눌러 **F5** 브라우저에서 웹 응용 프로그램을 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="519e7-210">변경 내용을 API의 응답 출력을 보려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="519e7-211">키를 눌러 브라우저 열리면 **F12** 아직 개발자 도구 열려 있지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="519e7-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="519e7-212">클릭 합니다 **네트워크** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="519e7-213">키를 눌러 합니다 **캡처 시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="519e7-214">URL 접미사를 추가 **/api/contact** 누릅니다 주소 표시줄에서 URL에는 **Enter** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="519e7-215">키를 눌러 합니다 **자세한 보기로 이동** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="519e7-216">선택 된 **응답 본문** 탭 합니다. Serialize 된 형태의 연락처 인스턴스 배열 나타내는 JSON 문자열로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="519e7-217">![JSON 직렬화는 복잡 한 웹 API 메서드 호출의 출력](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 직렬화는 복잡 한 웹 API 메서드 호출의 출력")</span><span class="sxs-lookup"><span data-stu-id="519e7-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="519e7-218">*복잡 한 웹 API 메서드 호출의 JSON 직렬화 된 출력*</span><span class="sxs-lookup"><span data-stu-id="519e7-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="519e7-219">작업 4-압축 풀기 서비스 계층 기능</span><span class="sxs-lookup"><span data-stu-id="519e7-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="519e7-220">이 작업에서는 개발자가 실제로 작업을 수행 하는 서비스의 재사용 가능성 있기 때문에, 컨트롤러 계층에서 해당 서비스 기능을 분리 하는 데 쉽게 서비스 계층에 기능을 추출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="519e7-221">솔루션 루트에 새 폴더를 만들고 이름을 **Services**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="519e7-222">이렇게 하려면 마우스 오른쪽 단추로 클릭 **ContactManager** 프로젝트 선택 **추가** | **새 폴더**, 이름을 *Services*합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="519e7-223">![서비스 폴더 만들기](build-restful-apis-with-aspnet-web-api/_static/image14.png "서비스 만들기 폴더")</span><span class="sxs-lookup"><span data-stu-id="519e7-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="519e7-224">*서비스 폴더 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="519e7-225">마우스 오른쪽 단추로 클릭 합니다 **Services** 선택한 폴더 **추가 | 클래스...**  상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="519e7-226">![서비스 폴더에 새 클래스 추가](build-restful-apis-with-aspnet-web-api/_static/image15.png "서비스 폴더에 새 클래스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="519e7-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="519e7-227">*서비스 폴더에 새 클래스를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="519e7-228">경우는 **새 항목 추가** 대화 상자가 나타나면 새 클래스의 이름을 **ContactRepository** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="519e7-229">![연락처 저장소 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일을 만드는](build-restful-apis-with-aspnet-web-api/_static/image16.png "연락처 저장소 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="519e7-230">*연락처 저장소 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="519e7-231">추가 하 여 지시문을 **ContactRepository.cs** 모델 네임 스페이스를 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="519e7-232">다음 강조 표시 된 코드를 추가 합니다 **ContactRepository.cs** GetAllContacts 메서드를 구현 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="519e7-233">(코드 조각- *웹 API 랩-Ex01-연락처 리포지토리*)</span><span class="sxs-lookup"><span data-stu-id="519e7-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="519e7-234">엽니다는 **ContactController.cs** 열려 있지 않으면 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="519e7-235">다음 추가 문을 사용 하 여 파일의 네임 스페이스 선언 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="519e7-236">다음 강조 표시 된 코드를 추가 합니다 **ContactController.cs** 서비스 구현의 사용 하 여 나머지 클래스 멤버가 만들 수 있도록 저장소의 인스턴스를 나타내는 개인 필드를 추가 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="519e7-237">(코드 조각- *Web API 랩-Ex01-연락처 컨트롤러*)</span><span class="sxs-lookup"><span data-stu-id="519e7-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="519e7-238">변경 된 **가져오기** 메서드를 사용 하면 연락처 저장소 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="519e7-239">(코드 조각- *리포지토리를 통해 연락처 목록을 반환 웹 API 랩-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="519e7-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="519e7-240">중단점을 설정 하는 **contact ¡© Controller**의 **가져오기** 메서드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="519e7-241">![연락처 컨트롤러에 중단점을 추가](build-restful-apis-with-aspnet-web-api/_static/image17.png "연락처 컨트롤러에 중단점을 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="519e7-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="519e7-242">*연락처 컨트롤러에 중단점을 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="519e7-243">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="519e7-244">브라우저가 열리면 키를 눌러 **F12** 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="519e7-245">클릭 합니다 **네트워크** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="519e7-246">클릭 합니다 **캡처 시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="519e7-247">접미사를 사용 하 여 주소 표시줄에 URL을 추가 **/api/contact** 누릅니다 **Enter** API 컨트롤러를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="519e7-248">Visual Studio 2012를 한 번 나눌 **가져올** 메서드 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="519e7-249">![Get 메서드 내에서 주요](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 메서드 내에서 주요")</span><span class="sxs-lookup"><span data-stu-id="519e7-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="519e7-250">*Get 메서드 내에서 분리*</span><span class="sxs-lookup"><span data-stu-id="519e7-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="519e7-251">**F5**를 눌러 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="519e7-252">으로 돌아가 Internet Explorer에 포커스가 없습니다 있으면</span><span class="sxs-lookup"><span data-stu-id="519e7-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="519e7-253">네트워크 캡처 창을 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-253">Note the network capture window.</span></span>

    <span data-ttu-id="519e7-254">![네트워크에서 Internet Explorer 웹 API 호출의 결과 보여 주는 보기](build-restful-apis-with-aspnet-web-api/_static/image19.png "네트워크 웹 API 호출의 결과 표시 하는 Internet Explorer에서 보기")</span><span class="sxs-lookup"><span data-stu-id="519e7-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="519e7-255">*웹 API 호출의 결과 표시 하는 Internet Explorer에서 네트워크 보기*</span><span class="sxs-lookup"><span data-stu-id="519e7-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="519e7-256">클릭 합니다 **자세한 보기로 이동** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="519e7-257">클릭 합니다 **응답 본문** 탭 합니다. API 호출의 JSON 출력을 확인 하 고 서비스 계층에서 검색할 두 개의 연락처를 나타내는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="519e7-258">![개발자 도구 창에서 웹 API에서 JSON 출력을 보는](build-restful-apis-with-aspnet-web-api/_static/image20.png "개발자 도구 창에서 웹 API에서 JSON 출력 보기")</span><span class="sxs-lookup"><span data-stu-id="519e7-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="519e7-259">*개발자 도구 창에서 웹 API에서 JSON 출력 보기*</span><span class="sxs-lookup"><span data-stu-id="519e7-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="519e7-260">연습 2: 읽기/쓰기 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="519e7-261">이 연습에서는 게시물을 구현 하 고 데이터 편집 기능을 사용 하 여 사용 하도록 설정 하려면 대화 상대 관리자에 대 한 PUT 메서드.</span><span class="sxs-lookup"><span data-stu-id="519e7-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="519e7-262">작업 1-웹 API 프로젝트를 열고</span><span class="sxs-lookup"><span data-stu-id="519e7-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="519e7-263">이 태스크에서는 사용자 입력을 수락할 수 있도록 실습 1에서 만든 웹 API 프로젝트를 향상 시키기 위해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="519e7-264">실행할 **Visual Studio 2012 Express for Web**,이 이동 작업을 수행 하 **시작** 유형과 **VS Express for Web** 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="519e7-265">엽니다는 **시작할** 솔루션에 있는 **소스/Ex02-ReadWriteWebAPI/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="519e7-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="519e7-266">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="519e7-267">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="519e7-268">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="519e7-269">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="519e7-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="519e7-270">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="519e7-271">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="519e7-272">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="519e7-273">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="519e7-274">엽니다는 **Services/ContactRepository.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="519e7-275">작업 2-연락처 리포지토리 구현은 데이터 지 속성 기능 추가</span><span class="sxs-lookup"><span data-stu-id="519e7-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="519e7-276">이 태스크에서는 유지 사용자 입력에 새 연락처 인스턴스 동의할 수 있도록 실습 1에서 만든 웹 API 프로젝트의 ContactRepository 클래스를 보강 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="519e7-277">다음 상수를 추가 합니다 **ContactRepository** 웹 서버 캐시 항목 키 이름이이 연습 뒷부분에서의 이름을 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="519e7-278">생성자를 추가 합니다 **ContactRepository** 다음 코드를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="519e7-279">(코드 조각- *웹 API 랩-Ex02-연락처 리포지토리 생성자*)</span><span class="sxs-lookup"><span data-stu-id="519e7-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="519e7-280">코드를 수정 합니다 **GetAllContacts** 아래 설명 된 대로 메서드.</span><span class="sxs-lookup"><span data-stu-id="519e7-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="519e7-281">(코드 조각- *웹 API 랩-Ex02-모든 연락처 가져오기*)</span><span class="sxs-lookup"><span data-stu-id="519e7-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="519e7-282">이 예제에서는 데모용 이며 값은 세션 저장소 메커니즘 또는 요청 저장소 수명 사용 하지 않고 동시에 여러 클라이언트에서 사용할 수는 있도록 저장 매체에으로 웹 서버의 캐시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="519e7-283">웹 서버 캐시 대신 Entity Framework, XML 저장소 또는 다른 다양 한 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="519e7-284">라는 새 메서드를 구현 **SaveContact** 에 **ContactRepository** 연락처를 저장 하는 작업을 수행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="519e7-285">**SaveContact** 메서드는 단일 취해야 **연락처** 성공 또는 실패를 나타내는 매개 변수 및 반환 된 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="519e7-286">(코드 조각- *웹 API 랩-Ex02-SaveContact 메서드 구현*)</span><span class="sxs-lookup"><span data-stu-id="519e7-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="519e7-287">연습 3: HTML 클라이언트에서 Web API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="519e7-288">이 연습에서는 웹 API를 호출 하려면 HTML 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="519e7-289">이 클라이언트는 JavaScript를 사용 하 여 Web API를 사용 하 여 데이터 교환을 원활 하 게 되며 HTML 태그를 사용 하 여 웹 브라우저에서 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="519e7-290">작업 1-연락처를 표시 하기 위한 GUI를 제공 하도록 인덱스 보기 수정</span><span class="sxs-lookup"><span data-stu-id="519e7-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="519e7-291">이 태스크에서는 HTML 브라우저에서 기존 연락처 목록을 표시 하는 요구 사항을 지원 하도록 웹 응용 프로그램의 기본 인덱스 뷰를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="519e7-292">엽니다 **Visual Studio 2012 Express for Web** 열려 있지 않으면입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="519e7-293">엽니다는 **시작할** 솔루션에 있는 **소스/Ex03-ConsumingWebAPI/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="519e7-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="519e7-294">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="519e7-295">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="519e7-296">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="519e7-297">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="519e7-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="519e7-298">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="519e7-299">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="519e7-300">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="519e7-301">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="519e7-302">엽니다는 **Index.cshtml** 파일에 있는 **Views/Home** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="519e7-303">Div 요소 내에서 HTML 코드를 id로 바꿉니다 **본문** 다음 코드와 같이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="519e7-304">Web API에 HTTP 요청을 수행 하는 파일의 맨 아래에 다음 Javascript 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="519e7-305">엽니다는 **ContactController.cs** 열려 있지 않으면 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="519e7-306">중단점을 설정 합니다 **가져오기** 메서드는 **contact ¡© Controller** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="519e7-307">![API 컨트롤러의 Get 메서드에 중단점을 배치한](build-restful-apis-with-aspnet-web-api/_static/image21.png "API 컨트롤러에서 Get 메서드의 중단점 배치")</span><span class="sxs-lookup"><span data-stu-id="519e7-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="519e7-308">*API 컨트롤러에서 Get 메서드의 중단점 배치*</span><span class="sxs-lookup"><span data-stu-id="519e7-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="519e7-309">**F5** 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-309">Press **F5** to run the project.</span></span> <span data-ttu-id="519e7-310">브라우저는 HTML 문서를 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-311">탐색 하는 응용 프로그램의 루트 URL을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="519e7-312">페이지가 로드 하 고 JavaScript 실행에서는 중단점이 적중 되지 것입니다 및 컨트롤러의 코드 실행을 일시 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="519e7-313">![VS Express for Web 사용 하 여 Web API 호출으로 디버깅](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web 사용 하 여 Web API 호출으로 디버깅")</span><span class="sxs-lookup"><span data-stu-id="519e7-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="519e7-314">*웹용 Visual Studio 2012 Express를 사용 하 여 Web API 호출으로 디버깅*</span><span class="sxs-lookup"><span data-stu-id="519e7-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="519e7-315">중단점 및 키를 눌러 제거 **F5** 또는 디버깅 도구 모음 **계속** 브라우저에서 보기를 로드 합니다. 계속 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="519e7-316">웹 API 호출이 완료 되 면 브라우저에서 목록 항목으로 표시를 호출 하는 Web API에서 반환 된 연락처 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="519e7-317">![브라우저에서 목록 항목으로 표시 하는 API 호출의 결과](build-restful-apis-with-aspnet-web-api/_static/image23.png "브라우저에서 목록 항목으로 표시 하는 API 호출의 결과")</span><span class="sxs-lookup"><span data-stu-id="519e7-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="519e7-318">*브라우저에서 목록 항목으로 표시 하는 API 호출의 결과*</span><span class="sxs-lookup"><span data-stu-id="519e7-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="519e7-319">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="519e7-320">작업 2-연락처 만들기 위한 GUI를 제공 하도록 인덱스 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="519e7-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="519e7-321">이 태스크에서는 MVC 응용 프로그램의 인덱스 뷰를 수정 하려면 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="519e7-322">사용자 입력 캡처 되며 새 연락처를 만드는 웹 API에 전송 하는 HTML 페이지에 추가할 폼 및 GUI에서 날짜를 수집 하려면 새 Web API 컨트롤러 메서드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="519e7-323">엽니다는 **ContactController.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="519e7-324">명명 된 컨트롤러 클래스에 새 메서드를 추가 **Post** 다음 코드와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="519e7-325">(코드 조각- *웹 API 랩-Ex03-Post 메서드*)</span><span class="sxs-lookup"><span data-stu-id="519e7-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="519e7-326">엽니다는 **Index.cshtml** 열려 있지 않으면 Visual Studio에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="519e7-327">이전 태스크에서 추가한 목록 바로 뒤 파일에 다음 HTML 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="519e7-328">문서의 맨 아래에 있는 스크립트 요소 내 데이터에 게시 된 Web API HTTP POST 호출을 사용 하는 단추 클릭 이벤트를 처리 하는 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="519e7-329">**ContactController.cs**에 중단점을 배치 합니다 **Post** 메서드.</span><span class="sxs-lookup"><span data-stu-id="519e7-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="519e7-330">키를 눌러 **F5** 브라우저에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="519e7-331">새 연락처 이름, Id 및 클릭에 대 한 페이지를 브라우저에서 로드 되 면 입력 합니다 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="519e7-332">![클라이언트 HTML 문서가 브라우저에 로드](build-restful-apis-with-aspnet-web-api/_static/image24.png "브라우저에 HTML 클라이언트 문서 로드")</span><span class="sxs-lookup"><span data-stu-id="519e7-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="519e7-333">*클라이언트 HTML 문서가 브라우저에 로드*</span><span class="sxs-lookup"><span data-stu-id="519e7-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="519e7-334">디버거 창 중단 하는 경우는 **게시물** 메서드, 속성을 살펴보십시오 합니다 **에 문의** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="519e7-335">값 형식으로 입력 데이터를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="519e7-336">![클라이언트에서 Web API에 전송 되는 연락처 개체](build-restful-apis-with-aspnet-web-api/_static/image25.png "클라이언트에서 Web API에 전송 되는 연락처 개체")</span><span class="sxs-lookup"><span data-stu-id="519e7-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="519e7-337">*클라이언트에서 Web API에 전송 되는 연락처 개체*</span><span class="sxs-lookup"><span data-stu-id="519e7-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="519e7-338">될 때까지 디버거에서 메서드를 통해 단계를 **응답** 변수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="519e7-339">검사 시 합니다 **지역** 디버거에서 창 표시 속성을 모두 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="519e7-340">![디버거에서 만든 응답](build-restful-apis-with-aspnet-web-api/_static/image26.png "디버거에서 만든 응답")</span><span class="sxs-lookup"><span data-stu-id="519e7-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="519e7-341">*디버거에서 만든 응답*</span><span class="sxs-lookup"><span data-stu-id="519e7-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="519e7-342">키를 누르면 **F5** 누르거나 **계속** 디버거에서 요청이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="519e7-343">새 연락처를 저장 하는 연락처 목록에 추가한 브라우저로 전환 하면 합니다 **ContactRepository** 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="519e7-344">![브라우저에 새 연락처 인스턴스를 성공적으로 만든 반영](build-restful-apis-with-aspnet-web-api/_static/image27.png "브라우저 반영 새 연락처 인스턴스 만들기 성공")</span><span class="sxs-lookup"><span data-stu-id="519e7-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="519e7-345">*성공적으로 만드는 새 연락처 인스턴스를 반영 하는 브라우저*</span><span class="sxs-lookup"><span data-stu-id="519e7-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="519e7-346">또한 Azure는 다음이 응용이 프로그램을 배포할 수 [부록 c: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixC)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>


---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="519e7-347">요약</span><span class="sxs-lookup"><span data-stu-id="519e7-347">Summary</span></span>

<span data-ttu-id="519e7-348">이 랩의 RESTful Web Api 프레임 워크를 사용 하 여 구현 하는 새로운 ASP.NET Web API 프레임 워크를 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="519e7-349">여기에서 임의 개수의 메커니즘을 사용 하 여 데이터 지 속성을 용이 하 게 하는 새 리포지토리를 만들고 간단한 것이이 랩의 예로 제공 하는 대신 해당 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="519e7-350">Web API는 다양 한 HTTP 및 JSON 또는 XML을 지 원하는 모든 언어로 작성 된 HTML이 아닌 클라이언트 로부터의 통신을 사용 하도록 설정 하는 등의 추가 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="519e7-351">일반적인 웹 응용 프로그램 외부에서 Web API를 호스트 하는 기능 것도 가능 합니다 뿐만 아니라 고유한 serialization 형식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="519e7-352">ASP.NET 웹 사이트에서 ASP.NET Web API 프레임 워크에 전용 영역이 [ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="519e7-353">이 사이트는 계속 최신 정보, 샘플 및 웹 API와 관련 된 뉴스 따라서 확인 자주 제공 거의 모든 장치 또는 개발 프레임 워크를 사용할 수 있는 사용자 지정 Web Api를 만드는 아트를 철저히 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="519e7-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="519e7-354">부록 a: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="519e7-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="519e7-355">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="519e7-356">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="519e7-357">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](build-restful-apis-with-aspnet-web-api/_static/image28.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="519e7-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="519e7-358">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="519e7-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="519e7-359">키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="519e7-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="519e7-360">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="519e7-361">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="519e7-362">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="519e7-363">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="519e7-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="519e7-364">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="519e7-365">![코드 조각 이름을 입력](build-restful-apis-with-aspnet-web-api/_static/image29.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="519e7-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="519e7-366">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="519e7-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="519e7-367">![Tab 키를 눌러 강조 표시 된 코드 조각을](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="519e7-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="519e7-368">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="519e7-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="519e7-369">![Tab 키를 다시 코드 조각 확장 됩니다](build-restful-apis-with-aspnet-web-api/_static/image31.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="519e7-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="519e7-370">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="519e7-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="519e7-371">마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="519e7-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="519e7-372">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="519e7-373">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="519e7-374">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="519e7-375">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](build-restful-apis-with-aspnet-web-api/_static/image32.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="519e7-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="519e7-376">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="519e7-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="519e7-377">![클릭 하 여 목록에서 관련 코드 조각 선택](build-restful-apis-with-aspnet-web-api/_static/image33.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="519e7-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="519e7-378">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="519e7-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="519e7-379">부록 b: Express 2012 for Web Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="519e7-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="519e7-380">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="519e7-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="519e7-381">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="519e7-382">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="519e7-383">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Azure SDK를 사용 하 여</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="519e7-384">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-384">Click on **Install Now**.</span></span> <span data-ttu-id="519e7-385">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="519e7-386">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="519e7-387">![Visual Studio Express를 설치](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="519e7-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="519e7-388">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="519e7-389">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="519e7-391">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="519e7-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="519e7-392">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-392">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="519e7-394">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="519e7-394">*Installation progress*</span></span>
6. <span data-ttu-id="519e7-395">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-395">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="519e7-397">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="519e7-397">*Installation completed*</span></span>
7. <span data-ttu-id="519e7-398">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="519e7-399">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="519e7-401">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="519e7-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="519e7-402">부록 c: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="519e7-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="519e7-403">이 부록은 Azure Portal에서 새 웹 사이트를 만들고 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="519e7-404">작업 1-Azure Portal에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="519e7-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="519e7-405">로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-406">Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="519e7-407">등록할 수 있습니다 [여기](https://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="519e7-408">![Windows Azure 포털에 로그온](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure 포털에 로그온")</span><span class="sxs-lookup"><span data-stu-id="519e7-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="519e7-409">*포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="519e7-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="519e7-410">클릭 **새로 만들기** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="519e7-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="519e7-411">![새 웹 사이트를 만드는](build-restful-apis-with-aspnet-web-api/_static/image40.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="519e7-412">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="519e7-413">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="519e7-414">선택한 **빨리 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="519e7-415">새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-416">Azure는 웹 응용 프로그램을 제어 하 고 관리할 수 있는 클라우드에서 실행 중인 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="519e7-417">빠른 생성 옵션을 사용 하면 포털 외부에서 Azure에 완전된 한 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="519e7-418">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="519e7-419">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](build-restful-apis-with-aspnet-web-api/_static/image41.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="519e7-420">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="519e7-421">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="519e7-422">웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="519e7-423">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="519e7-424">![새 웹 사이트를 찾아](build-restful-apis-with-aspnet-web-api/_static/image42.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="519e7-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="519e7-425">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="519e7-426">![실행 중인 웹 사이트](build-restful-apis-with-aspnet-web-api/_static/image43.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="519e7-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="519e7-427">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="519e7-427">*Web site running*</span></span>
6. <span data-ttu-id="519e7-428">포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="519e7-429">![웹 사이트 관리 페이지를 열어](build-restful-apis-with-aspnet-web-api/_static/image44.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="519e7-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="519e7-430">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="519e7-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="519e7-431">**대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="519e7-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-432">합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Azure 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="519e7-433">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="519e7-434">**Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Azure에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="519e7-435">![게시 프로필 다운로드 웹 사이트](build-restful-apis-with-aspnet-web-api/_static/image45.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="519e7-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="519e7-436">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="519e7-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="519e7-437">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="519e7-438">추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="519e7-439">![게시 프로필 파일을 저장](build-restful-apis-with-aspnet-web-api/_static/image46.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="519e7-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="519e7-440">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="519e7-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="519e7-441">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="519e7-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="519e7-442">응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="519e7-443">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="519e7-444">응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="519e7-445">SQL Database 서버에 Azure 관리 포털의 구독에서 볼 수 있습니다 **Sql Database** | **서버** | **서버대시보드**.</span><span class="sxs-lookup"><span data-stu-id="519e7-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="519e7-446">만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="519e7-447">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="519e7-448">만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="519e7-449">![SQL Database 서버 대시보드](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="519e7-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="519e7-450">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="519e7-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="519e7-451">다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="519e7-452">이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="519e7-454">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="519e7-455">한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="519e7-457">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="519e7-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="519e7-458">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="519e7-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="519e7-459">ASP.NET MVC 4 솔루션 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="519e7-460">에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="519e7-461">![응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image51.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="519e7-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="519e7-462">*웹 사이트를 게시합니다.*</span><span class="sxs-lookup"><span data-stu-id="519e7-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="519e7-463">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="519e7-464">![게시 프로필 가져오기](build-restful-apis-with-aspnet-web-api/_static/image52.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="519e7-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="519e7-465">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="519e7-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="519e7-466">클릭 **연결의 유효성을 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-466">Click **Validate Connection**.</span></span> <span data-ttu-id="519e7-467">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="519e7-468">연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="519e7-469">![연결 유효성 검사](build-restful-apis-with-aspnet-web-api/_static/image53.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="519e7-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="519e7-470">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="519e7-470">*Validating connection*</span></span>
4. <span data-ttu-id="519e7-471">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="519e7-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="519e7-472">![웹 배포 구성](build-restful-apis-with-aspnet-web-api/_static/image54.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="519e7-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="519e7-473">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="519e7-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="519e7-474">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="519e7-475">에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="519e7-476">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="519e7-477">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="519e7-478">예를 들어 새 데이터베이스 이름을 입력 합니다. *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="519e7-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="519e7-479">![대상 연결 문자열 구성](build-restful-apis-with-aspnet-web-api/_static/image55.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="519e7-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="519e7-480">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="519e7-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="519e7-481">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-481">Then click **OK**.</span></span> <span data-ttu-id="519e7-482">데이터베이스를 만들라는 메시지가 나오면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="519e7-483">![데이터베이스를 만드는](build-restful-apis-with-aspnet-web-api/_static/image56.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="519e7-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="519e7-484">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="519e7-484">*Creating the database*</span></span>
7. <span data-ttu-id="519e7-485">기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="519e7-486">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-486">Then click **Next**.</span></span>

    <span data-ttu-id="519e7-487">![SQL Database를 가리키는 연결 문자열](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="519e7-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="519e7-488">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="519e7-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="519e7-489">에 **미리 보기** 페이지에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="519e7-490">![웹 응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image58.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="519e7-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="519e7-491">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="519e7-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="519e7-492">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="519e7-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="519e7-493">![Windows Azure에 응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image59.png "응용 프로그램이 Windows Azure에 게시")</span><span class="sxs-lookup"><span data-stu-id="519e7-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="519e7-494">*응용 프로그램을 Azure에 게시*</span><span class="sxs-lookup"><span data-stu-id="519e7-494">*Application published to Azure*</span></span>
