---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6 부: 모델 유효성 검사에 데이터 주석 사용 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 6 부에서는 모델 V에 대 한 데이터 주석을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044950"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="66075-104">6부: 모델 유효성 검사에 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="66075-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="66075-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="66075-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="66075-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="66075-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="66075-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="66075-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="66075-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="66075-109">6 부에서는 모델 유효성 검사에 대 한 데이터 주석을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="66075-110">만들기 및 편집 양식에는 중요 한 문제가 있습니다. 즉, 유효성 검사를 수행 하 고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="66075-111">필수 필드를 비워 두거나 Price 필드에 문자를 입력 하는 등의 작업을 수행할 수 있으며, 첫 번째 오류는 데이터베이스에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="66075-112">모델 클래스에 데이터 주석을 추가 하 여 응용 프로그램에 유효성 검사를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="66075-113">데이터 주석을 사용 하면 모델 속성에 적용 하려는 규칙을 설명할 수 있으며, ASP.NET MVC는 이러한 규칙을 적용 하 고 사용자에 게 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="66075-114">앨범 폼에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="66075-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="66075-115">다음 데이터 주석 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="66075-116">**필수** – 속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66075-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="66075-117">**DisplayName** – 양식 필드 및 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-117">**DisplayName** – Defines the text to use on form fields and validation messages</span></span>
- <span data-ttu-id="66075-118">**Stringlength** – 문자열 필드의 최대 길이를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="66075-119">**범위** – 숫자 필드에 대 한 최대값 및 최소값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="66075-120">**Bind** – 모델 속성에 매개 변수 또는 폼 값을 바인딩할 때 제외 하거나 포함할 필드를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="66075-121">**ScaffoldColumn** – 편집기 양식에서 필드를 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="66075-122">*참고: 데이터 주석 특성을 사용한 모델 유효성 검사에 대 한 자세한 내용은 MSDN 설명서를 참조 하십시오.*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="66075-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="66075-123">앨범 클래스를 열고 맨 위에 다음 *using* 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="66075-124">다음으로 속성을 업데이트 하 여 아래와 같이 표시 및 유효성 검사 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="66075-125">여기서 장르 및 음악가도 가상 속성으로 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="66075-126">이렇게 하면 Entity Framework 필요에 따라 지연 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="66075-127">이러한 특성을 앨범 모델에 추가한 후에는 만들기 및 편집 화면에서 즉시 필드의 유효성 검사를 시작 하 고 선택한 표시 이름 (예: AlbumArtUrl 대신 앨범 아트 Url)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="66075-128">응용 프로그램을 실행 하 고/StoreManager/Create.로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="66075-129">다음에는 일부 유효성 검사 규칙을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="66075-130">0의 가격을 입력 하 고 제목을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="66075-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="66075-131">만들기 단추를 클릭 하면 정의 된 유효성 검사 규칙을 충족 하지 않는 필드를 표시 하는 유효성 검사 오류 메시지와 함께 표시 되는 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66075-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="66075-132">클라이언트 쪽 유효성 검사 테스트</span><span class="sxs-lookup"><span data-stu-id="66075-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="66075-133">사용자가 클라이언트 쪽 유효성 검사를 피할 수 있으므로 서버 쪽 유효성 검사는 응용 프로그램 관점에서 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="66075-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="66075-134">그러나 서버 쪽 유효성 검사를 구현 하는 웹 페이지 양식에는 세 가지 중요 한 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="66075-135">사용자는 폼이 게시 되 고 서버에서 유효성 검사가 수행 될 때까지 대기 하 고 해당 브라우저에 응답을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="66075-136">사용자는 필드를 수정 하 여 유효성 검사 규칙을 전달 하는 즉시 피드백을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="66075-137">사용자의 브라우저를 활용 하는 대신 유효성 검사 논리를 수행 하도록 서버 리소스를 낭비 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="66075-138">다행히 ASP.NET MVC 3 스 캐 폴드 템플릿은 클라이언트 쪽 유효성 검사를 기본 제공 하므로 추가 작업이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66075-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="66075-139">제목 필드에 한 문자를 입력 하면 유효성 검사 요구 사항이 충족 되므로 유효성 검사 메시지는 즉시 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66075-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="66075-140">[이전](mvc-music-store-part-5.md)
> [다음](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="66075-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
