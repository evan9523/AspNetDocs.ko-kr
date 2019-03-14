---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: '10부: 탐색 및 사이트 설계, 결론 최종 업데이트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 10 부에서는 탐색 및 S. 최종 업데이트...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f32509701dd112053aa4f31d6552601f961c7413
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049440"
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>10부: 탐색 및 사이트 디자인 최종 업데이트, 결론
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 10 부 탐색 및 사이트 설계, 결론 최종 업데이트를 설명합니다.


이 사이트에 대 한 주요 기능을 모두 완료 했으므로 했지만 아직도 몇 가지 기능이 사이트 탐색, 홈 페이지 및 저장소 찾아보기 페이지에 추가 합니다.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>쇼핑 카트 요약 부분 뷰 만들기

전체 사이트 사용자의 장바구니의 항목 수를 표시 하려고 합니다.

![](mvc-music-store-part-10/_static/image1.png)

우리의 Site.master에 추가 되는 부분 뷰를 만들어 쉽게 구현할 수 있습니다.

이전에 표시 된 것 처럼 ShoppingCart 컨트롤러 부분 뷰를 반환 하는 CartSummary 작업 메서드를 포함 합니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

CartSummary 부분 뷰를 만들려면 뷰/ShoppingCart 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 선택 합니다. CartSummary 뷰 이름을 지정 하 고 아래와 같이 "부분 뷰 만들기" 확인란을 확인 합니다.

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 부분 뷰는 실제로 간단한-바구니에 항목 수를 보여 주는 ShoppingCart 인덱스 뷰에 링크 일 뿐입니다. CartSummary.cshtml에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

Html.RenderAction 메서드를 사용 하 여 사이트 마스터를 비롯 하 여 사이트의 모든 페이지에 부분 뷰를 포함할 수 했습니다. RenderAction 작업 이름 ("CartSummary") 및 아래으로 ("ShoppingCart") 컨트롤러 이름을 지정 해야 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

이 사이트 레이아웃에 추가 하기 전에 만들겠습니다 장르 메뉴 Site.master 업데이트의 모든 한 번에 적용할 수 있습니다.

## <a name="creating-the-genre-menu-partial-view"></a>장르 메뉴 부분 뷰 만들기

수 좋을까요 스토어에서 사용할 수 있는 모든 장르를 나열 하는 장르 메뉴를 추가 하 여 스토어를 통해 탐색 하는 사용자에 대 한 훨씬 더 쉽습니다.

![](mvc-music-store-part-10/_static/image3.png)

동일한 따릅니다 단계도 GenreMenu 부분 뷰를 만들고 다음 사이트 마스터를 추가할 둘 수 있습니다. 먼저 다음 GenreMenu 컨트롤러 작업의 StoreController 추가:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

이 작업에는 다음에 만들 부분 뷰, 표시 되는 장르 목록을 반환 합니다.

*참고: 한다는이 작업을 부분 보기에서 사용할 수 있는이 컨트롤러 작업에서 [ChildActionOnly] 특성을 추가 했습니다. 이 특성에는 /Store/GenreMenu로 이동 하 여 실행 중인 컨트롤러 작업 수 없게 됩니다. 부분 보기에 대 한이 필요치 않으 나이 컨트롤러 작업은 예정 대로 사용 되도록 하려고 하므로 좋은 방법일 것입니다. 뷰는 뷰 엔진이 다른 보기에 포함 되는이 보기에 대 한 레이아웃을 사용 하면 안 됩니다 것을 알 수 있는 것이 아니라 PartialView 반환도 했습니다.*

GenreMenu 컨트롤러 작업 단추로 클릭 하 고 아래와 같이 데이터 클래스는 장르 보기를 사용 하 여 강력한 형식화 된 GenreMenu 명명 된 부분 뷰를 만듭니다.

![](mvc-music-store-part-10/_static/image4.png)

다음과 같이 순서가 지정 되지 않은 목록을 사용 하 여 항목을 표시 GenreMenu 부분 뷰에 대 한 코드 보기를 업데이트 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>부분 뷰를 표시 하려면 사이트 레이아웃 업데이트

부분 뷰 Site 레이아웃에 추가할 수 있습니다 (/뷰/공유/\_Layout.cshtml) Html.RenderAction()를 호출 하 여 합니다. 아래와 같이 몇 가지 추가 태그를 표시할 뿐만 아니라 둘을 추가 하겠습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

이제 응용 프로그램을 실행 하면 왼쪽된 탐색 영역에서 장르 및 맨 위에 있는 카트 요약 표시 됩니다 것입니다.

## <a name="update-to-the-store-browse-page"></a>저장소 찾아보기 페이지 업데이트

저장소 찾아보기 페이지 작동 하지만 매우 훌륭한 확인 하지 않습니다. 페이지 뷰 코드 (/Views/Store/Browse.cshtml에 있음) 다음과 같이 업데이트 하 여 더 나은 레이아웃 앨범 표시를 업데이트할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

진행 중인 여기 사용 Html.ActionLink 아닌 Url.Action 앨범 아트 워크 포함에 대 한 링크에 특수 한 서식을 적용할 수 있습니다.

*참고: 이러한 앨범에 대 한 제네릭 앨범 표지를 표시 하는 것입니다. 이 정보 데이터베이스에 저장 되 고 저장소 관리자를 통해 편집할 수 있습니다. 사용자 고유의 아트 워크를 추가할 수 있습니다.*

이제 장르를 찾아, 앨범 아트 워크를 사용 하 여 표 형식으로 표시 앨범 표시 됩니다 했습니다.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>상위 판매 앨범 표시 하도록 홈 페이지를 업데이트 하는 중

판매량을 늘리기 위해 홈 페이지의 앨범 판매 많이 기능 하고자 합니다. 처리도 몇 가지 추가 그래픽에 추가 하는 HomeController에 일부 업데이트를 만들 수 것입니다.

먼저 추가한 탐색 속성 앨범 클래스 EntityFramework 연결 된 것을 알 수 있도록 합니다. 마지막 몇 줄의 우리의 **앨범** 클래스가 다음과 같아집니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*참고: 사용 하 여 추가 해야 문을 System.Collections.Generic 네임 스페이스를 가져옵니다.*

먼저 storeDB 필드와는 다른 컨트롤러와 같이 문을 사용 하 여 MvcMusicStore.Models 추가할 것입니다. 다음으로, OrderDetails에 따라 상위 판매 앨범을 찾으려면 데이터베이스를 쿼리 하는 HomeController에 다음 메서드를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

이것이 개인 메서드를 컨트롤러 작업으로 사용할 수 있도록 않으려면입니다. 편의상, HomeController의 포함 하는 것 하지만 적절 하 게 별도 서비스 클래스에 비즈니스 논리를 이동 하는 것이 좋습니다.

준비에서 된 앨범 판매 상위 5 개 쿼리 및 뷰를 반환 하는 인덱스 컨트롤러 작업을 업데이트할 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

HomeController 업데이트에 대 한 전체 코드는 아래와 같습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

마지막으로, 모델 형식 업데이트 및 앨범 목록 맨 아래에 추가 하 여 앨범의 목록을 표시할 수 있도록 홈 인덱스 보기 업데이트 해야 합니다. 에서는 페이지 머리글 및 프로 모션 섹션을 추가할 수도이 수가 걸립니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

이제 응용 프로그램을 실행에서는 최상위 판매 앨범 및 판촉 메시지를 사용 하 여 업데이트 된 홈 페이지가 표시 됩니다.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>결론

ASP.NET MVC 쉽게 살펴본 등 데이터베이스 액세스, 멤버 자격, AJAX 사용 하 여 정교한 웹 사이트를 만들려고 합니다. 매우 신속 하 게 합니다. 다행히이 자습서가 제공한 고유한 ASP.NET MVC 응용 프로그램 구축을 시작 하는 데 필요한 도구!


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-9.md)
