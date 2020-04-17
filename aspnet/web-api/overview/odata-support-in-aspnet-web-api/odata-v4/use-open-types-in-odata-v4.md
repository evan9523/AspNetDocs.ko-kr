---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET 웹 API가 있는 OData v4의 오픈 형식 | 마이크로 소프트 문서
author: rick-anderson
description: OData v4에서 open 형식은 형식 정의에 선언된 모든 속성 외에 동적 속성을 포함하는 구조화된 형식입니다. 열기...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543732"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="c27a3-104">ASP.NET 웹 API를 사용하여 OData v4에서 열린 형식</span><span class="sxs-lookup"><span data-stu-id="c27a3-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="c27a3-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c27a3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c27a3-106">OData v4에서 *open 형식은* 형식 정의에 선언된 모든 속성 외에 동적 속성을 포함하는 구조화된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="c27a3-107">개방형 형식을 사용하면 데이터 모델에 유연성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="c27a3-108">이 자습서에서는 ASP.NET 웹 API OData에서 열린 형식을 사용하는 방법을 보여 주입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="c27a3-109">이 자습서에서는 웹 API에서 OData 끝점을 만드는 방법을 이미 알고 ASP.NET 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="c27a3-110">그렇지 않은 경우 먼저 [OData v4 끝점 만들기를](create-an-odata-v4-endpoint.md) 읽는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c27a3-111">튜토리얼에 사용되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c27a3-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c27a3-112">웹 API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="c27a3-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="c27a3-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="c27a3-113">OData v4</span></span>

<span data-ttu-id="c27a3-114">첫째, 일부 OData 용어:</span><span class="sxs-lookup"><span data-stu-id="c27a3-114">First, some OData terminology:</span></span>

- <span data-ttu-id="c27a3-115">엔터티 유형: 키가 있는 구조화 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="c27a3-116">복합 유형: 키가 없는 구조식 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="c27a3-117">열기 유형: 동적 속성이 있는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="c27a3-118">엔터티 형식과 복잡한 형식을 모두 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="c27a3-119">동적 속성의 값은 기본 형식, 복합 형식 또는 열거형 형식일 수 있습니다. 또는 이러한 유형의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="c27a3-120">열려 있는 형식에 대한 자세한 내용은 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c27a3-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="c27a3-121">웹 OData 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="c27a3-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="c27a3-122">NuGet 패키지 관리자를 사용하여 최신 웹 API OData 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="c27a3-123">패키지 관리자 콘솔 창에서:</span><span class="sxs-lookup"><span data-stu-id="c27a3-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="c27a3-124">CLR 유형 정의</span><span class="sxs-lookup"><span data-stu-id="c27a3-124">Define the CLR Types</span></span>

<span data-ttu-id="c27a3-125">먼저 EDM 모델을 CLR 유형으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="c27a3-126">EDM(엔터티 데이터 모델)이 생성되면</span><span class="sxs-lookup"><span data-stu-id="c27a3-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="c27a3-127">`Category`은 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="c27a3-128">`Address`는 복잡한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-128">`Address` is a complex type.</span></span> <span data-ttu-id="c27a3-129">(키가 없으므로 엔터티 형식이 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="c27a3-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="c27a3-130">`Customer`는 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-130">`Customer` is an entity type.</span></span> <span data-ttu-id="c27a3-131">(열쇠가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="c27a3-131">(It has a key.)</span></span>
- <span data-ttu-id="c27a3-132">`Press`는 개방형 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="c27a3-133">`Book`는 열린 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="c27a3-134">열린 형식을 만들려면 CLR 형식에는 동적 속성을 `IDictionary<string, object>`포함하는 형식의 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="c27a3-135">EDM 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="c27a3-135">Build the EDM Model</span></span>

<span data-ttu-id="c27a3-136">**ODataConventionModelBuilder를** 사용하여 EDM을 `Press` 만드는 `Book` 경우 `IDictionary<string, object>` 속성의 존재에 따라 개방형 유형으로 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="c27a3-137">**ODataModelBuilder를**사용하여 EDM을 명시적으로 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="c27a3-138">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="c27a3-138">Add an OData Controller</span></span>

<span data-ttu-id="c27a3-139">다음으로 OData 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-139">Next, add an OData controller.</span></span> <span data-ttu-id="c27a3-140">이 자습서에서는 GET 및 POST 요청만 지원하고 메모리 내 목록을 사용하여 엔터티를 저장하는 단순화된 컨트롤러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="c27a3-141">첫 번째 `Book` 인스턴스에는 동적 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="c27a3-142">두 `Book` 번째 인스턴스에는 다음과 같은 동적 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="c27a3-143">"게시됨": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="c27a3-143">"Published": Primitive type</span></span>
- <span data-ttu-id="c27a3-144">"작성자": 기본 형식의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c27a3-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="c27a3-145">"기타 범주": 열거형 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="c27a3-146">또한 해당 `Press` `Book` 인스턴스의 속성에는 다음과 같은 동적 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="c27a3-147">"블로그": 원시 형식</span><span class="sxs-lookup"><span data-stu-id="c27a3-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="c27a3-148">"주소": 복잡한 유형</span><span class="sxs-lookup"><span data-stu-id="c27a3-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="c27a3-149">메타데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="c27a3-149">Query the Metadata</span></span>

<span data-ttu-id="c27a3-150">OData 메타데이터 문서를 받으려면 GET `~/$metadata`요청을 로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="c27a3-151">응답 본문은 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="c27a3-152">메타데이터 문서에서 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="c27a3-153">`Book` 및 `Press` 형식의 경우 `OpenType` 특성값은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="c27a3-154">`Customer` 및 `Address` 형식에는 이 특성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="c27a3-155">`Book` 엔터티 유형에는 ISBN, 제목 및 Press의 세 가지 선언된 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="c27a3-156">OData 메타데이터에는 CLR 클래스의 `Book.Properties` 속성이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="c27a3-157">마찬가지로 `Press` 복합 형식에는 이름과 범주라는 두 개의 선언된 속성만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="c27a3-158">메타데이터에는 CLR `Press.DynamicProperties` 클래스의 속성이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="c27a3-159">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="c27a3-159">Query an Entity</span></span>

<span data-ttu-id="c27a3-160">ISBN이 "978-0-7356-7942-9"와 동일한 책을 얻으려면 GET 요청을 `~/Books('978-0-7356-7942-9')`로 보내십시오.</span><span class="sxs-lookup"><span data-stu-id="c27a3-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="c27a3-161">응답 본문은 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-161">The response body should look similar to the following.</span></span> <span data-ttu-id="c27a3-162">(더 읽기 쉽게 하기 위해 들여쓰기됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c27a3-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="c27a3-163">동적 속성은 선언된 속성과 인라인으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="c27a3-164">엔터티 게시</span><span class="sxs-lookup"><span data-stu-id="c27a3-164">POST an Entity</span></span>

<span data-ttu-id="c27a3-165">Book 엔터티를 추가하려면 에 POST `~/Books`요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="c27a3-166">클라이언트는 요청 페이로드에서 동적 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="c27a3-167">다음은 예제 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-167">Here is an example request.</span></span> <span data-ttu-id="c27a3-168">"가격" 및 "게시된" 속성을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="c27a3-169">컨트롤러 메서드에서 중단점을 설정하면 Web API가 `Properties` 이러한 속성을 사전에 추가한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c27a3-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="c27a3-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c27a3-170">Additional Resources</span></span>

[<span data-ttu-id="c27a3-171">OData 오픈 타입 샘플</span><span class="sxs-lookup"><span data-stu-id="c27a3-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
