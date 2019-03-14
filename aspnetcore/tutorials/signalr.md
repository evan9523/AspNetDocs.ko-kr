---
title: ASP.NET Core SignalR로 시작
author: bradygaster
description: 이 자습서에서는 ASP.NET Core SignalR을 사용하는 채팅 앱을 만듭니다.
ms.author: bradyg
ms.custom: mvc
ms.date: 11/30/2018
uid: tutorials/signalr
ms.openlocfilehash: 53ec924c2d7b4fac227be0c0bf24d93476528167
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029030"
---
# <a name="tutorial-get-started-with-aspnet-core-signalr"></a>자습서: ASP.NET Core SignalR 시작

본 자습서에서는 SignalR을 이용해서 실시간 앱을 구현하기 위한 기본 사항을 알려줍니다. 여기에서는 다음과 같은 작업을 수행하는 방법에 대해 배우게 됩니다.

> [!div class="checklist"]
> * 웹 프로젝트를 만듭니다.
> * SignalR 클라이언트 라이브러리를 추가합니다.
> * SignalR 허브를 만듭니다.
> * SignalR을 사용하도록 프로젝트를 구성합니다.
> * 모든 클라이언트에서 연결된 모든 클라이언트로 메시지를 보내는 코드를 추가합니다.

이 모든 과정을 마치면 동작하는 채팅 앱이 만들어집니다.

![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

[!INCLUDE [|Prerequisites](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-project"></a>웹 프로젝트 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* 메뉴에서 **파일 > 새 프로젝트**를 선택합니다.

* **새 프로젝트** 대화 상자에서 **설치됨 &gt; Visual C# &gt; 웹 &gt; ASP.NET Core 웹 애플리케이션**을 선택합니다. 프로젝트의 이름을 *SignalRChat*로 지정합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

* Razor Pages를 사용하는 프로젝트를 생성하려면 **웹 애플리케이션**을 선택합니다.

* **.NET Core**의 대상 프레임워크를 선택하고, **ASP.NET Core 2.2**를 선택하고, **확인**을 클릭합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 새 프로젝트 폴더를 만들 폴더에 대한 [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.

* 다음 명령을 실행합니다.

   ```console
   dotnet new webapp -o SignalRChat
   code -r SignalRChat
   ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **파일 > 새 솔루션**을 선택합니다.

* **.NET Core > 앱 > ASP.NET Core 웹앱**(**ASP.NET Core 웹앱(MVC) 선택 안 함**)을 선택합니다.

* **새로 만들기**를 선택합니다.

* 프로젝트 이름을 *SignalRChat*로 지정한 다음, **만들기**를 선택합니다.

---

## <a name="add-the-signalr-client-library"></a>SignalR 클라이언트 라이브러리 추가

SignalR 서버 라이브러리는 `Microsoft.AspNetCore.App` 메타패키지에 포함되어 있습니다. JavaScript 클라이언트 라이브러리는 프로젝트에 자동으로 포함되지 않습니다. 본 자습서에서는 라이브러리 관리자(LibMan)를 사용하여 *unpkg*에서 클라이언트 라이브러리를 가져옵니다. unpkg는 Node.js의 패키지 관리자인 npm에서 찾은 모든 내용을 전달할 수 있는 콘텐츠 배달 네트워크(CDN, Content Delivery Network)입니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **클라이언트 쪽 라이브러리**를 선택합니다.

* **클라이언트 쪽 라이브러리 추가** 대화 상자에서 **공급자**로 **unpkg**를 선택합니다. 

* **라이브러리**에 `@aspnet/signalr@1`을 입력하고 미리 보기가 아닌 최신 버전을 선택합니다.

  ![클라이언트 쪽 라이브러리 추가 대화 상자 - 라이브러리 선택](signalr/_static/libman1.png)

* **Choose specific files**(특정 파일 선택)를 선택하고 *dist/browser* 폴더를 확장한 후 *signalr.js* 및 *signalr.min.js*를 선택합니다.

* **대상 위치**를 *wwwroot/lib/signalr/* 로 설정하고 **설치**를 선택합니다.

  ![클라이언트 쪽 라이브러리 추가 대화 상자 - 파일 및 대상 선택](signalr/_static/libman2.png)

  그러면 LibMan이 *wwwroot/lib/signalr* 폴더를 생성한 다음 여기에 선택한 파일을 복사합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 통합 터미널에서 다음 명령을 실행하여 LibMan을 설치합니다.

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 다음 명령을 실행하고 LibMan을 사용하여 SignalR 클라이언트 라이브러리를 가져옵니다. 출력이 표시되기 전에 잠시 기다려야 할 수도 있습니다.

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  매개 변수는 다음 옵션을 지정합니다.
  * unpkg 공급자를 사용합니다.
  * 파일을 *wwwroot/lib/signalr* 대상으로 복사합니다.
  * 지정된 파일만 복사합니다.

  출력은 다음 예와 같습니다.

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **터미널**에서 다음 명령을 실행하여 LibMan을 설치합니다.

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).

* 다음 명령을 실행하고 LibMan을 사용하여 SignalR 클라이언트 라이브러리를 가져옵니다.

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  매개 변수는 다음 옵션을 지정합니다.
  * unpkg 공급자를 사용합니다.
  * 파일을 *wwwroot/lib/signalr* 대상으로 복사합니다.
  * 지정된 파일만 복사합니다.

  출력은 다음 예와 같습니다.

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

---

## <a name="create-a-signalr-hub"></a>SignalR 허브 만들기

*허브*는 클라이언트-서버 통신을 처리하는 높은 수준의 파이프라인으로 제공되는 클래스입니다.

* SignalRChat 프로젝트 폴더에서 *Hubs* 폴더를 만듭니다.

* *Hubs* 폴더에 다음 코드를 사용하여 *ChatHub.cs* 파일을 만듭니다.

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  `ChatHub` 클래스는 SignalR `Hub` 클래스에서 상속합니다. `Hub` 클래스는 연결, 그룹 및 메시징을 관리합니다.

  연결된 클라이언트에서 `SendMessage` 메서드를 호출하여 모든 클라이언트에 메시지를 보낼 수 있습니다. 메서드를 호출하는 JavaScript 클라이언트 코드는 자습서 뒷부분에 나와 있습니다. SignalR 코드는 최대한의 확장성을 제공할 수 있도록 비동기적입니다.

## <a name="configure-signalr"></a>SignalR 구성

SignalR 서버는 SignalR에 SignalR 요청을 전달하도록 구성되어야 합니다.

* 다음 강조 표시된 코드를 *Startup.cs* 파일에 추가합니다.

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  이러한 변경 사항은 ASP.NET Core 종속성 주입 시스템 및 미들웨어 파이프라인에 SignalR을 추가합니다.

## <a name="add-signalr-client-code"></a>SignalR 클라이언트 코드 추가

* *Pages\Index.cshtml*의 콘텐츠를 다음 코드로 바꿉니다.

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  위의 코드는:

  * 이름 및 메시지 텍스트에 대한 텍스트 상자 및 전송 단추를 만듭니다.
  * SignalR 허브에서 받은 메시지를 표시하기 위해 `id="messagesList"`를 사용하여 목록을 만듭니다.
  * SignalR에 대한 스크립트 참조 및 다음 단계에서 만드는 *chat.js* 애플리케이션 코드를 포함합니다.

* *wwwroot/js* 폴더에서 다음 코드를 사용하여 *chat.js* 파일을 만듭니다.

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  위의 코드는:

  * 연결을 만들고 시작합니다.
  * 허브에 메시지를 전송하는 처리기를 전송 단추에 추가합니다.
  * 허브에서 메시지를 수신하고 목록에 추가하는 처리기를 연결 개체에 추가합니다.

## <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* 통합 터미널에서 다음 명령을 실행합니다.

  ```console
  dotnet run -p SignalRChat.csproj
  ```
  
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **실행 > 디버깅하지 않고 시작**을 선택합니다.

---

* 주소 표시줄에서 URL을 복사하고, 다른 브라우저 인스턴스 또는 탭을 열고, 주소 표시줄에 URL을 붙여넣습니다.

* 브라우저 중 하나를 선택하고, 이름 및 메시지를 입력하고, **보내기 메시지** 단추를 선택합니다.

  이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.

  ![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> 앱이 작동하지 않는 경우 브라우저 개발자 도구(F12)를 열고 콘솔로 이동합니다. HTML 및 JavaScript 코드와 관련된 오류를 볼 수 있습니다. 예를 들어 지정되지 않은 다른 폴더에 *signalr.js*를 넣었다고 가정합니다. 이 경우 해당 파일에 대한 참조는 작동하지 않으며 콘솔에 404 오류가 표시됩니다.
> ![signalr.js 찾을 수 없음 오류](signalr/_static/f12-console.png)

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.

> [!div class="checklist"]
> * 웹앱 프로젝트를 만듭니다.
> * SignalR 클라이언트 라이브러리를 추가합니다.
> * SignalR 허브를 만듭니다.
> * SignalR을 사용하도록 프로젝트를 구성합니다.
> * 허브를 사용하여 모든 클라이언트에서 연결된 모든 클라이언트에 메시지를 보내는 코드를 추가합니다.

SignalR에 대해 자세히 알아보려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [ASP.NET Core SignalR 소개](xref:signalr/introduction)
