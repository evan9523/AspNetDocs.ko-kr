---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamic v. 강력한 형식의 뷰 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702948"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="830cd-103">Dynamic v.</span><span class="sxs-lookup"><span data-stu-id="830cd-103">Dynamic v.</span></span> <span data-ttu-id="830cd-104">강력한 형식의 보기</span><span class="sxs-lookup"><span data-stu-id="830cd-104">Strongly Typed Views</span></span>

<span data-ttu-id="830cd-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="830cd-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="830cd-106">다음 세 가지 방법으로 컨트롤러에서 ASP.NET MVC 3의 뷰로 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="830cd-107">강력한 형식의 모델 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="830cd-108">동적 형식 ( @model 동적 사용)</span><span class="sxs-lookup"><span data-stu-id="830cd-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="830cd-109">ViewBag 사용</span><span class="sxs-lookup"><span data-stu-id="830cd-109">Using the ViewBag</span></span>

<span data-ttu-id="830cd-110">동적 및 강력한 형식의 뷰를 비교 하 고 대조 하는 간단한 MVC 3 최상위 블로그 응용 프로그램을 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="830cd-111">컨트롤러는 간단한 블로그 목록으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="830cd-112">IndexNotStonglyTyped 된 () 메서드를 마우스 오른쪽 단추로 클릭 하 고 Razor 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="830cd-113">[![8475 NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="830cd-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="830cd-114">**강력한 형식의 뷰 만들기** 상자가 선택 되어 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="830cd-115">결과 보기에는 많은 정보가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="830cd-116">강력한 형식의 뷰가 아닌 동적을 사용 하기 때문에 intellisense는 유용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="830cd-117">완성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="830cd-118">[![6646 [1] NotStronglyTypedView_5F00_IE](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="830cd-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="830cd-119">이제 강력한 형식의 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="830cd-120">컨트롤러에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="830cd-121">정확 하 게 동일한 반환 뷰 (topBlogs)를 확인 합니다. 를 비 강력한 형식의 뷰로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="830cd-122">*StonglyTypedIndex ()* 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="830cd-123">이번에는 **블로그** 모델 클래스를 선택 하 고 스 캐 폴드 템플릿으로 **목록** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="830cd-124">[![5658 StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="830cd-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="830cd-125">새 보기 템플릿 내에서 intellisense 지원을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="830cd-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="830cd-126">[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="830cd-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>
