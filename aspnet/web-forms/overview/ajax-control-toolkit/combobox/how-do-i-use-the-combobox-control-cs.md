---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 'ComboBox 컨트롤을 사용 어떻게 할까요?? (C #) | Microsoft Docs'
author: rick-anderson
description: ComboBox는 사용자가 선택할 수 있는 옵션 목록과 함께 텍스트 상자의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 035bcb2fb6cce246b904c295aba15efd17c2c232
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045067"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>ComboBox 컨트롤을 사용 어떻게 할까요?? (C#)

[Microsoft](https://github.com/microsoft) 에서

> ComboBox는 사용자가 선택할 수 있는 옵션 목록과 함께 텍스트 상자의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.

이 자습서의 목표는 AJAX 컨트롤 Toolkit ComboBox 컨트롤을 설명 하는 것입니다. ComboBox는 표준 ASP.NET DropDownList 컨트롤과 TextBox 컨트롤을 조합 하는 것 처럼 작동 합니다. 기존 항목 목록에서 선택 하거나 새 항목을 입력할 수 있습니다.

ComboBox는 자동 완성 컨트롤 extender와 유사 하지만 컨트롤이 여러 시나리오에서 사용 됩니다. 자동 완성 extender는 일치 하는 항목을 가져오기 위해 웹 서비스를 쿼리 합니다. 반면 콤보 상자 컨트롤은 항목 집합을 사용 하 여 초기화 됩니다. 자동 완성 extender를 사용 하는 것은 작은 데이터 집합을 사용 하는 경우에 적합 합니다. (수백만 개의 자동차 부분), 작은 데이터 집합을 사용 하는 경우 (수십 개의 자동차 부분)에 적합 합니다.

## <a name="selecting-from-a-static-list-of-items"></a>항목의 정적 목록에서 선택

ComboBox 컨트롤을 사용 하는 간단한 샘플부터 살펴보겠습니다. 드롭다운 목록에서 항목의 정적 목록을 표시 하 려 한다고 가정 합니다. 그러나 목록이 완전 하지 않을 가능성을 열어 둘 수 있습니다. 사용자가 목록에 사용자 지정 값을 입력할 수 있도록 하려고 합니다.

새 ASP.NET Web Forms 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다. 프로젝트에 새 ASP.NET 페이지를 추가 하 고 디자인 뷰로 전환 합니다.

페이지에서 ComboBox 컨트롤을 사용 하려면 페이지에 ScriptManager 컨트롤을 추가 해야 합니다. AJAX 확장 탭 아래의 ScriptManager 컨트롤을 디자이너 화면으로 끌어 옵니다. 페이지 맨 위에 ScriptManager 컨트롤을 추가 해야 합니다. 서버 쪽 양식 열기 태그 바로 아래에 추가할 수 있습니다 &lt; &gt; .

그런 다음 ComboBox 컨트롤을 페이지로 끌어 옵니다. 다른 AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 extender를 사용 하 여 도구 상자에서 ComboBox 컨트롤을 찾을 수 있습니다 (그림 1 참조).

[![비즈니스 카드를 만드는 간단한 양식](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**그림 01**: 도구 상자에서 ComboBox 컨트롤 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image2.png))

콤보 상자 컨트롤을 사용 하 여 선택 항목의 정적 목록을 표시 합니다. 사용자는 세 가지 선택 항목인 고급, 중간 및 핫 (그림 2 참조) 목록에서 spiciness의 특정 수준을 선택할 수 있습니다.

[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**그림 02**: 정적 항목 목록에서 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image4.png))

콤보 상자 컨트롤에 이러한 선택 항목을 추가할 수 있는 두 가지 방법이 있습니다. 먼저 디자인 뷰의 컨트롤 위로 마우스를 가져가면 옵션 편집 작업 옵션을 선택 하 고 항목 편집기를 엽니다 (그림 3 참조).

[![ComboBox 항목 편집](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**그림 03**: 콤보 상자 항목 편집 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image6.png))

두 번째 옵션은 소스 뷰에서 열기 및 닫기 &lt; asp: ComboBox 태그 사이에 항목 목록을 추가 하는 것입니다 &gt; . 목록 1의 페이지에는 항목 목록이 있는 업데이트 된 콤보 상자가 있습니다.

**목록 1-정적 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

목록 1에서 페이지를 열면 ComboBox에서 기존 옵션 중 하나를 선택할 수 있습니다. 즉, 콤보 상자는 DropDownList 컨트롤과 똑같이 작동 합니다.

그러나 기존 목록에 없는 새 선택 항목 (예: 슈퍼 Spicy)을 입력 하는 옵션도 있습니다. 따라서 ComboBox는 TextBox 컨트롤 처럼 작동 합니다.

기존 항목을 선택 하거나 사용자 지정 항목을 입력 하 든 상관 없이 양식을 제출할 때 선택한 항목은 레이블 컨트롤에 표시 됩니다. 양식을 제출할 때 btnSubmit \_ 클릭 처리기가 실행 되 고 레이블을 업데이트 합니다 (그림 4 참조).

[![선택한 항목 표시](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**그림 04**: 선택한 항목 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image8.png))

ComboBox는 양식이 제출 된 후 선택 된 항목을 검색 하기 위해 DropDownList 컨트롤과 동일한 속성을 지원 합니다.

- SelectedItem. 텍스트-선택한 항목의 Text 속성 값을 표시 합니다.
- SelectedItem. 값-선택한 항목의 Value 속성 값을 표시 하거나 ComboBox에 입력 한 텍스트를 표시 합니다.
- SelectedValue-이 속성을 사용 하면 선택 된 기본 항목을 지정 하는 것을 제외 하 고 SelectedItem.

콤보 상자에 사용자 지정 선택 항목을 입력 하면 사용자 지정 항목이 SelectedItem. Text 및 SelectedItem. Value 속성 둘 다에 할당 됩니다.

## <a name="selecting-the-list-of-items-from-the-database"></a>데이터베이스에서 항목 목록 선택

ComboBox가 데이터베이스에서 표시 하는 항목 목록을 검색할 수 있습니다. 예를 들어, ComboBox를 SqlDataSource 컨트롤, ObjectDataSource 컨트롤, LinqDataSource 또는 EntityDataSource에 바인딩할 수 있습니다.

ComboBox의 영화 목록을 표시 하려고 한다고 가정 합니다. 동영상 데이터베이스 테이블에서 영화 목록을 검색 하려고 합니다. 다음 단계를 수행합니다.

1. 동영상이 .aspx 인 페이지 만들기
2. 도구 상자의 AJAX 확장 탭에 있는 ScriptManager를 페이지에 끌어 오면 ScriptManager 컨트롤을 페이지에 추가 합니다.
3. ComboBox를 페이지로 끌어 ComboBox 컨트롤을 페이지에 추가 합니다.
4. 디자인 뷰에서 ComboBox 컨트롤 위로 마우스를 이동 하 고 **데이터 원본 선택** 작업 옵션을 선택 합니다 (그림 5 참조). 데이터 소스 구성 마법사가 시작 됩니다.
5. **데이터 원본 선택** 단계에서 &lt; 새 데이터 원본 옵션을 선택 &gt; 합니다.
6. **데이터 소스 형식 선택** 단계에서 데이터베이스를 선택 합니다.
7. **데이터 연결 선택** 단계에서 데이터베이스 (예: MoviesDB)를 선택 합니다.
8. **응용 프로그램 구성 파일에 연결 문자열 저장** 단계에서 연결 문자열을 저장 하는 옵션을 선택 합니다.
9. **Select 문 구성** 단계에서 동영상 데이터베이스 테이블을 선택 하 고 모든 열을 선택 합니다.
10. **쿼리 테스트** 단계에서 마침 단추를 클릭 합니다.
11. **데이터 원본 선택** 단계로 돌아가서 표시할 필드의 제목 열을 선택 하 고 데이터 필드에 대 한 Id 열을 선택 합니다 (그림 참조).
12. 확인 단추를 클릭 하 여 마법사를 닫습니다.

[![데이터 원본 선택](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**그림 05**: 데이터 원본 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image10.png))

[![데이터 텍스트 및 값 필드 선택](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**그림 06**: 데이터 텍스트 및 값 필드 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image12.png))

위의 단계를 완료 한 후 ComboBox는 동영상 데이터베이스 테이블의 영화를 나타내는 SqlDataSource 컨트롤에 바인딩됩니다. 페이지의 원본은 목록 2와 같이 표시 됩니다 (약간의 형식 지정을 정리 함).

**목록 2-동영상과 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

ComboBox 컨트롤에는 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성이 있습니다. 브라우저에서 페이지를 열면 데이터베이스의 동영상 목록이 표시 됩니다 (그림 7 참조). 목록에서 영화를 선택 하거나 ComboBox에 영화를 입력 하 여 새 동영상을 입력할 수 있습니다.

[![동영상 목록 표시](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**그림 07**: 동영상 목록 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>DropDownStyle 설정

Combobox DropDownStyle 속성을 사용 하 여 ComboBox의 동작을 변경할 수 있습니다. 이 속성은 가능한 값을 허용 합니다.

- DropDown-(기본값) 콤보 상자에서 화살표를 클릭 하면 드롭다운 목록이 표시 되 고 사용자 지정 값을 입력할 수 있습니다.
- Simple-콤보 상자는 드롭다운 목록을 자동으로 표시 하 고 사용자 지정 값을 입력할 수 있습니다.
- DropDownList-콤보 상자는 DropDownList 컨트롤과 마찬가지로 작동 합니다.

DropDown과 Simple은 항목 목록이 표시 되는 경우와 다릅니다. Simple의 경우 ComboBox로 포커스를 이동할 때 목록이 즉시 표시 됩니다. 드롭다운의 경우 화살표를 클릭 하 여 항목 목록을 확인 해야 합니다.

DropDownList 값을 사용 하면 ComboBox 컨트롤이 표준 DropDownList 컨트롤과 똑같이 작동 합니다. 그러나 여기에는 중요 한 차이점이 있습니다. 이전 버전의 Internet Explorer에서는 무한 z 인덱스를 사용 하 여 DropDownList 컨트롤을 표시 하므로 컨트롤이 앞에 배치 된 컨트롤 앞에 표시 됩니다. ComboBox는 html &lt; &gt; select 태그 대신 html div 태그를 렌더링 하므로 &lt; &gt; combobox는 z 순서를 올바르게 지정 합니다.

## <a name="setting-the-autocompletemode"></a>AutoCompleteMode 설정

ComboBox AutoCompleteMode 속성을 사용 하 여 누군가가 ComboBox에 텍스트를 입력할 때 발생 하는 일을 지정할 수 있습니다. 이 속성은 다음과 같은 가능한 값을 허용 합니다.

- 없음-(기본값) 콤보 상자에서 자동 완성 동작을 제공 하지 않습니다.
- 제안-콤보 상자는 목록을 표시 하 고 목록에서 일치 하는 항목을 강조 표시 합니다 (그림 8 참조).
- 추가-콤보 상자에서 목록을 표시 하지 않고 목록에서 입력 한 항목에 일치 하는 항목을 추가 합니다 (그림 9 참조).
- SuggestAppend-콤보 상자는 목록을 표시 하 고 일치 하는 항목을 목록에서 입력 한 내용에 추가 합니다 (그림 10 참조).

[![ComboBox가 제안 합니다.](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**그림 08**: ComboBox에서 제안 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image16.png))

[![ComboBox가 일치 하는 텍스트를 추가 합니다.](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**그림 09**: ComboBox에 일치 하는 텍스트 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image18.png))

[![ComboBox가 제안 하 고 추가 합니다.](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**그림 10**: ComboBox가 제안 하 고 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image20.png))

## <a name="summary"></a>요약

이 자습서에서는 ComboBox 컨트롤을 사용 하 여 고정 된 항목 집합을 표시 하는 방법을 배웠습니다. 콤보 상자 컨트롤을 정적 항목 집합 및 데이터베이스 테이블에 바인딩합니다. 마지막으로 DropDownStyle 및 AutoCompleteMode 속성을 설정 하 여 ComboBox의 동작을 수정 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](how-do-i-use-the-combobox-control-vb.md)
