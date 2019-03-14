---
title: '자습서: ASP.NET Core에서 Razor 페이지 시작'
author: rick-anderson
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 81a2a76fc1cecc78b69226fe714d7c9272b04bf7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046040"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a>자습서: ASP.NET Core에서 Razor 페이지 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 시리즈의 첫 번째 자습서입니다. [시리즈](xref:tutorials/razor-pages/index)에서는 ASP.NET Core Razor Pages 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.

[!INCLUDE[](~/includes/advancedRP.md)]

시리즈가 끝나면 영화의 데이터베이스를 관리하는 앱이 생성됩니다.  

[!INCLUDE[View or download sample code](~/includes/rp/download.md)]

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Razor Pages 웹앱 만들기
> * 앱을 실행합니다.
> * 프로젝트 파일을 검사합니다.

이 자습서가 끝나면 나중에 자습서에서 빌드할 Razor Pages 웹앱을 사용할 수 있습니다.

![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-pages-web-app"></a>Razor 페이지 웹앱 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.

* 새 ASP.NET Core 웹 애플리케이션을 만듭니다. 프로젝트 이름을 **RazorPagesMovie**로 지정합니다. 코드를 복사하여 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.

  ![새 ASP.NET Core 웹 애플리케이션](razor-pages-start/_static/np_2.1.png)

* 드롭다운에서 **ASP.NET Core 2.2**를 선택한 다음, **웹 애플리케이션**을 선택합니다.

  ![새 ASP.NET Core 웹 애플리케이션](razor-pages-start/_static/np_2_2.2.png)

  다음 시작 프로젝트를 만듭니다.

  ![솔루션 탐색기](razor-pages-start/_static/se2.2.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.

* 디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.

* 다음 명령을 실행합니다.

  ```console
  dotnet new webapp -o RazorPagesMovie
  code -r RazorPagesMovie
  ```

  * `dotnet new` 명령은 *RazorPagesMovie* 폴더에서 새 Razor Pages 프로젝트를 만듭니다.
  * `code` 명령은 Visual Studio Code의 새 인스턴스에서 *RazorPagesMovie* 폴더를 엽니다.

  다음과 같은 대화 상자가 표시됩니다. **빌드 및 디버그에 필요한 자산이 'RazorPagesMovie'에서 누락되었습니다. 추가할까요?**

* **예**를 선택합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

터미널에서 다음 명령을 실행합니다.

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
```

이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor Pages 프로젝트를 만듭니다.

## <a name="open-the-project"></a>프로젝트 열기

Visual Studio에서 **파일 > 열기**를 선택하고 *RazorPagesMovie.csproj* 파일을 선택합니다.

<!-- End of VS tabs -->

---

## <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Ctrl+F5를 눌러 디버거 없이 실행합니다.

  [!INCLUDE[](~/includes/trustCertVS.md)]

  Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. `localhost`가 로컬 컴퓨터의 표준 호스트 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.
  
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* **Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.

  [!INCLUDE[](~/includes/trustCertVSC.md)]

  Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`로 이동합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.
  
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

**실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다. Visual Studio가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`으로 이동합니다.

[!INCLUDE[](~/includes/trustCertMac.md)]

<!-- End of VS tabs -->

---

* 앱의 홈페이지에서 **승인**을 선택하여 추적에 동의합니다.

  이 앱은 개인 정보를 추적하지 않지만 유럽 연합의 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 준수하기 위해 필요한 경우 프로젝트 템플릿에는 동의 기능이 포함됩니다.

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR2.2.png)

  다음 이미지에서는 추적에 동의한 후에 앱을 보여줍니다.

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

## <a name="examine-the-project-files"></a>프로젝트 파일 검사

이후 자습서에서 작업할 주요 프로젝트 폴더 및 파일에 대한 개요는 다음과 같습니다.

### <a name="pages-folder"></a>페이지 폴더

Razor 페이지 및 지원 파일이 들어 있습니다. 각 Razor 페이지는 파일 쌍입니다.

* Razor 구문을 사용하는 C# 코드로 HTML 태그를 포함하는 *.cshtml* 파일.
* 페이지 이벤트를 처리하는 C# 코드가 포함된 *.cshtml.cs* 파일.

지원 파일에는 밑줄로 시작하는 이름이 있습니다. 예를 들어 *_Layout.cshtml* 파일은 모든 페이지에 공통되는 UI 요소를 구성합니다. 이 파일은 페이지 맨 위에 있는 탐색 메뉴를 설정하고 페이지 맨 아래에 저작권 표시를 설정합니다. 자세한 내용은 <xref:mvc/views/layout>을 참조하세요.


### <a name="wwwroot-folder"></a>wwwroot 폴더

HTML 파일, JavaScript 파일 및 CSS 파일과 같은 정적 파일을 포함합니다. 자세한 내용은 <xref:fundamentals/static-files>을 참조하세요.

### <a name="appsettingsjson"></a>appSettings.json

연결 문자열과 같은 구성 데이터를 포함합니다. 자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.

### <a name="programcs"></a>Program.cs

프로그램의 진입점을 포함합니다. 자세한 내용은 <xref:fundamentals/host/web-host>을 참조하세요.

### <a name="startupcs"></a>Startup.cs

쿠키에 대한 동의 필요 여부 등 앱 동작을 구성하는 코드를 포함합니다. 자세한 내용은 <xref:fundamentals/startup>을 참조하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Razor Pages 웹앱을 만들었습니다.
> * 앱을 실행합니다.
> * 프로젝트 파일을 검사했습니다.

시리즈의 다음 자습서로 이동합니다.

> [!div class="step-by-step"]
> [모델 추가](xref:tutorials/razor-pages/model)
