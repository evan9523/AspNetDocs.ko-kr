---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 콤보박스 컨트롤은 어떻게 사용하나요? (C#) | 마이크로 소프트 문서
author: rick-anderson
description: 콤보박스는 사용자가 선택할 수 있는 옵션 목록과 텍스트 상자의 유연성을 결합한 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543807"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>콤보박스 컨트롤은 어떻게 사용하나요? (C#)

[로 마이크로 소프트](https://github.com/microsoft)

> 콤보박스는 사용자가 선택할 수 있는 옵션 목록과 텍스트 상자의 유연성을 결합한 ASP.NET AJAX 컨트롤입니다.

이 자습서의 목표는 AJAX 제어 툴킷 콤보박스 컨트롤을 설명하는 것입니다. 콤보박스는 표준 ASP.NET 드롭다운리스트 컨트롤과 텍스트 박스 컨트롤 사이의 조합처럼 작동합니다. 기존 항목 목록에서 선택하거나 새 항목을 입력할 수 있습니다.

ComboBox는 자동 완성 컨트롤 익스텐더와 유사하지만 컨트롤은 다른 시나리오에서 사용됩니다. 자동 완성 익스텐더는 웹 서비스를 쿼리하여 일치하는 항목을 가져옵니다. 반면 콤보박스 컨트롤은 항목 집합으로 초기화됩니다. ComboBox 컨트롤을 사용하는 동안 대량의 데이터 세트(수백만 대의 자동차 부품)로 작업하는 동안 AutoComplete 익스텐더를 사용하면 작은 데이터 집합(수십 개의 자동차 부품)으로 작업하는 것이 합리적입니다.

## <a name="selecting-from-a-static-list-of-items"></a>항목의 정적 목록에서 선택

의 콤보 박스 컨트롤을 사용하는 간단한 샘플로 시작하자. 드롭다운 목록에 항목의 정적 목록을 표시하려고 한다고 가정합니다. 그러나 목록이 완료되지 않았을 가능성을 열어 두려고 합니다. 사용자가 목록에 사용자 지정 값을 입력하도록 허용하려고 합니다.

새 ASP.NET 웹 폼 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다. 새 ASP.NET 페이지를 프로젝트에 추가하고 디자인 보기로 전환합니다.

페이지에서 ComboBox 컨트롤을 사용하려면 페이지에 ScriptManager 컨트롤을 추가해야 합니다. AJAX 확장 탭 아래에서 디자이너 표면으로 ScriptManager 컨트롤을 끕니까. 페이지 맨 위에 ScriptManager 컨트롤을 추가해야 합니다. 서버 측 &lt;양식&gt; 태그 열기 바로 아래에 추가할 수 있습니다.

다음으로, ComboBox 컨트롤을 페이지로 드래그합니다. 다른 AJAX 제어 툴킷 컨트롤 및 컨트롤 익스텐더와 함께 도구 상자에서 콤보박스 컨트롤을 찾을 수 있습니다(그림 1 참조).

[![명함을 만들기 위한 간단한 양식](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**그림 01**: 도구 상자에서 콤보박스 컨트롤 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image2.png)

콤보박스 컨트롤을 사용하여 정적 선택 목록을 표시합니다. 사용자는 순, 중간 및 핫의 세 가지 선택 목록에서 음식에 대한 특정 수준의 매운 맛을 선택할 수 있습니다(그림 2 참조).

[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**그림 02**: 항목의 정적 목록에서 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image4.png)

ComboBox 컨트롤에 이러한 옵션을 추가할 수 있는 방법에는 두 가지가 있습니다. 먼저 디자인 보기에서 컨트롤 위에 마우스를 가져가면 옵션 편집 작업 옵션을 선택하고 항목 편집기(그림 3 참조)를 엽니다.

[![콤보박스 항목 편집](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**그림 03**: 콤보박스 항목 편집[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-combobox-control-cs/_static/image6.png)

두 번째 옵션은 소스 보기에서 열기와 닫기 &lt;asp:ComboBox&gt; 태그 사이에 항목 목록을 추가하는 것입니다. 목록 1의 페이지에는 항목 목록이 있는 업데이트된 ComboBox가 포함되어 있습니다.

**목록 1 - 정적.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

리스팅 1에서 페이지를 열면 ComboBox에서 기존 옵션 중 하나를 선택할 수 있습니다. 즉, 콤보박스는 드롭다운리스트 컨트롤처럼 작동합니다.

그러나 기존 목록에 없는 새 선택(예: Super Spicy)을 입력할 수도 있습니다. 그래서, 콤보 박스는 텍스트 상자 컨트롤처럼 작동합니다.

기존 항목을 선택하든 사용자 지정 항목을 입력하든 양식을 제출할 때 선택 항목이 레이블 컨트롤에 나타납니다. 양식을 제출하면 btnSubmit\_Click 처리기가 레이블을 실행하고 업데이트합니다(그림 4 참조).

[![선택한 항목 표시](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**그림 04**: 선택한 항목 표시[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image8.png)

ComboBox는 양식을 제출한 후 선택한 항목을 검색하기 위한 DropDownList 컨트롤과 동일한 속성을 지원합니다.

- SelectedItem.Text - 선택한 항목의 텍스트 속성 값을 표시합니다.
- SelectedItem.Value - 선택한 항목의 Value 속성 값을 표시하거나 콤보박스에 입력된 텍스트를 표시합니다.
- Selected값 - 선택된 Item.Value와 동일합니다.이 속성을 사용하면 선택한 기본(초기) 항목을 지정할 수 있습니다.

ComboBox에 사용자 지정 선택을 입력하면 사용자 지정 선택이 SelectedItem.Text 및 SelectedItem.Value 속성 모두에 할당됩니다.

## <a name="selecting-the-list-of-items-from-the-database"></a>데이터베이스에서 항목 목록 선택

데이터베이스에서 ComboBox가 표시하는 항목 목록을 검색할 수 있습니다. 예를 들어 ComboBox를 SqlDataSource 컨트롤, 개체 데이터 소스 컨트롤, LinqDataSource 또는 EntityDataSource에 바인딩할 수 있습니다.

콤보박스에 영화 목록을 표시한다고 가정해 보십니까? Movies 데이터베이스 테이블에서 동영상 목록을 검색하려고 합니다. 다음 단계를 수행하세요.

1. Movies.aspx라는 페이지 만들기
2. 도구 상자의 AJAX 확장 탭 아래에서 스크립트 관리자를 페이지로 드래그하여 페이지에 ScriptManager 컨트롤을 추가합니다.
3. ComboBox를 페이지에 드래그하여 페이지에 콤보박스 컨트롤을 추가합니다.
4. 디자인 보기에서 ComboBox 컨트롤 위로 마우스를 마우스로 가리키고 **데이터 원본** 작업 선택 옵션을 선택합니다(그림 5 참조). 데이터 원본 구성 마법사가 시작됩니다.
5. 데이터 **원본 선택** 단계에서 &lt;새 데이터 원본&gt; 옵션을 선택합니다.
6. 데이터 **원본 유형 선택** 단계에서 데이터베이스를 선택합니다.
7. 데이터 연결 선택 단계에서 데이터베이스(예: MoviesDB.mdf)를 **선택합니다.**
8. 응용 **프로그램 구성 파일** 파일에 연결 문자열 저장 단계에서 연결 문자열을 저장하는 옵션을 선택합니다.
9. **명령문 선택** 구성 단계에서 Movies 데이터베이스 테이블을 선택하고 모든 열을 선택합니다.
10. 테스트 **쿼리** 단계에서 완료 단추를 클릭합니다.
11. **데이터 원본 선택** 단계에서 표시할 필드의 제목 열과 데이터 필드의 ID 열을 선택합니다(그림 참조).
12. 확인 버튼을 클릭하여 마법사를 닫습니다.

[![데이터 원본 선택](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**그림 05**: 데이터 원본 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image10.png)

[![데이터 텍스트 및 값 필드 선택](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**그림 06**: 데이터 텍스트 및 값 필드 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image12.png)

위의 단계를 완료하면 ComboBox는 Movies 데이터베이스 테이블의 동영상을 나타내는 SqlDataSource 컨트롤에 바인딩됩니다. 페이지의 소스는 목록 2처럼 보입니다 (서식을 약간 정리했습니다).

**리스팅 2 - 영화.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

콤보박스 컨트롤에는 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성이 있습니다. 브라우저에서 페이지를 열면 데이터베이스의 동영상 목록이 표시됩니다(그림 7 참조). 목록에서 영화를 선택하거나 ComboBox에 영화를 입력하여 새 영화를 입력할 수 있습니다.

[![영화 목록 표시](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**그림 07**: 동영상 목록[표시(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image14.png)

## <a name="setting-the-dropdownstyle"></a>드롭다운 스타일 설정

콤보박스 드롭다운스타일 속성을 사용하여 콤보박스의 동작을 변경할 수 있습니다. 이 속성은 가능한 값을 허용합니다.

- 드롭다운 - (기본값) 화살표를 클릭하면 ComboBox에 드롭다운 목록이 표시되고 사용자 지정 값을 입력할 수 있습니다.
- 단순 - 콤보박스는 드롭다운 목록을 자동으로 표시하며 사용자 지정 값을 입력할 수 있습니다.
- 드롭다운목록 - 콤보박스는 드롭다운리스트 컨트롤처럼 작동합니다.

드롭다운과 단순의 차이점은 항목 목록이 표시되는 경우입니다. 단순의 경우 포커스를 콤보박스로 이동할 때 목록이 즉시 표시됩니다. 드롭다운의 경우 화살표를 클릭하여 항목 목록을 확인합니다.

드롭다운목록 값을 사용하면 ComboBox 컨트롤이 표준 드롭다운리스트 컨트롤처럼 작동합니다. 그러나 여기에는 중요한 차이점이 있습니다. 이전 버전의 Internet Explorer에는 무한 z 인덱스가 있는 DropDownList 컨트롤이 표시되므로 컨트롤이 앞에 배치된 컨트롤 앞에 표시됩니다. &lt;콤보박스는 HTML 선택&gt; &lt;&gt; 태그 대신 HTML div 태그를 렌더링하므로 ComboBox는 z 순서를 올바르게 준수합니다.

## <a name="setting-the-autocompletemode"></a>자동 컴컴 모드 설정

ComboBox 자동 완료 모드 속성을 사용 하 여 다른 사용자가 ComboBox에 텍스트를 입력 할 때 발생 하는 방법을 지정 합니다. 이 속성은 다음과 같은 가능한 값을 허용합니다.

- 없음 - (기본값) ComboBox는 자동 완성 동작을 제공하지 않습니다.
- 제안 - ComboBox는 목록을 표시하고 목록에서 일치하는 항목을 강조 표시합니다(그림 8 참조).
- 추가 - ComboBox는 목록을 표시하지 않으며 목록에서 입력한 항목에 일치하는 항목을 추가합니다(그림 9 참조).
- 제안 앱- ComboBox는 모두 목록을 표시하고 목록에서 일치하는 항목을 입력한 항목으로 추가합니다(그림 10 참조).

[![콤보 박스는 제안을합니다](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**그림 08**: 콤보박스가 제안을[합니다(전체 크기 이미지를 보려면 클릭하세요)](how-do-i-use-the-combobox-control-cs/_static/image16.png)

[![콤보 박스는 일치하는 텍스트를 부속](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**그림 09**: ComboBox는 일치하는 텍스트를 추가했다[(클릭을 클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-combobox-control-cs/_static/image18.png)

[![콤보 박스 제안 하 고 부속](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**그림 10**: 콤보박스가 제안하고 부속[(클릭하여 전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-cs/_static/image20.png)

## <a name="summary"></a>요약

이 자습서에서는 ComboBox 컨트롤을 사용하여 고정된 항목 집합을 표시하는 방법을 배웠습니다. ComboBox 컨트롤을 정적 항목 집합과 데이터베이스 테이블에 바인딩합니다. 마지막으로 드롭다운 스타일 및 자동 컴컴 모드 속성을 설정하여 콤보박스의 동작을 수정하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](how-do-i-use-the-combobox-control-vb.md)
