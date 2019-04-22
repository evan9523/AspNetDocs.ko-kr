---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1-ASP.NET에서에서 BSON 지원 4.x
author: MikeWasson
description: ASP.NET 용.NET 클라이언트 앱 및 Web API 컨트롤러 (서버 쪽)에서 BSON을 사용 하는 방법을 보여 줍니다 4.x 합니다.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 911e2abcfd277075b3cba71e624ec6390b99a15e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59382233"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="140c0-103">ASP.NET Web API 2.1에서에서 BSON 지원</span><span class="sxs-lookup"><span data-stu-id="140c0-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="140c0-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="140c0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="140c0-105">이 항목에서는 Web API 컨트롤러 (서버 쪽) 및.NET 클라이언트 앱에서 BSON을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="140c0-106">Web API 2.1에서는 BSON 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="140c0-107">BSON 란?</span><span class="sxs-lookup"><span data-stu-id="140c0-107">What is BSON?</span></span>

<span data-ttu-id="140c0-108">[BSON](http://bsonspec.org/) 은 이진 serialization 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="140c0-109">"BSON"는 "이진 JSON"를 의미 하지만 BSON 및 JSON 매우 다른 방식으로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="140c0-110">BSON은 "JSON 유사한" 하므로 개체는 JSON과 유사한 이름-값 쌍으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="140c0-111">JSON에서와 달리 숫자 데이터 형식 문자열이 아니라 바이트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="140c0-112">BSON 가볍고, 검색이 용이 인코딩/디코딩 속도가 되도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="140c0-113">BSON은 JSON에 크기와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="140c0-114">데이터에 따라 BSON 페이로드는 JSON 페이로드 보다 작거나 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="140c0-115">이미지 파일과 같은 이진 데이터를 직렬화 하는 작업에 대 한 없기 때문에 이진 데이터가 base64로 인코딩된 BSON은 JSON 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="140c0-116">BSON 문서는 요소 길이 필드를 사용 하 여 접두사가 파서를 고를 디코딩하지 않고도 요소를 건너뛸 수 있도록 하기 때문에 스캔 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="140c0-117">인코딩 및 디코딩 되므로 효율적인 숫자 문자열이 아니라 숫자 데이터 형식이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="140c0-118">.NET 클라이언트 앱과 같은 네이티브 클라이언트에서 BSON을 사용 하 여 JSON 또는 XML과 같은 텍스트 기반 형식 대신 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="140c0-119">브라우저 클라이언트에는 아마도 JSON을 사용 하 있으므로 원하는 JavaScript JSON 페이로드에 직접 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="140c0-120">다행 스럽게도 Web API 사용 [콘텐츠 협상](content-negotiation.md)API 두 형식을 모두 지원 하 고 선택할 클라이언트 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="140c0-121">서버에서 BSON을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="140c0-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="140c0-122">Web API 구성에 추가 합니다 **BsonMediaTypeFormatter** 포맷터 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="140c0-123">이제 클라이언트는 "application/bson"을 요청 하는 경우 웹 API는 BSON 포맷터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="140c0-124">BSON 다른 미디어 유형을 연결할 SupportedMediaTypes 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="140c0-125">다음 코드는 지원 되는 미디어 유형으로 "application/vnd.contoso"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="140c0-126">예제에서는 HTTP 세션</span><span class="sxs-lookup"><span data-stu-id="140c0-126">Example HTTP Session</span></span>

<span data-ttu-id="140c0-127">이 예에서는 간단한 Web API 컨트롤러 및 다음 모델 클래스:</span><span class="sxs-lookup"><span data-stu-id="140c0-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="140c0-128">클라이언트는 다음 HTTP 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="140c0-129">응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="140c0-130">여기서 사용 하 여 이진 데이터를 바꿨습니다 &quot;.&quot; 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="140c0-131">다음 스크린 샷에서 원시 16 진수 값에서 Fiddler 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="140c0-132">HttpClient를 사용 하 여 BSON을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="140c0-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="140c0-133">.NET 클라이언트 앱에는 BSON 포맷터를 사용할 수 있습니다 **HttpClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="140c0-134">에 대 한 자세한 내용은 **HttpClient**를 참조 하세요 [웹 API에서는.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="140c0-135">다음 코드는 BSON을 받고 응답에서 BSON 페이로드 개체를 deserialize 하는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="140c0-136">서버에서 BSON을 요청 하려면 "application/bson" Accept 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="140c0-137">응답 본문을 deserialize 하는 데 사용 합니다 **BsonMediaTypeFormatter**합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="140c0-138">이 포맷터 아니므로 기본 포맷터 컬렉션에서 응답 본문을 읽을 때 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="140c0-139">다음 예제에서는 BSON을 포함 하는 POST 요청을 전송 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="140c0-140">이 코드의 대부분 이전 예제와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="140c0-141">하지만 합니다 **PostAsync** 메서드를 지정 **BsonMediaTypeFormatter** 포맷터로:</span><span class="sxs-lookup"><span data-stu-id="140c0-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="140c0-142">최상위 기본 형식 직렬화</span><span class="sxs-lookup"><span data-stu-id="140c0-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="140c0-143">모든 BSON 문서에는 키/값 쌍의 목록입니다. BSON 사양에는 정수나 문자열 같은 단일 원시 값을 직렬화 하는 작업에 대 한 구문을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="140c0-144">이 제한을 해결 하는 **BsonMediaTypeFormatter** 특별 한 경우 기본 형식 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="140c0-145">직렬화 하는 작업을 하기 전에 값을 변환 키/값 쌍을 키 "값"를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="140c0-146">예를 들어, API 컨트롤러는 정수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="140c0-147">직렬화 하는 작업을 하기 전에 BSON 포맷터 다음 키/값 쌍으로 변환:</span><span class="sxs-lookup"><span data-stu-id="140c0-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="140c0-148">Deserialize 할 때는 포맷터 원래 값으로 다시 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="140c0-149">그러나 다른 BSON 파서를 사용 하 여 클라이언트에 web API는 원시 값을 반환 하는 경우이 경우를 처리 하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="140c0-150">일반적으로 원시 값이 아니라 구조화 된 데이터를 반환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="140c0-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="140c0-151">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="140c0-151">Additional Resources</span></span>

[<span data-ttu-id="140c0-152">웹 API BSON 샘플</span><span class="sxs-lookup"><span data-stu-id="140c0-152">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="140c0-153">미디어 포맷터</span><span class="sxs-lookup"><span data-stu-id="140c0-153">Media Formatters</span></span>](media-formatters.md)
