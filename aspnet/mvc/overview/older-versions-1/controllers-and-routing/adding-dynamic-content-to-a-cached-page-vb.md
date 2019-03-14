---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 캐시 된 페이지 (VB)에 동적 콘텐츠 추가 | Microsoft Docs
author: microsoft
description: 같은 페이지의 동적이 고 캐시 된 콘텐츠를 조합 하는 방법에 알아봅니다. 캐시 후 대체를 사용 하면 배너 광고 o 같은 동적 콘텐츠를 표시할 수 있습니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 121a3a35c8255f1423d7008930315f76bbb8e8f9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053100"
---
<a name="adding-dynamic-content-to-a-cached-page-vb"></a>캐시된 페이지에 동적 콘텐츠 추가(VB)
====================
by [Microsoft](https://github.com/microsoft)

> 같은 페이지의 동적이 고 캐시 된 콘텐츠를 조합 하는 방법에 알아봅니다. 캐시 후 대체를 사용 하는 배너 광고 또는 뉴스 항목을 캐시에 출력 하는 페이지 내에서 같은 동적 콘텐츠를 표시할 수 있습니다.


출력 캐싱을 활용 하 고, ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. 매번 페이지가 요청 될 페이지를 다시 생성 하는 대신에 페이지를 한 번 생성 하 고 여러 사용자에 대 한 메모리에 캐시 될 수 있습니다.

하지만 문제가 있습니다. 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 어떻게? 예를 들어 페이지에서 배너 광고를 표시할 한다고 가정해 보겠습니다. 모든 사용자가 동일한 광고를 볼 수 있도록 캐시할 배너 광고 하지 않으려고 합니다. 이런 방식으로 모든 비용을 확인 하지 않습니다!

다행 스럽게도 쉽게 솔루션을 있습니다. 라는 ASP.NET 프레임 워크의 기능 활용을 걸릴 수 있습니다 *캐시 후 대체*합니다. 캐시 후 대체를 사용 하면 메모리에 캐시 된 페이지에 동적 콘텐츠를 대체할 수 있습니다.


일반적으로 출력 하는 경우 페이지를 사용 하 여 캐시 합니다 &lt;OutputCache&gt; 특성 페이지는 서버와 클라이언트 (웹 브라우저)에 캐시 됩니다. 캐시 후 대체를 사용 하면 페이지는 서버에만 캐시 됩니다.


#### <a name="using-post-cache-substitution"></a>캐시 후 대체를 사용 하 여

캐시 후 대체를 사용 하 여 두 단계가 필요 합니다. 첫째, 캐시 된 페이지에 표시 하려는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다. 다음으로, 동적 콘텐츠 페이지에 삽입할 HttpResponse.WriteSubstitution() 메서드를 호출.

예를 들어, 임의로 캐시 된 페이지에서 다른 뉴스 항목을 표시 한다고 가정해 보겠습니다. 목록 1에서 클래스 라는 RenderNews() 임의로 세 뉴스 항목의 목록에서 하나의 뉴스 항목을 반환 하는 단일 메서드를 노출 합니다.

**1 – Models\News.vb 나열**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

캐시 후 대체를 이용 하려면 HttpResponse.WriteSubstitution() 메서드를 호출 합니다. 동적 콘텐츠를 사용 하 여 캐시 된 페이지의 영역을 바꾸려면 WriteSubstitution() 메서드 코드를 설정 합니다. 목록 2 뷰에서 임의의 뉴스 항목을 표시 하려면 WriteSubstitution() 메서드가 사용 됩니다.

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

RenderNews 메서드 WriteSubstitution() 메서드에 전달 됩니다. RenderNews 메서드를 호출 하지는 알 수 있습니다. 대신 메서드에 대 한 참조를 AddressOf 연산자를 사용 하 여 WriteSubstitution() 전달 됩니다.

인덱스 보기 캐시 됩니다. 보기 3의 컨트롤러 뷰를 반환 합니다. Index () 작업을 사용 하 여 데코 레이트 된 통지를 &lt;OutputCache&gt; 60 초 동안 캐시를 위해 인덱스 보기로 시키는 특성입니다.

**Listing 3 – Controllers\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

인덱스 보기 캐시 된 경우에 인덱스 페이지를 요청 하는 경우 다른 임의의 뉴스 항목이 표시 됩니다. 인덱스 페이지를 요청 하면 페이지에 의해 표시 된 시간이 60 초 (그림 1 참조)에 대 한 변경 되지 않습니다. 페이지 캐시 되는 증명 하는 시간을 변경 하지 않는 팩트 합니다. 그러나 각 요청과 함께 WriteSubstitution() 메서드 – 임의의 뉴스 항목 – 변경에 의해 콘텐츠가 삽입 되는 합니다.

**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>캐시 후 대체를 사용 하 여 도우미 메서드에서

캐시 후 대체를 활용 하는 간단한 방법인 캡슐화 하는 데 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드를 호출 합니다. 이 방법은 4의 도우미 메서드에 의해 나와 있습니다.

**Listing 4 – Helpers\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

목록 4 두 메서드를 노출 하는 Visual Basic 모듈을 포함 되어 있습니다. RenderBanner() 및 RenderBannerInternal() 합니다. RenderBanner() 메서드를 실제 도우미 메서드를 나타냅니다. 이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.

RenderBanner() 메서드 RenderBannerInternal() WriteSubsitution() 메서드에 전달 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.

RenderBannerInternal() 메서드는 전용 메서드입니다. 이 메서드는 도우미 메서드도 노출할 수 없습니다. RenderBannerInternal() 메서드는 임의로 세 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 반환합니다.

목록 5에서 수정 된 인덱스 뷰 RenderBanner() 도우미 메서드를 사용 하는 방법을 보여 줍니다. 추가 &lt;가져오기 % @ %&gt; 지시문 MvcApplication1.Helpers 네임 스페이스를 가져오는 뷰의 맨 위에 있는 포함 됩니다. 이 네임 스페이스를 가져오지 않은, 경우에 Html 속성의 메서드로 RenderBanner() 메서드 나타나지 않습니다.

**5-Views\Home\Index.aspx (RenderBanner() 메서드로)를 나열합니다.**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

목록 5의 보기에서 렌더링 된 페이지를 요청 하면 다른 배너 광고를 각 요청과 함께 표시 됩니다 (그림 2 참조). 페이지 캐시 되지만 배너 광고 RenderBanner() 도우미 메서드에 의해 동적으로 삽입 됩니다.

**그림 2 – 임의의 배너 광고를 표시 된 인덱스 뷰**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>요약

이 자습서는 캐시 된 페이지의 콘텐츠를 동적으로 업데이트 하는 방법을 설명 합니다. 캐시 된 페이지에 지정 된 수를 동적 콘텐츠를 사용 하도록 설정 하려면 HttpResponse.WriteSubstitution() 메서드를 사용 하는 방법을 알아보았습니다. HTML 도우미 메서드 내 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법을 알아보았습니다.

가능한 – 웹 응용 프로그램의 성능에 상당한 영향을 미칠 수 있습니다이 캐싱을 활용 합니다. 이 자습서에서 설명 했 듯이 캐싱 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 사용할 수 있습니다.

> [!div class="step-by-step"]
> [이전](improving-performance-with-output-caching-vb.md)
> [다음](creating-a-controller-vb.md)
