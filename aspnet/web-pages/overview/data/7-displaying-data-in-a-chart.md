---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET 웹 페이지(Razor)가 있는 차트에 데이터 표시 | 마이크로 소프트 문서
author: rick-anderson
description: 이 장에서는 차트에 데이터를 표시하는 방법을 설명합니다. 이전 장에서는 수동으로 그리드에 데이터를 표시하는 방법을 배웠습니다. 이 장에서는...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542887"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>웹 페이지(Razor)를 ASP.NET 차트에 데이터 표시

[로 마이크로 소프트](https://github.com/microsoft)

> 이 문서에서는 도우미를 사용하여 차트를 사용하여 ASP.NET 웹 페이지(Razor) `Chart` 웹 사이트에 데이터를 표시하는 방법을 설명합니다.
> 
> **당신이 배울 것이다 무엇**:
> 
> - 차트에 데이터를 표시하는 방법.
> - 기본 제공 테마를 사용하여 차트에 스타일을 정하는 방법.
> - 차트를 저장하는 방법과 더 나은 성능을 위해 차트를 캐시하는 방법.
> 
> 다음은 이 문서에서 소개한 ASP.NET 프로그래밍 기능입니다.
> 
> - `Chart` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 웹 페이지 1.0 및 웹 페이지 2ASP.NET 에 적용됩니다.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>차트 도우미

데이터를 그래픽 형식으로 표시하려면 도우미를 사용할 `Chart` 수 있습니다. 도우미는 `Chart` 다양한 차트 유형의 데이터를 표시하는 이미지를 렌더링할 수 있습니다. 서식 지정 및 레이블 지정에 대한 많은 옵션을 지원합니다. 도우미는 `Chart` Microsoft Excel또는 영역 차트, 막대 차트, 열 차트, 꺾은줄 차트 및 원형 차트와 &#8212; 기타 도구에서 잘 알고 있을 수 있는 모든 유형의 차트와 주식 차트와 같은 보다 전문적인 차트를 포함하여 30개 이상의 유형의 차트를 렌더링할 수 있습니다.

| **지역도** ![설명: 지역도표 유형 그림](7-displaying-data-in-a-chart/_static/image1.jpg) | **막대 차트** ![설명: 막대형 차트 유형 그림](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **열체 차트** ![설명: 열수 차트 유형 그림](7-displaying-data-in-a-chart/_static/image3.jpg) | **표선 차트** ![설명: 선급선 차트 유형 그림](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **원형 차트** ![설명: 원형 차트 유형 그림](7-displaying-data-in-a-chart/_static/image5.jpg) | **주식 차트** ![설명: 주식 차트 유형 의 그림](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>차트 요소

차트는 데이터와 범례, 축, 계열 등과 같은 추가 요소를 표시합니다. 다음 그림은 `Chart` 도우미를 사용할 때 사용자 지정할 수 있는 많은 차트 요소를 보여 줍니다. 이 문서에서는 이러한 요소중 일부(전부는 아님)를 설정하는 방법을 보여 주어집니다.

![설명: 차트 요소를 보여주는 그림](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>데이터에서 차트 만들기

차트에 표시되는 데이터는 배열, 데이터베이스에서 반환된 결과 또는 XML 파일에 있는 데이터에서 나온 데이터일 수 있습니다.

### <a name="using-an-array"></a>배열 사용

[Razor 구문을 사용하여 ASP.NET 웹 페이지 프로그래밍 소개에서](https://go.microsoft.com/fwlink/?LinkId=202890)설명한 대로 배열을 사용하면 유사한 항목의 컬렉션을 단일 변수에 저장할 수 있습니다. 배열을 사용하여 차트에 포함할 데이터를 포함할 수 있습니다.

이 절차에서는 기본 차트 유형을 사용하여 배열의 데이터에서 차트를 만드는 방법을 보여 주며 이 절차에서 차트를 만드는 방법을 보여 주시면 됩니다. 또한 페이지 내에 차트를 표시하는 방법도 보여 주었습니다.

1. *ChartArrayBasic.cshtml이라는*새 파일을 만듭니다.
2. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    코드는 먼저 새 차트를 만들고 너비와 높이를 설정합니다. 메서드를 사용 하 여 `AddTitle` 차트 제목을 지정 합니다. 데이터를 추가하려면 메서드를 `AddSeries` 사용합니다. 이 `name`예제에서는 `xValue` `yValues` `AddSeries` 메서드의 " 및 매개 변수를 사용합니다. `name` 매개 변수가 차트 범례에 표시됩니다. `xValue` 매개 변수에는 차트의 가로 축을 따라 표시되는 데이터 배열이 포함되어 있습니다. `yValues` 매개변수에는 차트의 세로 점을 플롯하는 데 사용되는 데이터 배열이 포함되어 있습니다.

    메서드는 `Write` 실제로 차트를 렌더링합니다. 이 경우 차트 유형을 지정하지 않았기 때문에 `Chart` 도우미는 열차트인 기본 차트를 렌더링합니다.
3. 브라우저에서 페이지를 실행합니다. 브라우저에 차트가 표시됩니다. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>차트 데이터에 데이터베이스 쿼리 사용

차트로 만들 정보가 데이터베이스에 있는 경우 데이터베이스 쿼리를 실행한 다음 결과의 데이터를 사용하여 차트를 만들 수 있습니다. 이 절차에서는 웹 페이지 사이트에서 데이터베이스 작업 소개 문서에서 만든 데이터베이스의 데이터를 읽고 표시하는 방법을 보여 [ASP.NET.](https://go.microsoft.com/fwlink/?LinkId=202893)

1. 폴더가 아직 없는 경우 웹 사이트의 루트에 *앱\_데이터* 폴더를 추가합니다.
2. *앱\_데이터* 폴더에 ASP.NET [웹 페이지 사이트의 데이터베이스 작업 소개에](https://go.microsoft.com/fwlink/?LinkId=202893)설명된 *SmallBakery.sdf라는* 데이터베이스 파일을 추가합니다.
3. *ChartDataQuery.cshtml이라는*새 파일을 만듭니다.
4. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다.   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    코드는 먼저 SmallBakery 데이터베이스를 열고 . `db` 이 변수는 `Database` 데이터베이스에서 읽고 쓰는 데 사용할 수 있는 개체를 나타냅니다. 다음으로 코드는 SQL 쿼리를 실행하여 각 제품의 이름과 가격을 가져옵니다. 코드는 새 차트를 만들고 차트의 `DataBindTable` 메서드를 호출하여 데이터베이스 쿼리를 전달합니다. 이 메서드는 두 개의 `dataSource` 매개 변수를 사용합니다: 매개 `xField` 변수는 쿼리의 데이터에 대한 것이고 매개 변수를 사용하면 차트의 x축에 사용되는 데이터 열을 설정할 수 있습니다.

    `DataBindTable` 메서드를 사용하는 대신 도우미의 메서드를 `AddSeries` `Chart` 사용할 수 있습니다. 메서드를 `AddSeries` 사용 하 `xValue` `yValues` 고 매개 변수를 설정할 수 있습니다. 예를 들어 다음과 같은 `DataBindTable` 메서드를 사용하는 대신 다음과 같이 합니다.

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    다음과 `AddSeries` 같은 방법을 사용할 수 있습니다.

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    둘 다 동일한 결과를 렌더링합니다. 차트 `AddSeries` 형식과 데이터를 보다 명시적으로 지정할 수 있으므로 이 `DataBindTable` 방법은 더 유연하지만 추가 유연성이 필요하지 않은 경우 이 방법을 더 쉽게 사용할 수 있습니다.
5. 브라우저에서 페이지를 실행합니다. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML 데이터 사용

차트의 세 번째 옵션은 XML 파일을 차트의 데이터로 사용하는 것입니다. 이렇게 하려면 XML 파일에 XML 구조를 설명하는 스키마*파일(.xsd* 파일)도 있어야 합니다. 이 절차에서는 XML 파일에서 데이터를 읽는 방법을 보여 주며, 이 절차에서는 데이터를 읽는 방법을 보여 주시면 됩니다.

1. *\_앱 데이터* 폴더에서 *data.xml*이라는 새 XML 파일을 만듭니다.
2. 기존 XML을 가상의 회사의 직원에 대한 일부 XML 데이터인 다음으로 바꿉습니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. *\_앱 데이터* 폴더에서 *data.xsd라는*새 XML 파일을 만듭니다. (이 시간 확장은 *.xsd입니다.)*
4. 기존 XML을 다음으로 바꿉꿉을 다음과 같은 항목으로 바꿉입니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 웹 사이트의 루트에서 *ChartDataXML.cshtml이라는*새 파일을 만듭니다.
6. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    코드는 먼저 `DataSet` 개체를 만듭니다. 이 개체는 XML 파일에서 읽은 데이터를 관리하고 스키마 파일의 정보에 따라 구성하는 데 사용됩니다. (코드의 맨 위에는 명령문이 `using SystemData`포함되어 있습니다. 개체를 사용하여 `DataSet` 작업하려면 이 작업이 필요합니다. 자세한 내용은 이 문서의 후반부에서 [ &quot;명령문 및&quot; 정규화된 이름 사용을](#SB_UsingStatements) 참조하십시오.

    다음으로 코드는 데이터 `DataView` 집합을 기반으로 개체를 만듭니다. 데이터 뷰는 차트가 &#8212;, 읽기 및 플롯에 바인딩할 수 있는 개체를 제공합니다. 이 `AddSeries` 시간 `xValue` 및 `yValues` 매개 변수가 `DataView` 개체로 설정된 경우를 제외하고, 배열 데이터를 차트화할 때 앞서 보았듯이 차트는 메서드를 사용하여 데이터에 바인딩됩니다.

    이 예제에서는 특정 차트 유형을 지정하는 방법도 보여 주어 도 있습니다. 메서드에 데이터가 추가되면 `AddSeries` `chartType` 매개 변수도 원형 차트를 표시하도록 설정됩니다.
7. 브라우저에서 페이지를 실행합니다. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"사용" 명령문 및 정규화된 이름
> 
> Razor 구문을 ASP.NET 웹 페이지를 ASP.NET .NET 프레임워크는 수천 개의 구성 요소(클래스)로 구성됩니다. 이러한 모든 클래스에서 작업할 수 있도록 라이브러리와 *namespaces*다소 비슷합니다. 예를 들어 `System.Web` 네임스페이스에는 브라우저/서버 통신을 `System.Xml` 지원하는 클래스가 포함되고, 네임스페이스에는 XML `System.Data` 파일을 만들고 읽는 데 사용되는 클래스가 포함되며, 네임스페이스에는 데이터로 작업할 수 있는 클래스가 포함됩니다.
> 
> .NET Framework에서 지정된 클래스에 액세스하려면 코드는 클래스 이름뿐만 아니라 클래스가 있는 네임스페이스도 알아야 합니다. 예를 들어 `Chart` 도우미를 사용하려면 코드는 `System.Web.Helpers.Chart` 네임스페이스()와`System.Web.Helpers`클래스 이름()을`Chart`결합한 클래스를 찾아야 합니다. 이 이름은 .NET Framework의 광대 함 내에서 완전하고 명확한 위치에 &#8212; 클래스의 *정식 자격으로* 된 이름으로 알려져 있습니다. 코드에서 다음과 같이 표시됩니다.
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 그러나 클래스 나 도우미를 참조 할 때마다 이러한 길고 정규화된 이름을 사용해야하는 것은 번거롭고 오류가 발생하기 쉽습니다. 따라서 클래스 이름을 더 쉽게 사용할 수 있도록 .NET Framework의 여러 네임스페이스 중에서 소수에 불과한 관심 있는 네임스페이스를 *가져올* 수 있습니다. 네임스페이스를 가져온 경우 정규화된 이름()`Chart``System.Web.Helpers.Chart`대신 클래스 이름()만 사용할 수 있습니다. 코드가 실행되고 클래스 이름이 발생하면 가져온 네임스페이스만 사용하여 해당 클래스를 찾을 수 있습니다.
> 
> Razor 구문이 있는 ASP.NET 웹 페이지를 사용하여 웹 페이지를 만드는 경우 일반적으로 `WebPage` 클래스, 다양한 도우미 등을 포함하여 매번 동일한 클래스 집합을 사용합니다. 웹 사이트를 만들 때마다 관련 네임스페이스를 가져오는 작업을 저장하기 위해 모든 웹 사이트에 대해 핵심 네임스페이스 집합을 자동으로 가져오도록 ASP.NET 구성됩니다. 그렇기 때문에 네임스페이스를 다루거나 지금까지 가져오지 않아도 됩니다. 작업한 모든 클래스는 이미 가져온 네임스페이스에 있습니다.
> 
> 그러나 경우에 따라 자동으로 가져오는 네임스페이스에 없는 클래스로 작업해야 하는 경우가 있습니다. 이 경우 해당 클래스의 정규화된 이름을 사용하거나 클래스가 포함된 네임스페이스를 수동으로 가져올 수 있습니다. 네임스페이스를 가져오려면 문서 `using` 의`import` 이전 예제에서 보았듯이 명령문(Visual Basic)을 사용합니다.
> 
> 예를 들어 `DataSet` 클래스는 네임스페이스에 `System.Data` 있습니다. Razor `System.Data` 페이지에서네임스페이스를 ASP.NET 자동으로 사용할 수 없습니다. 따라서 정규화된 이름을 `DataSet` 사용하여 클래스와 함께 작업하려면 다음과 같은 코드를 사용할 수 있습니다.
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 클래스를 `DataSet` 반복적으로 사용해야하는 경우 다음과 같은 네임 스페이스를 가져 온 다음 코드에서 클래스 이름만 사용할 수 있습니다.
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 참조하려는 `using` 다른 .NET Framework 네임스페이스에 대한 문을 추가할 수 있습니다. 그러나 언급했듯이 작업할 대부분의 클래스는 *.cshtml* 및 *.vbhtml* 페이지에서 사용하기 위해 ASP.NET 자동으로 가져오는 네임스페이스에 있기 때문에 이 작업을 자주 수행할 필요가 없습니다.

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>웹 페이지 내부에 차트 표시

지금까지 본 예제에서는 차트를 만든 다음 차트를 그래픽으로 브라우저에 직접 렌더링합니다. 그러나 대부분의 경우 브라우저에서차트뿐만 아니라 페이지의 일부로 차트를 표시하려고 합니다. 이렇게 하려면 2단계 프로세스가 필요합니다. 첫 번째 단계는 이미 본 것처럼 차트를 생성하는 페이지를 만드는 것입니다.

두 번째 단계는 결과 이미지를 다른 페이지에 표시하는 것입니다. 이미지를 표시하려면 이미지를 표시하는 `<img>` 것과 동일한 방식으로 HTML 요소를 사용합니다. 그러나 *.jpg* 또는 *.png* 파일을 참조하는 대신 `<img>` 차트를 만드는 `Chart` 도우미가 포함된 *.cshtml* 파일을 참조합니다. 표시 페이지가 실행되면 `<img>` 요소는 도우미의 `Chart` 출력을 얻고 차트를 렌더링합니다.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. *ShowChart.cshtml이라는*파일을 만듭니다.
2. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    코드는 `<img>` 요소를 사용하여 *ChartArrayBasic.cshtml* 파일에서 이전에 만든 차트를 표시합니다.
3. 브라우저에서 웹 페이지를 실행합니다. *ShowChart.cshtml* 파일은 *ChartArrayBasic.cshtml* 파일에 포함된 코드를 기반으로 차트 이미지를 표시합니다.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>차트 스타일 지정

도우미는 `Chart` 차트의 모양을 사용자 지정할 수 있는 많은 옵션을 지원합니다. 색상, 글꼴, 테두리 등을 설정할 수 있습니다. 차트의 모양을 사용자 지정하는 쉬운 방법은 *테마를*사용하는 것입니다. 테마는 글꼴, 색, 레이블, 색상표, 테두리 및 효과를 사용하여 렌더링하는 방법을 지정하는 정보의 모음입니다. 차트 의 스타일은 차트 유형을 나타내지 않습니다.

다음 표에는 기본 제공 테마가 나열되어 있습니다.

| 테마 | 설명 |
| --- | --- |
| `Vanilla` | 흰색 배경에 빨간색 열을 표시합니다. |
| `Blue` | 파란색 그라데이션 배경에 파란색 열을 표시합니다. |
| `Green` | 녹색 그라데이션 배경에 파란색 열을 표시합니다. |
| `Yellow` | 노란색 그라데이션 배경에 주황색 열을 표시합니다. |
| `Vanilla3D` | 흰색 배경에 3D 빨간색 열을 표시합니다. |

새 차트를 만들 때 사용할 테마를 지정할 수 있습니다.

1. *ChartStyleGreen.cshtml이라는*새 파일을 만듭니다.
2. 페이지의 기존 콘텐츠를 다음으로 바꿉습니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    이 코드는 데이터에 데이터베이스를 사용 하지만 개체를 `theme` 만들 때 매개 변수를 `Chart` 추가 하는 이전 예제와 동일 합니다. 다음은 변경된 코드를 보여 주며,

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 브라우저에서 페이지를 실행합니다. 이전과 동일한 데이터가 표시되지만 차트는 더 세련된 것처럼 보입니다. 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>차트 저장

이 문서에서 `Chart` 지금까지 보았듯이 도우미를 사용하면 도우미가 호출될 때마다 처음부터 차트를 다시 만듭니다. 필요한 경우 차트의 코드는 데이터베이스를 다시 쿼리하거나 XML 파일을 다시 읽고 데이터를 가져옵니다. 경우에 따라 쿼리하는 데이터베이스가 큰 경우 또는 XML 파일에 많은 데이터가 포함된 경우와 같이 복잡한 작업이 될 수 있습니다. 차트에 많은 데이터가 포함되지 않더라도 이미지를 동적으로 만드는 프로세스는 서버 리소스를 차지하며 많은 사람들이 차트를 표시하는 페이지 나 페이지를 요청하는 경우 웹 사이트의 성능에 영향을 미칠 수 있습니다.

차트를 만들 때 발생할 수 있는 성능 영향을 줄이려면 차트를 처음 작성한 다음 저장할 수 있습니다. 차트를 다시 생성하는 대신 다시 필요한 경우 저장된 버전을 가져와렌더링할 수 있습니다.

다음과 같은 방법으로 차트를 저장할 수 있습니다.

- (서버)에서 컴퓨터 메모리에 차트를 캐시합니다.
- 차트를 이미지 파일로 저장합니다.
- 차트를 XML 파일로 저장합니다. 이 옵션을 사용하면 차트를 저장하기 전에 차트를 수정할 수 있습니다.

### <a name="caching-a-chart"></a>차트 캐싱

차트를 만든 후 차트를 캐시할 수 있습니다. 차트를 캐싱하면 차트를 다시 표시해야 하는 경우 차트를 다시 만들 필요가 없습니다. 차트를 캐시에 저장하면 해당 차트에 고유해야 하는 키를 지정합니다.

서버의 메모리부족이 면 캐시에 저장된 차트가 제거될 수 있습니다. 또한 어떤 이유로든 응용 프로그램이 다시 시작되면 캐시가 지워집니다. 따라서 캐시된 차트로 작업하는 표준 방법은 항상 캐시에서 사용할 수 있는지 여부를 먼저 확인한 다음 만들지 않으면 만들거나 다시 만드는 것입니다.

1. 웹 사이트의 루트에서 *ShowCachedChart.cshtml이라는*파일을 만듭니다.
2. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    태그에는 `<img>` `src` *ChartSaveToCache.cshtml* 파일을 가리키고 쿼리 문자열로 페이지에 키를 전달하는 특성이 포함되어 있습니다. 키에는 myChartKey &quot;&quot;값이 포함되어 있습니다. *ChartSaveToCache.cshtml* 파일에는 `Chart` 차트를 만드는 도우미가 포함되어 있습니다. 잠시 후 이 페이지를 만듭니다.

    페이지 *끝에ClearCache.cshtml*이라는 페이지에 대 한 링크가 있다. 곧 만들 페이지입니다. 이 예제에 대한 캐싱을 테스트하려면 *ClearCache.cshtml이* 필요합니다 .
3. 웹 사이트의 루트에서 *ChartSaveToCache.cshtml이라는*새 파일을 만듭니다.
4. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    코드는 먼저 쿼리 문자열의 키 값으로 전달된 것이 있는지 여부를 확인합니다. 이 경우 코드는 `GetFromCache` 메서드를 호출하고 키를 전달하여 캐시에서 차트를 읽으려고 시도합니다. 해당 키 아래의 캐시에 차트가 처음 요청될 때 발생하는 것이 없는 것으로 판명되면 코드는 평소와 같이 차트를 만듭니다. 차트가 완료되면 코드는 을 호출하여 `SaveToCache`캐시에 저장합니다. 이 메서드에는 키가 필요하므로 나중에 차트를 요청할 수 있으며 차트를 캐시에 저장해야 하는 시간이 필요합니다. 차트를 캐시하는 정확한 시간은 차트가 나타내는 데이터가 변경될 수 있다고 생각한 빈도에 따라 달라집니다. 또한 `SaveToCache` 이 메서드는 차트에 `slidingExpiration` 액세스할 때마다 시간 시간 지정 카운터가 재설정되는 경우 매개 변수 &#8212; 이 방법을 사용합니다. 이 경우 실제로 는 차트의 캐시 항목이 마지막으로 차트에 액세스한 후 2분 후에 만료됨을 의미합니다. (슬라이딩 만료에 대한 대안은 절대 만료이므로 캐시 항목이 액세스 빈도에 관계없이 캐시에 넣은 후 정확히 2분 후에 만료됩니다.)

    마지막으로 코드는 메서드를 `WriteFromCache` 사용하여 캐시에서 차트를 가져오고 렌더링합니다. 이 메서드는 차트가 `if` 시작되었거나 캐시에 저장해야 하는지 여부에 관계없이 캐시에서 차트를 가져옵니다.

    예제에서 메서드에는 `AddTitle` 타임스탬프가 포함되어 있습니다. (제목에 &#8212; &#8212; `DateTime.Now` 현재 날짜와 시간을 추가합니다.)
5. *ClearCache.cshtml이라는* 새 페이지를 만들고 해당 콘텐츠를 다음 으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    이 페이지는 `WebCache` 도우미를 사용하여 *ChartSaveToCache.cshtml에*캐시된 차트를 제거합니다. 앞서 언급했듯이 일반적으로 이와 같은 페이지가 있을 필요는 없습니다. 캐싱을 더 쉽게 테스트할 수 있도록 여기에만 만듭니다.
6. 브라우저에서 *ShowCachedChart.cshtml* 웹 페이지를 실행합니다. 이 페이지에는 *ChartSaveToCache.cshtml* 파일에 포함된 코드를 기반으로 차트 이미지가 표시됩니다. 차트 제목에 타임스탬프가 말하는 내용을 기록해 둡니다. 

    ![설명: 차트 제목에 타임스탬프가 있는 기본 차트 그림](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 브라우저를 닫습니다.
8. *쇼캐시차트.cshtml을* 다시 실행합니다. 타임스탬프는 차트가 재생성되지 않고 대신 캐시에서 읽었음을 나타내는 이전과 동일합니다.
9. *ShowCachedChart.cshtml에서*캐시 **지우기** 링크를 클릭합니다. 이렇게 하면 캐시가 지워졌다고 보고하는 *ClearCache.cshtml로*이동합니다.
10. **쇼캐시차트로 돌아가기** 링크를 클릭하거나 웹매트릭스에서 *ShowCachedChart.cshtml을* 다시 실행합니다. 캐시가 지워졌기 때문에 이번에는 타임스탬프가 변경되었습니다. 따라서 코드는 차트를 다시 생성하고 캐시에 다시 넣어야 했습니다.

### <a name="saving-a-chart-as-an-image-file"></a>차트를 이미지 파일로 저장

차트를 서버에 이미지 파일(예: *.jpg* 파일)으로 저장할 수도 있습니다. 그런 다음 이미지 파일을 이미지와 같은 방식으로 사용할 수 있습니다. 장점은 파일이 임시 캐시에 저장되지 않고 저장된다는 것입니다. 새 차트 이미지를 서로 다른 시간(예: 매시간)에 저장한 다음 시간에 따라 발생하는 변경 내용을 영구적으로 기록할 수 있습니다. 웹 응용 프로그램에 이미지 파일을 넣을 서버의 폴더에 파일을 저장할 수 있는 권한이 있는지 확인해야 합니다.

1. 웹 사이트의 루트에서 아직 존재하지 않는 경우 * \_ChartFiles라는* 폴더를 만듭니다.
2. 웹 사이트의 루트에서 *ChartSave.cshtml이라는*새 파일을 만듭니다.
3. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    코드는 먼저 `File.Exists` 메서드를 호출하여 *.jpg* 파일이 있는지 확인합니다. 파일이 없으면 코드는 배열에서 새 `Chart` 파일을 만듭니다. 이번에는 코드가 메서드를 `Save` 호출하고 매개 `path` 변수를 전달하여 차트를 저장할 위치의 파일 경로 및 파일 이름을 지정합니다. 페이지 본문에서 `<img>` 요소는 *표시할 .jpg* 파일을 가리키는 경로를 사용합니다.
4. *ChartSave.cshtml 파일을 실행합니다.*
5. 웹매트릭스로 돌아갑니다. *chart01.jpg라는* 이미지 파일이 * \_ChartFiles* 폴더에 저장되었습니다.

### <a name="saving-a-chart-as-an-xml-file"></a>차트를 XML 파일로 저장

마지막으로 차트를 서버에 XML 파일로 저장할 수 있습니다. 차트를 캐싱하거나 차트를 파일에 저장하는 데 이 방법을 사용하면 원하는 경우 차트를 표시하기 전에 XML을 수정할 수 있다는 이점이 있습니다. 응용 프로그램에는 이미지 파일을 넣을 서버의 폴더에 대한 읽기/쓰기 권한이 있어야 합니다.

1. 웹 사이트의 루트에서 *ChartSaveXml.cshtml이라는*새 파일을 만듭니다.
2. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    이 코드는 XML 파일을 사용한다는 점을 제외하면 캐시에 차트를 저장하기 위해 이전에 본 코드와 유사합니다. 코드는 먼저 `File.Exists` 메서드를 호출하여 XML 파일이 있는지 확인합니다. 파일이 있는 경우 코드는 새 `Chart` 개체를 만들고 파일 `themePath` 이름을 매개 변수로 전달합니다. 이렇게 하면 XML 파일의 모든 것을 기반으로 차트가 만들어집니다. XML 파일이 아직 존재하지 않는 경우 코드는 정상과 같은 `SaveXml` 차트를 만들고 이를 저장하기 위해 호출합니다. 차트는 이전에 보았듯이 `Write` 메서드를 사용하여 렌더링됩니다.

    캐싱을 보여 준 페이지와 마찬가지로 이 코드에는 차트 제목에 타임스탬프가 포함됩니다.
3. *ChartDisplayXMLChart.cshtml이라는* 새 페이지를 만들고 다음 마크업을 추가합니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. *차트디스플레이XML차트.cshtml* 페이지를 실행합니다. 차트가 표시됩니다. 차트 제목에 있는 타임스탬프를 기록해 둡니다.
5. 브라우저를 닫습니다.
6. WebMatrix에서 * \_ChartFiles* 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 고침을**클릭한 다음 폴더를 엽니다. 이 폴더의 *XMLChart.xml* 파일은 `Chart` 도우미에 의해 만들어졌습니다. 

    ![설명: 차트 도우미에 의해 생성된 XMLChart.xml 파일을 보여주는 _ChartFiles 폴더입니다.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. *ChartDisplayXMLChart.cshtml* 페이지를 다시 실행합니다. 차트에는 페이지를 처음 실행했을 때와 동일한 타임스탬프가 표시됩니다. 이전에 저장한 XML에서 차트가 생성되기 때문입니다.
8. 웹매트릭스에서 * \_ChartFiles* 폴더를 열고 *XMLChart.xml* 파일을 삭제합니다.
9. *ChartDisplayXMLChart.cshtml* 페이지를 한 번 더 실행합니다. 이번에는 `Chart` 도우미가 XML 파일을 다시 만들어야 했기 때문에 타임스탬프가 업데이트됩니다. 원하는 경우 * \_ChartFiles* 폴더를 확인하고 XML 파일이 돌아왔다는 것을 확인합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)
- [ASP.NET 웹 페이지 사이트에서 캐싱을 사용하여 성능 향상](https://go.microsoft.com/fwlink/?LinkId=202903)
- [차트](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) 클래스(MSDN의 웹 페이지 API 참조 ASP.NET)
