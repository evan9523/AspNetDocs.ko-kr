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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API의 JSON 및 XML 직렬화

[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API의 JSON 및 XML 포맷터에 대해 설명 합니다.

ASP.NET Web API *미디어 형식 포맷터* 는 다음을 수행할 수 있는 개체입니다.

- HTTP 메시지 본문에서 CLR 개체 읽기
- HTTP 메시지 본문에 CLR 개체를 씁니다.

Web API는 JSON 및 XML에 대 한 미디어 유형 포맷터를 제공 합니다. 프레임 워크는 기본적으로 이러한 포맷터를 파이프라인에 삽입 합니다. 클라이언트는 HTTP 요청의 Accept 헤더에 JSON 또는 XML을 요청할 수 있습니다.

## <a name="contents"></a>콘텐츠

- [JSON Media-Type 포맷터](#json_media_type_formatter)

    - [읽기 전용 속성](#json_readonly)
    - [날짜](#json_dates)
    - [들여쓰기](#json_indenting)
    - [카멜식 대/소문자 구분](#json_camelcasing)
    - [익명 및 Weakly-Typed 개체](#json_anon)
- [XML Media-Type 포맷터](#xml_media_type_formatter)

    - [읽기 전용 속성](#xml_readonly)
    - [날짜](#xml_dates)
    - [들여쓰기](#xml_indenting)
    - [XML Serializer Per-Type 설정](#xml_pertype)
- [JSON 또는 XML 포맷터 제거](#removing_the_json_or_xml_formatter)
- [순환 개체 참조 처리](#handling_circular_object_references)
- [개체 Serialization 테스트](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Media-Type 포맷터

JSON 형식 지정은 **JsonMediaTypeFormatter** 클래스에서 제공 합니다. 기본적으로 **JsonMediaTypeFormatter** 는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 라이브러리를 사용 하 여 serialization을 수행 합니다. Json.NET는 타사 오픈 소스 프로젝트입니다.

원하는 경우 Json.NET 대신 **DataContractJsonSerializer** 를 사용 하도록 **JsonMediaTypeFormatter** 클래스를 구성할 수 있습니다. 이렇게 하려면 **UseDataContractJsonSerializer** 속성을 **true**로 설정 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON serialization

이 섹션에서는 기본 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer를 사용 하 여 JSON 포맷터의 몇 가지 특정 동작에 대해 설명 합니다. 이는 Json.NET 라이브러리의 포괄적인 설명서가 아닙니다. 자세한 내용은 [Json.NET 설명서](http://james.newtonking.com/projects/json/help/)를 참조 하세요.

#### <a name="what-gets-serialized"></a>Serialize 되는 항목

기본적으로 모든 public 속성 및 필드는 직렬화 된 JSON에 포함 됩니다. 속성 또는 필드를 생략 하려면 **JsonIgnore** 특성을 사용 하 여 데코 레이트 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

&quot;옵트인 (opt in) 방식을 선호 하는 경우 &quot; 클래스를 **DataContract** 특성으로 데코 레이트 합니다. 이 특성이 있는 경우 멤버는 **DataMember**가 없는 한 무시 됩니다. 또한 **DataMember** 를 사용 하 여 전용 멤버를 serialize 할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Read-Only 속성

읽기 전용 속성은 기본적으로 serialize 됩니다.

<a id="json_dates"></a>
### <a name="dates"></a>날짜

기본적으로 Json.NET는 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식으로 날짜를 기록 합니다. UTC (협정 세계시)의 날짜는 "Z" 접미사로 작성 됩니다. 현지 시간 날짜에는 표준 시간대 오프셋이 포함 됩니다. 예를 들면 다음과 같습니다.

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

기본적으로 Json.NET는 표준 시간대를 유지 합니다. DateTimeZoneHandling 속성을 설정 하 여이를 재정의할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 대신 [MICROSOFT JSON 날짜 형식](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ()을 사용 하려는 경우 `"\/Date(ticks)\/"` Serializer 설정에서 **DateFormatHandling** 속성을 설정 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기 된 JSON을 작성 하려면 **서식** 설정을 서식으로 설정 **합니다. 들여쓰기**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>카멜식 대/소문자 구분

데이터 모델을 변경 하지 않고 카멜식 대/소문자 구분을 사용 하 여 JSON 속성 이름을 쓰려면 serializer에서 **CamelCasePropertyNamesContractResolver** 를 설정 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>익명 및 Weakly-Typed 개체

작업 메서드는 익명 개체를 반환 하 고이를 JSON으로 serialize 할 수 있습니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

응답 메시지 본문에는 다음 JSON이 포함 됩니다.

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

웹 API가 클라이언트에서 느슨하게 구조화 된 JSON 개체를 수신 하는 경우 요청 본문을의Newtonsoft.Jsdeserialize 할 수 있습니다 ** . Linq. JObject** 형식입니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

그러나 강력한 형식의 데이터 개체를 사용 하는 것이 일반적으로 더 좋습니다. 그런 다음 데이터를 직접 구문 분석할 필요가 없으며 모델 유효성 검사의 이점을 얻을 수 있습니다.

XML serializer는 익명 형식 또는 **Jobject** 인스턴스를 지원 하지 않습니다. JSON 데이터에 이러한 기능을 사용 하는 경우이 문서의 뒷부분에서 설명 하는 대로 파이프라인에서 XML 포맷터를 제거 해야 합니다.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML Media-Type 포맷터

XML 서식 지정은 **XmlMediaTypeFormatter** 클래스에 의해 제공 됩니다. 기본적으로 **XmlMediaTypeFormatter** 는 **DataContractSerializer** 클래스를 사용 하 여 serialization을 수행 합니다.

원하는 경우 **DataContractSerializer**대신 **XmlSerializer** 를 사용 하도록 **XmlMediaTypeFormatter** 를 구성할 수 있습니다. 이렇게 하려면 **UseXmlSerializer** 속성을 **true**로 설정 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer** 클래스는 **DataContractSerializer**보다 좁은 형식의 집합을 지원 하지만 결과 XML에 대 한 더 많은 제어를 제공 합니다. 기존 XML 스키마와 일치 해야 하는 경우 **XmlSerializer** 를 사용 하는 것이 좋습니다.

### <a name="xml-serialization"></a>XML Serialization

이 섹션에서는 기본 **DataContractSerializer**를 사용 하 여 XML 포맷터의 몇 가지 특정 동작에 대해 설명 합니다.

기본적으로 DataContractSerializer는 다음과 같이 동작 합니다.

- 모든 public 읽기/쓰기 속성과 필드가 serialize 됩니다. 속성이 나 필드를 생략 하려면 **Ignoredatamember** 특성을 사용 하 여 데코 레이트 합니다.
- 전용 및 보호 된 멤버는 serialize 되지 않습니다.
- 읽기 전용 속성은 serialize 되지 않습니다. 그러나 읽기 전용 컬렉션 속성의 내용은 serialize 됩니다.
- 클래스 및 멤버 이름은 클래스 선언에 표시 되는 그대로 XML로 작성 됩니다.
- 기본 XML 네임 스페이스가 사용 됩니다.

Serialization을 보다 세부적으로 제어 해야 하는 경우에는 **DataContract** 특성을 사용 하 여 클래스를 데코레이팅 할 수 있습니다. 이 특성이 있는 경우 클래스는 다음과 같이 serialize 됩니다.

- &quot;옵트인 (Opt in) &quot; 방법: 속성 및 필드는 기본적으로 serialize 되지 않습니다. 속성 또는 필드를 serialize 하려면 **DataMember** 특성을 사용 하 여 데코 레이트 합니다.
- Private 또는 protected 멤버를 serialize 하려면 **DataMember** 특성을 사용 하 여 데코 레이트 합니다.
- 읽기 전용 속성은 serialize 되지 않습니다.
- XML에 클래스 이름이 표시 되는 방식을 변경 하려면 **DataContract** 특성에 *name* 매개 변수를 설정 합니다.
- 멤버 이름이 XML에 표시 되는 방식을 변경 하려면 **DataMember** 특성에 *name* 매개 변수를 설정 합니다.
- XML 네임 스페이스를 변경 하려면 **DataContract** 클래스에서 *namespace* 매개 변수를 설정 합니다.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Read-Only 속성

읽기 전용 속성은 serialize 되지 않습니다. 읽기 전용 속성에 지원 전용 필드가 있으면 비공개 필드를 **DataMember** 특성으로 표시할 수 있습니다. 이 방법에는 클래스에 대 한 **DataContract** 특성이 필요 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>날짜

날짜는 ISO 8601 형식으로 작성 됩니다. 예를 들어 &quot; 2012-05-23T20:21:37.9116538 z가 &quot; 있습니다.

<a id="xml_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기 된 XML을 쓰려면 **들여쓰기** 속성을 **true**로 설정 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>XML Serializer Per-Type 설정

다른 CLR 형식에 대해 다른 XML serializer를 설정할 수 있습니다. 예를 들어 이전 버전과의 호환성을 위해 **XmlSerializer** 를 필요로 하는 특정 데이터 개체가 있을 수 있습니다. 이 개체에는 **XmlSerializer** 를 사용 하 고 다른 형식에는 **DataContractSerializer** 를 계속 사용할 수 있습니다.

특정 형식에 대 한 XML serializer를 설정 하려면 **Setserializer**를 호출 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

**XmlSerializer** 또는 **XmlObjectSerializer**에서 파생 되는 모든 개체를 지정할 수 있습니다.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON 또는 XML 포맷터 제거

포맷터 목록에서 JSON 포맷터 또는 XML 포맷터를 사용 하지 않으려면 해당 포맷터를 제거할 수 있습니다. 이 작업을 수행 하는 주요 이유는 다음과 같습니다.

- 특정 미디어 유형에 대 한 웹 API 응답을 제한 합니다. 예를 들어 JSON 응답만 지원 하 고 XML 포맷터는 제거 하도록 결정할 수 있습니다.
- 기본 포맷터를 사용자 지정 포맷터로 바꿉니다. 예를 들어 json 포맷터를 JSON 포맷터의 사용자 지정 구현으로 바꿀 수 있습니다.

다음 코드에서는 기본 포맷터를 제거 하는 방법을 보여 줍니다. Global.asax에 정의 된 **응용 프로그램 \_ 시작** 메서드에서이 메서드를 호출 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>순환 개체 참조 처리

기본적으로 JSON 및 XML 포맷터는 모든 개체를 값으로 씁니다. 두 속성이 같은 개체를 참조 하거나 동일한 개체가 컬렉션에 두 번 표시 되는 경우 포맷터는 개체를 두 번 serialize 합니다. 이는 serializer가 그래프에서 루프를 검색할 때 예외를 throw 하기 때문에 개체 그래프가 순환을 포함 하는 경우의 특정 문제입니다.

다음 개체 모델 및 컨트롤러를 고려 하십시오.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

이 작업을 호출 하면 포맷터가 예외를 throw 하 여 클라이언트에 대 한 상태 코드 500 (내부 서버 오류) 응답으로 변환 됩니다.

JSON에서 개체 참조를 유지 하려면 global.asax 파일의 **응용 프로그램 \_ 시작** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

이제 컨트롤러 작업은 다음과 같은 JSON을 반환 합니다.

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Serializer는 &quot; &quot; 두 개체 모두에 $id 속성을 추가 합니다. 또한 Employee 속성이 루프를 생성 하는 것을 감지 하 여 값을 개체 참조 인 { &quot; $ref &quot; : &quot; 1 &quot; }로 바꿉니다.

> [!NOTE]
> JSON에서 개체 참조는 표준이 아닙니다. 이 기능을 사용 하기 전에 클라이언트에서 결과를 구문 분석할 수 있는지 여부를 고려 합니다. 단순히 그래프에서 주기를 제거 하는 것이 더 좋을 수 있습니다. 예를 들어 직원에서 부서에 대 한 링크는이 예제에서 정말 필요 하지 않습니다.

XML에서 개체 참조를 유지 하기 위해 두 가지 옵션이 있습니다. 간단한 옵션은 모델 클래스에를 추가 하는 것입니다 `[DataContract(IsReference=true)]` . *IsReference* 매개 변수는 개체 참조를 사용 하도록 설정 합니다. **DataContract** 는 직렬화를 옵트인 하므로 속성에 **DataMember** 특성도 추가 해야 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

이제 포맷터는 다음과 유사한 XML을 생성 합니다.

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

모델 클래스에서 특성을 사용 하지 않으려면 다른 옵션을 사용 합니다. 즉, 새 유형별 **DataContractSerializer** 인스턴스를 만들고 생성자에서 *preserveObjectReferences* 를 **true** 로 설정 합니다. 그런 다음이 인스턴스를 XML 미디어 형식 포맷터의 유형별 serializer로 설정 합니다. 다음 코드에서는이 작업을 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>개체 Serialization 테스트

Web API를 설계할 때 데이터 개체가 serialize 되는 방법을 테스트 하는 것이 유용 합니다. 컨트롤러를 만들거나 컨트롤러 작업을 호출 하지 않고도이 작업을 수행할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
