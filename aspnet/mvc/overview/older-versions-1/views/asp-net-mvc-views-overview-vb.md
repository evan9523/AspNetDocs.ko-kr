---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 뷰 개요 (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 뷰는 무엇 이며 HTML 페이지와 어떻게 다릅니까? 이 자습서에서는 Stephen Walther가 보기를 소개 하 고, 다음을 수행할 수 있는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044668"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC 보기 개요(VB)

[Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC 뷰는 무엇 이며 HTML 페이지와 어떻게 다릅니까? 이 자습서에서 Stephen Walther는 뷰를 소개 하 고 뷰 내에서 뷰 데이터 및 HTML 도우미를 활용 하는 방법을 보여 줍니다.

이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다. 이 자습서의 끝 부분에서는 새 뷰를 만들고, 컨트롤러에서 뷰로 데이터를 전달 하 고, HTML 도우미를 사용 하 여 보기에서 콘텐츠를 생성 하는 방법을 이해 해야 합니다.

## <a name="understanding-views"></a>뷰 이해

ASP.NET 또는 Active Server 페이지와 달리 ASP.NET MVC에는 페이지에 직접 해당 하는 항목이 포함 되지 않습니다. ASP.NET MVC 응용 프로그램에서 브라우저의 주소 표시줄에 입력 하는 URL의 경로에 해당 하는 페이지가 디스크에 없습니다. ASP.NET MVC 응용 프로그램의 페이지에 가장 가까운 항목은 *뷰*라고 합니다.

ASP.NET MVC 응용 프로그램에서 들어오는 브라우저 요청은 컨트롤러 작업에 매핑됩니다. 컨트롤러 작업에서 뷰를 반환할 수 있습니다. 그러나 컨트롤러 작업은 다른 유형의 작업 (예: 다른 컨트롤러 작업으로 리디렉션)을 수행할 수 있습니다.

목록 1은 HomeController 라는 간단한 컨트롤러를 포함 합니다. HomeController는 Index () 및 Details () 라는 두 개의 컨트롤러 동작을 노출 합니다.

**목록 1-HomeController**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 작업 인 Index () 작업을 호출할 수 있습니다.

/Home/Index

브라우저에이 주소를 입력 하 여 두 번째 작업 인 Details () 작업을 호출할 수 있습니다.

/Home/Details

Index () 작업은 뷰를 반환 합니다. 사용자가 만드는 대부분의 작업은 뷰를 반환 합니다. 그러나 작업은 다른 유형의 작업 결과를 반환할 수 있습니다. 예를 들어 Details () 작업은 들어오는 요청을 Index () 작업으로 리디렉션하는 RedirectToActionResult를 반환 합니다.

Index () 작업에는 다음 코드 줄 하나가 포함 됩니다.

보기 ()

이 코드 줄은 웹 서버의 다음 경로에 있어야 하는 뷰를 반환 합니다.

\Views\Home\Index.aspx

뷰의 경로는 컨트롤러 이름 및 컨트롤러 작업의 이름에서 유추 됩니다.

선호 하는 경우 보기에 대해 명시적으로 지정할 수 있습니다. 다음 코드 줄은 Fred 라는 뷰를 반환 합니다.

보기 (Fred)

이 코드 줄을 실행 하면 다음 경로에서 뷰가 반환 됩니다.

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들려는 경우 뷰 이름에 대해 명시적으로 확인 하는 것이 좋습니다. 이렇게 하면 단위 테스트를 만들어 컨트롤러 작업에서 예상한 뷰가 반환 되었는지 확인할 수 있습니다.

## <a name="adding-content-to-a-view"></a>뷰에 콘텐츠 추가

뷰는 스크립트를 포함할 수 있는 표준 (X) HTML 문서입니다. 스크립트를 사용 하 여 동적 콘텐츠를 뷰에 추가 합니다.

예를 들어 목록 2의 보기는 현재 날짜 및 시간을 표시 합니다.

**목록 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

목록 2에 있는 HTML 페이지의 본문에는 다음 스크립트가 포함 되어 있습니다.

&lt;% Response. Write (DateTime. Now)%&gt;

스크립트 구분 기호% 및%를 사용 하 여 &lt; &gt; 스크립트의 시작과 끝을 표시 합니다. 이 스크립트는 Visual basic으로 작성 되었습니다. 브라우저에 콘텐츠를 렌더링 하는 Write () 메서드를 호출 하 여 현재 날짜 및 시간을 표시 합니다. 스크립트 구분 기호 &lt; % 및%는 &gt; 하나 이상의 문을 실행 하는 데 사용할 수 있습니다.

자주 Write ()를 호출 하므로 Microsoft는 Response () 메서드를 호출 하는 바로 가기를 제공 합니다. 목록 3의 뷰에서는 &lt; % = 및% 구분 기호를 &gt; 호출 하 여 Write () 호출을 위한 바로 가기로 사용 합니다.

**목록 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

모든 .NET 언어를 사용 하 여 뷰에서 동적 콘텐츠를 생성할 수 있습니다. 일반적으로 Visual Basic .NET 또는 c #을 사용 하 여 컨트롤러 및 뷰를 작성 합니다.

## <a name="using-html-helpers-to-generate-view-content"></a>HTML 도우미를 사용 하 여 뷰 콘텐츠 생성

보기에 콘텐츠를 더 쉽게 추가할 수 있도록 *HTML 도우미*라는 기능을 활용할 수 있습니다. 일반적으로 HTML 도우미는 문자열을 생성 하는 메서드입니다. HTML 도우미를 사용 하 여 텍스트 상자, 링크, 드롭다운 목록 및 목록 상자와 같은 표준 HTML 요소를 생성할 수 있습니다.

예를 들어 목록 4의 뷰는 세 가지 HTML 도우미 인 Html.beginform (), TextBox () 및 Password () 도우미를 사용 하 여 로그인 폼을 생성 합니다 (그림 1 참조).

**목록 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**그림 01**: 표준 로그인 양식 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-views-overview-vb/_static/image2.png))

모든 HTML 도우미 메서드는 뷰의 Html 속성에서 호출 됩니다. 예를 들어, Html. TextBox () 메서드를 호출 하 여 텍스트 상자를 렌더링 합니다.

&lt; &gt; Html. TextBox () 및 Html. Password () 도우미를 모두 호출할 때 스크립트 구분 기호% = 및%를 사용 합니다. 이러한 도우미는 단순히 문자열을 반환 합니다. 브라우저에 문자열을 렌더링 하기 위해 Write ()를 호출 해야 합니다.

HTML 도우미 메서드 사용은 선택 사항입니다. 이러한 작업을 수행 하면 작성 해야 하는 HTML 및 스크립트의 양이 줄어들어 더 쉽게 사용할 수 있습니다. 목록 5의 뷰는 HTML 도우미를 사용 하지 않고 목록 4의 뷰와 정확히 동일한 폼을 렌더링 합니다.

**목록 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

사용자 고유의 HTML 도우미를 만들 수도 있습니다. 예를 들어, HTML 테이블에 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView () 도우미 메서드를 만들 수 있습니다. **사용자 지정 HTML 도우미 만들기**자습서의이 항목을 탐색 합니다.

## <a name="using-view-data-to-pass-data-to-a-view"></a>뷰 데이터를 사용 하 여 보기에 데이터 전달

데이터 보기를 사용 하 여 컨트롤러에서 보기로 데이터를 전달 합니다. 메일을 통해 보내는 패키지와 같은 뷰 데이터를 생각해 보십시오. 컨트롤러에서 뷰로 전달 된 모든 데이터는이 패키지를 사용 하 여 보내야 합니다. 예를 들어 목록 6의 컨트롤러는 데이터를 볼 수 있도록 메시지를 추가 합니다.

**목록 6-제품 컨트롤러 .vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

Controller ViewData 속성은 이름/값 쌍의 컬렉션을 나타냅니다. 목록 6에서 Index () 메서드는 값이 Hello World! 인 message 라는 뷰 데이터 컬렉션에 항목을 추가 합니다. Index () 메서드에서 뷰를 반환 하는 경우 뷰 데이터는 뷰에 자동으로 전달 됩니다.

목록 7의 뷰는 보기 데이터에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.

**목록 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

뷰에서는 메시지를 렌더링할 때 Html 도우미 메서드를 사용 합니다. Html. 인코드 () HTML 도우미는 및와 같은 특수 문자 &lt; 를 &gt; 웹 페이지에 표시 하기에 안전한 문자로 인코딩합니다. 사용자가 웹 사이트로 전송 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.

(제품 컨트롤러에서 메시지를 직접 만들었기 때문에 메시지를 인코딩할 필요가 없습니다. 그러나 뷰 내의 뷰 데이터에서 검색 된 콘텐츠를 표시 하는 경우 항상 Html. 인코드 () 메서드를 호출 하는 것이 좋습니다.

목록 7에서는 보기 데이터를 활용 하 여 컨트롤러에서 뷰로 간단한 문자열 메시지를 전달 했습니다. 데이터 보기를 사용 하 여 컨트롤러에서 보기에 데이터베이스 레코드 컬렉션과 같은 다른 유형의 데이터를 전달할 수도 있습니다. 예를 들어 Products 데이터베이스 테이블의 내용을 뷰에 표시 하려면 데이터 보기에서 데이터베이스 레코드의 컬렉션을 전달 합니다.

또한 컨트롤러에서 뷰로 강력한 형식의 뷰 데이터를 전달 하는 옵션도 있습니다. **강력한 형식의 뷰 데이터 및 뷰 이해**자습서의이 항목을 탐색 합니다.

## <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 했습니다. 첫 번째 섹션에서는 프로젝트에 새 뷰를 추가 하는 방법을 알아보았습니다. 특정 컨트롤러에서 호출 하려면 보기를 오른쪽 폴더에 추가 해야 한다는 것을 배웠습니다. 다음으로 HTML 도우미 항목에 대해 설명 했습니다. HTML 도우미를 사용 하 여 표준 HTML 콘텐츠를 쉽게 생성 하는 방법을 배웠습니다. 마지막으로, 보기 데이터를 활용 하 여 컨트롤러에서 보기로 데이터를 전달 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](passing-data-to-view-master-pages-cs.md)
> [다음](creating-custom-html-helpers-vb.md)
