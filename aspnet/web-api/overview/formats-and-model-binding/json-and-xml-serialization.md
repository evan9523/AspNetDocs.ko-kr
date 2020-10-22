---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API의 JSON 및 XML 직렬화-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x의 ASP.NET Web API에 있는 JSON 및 XML 포맷터에 대해 설명 합니다.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345169"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="15d15-103">ASP.NET Web API의 JSON 및 XML 직렬화</span><span class="sxs-lookup"><span data-stu-id="15d15-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="15d15-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="15d15-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="15d15-105">이 문서에서는 ASP.NET Web API의 JSON 및 XML 포맷터에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="15d15-106">ASP.NET Web API *미디어 형식 포맷터* 는 다음을 수행할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="15d15-107">HTTP 메시지 본문에서 CLR 개체 읽기</span><span class="sxs-lookup"><span data-stu-id="15d15-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="15d15-108">HTTP 메시지 본문에 CLR 개체를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="15d15-109">Web API는 JSON 및 XML에 대 한 미디어 유형 포맷터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="15d15-110">프레임 워크는 기본적으로 이러한 포맷터를 파이프라인에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="15d15-111">클라이언트는 HTTP 요청의 Accept 헤더에 JSON 또는 XML을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="15d15-112">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="15d15-112">Contents</span></span>

- [<span data-ttu-id="15d15-113">JSON Media-Type 포맷터</span><span class="sxs-lookup"><span data-stu-id="15d15-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="15d15-114">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="15d15-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="15d15-115">날짜</span><span class="sxs-lookup"><span data-stu-id="15d15-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="15d15-116">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="15d15-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="15d15-117">카멜식 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="15d15-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="15d15-118">익명 및 Weakly-Typed 개체</span><span class="sxs-lookup"><span data-stu-id="15d15-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="15d15-119">XML Media-Type 포맷터</span><span class="sxs-lookup"><span data-stu-id="15d15-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="15d15-120">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="15d15-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="15d15-121">날짜</span><span class="sxs-lookup"><span data-stu-id="15d15-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="15d15-122">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="15d15-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="15d15-123">XML Serializer Per-Type 설정</span><span class="sxs-lookup"><span data-stu-id="15d15-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="15d15-124">JSON 또는 XML 포맷터 제거</span><span class="sxs-lookup"><span data-stu-id="15d15-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="15d15-125">순환 개체 참조 처리</span><span class="sxs-lookup"><span data-stu-id="15d15-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="15d15-126">개체 Serialization 테스트</span><span class="sxs-lookup"><span data-stu-id="15d15-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="15d15-127">JSON Media-Type 포맷터</span><span class="sxs-lookup"><span data-stu-id="15d15-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="15d15-128">JSON 형식 지정은 **JsonMediaTypeFormatter** 클래스에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="15d15-129">기본적으로 **JsonMediaTypeFormatter** 는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 라이브러리를 사용 하 여 serialization을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="15d15-130">Json.NET는 타사 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="15d15-131">원하는 경우 Json.NET 대신 **DataContractJsonSerializer** 를 사용 하도록 **JsonMediaTypeFormatter** 클래스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="15d15-132">이렇게 하려면 **UseDataContractJsonSerializer** 속성을 **true**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="15d15-133">JSON serialization</span><span class="sxs-lookup"><span data-stu-id="15d15-133">JSON Serialization</span></span>

<span data-ttu-id="15d15-134">이 섹션에서는 기본 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer를 사용 하 여 JSON 포맷터의 몇 가지 특정 동작에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="15d15-135">이는 Json.NET 라이브러리의 포괄적인 설명서가 아닙니다. 자세한 내용은 [Json.NET 설명서](http://james.newtonking.com/projects/json/help/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="15d15-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="15d15-136">Serialize 되는 항목</span><span class="sxs-lookup"><span data-stu-id="15d15-136">What Gets Serialized?</span></span>

<span data-ttu-id="15d15-137">기본적으로 모든 public 속성 및 필드는 직렬화 된 JSON에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="15d15-138">속성 또는 필드를 생략 하려면 **JsonIgnore** 특성을 사용 하 여 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="15d15-139">&quot;옵트인 (opt in) 방식을 선호 하는 경우 &quot; 클래스를 **DataContract** 특성으로 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="15d15-140">이 특성이 있는 경우 멤버는 **DataMember**가 없는 한 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="15d15-141">또한 **DataMember** 를 사용 하 여 전용 멤버를 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="15d15-142">Read-Only 속성</span><span class="sxs-lookup"><span data-stu-id="15d15-142">Read-Only Properties</span></span>

<span data-ttu-id="15d15-143">읽기 전용 속성은 기본적으로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="15d15-144">날짜</span><span class="sxs-lookup"><span data-stu-id="15d15-144">Dates</span></span>

<span data-ttu-id="15d15-145">기본적으로 Json.NET는 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식으로 날짜를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="15d15-146">UTC (협정 세계시)의 날짜는 "Z" 접미사로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="15d15-147">현지 시간 날짜에는 표준 시간대 오프셋이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="15d15-148">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="15d15-149">기본적으로 Json.NET는 표준 시간대를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="15d15-150">DateTimeZoneHandling 속성을 설정 하 여이를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="15d15-151">ISO 8601 대신 [MICROSOFT JSON 날짜 형식](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ()을 사용 하려는 경우 `"\/Date(ticks)\/"` Serializer 설정에서 **DateFormatHandling** 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="15d15-152">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="15d15-152">Indenting</span></span>

<span data-ttu-id="15d15-153">들여쓰기 된 JSON을 작성 하려면 **서식** 설정을 서식으로 설정 **합니다. 들여쓰기**:</span><span class="sxs-lookup"><span data-stu-id="15d15-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="15d15-154">카멜식 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="15d15-154">Camel Casing</span></span>

<span data-ttu-id="15d15-155">데이터 모델을 변경 하지 않고 카멜식 대/소문자 구분을 사용 하 여 JSON 속성 이름을 쓰려면 serializer에서 **CamelCasePropertyNamesContractResolver** 를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="15d15-156">익명 및 Weakly-Typed 개체</span><span class="sxs-lookup"><span data-stu-id="15d15-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="15d15-157">작업 메서드는 익명 개체를 반환 하 고이를 JSON으로 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="15d15-158">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="15d15-159">응답 메시지 본문에는 다음 JSON이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="15d15-160">웹 API가 클라이언트에서 느슨하게 구조화 된 JSON 개체를 수신 하는 경우 요청 본문을의Newtonsoft.Jsdeserialize 할 수 있습니다 \*\* . Linq. JObject\*\* 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="15d15-161">그러나 강력한 형식의 데이터 개체를 사용 하는 것이 일반적으로 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="15d15-162">그런 다음 데이터를 직접 구문 분석할 필요가 없으며 모델 유효성 검사의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="15d15-163">XML serializer는 익명 형식 또는 **Jobject** 인스턴스를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="15d15-164">JSON 데이터에 이러한 기능을 사용 하는 경우이 문서의 뒷부분에서 설명 하는 대로 파이프라인에서 XML 포맷터를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="15d15-165">XML Media-Type 포맷터</span><span class="sxs-lookup"><span data-stu-id="15d15-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="15d15-166">XML 서식 지정은 **XmlMediaTypeFormatter** 클래스에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="15d15-167">기본적으로 **XmlMediaTypeFormatter** 는 **DataContractSerializer** 클래스를 사용 하 여 serialization을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="15d15-168">원하는 경우 **DataContractSerializer**대신 **XmlSerializer** 를 사용 하도록 **XmlMediaTypeFormatter** 를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="15d15-169">이렇게 하려면 **UseXmlSerializer** 속성을 **true**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="15d15-170">**XmlSerializer** 클래스는 **DataContractSerializer**보다 좁은 형식의 집합을 지원 하지만 결과 XML에 대 한 더 많은 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="15d15-171">기존 XML 스키마와 일치 해야 하는 경우 **XmlSerializer** 를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="15d15-172">XML Serialization</span><span class="sxs-lookup"><span data-stu-id="15d15-172">XML Serialization</span></span>

<span data-ttu-id="15d15-173">이 섹션에서는 기본 **DataContractSerializer**를 사용 하 여 XML 포맷터의 몇 가지 특정 동작에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="15d15-174">기본적으로 DataContractSerializer는 다음과 같이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="15d15-175">모든 public 읽기/쓰기 속성과 필드가 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="15d15-176">속성이 나 필드를 생략 하려면 **Ignoredatamember** 특성을 사용 하 여 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="15d15-177">전용 및 보호 된 멤버는 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="15d15-178">읽기 전용 속성은 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="15d15-179">그러나 읽기 전용 컬렉션 속성의 내용은 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="15d15-180">클래스 및 멤버 이름은 클래스 선언에 표시 되는 그대로 XML로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="15d15-181">기본 XML 네임 스페이스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-181">A default XML namespace is used.</span></span>

<span data-ttu-id="15d15-182">Serialization을 보다 세부적으로 제어 해야 하는 경우에는 **DataContract** 특성을 사용 하 여 클래스를 데코레이팅 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="15d15-183">이 특성이 있는 경우 클래스는 다음과 같이 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="15d15-184">&quot;옵트인 (Opt in) &quot; 방법: 속성 및 필드는 기본적으로 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="15d15-185">속성 또는 필드를 serialize 하려면 **DataMember** 특성을 사용 하 여 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="15d15-186">Private 또는 protected 멤버를 serialize 하려면 **DataMember** 특성을 사용 하 여 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="15d15-187">읽기 전용 속성은 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="15d15-188">XML에 클래스 이름이 표시 되는 방식을 변경 하려면 **DataContract** 특성에 *name* 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="15d15-189">멤버 이름이 XML에 표시 되는 방식을 변경 하려면 **DataMember** 특성에 *name* 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="15d15-190">XML 네임 스페이스를 변경 하려면 **DataContract** 클래스에서 *namespace* 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="15d15-191">Read-Only 속성</span><span class="sxs-lookup"><span data-stu-id="15d15-191">Read-Only Properties</span></span>

<span data-ttu-id="15d15-192">읽기 전용 속성은 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="15d15-193">읽기 전용 속성에 지원 전용 필드가 있으면 비공개 필드를 **DataMember** 특성으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="15d15-194">이 방법에는 클래스에 대 한 **DataContract** 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="15d15-195">날짜</span><span class="sxs-lookup"><span data-stu-id="15d15-195">Dates</span></span>

<span data-ttu-id="15d15-196">날짜는 ISO 8601 형식으로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="15d15-197">예를 들어 &quot; 2012-05-23T20:21:37.9116538 z가 &quot; 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="15d15-198">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="15d15-198">Indenting</span></span>

<span data-ttu-id="15d15-199">들여쓰기 된 XML을 쓰려면 **들여쓰기** 속성을 **true**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="15d15-200">XML Serializer Per-Type 설정</span><span class="sxs-lookup"><span data-stu-id="15d15-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="15d15-201">다른 CLR 형식에 대해 다른 XML serializer를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="15d15-202">예를 들어 이전 버전과의 호환성을 위해 **XmlSerializer** 를 필요로 하는 특정 데이터 개체가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="15d15-203">이 개체에는 **XmlSerializer** 를 사용 하 고 다른 형식에는 **DataContractSerializer** 를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="15d15-204">특정 형식에 대 한 XML serializer를 설정 하려면 **Setserializer**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="15d15-205">**XmlSerializer** 또는 **XmlObjectSerializer**에서 파생 되는 모든 개체를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="15d15-206">JSON 또는 XML 포맷터 제거</span><span class="sxs-lookup"><span data-stu-id="15d15-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="15d15-207">포맷터 목록에서 JSON 포맷터 또는 XML 포맷터를 사용 하지 않으려면 해당 포맷터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="15d15-208">이 작업을 수행 하는 주요 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="15d15-209">특정 미디어 유형에 대 한 웹 API 응답을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="15d15-210">예를 들어 JSON 응답만 지원 하 고 XML 포맷터는 제거 하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="15d15-211">기본 포맷터를 사용자 지정 포맷터로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="15d15-212">예를 들어 json 포맷터를 JSON 포맷터의 사용자 지정 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="15d15-213">다음 코드에서는 기본 포맷터를 제거 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="15d15-214">Global.asax에 정의 된 **응용 프로그램 \_ 시작** 메서드에서이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="15d15-215">순환 개체 참조 처리</span><span class="sxs-lookup"><span data-stu-id="15d15-215">Handling Circular Object References</span></span>

<span data-ttu-id="15d15-216">기본적으로 JSON 및 XML 포맷터는 모든 개체를 값으로 씁니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="15d15-217">두 속성이 같은 개체를 참조 하거나 동일한 개체가 컬렉션에 두 번 표시 되는 경우 포맷터는 개체를 두 번 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="15d15-218">이는 serializer가 그래프에서 루프를 검색할 때 예외를 throw 하기 때문에 개체 그래프가 순환을 포함 하는 경우의 특정 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="15d15-219">다음 개체 모델 및 컨트롤러를 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="15d15-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="15d15-220">이 작업을 호출 하면 포맷터가 예외를 throw 하 여 클라이언트에 대 한 상태 코드 500 (내부 서버 오류) 응답으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="15d15-221">JSON에서 개체 참조를 유지 하려면 global.asax 파일의 **응용 프로그램 \_ 시작** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="15d15-222">이제 컨트롤러 작업은 다음과 같은 JSON을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="15d15-223">Serializer는 &quot; &quot; 두 개체 모두에 $id 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="15d15-224">또한 Employee 속성이 루프를 생성 하는 것을 감지 하 여 값을 개체 참조 인 { &quot; $ref &quot; : &quot; 1 &quot; }로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="15d15-225">JSON에서 개체 참조는 표준이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="15d15-226">이 기능을 사용 하기 전에 클라이언트에서 결과를 구문 분석할 수 있는지 여부를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="15d15-227">단순히 그래프에서 주기를 제거 하는 것이 더 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="15d15-228">예를 들어 직원에서 부서에 대 한 링크는이 예제에서 정말 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="15d15-229">XML에서 개체 참조를 유지 하기 위해 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="15d15-230">간단한 옵션은 모델 클래스에를 추가 하는 것입니다 `[DataContract(IsReference=true)]` .</span><span class="sxs-lookup"><span data-stu-id="15d15-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="15d15-231">*IsReference* 매개 변수는 개체 참조를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="15d15-232">**DataContract** 는 직렬화를 옵트인 하므로 속성에 **DataMember** 특성도 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="15d15-233">이제 포맷터는 다음과 유사한 XML을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="15d15-234">모델 클래스에서 특성을 사용 하지 않으려면 다른 옵션을 사용 합니다. 즉, 새 유형별 **DataContractSerializer** 인스턴스를 만들고 생성자에서 *preserveObjectReferences* 를 **true** 로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="15d15-235">그런 다음이 인스턴스를 XML 미디어 형식 포맷터의 유형별 serializer로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="15d15-236">다음 코드에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="15d15-237">개체 Serialization 테스트</span><span class="sxs-lookup"><span data-stu-id="15d15-237">Testing Object Serialization</span></span>

<span data-ttu-id="15d15-238">Web API를 설계할 때 데이터 개체가 serialize 되는 방법을 테스트 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="15d15-239">컨트롤러를 만들거나 컨트롤러 작업을 호출 하지 않고도이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d15-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
