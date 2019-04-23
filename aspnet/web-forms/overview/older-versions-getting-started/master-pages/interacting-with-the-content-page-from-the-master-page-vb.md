---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: 마스터 페이지 (VB)에서 콘텐츠 페이지와 상호 작용 | Microsoft Docs
author: rick-anderson
description: 메서드를 호출, 마스터 페이지의 코드에서 콘텐츠 페이지의 등 속성을 설정 하는 방법을 검사 합니다.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f0575474bc750cad15ac74c522e3138b326d880c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400011"
---
# <a name="interacting-with-the-content-page-from-the-master-page-vb"></a>마스터 페이지에서 콘텐츠 페이지와 상호 작용(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> 메서드를 호출, 마스터 페이지의 코드에서 콘텐츠 페이지의 등 속성을 설정 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

이전 자습서에는 콘텐츠 페이지의 마스터 페이지를 사용 하 여 프로그래밍 방식으로 상호 작용 하는 방법을 검사 합니다. 제품 추가 하는 재현 율 5를 가장 최근에 나열 하는 GridView 컨트롤을 포함 하도록 마스터 페이지를 업데이트 했습니다. 그런 다음 사용자는 새 제품을 추가할 수는 콘텐츠 페이지를 만들었습니다. 새 제품에 추가 되 면 콘텐츠 페이지를 마스터 페이지는 GridView 새로 고쳐 방금 추가 된 제품을 포함 하도록 지시 해야 합니다. 이 기능은 마스터 페이지를 새로 고친에 바인딩된 데이터가 GridView에 공용 메서드를 추가 하 고 다음 콘텐츠 페이지에서 해당 메서드를 호출 하 여 작업을 수행 했습니다.

콘텐츠 및 마스터 페이지 상호 작용의 가장 일반적인 형태는 콘텐츠 페이지에서 시작 합니다. 그러나 마스터 페이지 작업에 현재 콘텐츠 페이지 rouse 수 및 마스터 페이지 콘텐츠 페이지도 표시 되는 데이터를 수정 하는 데 사용할 수 있는 사용자 인터페이스 요소를 포함 하는 경우 이러한 기능을 해야 할 수 있습니다. 모든 제품의 가격을 두 배로, GridView의 제품 정보 제어를 표시 하 고 단추를 포함 하는 마스터 페이지 컨트롤을 클릭할 때 콘텐츠 페이지를 고려해 야 합니다. 이전 자습서의 예제에서는 마찬가지로 double 가격은 새로운 가격 표시 되도록 단추를 클릭 한 후 새로 고칠 수 해야 하는 GridView 이지만이 시나리오에서는 콘텐츠 페이지를 작업으로 rouse 해야 하는 마스터 페이지입니다.

이 자습서에서는 마스터 페이지 콘텐츠 페이지에 정의 된 기능을 호출 하는 방법을 살펴봅니다.

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>시작 이벤트 및 이벤트 처리기를 통해 프로그래밍 방식 상호 작용

마스터 페이지에서 콘텐츠 페이지 기능을 호출 하는 반대 방향의 보다 쉽지 않습니다. 콘텐츠 페이지는 콘텐츠 페이지에서 프로그래밍 방식 상호 작용을 시작 하는 경우 단일 마스터 페이지에 있으므로 공용 메서드 및 속성 이란 목표인 알고 있습니다. 그러나 마스터 페이지, 콘텐츠 페이지 수를 각각 고유한 속성 및 메서드 집합을 가질 수 있습니다. 방법, 그런 다음에서는 코드를 작성할 수 콘텐츠 페이지는 런타임 시까지 호출 모릅니다 때 콘텐츠 페이지에서 일부 작업을 수행 하도록 마스터 페이지에서?

ASP.NET 웹 컨트롤을, 단추 컨트롤과 같은 것이 좋습니다. 단추 컨트롤을 임의 개수의 ASP.NET 페이지에서 나타날 수 있으며는 경고할 수 있습니다 페이지를 클릭 했는지 메커니즘이 필요 합니다. 사용 하 여 이렇게 *이벤트*합니다. 단추 컨트롤 발생 하는 특히 해당 `Click` 이벤트; 클릭할 때 단추가 포함 된 ASP.NET 페이지 필요에 따라 응답할 수를 통해 해당 알림을 *이벤트 처리기*합니다.

이 동일한 패턴에 해당 콘텐츠 페이지는 마스터 페이지 트리거 기능에 사용할 수 있습니다.

1. 마스터 페이지에 이벤트를 추가 합니다.
2. 마스터 페이지에서 해당 콘텐츠 페이지를 사용 하 여 통신 해야 할 때마다 이벤트를 발생 시킵니다. 예를 들어, 마스터 페이지를 경고 해당 콘텐츠 페이지는 사용자가 가격은 두 배로 증가 해야 하는 경우 가격은 두 배로 증가 한 후에 즉시 해당 이벤트가 발생 됩니다.
3. 일부 작업을 수행 해야 하는 이러한 콘텐츠 페이지에서 이벤트 처리기를 만듭니다.

이 자습서의 나머지이 부분; 소개에 설명 된 예제를 구현 합니다. 즉, 데이터베이스에서 제품을 나열 하는 콘텐츠 페이지와 마스터 페이지 단추를 포함 하는 가격을 두 배로 제어 합니다.

## <a name="step-1-displaying-products-in-a-content-page"></a>1단계: 콘텐츠 페이지에서 제품 표시

이 첫 번째 업무 우선 순위는 Northwind 데이터베이스에서 제품을 나열 하는 콘텐츠 페이지를 만드는 것입니다. (이전 자습서에서는 Northwind 데이터베이스 프로젝트에 추가 했습니다 [ *콘텐츠 페이지에서 마스터 페이지와 상호 작용*](interacting-with-the-master-page-from-the-content-page-vb.md).) 새 ASP.NET 페이지를 추가 하 여 시작 합니다 `~/Admin` 라는 폴더 `Products.aspx`에 바인딩하지 하 여는 `Site.master` 마스터 페이지입니다. 그림 1에서는이 페이지는 웹 사이트에 추가한 후 솔루션 탐색기를 보여 줍니다.


[![Admin 폴더를 새 ASP.NET 페이지를 추가 합니다.](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**그림 01**: 새 ASP.NET 페이지를 추가 합니다 `Admin` 폴더 ([큰 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png))


회수에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 라는 기본 페이지를 사용자 지정 클래스를 만들었습니다 자습서 `BasePage` 생성 하는 페이지의 제목이 없는 경우 명시적으로 설정 합니다. 로 이동 합니다 `Products.aspx` 페이지의 코드 숨김 클래스에서 파생 되 게 하 고 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트 된 `Web.sitemap` 이 단원에 대 한 항목을 포함 하는 파일입니다. 아래에 다음 태그를 추가 합니다 `<siteMapNode>` 마스터 페이지 상호 작용 단원으로 콘텐츠에 대 한 합니다.


[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

이 추가 `<siteMapNode>` 요소 단원에서 반영 됩니다 (그림 5 참조)를 나열 합니다.

돌아가서 `Products.aspx`합니다. 콘텐츠 컨트롤에 대 한 `MainContent`GridView 컨트롤을 추가 하 고 이름을 `ProductsGrid`입니다. GridView 라는 새 SqlDataSource 컨트롤을 바인딩할 `ProductsDataSource`합니다.


[![GridView 새 SqlDataSource 컨트롤에 바인딩](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**그림 02**: GridView 새 SqlDataSource 컨트롤을 바인딩할 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png))


Northwind 데이터베이스 사용 마법사를 구성 합니다. 이전 자습서를 수행한 경우 명명 된 연결 문자열을 했어야 `NorthwindConnectionString` 에서 `Web.config`합니다. 그림 3에 나와 있는 것 처럼 드롭 다운 목록에서이 연결 문자열을 선택 합니다.


[![SqlDataSource Northwind 데이터베이스를 사용 하도록 구성](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**그림 03**: SqlDataSource Northwind 데이터베이스를 사용 하도록 구성 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png))


다음으로, 데이터 소스 컨트롤을 지정 `SELECT` 드롭 다운 목록에서 Products 테이블을 선택 하 고 반환 하 여 문을 합니다 `ProductName` 및 `UnitPrice` 열 (그림 4 참조). 다음을 클릭 하 고 데이터 소스 구성 마법사를 완료 한 다음 끝냅니다.


[![Products 테이블에서 ProductName 및 UnitPrice 필드를 반환 합니다.](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**그림 04**: 반환 된 `ProductName` 및 `UnitPrice` 에서 필드를 `Products` 테이블 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png))


이것이 전부입니다! 마법사를 완료 한 후 Visual Studio는 두 BoundFields 미러 SqlDataSource 컨트롤에서 반환 된 두 개의 필드를 GridView에 추가 합니다. GridView 및 SqlDataSource 컨트롤 태그는 다음과 같습니다. 그림 5는 브라우저를 통해 볼 때 결과 보여 줍니다.


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]


[![각 제품 및 해당 가격 GridView에 나열 됩니다.](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**그림 05**: 각 제품 및 해당 가격 GridView에 나열 됩니다 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png))


> [!NOTE]
> 자유롭게 GridView의 모양을 정리할 수 있습니다. 몇 가지 제안 사항에 표시 된 UnitPrice 값을 통화로 서식 지정 및 배경색 및 글꼴을 사용 하 여 표 모양 향상을 위해 포함 됩니다. 표시 및 ASP.NET에서 데이터 서식 지정에 대 한 자세한 내용은 참조 내 [데이터 자습서 시리즈를 사용 하 여 작업](../../data-access/index.md)합니다.


## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>2단계: 마스터 페이지에 이중 가격 단추 추가

다음 태스크는 단추 웹 컨트롤에 마스터 페이지를 추가 하려면 클릭 하면 데이터베이스에서 모든 제품의 가격 double입니다. 엽니다는 `Site.master` 아래에 배치 디자이너 도구 상자에서 단추를 끌어서 마스터 페이지는 `RecentProductsDataSource` 이전 자습서에서 추가한 SqlDataSource 컨트롤입니다. 설정 단추 `ID` 속성을 `DoublePrice` 고 `Text` 속성을 "Double 제품 가격"입니다.

다음으로 마스터 페이지 이름을 SqlDataSource 컨트롤을 추가 `DoublePricesDataSource`합니다. 이 SqlDataSource를 사용 하 여 실행 하는 `UPDATE` 모든 가격의 두 배로 문입니다. 구체적으로 설정 해야 해당 `ConnectionString` 하 고 `UpdateCommand` 적절 한 연결 문자열 속성 및 `UPDATE` 문입니다. 이 SqlDataSource 컨트롤을 호출 해야 `Update` 메서드는 경우는 `DoublePrice` 단추를 클릭 합니다. 설정 하는 `ConnectionString` 및 `UpdateCommand` 속성인 SqlDataSource 컨트롤을 선택 하 고 속성 창으로 이동 합니다. `ConnectionString` 속성 목록에 이미 저장 된 연결 문자열 `Web.config` ; 드롭다운 목록을 선택 합니다 `NorthwindConnectionString` 그림 6에 표시 된 대로 옵션.


[![SqlDataSource를 위해 사용 하도록 구성](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**그림 06**: SqlDataSource를 사용 하 여 구성 합니다 `NorthwindConnectionString` ([큰 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png))


설정 하는 `UpdateCommand` 속성을 속성 창에서 UpdateQuery 옵션을 찾습니다. 이 속성을 선택 하면; 줄임표 단추를 표시 합니다. 그림 7 명령 및 매개 변수 편집기 대화 상자를 표시 하려면이 단추를 클릭 합니다. 다음을 입력 `UPDATE` 문을 대화 상자의 텍스트 상자에 붙여넣습니다.


[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

이 문을 실행 하는 경우 두 배로 증가 합니다 `UnitPrice` 의 각 레코드에 대 한 값을 `Products` 테이블.


[![SqlDataSource의 UpdateCommand 속성 설정](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**그림 07**: SqlDataSource의 설정 `UpdateCommand` 속성 ([큰 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png))


이러한 속성을 설정한 다음 단추 및 SqlDataSource 컨트롤의 선언적 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

에 호출을 해당 `Update` 메서드 때는 `DoublePrice` 단추를 클릭 합니다. 만들기는 `Click` 에 대 한 이벤트 처리기는 `DoublePrice` 단추 다음 코드를 추가 하 고:


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

이 기능을 테스트 하려면 다음을 방문 합니다 `~/Admin/Products.aspx` 페이지에서는 1 단계에서에서 만든 "Double 제품 가격" 단추를 클릭 합니다. 포스트백을 발생 시키는 단추를 클릭 하 고 실행 합니다 `DoublePrice` 단추의 `Click` 모든 제품의 가격을 두 배로 높일 경우 이벤트 처리기입니다. 페이지를 다시 렌더링 한 다음 및 태그를 반환 하 고 브라우저에 다시 표시 합니다. 그러나 콘텐츠 페이지에 GridView "Double 제품 가격" 전에 단추를 클릭 한 동일한 가격 나열 됩니다. 즉, 데이터가 GridView에 처음 로드 상태로 다시 로드 되지 않습니다 포스트백에서 달리 지시 하지 않으면 뷰 상태에 저장 했습니다. 로 돌아와서를 다른 페이지를 방문 하는 경우는 `~/Admin/Products.aspx` 페이지 업데이트 된 가격을 볼 수 있습니다.

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>3단계: 두 배가 되므로 이벤트 경우의 가격을 발생 합니다.

때문에 GridView는 `~/Admin/Products.aspx` "Double 제품 가격" 단추를 클릭 하지 않은 또는 작동 하지 않는 사용자 생각할 작업 수, 페이지 두 배로 높일 경우 가격 즉시 반영 되지 않습니다. 수 시도 단추를 클릭 하면 시간, 가격은 나중에 다시 두 배로 높일 경우 몇 가지 추가 합니다. 콘텐츠의 그리드 있어야이 문제를 해결 하려면 페이지 두 배가 되므로 직후 새 가격을 표시 합니다.

이 자습서의 앞부분에서 설명 했 듯이 사용자가 클릭할 때마다 마스터 페이지에서 이벤트를 발생 해야 합니다 `DoublePrice` 단추입니다. 이벤트는 흥미로운 발생 하는 다른 클래스 (이벤트 구독자)의 집합을 다른 알릴 하나의 클래스 (이벤트 게시자)에 대 한 방법이 있습니다. 이 예제에서 마스터 페이지는 이벤트 게시자; 이러한 콘텐츠 페이지는 경우를 고려 하는 `DoublePrice` 단추를 클릭 하면 구독자는 합니다.

클래스를 만들어 이벤트를 구독을 *이벤트 처리기*, 발생 한 이벤트에 대 한 응답에서 실행 되는 방법인 합니다. 독자분 께서는 정의 하 여 이벤트를 정의 하는 게시자는 *이벤트 대리자*합니다. 이벤트 대리자 이벤트 처리기에 동의 해야 하는 입력된 매개 변수를 지정 합니다. .NET framework에서 이벤트 대리자 값을 반환 및 두 개의 입력된 매개 변수를 수락 수행:

- `Object`, 이벤트 소스를 식별 하 고
- 파생 된 클래스 `System.EventArgs`

이벤트 처리기에 전달 된 두 번째 매개 변수는 이벤트에 대 한 추가 정보를 포함할 수 있습니다. 기본 `EventArgs` 클래스는 모든 정보를 전달 하지,.NET Framework에는 클래스를 확장 하는 많은 `EventArgs` 추가 속성을 포함 합니다. 예를 들어를 `CommandEventArgs` 인스턴스에 응답 하는 이벤트 처리기로 전달 되는 `Command` 이벤트를 두 정보 속성을 포함 하 고: `CommandArgument` 및 `CommandName`.

> [!NOTE]
> 만들기에 대 한 자세한 내용은 시키고 이벤트 처리, 참조 [이벤트 및 대리자](https://msdn.microsoft.com/library/17sde2xt.aspx) 하 고 [단순 영어에서 이벤트 대리자](http://www.codeproject.com/KB/cs/eventdelegates.aspx)합니다.


이벤트 정의 다음 구문을 사용 합니다.


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

사용자가 클릭 될 때 콘텐츠 페이지를 경고에 필요 하기 때문에 합니다 `DoublePrice` 단추 및 기타 추가 정보를 전달할 필요가 없습니다, 이벤트 대리자를 사용할 수 있습니다 `EventHandler`, 두 번째 피연산자로으로 허용 하는 이벤트 처리기를 정의 하는 매개 변수 형식의 개체 `System.EventArgs`합니다. 마스터 페이지에서 이벤트를 만들려면, 마스터 페이지의 코드 숨김 클래스에 다음 코드 줄을 추가 합니다.


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

위의 코드는 공용 이벤트 라는 마스터 페이지를 추가 `PricesDoubled`합니다. 이제 가격의 두 배로 이후이 이벤트가 발생 해야 합니다. 이벤트를 발생 시키려면 다음 구문을 사용 하 여:


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

여기서 *보낸 사람* 하 고 *eventArgs* 은 구독자의 이벤트 처리기에 전달 하려는 값입니다.

업데이트를 `DoublePrice` `Click` 이벤트 처리기를 다음 코드로 바꿉니다.


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

이전과 마찬가지로 합니다 `Click` 이벤트 처리기를 호출 하 여 시작 합니다 `DoublePricesDataSource` SqlDataSource 컨트롤의 `Update` 모든 제품의 가격을 두 번 하는 방법. 두 개의 추가 이벤트 처리기에는 다음과 같습니다. 첫 번째는 `RecentProducts` GridView의 데이터가 새로 고쳐집니다. 이 GridView 이전 자습서에서 마스터 페이지에 추가한 하 고 5 개의 가장 최근에 추가 된 제품을 표시 합니다. 이 표를 새로 고쳐 이러한 5 개 제품에 대 한 바로 이중 가격 표시 되도록 해야 합니다. 다음은 `PricesDoubled` 이벤트가 발생 합니다. 마스터 페이지 자체에 대 한 참조 (`Me`) 이벤트 소스와 빈 이벤트 처리기에 보내지는 `EventArgs` 개체 이벤트 인수로 서 전송 됩니다.

## <a name="step-4-handling-the-event-in-the-content-page"></a>4단계: 콘텐츠 페이지에서 이벤트를 처리

마스터 페이지를 발생 하는 시점에서 해당 `PricesDoubled` 이벤트 때마다는 `DoublePrice` 단추 컨트롤을 클릭 합니다. 그러나이 절반에 불과합니다-구독자에서 이벤트를 처리 해야 합니다. 이 두 단계: 이벤트 처리기를 만들고 이벤트 처리기는 이벤트가 발생할 때 실행 되도록 이벤트 작성 코드를 추가 합니다.

명명 된 이벤트 처리기를 만들어 시작 `Master_PricesDoubled`합니다. 정의한 방법으로 인해 합니다 `PricesDoubled` 마스터 페이지의 이벤트는 이벤트 처리기의 두 입력된 매개 변수 형식 이어야 합니다 `Object` 및 `EventArgs`, 각각. 이벤트 처리기 호출에서을 `ProductsGrid` GridView의 `DataBind` 표에 데이터를 다시 바인딩해야 하는 방법입니다.


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

이벤트 처리기에 대 한 코드는 완료 되었지만 아직에 했습니다 마스터 페이지의 연결 `PricesDoubled` 이 이벤트 처리기에는 이벤트입니다. 다음 구문을 통해 이벤트 처리기에 이벤트를 연결 하는 구독자:


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

*게시자* 이벤트를 제공 하는 개체에 대 한 참조가 *eventName*, 및 *methodName* 구독자에 정의 된 이벤트 처리기의 이름입니다.

이 이벤트 연결 코드 페이지를 처음 방문할 및 후속 포스트백에서 실행 해야 하 고 시점 이벤트를 발생 시킬 때 앞에 오는 페이지 수명 주기에서 발생 해야 합니다. 페이지 수명 주기 초기에 발생 하는 PreInit 단계에서 시점 이벤트 작성 코드를 추가할 경우

오픈 `~/Admin/Products.aspx` 만들어를 `Page_PreInit` 이벤트 처리기:


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

이 연결 코드를 완료 하기 위해 콘텐츠 페이지에서 마스터 페이지를 프로그래밍 방식으로 참조를 해야 합니다. 이전 자습서에서 설명한 대로, 두 가지 이렇게 하려면:

- 자유로운 형식의 캐스팅 하 여 `Page.Master` 속성을 적절 한 마스터 페이지 형식 또는
- 추가 하 여는 `@MasterType` 지시문을 `.aspx` 페이지를 사용 하는 강력한 형식의 `Master` 속성입니다.

후자의 방법을 사용해 보겠습니다. 다음 추가 `@MasterType` 페이지의 선언적 태그의 맨 위에 지시문:


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

다음 이벤트 배선을 코드를 추가 합니다 `Page_PreInit` 이벤트 처리기:


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

이 코드를 사용 하 여 콘텐츠 페이지에 GridView 새로 고쳐질 때마다는 `DoublePrice` 단추를 클릭 합니다.

그림 8과 9이이 동작을 보여 줍니다. 그림 8에서는 먼저 방문 되 면 페이지를 보여 줍니다. 둘 다에 값을 가격에 `RecentProducts` (마스터 페이지의 왼쪽된 열)의 GridView 및 `ProductsGrid` (콘텐츠 페이지)에 GridView입니다. 그림 9에서는 동일한 직후 화면을 `DoublePrice` 버튼을 클릭 합니다. 알 수 있듯이 새 가격은 두 Gridview에 즉시 반영 됩니다.


[![초기 가격 값](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**그림 08**: 초기 가격 값 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png))


[![Just-Doubled 가격을 Gridview에 표시 됩니다.](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**그림 09**: Just-Doubled 가격을 Gridview에 표시 됩니다 ([클릭 하 여 큰 이미지 보기](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png))


## <a name="summary"></a>요약

이상적으로 마스터 페이지 및 콘텐츠 페이지 서로 완전히 별개 이며 필요 없는 수준의 상호 작용 합니다. 그러나 마스터 페이지 또는 마스터 페이지나 콘텐츠 페이지에서 수정할 수 있는 데이터를 표시 하는 콘텐츠 페이지에 있는 경우 다음 해야 마스터 페이지에 콘텐츠 페이지 (또는 그 반대로는) 경고 표시를 업데이트할 수 있도록 데이터가 수정 되는 경우. 이전 자습서에서 콘텐츠 페이지의 마스터 페이지를 사용 하 여 프로그래밍 방식으로 상호 작용 하는 방법을 살펴보았습니다. 이 자습서에서 마스터 페이지 시작 상호 작용 하는 방법을 살펴보았습니다.

마스터 페이지는 콘텐츠와 프로그래밍 방식 상호 작용 콘텐츠 또는 마스터 페이지에서 가져올 수 있습니다, 하는 동안 사용 되는 상호 작용 패턴 하기 위해 원본에 따라 달라 집니다. 때문에 콘텐츠 페이지 단일 마스터 페이지는 하지만 마스터 페이지 수 많은 다른 콘텐츠 페이지를 보유 하는 차이가 발생 합니다. 콘텐츠 페이지와 직접 상호 작용 하는 마스터 페이지 대신 마스터 페이지에 일부 작업을 수행한 신호를 보내는 이벤트를 발생 하는 것이 좋습니다. 작업에 대 한 처리는 이러한 콘텐츠 페이지는 이벤트 처리기를 만들 수 있습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Asp.net에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [이벤트 및 대리자](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [콘텐츠 및 마스터 페이지 간에 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터를 사용 하 여 작업](../../data-access/index.md)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](interacting-with-the-master-page-from-the-content-page-vb.md)
> [다음](master-pages-and-asp-net-ajax-vb.md)
