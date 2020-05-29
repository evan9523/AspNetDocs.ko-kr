---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2.2를 사용 하는 OData v4에 포함 Microsoft Docs
author: rick-anderson
description: 일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에만 액세스할 수 있습니다. 그러나 OData v4는 Singleton 및 Con 이라는 두 가지 추가 옵션을 제공 합니다.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173006"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2.2을 사용한 OData v4의 포함

Jinfu Tan

> 일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에만 액세스할 수 있습니다. 그러나 OData v4는 두 가지 추가 옵션인 Singleton과 포함을 제공 하며, 둘 다 WebAPI 2.2에서 지원 됩니다.

이 항목에서는 WebApi 2.2의 OData 끝점에서 포함을 정의 하는 방법을 보여 줍니다. 포함에 대 한 자세한 내용은 [OData v4로 포함](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/)을 참조 하세요. Web API에서 OData V4 끝점을 만들려면 [ASP.NET Web API 2.2를 사용 하 여 odata V4 엔드포인트 만들기](create-an-odata-v4-endpoint.md)를 참조 하세요.

먼저이 데이터 모델을 사용 하 여 OData 서비스에서 포함 도메인 모델을 만듭니다.

![데이터 모델](odata-containment-in-web-api-22/_static/image1.png)

계정에 많은 PaymentInstruments (PI)가 포함 되어 있지만 PI에 대 한 엔터티 집합을 정의 하지 않습니다. 대신, Pi는 계정을 통해서만 액세스할 수 있습니다.

[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)에서이 항목에 사용 된 솔루션을 다운로드할 수 있습니다.

## <a name="defining-the-data-model"></a>데이터 모델 정의

1. CLR 형식을 정의 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`특성은 포함 탐색 속성에 사용 됩니다.
2. CLR 형식에 따라 EDM 모델을 생성 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    는 `ODataConventionModelBuilder` `Contained` 특성이 해당 탐색 속성에 추가 되는 경우 EDM 모델 빌드를 처리 합니다. 속성이 컬렉션 형식인 경우에 `GetCount(string NameContains)` 도 함수가 생성 됩니다.

    생성 되는 메타 데이터는 다음과 같습니다.

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`특성은 탐색 속성이 포함 임을 나타냅니다.

## <a name="define-the-containing-entity-set-controller"></a>포함 하는 엔터티 집합 컨트롤러 정의

포함 된 엔터티에는 자체 컨트롤러가 없습니다. 작업은 포함 하는 엔터티 집합 컨트롤러에 정의 됩니다. 이 샘플에는 AccountsController 있지만 PaymentInstrumentsController는 없습니다.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData 경로 세그먼트가 4 개 이상인 경우 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 에는 위의 컨트롤러에서와 같이 특성 라우팅만 작동 합니다. 그렇지 않은 경우에는 특성과 기본 라우팅이 모두 작동 합니다. 예를 들어와 `GetPayInPIs(int key)` 일치 `GET ~/Accounts(1)/PayinPIs` 합니다.

*이 문서의 원래 내용에 대 한 Leo Hu-hu을 주셔서 감사 합니다.*
