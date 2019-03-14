---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062600"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Movie 모델 스캐폴드

* 명령줄에서 다음을 실행합니다(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 프로젝트 디렉터리에서).

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

오류가 표시될 경우:
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

앞의 오류는 잘못된 디렉터리에 있는 경우 발생합니다. 명령 셸에서 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)를 연 다음, 이전 명령을 실행합니다.

오류가 표시될 경우:
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

Visual Studio를 종료하고 명령을 다시 실행합니다.
