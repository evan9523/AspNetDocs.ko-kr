---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 모델 바인딩 및 web forms를 사용 하는 프로젝트에 추가 비즈니스 논리 레이어 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65109169"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="f12c4-104">모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 레이어 추가</span><span class="sxs-lookup"><span data-stu-id="f12c4-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="f12c4-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f12c4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f12c4-106">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="f12c4-107">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="f12c4-108">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="f12c4-109">이 자습서에서는 비즈니스 논리 레이어를 사용 하 여 모델 바인딩을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="f12c4-110">데이터 메서드를 호출 하려면 현재 페이지 이외의 개체가 사용 되도록 지정 OnCallingDataMethods 멤버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="f12c4-111">이 자습서에서 만든 프로젝트를 기반 합니다 [이전](retrieving-data.md) 시리즈의 파트입니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="f12c4-112">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f12c4-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="f12c4-113">다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="f12c4-114">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="f12c4-115">만들 내용</span><span class="sxs-lookup"><span data-stu-id="f12c4-115">What you'll build</span></span>

<span data-ttu-id="f12c4-116">모델 바인딩을 사용 하면 웹 페이지에 대 한 코드 숨김 파일에서 또는 별도 비즈니스 논리 클래스에서 데이터 상호 작용 코드를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="f12c4-117">이전 자습서에는 데이터 상호 작용 코드에 대 한 코드 숨김 파일을 사용 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="f12c4-118">이 방법은 소규모 사이트에 있지만 코드 반복 및 어려움 대규모 사이트 유지 관리 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="f12c4-119">또한 프로그래밍 방식으로 추상화 계층이 없으므로 코드 숨김 파일에에서 있는 코드를 테스트 하는 것이 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="f12c4-120">데이터 상호 작용 코드를 중앙 집중화 함으로써 모든 데이터와 상호 작용에 대 한 논리를 포함 하는 비즈니스 논리 레이어를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="f12c4-121">그런 다음 웹 페이지에서 비즈니스 논리 계층을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="f12c4-122">이 자습서에는 모든 비즈니스 논리 계층으로 이전 자습서에서 작성 한 코드를 이동한 다음 페이지에서 해당 코드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="f12c4-123">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="f12c4-124">코드 숨김 파일에서 비즈니스 논리 레이어 코드 이동</span><span class="sxs-lookup"><span data-stu-id="f12c4-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="f12c4-125">비즈니스 논리 계층에서 메서드를 호출 하 여 데이터 바인딩된 컨트롤 변경</span><span class="sxs-lookup"><span data-stu-id="f12c4-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="f12c4-126">비즈니스 논리 레이어 만들기</span><span class="sxs-lookup"><span data-stu-id="f12c4-126">Create business logic layer</span></span>

<span data-ttu-id="f12c4-127">이제 웹 페이지에서 호출 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="f12c4-128">이 클래스의 메서드는 이전 자습서에서 사용 된 메서드를 유사 하 고 값 공급자 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="f12c4-129">먼저 이라는 새 폴더를 추가 **BLL**합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-129">First, add a new folder called **BLL**.</span></span>

![폴더 추가](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="f12c4-131">BLL 폴더에서 라는 새 클래스를 만듭니다 **SchoolBL.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="f12c4-132">데이터 작업을 마치 원래 코드 숨김 파일에 있는 모든 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="f12c4-133">메서드는 메서드를 코드 숨김 파일에서와 거의 동일 하지만 일부 변경 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="f12c4-134">참고에서 가장 중요 한 변경의 인스턴스 내에서 코드를 실행 하 고 더 이상 되는 것 **페이지** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="f12c4-135">페이지 클래스를 포함 합니다 **tryupdatemodel에 전달** 메서드 및 **ModelState** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="f12c4-136">이 코드는 비즈니스 논리 계층으로 이동 하면 이러한 멤버를 호출 하려면 페이지 클래스의 인스턴스는 더 이상.</span><span class="sxs-lookup"><span data-stu-id="f12c4-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="f12c4-137">를이 문제를 해결 하기 위해 추가 해야 합니다는 **ModelMethodContext** tryupdatemodel에 전달 하거나 ModelState에 액세스 하는 모든 메서드에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="f12c4-138">호출 tryupdatemodel에 전달 하거나 ModelState 검색할이 ModelMethodContext 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="f12c4-139">이 새 매개 변수에 대 한 계정 웹 페이지에 아무 것도 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="f12c4-140">SchoolBL.cs에서 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="f12c4-141">비즈니스 논리 계층에서 데이터를 검색할 기존 페이지를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="f12c4-142">마지막으로 쿼리를 사용 하 여 비즈니스 논리 계층을 사용 하 여 코드 숨김 파일에에서 Students.aspx, AddStudent.aspx, 및 Courses.aspx 페이지를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="f12c4-143">AddStudent, 학생과 강좌에 대 한 코드 숨김 파일에서 삭제 하거나 다음과 같은 쿼리 메서드를 주석:</span><span class="sxs-lookup"><span data-stu-id="f12c4-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="f12c4-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="f12c4-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="f12c4-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="f12c4-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="f12c4-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="f12c4-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="f12c4-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="f12c4-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="f12c4-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="f12c4-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="f12c4-149">이제 해야 코드가 없는 데이터 작업에 관련 된 코드 숨김 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="f12c4-150">합니다 **OnCallingDataMethods** 이벤트 처리기를 사용 하면 데이터 메서드를 사용 하는 개체를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="f12c4-151">Students.aspx에서 해당 이벤트 처리기에 대 한 값을 추가 하 고 데이터 메서드 이름에는 비즈니스 논리 클래스의 메서드 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="f12c4-152">Students.aspx에 대 한 코드 숨김 파일에서 CallingDataMethods 이벤트에 대 한 이벤트 처리기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="f12c4-153">이 이벤트 처리기에서 데이터 작업에 대 한 비즈니스 논리 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="f12c4-154">AddStudent.aspx에서 유사한 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="f12c4-155">Courses.aspx에서 유사한 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="f12c4-156">응용 프로그램을 실행 하 고 페이지의 모든 이전에 사용 했던 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="f12c4-157">또한 유효성 검사 논리가 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="f12c4-158">결론</span><span class="sxs-lookup"><span data-stu-id="f12c4-158">Conclusion</span></span>

<span data-ttu-id="f12c4-159">이 자습서에서는 데이터 액세스 계층 및 비즈니스 논리 레이어를 사용 하도록 응용 프로그램 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="f12c4-160">지정한 데이터 컨트롤 데이터 작업에 대 한 현재 페이지 없는 개체를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="f12c4-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f12c4-161">이전</span><span class="sxs-lookup"><span data-stu-id="f12c4-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
