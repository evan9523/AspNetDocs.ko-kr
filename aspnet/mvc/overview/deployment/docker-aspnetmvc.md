---
uid: mvc/overview/deployment/docker-aspnetmvc
title: ASP.NET MVC 애플리케이션을 Windows 컨테이너로 마이그레이션
description: 기존 ASP.NET MVC 애플리케이션을 가져와 Windows Docker 컨테이너에서 실행하는 방법을 알아봅니다.
keywords: Windows 컨테이너, Docker, ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 1c5e6af79c87123891ddd4d30c60e3a427910e9d
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763483"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="0e6d9-104">ASP.NET MVC 애플리케이션을 Windows 컨테이너로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0e6d9-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="0e6d9-105">Windows 컨테이너에서 기존 .NET Framework 기반 애플리케이션을 실행하려면 앱을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="0e6d9-106">Windows 컨테이너에서 앱을 실행하려면 앱을 포함하는 Docker 이미지를 만들고 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="0e6d9-107">이 항목에서는 기존 [ASP.NET MVC 애플리케이션](http://www.asp.net/mvc)을 가져오고 Windows 컨테이너에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="0e6d9-108">기존 ASP.NET MVC 앱으로 시작한 다음 Visual Studio를 사용하여 게시된 자산을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="0e6d9-109">Docker를 사용하여 앱을 포함하고 실행하는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="0e6d9-110">Windows 컨테이너에서 실행 중인 사이트로 이동하고 앱이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="0e6d9-111">이 문서에서는 Docker에 대한 기본적으로 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="0e6d9-112">[Docker 개요](https://docs.docker.com/engine/understanding-docker/)를 참고하여 Docker에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="0e6d9-113">컨테이너에서 실행할 앱은 임의로 질문에 대답하는 간단한 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="0e6d9-114">이 앱은 인증이나 데이터베이스 스토리지가 없는 기본 MVC 애플리케이션으로, 웹 계층을 컨테이너로 이동하는 데 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="0e6d9-115">이후 항목에서는 컨테이너화된 애플리케이션에서 영구 스토리지를 이동 및 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="0e6d9-116">애플리케이션 이동 과정은 다음 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="0e6d9-117">이미지에 대한 자산을 빌드하는 게시 태스크 만들기</span><span class="sxs-lookup"><span data-stu-id="0e6d9-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="0e6d9-118">애플리케이션을 실행할 Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="0e6d9-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="0e6d9-119">이미지를 실행하는 Docker 컨테이너 시작</span><span class="sxs-lookup"><span data-stu-id="0e6d9-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="0e6d9-120">브라우저를 사용하여 애플리케이션 확인</span><span class="sxs-lookup"><span data-stu-id="0e6d9-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="0e6d9-121">[완료된 애플리케이션](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/deployment/docker-aspnetmvc/samples/MVCRandomAnswerGenerator)은 GitHub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-121">The [finished application](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/deployment/docker-aspnetmvc/samples/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e6d9-122">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0e6d9-122">Prerequisites</span></span>

<span data-ttu-id="0e6d9-123">개발 컴퓨터에는 다음 소프트웨어가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="0e6d9-124">[Windows 10 기념일 업데이트](https://www.microsoft.com/software-download/windows10/) (또는 그 이상) 또는 [windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) 이상</span><span class="sxs-lookup"><span data-stu-id="0e6d9-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="0e6d9-125">[Windows용 Docker](https://docs.docker.com/docker-for-windows/) - 안정적인 버전 1.13.0 또는 1.12 베타 26 이상 버전</span><span class="sxs-lookup"><span data-stu-id="0e6d9-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="0e6d9-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0e6d9-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="0e6d9-127">Windows Server 2016을 사용하는 경우 [컨테이너 호스트 배포 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)에 대한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="0e6d9-128">Docker를 설치하고 시작한 후에 트레이 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows 컨테이너로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="0e6d9-129">그러려면 Windows를 기반으로 하는 Docker 이미지를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="0e6d9-130">이 명령을 실행하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="0e6d9-131">![Windows 컨테이너][windows-container]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="0e6d9-132">게시 스크립트</span><span class="sxs-lookup"><span data-stu-id="0e6d9-132">Publish script</span></span>

<span data-ttu-id="0e6d9-133">동일한 위치에서 Docker 이미지에 로드해야 하는 모든 자산을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="0e6d9-134">Visual Studio **게시** 명령을 사용하여 앱에 대한 게시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="0e6d9-135">이 프로필은 이 자습서의 뒷부분에서 대상 이미지에 복사할 모든 자산을 디렉터리 트리 하나에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="0e6d9-136">**게시 단계**</span><span class="sxs-lookup"><span data-stu-id="0e6d9-136">**Publish Steps**</span></span>

1. <span data-ttu-id="0e6d9-137">Visual Studio에서 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="0e6d9-138">**사용자 지정 프로필 단추**를 클릭 한 다음 **파일 시스템** 을 방법으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="0e6d9-139">디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-139">Choose the directory.</span></span> <span data-ttu-id="0e6d9-140">규칙에 따라 다운로드한 샘플은 `bin\Release\PublishOutput`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="0e6d9-141">![게시 연결][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="0e6d9-142">**설정** 탭의 **파일 게시 옵션** 섹션을 엽니다. **게시 중 미리 컴파일**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="0e6d9-143">이 최적화는 Docker 컨테이너의 뷰를 컴파일하며 미리 컴파일된 뷰를 복사함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="0e6d9-144">![게시 설정][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="0e6d9-145">**게시**를 클릭하면 Visual Studio에서 필요한 모든 자산을 대상 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="0e6d9-146">이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="0e6d9-146">Build the image</span></span>

<span data-ttu-id="0e6d9-147">Docker 이미지를 정의 하는 *Dockerfile* 이라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="0e6d9-148">*Dockerfile* 에는 최종 이미지를 작성 하는 지침이 포함 되어 있으며 기본 이미지 이름, 필수 구성 요소, 실행 하려는 앱 및 기타 구성 이미지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="0e6d9-149">*Dockerfile* 은 `docker build` 이미지를 만드는 명령에 대 한 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="0e6d9-150">이 연습에서는 `microsoft/aspnet` [Docker 허브](https://hub.docker.com/r/microsoft/aspnet/)에 있는 이미지를 기반으로 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="0e6d9-151">기본 이미지인 `microsoft/aspnet`은 Windows Server 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="0e6d9-152">여기에는 Windows Server Core, IIS 및 ASP.NET 4.7.2가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="0e6d9-153">컨테이너에서 이 이미지를 실행하면 IIS 및 설치된 웹 사이트가 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="0e6d9-154">이미지를 만드는 Dockerfile은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="0e6d9-155">이 Dockerfile에는 `ENTRYPOINT` 명령이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="0e6d9-156">해당 명령이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-156">You don't need one.</span></span> <span data-ttu-id="0e6d9-157">IIS를 사용 하 여 Windows Server를 실행 하는 경우 IIS 프로세스는 aspnet 기본 이미지에서 시작 하도록 구성 된 entrypoint입니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="0e6d9-158">Docker 빌드 명령을 실행하여 ASP.NET 앱을 실행하는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="0e6d9-159">이렇게 하려면 프로젝트의 디렉터리에서 PowerShell 창을 열고 솔루션 디렉터리에 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="0e6d9-160">이 명령은 Dockerfile의 지침을 사용 하 여 이미지를 mvcrandomanswers로 명명 (-t 태깅) 하는 새 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="0e6d9-161">이 과정에 [Docker Hub](http://hub.docker.com)에서 기본 이미지를 끌어온 다음 해당 이미지에 앱이 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="0e6d9-162">명령이 완료되면 `docker images` 명령을 실행하여 새 이미지에 대한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="0e6d9-163">사용자 컴퓨터의 이미지 ID는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="0e6d9-164">이제 앱을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="0e6d9-165">컨테이너 시작</span><span class="sxs-lookup"><span data-stu-id="0e6d9-165">Start a container</span></span>

<span data-ttu-id="0e6d9-166">다음 `docker run` 명령을 실행하여 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="0e6d9-167">`-d` 인수는 분리된 모드로 이미지를 시작하도록 Docker에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="0e6d9-168">즉, Docker 이미지가 현재 셸에서 연결이 끊긴 상태로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="0e6d9-169">대부분의 docker 예제에서 컨테이너와 호스트 포트를 매핑하기 위해-p가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="0e6d9-170">기본 aspnet 이미지는 포트 80에서 수신 대기 하 고 노출 하도록 컨테이너를 이미 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="0e6d9-171">`--name randomanswers`는 실행 중인 컨테이너에 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="0e6d9-172">대부분의 명령에서 컨테이너 ID 대신 이 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="0e6d9-173">`mvcrandomanswers`는 시작할 이미지의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="0e6d9-174">브라우저에서 확인</span><span class="sxs-lookup"><span data-stu-id="0e6d9-174">Verify in the browser</span></span>

<span data-ttu-id="0e6d9-175">컨테이너가 시작 되 면 표시 된 예제에서를 사용 하 여 실행 중인 컨테이너에 연결 `http://localhost` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="0e6d9-176">해당 URL을 브라우저에 입력하면 실행 중인 사이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="0e6d9-177">일부 VPN 또는 프록시 소프트웨어가 사이트로 이동하지 못하도록 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="0e6d9-178">일시적으로 사용하지 않도록 설정하여 컨테이너가 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="0e6d9-179">GitHub의 샘플 디렉터리에는 이러한 명령을 자동으로 실행하는 [PowerShell 스크립트](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="0e6d9-180">PowerShell 창을 열고 디렉터리를 솔루션 디렉터리로 변경한 후 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="0e6d9-181">위의 명령은 이미지를 빌드하고 컴퓨터에 있는 이미지 목록을 표시 하며 컨테이너를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="0e6d9-182">컨테이너를 중지하려면 `docker stop` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="0e6d9-183">컨테이너를 제거하려면 `docker rm` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows 컨테이너로 전환"
[publish-connection]: media/aspnetmvc/PublishConnection.png "파일 시스템에 게시"
[publish-settings]: media/aspnetmvc/PublishSettings.png "게시 설정"
