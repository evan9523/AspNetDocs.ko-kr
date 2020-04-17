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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET 웹 API를 사용하여 OData v4에서 열린 형식

[로 마이크로 소프트](https://github.com/microsoft)

> OData v4에서 *open 형식은* 형식 정의에 선언된 모든 속성 외에 동적 속성을 포함하는 구조화된 형식입니다. 개방형 형식을 사용하면 데이터 모델에 유연성을 추가할 수 있습니다. 이 자습서에서는 ASP.NET 웹 API OData에서 열린 형식을 사용하는 방법을 보여 주입니다.
> 
> 이 자습서에서는 웹 API에서 OData 끝점을 만드는 방법을 이미 알고 ASP.NET 가정합니다. 그렇지 않은 경우 먼저 [OData v4 끝점 만들기를](create-an-odata-v4-endpoint.md) 읽는 것으로 시작합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>튜토리얼에 사용되는 소프트웨어 버전
> 
> 
> - 웹 API OData 5.3
> - OData v4

첫째, 일부 OData 용어:

- 엔터티 유형: 키가 있는 구조화 된 형식입니다.
- 복합 유형: 키가 없는 구조식 형식입니다.
- 열기 유형: 동적 속성이 있는 형식입니다. 엔터티 형식과 복잡한 형식을 모두 열 수 있습니다.

동적 속성의 값은 기본 형식, 복합 형식 또는 열거형 형식일 수 있습니다. 또는 이러한 유형의 컬렉션입니다. 열려 있는 형식에 대한 자세한 내용은 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)참조하십시오.

## <a name="install-the-web-odata-libraries"></a>웹 OData 라이브러리 설치

NuGet 패키지 관리자를 사용하여 최신 웹 API OData 라이브러리를 설치합니다. 패키지 관리자 콘솔 창에서:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR 유형 정의

먼저 EDM 모델을 CLR 유형으로 정의합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

EDM(엔터티 데이터 모델)이 생성되면

- `Category`은 열거형입니다.
- `Address`는 복잡한 형식입니다. (키가 없으므로 엔터티 형식이 아닙니다.)
- `Customer`는 엔터티 형식입니다. (열쇠가 있습니다.)
- `Press`는 개방형 복합 유형입니다.
- `Book`는 열린 엔터티 형식입니다.

열린 형식을 만들려면 CLR 형식에는 동적 속성을 `IDictionary<string, object>`포함하는 형식의 속성이 있어야 합니다.

## <a name="build-the-edm-model"></a>EDM 모델 빌드

**ODataConventionModelBuilder를** 사용하여 EDM을 `Press` 만드는 `Book` 경우 `IDictionary<string, object>` 속성의 존재에 따라 개방형 유형으로 자동으로 추가됩니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

**ODataModelBuilder를**사용하여 EDM을 명시적으로 빌드할 수도 있습니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

다음으로 OData 컨트롤러를 추가합니다. 이 자습서에서는 GET 및 POST 요청만 지원하고 메모리 내 목록을 사용하여 엔터티를 저장하는 단순화된 컨트롤러를 사용합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

첫 번째 `Book` 인스턴스에는 동적 속성이 없습니다. 두 `Book` 번째 인스턴스에는 다음과 같은 동적 속성이 있습니다.

- "게시됨": 기본 형식
- "작성자": 기본 형식의 컬렉션
- "기타 범주": 열거형 형식의 컬렉션입니다.

또한 해당 `Press` `Book` 인스턴스의 속성에는 다음과 같은 동적 속성이 있습니다.

- "블로그": 원시 형식
- "주소": 복잡한 유형

## <a name="query-the-metadata"></a>메타데이터 쿼리

OData 메타데이터 문서를 받으려면 GET `~/$metadata`요청을 로 보냅니다. 응답 본문은 다음과 유사해야 합니다.

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

메타데이터 문서에서 다음을 확인할 수 있습니다.

- `Book` 및 `Press` 형식의 경우 `OpenType` 특성값은 true입니다. `Customer` 및 `Address` 형식에는 이 특성이 없습니다.
- `Book` 엔터티 유형에는 ISBN, 제목 및 Press의 세 가지 선언된 속성이 있습니다. OData 메타데이터에는 CLR 클래스의 `Book.Properties` 속성이 포함되지 않습니다.
- 마찬가지로 `Press` 복합 형식에는 이름과 범주라는 두 개의 선언된 속성만 있습니다. 메타데이터에는 CLR `Press.DynamicProperties` 클래스의 속성이 포함되지 않습니다.

## <a name="query-an-entity"></a>엔터티 쿼리

ISBN이 "978-0-7356-7942-9"와 동일한 책을 얻으려면 GET 요청을 `~/Books('978-0-7356-7942-9')`로 보내십시오. 응답 본문은 다음과 유사해야 합니다. (더 읽기 쉽게 하기 위해 들여쓰기됩니다.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

동적 속성은 선언된 속성과 인라인으로 포함됩니다.

## <a name="post-an-entity"></a>엔터티 게시

Book 엔터티를 추가하려면 에 POST `~/Books`요청을 보냅니다. 클라이언트는 요청 페이로드에서 동적 속성을 설정할 수 있습니다.

다음은 예제 요청입니다. "가격" 및 "게시된" 속성을 기록합니다.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

컨트롤러 메서드에서 중단점을 설정하면 Web API가 `Properties` 이러한 속성을 사전에 추가한 것을 확인할 수 있습니다.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>추가 리소스

[OData 오픈 타입 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
