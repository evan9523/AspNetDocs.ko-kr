---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: (VB) 텍스트 상자에 특정 문자만 허용 | Microsoft Docs
author: wenz
description: ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다. 그러나이 여전히 해도 사용자 입력 으로부터 잘못 된...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0f13140fcafd666a89c27acb829e4e762eff29
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127454"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>텍스트 상자에 특정 문자만 허용(VB)

by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다. 그러나이 여전히 해도 잘못 된 문자를 입력 하 고 양식을 제출 하는 동안 사용자가 있습니다.

## <a name="overview"></a>개요

ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다. 그러나이 여전히 해도 잘못 된 문자를 입력 하 고 양식을 제출 하는 동안 사용자가 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX Control Toolkit에 포함 된 `FilteredTextBox` 입력란을 확장 하는 컨트롤입니다. 활성화 되 면 특정 문자 집합만 필드에 입력할 수 있습니다.

이렇게 하려면 먼저 해야 일반적으로 ASP.NET AJAX `ScriptManager` 도 ASP.NET AJAX Control Toolkit에서 사용 되는 JavaScript 라이브러리를 로드 하는:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

그런 다음 텍스트 상자를 해야합니다.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

마지막으로 `FilteredTextBoxExtender` 문자는 사용자가 입력 수를 제한 하는 컨트롤을 담당 합니다. 먼저 설정 합니다 `TargetControlID` 특성을 합니다 `ID` 의 `TextBox` 컨트롤. 그런 다음 중 하나를 선택 `FilterType` 값:

- `Custom` 기본값은 유효한 문자 목록을 제공 해야 합니다.
- `LowercaseLetters` 소문자만
- `Numbers` 숫자만
- `UppercaseLetters` 대문자로

경우는 `Custom FilterType` 사용 되는 `ValidChars` 속성 집합 이어야 하며 입력 될 수 있는 문자 목록을 제공 합니다. 그런데: 텍스트 상자에 텍스트를 붙여 넣습니다. 하려는 모든 유효 하지 않은 문자 제거 됩니다.

여기에 대 한 태그를 `FilteredTextBoxExtender` 만 숫자를 허용 하는 컨트롤 (또한 되었을 수 있는 `FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

JavaScript가 설정 된 경우에 문자를 입력 하 고 페이지를 실행 작동 하지 않습니다. 그러나 숫자 페이지에 표시 합니다. 하지만 보호 `FilteredTextBox` 제공 완벽 아닙니다. JavaScript를 사용 하는 경우 추가 유효성 검사 의미, 즉, ASP를 사용 해야 하므로 모든 데이터를 텍스트 상자에 입력할 수 있습니다. NET의 유효성 검사를 제어 합니다.

[![숫자만 입력할 수](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

숫자만 입력 될 수 있습니다 ([클릭 하 여 큰 이미지 보기](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](allowing-only-certain-characters-in-a-text-box-cs.md)
