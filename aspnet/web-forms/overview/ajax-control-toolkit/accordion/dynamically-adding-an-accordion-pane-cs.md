---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 동적으로 추가 하는 Accordion 창 (C#) | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 일반적으로 패널 w 선언 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 16cefadb7086a658b20558526757f9229a43fcc9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027310"
---
<a name="dynamically-adding-an-accordion-pane-c"></a>동적으로 추가 하는 Accordion 창 (C#)
====================
by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.

## <a name="steps"></a>단계

Accordion 컨트롤 서버 쪽 코드에 모든 중요 한 속성을 표시 합니다. 무엇 보다도 `Panes` 속성은 Accordion을 구성 하는 창의 컬렉션에 대 한 액세스 권한을 부여 합니다. 형식의 모든 창 `AccordionPane`합니다. 따라서 이러한 창을 만드는 간단 합니다.

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`HeaderContainer` 의 속성 `AccordionPane` ; 창의 헤더 섹션 내에 있는 ASP.NET 컨트롤에 대 한 액세스를 제공 합니다 `ContentContainer` 의 속성 `AccordionPane` 창의 콘텐츠 섹션에 대 한 동일한 작업을 수행 합니다. 이 ASP.NET 코드를 창에 내용을 추가할 수 있습니다.

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

마지막으로 pane(s) 추가 해야 합니다는 `Panes` 는 Accordion 컬렉션:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

두 개의 창이 Accordion 컨트롤에 추가 하는 전체 서버 쪽 코드는 다음과 같습니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

누락 된 유일한 요소는 ASP.NET의 유무에 따라 달라 지는 자체 Accordion `ScriptManager` 제어 합니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

Accordion 컨트롤에서 참조 하는 두 개의 CSS 클래스 예제를 완료 하려면 브라우저에 대 한 스타일 정보를 제공 합니다.

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


[![accordion에 데이터를 서버 쪽 코드에서 동적으로 추가](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

서버 쪽 코드에서 동적으로 추가한는 accordion에 데이터 ([클릭 하 여 큰 이미지 보기](dynamically-adding-an-accordion-pane-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](databinding-to-an-accordion-cs.md)
> [다음](databinding-to-an-accordion-vb.md)
