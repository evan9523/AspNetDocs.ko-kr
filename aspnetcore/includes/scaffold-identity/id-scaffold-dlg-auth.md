---
ms.openlocfilehash: cb9041a466309a400b19cdecd76f653499c6ac4b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053980"
---
Identity 스 캐 폴더를 실행 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 > **추가** > **스 캐 폴드 된 새 항목**합니다.
* 왼쪽된 창에서 합니다 **스 캐 폴드 추가** 대화 상자에서 **Identity** > **추가**합니다.
* 에 **ADD Id** 대화 상자에서 원하는 옵션을 선택 합니다.
  * 기존 레이아웃 페이지를 선택 하거나 잘못 된 태그를 사용 하 여 레이아웃 파일을 덮어쓰게 됩니다. 기존  *\_Layout.cshtml* 파일을 선택 하면 것 **하지** 덮어씁니다.

 예를 들어 `~/Pages/Shared/_Layout.cshtml` Razor 페이지에 대 한 `~/Views/Shared/_Layout.cshtml` MVC 프로젝트
* 기존 데이터 컨텍스트를 사용 하려면 재정의를 하나 이상의 파일을 선택 합니다. 데이터 컨텍스트를 추가 하려면 파일을 하나 이상 선택 해야 합니다.
  * 데이터 컨텍스트 클래스를 선택 합니다.
  * 선택 **추가**합니다.
* 새 사용자 컨텍스트를 만들고 Id에 대 한 사용자 지정 사용자 클래스를 만들 수 있습니다.
  * 선택 된 **+** 새 단추 **데이터 컨텍스트 클래스**합니다.
  * 선택 **추가**합니다.

참고: 새 사용자 컨텍스트를 만드는 경우 재정의 파일을 선택할 필요가 없습니다.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

ASP.NET Core 스 캐 폴더를 이전에 설치 하지 않은 경우 지금 설치 합니다.

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

에 대 한 패키지 참조 추가 [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) 프로젝트 (\*.csproj) 파일입니다. 프로젝트 디렉터리에서 다음 명령을 실행 합니다.

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Identity 스 캐 폴더 옵션을 나열 하려면 다음 명령을 실행 합니다.

```cli
dotnet aspnet-codegenerator identity -h
```

프로젝트 폴더에서 원하는 옵션을 사용 하 여 Identity 스 캐 폴더를 실행 합니다. 예를 들어, 기본 UI 사용 하 여 id 및 파일의 최소 수를을 설정 하려면 다음 명령을 실행 합니다. 프로그램 DB 컨텍스트에 대 한 올바른 정규화 된 이름을 사용 합니다.

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

Powershell 명령 구분 기호로 세미콜론을 사용합니다. Powershell을 사용 하는 경우 파일 목록에 세미콜론을 이스케이프 또는 큰따옴표로 파일 목록을 저장 합니다. 예를 들어:

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"
```

Identity 스 캐 폴더를 지정 하지 않고 실행 하는 경우는 `--files` 플래그 또는 `--useDefaultUI` 플래그를 모두 사용할 수 있는 Identity UI 페이지가 프로젝트에 생성 됩니다.

-------------
