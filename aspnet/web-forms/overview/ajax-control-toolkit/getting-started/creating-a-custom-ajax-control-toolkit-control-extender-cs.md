---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 사용자 지정 AJAX 제어 툴킷 제어 익스텐더 만들기(C#) | 마이크로 소프트 문서
author: rick-anderson
description: 사용자 지정 Extenders를 사용하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정하고 확장할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543030"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> 사용자 지정 Extenders를 사용하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정하고 확장할 수 있습니다.

이 자습서에서는 사용자 지정 AJAX 제어 도구 키트 컨트롤 익스텐더를 만드는 방법을 알아봅니다. 텍스트 상자에 텍스트를 입력할 때 단추의 상태를 사용 하지 않는 것에서 활성화로 변경 하는 간단 하지만 유용한 새 extender를 만듭니다. 이 자습서를 읽은 후, 당신은 당신의 자신의 컨트롤 익스텐더와 ASP.NET AJAX 툴킷을 확장 할 수있을 것입니다.

Visual Studio 또는 Visual 웹 개발자를 사용하여 사용자 지정 컨트롤 익스텐더를 만들 수 있습니다(최신 버전의 Visual Web Developer이 있는지 확인).

## <a name="overview-of-the-disabledbutton-extender"></a>사용 안 함 단추 익스텐더의 개요

우리의 새로운 컨트롤 익스텐더는 DisabledButton 익스텐더라는 이름입니다. 이 익스텐더에는 세 가지 속성이 있습니다.

- TargetControlID - 컨트롤이 확장되는 텍스트 상자입니다.
- TargetButtonIID - 비활성화되어 있거나 활성화된 단추입니다.
- 비활성화텍스트 - 처음에 버튼에 표시되는 텍스트입니다. 입력을 시작하면 Button 텍스트 속성의 값이 표시됩니다.

비활성화 단추 확장기를 텍스트 상자 및 단추 컨트롤에 연결합니다. 텍스트를 입력하기 전에 단추를 사용하지 않도록 설정하면 텍스트 상자 와 버튼이 다음과 같습니다.

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

(전체[크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)

텍스트 입력을 시작하면 Button이 활성화되고 텍스트 상자 및 단추는 다음과 같습니다.

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

(전체[크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)

컨트롤 익스텐더를 만들려면 다음 세 개의 파일을 만들어야 합니다.

- DisabledButtonExtender.cs - 이 파일은 익스텐더 만들기를 관리하고 디자인 타임에 속성을 설정할 수 있는 서버 측 제어 클래스입니다. 또한 익스텐더에서 설정할 수 있는 속성을 정의합니다. 이러한 속성은 코드 및 디자인 타임에 액세스할 수 있으며 DisableButtonBehavior.js 파일에 정의된 속성을 일치시입니다.
- DisabledButtonBehavior.js -- 이 파일은 모든 클라이언트 스크립트 논리를 추가하는 곳입니다.
- DisabledButtonDesigner.cs - 이 클래스는 디자인 타임 기능을 가능하게 합니다. 컨트롤 익스텐더가 Visual Studio/Visual 웹 개발자 디자이너에서 올바르게 작동하려면 이 클래스가 필요합니다.

따라서 컨트롤 익스텐더는 서버 측 컨트롤, 클라이언트 측 동작 및 서버 측 디자이너 클래스로 구성됩니다. 다음 섹션에서 이러한 세 파일을 모두 만드는 방법에 대해 알아봅니다.

## <a name="creating-the-custom-extender-website-and-project"></a>사용자 지정 익스텐더 웹 사이트 및 프로젝트 만들기

첫 번째 단계는 Visual Studio/Visual 웹 개발자에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다. 클래스 라이브러리 프로젝트에서 사용자 지정 익스텐더를 만들고 웹 사이트에서 사용자 지정 익스텐더를 테스트합니다.

웹 사이트로 시작해 보겠습니다. 다음 단계에 따라 웹 사이트를 만듭니다.

1. 메뉴 옵션 **파일, 새 웹 사이트를**선택합니다.
2. ASP.NET **웹 사이트** 템플릿을 선택합니다.
3. 새 웹 사이트 웹 *사이트 이름1*.
4. **확인** 단추를 클릭합니다.

다음으로 컨트롤 익스텐더에 대한 코드를 포함하는 클래스 라이브러리 프로젝트를 만들어야 합니다.

1. 메뉴 옵션 **파일, 추가, 새 프로젝트**를 선택합니다.
2. 클래스 **라이브러리** 템플릿을 선택합니다.
3. 사용자 지정 Extenders 라는 이름으로 새 클래스 라이브러리의 이름을 **지정합니다.**
4. **확인** 단추를 클릭합니다.

이 단계를 완료하면 솔루션 탐색기 창이 그림 1과 같아야 합니다.

[![웹 사이트 및 클래스 라이브러리 프로젝트와 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트가 있는 솔루션[(전체 크기 이미지를 보려면 클릭하십시오)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)

다음으로 클래스 라이브러리 프로젝트에 필요한 모든 어셈블리 참조를 추가해야 합니다.

1. 사용자 지정 확장자 프로젝트를 마우스 오른쪽 단추로 클릭하고 **참조 추가**옵션을 선택합니다.
2. .NET 탭을 선택합니다.
3. 다음 어셈블리에 대한 참조를 추가합니다.

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. 시스템.웹.확장.Design.dll
4. 찾아보기 탭을 선택합니다.
5. AjaxControlToolkit.dll 어셈블리에 대한 참조를 추가합니다. 이 어셈블리는 AJAX 제어 도구 키트를 다운로드한 폴더에 있습니다.

이 단계를 완료하면 클래스 라이브러리 프로젝트 참조 폴더가 그림 2와 같아야 합니다.

[![필수 참조가 있는 참조 폴더](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**그림 02**: 필요한 참조가 있는 참조[폴더(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)

## <a name="creating-the-custom-control-extender"></a>사용자 지정 제어 익스텐더 만들기

이제 클래스 라이브러리를 통해 익스텐더 컨트롤을 구축할 수 있습니다. 사용자 지정 익스텐더 컨트롤 클래스의 베어 골격부터 시작하겠습니다(목록 1 참조).

**리스팅 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

목록 1의 컨트롤 익스텐더 클래스에 대해 알 수 있는 몇 가지 사항이 있습니다. 먼저 클래스가 기본 ExtenderControlBase 클래스에서 상속됩니다. 모든 AJAX 제어 툴킷 익스텐더 컨트롤은 이 기본 클래스에서 파생됩니다. 예를 들어 기본 클래스에는 모든 컨트롤 익스텐더의 필수 속성인 TargetID 속성이 포함됩니다.

다음으로 클래스에는 클라이언트 스크립트와 관련된 다음 두 가지 특성이 포함되어 있습니다.

- WebResource - 파일을 어셈블리에 포함된 리소스로 포함시킵니다.
- ClientScriptResource - 스크립트 리소스를 어셈블리에서 검색합니다.

WebResource 특성은 사용자 지정 익스텐더가 컴파일될 때 MyControlBehavior.js 자바스크립트 파일을 어셈블리에 포함하는 데 사용됩니다. ClientScriptResource 특성은 사용자 지정 익스텐더가 웹 페이지에서 사용될 때 어셈블리에서 MyControlBehavior.js 스크립트를 검색하는 데 사용됩니다.

WebResource 및 ClientScriptResource 특성이 작동하려면 JavaScript 파일을 포함된 리소스로 컴파일해야 합니다. 솔루션 탐색기 창에서 파일을 선택하고 속성 시트를 열고 *빌드* **작업** 속성에 포함된 리소스 값을 할당합니다.

컨트롤 익스텐더에는 TargetControlType 특성도 포함되어 있습니다. 이 특성은 컨트롤 익스텐더에서 확장되는 컨트롤 유형을 지정하는 데 사용됩니다. 목록 1의 경우 컨트롤 익스텐더가 TextBox를 확장하는 데 사용됩니다.

마지막으로 사용자 지정 익스텐더에 MyProperty라는 속성이 포함되어 있습니다. 속성은 ExtenderControlProperty 특성으로 표시됩니다. GetPropertyValue() 및 SetPropertyValue() 메서드는 서버 측 컨트롤 익스텐더에서 클라이언트 측 동작으로 속성 값을 전달하는 데 사용됩니다.

의 가서 우리의 DisabledButton 익스텐더에 대한 코드를 구현할 수 있습니다. 이 익스텐더에 대한 코드는 목록 2에서 찾을 수 있습니다.

**리스팅 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

목록 2의 비활성화 된 Button 익스텐더에는 TargetButtonID 및 DisabledText라는 두 개의 속성이 있습니다. TargetButtonID 속성에 적용된 IDReferenceProperty는 Button 컨트롤의 ID 이외의 다른 것을 이 속성에 할당하지 못하게 합니다.

WebResource 및 ClientScriptResource 특성은 이 확장기와 DisabledButtonBehavior.js라는 파일에 있는 클라이언트 측 동작을 연결합니다. 다음 섹션에서이 자바 스크립트 파일에 대해 설명합니다.

## <a name="creating-the-custom-extender-behavior"></a>사용자 지정 확장기 동작 만들기

컨트롤 익스텐더의 클라이언트 쪽 구성 요소를 동작이라고 합니다. 단추를 사용하지 않도록 설정 및 활성화하기 위한 실제 논리는 DisabledButton 동작에 포함되어 있습니다. 동작에 대한 자바스크립트 코드는 목록 3에 포함되어 있습니다.

**목록 3 - 비활성화된 Button.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

목록 3의 자바 스크립트 파일에는 비활성화 된 ButtonBehavior라는 클라이언트 측 클래스가 포함되어 있습니다. 이 클래스는 서버 측 트윈과 마찬가지로 TargetButtonID 및 DisabledText라는 두\_개의 속성을 포함하며 TargetButtonID/set TargetButtonID를\_얻고 DisabledText/set DisabledText를\_\_사용하여 액세스할 수 있습니다.

initialize() 메서드는 키업 이벤트 처리기를 동작에 대한 대상 요소와 연결합니다. 이 동작과 연결된 TextBox에 문자를 입력할 때마다 키업 처리기가 실행됩니다. 키업 처리기는 동작과 연결된 TextBox에 텍스트가 포함되어 있는지 여부에 따라 Button을 활성화하거나 사용하지 않도록 설정합니다.

리스팅 3에서 자바스크립트 파일을 포함된 리소스로 컴파일해야 합니다. 솔루션 탐색기 창에서 파일을 선택하고 속성 시트를 열고 *빌드* **작업** 속성에 포함된 리소스 값을 할당합니다(그림 3 참조). 이 옵션은 비주얼 스튜디오와 비주얼 웹 개발자 모두에서 사용할 수 있습니다.

[![포함된 리소스로 JavaScript 파일 추가](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**그림 03**: 자바스크립트 파일을 임베디드 리소스로 추가[(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)

## <a name="creating-the-custom-extender-designer"></a>사용자 지정 익스텐더 디자이너 만들기

Extender를 완료하기 위해 만들어야 하는 마지막 클래스가 하나 있습니다. 목록 4에서 디자이너 클래스를 만들어야 합니다. 이 클래스는 확장자가 Visual Studio/Visual 웹 개발자 디자이너와 올바르게 행동하도록 하는 데 필요합니다.

**리스팅 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

목록 4의 디자이너를 디자이너 특성과 DisabledButton 익스텐더와 연결합니다. 다음과 같이 디자이너 특성을 DisabledButtonExtender 클래스에 적용해야 합니다.

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>사용자 지정 익스텐더 사용

이제 비활성화 버튼 컨트롤 익스텐더 만들기를 마쳤으니 ASP.NET 웹 사이트에서 사용할 시간입니다. 먼저 도구 상자에 사용자 지정 익스텐더를 추가해야 합니다. 다음 단계를 수행하세요.

1. 솔루션 탐색기 창에서 페이지를 두 번 클릭하여 ASP.NET 페이지를 엽니다.
2. 도구 상자를 마우스 오른쪽 단추로 클릭하고 메뉴 선택 옵션 **항목 선택.**
3. 도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리를 찾아봅습니다.
4. **확인** 버튼을 클릭하여 대화 상자를 닫습니다.

이 단계를 완료하면 비활성화 단추 컨트롤 익스텐더가 도구 상자에 나타납니다(그림 4 참조).

[![도구 상자의 비활성화 단추](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**그림 04**: 도구 상자의 비활성화 버튼[(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)

다음으로 새 ASP.NET 페이지를 만들어야 합니다. 다음 단계를 수행하세요.

1. ShowDisabledButton.aspx라는 새 ASP.NET 페이지를 만듭니다.
2. 스크립트 관리자를 페이지로 드래그합니다.
3. 텍스트 상자 컨트롤을 페이지로 끕습니다.
4. 단추 컨트롤을 페이지로 끕습니다.
5. 속성 창에서 Button ID 속성을 <em>btnSave</em> 값으로 변경하고 Text 속성을 *\*Save*값으로 변경합니다.

우리는 표준 ASP.NET 텍스트 상자와 버튼 컨트롤과 페이지를 만들었습니다.

다음으로, 비활성화 된 단추 확장기를 사용 하 고 TextBox 컨트롤을 확장 해야 합니다.

1. Extender 마법사 대화 상자를 열려면 **확장작업 추가** 옵션을 선택합니다(그림 5 참조). 대화 상자에는 사용자 지정 비활성화단추 익스텐더가 포함되어 있습니다.
2. 비활성화 단추 익스텐더를 선택하고 **확인** 단추를 클릭합니다.

[![익스텐더 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**그림 05**: 확장기 마법사 대화 상자[(클릭하여 전체 크기 이미지 보기)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)

마지막으로 DisabledButton 익스텐더의 속성을 설정할 수 있습니다. TextBox 컨트롤의 속성을 수정하여 DisabledButton 익스텐더의 속성을 수정할 수 있습니다.

1. 디자이너에서 텍스트 상자를 선택합니다.
2. 속성 창에서 Extenders 노드를 확장합니다(그림 6 참조).
3. DisabledText 속성에 *저장* 값 과 *값 btnSave* TargetButtonID 속성에 할당 합니다.

[![익스텐더 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**그림 06**: 확장 속성[설정(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)

페이지를 실행하면(F5를 누르면) 단추 컨트롤이 처음에 비활성화됩니다. 텍스트 상자에 텍스트를 입력하기 시작하면 단추 컨트롤이 활성화됩니다(그림 7 참조).

[![비활성화된 단추 익스텐더가 실행 중](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**그림 07**: 비활성화 단추 익스텐더 가 작동하는[경우(클릭하여 전체 크기 이미지 보기)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)

## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 익스텐더 컨트롤을 사용하여 AJAX 제어 도구 키트를 확장하는 방법을 설명하는 것이었습니다. 이 자습서에서는 간단한 DisabledButton 컨트롤 익스텐더를 만들었습니다. 비활성화된 Button Extender 클래스, DisabledButtonBehavior 자바 스크립트 동작 및 DisabledButtonDesigner 클래스를 만들어이 확장기를 구현 했습니다. 사용자 지정 컨트롤 extender를 만들 때마다 비슷한 단계 집합을 따릅니다.

> [!div class="step-by-step"]
> [이전](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [다음](get-started-with-the-ajax-control-toolkit-vb.md)
