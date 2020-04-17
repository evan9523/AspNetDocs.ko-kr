---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET 웹 API를 사용하여 OData v4의 복잡한 형식 상속 | 마이크로 소프트 문서
author: rick-anderson
description: OData v4 사양에 따라 복소수 형식은 다른 복잡한 형식에서 상속할 수 있습니다. (복잡한 형식은 키가 없는 구조형입니다.) 웹 API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543602"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>ASP.NET 웹 API를 사용하여 OData v4의 복잡한 형식 상속

[로 마이크로 소프트](https://github.com/microsoft)

> OData v4 [사양에](http://www.odata.org/documentation/odata-version-4-0/)따라 복소수 형식은 다른 복잡한 형식에서 상속될 수 있습니다. (복잡한 *complex* 형식은 키가 없는 구조형입니다.) 웹 API OData 5.3은 복잡한 형식 상속을 지원합니다.
> 
> 이 항목에서는 복잡한 상속 형식을 사용하여 엔터티 데이터 모델(EDM)을 빌드하는 방법을 보여 주며 이 항목에서는 전체 소스 코드는 [OData 복합유형 상속 샘플을](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)참조하십시오.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>튜토리얼에 사용되는 소프트웨어 버전
> 
> 
> - 웹 API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>모델 계층 구조

복잡한 형식 상속을 설명하기 위해 다음 클래스 계층 구조를 사용합니다.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`는 추상 복합 유형입니다. `Rectangle``Circle` 및 `Triangle`에서 `Shape`파생된 복합 형식이며 `RoundRectangle` 에서 `Rectangle`파생됩니다. `Window`은 엔터티 유형이며 `Shape` 인스턴스를 포함합니다.

다음은 이러한 형식을 정의하는 CLR 클래스입니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM 모델 빌드

EDM을 만들려면 CLR 형식의 상속 관계를 유추하는 **ODataConventionModelBuilder를**사용할 수 있습니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

**ODataModelBuilder를**사용하여 EDM을 명시적으로 빌드할 수도 있습니다. 이렇게 하면 더 많은 코드가 필요하지만 EDM을 보다 세한 제어할 수 있습니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

이 두 예제는 동일한 EDM 스키마를 만듭니다.

## <a name="metadata-document"></a>메타데이터 문서

다음은 복잡한 형식 상속을 보여 줄 수 있는 OData 메타데이터 문서입니다.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

메타데이터 문서에서 다음을 확인할 수 있습니다.

- 복소수 형식은 `Shape` 추상적입니다.
- 및 `Rectangle` `Triangle` `Circle` 복합 형식에는 기본 형식이 `Shape`있습니다.
- `RoundRectangle` 형식에는 기본 형식이 `Rectangle`있습니다.

## <a name="casting-complex-types"></a>주조 복합 유형

이제 복잡한 형식에 대한 캐스팅이 지원됩니다. 예를 들어 다음 쿼리는 `Shape` `Rectangle`a를 에 캐스팅합니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

응답 페이로드는 다음과 같습니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
