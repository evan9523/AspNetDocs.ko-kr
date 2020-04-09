---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET 웹 API에서 JSON 및 XML 직렬화 - ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x에 대한 ASP.NET 웹 API에서 JSON 및 XML 포터에 대해 설명합니다.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675834"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="e4ac2-103">ASP.NET 웹 API에서 JSON 및 XML 직렬화</span><span class="sxs-lookup"><span data-stu-id="e4ac2-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="e4ac2-104">로 [마이크 와슨](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e4ac2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e4ac2-105">이 문서에서는 웹 API의 JSON 및 XML 포터에 대해 설명합니다ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="e4ac2-106">ASP.NET 웹 API에서 *미디어 형식 포터(formatter)는* 다음을 수행할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="e4ac2-107">HTTP 메시지 본문에서 CLR 개체 읽기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="e4ac2-108">HTTP 메시지 본문에 CLR 개체 쓰기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="e4ac2-109">웹 API는 JSON 및 XML 모두에 대한 미디어 형식 포터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="e4ac2-110">프레임워크는 기본적으로 이러한 포터를 파이프라인에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="e4ac2-111">클라이언트는 HTTP 요청의 Accept 헤더에서 JSON 또는 XML을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="e4ac2-112">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e4ac2-112">Contents</span></span>

- [<span data-ttu-id="e4ac2-113">JSON 미디어 형 포터</span><span class="sxs-lookup"><span data-stu-id="e4ac2-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="e4ac2-114">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="e4ac2-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="e4ac2-115">Dates</span><span class="sxs-lookup"><span data-stu-id="e4ac2-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="e4ac2-116">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="e4ac2-117">낙타 케이싱</span><span class="sxs-lookup"><span data-stu-id="e4ac2-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="e4ac2-118">익명 및 약한 형식의 개체</span><span class="sxs-lookup"><span data-stu-id="e4ac2-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="e4ac2-119">XML 미디어 형 포터</span><span class="sxs-lookup"><span data-stu-id="e4ac2-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="e4ac2-120">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="e4ac2-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="e4ac2-121">Dates</span><span class="sxs-lookup"><span data-stu-id="e4ac2-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="e4ac2-122">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="e4ac2-123">유형별 XML 직렬화기 설정</span><span class="sxs-lookup"><span data-stu-id="e4ac2-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="e4ac2-124">JSON 또는 XML 포터 제거</span><span class="sxs-lookup"><span data-stu-id="e4ac2-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="e4ac2-125">순환 객체 참조 처리</span><span class="sxs-lookup"><span data-stu-id="e4ac2-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="e4ac2-126">개체 직렬화 테스트</span><span class="sxs-lookup"><span data-stu-id="e4ac2-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="e4ac2-127">JSON 미디어 형 포터</span><span class="sxs-lookup"><span data-stu-id="e4ac2-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="e4ac2-128">JSON 서식은 **JsonMediaTypeFormatter** 클래스에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="e4ac2-129">기본적으로 **JsonMediaTypeFormatter는** [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 라이브러리를 사용하여 직렬화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="e4ac2-130">Json.NET 타사 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="e4ac2-131">원하는 경우 Json.NET 대신 **DataContractJson Serializer를** 사용하도록 **JsonMediaTypeFormatter** 클래스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="e4ac2-132">이렇게 하려면 **useDataContractJson Serializer** 속성을 **true로**설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="e4ac2-133">JSON serialization</span><span class="sxs-lookup"><span data-stu-id="e4ac2-133">JSON Serialization</span></span>

<span data-ttu-id="e4ac2-134">이 섹션에서는 기본 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 직렬화기를 사용하여 JSON 포매터의 몇 가지 특정 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="e4ac2-135">이는 Json.NET 라이브러리에 대한 포괄적인 문서화를 의미하지 는 않습니다. 자세한 내용은 Json.NET [문서를](http://james.newtonking.com/projects/json/help/)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="e4ac2-136">직렬화되는 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e4ac2-136">What Gets Serialized?</span></span>

<span data-ttu-id="e4ac2-137">기본적으로 모든 공용 속성 및 필드는 직렬화된 JSON에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="e4ac2-138">속성 이나 필드를 생략 하려면 **JsonIgnore** 특성으로 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="e4ac2-139">&quot;옵트인&quot; 방식을 선호하는 경우 DataContract 특성으로 클래스를 **장식합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4ac2-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="e4ac2-140">이 특성이 있으면 **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="e4ac2-141">**DataMember를** 사용하여 개인 멤버를 일련화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="e4ac2-142">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="e4ac2-142">Read-Only Properties</span></span>

<span data-ttu-id="e4ac2-143">읽기 전용 속성은 기본적으로 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="e4ac2-144">날짜</span><span class="sxs-lookup"><span data-stu-id="e4ac2-144">Dates</span></span>

<span data-ttu-id="e4ac2-145">기본적으로 Json.NET [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식으로 날짜를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="e4ac2-146">UTC(조정된 유니버설 타임)의 날짜는 "Z" 접미사로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="e4ac2-147">현지 시간의 날짜에는 표준 시간대 오프셋이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="e4ac2-148">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="e4ac2-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="e4ac2-149">기본적으로 Json.NET 표준 시간대를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="e4ac2-150">DateTimeZoneHandling 속성을 설정 하 여이 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="e4ac2-151">ISO 8601 대신 [Microsoft JSON 날짜 형식](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ()`"\/Date(ticks)\/"`을 사용하려면 직렬화기 설정에서 **DateFormatHandling** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="e4ac2-152">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-152">Indenting</span></span>

<span data-ttu-id="e4ac2-153">들여쓰기된 JSON을 작성하려면 **서식** 지정 설정을 **서식 지정으로 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4ac2-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="e4ac2-154">낙타 케이싱</span><span class="sxs-lookup"><span data-stu-id="e4ac2-154">Camel Casing</span></span>

<span data-ttu-id="e4ac2-155">데이터 모델을 변경하지 않고 낙타 대/소문자를 사용하여 JSON 속성 이름을 작성하려면 serializer에 **CamelCasePropertyNames계약 해결자를** 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="e4ac2-156">익명 및 약한 형식의 개체</span><span class="sxs-lookup"><span data-stu-id="e4ac2-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="e4ac2-157">작업 메서드는 익명 개체를 반환 하 고 JSON에 직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="e4ac2-158">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="e4ac2-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="e4ac2-159">응답 메시지 본문에는 다음 JSON이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="e4ac2-160">웹 API가 클라이언트에서 느슨하게 구조화된 JSON 개체를 수신하는 경우 요청 본문을 **Newtonsoft.Json.Linq.JObject** 유형으로 역직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="e4ac2-161">그러나 일반적으로 강력하게 입력된 데이터 개체를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="e4ac2-162">그런 다음 데이터를 직접 구문 분석할 필요가 없으며 모델 유효성 검사의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="e4ac2-163">XML serializer는 익명 형식 또는 **JObject** 인스턴스를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="e4ac2-164">JSON 데이터에 이러한 기능을 사용하는 경우 이 문서의 설명과 같이 파이프라인에서 XML 포매터를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="e4ac2-165">XML 미디어 형 포터</span><span class="sxs-lookup"><span data-stu-id="e4ac2-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="e4ac2-166">XML 서식은 **XmlMediaTypeFormatter** 클래스에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="e4ac2-167">기본적으로 **XmlMediaTypeFormatter는** **데이터계약 직렬화자** 클래스를 사용하여 직렬화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="e4ac2-168">원하는 경우 **데이터 계약 직렬화기**대신 **Xml Serializer를** 사용하도록 **XmlMediaTypeFormatter를** 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="e4ac2-169">이렇게 하려면 **UseXml Serializer** 속성을 **true로**설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="e4ac2-170">**Xml Serializer** 클래스는 **DataContract Serializer보다**더 좁은 형식 집합을 지원하지만 결과 XML에 대한 더 많은 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="e4ac2-171">기존 XML 스키마와 일치해야 하는 경우 **Xml Serializer를** 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="e4ac2-172">XML 직렬화</span><span class="sxs-lookup"><span data-stu-id="e4ac2-172">XML Serialization</span></span>

<span data-ttu-id="e4ac2-173">이 섹션에서는 기본 **DataContractSerializer**를 사용하여 XML 포터의 몇 가지 특정 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="e4ac2-174">기본적으로 DataContract Serializer는 다음과 같이 행동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="e4ac2-175">모든 공용 읽기/쓰기 속성 및 필드는 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="e4ac2-176">속성 또는 필드를 생략하려면 IgnoreDataMember 특성으로 **장식합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4ac2-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="e4ac2-177">개인 및 보호된 멤버는 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="e4ac2-178">읽기 전용 속성은 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="e4ac2-179">그러나 읽기 전용 컬렉션 속성의 내용은 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="e4ac2-180">클래스 및 멤버 이름은 클래스 선언에 나타나는 것과 정확히 XML에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="e4ac2-181">기본 XML 네임스페이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-181">A default XML namespace is used.</span></span>

<span data-ttu-id="e4ac2-182">직렬화를 보다 세월한 제어가 필요한 경우 **DataContract** 특성으로 클래스를 장식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="e4ac2-183">이 특성이 있으면 클래스는 다음과 같이 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="e4ac2-184">&quot;접근&quot; 방식 선택: 속성 및 필드는 기본적으로 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="e4ac2-185">속성 또는 필드를 직렬화하려면 **DataMember** 특성으로 장식합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="e4ac2-186">개인 또는 보호된 멤버를 직렬화하려면 **DataMember** 특성으로 꾸미십시오.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="e4ac2-187">읽기 전용 속성은 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="e4ac2-188">클래스 이름이 XML에 표시되는 방식을 변경하려면 **DataContract** 특성에서 *Name* 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="e4ac2-189">구성원 이름이 XML에 표시되는 방식을 변경하려면 **DataMember** 특성에서 *Name* 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="e4ac2-190">XML 네임스페이스를 변경하려면 **DataContract** 클래스에서 *네임스페이스* 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="e4ac2-191">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="e4ac2-191">Read-Only Properties</span></span>

<span data-ttu-id="e4ac2-192">읽기 전용 속성은 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="e4ac2-193">읽기 전용 속성에 백업 전용 필드가 있는 경우 **DataMember** 특성으로 개인 필드를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="e4ac2-194">이 방법을 사용하려면 클래스의 **DataContract** 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="e4ac2-195">날짜</span><span class="sxs-lookup"><span data-stu-id="e4ac2-195">Dates</span></span>

<span data-ttu-id="e4ac2-196">날짜는 ISO 8601 형식으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="e4ac2-197">예를 들어 &quot;2012-05-23T20:21:37.9116538Z.&quot;</span><span class="sxs-lookup"><span data-stu-id="e4ac2-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="e4ac2-198">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="e4ac2-198">Indenting</span></span>

<span data-ttu-id="e4ac2-199">들여쓰기XML을 작성하려면 **들여쓰기** 속성을 **true로**설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="e4ac2-200">유형별 XML 직렬화기 설정</span><span class="sxs-lookup"><span data-stu-id="e4ac2-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="e4ac2-201">다른 CLR 유형에 대해 서로 다른 XML 직렬화기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="e4ac2-202">예를 들어 이전 버전과의 호환성을 위해 **Xml Serializer가** 필요한 특정 데이터 개체가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="e4ac2-203">이 개체에 **Xml Serializer를** 사용하고 다른 형식에 **대해 DataContract Serializer를** 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="e4ac2-204">특정 형식에 대한 XML 직렬화기를 설정하려면 **Set Serializer를**호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="e4ac2-205">**Xml Serializer 또는 XmlObject Serializer에서** 파생되는 모든 개체를 지정할 수 있습니다. **XmlObjectSerializer**</span><span class="sxs-lookup"><span data-stu-id="e4ac2-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="e4ac2-206">JSON 또는 XML 포터 제거</span><span class="sxs-lookup"><span data-stu-id="e4ac2-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="e4ac2-207">JSON 포매터 또는 XML 포터터를 사용하지 않으려면 포터 목록에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="e4ac2-208">이 작업을 수행하는 주된 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="e4ac2-209">웹 API 응답을 특정 미디어 유형에 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="e4ac2-210">예를 들어 JSON 응답만 지원하고 XML 포터만 제거하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="e4ac2-211">기본 포터를 사용자 지정 포터로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="e4ac2-212">예를 들어 JSON 포터터를 JSON 포터의 사용자 지정 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="e4ac2-213">다음 코드는 기본 포matters를 제거하는 방법을 보여 주며,</span><span class="sxs-lookup"><span data-stu-id="e4ac2-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="e4ac2-214">Global.asax에 정의된 **응용 프로그램\_시작** 메서드에서 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="e4ac2-215">순환 객체 참조 처리</span><span class="sxs-lookup"><span data-stu-id="e4ac2-215">Handling Circular Object References</span></span>

<span data-ttu-id="e4ac2-216">기본적으로 JSON 및 XML 포matters는 모든 개체를 값으로 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="e4ac2-217">두 속성이 동일한 개체를 참조하거나 동일한 개체가 컬렉션에 두 번 나타나는 경우 formatter는 개체를 두 번 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="e4ac2-218">이 문제는 개체 그래프에 주기가 포함된 경우 직렬화기가 그래프에서 루프를 검색할 때 예외를 throw하기 때문에 특히 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="e4ac2-219">다음 개체 모델 및 컨트롤러를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="e4ac2-220">이 작업을 호출하면 formatter가 예외를 throw하여 클라이언트에 대한 상태 코드 500(내부 서버 오류) 응답으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="e4ac2-221">JSON에서 개체 참조를 유지하려면 Global.asax 파일의 **응용 프로그램\_시작** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="e4ac2-222">이제 컨트롤러 작업은 다음과 같은 JSON을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="e4ac2-223">serializer는 두 &quot;개체에&quot; $id 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="e4ac2-224">또한 Employee.Department 속성이 루프를 만드는 것을 감지하여 값을 개체 참조인&quot;{$ref&quot;&quot;:&quot;1 }로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="e4ac2-225">JSON에서는 개체 참조가 표준이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="e4ac2-226">이 기능을 사용하기 전에 클라이언트가 결과를 구문 분석할 수 있는지 여부를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="e4ac2-227">그래프에서 주기를 제거하는 것이 더 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="e4ac2-228">예를 들어 이 예제에서는 Employee에서 부서로 돌아가는 링크가 실제로 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="e4ac2-229">XML에서 개체 참조를 보존하려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="e4ac2-230">더 간단한 옵션은 모델 `[DataContract(IsReference=true)]` 클래스에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="e4ac2-231">*IsReference* 매개 변수는 개체 참조를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="e4ac2-232">**DataContract는** 직렬화를 옵트인하므로 속성에 **DataMember** 특성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="e4ac2-233">이제 포터는 다음과 유사한 XML을 생성합니다:</span><span class="sxs-lookup"><span data-stu-id="e4ac2-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="e4ac2-234">모델 클래스의 특성을 피하려면 새 형식별 **DataContractSerializer** 인스턴스를 만들고 생성자에서 *true로 preserveObjectReferences를* 설정하는 또 다른 옵션이 있습니다. **true**</span><span class="sxs-lookup"><span data-stu-id="e4ac2-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="e4ac2-235">그런 다음 이 인스턴스를 XML 미디어 형식 포터의 형식별 직렬화자로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="e4ac2-236">다음 코드는 이 작업을 수행하는 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과</span><span class="sxs-lookup"><span data-stu-id="e4ac2-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="e4ac2-237">개체 직렬화 테스트</span><span class="sxs-lookup"><span data-stu-id="e4ac2-237">Testing Object Serialization</span></span>

<span data-ttu-id="e4ac2-238">웹 API를 디자인할 때 데이터 개체가 직렬화되는 방식을 테스트하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="e4ac2-239">컨트롤러를 만들거나 컨트롤러 작업을 호출하지 않고도 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ac2-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
