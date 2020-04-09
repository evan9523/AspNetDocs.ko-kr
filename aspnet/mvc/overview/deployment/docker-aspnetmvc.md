---
uid: mvc/overview/deployment/docker-aspnetmvc
title: ASP.NET MVC 애플리케이션을 Windows 컨테이너로 마이그레이션
description: 기존 ASP.NET MVC 애플리케이션을 가져와 Windows Docker 컨테이너에서 실행하는 방법을 알아봅니다.
keywords: 윈도우 컨테이너, 도커, ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675190"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>ASP.NET MVC 애플리케이션을 Windows 컨테이너로 마이그레이션

Windows 컨테이너에서 기존 .NET Framework 기반 애플리케이션을 실행하려면 앱을 변경할 필요가 없습니다. Windows 컨테이너에서 앱을 실행하려면 앱을 포함하는 Docker 이미지를 만들고 컨테이너를 시작합니다. 이 항목에서는 기존 [ASP.NET MVC 애플리케이션](http://www.asp.net/mvc)을 가져오고 Windows 컨테이너에 배포하는 방법을 설명합니다.

기존 ASP.NET MVC 앱으로 시작한 다음 Visual Studio를 사용하여 게시된 자산을 빌드합니다. Docker를 사용하여 앱을 포함하고 실행하는 이미지를 만듭니다. Windows 컨테이너에서 실행 중인 사이트로 이동하고 앱이 작동하는지 확인합니다.

이 문서에서는 Docker에 대한 기본적으로 이해하고 있다고 가정합니다. [Docker 개요](https://docs.docker.com/engine/understanding-docker/)를 참고하여 Docker에 대해 알아볼 수 있습니다.

컨테이너에서 실행할 앱은 임의로 질문에 대답하는 간단한 웹 사이트입니다. 이 앱은 인증이나 데이터베이스 스토리지가 없는 기본 MVC 애플리케이션으로, 웹 계층을 컨테이너로 이동하는 데 집중할 수 있게 합니다. 이후 항목에서는 컨테이너화된 애플리케이션에서 영구 스토리지를 이동 및 관리하는 방법을 보여줍니다.

애플리케이션 이동 과정은 다음 단계로 이루어집니다.

1. [이미지에 대한 자산을 빌드하는 게시 태스크 만들기](#publish-script)
1. [애플리케이션을 실행할 Docker 이미지 빌드](#build-the-image)
1. [이미지를 실행하는 Docker 컨테이너 시작](#start-a-container)
1. [브라우저를 사용하여 애플리케이션 확인](#verify-in-the-browser)

[완료된 애플리케이션](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator)은 GitHub에 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

개발 컴퓨터에는 다음 소프트웨어가 있어야 합니다.

- [윈도우 10 주년 기념 업데이트](https://www.microsoft.com/software-download/windows10/) (이상) 또는 [윈도우 서버 2016](https://www.microsoft.com/cloud-platform/windows-server) (이상)
- [Windows용 Docker](https://docs.docker.com/docker-for-windows/) - 안정적인 버전 1.13.0 또는 1.12 베타 26 이상 버전
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Windows Server 2016을 사용하는 경우 [컨테이너 호스트 배포 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)에 대한 지침을 따르세요.

Docker를 설치하고 시작한 후에 트레이 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows 컨테이너로 전환**을 선택합니다. 그러려면 Windows를 기반으로 하는 Docker 이미지를 실행해야 합니다. 이 명령을 실행하는 데 몇 초 정도 걸립니다.

![윈도우 컨테이너][windows-container]

## <a name="publish-script"></a>게시 스크립트

동일한 위치에서 Docker 이미지에 로드해야 하는 모든 자산을 수집합니다. Visual Studio **게시** 명령을 사용하여 앱에 대한 게시 프로필을 만들 수 있습니다. 이 프로필은 이 자습서의 뒷부분에서 대상 이미지에 복사할 모든 자산을 디렉터리 트리 하나에 배치합니다.

**게시 단계**

1. Visual Studio에서 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.
1. 사용자 **지정 프로필 단추를**클릭한 다음 **파일 시스템을** 메서드로 선택합니다.
1. 디렉터리를 선택합니다. 규칙에 따라 다운로드한 샘플은 `bin\Release\PublishOutput`을 사용합니다.

![게시 연결][publish-connection]

**설정** 탭의 **파일 게시 옵션** 섹션을 **Precompile during publishing**엽니다. 이 최적화는 Docker 컨테이너의 뷰를 컴파일하며 미리 컴파일된 뷰를 복사함을 의미합니다.

![설정 게시][publish-settings]

**게시**를 클릭하면 Visual Studio에서 필요한 모든 자산을 대상 폴더에 복사합니다.

## <a name="build-the-image"></a>이미지 빌드

*Dockerfile이라는* 새 파일을 만들어 Docker 이미지를 정의합니다. *Dockerfile에는* 최종 이미지를 빌드하는 지침이 포함되어 있으며 기본 이미지 이름, 필수 구성 요소, 실행하려는 앱 및 기타 구성 이미지가 포함됩니다. *Dockerfile은* 이미지를 만드는 `docker build` 명령에 대한 입력입니다.

이 연습에서는 [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/)에 있는 `microsoft/aspnet` 이미지를 기반으로 이미지를 빌드합니다.
기본 이미지인 `microsoft/aspnet`은 Windows Server 이미지입니다. 여기에는 Windows 서버 코어, IIS 및 ASP.NET 4.7.2가 포함되어 있습니다. 컨테이너에서 이 이미지를 실행하면 IIS 및 설치된 웹 사이트가 자동으로 시작됩니다.

이미지를 만드는 Dockerfile은 다음과 같이 표시됩니다.

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

이 Dockerfile에는 `ENTRYPOINT` 명령이 없습니다. 해당 명령이 필요하지 않습니다. IIS를 사용하여 Windows Server를 실행할 때 IIS 프로세스는 aspnet 기본 이미지에서 시작하도록 구성된 진입점입니다.

Docker 빌드 명령을 실행하여 ASP.NET 앱을 실행하는 이미지를 만듭니다. 이렇게 하려면 프로젝트 디렉터리에서 PowerShell 창을 열고 솔루션 디렉터리에서 다음 명령을 입력합니다.

```console
docker build -t mvcrandomanswers .
```

이 명령은 Dockerfile의 명령을 사용하여 새 이미지를 빌드하여 이미지를 mvcrandomanswers로 명명(-태그 지정)합니다. 이 과정에 [Docker Hub](http://hub.docker.com)에서 기본 이미지를 끌어온 다음 해당 이미지에 앱이 추가될 수 있습니다.

명령이 완료되면 `docker images` 명령을 실행하여 새 이미지에 대한 정보를 확인할 수 있습니다.

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

사용자 컴퓨터의 이미지 ID는 다릅니다. 이제 앱을 실행해 보겠습니다.

## <a name="start-a-container"></a>컨테이너 시작

다음 `docker run` 명령을 실행하여 컨테이너를 시작합니다.

```console
docker run -d --name randomanswers mvcrandomanswers
```

`-d` 인수는 분리된 모드로 이미지를 시작하도록 Docker에 지정합니다. 즉, Docker 이미지가 현재 셸에서 연결이 끊긴 상태로 실행됩니다.

많은 docker 예제에서 컨테이너 및 호스트 포트를 매핑하는 -p가 표시될 수 있습니다. 기본 aspnet 이미지는 이미 포트 80에서 수신 및 노출하도록 컨테이너를 구성했습니다.

`--name randomanswers`는 실행 중인 컨테이너에 이름을 제공합니다. 대부분의 명령에서 컨테이너 ID 대신 이 이름을 사용할 수 있습니다.

`mvcrandomanswers`는 시작할 이미지의 이름입니다.

## <a name="verify-in-the-browser"></a>브라우저에서 확인

컨테이너가 시작되면 표시된 예제를 `http://localhost` 사용하여 실행 중인 컨테이너에 연결합니다. 해당 URL을 브라우저에 입력하면 실행 중인 사이트가 표시됩니다.

> [!NOTE]
> 일부 VPN 또는 프록시 소프트웨어가 사이트로 이동하지 못하도록 차단할 수도 있습니다.
> 일시적으로 사용하지 않도록 설정하여 컨테이너가 작동하는지 확인할 수 있습니다.

GitHub의 샘플 디렉터리에는 이러한 명령을 자동으로 실행하는 [PowerShell 스크립트](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)가 들어 있습니다. PowerShell 창을 열고 디렉터리를 솔루션 디렉터리로 변경한 후 다음을 입력합니다.

```console
./run.ps1
```

위의 명령은 이미지를 빌드하고 컴퓨터에 이미지 목록을 표시하고 컨테이너를 시작합니다.

컨테이너를 중지하려면 `docker stop` 명령을 실행합니다.

```console
docker stop randomanswers
```

컨테이너를 제거하려면 `docker rm` 명령을 실행합니다.

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows 컨테이너로 전환"
[publish-connection]: media/aspnetmvc/PublishConnection.png "파일 시스템에 게시"
[publish-settings]: media/aspnetmvc/PublishSettings.png "설정 게시"
