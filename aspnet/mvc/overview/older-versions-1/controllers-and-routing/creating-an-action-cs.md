---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 액션 만들기(C#) | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET MVC 컨트롤러에 새 작업을 추가하는 방법에 대해 알아봅니다. 메서드가 작업으로 수행되는 데 대한 요구 사항에 대해 알아봅니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542276"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="badf6-104">작업 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="badf6-104">Creating an Action (C#)</span></span>

<span data-ttu-id="badf6-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="badf6-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="badf6-106">ASP.NET MVC 컨트롤러에 새 작업을 추가하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="badf6-107">메서드가 작업으로 수행되는 데 대한 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="badf6-108">이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="badf6-109">작업 메서드의 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="badf6-110">메서드가 작업으로 노출되는 것을 방지하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="badf6-111">컨트롤러에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="badf6-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="badf6-112">컨트롤러에 새 메서드를 추가하여 컨트롤러에 새 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="badf6-113">예를 들어 목록 1의 컨트롤러에는 Index()라는 작업과 SayHello()라는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="badf6-114">두 메서드 모두 작업으로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="badf6-115">**목록 1 - 컨트롤러\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="badf6-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="badf6-116">행동으로 우주에 노출되기 위해, 방법은 특정 요구 사항을 충족해야합니다 :</span><span class="sxs-lookup"><span data-stu-id="badf6-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="badf6-117">메서드는 공용이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-117">The method must be public.</span></span>
- <span data-ttu-id="badf6-118">메서드는 정적 메서드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="badf6-119">메서드는 확장 메서드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="badf6-120">메서드는 생성자, 게터 또는 setter가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="badf6-121">메서드에 열려 있는 제네릭 형식을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="badf6-122">메서드는 컨트롤러 기본 클래스의 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="badf6-123">메서드는 **ref** 또는 **out** 매개 변수를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="badf6-124">컨트롤러 작업의 반환 유형에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="badf6-125">컨트롤러 작업은 문자열, DateTime, Random 클래스의 인스턴스 또는 void를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="badf6-126">ASP.NET MVC 프레임워크는 작업 결과가 아닌 반환 형식을 문자열로 변환하고 문자열을 브라우저로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="badf6-127">이러한 요구 사항을 위반하지 않는 메서드를 컨트롤러에 추가하면 메서드가 컨트롤러 작업으로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="badf6-128">여기에주의하십시오.</span><span class="sxs-lookup"><span data-stu-id="badf6-128">Be careful here.</span></span> <span data-ttu-id="badf6-129">인터넷에 연결된 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="badf6-130">예를 들어 DeleteMyWebsite() 컨트롤러 작업을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="badf6-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="badf6-131">공용 메서드가 호출되지 않도록 방지</span><span class="sxs-lookup"><span data-stu-id="badf6-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="badf6-132">컨트롤러 클래스에서 공용 메서드를 만들어야 하고 메서드를 컨트롤러 작업으로 노출하지 않으려면 [NonAction] 특성을 사용하여 메서드가 호출되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="badf6-133">예를 들어 목록 2의 컨트롤러에는 [NonAction] 특성으로 장식된 CompanySecrets()라는 공용 메서드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="badf6-134">**목록 2 - 컨트롤러\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="badf6-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="badf6-135">브라우저의 주소 표시줄에 /Work/CompanySecrets를 입력하여 CompanySecrets() 컨트롤러 작업을 호출하려고 하면 그림 1의 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="badf6-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="badf6-136">[![비동작 메서드 호출](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="badf6-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="badf6-137">**그림 01**: 비동작 메서드[호출(전체 크기 이미지를 보려면 클릭)](creating-an-action-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="badf6-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="badf6-138">[이전](creating-a-controller-cs.md)
> [다음](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
