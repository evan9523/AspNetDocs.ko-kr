---
title: ASP.NET Core 디렉터리 구조
author: guardrex
description: 게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 12/11/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 4bc5ead8e24c4bb7fe6cd2f52fd2aa622187180c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025080"
---
# <a name="aspnet-core-directory-structure"></a>ASP.NET Core 디렉터리 구조

[Luke Latham](https://github.com/guardrex)으로

*게시* 디렉터리에는 [dotnet 게시](/dotnet/core/tools/dotnet-publish) 명령에 의해 생성된 앱의 배포 가능한 자산이 포함되어 있습니다. 디렉터리에는 다음이 포함됩니다.

* 애플리케이션 파일
* 구성 파일
* 정적 자산
* 패키지
* 런타임([자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)만 해당)

| 앱 형식 | 디렉터리 구조 |
| -------- | ------------------- |
| [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</li><li>Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</li><li>Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</li><li>wwwroot&dagger;</li><li>*\.dll 파일</li><li>{ASSEMBLY NAME}.deps.json</li><li>{ASSEMBLY NAME}.dll</li><li>{ASSEMBLY NAME}.pdb</li><li>{ASSEMBLY NAME}.Views.dll</li><li>{ASSEMBLY NAME}.Views.pdb</li><li>{ASSEMBLY NAME}.runtimeconfig.json</li><li>web.config(IIS 배포)</li></ul></li></ul> |
| [자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</li><li>Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</li><li>Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</li><li>wwwroot&dagger;</li><li>\*.dll 파일</li><li>{ASSEMBLY NAME}.deps.json</li><li>{ASSEMBLY NAME}.dll</li><li>{ASSEMBLY NAME}.exe</li><li>{ASSEMBLY NAME}.pdb</li><li>{ASSEMBLY NAME}.Views.dll</li><li>{ASSEMBLY NAME}.Views.pdb</li><li>{ASSEMBLY NAME}.runtimeconfig.json</li><li>web.config(IIS 배포)</li></ul></li></ul> |

&dagger;디렉터리를 나타냄

*publish* 디렉터리는 배포의 *애플리케이션 기본 경로*라고도 하는 *콘텐츠 루트 경로*를 나타냅니다. 서버에 배포된 앱의 *publish* 디렉터리에 어떤 이름을 지정하더라도 해당 위치는 호스트된 앱에 대한 서버의 실제 경로로 사용됩니다.

*wwwroot* 디렉터리(있는 경우)에는 정적 자산만 포함됩니다.

다음 두 가지 방법 중 하나를 사용하여 *Logs* 디렉터리를 배포용으로 만들 수 있습니다.

* 다음 `<Target>` 요소를 프로젝트 파일에 추가합니다.

   ```xml
   <Target Name="CreateLogsFolder" AfterTargets="Publish">
     <MakeDir Directories="$(PublishDir)Logs" 
              Condition="!Exists('$(PublishDir)Logs')" />
     <WriteLinesToFile File="$(PublishDir)Logs\.log" 
                       Lines="Generated file" 
                       Overwrite="True" 
                       Condition="!Exists('$(PublishDir)Logs\.log')" />
   </Target>
   ```

   `<MakeDir>` 요소는 게시된 출력에 빈 *Logs* 폴더를 만듭니다. 이 요소는 `PublishDir` 속성을 사용하여 폴더를 만들 대상 위치를 확인합니다. 웹 배포와 같은 여러 배포 방법에서는 배포 중에 빈 폴더를 건너뜁니다. `<WriteLinesToFile>` 요소는 파일이 서버에 배포되도록 *Logs* 폴더에 파일을 생성합니다. 대상 폴더에 대한 쓰기 권한이 작업자 프로세스에 없는 경우 이 방법을 사용한 폴더 만들기가 실패합니다.

* 배포 시 서버에서 *Logs* 디렉터리를 실제로 만드세요.

배포 디렉터리에는 읽기/실행 권한이 필요합니다. *Logs* 디렉터리에는 읽기/쓰기 권한이 필요합니다. 파일이 작성되는 추가 디렉터리에는 읽기/쓰기 권한이 필요합니다.

[ASP.NET Core 모듈 stdout 로깅](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)은 배포에 *로그* 폴더가 필요하지 않습니다. 모듈은 로그 파일을 만들 때 `stdoutLogFile` 경로에 폴더를 만들 수 있습니다. *로그* 폴더를 만드는 것은 [ASP.NET Core 모듈 향상된 디버그 로깅](xref:host-and-deploy/aspnet-core-module#enhanced-diagnostic-logs)에 유용합니다. `<handlerSetting>` 값에 제공된 경로에 있는 폴더는 모듈에서 자동으로 생성되지 않으며 모듈이 디버그 로그를 작성할 수 있도록 배포에 미리 존재해야 합니다.

## <a name="additional-resources"></a>추가 자료

* [dotnet publish](/dotnet/core/tools/dotnet-publish)
* [.NET Core 애플리케이션 배포](/dotnet/core/deploying/)
* [대상 프레임워크](/dotnet/standard/frameworks)
* [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)
