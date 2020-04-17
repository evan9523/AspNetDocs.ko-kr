---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 마스터 페이지 보기(C#)를 사용할 수 있는 페이지 레이아웃 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다. 당신은 사용할 수 있습니다 ...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542523"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a>보기 마스터 페이지를 사용하여 페이지 레이아웃 만들기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> 이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다. 예를 들어 보기 마스터 페이지를 사용하여 두 열 페이지 레이아웃을 정의하고 웹 응용 프로그램의 모든 페이지에 대해 두 열 레이아웃을 사용할 수 있습니다.

## <a name="creating-page-layouts-with-view-master-pages"></a>마스터 페이지 보기를 사용할 수 있는 페이지 레이아웃 만들기

이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다. 예를 들어 보기 마스터 페이지를 사용하여 두 열 페이지 레이아웃을 정의하고 웹 응용 프로그램의 모든 페이지에 대해 두 열 레이아웃을 사용할 수 있습니다.

또한 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에서 공통 콘텐츠를 공유할 수도 있습니다. 예를 들어 보기 마스터 페이지에 웹 사이트 로고, 탐색 링크 및 배너 광고를 배치할 수 있습니다. 이렇게 하면 응용 프로그램의 모든 페이지에 이 콘텐츠가 자동으로 표시됩니다.

이 자습서에서는 새 보기 마스터 페이지를 만들고 마스터 페이지를 기반으로 새 보기 콘텐츠 페이지를 만드는 방법을 알아봅니다.

### <a name="creating-a-view-master-page"></a>뷰 마스터 페이지 만들기

먼저 두 개의 열 레이아웃을 정의하는 뷰 마스터 페이지를 만들어 보겠습니다. View\Shared 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**및 **MVC 뷰 마스터 페이지** 템플릿을 선택하여 MVC 프로젝트에 새 뷰 마스터 페이지를 추가합니다(그림 1 참조).

[![보기 마스터 페이지 추가](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

**그림 01**: 뷰 마스터 페이지 추가[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)

응용 프로그램에서 두 개 이상의 뷰 마스터 페이지를 만들 수 있습니다. 각 뷰 마스터 페이지는 다른 페이지 레이아웃을 정의할 수 있습니다. 예를 들어 특정 페이지에 2열 레이아웃과 다른 페이지에 3열 레이아웃이 있어야 할 수 있습니다.

뷰 마스터 페이지는 표준 ASP.NET MVC 보기와 매우 유사합니다. 그러나 일반 보기와 달리 뷰 마스터 페이지에는 `<asp:ContentPlaceHolder>` 하나 이상의 태그가 포함되어 있습니다. 태그는 `<contentplaceholder>` 개별 콘텐츠 페이지에서 재정의할 수 있는 마스터 페이지의 영역을 표시하는 데 사용됩니다.

예를 들어 목록 1의 뷰 마스터 페이지는 두 개의 열 레이아웃을 정의합니다. 여기에는 `<contentplaceholder>` 두 개의 태그가 포함되어 있습니다. 각 `<ContentPlaceHolder>` 열에 대해 하나씩.

**리스팅 1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

목록 1의 뷰 마스터 페이지의 본문에는 두 열에 해당하는 두 `<div>` 개의 태그가 포함되어 있습니다. 계단식 스타일 시트 열 클래스는 `<div>` 두 태그에 모두 적용됩니다. 이 클래스는 마스터 페이지 의 맨 위에 선언된 스타일 시트에 정의되어 있습니다. 디자인 보기로 전환하여 뷰 마스터 페이지가 렌더링되는 방법을 미리 볼 수 있습니다. 소스 코드 편집기 왼쪽 하단에 있는 디자인 탭을 클릭합니다(그림 2 참조).

[![디자이너의 마스터 페이지 미리 보기](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

**그림 02**: 디자이너의 마스터 페이지 미리 보기[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)

### <a name="creating-a-view-content-page"></a>보기 콘텐츠 페이지 만들기

뷰 마스터 페이지를 만든 후 보기 마스터 페이지를 기반으로 하나 이상의 보기 콘텐츠 페이지를 만들 수 있습니다. 예를 들어 View\Home 폴더를 마우스 오른쪽 단추로 클릭하고, **추가, 새 항목**선택, **MVC 보기 콘텐츠 페이지** 템플릿 선택, Index.aspx 이름 입력 및 **추가** 단추를 클릭하여 홈 컨트롤러의 인덱스 보기 콘텐츠 페이지를 만들 수 있습니다(그림 3 참조).

[![보기 콘텐츠 페이지 추가](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

**그림 03**: 보기 콘텐츠 페이지 추가[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)

추가 단추를 클릭하면 보기 콘텐츠 페이지와 연결할 보기 마스터 페이지를 선택할 수 있는 새 대화 상자가 나타납니다(그림 4 참조). 이전 섹션에서 만든 Site.master 보기 마스터 페이지로 이동할 수 있습니다.

[![마스터 페이지 선택](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

**그림 04**: 마스터 페이지 선택[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)

Site.master 마스터 페이지를 기반으로 새 보기 콘텐츠 페이지를 만든 후 목록 2에서 파일을 가져옵니다.

**리스팅 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

이 보기에는 `<asp:Content>` 뷰 마스터 페이지의 각 `<asp:ContentPlaceHolder>` 태그에 해당하는 태그가 포함되어 있습니다. 각 `<asp:Content>` 태그에는 재정의하는 특정 `<asp:ContentPlaceHolder>` 을 가리키는 ContentPlaceHolderID 특성이 포함됩니다.

또한 목록 2의 콘텐츠 보기 페이지에는 일반적인 HTML 태그가 포함되어 있지 않습니다. 예를 들어, 개폐 `<html>` 또는 `<head>` 태그를 포함하지 않습니다. 모든 일반 열기 및 닫는 태그는 뷰 마스터 페이지에 포함됩니다.

보기 콘텐츠 페이지에 표시하려는 모든 콘텐츠는 `<asp:Content>` 태그 내에 배치해야 합니다. 이러한 태그 외부에 HTML 또는 기타 콘텐츠를 배치하면 페이지를 보려고 할 때 오류가 발생합니다.

콘텐츠 보기 페이지의 마스터 페이지에서 `<asp:ContentPlaceHolder>` 모든 태그를 재정의할 필요는 없습니다. `<asp:ContentPlaceHolder>` 태그를 특정 콘텐츠로 바꾸려는 경우에만 태그를 재정의하면 됩니다.

예를 들어 목록 3의 수정된 인덱스 `<asp:Content>` 보기에는 두 개의 태그만 포함됩니다. 각 태그에는 `<asp:Content>` 일부 텍스트가 포함되어 있습니다.

**리스팅 3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

목록 3의 보기가 요청되면 그림 5의 페이지를 렌더링합니다. 뷰는 두 개의 열이 있는 페이지를 렌더링합니다. 또한 뷰 콘텐츠 페이지의 콘텐츠가 뷰 마스터 페이지의 콘텐츠와 병합됩니다.

[![인덱스 보기 콘텐츠 페이지](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

**그림 05**: 색인 보기 콘텐츠 페이지[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)

### <a name="modifying-view-master-page-content"></a>보기 마스터 페이지 콘텐츠 수정

뷰 마스터 페이지로 작업할 때 거의 즉시 발생하는 한 가지 문제는 다른 보기 콘텐츠 페이지가 요청될 때 뷰 마스터 페이지 콘텐츠를 수정하는 문제입니다. 예를 들어 웹 응용 프로그램의 각 페이지에 고유한 제목을 두도록 할 수 있습니다. 그러나 제목은 보기 콘텐츠 페이지가 아니라 뷰 마스터 페이지에 선언됩니다. 그렇다면 각 보기 콘텐츠 페이지의 페이지 제목을 어떻게 사용자 지정합니까?

보기 콘텐츠 페이지에 표시되는 제목을 수정하는 방법에는 두 가지가 있습니다. 먼저 보기 콘텐츠 페이지 상단에 선언된 `<%@ page %>` 지시의 제목 특성에 페이지 제목을 할당할 수 있습니다. 예를 들어 페이지 제목 "Super Great Website"를 색인 보기에 할당하려면 색인 보기 맨 위에 다음 지시문을 포함할 수 있습니다.

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

색인 보기가 브라우저에 렌더링되면 원하는 제목이 브라우저 제목 표시줄에 나타납니다.

[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)

제목 특성이 작동하려면 마스터 보기 페이지가 충족해야 하는 중요한 요구 사항이 하나 있습니다. 뷰 마스터 페이지에는 `<head runat="server">` 헤더에 대한 `<head>` 일반 태그 대신 태그가 포함되어야 합니다. 태그에 `<head>` runat="server" 특성이 포함되지 않으면 제목이 나타나지 않습니다. 기본 보기 마스터 페이지에는 `<head runat="server">` 필수 태그가 포함됩니다.

개별 보기 콘텐츠 페이지에서 마스터 페이지 콘텐츠를 수정하는 또 다른 방법은 `<asp:ContentPlaceHolder>` 태그에서 수정할 영역을 래핑하는 것입니다. 예를 들어 제목뿐만 아니라 마스터 뷰 페이지에서 렌더링되는 메타 태그도 변경하려고 한다고 가정해 보겠습니다. 목록 4의 마스터 보기 `<asp:ContentPlaceHolder>` 페이지에는 `<head>` 태그 내에 태그가 포함되어 있습니다.

**리스팅 4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

목록 4의 `<asp:ContentPlaceHolder>` 태그에는 기본 제목및 기본 메타 태그와 같은 기본 콘텐츠가 포함되어 있습니다. 개별 보기 콘텐츠 페이지에서 `<asp:ContentPlaceHolder>` 이 태그를 재정의하지 않으면 기본 콘텐츠가 표시됩니다.

목록 5의 `<asp:ContentPlaceHolder>` 콘텐츠 보기 페이지는 사용자 지정 제목 및 사용자 지정 메타 태그를 표시하기 위해 태그를 재정의합니다.

**리스팅 5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a>요약

이 자습서에서는 마스터 페이지를 보고 콘텐츠 페이지를 볼 수 있는 기본 소개를 제공했습니다. 새 보기 마스터 페이지를 만들고 이를 기반으로 보기 콘텐츠 페이지를 만드는 방법을 배웠습니다. 또한 특정 보기 콘텐츠 페이지에서 보기 마스터 페이지의 내용을 수정하는 방법도 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [다음](passing-data-to-view-master-pages-cs.md)
