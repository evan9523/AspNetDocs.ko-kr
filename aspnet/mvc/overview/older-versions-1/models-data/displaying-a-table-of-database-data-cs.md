---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 데이터베이스 데이터 테이블 표시(C#) | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 데이터베이스 레코드 집합을 표시하는 두 가지 방법을 보여 줍니다. HTML ta에서 데이터베이스 레코드 집합을 포맷하는 두 가지 방법을 보여 드리겠습니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542056"
---
# <a name="displaying-a-table-of-database-data-c"></a>데이터베이스 데이터의 테이블 표시(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> 이 자습서에서는 데이터베이스 레코드 집합을 표시하는 두 가지 방법을 보여 줍니다. HTML 테이블에서 데이터베이스 레코드 집합을 서식지정하는 두 가지 방법을 보여 드리겠습니다. 먼저 뷰 내에서 데이터베이스 레코드를 직접 포맷하는 방법을 보여 드리겠습니다. 다음으로 데이터베이스 레코드를 서식 지정할 때 부분을 활용하는 방법을 설명합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시하는 방법을 설명하는 것입니다. 먼저 Visual Studio에 포함된 스캐폴딩 도구를 사용하여 레코드 집합을 자동으로 표시하는 뷰를 생성하는 방법을 알아봅니다. 다음으로 데이터베이스 레코드를 서식 지정할 때 일부를 템플릿으로 사용하는 방법을 알아봅니다.

## <a name="create-the-model-classes"></a>모델 클래스 작성

Movies 데이터베이스 테이블의 레코드 집합을 표시할 예정입니다. Movies 데이터베이스 테이블에는 다음 열이 포함되어 있습니다.

<a id="0.3_table01"></a>

| **열 이름** | **데이터 유형** | **Null 허용** |
| --- | --- | --- |
| Id | Int | False |
| 제목 | 은바르르 (200) | False |
| 감독 | 응바르차르 (50) | False |
| 날짜 발표 | DateTime | False |

ASP.NET MVC 응용 프로그램에서 Movies 테이블을 나타내려면 모델 클래스를 만들어야 합니다. 이 자습서에서는 Microsoft 엔터티 프레임워크를 사용하여 모델 클래스를 만듭니다.

> [!NOTE] 
> 
> 이 자습서에서는 Microsoft 엔터티 프레임워크를 사용합니다. 그러나 LINQ에서 SQL, NHibernate 또는 ADO.NET ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용하기 위해 다양한 기술을 사용할 수 있다는 점을 이해하는 것이 중요합니다.

다음 단계에 따라 엔터티 데이터 모델 마법사를 시작합니다.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**선택.
2. **데이터** 범주를 선택하고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택합니다.
3. 데이터 모델에 *MoviesDBModel.edmx라는* 이름을 지정하고 **추가** 단추를 클릭합니다.

추가 단추를 클릭하면 엔터티 데이터 모델 마법사가 나타납니다(그림 1 참조). 다음 단계에 따라 마법사를 완료합니다.

1. 모델 내용 선택 단계에서 **데이터베이스에서 생성** 옵션을 **선택합니다.**
2. 데이터 **연결 선택** 단계에서 는 *MoviesDB.mdf* 데이터 연결 및 연결 설정에 *대해 MoviesDBEntities라는* 이름을 사용합니다. **다음** 단추를 클릭합니다.
3. 데이터베이스 **개체 선택** 단계에서 테이블 노드를 확장하고 동영상 테이블을 선택합니다. 네임스페이스 *모델을* 입력하고 **완료** 버튼을 클릭합니다.

[![SQL 클래스에 LINQ 만들기](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**그림 01**: SQL 클래스에 LINQ 만들기[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image2.png)

엔터티 데이터 모델 마법사를 완료하면 엔터티 데이터 모델 디자이너가 열립니다. 디자이너는 동영상 엔터티를 표시해야 합니다(그림 2 참조).

[![엔터티 데이터 모델 디자이너](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**그림 02**: 엔터티 데이터 모델 디자이너[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image4.png)

계속하기 전에 한 가지 변화를 만들어야 합니다. 엔터티 데이터 마법사는 Movies 데이터베이스 테이블을 나타내는 *Movies라는* 모델 클래스를 생성합니다. Movies 클래스를 사용하여 특정 영화를 나타내기 때문에 클래스의 이름을 *동영상* 대신 *Movie* 동영상(복수편이 아닌 단수)으로 수정해야 합니다.

디자이너 표면에서 클래스 이름을 두 번 클릭하고 클래스 이름을 동영상에서 동영상으로 변경합니다. 이렇게 변경한 후 **저장** 단추(플로피 디스크의 아이콘)를 클릭하여 Movie 클래스를 생성합니다.

## <a name="create-the-movies-controller"></a>동영상 컨트롤러 만들기

이제 데이터베이스 레코드를 나타낼 수 있는 방법이 있으므로 영화 컬렉션을 반환하는 컨트롤러를 만들 수 있습니다. 시각적 스튜디오 솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭하고 **컨트롤러 추가** 옵션(그림 3 참조)을 선택합니다.

[![컨트롤러 추가 메뉴](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**그림 03**: 컨트롤러 추가 메뉴[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image6.png)

컨트롤러 **추가** 대화 상자가 나타나면 컨트롤러 이름 MovieController를 입력합니다(그림 4 참조). 새 컨트롤러를 추가하려면 **추가** 단추를 클릭합니다.

[![컨트롤러 추가 대화 상자](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**그림 04**: 컨트롤러 추가 대화 상자[(클릭하여 전체 크기 이미지 보기)](displaying-a-table-of-database-data-cs/_static/image8.png)

데이터베이스 레코드 집합을 반환하도록 동영상 컨트롤러에서 노출하는 Index() 작업을 수정해야 합니다. 목록 1의 컨트롤러처럼 보이게 하여 컨트롤러를 수정합니다.

**목록 1 – 컨트롤러\MovieController.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

목록 1에서 MoviesDBEntities 클래스는 MoviesDB 데이터베이스를 나타내는 데 사용됩니다. 이 클래스를 사용하려면 다음과 같이 MvcApplication1.Models 네임스페이스를 가져와야 합니다.

MvcApplication1.모델 사용;

식 *엔터티입니다. MovieSet.ToList()는* Movies 데이터베이스 테이블의 모든 동영상 집합을 반환합니다.

## <a name="create-the-view"></a>뷰 만들기

HTML 테이블에 데이터베이스 레코드 집합을 표시하는 가장 쉬운 방법은 Visual Studio에서 제공하는 스캐폴딩을 활용하는 것입니다.

메뉴 옵션 **빌드, 빌드 솔루션을**선택하여 응용 프로그램을 빌드합니다. **보기 추가** 대화 상자를 열기 전에 응용 프로그램을 빌드해야 하거나 데이터 클래스가 대화 상자에 나타나지 않습니다.

Index() 작업을 마우스 오른쪽 단추로 클릭하고 **보기 추가** 옵션을 선택합니다(그림 5 참조).

[![뷰 추가](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**그림 05**: 보기 추가[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image10.png)

뷰 **추가** 대화 상자에서 **강력한 형식의 뷰 만들기라는 레이블이**붙은 확인란을 선택합니다. Movie 클래스를 **뷰 데이터 클래스로**선택합니다. *목록을* 뷰 **콘텐츠로** 선택합니다(그림 6 참조). 이러한 옵션을 선택하면 동영상 목록이 표시되는 강력한 형식의 뷰가 생성됩니다.

[![보기 추가 대화 상자](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**그림 06**: 추가 보기 대화[상자(클릭하여 전체 크기 이미지 보기)](displaying-a-table-of-database-data-cs/_static/image12.png)

**추가** 단추를 클릭하면 목록 2의 보기가 자동으로 생성됩니다. 이 보기에는 동영상 컬렉션을 반복하고 동영상의 각 속성을 표시하는 데 필요한 코드가 포함되어 있습니다.

**목록 2 – 보기\영화\인덱스.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

메뉴 옵션 **디버그, 디버깅 시작(또는** F5 키 를 누르기)을 선택하여 응용 프로그램을 실행할 수 있습니다. 응용 프로그램을 실행실행하여 인터넷 익스플로러를 시작합니다. /동영상 URL로 이동하면 그림 7의 페이지가 표시됩니다.

[![영화 테이블](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**그림 07**: 동영상 표[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image14.png)

그림 7에서 데이터베이스 레코드 그리드의 모양에 대해 아무것도 좋아하지 않는 경우 인덱스 보기를 수정하기만 하면 됩니다. 예를 들어 인덱스 보기를 수정하여 *해제된* *날짜로* 날짜 해제 헤더를 변경할 수 있습니다.

## <a name="create-a-template-with-a-partial"></a>부분 템플릿 만들기

뷰가 너무 복잡해지면 뷰를 부분적으로 나누는 것이 좋습니다. 부분적인 부분 설정을 사용하면 뷰를 더 쉽게 이해하고 유지할 수 있습니다. 각 동영상 데이터베이스 레코드의 서식을 지정하기 위해 템플릿으로 사용할 수 있는 부분을 만듭니다.

다음 단계를 수행하여 일부를 만듭니다.

1. View\Movie 폴더를 마우스 오른쪽 단추로 클릭하고 **보기 추가**옵션을 선택합니다.
2. 레이블이 붙은 확인란을 *선택합니다.ascx 부분 뷰 만들기.*
3. 부분 *동영상 템플릿의*이름을 지정합니다.
4. 레이블이 붙은 확인란을 **선택합니다.**
5. 뷰 데이터 *클래스로*동영상 입니다.
6. *보기 내용으로*비어를 선택합니다.
7. **추가** 단추를 클릭하여 프로젝트에 일부를 추가합니다.

이 단계를 완료한 후 MovieTemplate 일부를 수정하여 목록 3처럼 보이게 합니다.

**목록 3 – 보기\영화\영화템플릿.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

목록 3의 부분 레코드 행에 대한 템플릿이 포함되어 있습니다.

목록 4에서 수정된 인덱스 보기는 동영상 템플릿 일부를 사용합니다.

**목록 4 – 보기\영화\인덱스.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

목록 4의 보기에는 모든 동영상을 반복하는 foreach 루프가 포함되어 있습니다. 각 동영상에 대해 MovieTemplate 부분의 포맷을 사용하여 동영상의 서식을 지정합니다. MovieTemplate는 RenderPartial() 도우미 메서드를 호출하여 렌더링됩니다.

수정된 인덱스 보기는 데이터베이스 레코드의 동일한 HTML 테이블을 렌더링합니다. 그러나 보기가 크게 단순화되었습니다.

RenderPartial() 메서드는 문자열을 반환하지 않으므로 대부분의 다른 도우미 메서드와 다릅니다. 따라서 % Html.RenderPartial()를 &lt;사용하여 RenderPartial() 메서드를 호출해야 합니다. %= Html.RenderPartial(대신 %);&gt; &lt; %&gt;.

## <a name="summary"></a>요약

이 자습서의 목표는 HTML 테이블에 데이터베이스 레코드 집합을 표시하는 방법을 설명하는 것이었습니다. 먼저 Microsoft 엔터티 프레임워크를 활용하여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환하는 방법을 배웠습니다. 다음으로 Visual Studio 스캐폴딩을 사용하여 항목 컬렉션을 자동으로 표시하는 뷰를 생성하는 방법을 배웠습니다. 마지막으로 일부를 활용하여 뷰를 단순화하는 방법을 배웠습니다. 각 데이터베이스 레코드의 서식을 지정할 수 있도록 일부를 템플릿으로 사용하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-linq-to-sql-cs.md)
> [다음](performing-simple-validation-cs.md)
