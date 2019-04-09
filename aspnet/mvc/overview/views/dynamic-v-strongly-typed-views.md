---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamic v. Strongly Typed Views | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3235fc58fbf93cb87946f8ebd4a478eff7ce80e3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59386140"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="75ba7-103">Dynamic v.</span><span class="sxs-lookup"><span data-stu-id="75ba7-103">Dynamic v.</span></span> <span data-ttu-id="75ba7-104">강력한 형식의 보기</span><span class="sxs-lookup"><span data-stu-id="75ba7-104">Strongly Typed Views</span></span>

<span data-ttu-id="75ba7-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="75ba7-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="75ba7-106">ASP.NET MVC 3에서 뷰 컨트롤러에서 정보를 전달 하는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="75ba7-107">강력한 형식의 모델 개체로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="75ba7-108">동적 형식으로 (사용 하 여 @model 동적)</span><span class="sxs-lookup"><span data-stu-id="75ba7-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="75ba7-109">ViewBag을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="75ba7-109">Using the ViewBag</span></span>

<span data-ttu-id="75ba7-110">간단한 MVC 3 위 블로그 응용 프로그램을 비교 및 대조 동적이 고 강력한 형식의 뷰를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="75ba7-111">컨트롤러 시작 블로그 단순 목록:</span><span class="sxs-lookup"><span data-stu-id="75ba7-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="75ba7-112">IndexNotStonglyTyped() 메서드를 마우스 오른쪽 단추로 클릭 하 고 Razor 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

[![8<span data-ttu-id="75ba7-113">475.NotStronglyTypedView[1]]</span><span class="sxs-lookup"><span data-stu-id="75ba7-113">475.NotStronglyTypedView[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

<span data-ttu-id="75ba7-114">있는지 확인 합니다 **강력한 형식의 뷰를 만들** 선택 하지 않으면.</span><span class="sxs-lookup"><span data-stu-id="75ba7-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="75ba7-115">결과 뷰가 대부분 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="75ba7-116">동적 및 강력한 형식의 뷰가 아니라를 사용 하므로 intellisense는 데 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="75ba7-117">완료 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6<span data-ttu-id="75ba7-118">646.NotStronglyTypedView_5F00_IE[1]]</span><span class="sxs-lookup"><span data-stu-id="75ba7-118">646.NotStronglyTypedView_5F00_IE[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

<span data-ttu-id="75ba7-119">이제 강력한 형식의 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="75ba7-120">컨트롤러에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="75ba7-121">정확 하 게 된 동일한 반환 View(topBlogs);는 알 수 있습니다. 아닌 강력한 형식의 뷰를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="75ba7-122">내부에서 마우스 오른쪽 단추로 클릭 *StonglyTypedIndex()* 선택한 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="75ba7-123">이 시간을 선택 합니다 **블로그** 선택한 모델 클래스 **목록** 스 캐 폴드 템플릿으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

[![5<span data-ttu-id="75ba7-124">658.StrongView[1]]</span><span class="sxs-lookup"><span data-stu-id="75ba7-124">658.StrongView[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

<span data-ttu-id="75ba7-125">새 템플릿 보기 내에서 intellisense 지원을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-125">Inside the new view template we get intellisense support.</span></span>

[![7<span data-ttu-id="75ba7-126">002.IntelliSense[1]]</span><span class="sxs-lookup"><span data-stu-id="75ba7-126">002.IntelliSense[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

<span data-ttu-id="75ba7-127">C# 프로젝트를 다운로드할 수 있습니다 [여기](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba7-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
