---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 모델 바인딩 및 web forms를 사용 하 여 JQuery UI Datepicker 통합 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: ff1b17295c58d40d55bdcd4346b83121b579bb4c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030960"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="a4677-104">모델 바인딩 및 web forms를 사용 하 여 JQuery UI Datepicker 통합</span><span class="sxs-lookup"><span data-stu-id="a4677-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>
====================
<span data-ttu-id="a4677-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a4677-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a4677-106">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="a4677-107">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="a4677-108">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="a4677-109">이 자습서에서는 JQuery UI를 추가 하는 방법을 보여 줍니다 [Datepicker 위젯](http://jqueryui.com/datepicker/) Web Form을 사용 하 여 모델을 선택한 값을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="a4677-110">이 자습서에서 만든 프로젝트를 기반 합니다 [첫 번째](retrieving-data.md) 하 고 [두 번째](updating-deleting-and-creating-data.md) 시리즈의 파트입니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="a4677-111">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="a4677-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="a4677-112">다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="a4677-113">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="a4677-114">만들 내용</span><span class="sxs-lookup"><span data-stu-id="a4677-114">What you'll build</span></span>

<span data-ttu-id="a4677-115">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="a4677-116">학생 등록 날짜를 기록 하기 위해 모델에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="a4677-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="a4677-117">JQuery UI Datepicker 위젯을 사용 하 여 등록 날짜를 선택 하려면 사용자를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a4677-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="a4677-118">등록 날짜에 대 한 유효성 검사 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="a4677-119">JQuery UI Datepicker 위젯을 사용 하면 쉽게 필드와 상호 작용할 때 표시 되는 달력에서 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="a4677-120">이 위젯을 사용 하 여 수동으로 날짜를 입력 하는 보다 사용자에 대 한 더 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="a4677-121">데이터 작업에 대 한 모델 바인딩을 사용 하는 페이지 Datepicker 위젯 통합 적은 양의 추가 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="a4677-122">모델에 새 속성 추가</span><span class="sxs-lookup"><span data-stu-id="a4677-122">Add a new property to the model</span></span>

<span data-ttu-id="a4677-123">먼저 추가 합니다는 **날짜/시간** 속성에 학생을 모델링 하 고 해당 변경 내용을 데이터베이스에 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="a4677-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="a4677-124">오픈 **UniversityModels.cs**, 학생 모델을 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="a4677-125">합니다 **RangeAttribute** 속성에 대 한 유효성 검사 규칙을 적용 하기 위해 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="a4677-126">이 자습서에서는 Contoso University는 2013 년 1 월 1 일 년에 설립 된 이전 등록 날짜가 유효 하지 않습니다 고 가정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="a4677-127">패키지 관리 창에서 명령을 실행 하 여 마이그레이션을 추가 **추가 마이그레이션 AddEnrollmentDate**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="a4677-128">마이그레이션 코드 Student 테이블에 새 날짜/시간 열을 추가 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="a4677-129">RangeAttribute에서 지정 된 값에 맞게, 아래 강조 표시 된 코드에 표시 된 대로 새 열에 대 한 기본값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="a4677-130">마이그레이션 파일에 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-130">Save your change to the migration file.</span></span>

<span data-ttu-id="a4677-131">데이터를 다시 시드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-131">You do not need to seed the data again.</span></span> <span data-ttu-id="a4677-132">따라서 엽니다 **Configuration.cs** 마이그레이션 폴더에 제거 하거나에서 코드를 주석 처리 합니다 **초기값** 메서드.</span><span class="sxs-lookup"><span data-stu-id="a4677-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="a4677-133">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-133">Save and close the file.</span></span>

<span data-ttu-id="a4677-134">이제 명령을 **데이터베이스 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="a4677-135">이제 데이터베이스 열에 있는 EnrollmentDate에 대 한 기본값을 갖는 모든 기존 레코드에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a4677-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="a4677-136">등록 날짜에 대 한 동적 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="a4677-137">이제 표시 하 고 등록 날짜 편집에 대 한 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="a4677-138">이 시점에서 텍스트 상자를 통해 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="a4677-139">자습서의 뒷부분에 나오는 JQuery Datepicker 위젯에 입력란을 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="a4677-140">먼저 것이를 변경할 필요가 없습니다 명심 해야 합니다 **AddStudent.aspx** 파일.</span><span class="sxs-lookup"><span data-stu-id="a4677-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="a4677-141">DynamicEntity 컨트롤 새 속성을 자동으로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="a4677-142">오픈 **Students.aspx**를 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="a4677-143">응용 프로그램을 실행 하 고 날짜를 입력 하 여 등록 날짜의 값을 설정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="a4677-144">새 학생을 추가 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="a4677-144">When adding a new student:</span></span>

![설정된 된 날짜](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="a4677-146">또는 기존 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-146">Or, editing an existing value:</span></span>

![날짜 편집](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="a4677-148">입력 날짜 작동 하지만 고객 환경을 제공 하려는 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="a4677-149">다음 섹션에서는 달력을 통해 날짜를 선택 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="a4677-150">JQuery UI를 사용 하려면 NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="a4677-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="a4677-151">합니다 **쥬 스 잔 UI** NuGet 패키지에는 웹 응용 프로그램에 JQuery UI 위젯 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="a4677-152">이 패키지를 사용 하려면 NuGet을 통해 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-152">To use this package, install it through NuGet.</span></span>

![쥬 스 잔 UI 추가](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="a4677-154">버전을 설치 하는 쥬 스 잔 UI 응용 프로그램에서 JQuery 버전이 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="a4677-155">이 자습서를 진행 하기 전에 응용 프로그램을 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="a4677-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="a4677-156">JavaScript 오류가 발생 하는 경우에 JQuery 버전을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="a4677-157">JQuery의 예상된 버전 (버전 1.8.2이이 자습서를 작성 시), 스크립트 폴더에 추가 하거나 Site.master에서 JQuery 파일의 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="a4677-158">Datepicker 위젯을 포함할 DateTime 템플릿을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a4677-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="a4677-159">날짜/시간 값을 편집 하는 것에 대 한 동적 데이터 템플릿과 Datepicker 위젯을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="a4677-160">위젯 템플릿에 추가 하 여 두 폼에 새 학생을 추가 및 편집 학생용 그리드 보기에서 자동으로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="a4677-161">오픈 **날짜/시간\_Edit.ascx**를 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="a4677-162">코드 숨김 파일에서 DatePicker에 대 한 최소 및 최대 날짜를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="a4677-163">이러한 값을 설정 하 여 잘못 된 날짜를 이동할 수 없도록 사용자를 못합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="a4677-164">최소 및 최대 값을 검색 합니다는 **RangeAttribute** 제공 되는 경우 날짜/시간 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="a4677-165">오픈 **날짜/시간\_Edit.ascx.cs**, 다음 강조 표시 된 코드 페이지를 추가 하 고\_메서드를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="a4677-166">웹 응용 프로그램을 실행 하 고 AddStudent 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="a4677-167">필드에 대 한 값을 제공 하 고 등록 날짜에 대 한 텍스트 상자에서 클릭 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![날짜 선택](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="a4677-169">날짜를 선택 하 고 클릭 **삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="a4677-170">RangeAttribute 서버의 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="a4677-171">Datepicker에 minDate 속성을 설정 하 여도 클라이언트에서 유효성 검사를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="a4677-172">달력 사용자 minDate 변수의 이전 날짜를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="a4677-173">그리드 보기에서 레코드를 편집할 때 달력도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView의 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="a4677-175">결론</span><span class="sxs-lookup"><span data-stu-id="a4677-175">Conclusion</span></span>

<span data-ttu-id="a4677-176">이 자습서에서는 JQuery 위젯 모델 바인딩을 사용 하는 web form을 통합 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="a4677-177">다음에 [자습서](using-query-string-values-to-retrieve-data.md), 데이터를 선택할 때 쿼리 문자열 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4677-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4677-178">[이전](sorting-paging-and-filtering-data.md)
> [다음](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="a4677-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
