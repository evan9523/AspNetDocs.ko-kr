---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API에서에서 JSON 및 XML | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 05/30/2012
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 47967e6e1dd0e84b6059c07d7544c0e755fdf510
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028930"
---
<a name="json-and-xml-serialization-in-aspnet-web-api"></a>JSON 및 XML 직렬화에 ASP.NET Web API
====================
[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API에서 JSON 및 XML 포맷터를 설명 합니다.

ASP.NET Web API에는 *미디어 유형 포맷터* 는 개체 수입니다.

- HTTP에서 읽기 CLR 개체로 메시지 본문
- HTTP 메시지 본문에 CLR 개체를 작성 합니다.

웹 API는 JSON 및 XML에 대 한 미디어 유형 포맷터를 제공합니다. 프레임 워크는 기본적으로 파이프라인에 이러한 포맷터를 삽입합니다. 클라이언트는 HTTP 요청의 Accept 헤더의 JSON 또는 XML 요청할 수 있습니다.

## <a name="contents"></a>목차

- [JSON 미디어 유형 포맷터입니다.](#json_media_type_formatter)

    - [읽기 전용 속성](#json_readonly)
    - [날짜](#json_dates)
    - [들여쓰기](#json_indenting)
    - [카멜식 대/소문자](#json_camelcasing)
    - [익명 및 약한 형 개체](#json_anon)
- [XML 미디어 유형 포맷터입니다.](#xml_media_type_formatter)

    - [읽기 전용 속성](#xml_readonly)
    - [날짜](#xml_dates)
    - [들여쓰기](#xml_indenting)
    - [형식당 하나의 XML 직렬 변환기 설정](#xml_pertype)
- [JSON 또는 XML 포맷터를 제거합니다.](#removing_the_json_or_xml_formatter)
- [순환 개체 참조를 처리합니다.](#handling_circular_object_references)
- [테스트 개체 Serialization](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON 미디어 유형 포맷터입니다.

제공 하는 JSON 형식 지정 된 **JsonMediaTypeFormatter** 클래스입니다. 기본적으로 **JsonMediaTypeFormatter** 사용 하는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serialization을 수행 하는 라이브러리입니다. Json.NET 타사 오픈 소스 프로젝트입니다.

원하는 경우 구성할 수 있습니다는 **JsonMediaTypeFormatter** 클래스를 사용 합니다 **DataContractJsonSerializer** Json.NET 대신 합니다. 이렇게 하려면 설정 합니다 **UseDataContractJsonSerializer** 속성을 **true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON serialization

이 섹션에서는 기본값을 사용 하 여 JSON 포맷터의 몇 가지 특정 동작을 설명 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer입니다. Json.NET library;의 포괄적인 설명서를 다루지는지 않습니다. 자세한 내용은 참조는 [Json.NET 설명서](http://james.newtonking.com/projects/json/help/)합니다.

#### <a name="what-gets-serialized"></a>Serialize 되는 요소?

기본적으로 모든 public 속성과 필드가 serialize 된 JSON에 포함 됩니다. 속성 또는 필드를 생략 하려면 데코 레이트 하는 **JsonIgnore** 특성입니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

원하는 경우는 &quot;옵트인&quot; 접근을 사용 하 여 클래스를 데코 레이트 합니다 **DataContract** 특성입니다. 이 특성이 있는 경우에 멤버를 무시에 대 한 필요 합니다 **DataMember**합니다. 사용할 수도 있습니다 **DataMember** 전용 멤버를 serialize 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>읽기 전용 속성

읽기 전용 속성은 기본적으로 serialize 됩니다.

<a id="json_dates"></a>
### <a name="dates"></a>날짜

기본적으로 Json.NET 날짜를 씁니다 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식입니다. Utc (협정 세계시) 날짜는 "Z" 접미사를 사용 하 여 기록 됩니다. 현지 시간에서 날짜-표준 시간대 오프셋을 포함합니다. 예를 들어:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Json.NET 기본적으로 표준 시간대를 유지합니다. DateTimeZoneHandling 속성을 설정 하 여이 재정의할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

사용 하려는 경우 [Microsoft JSON 날짜 형식을](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) ISO 8601 대신 설정 된 **DateFormatHandling** serializer 설정에 대 한 속성:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기 된 JSON을 작성 하려면 설정 합니다 **서식** 설정을 **Formatting.Indented**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>카멜식 대/소문자

JSON 속성 이름을 카멜식 대/소문자를 사용 하 여 데이터 모델을 변경 하지 않고를 작성 하려면 설정 합니다 **CamelCasePropertyNamesContractResolver** serializer에서:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>익명 및 약한 형 개체

동작 메서드는 익명 개체를 반환 하 고 JSON으로 serialize 할 수 있습니다. 예를 들어:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

응답 메시지 본문은 다음 JSON이 포함 됩니다.

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

웹 API가 받은 느슨하게 구조화 클라이언트에서 JSON 개체, 경우 요청 본문을 deserialize 할 수는 **Newtonsoft.Json.Linq.JObject** 형식입니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

그러나는 강력한 형식의 데이터 개체를 사용 하는 것이 좋습니다. 그런 다음 사용자가 직접 데이터를 구문 분석 필요가 없습니다 및 모델 유효성 검사의 이점을 얻을 수 있습니다.

XML serializer 익명 형식을 지원 하지 않습니다 또는 **JObject** 인스턴스. JSON 데이터에 대 한 이러한 기능을 사용 하는 경우이 문서의 뒷부분에 설명 된 대로 XML 포맷터 파이프라인에서 제거 해야 합니다.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML 미디어 유형 포맷터입니다.

제공 하는 XML 서식 지정 된 **XmlMediaTypeFormatter** 클래스입니다. 기본적으로 **XmlMediaTypeFormatter** 사용 하는 **DataContractSerializer** serialization을 수행 하는 클래스입니다.

원하는 경우 구성할 수 있습니다는 **XmlMediaTypeFormatter** 사용 하는 **XmlSerializer** 대신 합니다 **DataContractSerializer**합니다. 이렇게 하려면 설정 합니다 **UseXmlSerializer** 속성을 **true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

합니다 **XmlSerializer** 클래스 형식 보다 적은 집합을 지원 **DataContractSerializer**, 하지만 결과 XML 통해 더 많은 제어를 제공 합니다. 사용 하는 것이 좋습니다 **XmlSerializer** 기존 XML 스키마와 일치 하는 경우.

### <a name="xml-serialization"></a>XML Serialization

이 섹션에서는 기본값을 사용 하 여 XML 포맷터의 몇 가지 특정 동작을 설명 **DataContractSerializer**합니다.

기본적으로 DataContractSerializer는 다음과 같이 동작합니다.

- 모든 공용 읽기/쓰기 속성과 필드가 serialize 됩니다. 속성 또는 필드를 생략 하려면 데코 레이트 하는 **IgnoreDataMember** 특성입니다.
- Private 및 protected 멤버는 serialize 되지 않습니다.
- 읽기 전용 속성이 serialize 되지 않습니다. 그러나 (읽기 전용 컬렉션 속성의 내용은 serialize 됩니다.)
- 클래스 선언에 표시 된 대로 클래스 및 멤버 이름의 XML로 작성 됩니다.
- 기본 XML 네임 스페이스 사용 됩니다.

사용 하 여 클래스를 데코레이팅 할 수 있습니다 더 많이 제어할 serialization에 필요한 경우는 **DataContract** 특성입니다. 이 특성이 있는 경우 클래스는 다음과 같이 serialize 됩니다.

- &quot;옵트인&quot; 접근 방식: 기본적으로 속성과 필드가 serialize 되지 않습니다. 속성 또는 필드를 serialize 하려면 데코 레이트 하는 **DataMember** 특성입니다.
- Private 또는 protected 멤버를 serialize 하려면 데코 레이트 하는 **DataMember** 특성입니다.
- 읽기 전용 속성이 serialize 되지 않습니다.
- 클래스 이름을 XML에 표시 되는 방식을 변경 하려면 설정 합니다 *이름* 에 매개 변수를 **DataContract** 특성입니다.
- 멤버 이름을 XML에 표시 되는 방식을 변경 하려면 설정 합니다 *이름* 에 매개 변수를 **DataMember** 특성입니다.
- XML 네임 스페이스를 변경 하려면 설정 합니다 *Namespace* 에 매개 변수를 **DataContract** 클래스입니다.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>읽기 전용 속성

읽기 전용 속성이 serialize 되지 않습니다. 읽기 전용 속성을 지 원하는 private 필드에 사용 하 여 개인 필드를 표시할 수 있습니다 합니다 **DataMember** 특성입니다. 이 접근 방식에서는 합니다 **DataContract** 클래스의 특성입니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>날짜

날짜는 ISO 8601 형식으로 기록 됩니다. 예를 들어 &quot;2012-05-23T20:21:37.9116538Z&quot;합니다.

<a id="xml_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기 된 XML을 쓸 설정 합니다 **들여쓰기** 속성을 **true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>형식당 하나의 XML 직렬 변환기 설정

다른 CLR 형식에 대 한 다른 XML 직렬 변환기를 설정할 수 있습니다. 예를 들어 필요한 특정 데이터 개체를 해야 할 수 있습니다 **XmlSerializer** 이전 버전과 호환성에 대 한 합니다. 사용할 수 있습니다 **XmlSerializer** 이 개체를 사용 하 여 계속 **DataContractSerializer** 다른 형식에 대 한 합니다.

특정 형식에 대 한 XML 직렬 변환기를 설정 하려면 호출 **SetSerializer**합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

지정할 수는 **XmlSerializer** 에서 파생 된 모든 개체 또는 **XmlObjectSerializer**합니다.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON 또는 XML 포맷터를 제거합니다.

JSON 포맷터 또는 XML 포맷터를 사용 하지 않을 경우 포맷터 목록에서 제거할 수 있습니다. 이 작업을 수행 하는 주요 이유가 있습니다.

- 특정 미디어 유형의 웹 API 응답 내용을 제한 합니다. 예를 들어 JSON 응답 에서만 지원 및 XML 포맷터를 제거할 수도 있습니다.
- 기본 포맷터를 사용자 지정 포맷터를 바꿉니다. 예를 들어 JSON 포맷터의 고유한 사용자 지정 구현을 사용 하 여 JSON 포맷터를 바꿀 수 있습니다.

다음 코드는 기본 포맷터를 제거 하는 방법을 보여 줍니다. 이를 호출 하면 **응용 프로그램\_시작** Global.asax에 정의 된 메서드를 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>순환 개체 참조를 처리합니다.

기본적으로 JSON 및 XML 포맷터를 값으로 모든 개체를 작성합니다. 두 속성이 같은 개체를 참조 하는 경우, 동일한 개체를 컬렉션에 두 번 표시 하는 경우 포맷터 개체를 두 번 serialize 됩니다. 왜냐하면 특정 문제를 개체 그래프에는 주기를 포함 하는 경우 serializer가 그래프에는 루프를 감지 하는 경우 예외가 throw 됩니다.

다음 개체 모델 및 컨트롤러를 고려 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

이 작업을 호출 하면 포맷터를 클라이언트에 상태 코드 500 (내부 서버 오류) 응답을 변환 하는 예외가 발생 합니다.

JSON에서 개체 참조를 유지 하려면 다음 코드를 추가 합니다 **응용 프로그램\_시작** Global.asax 파일에는 메서드:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

이제 컨트롤러 작업에서는 다음과 같은 JSON을 반환 합니다.

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

직렬 변환기를 추가 하는 &quot;$id&quot; 두 개체에는 속성입니다. 또한 감지한 Employee.Department 속성 개체 참조를 사용 하 여 값을 대체 하도록 루프를 만듭니다. {&quot;$ref&quot;:&quot;1&quot;}.

> [!NOTE]
> 개체 참조는 json에서 표준 아닙니다. 이 기능을 사용 하기 전에 클라이언트에 결과 구문 분석할 수 있는지 여부를 하는 것이 좋습니다. 그래프에서 주기를 제거 하려면 단순히 좋을 것입니다. 예를 들어,이 예제에서 직원 부서에 다시 링크를 실제로 필요 하지 않습니다.


XML에서 개체 참조를 유지 하는 두 가지 옵션이 있습니다. 간단한 옵션은 추가 `[DataContract(IsReference=true)]` 모델 클래스에 있습니다. 합니다 *IsReference* 개체 참조 매개 변수를 사용 합니다. 유의 해야 **DataContract** 추가할 해야 하므로 옵트인, 직렬화를 사용 하면 **DataMember** 속성 특성:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

포맷터와 유사한 XML 생성은 이제 다음과 같습니다.

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

모델 클래스의 특성을 방지 하려는 경우 또 다른 옵션: 만들 새 형식별 **DataContractSerializer** 인스턴스 및 설정 *preserveObjectReferences* 에 **true** 생성자에서. XML 미디어 유형 포맷터에서 형식당 하나의 serializer로이 인스턴스를 설정 합니다. 다음 코드에는이 작업을 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>테스트 개체 Serialization

Web API를 디자인할 때 데이터 개체는 직렬화 하는 방법을 테스트 하는 데 유용 합니다. 컨트롤러 만들기 또는 컨트롤러 작업을 호출 하지 않고이 수행할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
