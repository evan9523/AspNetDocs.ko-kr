---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 비주얼 스튜디오를 사용하여 웹 페이지(Razor)ASP.NET 프로그래밍 | 마이크로 소프트 문서
author: Rick-Anderson
description: 이 부록에서는 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용하여 ASP.NET 웹 페이지를 Razor 구문으로 프로그래밍하는 방법을 설명합니다.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542900"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>비주얼 스튜디오를 사용하여 웹 페이지(Razor)ASP.NET 프로그래밍

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Visual Studio 또는 Visual Web Developer Express를 사용하여 ASP.NET 웹 페이지(Razor) 웹 사이트를 프로그래밍하는 방법을 설명합니다.
>
> 학습할 내용
>
> - Visual Studio 버전의 ASP.NET 웹 페이지로 작업하려면 설치해야 하는 사항(있는 경우).
> - 비주얼 웹 개발자 2010 익스프레스에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법.
> - IntelliSense 및 디버거를 포함하여 ASP.NET Razor 페이지와 함께 작업하는 비주얼 스튜디오에서 기능을 사용하는 방법.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>튜토리얼에 사용되는 소프트웨어 버전
>
>
> - ASP.NET 웹 페이지 (면도기) 3
> - Visual Studio 2013
> - 웹 매트릭스 3
>
>
> 이 자습서에서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2에서도 작동합니다.

WebMatrix 또는 다른 많은 코드 편집기에서 Razor 구문으로 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다. 또한 웹 사이트뿐만 아니라 다양한 유형의 응용 프로그램을 만들기 위한 강력한 도구 집합을 제공하는 IDE(모든 기능을 갖춘 통합 개발 환경)인 Microsoft Visual Studio를 사용할 수도 있습니다. ASP.NET Razor 페이지로 작업하려면 [Visual Studio 2017을](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)사용할 수 있습니다.

Visual Studio에서 Razor 웹 페이지를 ASP.NET 프로그래밍에 제공하는 두 가지 유용한 기능은 다음과 같습니다.

- *인텔리센스*. 비주얼 스튜디오에 내장 된 IntelliSense 기능은 웹 매트릭스에서 IntelliSense보다 더 포괄적이다.
- *디버거*. 디버거를 사용하면 프로그램을 실행하는 동안 중지하고, 변수를 검사하고, 코드 줄을 한 줄씩 단계별로 단계별로 실행하여 코드 문제를 해결할 수 있습니다.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>ASP.NET 웹 페이지의 다른 버전과 함께 Visual Studio 사용

Visual Studio 2017에서 ASP.NET 웹 앱을 개발하려면 **ASP.NET 및 웹 개발** 워크로드를 설치합니다.

Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대한 지원이 포함되어 있습니다. (ASP.NET 웹 페이지를 지원하기 위해 필요한 패키지는 Visual Studio를 설치할 때 설치됩니다.)

Visual Studio 2010에는 ASP.NET 웹 페이지에 대한 지원이 기본적으로 포함되지 않습니다. Visual Studio 2010에서 ASP.NET 웹 페이지를 사용하려면 ASP.NET MVC 패키지를 설치해야 합니다. 웹 페이지 2를 ASP.NET 위해 MVC 4를 ASP.NET 설치합니다.

다음 표에는 여러 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대한 지원이 요약되어 있습니다.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 웹 페이지 2** | MVC 4에 ASP.NET 설치 | (포함) | (포함) |
| **ASP.NET 웹 페이지 3** |  | NuGet을 통해 ASP.NET 웹 페이지 3으로 업데이트 | (포함) |

Visual Studio 2010에서 작업하려면 [Visual Studio 2010의 ASP.NET 웹 페이지에 대한 지원 설치를](#vs2010support)참조하십시오.

## <a name="launching-visual-studio-from-webmatrix"></a>웹매트릭스에서 비주얼 스튜디오 시작

WebMatrix에서 프로젝트를 시작하고 Visual Studio로 전환하려는 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 열 수 있는 단추를 제공합니다. 이 단추를 사용하려면 컴퓨터에 Visual Studio가 설치되어 있어야 합니다. 다음 이미지는 WebMatrix의 단추를 보여 주며,

![비주얼 스튜디오 시작](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

단추를 클릭하면 프로젝트가 Visual Studio에서 열립니다. WebMatrix와 Visual Studio 간에 아무런 문제 없이 앞뒤로 전환할 수 있습니다. 다른 환경에서 파일이 변경되었으며 최신 변경 내용을 얻으려면 다시 로드해야 하는 경우 알림을 받게 됩니다.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>비주얼 스튜디오에서 ASP.NET 면도기 사이트 만들기

Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면 다음 단계를 수행하십시오.

1. Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 웹 사이트를**클릭합니다.

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 새 **웹 사이트** 대화 상자에서 사용할 언어(Visual C# 또는 Visual Basic)를 선택합니다.
4. ASP.NET **웹 사이트(Razor)** 템플릿을 선택합니다.

    ![면도기 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **확인**을 클릭합니다.

새 프로젝트가 존재하며 시작하는 데 도움이 되는 몇 가지 기본 웹 페이지가 채워집니다.

### <a name="using-intellisense"></a>IntelliSense 사용

이제 사이트를 만들었으니 Visual Studio에서 IntelliSense가 어떻게 작동하는지 확인할 수 있습니다.

1. 방금 만든 웹 사이트에서 *Default.cshtml* 페이지를 엽니다.
2. 페이지의 `<h3>` 태그 후 점 포함을 입력합니다. `@ServerInfo.` IntelliSense가 드롭다운 목록에서 `ServerInfo` 도우미에 사용할 수 있는 메서드를 표시하는 방법을 확인합니다.

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 목록에서 `GetHtml` 메서드를 선택한 다음 Enter를 누릅니다. IntelliSense는 자동으로 메서드를 채웁니다. C#의 모든 메서드와 마찬가지로 메서드 `()` 다음의 문자를 추가해야 합니다. 메서드에 `GetHtml` 대 한 완료 된 코드는 다음과 같습니다.

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 페이지를 실행하려면 Ctrl+F5를 누릅니다. 브라우저에 표시될 때 페이지의 모양은 다음과 같습니다.

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 브라우저를 닫습니다.

### <a name="using-the-debugger"></a>디버거 사용

1. *Default.cshtml* 페이지 의 맨 위에 는 `Page.Title`로 시작하는 줄 다음에 다음 코드 줄을 추가합니다.

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 코드 왼쪽에 있는 편집기의 회색 여백에서 이 새 줄 옆을 클릭하여 *중단점을 추가합니다.* 중단점은 디버거에게 해당 시점에서 프로그램 실행을 중지하도록 지시하는 마커이므로 무슨 일이 일어나고 있는지 확인할 수 있습니다.

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. `ServerInfo.GetHtml` 메서드에 대한 호출을 제거하고 해당 위치에 `@myTime` 있는 변수에 호출을 추가합니다. 이 호출은 새 코드 줄에서 반환되는 현재 시간 값을 표시합니다.
4. F5를 눌러 디버거에서 페이지를 실행합니다. 페이지는 설정한 중단점에서 중지됩니다. 다음 이미지는 중단점(노란색)이 있는 편집기에서 페이지의 모양을 보여 주며 있습니다.

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 디버그 도구 모음에서 **단계 입력** 단추(또는 F11 를 누르기)를 클릭하여 다음 코드 줄을 실행합니다. 이 단추를 클릭할 때마다 다음 코드 줄로 실행을 진행합니다.

    ![버튼으로 단계](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 마우스 포인터를 `myTime` 위에 놓거나 **지역 변수** 및 **콜 스택** 창에 표시된 값을 검사하여 변수값을 검사합니다. Visual Studio는 변수의 값을 표시합니다.

    ![시간 값 표시](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 변수를 검사하고 코드를 단계별로 실행하면 F5를 눌러 각 줄에서 멈추지 않고 페이지를 계속 실행합니다. 모든 코드를 단계적 단계적 단계로 완료하면 브라우저에 페이지가 표시됩니다.

디버거 및 Visual Studio에서 코드를 디버깅하는 방법에 대한 자세한 내용은 [연습: 비주얼 웹 개발자의 웹 페이지 디버깅을](https://msdn.microsoft.com/library/z9e7w6cs.aspx)참조하십시오.

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>비주얼 스튜디오와 ASP.NET MVC 프로젝트에서 면도기 사용

Razor 구문은 ASP.NET MVC 프로젝트에서도 광범위하게 사용됩니다. MVC는 동적 웹 사이트를 구축하는 강력한 패턴 기반 방법입니다. ASP.NET 웹 페이지 사이트를 유지 관리하기 어려워지면 ASP.NET MVC 응용 프로그램으로 변환하는 것이 좋습니다. MVC 응용 프로그램을 만드는 예제는 [ASP.NET MVC 5로 시작하기 를](../../../mvc/overview/getting-started/introduction/getting-started.md)참조하십시오.

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010에서 ASP.NET 웹 페이지에 대한 지원 설치

이 섹션에서는 Visual Web Developer Express 2010 및 ASP.NET 웹 페이지 도구를 시각적 스튜디오용으로 설치하는 방법을 보여 주며, 이 섹션에서는 다음과 같은 방법을 설명합니다.

1. 웹 플랫폼 설치 관리자가 아직 없는 경우 다음 URL에서 다운로드합니다.

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 웹 플랫폼 설치 관리자를 실행합니다.
3. **제품** 탭을 클릭합니다.

    ![웹PI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. ASP.NET **MVC 4(ASP.NET** 웹 페이지 2의 경우)를 검색한 다음 **에 추가를**클릭합니다. 이러한 제품에는 ASP.NET Razor 웹 사이트를 구축하기 위한 Visual Studio 도구가 포함됩니다.

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 설치를 **Install** 클릭하여 설치를 완료합니다.
