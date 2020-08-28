---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: 사용자 지정 Extender를 사용 하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정 하 고 확장할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: ec1272da59e351679dd0e8761f12af84fcf09a75
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045249"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기(VB)

[Microsoft](https://github.com/microsoft) 에서

> 사용자 지정 Extender를 사용 하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정 하 고 확장할 수 있습니다.

이 자습서에서는 사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 extender를 만드는 방법에 대해 알아봅니다. 텍스트 상자에 텍스트를 입력 하는 경우 단추의 상태를 사용 안 함에서 사용으로 변경 하는 간단 하 고 유용한 새 extender를 만듭니다. 이 자습서를 읽은 후에는 사용자 고유의 컨트롤 extender로 ASP.NET AJAX Toolkit를 확장할 수 있습니다.

Visual Studio 또는 Visual Web Developer를 사용 하 여 사용자 지정 컨트롤 extender를 만들 수 있습니다 (최신 버전의 Visual Web Developer가 있는지 확인).

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton Extender의 개요

새 컨트롤 extender의 이름은 DisabledButton extender로 지정 됩니다. 이 extender에는 다음과 같은 세 가지 속성이 있습니다.

- TargetControlID-컨트롤이 확장 하는 텍스트 상자입니다.
- TargetButtonIID-사용 하지 않거나 사용 하도록 설정 된 단추입니다.
- DisabledText-처음에 단추에 표시 되는 텍스트입니다. 입력을 시작 하면 단추 텍스트 속성의 값이 표시 됩니다.

DisabledButton extender를 TextBox 및 Button 컨트롤에 후크 합니다. 텍스트를 입력 하기 전에 단추가 비활성화 되 고 텍스트 상자와 단추가 다음과 같이 표시 됩니다.

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))

텍스트 입력을 시작한 후 단추가 활성화 되 고 텍스트 상자와 단추가 다음과 같이 표시 됩니다.

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))

컨트롤 extender를 만들려면 다음 세 개의 파일을 만들어야 합니다.

- DisabledButtonExtender-이 파일은 extender 만들기를 관리 하 고 디자인 타임에 속성을 설정 하는 데 사용할 수 있는 서버측 컨트롤 클래스입니다. 또한 extender에서 설정할 수 있는 속성을 정의 합니다. 이러한 속성은 코드와 디자인 타임에 액세스할 수 있으며 DisableButtonBehavior.js 파일에 정의 된 속성과 일치 합니다.
- DisabledButtonBehavior.js--이 파일을 통해 모든 클라이언트 스크립트 논리를 추가할 수 있습니다.
- DisabledButtonDesigner-이 클래스는 디자인 타임 기능을 사용 하도록 설정 합니다. Visual Studio/Visual Web Developer Designer에서 컨트롤 extender가 제대로 작동 하도록 하려면이 클래스가 필요 합니다.

따라서 컨트롤 extender는 서버측 컨트롤, 클라이언트 쪽 동작 및 서버 쪽 디자이너 클래스로 구성 됩니다. 다음 섹션에서 이러한 세 파일을 모두 만드는 방법을 알아봅니다.

## <a name="creating-the-custom-extender-website-and-project"></a>사용자 지정 Extender 웹 사이트 및 프로젝트 만들기

첫 번째 단계는 Visual Studio/Visual Web Developer에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다. 클래스 라이브러리 프로젝트에서 사용자 지정 extender를 만들고 웹 사이트에서 사용자 지정 extender를 테스트 합니다.

웹 사이트부터 시작 해 보겠습니다. 웹 사이트를 만들려면 다음 단계를 따르세요.

1. 메뉴 옵션 **파일, 새 웹 사이트를**선택 합니다.
2. **ASP.NET 웹 사이트** 템플릿을 선택 합니다.
3. 새 웹 사이트의 이름을 *Website1*로 합니다.
4. **확인** 단추를 클릭합니다.

다음으로, 컨트롤 extender에 대 한 코드를 포함 하는 클래스 라이브러리 프로젝트를 만들어야 합니다.

1. 메뉴 옵션 **파일, 추가, 새 프로젝트**를 선택 합니다.
2. **클래스 라이브러리** 템플릿을 선택 합니다.
3. 이름이 **Customextenders**인 새 클래스 라이브러리의 이름을로 바꿉니다.
4. **확인** 단추를 클릭합니다.

이러한 단계를 완료 한 후 솔루션 탐색기 창은 그림 1과 같습니다.

[![웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하는 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하는 솔루션 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))

다음으로 클래스 라이브러리 프로젝트에 필요한 모든 어셈블리 참조를 추가 해야 합니다.

1. CustomExtenders 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **참조 추가**를 선택 합니다.
2. .NET 탭을 선택합니다.
3. 다음 어셈블리에 대한 참조를 추가합니다.

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. 찾아보기 탭을 선택합니다.
5. AjaxControlToolkit.dll 어셈블리에 대 한 참조를 추가 합니다. 이 어셈블리는 AJAX 컨트롤 도구 키트를 다운로드 한 폴더에 있습니다.

프로젝트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 다음 참조 탭을 클릭 하 여 모든 오른쪽 참조를 추가 했는지 확인할 수 있습니다 (그림 2 참조).

[![필요한 참조가 있는 폴더 참조](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**그림 02**: 필요한 참조가 있는 폴더 참조 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>사용자 지정 컨트롤 Extender 만들기

이제 클래스 라이브러리를 만들었으므로 extender 컨트롤 빌드를 시작할 수 있습니다. 사용자 지정 extender 컨트롤 클래스의 완전 한 뼈부터 살펴보겠습니다 (목록 1 참조).

**목록 1-MyCustomExtender .vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

목록 1에서 컨트롤 extender 클래스에 대 한 몇 가지 사항을 확인 해야 합니다. 먼저 클래스가 기본 ExtenderControlBase 클래스에서 상속 되는지 확인 합니다. 모든 AJAX Control Toolkit extender 컨트롤은이 기본 클래스에서 파생 됩니다. 예를 들어 기본 클래스는 모든 컨트롤 extender의 필수 속성인 TargetID 속성을 포함 합니다.

다음으로 클래스에는 클라이언트 스크립트와 관련 된 다음 두 가지 특성이 포함 되어 있습니다.

- Webresource.axd-파일이 어셈블리에 포함 리소스로 포함 되도록 합니다.
- ClientScriptResource-어셈블리에서 스크립트 리소스를 검색 합니다.

Webresource.axd 특성은 사용자 지정 extender가 컴파일될 때 어셈블리에 MyControlBehavior.js JavaScript 파일을 포함 하는 데 사용 됩니다. ClientScriptResource 특성은 웹 페이지에서 사용자 지정 extender를 사용할 때 어셈블리에서 MyControlBehavior.js 스크립트를 검색 하는 데 사용 됩니다.

Webresource.axd 및 ClientScriptResource 특성이 작동 하려면 JavaScript 파일을 포함 리소스로 컴파일해야 합니다. 솔루션 탐색기 창에서 파일을 선택 하 고 속성 시트를 연 후에 *포함 된 리소스* 값을 **빌드 작업** 속성에 할당 합니다.

컨트롤 extender에는 TargetControlType 특성도 포함 되어 있습니다. 이 특성은 컨트롤 extender에 의해 확장 되는 컨트롤의 형식을 지정 하는 데 사용 됩니다. 목록 1의 경우 컨트롤 extender를 사용 하 여 텍스트 상자를 확장 합니다.

마지막으로, 사용자 지정 extender에 이름이 T.myproperty 인 속성이 포함 되어 있는지 확인 합니다. 속성은 ExtenderControlProperty 특성으로 표시 됩니다. GetPropertyValue () 및 SetPropertyValue () 메서드는 서버측 컨트롤 extender의 속성 값을 클라이언트 쪽 동작으로 전달 하는 데 사용 됩니다.

계속 해 서 DisabledButton extender에 대 한 코드를 구현 해 보겠습니다. 이 extender에 대 한 코드는 목록 2에서 찾을 수 있습니다.

**목록 2-DisabledButtonExtender**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

목록 2의 DisabledButton extender에는 TargetButtonID 및 DisabledText 라는 두 개의 속성이 있습니다. TargetButtonID 속성에 적용 된 IDReferenceProperty는 단추 컨트롤의 ID 이외의 항목을이 속성에 할당 하는 것을 방지 합니다.

Webresource.axd 및 ClientScriptResource 특성은 DisabledButtonBehavior.js 라는 파일에 있는 클라이언트측 동작을이 extender와 연결 합니다. 이 JavaScript 파일에 대해서는 다음 섹션에서 설명 합니다.

## <a name="creating-the-custom-extender-behavior"></a>사용자 지정 Extender 동작 만들기

컨트롤 extender의 클라이언트 쪽 구성 요소를 동작 이라고 합니다. 단추를 사용 하지 않도록 설정 하 고 설정 하는 실제 논리는 DisabledButton 동작에 포함 됩니다. 동작에 대 한 JavaScript 코드는 목록 3에 포함 되어 있습니다.

**목록 3-DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

목록 3의 JavaScript 파일에는 이름이 DisabledButtonBehavior 인 클라이언트 쪽 클래스가 있습니다. TargetButtonID 및 DisabledText 라는 두 개의 속성을 포함 하는이 클래스에는 get TargetButtonID/set TargetButtonID를 사용 하 여 액세스할 수 있으며 \_ \_ get \_ DisabledText/set DisabledText \_ 를 사용 하 여 액세스할 수 있습니다.

Initialize () 메서드는 keyup 이벤트 처리기를 동작의 대상 요소와 연결 합니다. 이 동작과 연결 된 텍스트 상자에 문자를 입력할 때마다 keyup 처리기가 실행 됩니다. Keyup 처리기는 동작과 연결 된 텍스트 상자에 텍스트가 포함 되어 있는지 여부에 따라 단추를 사용 하거나 사용 하지 않도록 설정 합니다.

목록 3에서 JavaScript 파일을 포함 리소스로 컴파일해야 합니다. 솔루션 탐색기 창에서 파일을 선택 하 고 속성 시트를 연 후에 *포함 된 리소스* 값을 **빌드 작업** 속성에 할당 합니다 (그림 3 참조). 이 옵션은 Visual Studio 및 Visual Web Developer에서 사용할 수 있습니다.

[![JavaScript 파일을 포함 리소스로 추가](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**그림 03**: JavaScript 파일을 포함 리소스로 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>사용자 지정 Extender 디자이너 만들기

Extender를 완료 하기 위해 만들어야 하는 마지막 클래스가 하나 있습니다. 목록 4에서 designer 클래스를 만들어야 합니다. 이 클래스는 Visual Studio/Visual Web Developer Designer에서 extender가 제대로 작동 하도록 하는 데 필요 합니다.

**목록 4-DisabledButtonDesigner**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

목록 4의 디자이너를 Designer 특성을 사용 하 여 DisabledButton extender와 연결 합니다. 다음과 같이 Designer 특성을 DisabledButtonExtender 클래스에 적용 해야 합니다.

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>사용자 지정 Extender 사용

이제 DisabledButton 컨트롤 extender 만들기를 완료 했으므로 ASP.NET 웹 사이트에서 사용할 수 있습니다. 먼저 도구 상자에 사용자 지정 extender를 추가 해야 합니다. 다음 단계를 수행합니다.

1. 솔루션 탐색기 창에서 페이지를 두 번 클릭 하 여 ASP.NET 페이지를 엽니다.
2. 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **항목 선택**을 선택 합니다.
3. 도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리로 이동 합니다.
4. **확인** 단추를 클릭 하 여 대화 상자를 닫습니다.

이러한 단계를 완료 한 후에는 DisabledButton 컨트롤 extender가 도구 상자에 표시 됩니다 (그림 4 참조).

[![도구 상자의 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**그림 04**: 도구 상자에 DisabledButton ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))

다음으로 새 ASP.NET 페이지를 만들어야 합니다. 다음 단계를 수행합니다.

1. ShowDisabledButton 라는 새 ASP.NET 페이지를 만듭니다.
2. ScriptManager를 페이지로 끌어옵니다.
3. TextBox 컨트롤을 페이지로 끌어 옵니다.
4. 단추 컨트롤을 페이지로 끌어 옵니다.
5. 속성 창에서 단추 ID 속성을 <em>btnSave</em> 값으로 변경 하 고 Text 속성을 *Save \* *값으로 변경 합니다.

표준 ASP.NET 텍스트 상자 및 단추 컨트롤을 사용 하 여 페이지를 만들었습니다.

다음으로, DisabledButton extender를 사용 하 여 TextBox 컨트롤을 확장 해야 합니다.

1. Extender 작업 **추가** 옵션을 선택 하 여 extender 마법사 대화 상자를 엽니다 (그림 5 참조). 대화 상자에 사용자 지정 DisabledButton extender가 포함 되어 있는지 확인 합니다.
2. DisabledButton extender를 선택 하 고 **확인** 단추를 클릭 합니다.

[![Extender 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**그림 05**: Extender 마법사 대화 상자 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))

마지막으로 DisabledButton extender의 속성을 설정할 수 있습니다. TextBox 컨트롤의 속성을 수정 하 여 DisabledButton extender의 속성을 수정할 수 있습니다.

1. 디자이너에서 텍스트 상자를 선택 합니다.
2. 속성 창에서 Extender 노드를 확장 합니다 (그림 6 참조).
3. DisabledText 속성에 *Save* 값을 할당 하 고 TargetButtonID 속성에 *btnSave* 값을 할당 합니다.

[![Extender 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**그림 06**: extender 속성 설정 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))

F5 키를 눌러 페이지를 실행 하면 단추 컨트롤이 처음에 비활성화 됩니다. 텍스트 상자에 텍스트를 입력 하는 즉시 단추 컨트롤이 사용 됩니다 (그림 7 참조).

[![DisabledButton extender의 동작](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**그림 07**: 실행 중인 DisabledButton extender ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))

## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 extender 컨트롤을 사용 하 여 AJAX 컨트롤 도구 키트를 확장 하는 방법을 설명 하는 것입니다. 이 자습서에서는 간단한 DisabledButton 컨트롤 extender를 만들었습니다. DisabledButtonExtender 클래스, DisabledButtonBehavior JavaScript 동작 및 DisabledButtonDesigner 클래스를 만들어이 extender를 구현 했습니다. 사용자 지정 컨트롤 extender를 만들 때마다 비슷한 단계 집합을 따릅니다.

> [!div class="step-by-step"]
> [이전](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
