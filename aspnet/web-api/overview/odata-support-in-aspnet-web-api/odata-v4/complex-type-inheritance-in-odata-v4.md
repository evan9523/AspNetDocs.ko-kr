---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET 웹 API를 사용하여 OData v4의 복잡한 형식 상속 | 마이크로 소프트 문서
author: rick-anderson
description: OData v4 사양에 따라 복소수 형식은 다른 복잡한 형식에서 상속할 수 있습니다. (복잡한 형식은 키가 없는 구조형입니다.) 웹 API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543602"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="eeed1-104">ASP.NET 웹 API를 사용하여 OData v4의 복잡한 형식 상속</span><span class="sxs-lookup"><span data-stu-id="eeed1-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="eeed1-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="eeed1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="eeed1-106">OData v4 [사양에](http://www.odata.org/documentation/odata-version-4-0/)따라 복소수 형식은 다른 복잡한 형식에서 상속될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="eeed1-107">(복잡한 *complex* 형식은 키가 없는 구조형입니다.) 웹 API OData 5.3은 복잡한 형식 상속을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="eeed1-108">이 항목에서는 복잡한 상속 형식을 사용하여 엔터티 데이터 모델(EDM)을 빌드하는 방법을 보여 주며 이 항목에서는</span><span class="sxs-lookup"><span data-stu-id="eeed1-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="eeed1-109">전체 소스 코드는 [OData 복합유형 상속 샘플을](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="eeed1-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="eeed1-110">튜토리얼에 사용되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="eeed1-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="eeed1-111">웹 API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="eeed1-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="eeed1-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="eeed1-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="eeed1-113">모델 계층 구조</span><span class="sxs-lookup"><span data-stu-id="eeed1-113">Model Hierarchy</span></span>

<span data-ttu-id="eeed1-114">복잡한 형식 상속을 설명하기 위해 다음 클래스 계층 구조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="eeed1-115">`Shape`는 추상 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="eeed1-116">`Rectangle``Circle` 및 `Triangle`에서 `Shape`파생된 복합 형식이며 `RoundRectangle` 에서 `Rectangle`파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="eeed1-117">`Window`은 엔터티 유형이며 `Shape` 인스턴스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="eeed1-118">다음은 이러한 형식을 정의하는 CLR 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="eeed1-119">EDM 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="eeed1-119">Build the EDM Model</span></span>

<span data-ttu-id="eeed1-120">EDM을 만들려면 CLR 형식의 상속 관계를 유추하는 **ODataConventionModelBuilder를**사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="eeed1-121">**ODataModelBuilder를**사용하여 EDM을 명시적으로 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="eeed1-122">이렇게 하면 더 많은 코드가 필요하지만 EDM을 보다 세한 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="eeed1-123">이 두 예제는 동일한 EDM 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="eeed1-124">메타데이터 문서</span><span class="sxs-lookup"><span data-stu-id="eeed1-124">Metadata Document</span></span>

<span data-ttu-id="eeed1-125">다음은 복잡한 형식 상속을 보여 줄 수 있는 OData 메타데이터 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="eeed1-126">메타데이터 문서에서 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="eeed1-127">복소수 형식은 `Shape` 추상적입니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="eeed1-128">및 `Rectangle` `Triangle` `Circle` 복합 형식에는 기본 형식이 `Shape`있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="eeed1-129">`RoundRectangle` 형식에는 기본 형식이 `Rectangle`있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="eeed1-130">주조 복합 유형</span><span class="sxs-lookup"><span data-stu-id="eeed1-130">Casting Complex Types</span></span>

<span data-ttu-id="eeed1-131">이제 복잡한 형식에 대한 캐스팅이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="eeed1-132">예를 들어 다음 쿼리는 `Shape` `Rectangle`a를 에 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="eeed1-133">응답 페이로드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eeed1-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
