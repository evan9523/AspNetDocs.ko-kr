---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2에서에서 작업의 결과 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/03/2014
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: b2b5ae5e5cef19e75a184aa28ac838a31e5ef1fd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061780"
---
<a name="action-results-in-web-api-2"></a><span data-ttu-id="6dc6d-102">Web API 2의 작업 결과</span><span class="sxs-lookup"><span data-stu-id="6dc6d-102">Action Results in Web API 2</span></span>
====================
<span data-ttu-id="6dc6d-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6dc6d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6dc6d-104">이 항목에서는 ASP.NET Web API HTTP 응답 메시지에 컨트롤러 작업에서 반환 값을 변환 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="6dc6d-105">Web API 컨트롤러 작업에는 다음 중 하나를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="6dc6d-106">void</span><span class="sxs-lookup"><span data-stu-id="6dc6d-106">void</span></span>
2. <span data-ttu-id="6dc6d-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="6dc6d-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="6dc6d-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="6dc6d-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="6dc6d-109">다른 형식</span><span class="sxs-lookup"><span data-stu-id="6dc6d-109">Some other type</span></span>

<span data-ttu-id="6dc6d-110">이 따라 반환 되 면 Web API 다른 메커니즘을 사용 하 여 HTTP 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="6dc6d-111">반환 형식</span><span class="sxs-lookup"><span data-stu-id="6dc6d-111">Return type</span></span> | <span data-ttu-id="6dc6d-112">Web API에서 응답을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="6dc6d-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="6dc6d-113">void</span><span class="sxs-lookup"><span data-stu-id="6dc6d-113">void</span></span> | <span data-ttu-id="6dc6d-114">빈 204 (내용 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="6dc6d-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="6dc6d-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="6dc6d-116">HTTP 응답 메시지에 직접 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="6dc6d-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="6dc6d-117">**IHttpActionResult**</span></span> | <span data-ttu-id="6dc6d-118">호출 **ExecuteAsync** 만들려는 **HttpResponseMessage**, 다음 HTTP 응답 메시지를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="6dc6d-119">다른 형식</span><span class="sxs-lookup"><span data-stu-id="6dc6d-119">Other type</span></span> | <span data-ttu-id="6dc6d-120">Serialize 된 반환 값을 응답 본문;에 쓰기 200 (정상)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="6dc6d-121">이 항목의 나머지 각 옵션을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="6dc6d-122">void</span><span class="sxs-lookup"><span data-stu-id="6dc6d-122">void</span></span>

<span data-ttu-id="6dc6d-123">반환 형식이 `void`, Web API에는 단순히 빈 HTTP 응답 상태 코드 204 (내용 없음)를 사용 하 여 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="6dc6d-124">예제에서는 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="6dc6d-125">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="6dc6d-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="6dc6d-126">HttpResponseMessage</span></span>

<span data-ttu-id="6dc6d-127">작업을 반환 하는 경우는 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API 반환 값으로 변환 합니다 직접 HTTP 응답 메시지의 속성을 사용 하는 **HttpResponseMessage** 채울 개체입니다는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="6dc6d-128">이 옵션은 많은 응답 메시지에 대 한 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="6dc6d-129">예를 들어 다음 컨트롤러 작업을 캐시 제어 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="6dc6d-130">응답:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="6dc6d-131">도메인 모델을 전달 하는 경우는 **CreateResponse** 메서드를 사용 하 여 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 응답 본문에 직렬화 된 모델을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="6dc6d-132">Web API 요청에 Accept 헤더를 사용 하 여 포맷터 선택.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="6dc6d-133">자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="6dc6d-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="6dc6d-134">IHttpActionResult</span></span>

<span data-ttu-id="6dc6d-135">합니다 **IHttpActionResult** 인터페이스는 Web API 2에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="6dc6d-136">기본적으로 정의 하는 **HttpResponseMessage** 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="6dc6d-137">사용 하는 몇 가지 이점은 다음과 같습니다 합니다 **IHttpActionResult** 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="6dc6d-138">간소화 [단위 테스트](../testing-and-debugging/unit-testing-controllers-in-web-api.md) 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="6dc6d-139">별도 클래스로 HTTP 응답을 만들기 위한 일반적인 논리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="6dc6d-140">응답 생성의 하위 수준 세부 정보를 숨겨 명확 하 게, 컨트롤러 작업의 의도를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="6dc6d-141">**IHttpActionResult** 단일 메서드를 포함 **ExecuteAsync**를 비동기적으로 만듭니다는 **HttpResponseMessage** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="6dc6d-142">컨트롤러 작업을 반환 하는 경우는 **IHttpActionResult**, Web API를 호출 합니다 **ExecuteAsync** 메서드를를 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="6dc6d-143">변환 후 합니다 **HttpResponseMessage** HTTP 응답 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="6dc6d-144">한 간단한 않아도 됨 다음과 같습니다 **IHttpActionResult** 를 만드는 일반 텍스트 응답:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-144">Here is a simple implementaton of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="6dc6d-145">예제에서는 컨트롤러 작업:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="6dc6d-146">응답:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="6dc6d-147">더 자주 사용 하 여 합니다 **IHttpActionResult** 구현에서 정의 합니다 **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-147">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="6dc6d-148">합니다 **ApiController** 클래스는 이러한 기본 제공 작업 결과 반환 하는 도우미 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="6dc6d-149">다음 예제에서는 요청에 기존 제품 ID가 일치 하지 않는 경우 컨트롤러 호출 [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 404 (찾을 수 없음) 응답을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="6dc6d-150">컨트롤러를 호출 하는 고, 그렇지 [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), 제품을 포함 하는 200 (정상) 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="6dc6d-151">다른 반환 형식</span><span class="sxs-lookup"><span data-stu-id="6dc6d-151">Other Return Types</span></span>

<span data-ttu-id="6dc6d-152">반환 다른 모든 형식에 대 한 웹 API에 사용 된 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 반환 값을 serialize 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="6dc6d-153">웹 API는 응답 본문에 serialize 된 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="6dc6d-154">응답 상태 코드는 200 (정상).</span><span class="sxs-lookup"><span data-stu-id="6dc6d-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="6dc6d-155">이 방식의 단점은 404와 같이 오류 코드를 직접 반환할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="6dc6d-156">그러나 throw 할 수 있습니다는 **HttpResponseException** 오류 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="6dc6d-157">자세한 내용은 [ASP.NET Web API의 예외 처리](../error-handling/exception-handling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="6dc6d-158">Web API 요청에 Accept 헤더를 사용 하 여 포맷터 선택.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="6dc6d-159">자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6d-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="6dc6d-160">요청 예제</span><span class="sxs-lookup"><span data-stu-id="6dc6d-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="6dc6d-161">예제 응답:</span><span class="sxs-lookup"><span data-stu-id="6dc6d-161">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
