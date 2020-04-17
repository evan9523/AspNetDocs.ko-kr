---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 캐시된 페이지(VB)에 동적 콘텐츠 추가 | 마이크로 소프트 문서
author: rick-anderson
description: 동일한 페이지에서 동적 및 캐시된 콘텐츠를 혼합하는 방법을 알아봅니다. 포스트 캐시 대체를 사용하면 배너 광고와 같은 동적 콘텐츠를 표시 할 수 있습니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542263"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>캐시된 페이지에 동적 콘텐츠 추가(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> 동일한 페이지에서 동적 및 캐시된 콘텐츠를 혼합하는 방법을 알아봅니다. 캐시 후 대체를 사용하면 출력 캐시된 페이지 내에 배너 광고 또는 뉴스 항목과 같은 동적 콘텐츠를 표시할 수 있습니다.

출력 캐싱을 활용하면 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시킬 수 있습니다. 페이지를 요청할 때마다 페이지를 다시 생성하는 대신 페이지를 한 번 생성하고 여러 사용자를 위해 메모리에 캐시할 수 있습니다.

그러나 문제가 있습니다. 페이지에 동적 콘텐츠를 표시해야 하는 경우 어떻게 해야 합니까? 예를 들어 페이지에 배너 광고를 표시한다고 가정해 보겠습니다. 모든 사용자가 동일한 광고를 볼 수 있도록 배너 광고를 캐시하지 않으려고 합니다. 당신은 그런 식으로 돈을 벌수 없을 것입니다!

다행히도 쉬운 해결책이 있습니다. *포스트 캐시 대체라는*ASP.NET 프레임워크의 기능을 활용할 수 있습니다. 캐시 후 대체를 사용하면 메모리에 캐시된 페이지에서 동적 콘텐츠를 대체할 수 있습니다.

일반적으로 &lt;OutputCache&gt; 특성을 사용하여 페이지를 캐시할 때 페이지는 서버와 클라이언트(웹 브라우저)에 캐시됩니다. 사후 캐시 대체를 사용하면 페이지는 서버에서만 캐시됩니다.

#### <a name="using-post-cache-substitution"></a>사후 캐시 대체 사용

사후 캐시 대체를 사용하려면 두 단계가 필요합니다. 먼저 캐시된 페이지에 표시할 동적 콘텐츠를 나타내는 문자열을 반환하는 메서드를 정의해야 합니다. 그런 다음 HttpResponse.WriteSubstitution() 메서드를 호출하여 동적 콘텐츠를 페이지에 삽입합니다.

예를 들어 캐시된 페이지에 다른 뉴스 항목을 임의로 표시하려는 경우를 가정해 보겠습니다. 목록 1의 클래스는 세 개의 뉴스 항목 목록에서 하나의 뉴스 항목을 임의로 반환하는 RenderNews()라는 단일 메서드를 노출합니다.

**목록 1 – 모델\뉴스.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

사후 캐시 대체를 활용하려면 HttpResponse.WriteSubstitution() 메서드를 호출합니다. WriteSubstitution() 메서드는 캐시된 페이지의 영역을 동적 콘텐츠로 대체하도록 코드를 설정합니다. WriteSubitution() 메서드는 목록 2의 보기에 임의의 뉴스 항목을 표시 하는 데 사용 됩니다.

**목록 2 – 보기\홈\인덱스.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

RenderNews 메서드는 WriteSubitution() 메서드에 전달 됩니다. RenderNews 메서드가 호출되지 않습니다. 대신 메서드에 대 한 참조는 AddressOf 연산자의 도움으로 WriteSubitution()에 전달 됩니다.

인덱스 보기가 캐시됩니다. 보기는 목록 3의 컨트롤러에 의해 반환됩니다. Index() 작업은 &lt;Index 보기를 60초&gt; 동안 캐시하도록 하는 OutputCache 특성으로 장식되어 있습니다.

**목록 3 – 컨트롤러\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

인덱스 보기가 캐시되어 있더라도 인덱스 페이지를 요청할 때 다른 임의의 뉴스 항목이 표시됩니다. 색인 페이지를 요청하면 페이지에 표시되는 시간이 60초 동안 변경되지 않습니다(그림 1 참조). 시간이 변경되지 않는다는 사실은 페이지가 캐시되었음을 증명합니다. 그러나 WriteSubitution() 메서드에 의해 주입된 콘텐츠(임의의 뉴스 항목)는 각 요청에 따라 변경됩니다.

**그림 1 - 캐시된 페이지에 동적 뉴스 항목 주입**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>도우미 메서드에서 사후 캐시 대체 사용

포스트 캐시 대체를 활용하는 더 쉬운 방법은 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드에 대한 호출을 캡슐화하는 것입니다. 이 방법은 목록 4의 도우미 메서드에 의해 설명됩니다.

**목록 4 – 도우미\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

목록 4에는 렌더배너() 및 렌더배너내부()의 두 가지 방법을 노출하는 시각적 기본 모듈이 포함되어 있습니다. RenderBanner() 메서드는 실제 도우미 메서드를 나타냅니다. 이 메서드는 표준 ASP.NET MVC HtmlHelper 클래스를 확장하여 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있습니다.

렌더배너() 메서드는 렌더배너내부() 메서드를 WriteSubstitution() 메서드에 전달하는 HttpResponse.WriteSubstitution() 메서드를 호출합니다.

렌더배너내부() 메서드는 전용 메서드입니다. 이 메서드는 도우미 메서드로 노출 되지 않습니다. RenderBannerInternal() 메서드는 세 개의 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 임의로 반환합니다.

목록 5의 수정된 인덱스 보기는 RenderBanner() 도우미 메서드를 사용하는 방법을 보여 줍니다. MvcApplication1.helpers 네임스페이스를 가져오기 위해 뷰 상단에 추가 &lt;%@ 가져오기 %&gt; 지시문이 포함되어 있습니다. 이 네임스페이스를 가져오지 않으면 RenderBanner() 메서드가 Html 속성에 메서드로 나타나지 않습니다.

**목록 5 – 보기\홈\Index.aspx (렌더 배너() 방법)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

목록 5의 보기에 의해 렌더링된 페이지를 요청하면 각 요청과 함께 다른 배너 광고가 표시됩니다(그림 2 참조). 페이지는 캐시되지만 배너 보급 알림은 RenderBanner() 도우미 메서드에 의해 동적으로 삽입됩니다.

**그림 2 - 임의 배너 광고를 표시하는 인덱스 보기**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 캐시된 페이지에서 콘텐츠를 동적으로 업데이트하는 방법을 설명했습니다. HttpResponse.WriteSubstitution() 메서드를 사용하여 캐시된 페이지에 동적 콘텐츠를 삽입할 수 있도록 하는 방법을 배웠습니다. HTML 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법도 배웠습니다.

가능하면 캐싱을 활용하여 웹 응용 프로그램의 성능에 극적인 영향을 줄 수 있습니다. 이 자습서에서 설명한 대로 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 캐싱을 활용할 수 있습니다.

> [!div class="step-by-step"]
> [이전](improving-performance-with-output-caching-vb.md)
> [다음](creating-a-controller-vb.md)
