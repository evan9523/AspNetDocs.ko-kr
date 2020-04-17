---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML 편집기 컨트롤을 사용하려면 어떻게 해야 합니까? (VB) | 마이크로 소프트 문서
author: rick-anderson
description: HTMLEditor는 도구 모음의 버튼을 통해 HTML 콘텐츠를 쉽게 만들고 편집 할 수있는 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542835"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>HTML 편집기 컨트롤을 사용하려면 어떻게 해야 합니까? (VB)

[로 마이크로 소프트](https://github.com/microsoft)

> HTMLEditor는 도구 모음의 버튼을 통해 HTML 콘텐츠를 쉽게 만들고 편집 할 수있는 ASP.NET AJAX 컨트롤입니다.

이 자습서의 목표는 AJAX 제어 도구 키트에 포함된 HTML 편집기 컨트롤에 대한 개요를 제공하는 것입니다. HTML 편집기에는 글꼴 크기 변경, 글꼴 선택, 배경 색 변경, 전경 색상 수정, 링크 추가, 이미지 추가, 텍스트 정렬 변경, 잘라내기, 복사 및 붙여넣기 작업 수행(그림 1 참조)에 대한 옵션이 포함되어 있습니다.

[![HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**그림 01**: HTML 편집기[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-vb/_static/image2.png)

HTML 편집기를 사용하면 디자인 모드를 사용하여 콘텐츠를 입력하거나 HTML을 직접 입력할 수 있습니다. HTML 콘텐츠를 미리 볼 수 있는 옵션도 제공됩니다(그림 2 참조).

[![디자인, HTML 및 미리 보기 버튼](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**그림 02**: 디자인, HTML 및 미리보기 버튼[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-vb/_static/image4.png)

이 자습서에서는 HTML 편집기를 표시 하는 방법, HTML 편집기에 나타나는 도구 모음 단추를 사용자 지정 하는 방법 및 교차 사이트 스크립팅 공격을 방지 하는 방법에 대해 알아봅니다.

## <a name="displaying-the-html-editor"></a>HTML 편집기 표시

ASP.NET 페이지에서 HTML 편집기를 사용하려면 먼저 페이지에 ScriptManager 컨트롤을 추가해야 합니다. ScriptManager 컨트롤은 Visual Studio/Visual 웹 개발자 익스프레스 도구 상자의 AJAX 확장 탭 아래에 있습니다.

페이지의 다른 컨트롤보다 앞에 ScriptManager 컨트롤을 페이지 상단에 배치해야 합니다. 예를 들어, 열기 서버 측 &lt;양식&gt; 태그 바로 아래에 배치할 수 있습니다.

HTML 편집기 컨트롤은 나머지 AJAX 제어 도구 키트 컨트롤과 함께 도구 상자에 있습니다. 편집기 컨트롤의 이름이 지정됩니다(그림 3 참조).

[![HTML 편집기 컨트롤](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**그림 03**: HTML 편집기 컨트롤[(클릭으로 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-vb/_static/image6.png)

HTML 편집기를 페이지로 드래그한 후 속성 시트에서 해당 속성을 설정할 수 있습니다. 예를 들어 일반적으로 폭 및 높이 속성을 설정하려고 합니다. 목록 1에는 HTML 편집기가 포함된 ASP.NET 페이지의 소스가 포함되어 있습니다.

**목록 1 - SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

목록 1의 페이지에는 HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤이 포함되어 있습니다. 단추를 클릭하면 HTML 편집기의 내용이 리터럴 컨트롤에 나타납니다(그림 4 참조).

[![HTML 편집기와 함께 양식 제출](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**그림 04**: HTML 편집기로 양식 제출[(클릭하려면 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-vb/_static/image8.png)

HTML 편집기 콘텐츠 속성은 HTML 편집기에 입력된 HTML 콘텐츠를 검색하는 데 사용됩니다. 이 HTML 콘텐츠에는 자바스크립트가 포함될 수 있습니다. 다음 섹션에서는 JavaScript 주입 공격을 방지하는 방법에 대해 설명합니다.

## <a name="customizing-the-html-editor-toolbar"></a>HTML 편집기 도구 모음 사용자 지정

편집기에서 나타나는 단추를 정확하게 사용자 지정할 수 있습니다. 예를 들어 사용자가 HTML 편집기를 HTML 모드로 전환하지 못하도록 HTML 탭을 제거할 수 있습니다. 또는 사용자가 포럼 메시지 게시물에서 지나치게 큰 텍스트를 만들지 못하도록 글꼴 크기 드롭다운 목록을 제거할 수 있습니다(그림 5 참조).

[![사용자 정의 HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**그림 05**: 사용자 정의 HTML 편집기[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-html-editor-control-vb/_static/image10.png)

기본 편집기 클래스에서 새 HTML 편집기 파생 을 통해 도구 모음 단추를 사용자 지정 합니다. 예를 들어 목록 2의 사용자 지정 편집기에는 굵게 및 기울임꼴에 대한 도구 모음 단추만 포함되어 있습니다. 다른 모든 도구 모음 버튼이 제거되었습니다. 또한 HTML 탭이 편집기 하단에서 제거되었습니다(하지만 디자인 및 미리 보기 탭은 여전히 있습니다).

**목록 2\_- 앱 코드\사용자 지정 편집기.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

클래스가 자동으로 컴파일되도록 앱\_코드 폴더에 목록 2의 클래스를 추가해야 합니다. 앱\_코드 폴더가 웹 사이트에 없는 경우 폴더를 추가하기만 하면 됩니다.

사용자 지정 편집기를 만든 후 일반 HTML 편집기를 추가하는 것과 동일한 방법으로 ASP.NET 페이지에 추가할 수 있습니다(목록 3 참조).

**목록 3 - 쇼 사용자 정의 편집기.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>XSS(교차 사이트 스크립팅) 공격 방지

사용자의 입력을 수락하고 웹 사이트에 해당 입력을 다시 표시할 때마다 XSS(교차 사이트 스크립팅) 공격에 대한 웹 사이트를 열 수 있습니다. 이론적으로 악의적인 해커는 입력이 다시 표시될 때 실행되는 JavaScript 코드를 제출할 수 있습니다. 자바 스크립트는 사용자 암호 또는 기타 중요한 정보를 도용하는 데 사용할 수 있습니다.

일반적으로 웹 페이지에 표시하기 전에 사용자로부터 검색한 입력을 암호화하여 XSS 공격을 물리칠 수 있습니다. 그러나 HTML 편집기의 출력을 인코딩하면 스크립트 &lt;&gt; 태그를 인코딩할 뿐만 아니라 모든 HTML 태그도 인코딩됩니다. 즉, 글꼴 유형, 글꼴 크기 및 배경 색과 같은 모든 서식이 손실됩니다.

암호, 신용 카드 번호 및 주민등록 번호와 같은 사용자로부터 중요한 정보를 수집하는 경우 HTML 편집기에서 사용자로부터 검색하는 인코딩되지 않은 콘텐츠를 표시해서는 안 됩니다. HTML 콘텐츠를 다시 표시하지 않거나 신뢰할 수 있는 당사자가 HTML 콘텐츠를 웹 사이트에 제출하는 경우에만 HTML 편집기를 사용해야 합니다.

예를 들어 블로그 응용 프로그램을 만들고 있다고 가정해 보겠습니다. 이 경우 블로그 게시물을 작성할 때 HTML 편집기를 사용 하는 것이 합리적이다. 당신은 블로그 게시물을 제출하는 유일한 사람이고, 아마도, 당신은 악의적 인 자바 스크립트를 제출하지 자신을 신뢰할 수 있습니다. 그러나 익명 사용자가 주석을 게시할 수 있도록 허용할 때 HTML 편집기를 사용하는 것은 의미가 없습니다. 사용자가 암호와 같은 중요한 정보를 제출하는 경우 특히 주의해야 합니다. 악의적인 사용자가 암호를 도용하는 데 적합한 JavaScript가 포함된 댓글을 게시할 수 있습니다.

## <a name="summary"></a>요약

이 자습서에서는 AJAX 제어 도구 키트에 포함된 HTML 편집기 컨트롤에 대한 간략한 개요를 제공했습니다. HTML 편집기를 사용하여 사용자의 풍부한 콘텐츠를 수락하고 콘텐츠를 서버에 제출하는 방법을 배웠습니다. 또한 HTML 편집기에서 표시되는 도구 모음 단추를 사용자 지정하는 방법에 대해서도 설명했습니다. 마지막으로 HTML 편집기를 사용하여 잠재적으로 악의적인 입력을 수락할 때 사이트 간 스크립팅 공격을 방지하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](how-do-i-use-the-html-editor-control-cs.md)
