---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 모델 바인딩 및 web forms에 JQuery UI Datepicker 통합 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521981"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="999a6-104">모델 바인딩 및 web forms에 JQuery UI Datepicker 통합</span><span class="sxs-lookup"><span data-stu-id="999a6-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="999a6-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="999a6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="999a6-106">이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="999a6-107">모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="999a6-108">이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="999a6-109">이 자습서에서는 웹 양식에 JQuery UI [Datepicker 위젯을](http://jqueryui.com/datepicker/) 추가 하 고 모델 바인딩을 사용 하 여 선택한 값으로 데이터베이스를 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="999a6-110">이 자습서는 계열의 [첫](retrieving-data.md) 번째와 [두 번째](updating-deleting-and-creating-data.md) 부분에서 만든 프로젝트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="999a6-111">또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="999a6-112">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="999a6-113">이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="999a6-114">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="999a6-114">What you'll build</span></span>

<span data-ttu-id="999a6-115">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="999a6-116">모델에 속성을 추가 하 여 학생의 등록 날짜 기록</span><span class="sxs-lookup"><span data-stu-id="999a6-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="999a6-117">사용자가 JQuery UI Datepicker 위젯을 사용 하 여 등록 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="999a6-118">등록 날짜에 대 한 유효성 검사 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="999a6-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="999a6-119">사용자는 JQuery UI Datepicker 위젯을 사용 하 여 사용자가 필드와 상호 작용할 때 팝업 되는 달력에서 날짜를 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="999a6-120">이 위젯을 사용 하면 사용자가 수동으로 날짜를 입력 하는 것 보다 더 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="999a6-121">데이터 작업에 모델 바인딩을 사용 하는 페이지에 Datepicker 위젯을 통합 하려면 약간의 추가 작업만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="999a6-122">모델에 새 속성 추가</span><span class="sxs-lookup"><span data-stu-id="999a6-122">Add a new property to the model</span></span>

<span data-ttu-id="999a6-123">먼저 Student 모델에 **Datetime** 속성을 추가 하 고이 변경 내용을 데이터베이스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="999a6-124">**UniversityModels.cs**를 열고 강조 표시 된 코드를 학생 모델에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="999a6-125">범위 **특성** 은 속성에 대 한 유효성 검사 규칙을 적용 하기 위해 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="999a6-126">이 자습서에서는 Contoso 대학이 2013 년 1 월 1 일에 설립 된 것으로 가정 하므로 이전 등록 날짜가 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="999a6-127">패키지 관리 창에서 **add Migration AddEnrollmentDate**명령을 실행 하 여 마이그레이션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="999a6-128">마이그레이션 코드는 Student 테이블에 새 Datetime 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="999a6-129">범위 특성에 지정 된 값과 일치 시키려면 아래 강조 표시 된 코드에 표시 된 대로 새 열에 대 한 기본값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="999a6-130">마이그레이션 파일의 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-130">Save your change to the migration file.</span></span>

<span data-ttu-id="999a6-131">데이터를 다시 시드해야 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-131">You do not need to seed the data again.</span></span> <span data-ttu-id="999a6-132">따라서 마이그레이션 폴더에서 **Configuration.cs** 를 열고 **초기값** 메서드에서 코드를 제거 하거나 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="999a6-133">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-133">Save and close the file.</span></span>

<span data-ttu-id="999a6-134">이제 **update-database**명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="999a6-135">이제 열이 데이터베이스에 존재 하 고 모든 기존 레코드에 EnrollmentDate에 대 한 기본값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="999a6-136">등록 날짜에 대 한 동적 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="999a6-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="999a6-137">이제 등록 날짜를 표시 하 고 편집 하기 위한 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="999a6-138">이 시점에서 텍스트 상자를 통해 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="999a6-139">이 자습서의 뒷부분에서 텍스트 상자를 JQuery Datepicker widget으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="999a6-140">먼저 **Addstudent .aspx** 파일을 변경 하지 않아도 된다는 점에 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="999a6-141">DynamicEntity 컨트롤이 새 속성을 자동으로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="999a6-142">**학습자**를 열고 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="999a6-143">응용 프로그램을 실행 하 고 날짜를 입력 하 여 등록 날짜의 값을 설정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="999a6-144">새 학생을 추가 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="999a6-144">When adding a new student:</span></span>

![날짜 설정](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="999a6-146">또는 기존 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-146">Or, editing an existing value:</span></span>

![날짜 편집](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="999a6-148">날짜를 입력 하는 작업은 작동 하지만 사용자가 제공 하려는 사용자 환경이 아닐 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="999a6-149">다음 섹션에서는 달력을 통해 날짜를 선택 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="999a6-150">JQuery UI를 사용 하려면 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="999a6-151">**주스 ui** NuGet 패키지를 사용 하면 JQuery ui 위젯을 웹 응용 프로그램에 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="999a6-152">이 패키지를 사용 하려면 NuGet을 통해 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-152">To use this package, install it through NuGet.</span></span>

![주스 UI 추가](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="999a6-154">설치한 주스 UI 버전이 응용 프로그램의 JQuery 버전과 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="999a6-155">이 자습서를 진행 하기 전에 응용 프로그램을 실행 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="999a6-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="999a6-156">JavaScript 오류가 발생 하면 JQuery 버전을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="999a6-157">필요한 JQuery 버전을 Scripts 폴더에 추가할 수 있습니다 (이 자습서를 작성할 때 버전 1.8.2). 또는 site.master에서 JQuery 파일의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="999a6-158">Datepicker 위젯을 포함 하도록 DateTime 템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="999a6-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="999a6-159">Datetime 값을 편집 하기 위해 동적 데이터 템플릿에 Datepicker 위젯을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="999a6-160">템플릿에 위젯을 추가 하면 새 학생을 추가 하기 위한 양식과 학생 편집을 위한 그리드 보기에서 자동으로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="999a6-161">**날짜/시간\_** 을 열고 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="999a6-162">코드 숨김이 있는 파일에서는 DatePicker에 대 한 최소 및 최대 날짜를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="999a6-163">이러한 값을 설정 하 여 사용자가 잘못 된 날짜로 이동 하는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="999a6-164">DateTime 속성의 범위 **특성** (제공 된 경우)에 대 한 최소값과 최대값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="999a6-165">**DateTime\_Edit.ascx.cs**를 열고 페이지\_Load 메서드에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="999a6-166">웹 응용 프로그램을 실행 하 고 AddStudent 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="999a6-167">필드에 대 한 값을 제공 합니다. 등록 날짜에 대 한 텍스트 상자를 클릭 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![날짜 선택](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="999a6-169">날짜를 선택 하 고 **삽입**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="999a6-170">범위 특성은 서버에 대 한 유효성 검사를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="999a6-171">Datepicker에 minDate 속성을 설정 하 여 클라이언트에서 유효성 검사도 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="999a6-172">달력을 사용 하면 사용자가 minDate 값 이전 날짜로 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="999a6-173">그리드 보기에서 레코드를 편집 하는 경우에도 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView의 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="999a6-175">결론</span><span class="sxs-lookup"><span data-stu-id="999a6-175">Conclusion</span></span>

<span data-ttu-id="999a6-176">이 자습서에서는 모델 바인딩을 사용 하는 웹 폼에 JQuery 위젯을 통합 하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="999a6-177">다음 [자습서](using-query-string-values-to-retrieve-data.md)에서는 데이터를 선택 하는 경우 쿼리 문자열 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="999a6-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="999a6-178">[이전](sorting-paging-and-filtering-data.md)
> [다음](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="999a6-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
