---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 액션 만들기(VB) | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET MVC 컨트롤러에 새 작업을 추가하는 방법에 대해 알아봅니다. 메서드가 작업으로 수행되는 데 대한 요구 사항에 대해 알아봅니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542250"
---
# <a name="creating-an-action-vb"></a>작업 만들기(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET MVC 컨트롤러에 새 작업을 추가하는 방법에 대해 알아봅니다. 메서드가 작업으로 수행되는 데 대한 요구 사항에 대해 알아봅니다.

이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명하는 것입니다. 작업 메서드의 요구 사항에 대해 알아봅니다. 메서드가 작업으로 노출되는 것을 방지하는 방법도 알아봅니다.

## <a name="adding-an-action-to-a-controller"></a>컨트롤러에 작업 추가

컨트롤러에 새 메서드를 추가하여 컨트롤러에 새 작업을 추가합니다. 예를 들어 목록 1의 컨트롤러에는 Index()라는 작업과 SayHello()라는 작업이 포함됩니다. 두 메서드 모두 작업으로 노출됩니다.

**목록 1 - 컨트롤러\홈컨트롤러.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

행동으로 우주에 노출되기 위해, 방법은 특정 요구 사항을 충족해야합니다 :

- 메서드는 공용이어야 합니다.
- 메서드는 정적 메서드일 수 없습니다.
- 메서드는 확장 메서드일 수 없습니다.
- 메서드는 생성자, 게터 또는 setter가 될 수 없습니다.
- 메서드에 열려 있는 제네릭 형식을 가질 수 없습니다.
- 메서드는 컨트롤러 기본 클래스의 메서드가 아닙니다.
- 메서드는 **ref** 또는 **out** 매개 변수를 포함할 수 없습니다.

컨트롤러 작업의 반환 유형에는 제한이 없습니다. 컨트롤러 작업은 문자열, DateTime, Random 클래스의 인스턴스 또는 void를 반환할 수 있습니다. ASP.NET MVC 프레임워크는 작업 결과가 아닌 반환 형식을 문자열로 변환하고 문자열을 브라우저로 렌더링합니다.

이러한 요구 사항을 위반하지 않는 메서드를 컨트롤러에 추가하면 메서드가 컨트롤러 작업으로 노출됩니다. 여기에주의하십시오. 인터넷에 연결된 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다. 예를 들어 DeleteMyWebsite() 컨트롤러 작업을 만들지 마십시오.

## <a name="preventing-a-public-method-from-being-invoked"></a>공용 메서드가 호출되지 않도록 방지

컨트롤러 클래스에서 공용 메서드를 만들어야 하고 메서드를 컨트롤러 작업으로 노출하지 않으려면 &lt;NonAction&gt; 특성을 사용하여 메서드가 호출되지 않도록 할 수 있습니다. 예를 들어 목록 2의 컨트롤러에는 비동작 &lt;&gt; 특성으로 장식된 CompanySecrets()라는 공용 메서드가 포함되어 있습니다.

**목록 2 - 컨트롤러\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

브라우저의 주소 표시줄에 /Work/CompanySecrets를 입력하여 CompanySecrets() 컨트롤러 작업을 호출하려고 하면 그림 1의 오류 메시지가 표시됩니다.

[![비동작 메서드 호출](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**그림 01**: 비동작 메서드[호출(전체 크기 이미지를 보려면 클릭)](creating-an-action-vb/_static/image2.png)

> [!div class="step-by-step"]
> [이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)
