---
title: ASP.NET Core MVC 시작
author: rick-anderson
description: ASP.NET Core MVC를 시작하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: c09c06f55c4179e9e2174f0063ab7387b7e4c31b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059250"
---
# <a name="get-started-with-aspnet-core-mvc"></a>ASP.NET Core MVC 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 자습서에서는 ASP.NET Core MVC 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.

앱은 동영상 제목의 데이터베이스를 관리합니다. 여기에서는 다음과 같은 작업을 수행하는 방법에 대해 배우게 됩니다.

> [!div class="checklist"]
> * 웹앱을 만듭니다.
> * 모델 추가 및 스캐폴드
> * 데이터베이스 작업
> * 검색 및 유효성 검사 추가

마지막으로 동영상 데이터를 관리하고 표시할 수 있는 앱이 있습니다.

[!INCLUDE[](~/includes/mvc-intro/download.md)]

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a>웹앱 만들기

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

**새 프로젝트** 대화 상자를 완료합니다.

* 왼쪽 창에서 **.NET Core**를 선택합니다.
* 가운데 창에서 **ASP.NET Core 웹 애플리케이션(.NET Core)** 을 선택합니다.
* 프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).
* **확인** 선택

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project2-21.png)

**새 ASP.NET Core 웹 애플리케이션(.NET Core) - MvcMovie** 대화 상자를 완료합니다.

* 버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.2**를 선택합니다.
* **웹 애플리케이션(모델-뷰-컨트롤러)** 을 선택합니다.
* **확인**을 선택합니다.

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project22-21.png)

Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다. 프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다. 다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

이 자습서에서는 VS 코드를 잘 알고 있다고 가정합니다. 자세한 내용은 [VS 코드 시작](https://code.visualstudio.com/docs) 및 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.

* [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.
* 디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.
* 다음 명령을 실행합니다.

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * **이 있는 대화 상자가 나타나고 'MvcMovie'에서 빌드 및 디버그에 필요한 자산이 누락되었습니다. 추가할까요?**  **예**를 선택합니다.

  * `dotnet new mvc -o MvcMovie`: *MvcMovie* 폴더에 새 ASP.NET Core MVC 포로젝트를 만듭니다.
  * `code -r MvcMovie`: Visual Studio Code에서 *MvcMovie.csproj* 프로젝트 파일을 로드합니다.

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **파일** > **새 솔루션**을 선택합니다.

  ![macOS 새 솔루션](~/tutorials/first-web-api-mac/_static/sln.png)

* **.NET Core 앱** > **ASP.NET Core** > **ASP.NET Core Web App(MVC)** > **다음**을 선택합니다.

  ![macOS 새 프로젝트 대화 상자](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* **새 ASP.NET Core Web API 구성** 대화 상자에서 **.NET Core 2.2*라는 기본 **대상 프레임워크**를 수락합니다.

* 프로젝트 이름을 **MvcMovie**로 지정하고 **만들기**를 선택합니다.

---  
<!-- End of VS tabs -->

### <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

**Ctrl-F5**를 선택하여 비디버그 모드에서 앱을 실행합니다.

[!INCLUDE[](~/includes/trustCertVS.md)]

* Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.
* Ctrl+F5(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.
* **디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.

  ![디버그 메뉴](start-mvc/_static/debug_menu.png)

* **IIS Express** 단추를 선택하여 앱을 디버그할 수 있습니다.

  ![IIS Express](start-mvc/_static/iis_express.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code) 

Ctrl+F5를 눌러 디버거 없이 실행합니다.

[!INCLUDE[](~/includes/trustCertVSC.md)]

  Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `https://localhost:5001`로 이동합니다. 주소 표시줄에 `localhost:port:5001`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.

  Ctrl+F5(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

**실행** > **디버깅하지 않고 시작**을 선택하여 앱을 시작합니다. Mac용 Visual Studio에서 [Kestrel](xref:fundamentals/servers/index#kestrel) 서버를 시작하고, 브라우저를 실행하며, `http://localhost:port`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.

[!INCLUDE[](~/includes/trustCertMac.md)]

* 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.
* **실행** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.

------

* **승인**을 선택하여 추적에 동의합니다. 이 앱은 개인 정보를 추적하지 않습니다. 템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.

  ![홈 또는 인덱스 페이지](start-mvc/_static/privacy.png)

  다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.

  ![홈 또는 인덱스 페이지](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.

> [!div class="step-by-step"]
> [다음](adding-controller.md)  
