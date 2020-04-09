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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET 웹 API에서 JSON 및 XML 직렬화

로 [마이크 와슨](https://github.com/MikeWasson)

이 문서에서는 웹 API의 JSON 및 XML 포터에 대해 설명합니다ASP.NET.

ASP.NET 웹 API에서 *미디어 형식 포터(formatter)는* 다음을 수행할 수 있는 개체입니다.

- HTTP 메시지 본문에서 CLR 개체 읽기
- HTTP 메시지 본문에 CLR 개체 쓰기

웹 API는 JSON 및 XML 모두에 대한 미디어 형식 포터를 제공합니다. 프레임워크는 기본적으로 이러한 포터를 파이프라인에 삽입합니다. 클라이언트는 HTTP 요청의 Accept 헤더에서 JSON 또는 XML을 요청할 수 있습니다.

## <a name="contents"></a>콘텐츠

- [JSON 미디어 형 포터](#json_media_type_formatter)

    - [읽기 전용 속성](#json_readonly)
    - [Dates](#json_dates)
    - [들여쓰기](#json_indenting)
    - [낙타 케이싱](#json_camelcasing)
    - [익명 및 약한 형식의 개체](#json_anon)
- [XML 미디어 형 포터](#xml_media_type_formatter)

    - [읽기 전용 속성](#xml_readonly)
    - [Dates](#xml_dates)
    - [들여쓰기](#xml_indenting)
    - [유형별 XML 직렬화기 설정](#xml_pertype)
- [JSON 또는 XML 포터 제거](#removing_the_json_or_xml_formatter)
- [순환 객체 참조 처리](#handling_circular_object_references)
- [개체 직렬화 테스트](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON 미디어 형 포터

JSON 서식은 **JsonMediaTypeFormatter** 클래스에서 제공합니다. 기본적으로 **JsonMediaTypeFormatter는** [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 라이브러리를 사용하여 직렬화를 수행합니다. Json.NET 타사 오픈 소스 프로젝트입니다.

원하는 경우 Json.NET 대신 **DataContractJson Serializer를** 사용하도록 **JsonMediaTypeFormatter** 클래스를 구성할 수 있습니다. 이렇게 하려면 **useDataContractJson Serializer** 속성을 **true로**설정합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON serialization

이 섹션에서는 기본 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 직렬화기를 사용하여 JSON 포매터의 몇 가지 특정 동작에 대해 설명합니다. 이는 Json.NET 라이브러리에 대한 포괄적인 문서화를 의미하지 는 않습니다. 자세한 내용은 Json.NET [문서를](http://james.newtonking.com/projects/json/help/)참조하십시오.

#### <a name="what-gets-serialized"></a>직렬화되는 것은 무엇입니까?

기본적으로 모든 공용 속성 및 필드는 직렬화된 JSON에 포함됩니다. 속성 이나 필드를 생략 하려면 **JsonIgnore** 특성으로 장식 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

&quot;옵트인&quot; 방식을 선호하는 경우 DataContract 특성으로 클래스를 **장식합니다.** 이 특성이 있으면 **DataMember**. **DataMember를** 사용하여 개인 멤버를 일련화할 수도 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>읽기 전용 속성

읽기 전용 속성은 기본적으로 직렬화됩니다.

<a id="json_dates"></a>
### <a name="dates"></a>날짜

기본적으로 Json.NET [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식으로 날짜를 씁니다. UTC(조정된 유니버설 타임)의 날짜는 "Z" 접미사로 작성됩니다. 현지 시간의 날짜에는 표준 시간대 오프셋이 포함됩니다. 예를 들어:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

기본적으로 Json.NET 표준 시간대를 유지합니다. DateTimeZoneHandling 속성을 설정 하 여이 재정의할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 대신 [Microsoft JSON 날짜 형식](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ()`"\/Date(ticks)\/"`을 사용하려면 직렬화기 설정에서 **DateFormatHandling** 속성을 설정합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기된 JSON을 작성하려면 **서식** 지정 설정을 **서식 지정으로 설정합니다.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>낙타 케이싱

데이터 모델을 변경하지 않고 낙타 대/소문자를 사용하여 JSON 속성 이름을 작성하려면 serializer에 **CamelCasePropertyNames계약 해결자를** 설정합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>익명 및 약한 형식의 개체

작업 메서드는 익명 개체를 반환 하 고 JSON에 직렬화할 수 있습니다. 예를 들어:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

응답 메시지 본문에는 다음 JSON이 포함됩니다.

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

웹 API가 클라이언트에서 느슨하게 구조화된 JSON 개체를 수신하는 경우 요청 본문을 **Newtonsoft.Json.Linq.JObject** 유형으로 역직렬화할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

그러나 일반적으로 강력하게 입력된 데이터 개체를 사용하는 것이 좋습니다. 그런 다음 데이터를 직접 구문 분석할 필요가 없으며 모델 유효성 검사의 이점을 얻을 수 있습니다.

XML serializer는 익명 형식 또는 **JObject** 인스턴스를 지원하지 않습니다. JSON 데이터에 이러한 기능을 사용하는 경우 이 문서의 설명과 같이 파이프라인에서 XML 포매터를 제거해야 합니다.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML 미디어 형 포터

XML 서식은 **XmlMediaTypeFormatter** 클래스에서 제공합니다. 기본적으로 **XmlMediaTypeFormatter는** **데이터계약 직렬화자** 클래스를 사용하여 직렬화를 수행합니다.

원하는 경우 **데이터 계약 직렬화기**대신 **Xml Serializer를** 사용하도록 **XmlMediaTypeFormatter를** 구성할 수 있습니다. 이렇게 하려면 **UseXml Serializer** 속성을 **true로**설정합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**Xml Serializer** 클래스는 **DataContract Serializer보다**더 좁은 형식 집합을 지원하지만 결과 XML에 대한 더 많은 제어를 제공합니다. 기존 XML 스키마와 일치해야 하는 경우 **Xml Serializer를** 사용하는 것이 좋습니다.

### <a name="xml-serialization"></a>XML 직렬화

이 섹션에서는 기본 **DataContractSerializer**를 사용하여 XML 포터의 몇 가지 특정 동작에 대해 설명합니다.

기본적으로 DataContract Serializer는 다음과 같이 행동합니다.

- 모든 공용 읽기/쓰기 속성 및 필드는 직렬화됩니다. 속성 또는 필드를 생략하려면 IgnoreDataMember 특성으로 **장식합니다.**
- 개인 및 보호된 멤버는 직렬화되지 않습니다.
- 읽기 전용 속성은 직렬화되지 않습니다. 그러나 읽기 전용 컬렉션 속성의 내용은 직렬화됩니다.
- 클래스 및 멤버 이름은 클래스 선언에 나타나는 것과 정확히 XML에 기록됩니다.
- 기본 XML 네임스페이스가 사용됩니다.

직렬화를 보다 세월한 제어가 필요한 경우 **DataContract** 특성으로 클래스를 장식할 수 있습니다. 이 특성이 있으면 클래스는 다음과 같이 직렬화됩니다.

- &quot;접근&quot; 방식 선택: 속성 및 필드는 기본적으로 직렬화되지 않습니다. 속성 또는 필드를 직렬화하려면 **DataMember** 특성으로 장식합니다.
- 개인 또는 보호된 멤버를 직렬화하려면 **DataMember** 특성으로 꾸미십시오.
- 읽기 전용 속성은 직렬화되지 않습니다.
- 클래스 이름이 XML에 표시되는 방식을 변경하려면 **DataContract** 특성에서 *Name* 매개 변수를 설정합니다.
- 구성원 이름이 XML에 표시되는 방식을 변경하려면 **DataMember** 특성에서 *Name* 매개 변수를 설정합니다.
- XML 네임스페이스를 변경하려면 **DataContract** 클래스에서 *네임스페이스* 매개 변수를 설정합니다.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>읽기 전용 속성

읽기 전용 속성은 직렬화되지 않습니다. 읽기 전용 속성에 백업 전용 필드가 있는 경우 **DataMember** 특성으로 개인 필드를 표시할 수 있습니다. 이 방법을 사용하려면 클래스의 **DataContract** 특성이 필요합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>날짜

날짜는 ISO 8601 형식으로 작성됩니다. 예를 들어 &quot;2012-05-23T20:21:37.9116538Z.&quot;

<a id="xml_indenting"></a>
### <a name="indenting"></a>들여쓰기

들여쓰기XML을 작성하려면 **들여쓰기** 속성을 **true로**설정합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>유형별 XML 직렬화기 설정

다른 CLR 유형에 대해 서로 다른 XML 직렬화기를 설정할 수 있습니다. 예를 들어 이전 버전과의 호환성을 위해 **Xml Serializer가** 필요한 특정 데이터 개체가 있을 수 있습니다. 이 개체에 **Xml Serializer를** 사용하고 다른 형식에 **대해 DataContract Serializer를** 계속 사용할 수 있습니다.

특정 형식에 대한 XML 직렬화기를 설정하려면 **Set Serializer를**호출합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

**Xml Serializer 또는 XmlObject Serializer에서** 파생되는 모든 개체를 지정할 수 있습니다. **XmlObjectSerializer**

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON 또는 XML 포터 제거

JSON 포매터 또는 XML 포터터를 사용하지 않으려면 포터 목록에서 제거할 수 있습니다. 이 작업을 수행하는 주된 이유는 다음과 같습니다.

- 웹 API 응답을 특정 미디어 유형에 제한합니다. 예를 들어 JSON 응답만 지원하고 XML 포터만 제거하도록 결정할 수 있습니다.
- 기본 포터를 사용자 지정 포터로 대체합니다. 예를 들어 JSON 포터터를 JSON 포터의 사용자 지정 구현으로 바꿀 수 있습니다.

다음 코드는 기본 포matters를 제거하는 방법을 보여 주며, Global.asax에 정의된 **응용 프로그램\_시작** 메서드에서 이 메서드를 호출합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>순환 객체 참조 처리

기본적으로 JSON 및 XML 포matters는 모든 개체를 값으로 씁니다. 두 속성이 동일한 개체를 참조하거나 동일한 개체가 컬렉션에 두 번 나타나는 경우 formatter는 개체를 두 번 직렬화합니다. 이 문제는 개체 그래프에 주기가 포함된 경우 직렬화기가 그래프에서 루프를 검색할 때 예외를 throw하기 때문에 특히 문제가 됩니다.

다음 개체 모델 및 컨트롤러를 고려합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

이 작업을 호출하면 formatter가 예외를 throw하여 클라이언트에 대한 상태 코드 500(내부 서버 오류) 응답으로 변환됩니다.

JSON에서 개체 참조를 유지하려면 Global.asax 파일의 **응용 프로그램\_시작** 메서드에 다음 코드를 추가합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

이제 컨트롤러 작업은 다음과 같은 JSON을 반환합니다.

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

serializer는 두 &quot;개체에&quot; $id 속성을 추가합니다. 또한 Employee.Department 속성이 루프를 만드는 것을 감지하여 값을 개체 참조인&quot;{$ref&quot;&quot;:&quot;1 }로 바꿉습니다.

> [!NOTE]
> JSON에서는 개체 참조가 표준이 아닙니다. 이 기능을 사용하기 전에 클라이언트가 결과를 구문 분석할 수 있는지 여부를 고려합니다. 그래프에서 주기를 제거하는 것이 더 좋을 수 있습니다. 예를 들어 이 예제에서는 Employee에서 부서로 돌아가는 링크가 실제로 필요하지 않습니다.

XML에서 개체 참조를 보존하려면 두 가지 옵션이 있습니다. 더 간단한 옵션은 모델 `[DataContract(IsReference=true)]` 클래스에 추가하는 것입니다. *IsReference* 매개 변수는 개체 참조를 활성화합니다. **DataContract는** 직렬화를 옵트인하므로 속성에 **DataMember** 특성을 추가해야 합니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

이제 포터는 다음과 유사한 XML을 생성합니다:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

모델 클래스의 특성을 피하려면 새 형식별 **DataContractSerializer** 인스턴스를 만들고 생성자에서 *true로 preserveObjectReferences를* 설정하는 또 다른 옵션이 있습니다. **true** 그런 다음 이 인스턴스를 XML 미디어 형식 포터의 형식별 직렬화자로 설정합니다. 다음 코드는 이 작업을 수행하는 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>개체 직렬화 테스트

웹 API를 디자인할 때 데이터 개체가 직렬화되는 방식을 테스트하는 것이 유용합니다. 컨트롤러를 만들거나 컨트롤러 작업을 호출하지 않고도 이 작업을 수행할 수 있습니다.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
