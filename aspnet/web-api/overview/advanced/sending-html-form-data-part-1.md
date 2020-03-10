---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API에서 HTML 양식 데이터 보내기: x-www-form-urlencoded Data-ASP.NET 4.x'
author: MikeWasson
description: 이 문서에서는 ASP.NET 4.x를 사용 하 여 Web API 컨트롤러에 양식 x-www-form-urlencoded 데이터를 게시 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449243"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="02cae-103">ASP.NET Web API에서 HTML 양식 데이터 보내기: 양식 x-www-form-urlencoded 데이터</span><span class="sxs-lookup"><span data-stu-id="02cae-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="02cae-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="02cae-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="02cae-105">1 부: 양식 x-www-form-urlencoded 데이터</span><span class="sxs-lookup"><span data-stu-id="02cae-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="02cae-106">이 문서에서는 Web API 컨트롤러에 양식-x-www-form-urlencoded 데이터를 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="02cae-107">HTML 양식 개요</span><span class="sxs-lookup"><span data-stu-id="02cae-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="02cae-108">복합 형식 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="02cae-109">AJAX를 통해 폼 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="02cae-110">단순 형식 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="02cae-111">[완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="02cae-112">HTML 양식 개요</span><span class="sxs-lookup"><span data-stu-id="02cae-112">Overview of HTML Forms</span></span>

<span data-ttu-id="02cae-113">HTML 양식은 GET 또는 POST를 사용 하 여 서버에 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="02cae-114">**Form** 요소의 **METHOD** 특성은 HTTP 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="02cae-115">기본 메서드는 GET입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-115">The default method is GET.</span></span> <span data-ttu-id="02cae-116">폼에서 GET을 사용 하는 경우 양식 데이터는 URI에서 쿼리 문자열로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="02cae-117">폼에서 POST를 사용 하는 경우 양식 데이터가 요청 본문에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="02cae-118">게시 된 데이터의 경우 **enctype** 특성은 요청 본문의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="02cae-119">enctype</span><span class="sxs-lookup"><span data-stu-id="02cae-119">enctype</span></span> | <span data-ttu-id="02cae-120">Description</span><span class="sxs-lookup"><span data-stu-id="02cae-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02cae-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="02cae-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="02cae-122">양식 데이터는 URI 쿼리 문자열과 비슷하게 이름/값 쌍으로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="02cae-123">POST에 대 한 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="02cae-124">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="02cae-124">multipart/form-data</span></span> | <span data-ttu-id="02cae-125">양식 데이터는 다중 파트 MIME 메시지로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="02cae-126">서버에 파일을 업로드 하는 경우이 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="02cae-127">이 문서의 1 부에서는 x-www-form-urlencoded 형식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="02cae-128">[2 부](sending-html-form-data-part-2.md) 에서는 다중 부분 MIME을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="02cae-129">복합 형식 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-129">Sending Complex Types</span></span>

<span data-ttu-id="02cae-130">일반적으로 여러 양식 컨트롤에서 가져온 값으로 구성 되는 복합 형식을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="02cae-131">상태 업데이트를 나타내는 다음 모델을 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02cae-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="02cae-132">다음은 POST를 통해 `Update` 개체를 수락 하는 Web API 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="02cae-133">이 컨트롤러는 [작업 기반 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)사용 하므로 경로 템플릿은 api/{controller}/{action}/{id}&quot;&quot;됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="02cae-134">클라이언트는 &quot;/api/updates/complex&quot;에 데이터를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="02cae-135">이제 사용자가 상태 업데이트를 제출 하는 HTML 양식을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="02cae-136">폼의 **action** 특성은 컨트롤러 작업의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="02cae-137">다음은에 입력 된 일부 값이 있는 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="02cae-138">사용자가 제출을 클릭 하면 브라우저에서 다음과 같은 HTTP 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="02cae-139">요청 본문에는 이름/값 쌍으로 형식이 지정 된 양식 데이터가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="02cae-140">Web API는 이름/값 쌍을 자동으로 `Update` 클래스의 인스턴스로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="02cae-141">AJAX를 통해 폼 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="02cae-142">사용자가 폼을 제출 하면 브라우저가 현재 페이지에서 벗어나 응답 메시지의 본문을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="02cae-143">응답이 HTML 페이지인 경우에는이 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="02cae-144">그러나 web API를 사용 하는 경우 응답 본문은 일반적으로 비어 있거나 JSON과 같은 구조화 된 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="02cae-145">이 경우 페이지에서 응답을 처리할 수 있도록 AJAX 요청을 사용 하 여 폼 데이터를 전송 하는 것이 더 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="02cae-146">다음 코드에서는 jQuery를 사용 하 여 폼 데이터를 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="02cae-147">JQuery **submit** 함수는 form 작업을 새 함수로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="02cae-148">이는 제출 단추의 기본 동작을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="02cae-149">**Serialize** 함수는 폼 데이터를 이름/값 쌍으로 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="02cae-150">서버에 폼 데이터를 전송 하려면 `$.post()`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="02cae-151">요청이 완료 되 면 `.success()` 또는 `.error()` 처리기가 사용자에 게 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="02cae-152">단순 형식 보내기</span><span class="sxs-lookup"><span data-stu-id="02cae-152">Sending Simple Types</span></span>

<span data-ttu-id="02cae-153">이전 섹션에서는 모델 클래스의 인스턴스로 deserialize 된 Web API를 복합 형식으로 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="02cae-154">문자열 등의 단순 형식을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="02cae-155">단순 형식을 보내기 전에 복합 형식의 값을 대신 래핑하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="02cae-156">이렇게 하면 서버 쪽에서 모델 유효성 검사의 이점을 얻을 수 있으며 필요한 경우 모델을 더 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="02cae-157">단순 유형을 전송 하는 기본 단계는 동일 하지만 두 가지 미묘한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="02cae-158">먼저 컨트롤러에서 **Frombody** 특성을 사용 하 여 매개 변수 이름을 데코레이팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="02cae-159">기본적으로 웹 API는 요청 URI에서 단순 형식을 가져오려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="02cae-160">**Frombody** 특성은 요청 본문에서 값을 읽도록 웹 API에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="02cae-161">Web API는 응답 본문을 한 번만 읽어서 요청 본문에서 동작의 매개 변수를 하나만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="02cae-162">요청 본문에서 여러 값을 가져와야 하는 경우에는 복합 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="02cae-163">둘째, 클라이언트는 다음 형식의 값을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="02cae-164">특히 이름/값 쌍의 이름 부분은 단순 형식에 대해 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="02cae-165">모든 브라우저에서 HTML 폼에 대해이 기능을 지원 하지는 않지만 다음과 같이 스크립트에서이 형식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="02cae-166">예제 폼은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="02cae-167">폼 값을 제출 하는 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="02cae-168">이전 스크립트의 유일한 차이점은 **post** 함수로 전달 되는 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="02cae-169">동일한 방법을 사용 하 여 단순 형식의 배열을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cae-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="02cae-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="02cae-170">Additional Resources</span></span>

[<span data-ttu-id="02cae-171">2 부: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="02cae-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
