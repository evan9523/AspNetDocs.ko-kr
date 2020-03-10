---
uid: signalr/overview/performance/scaleout-with-redis
title: SignalR 확장 with Redis | Microsoft Docs
author: bradygaster
description: 이전 버전의에 대 한 자세한 내용은이 항목에서 사용 된 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR 버전 2 이전 버전의 항목을 참조 하세요.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467777"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="31234-103">Redis로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="31234-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="31234-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="31234-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="31234-105">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="31234-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="31234-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="31234-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="31234-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="31234-107">.NET 4.5</span></span>
> - <span data-ttu-id="31234-108">SignalR 버전 2.4</span><span class="sxs-lookup"><span data-stu-id="31234-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="31234-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="31234-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="31234-110">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="31234-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="31234-111">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="31234-111">Questions and comments</span></span>
>
> <span data-ttu-id="31234-112">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="31234-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="31234-113">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="31234-114">이 자습서에서는 [Redis](http://redis.io/) 를 사용 하 여 별도의 두 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 통해 메시지를 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="31234-115">Redis는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="31234-116">또한 게시/구독 모델을 사용 하는 메시징 시스템을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="31234-117">SignalR Redis 후면판은 pub/sub 기능을 사용 하 여 메시지를 다른 서버로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="31234-118">이 자습서에서는 다음 3 개의 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="31234-119">SignalR 응용 프로그램을 배포 하는 데 사용할 Windows를 실행 하는 두 대의 서버</span><span class="sxs-lookup"><span data-stu-id="31234-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="31234-120">Redis를 실행 하는 데 사용할 Linux를 실행 하는 하나의 서버.</span><span class="sxs-lookup"><span data-stu-id="31234-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="31234-121">이 자습서의 스크린샷에서는 Ubuntu 12.04 TLS를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="31234-122">사용할 물리적 서버가 세 대 이상 없는 경우 Hyper-v에서 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="31234-123">또 다른 옵션은 Azure에서 Vm을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="31234-124">이 자습서에서는 공식 Redis 구현을 사용 하지만 MSOpenTech에서 [Redis의 Windows 포트](https://github.com/MSOpenTech/redis) 도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="31234-125">설정 및 구성은 서로 다르지만 단계는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="31234-126">SignalR 확장 with Redis는 Redis 클러스터를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="31234-127">개요</span><span class="sxs-lookup"><span data-stu-id="31234-127">Overview</span></span>

<span data-ttu-id="31234-128">자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="31234-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="31234-129">Redis를 설치 하 고 Redis 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="31234-130">응용 프로그램에 다음 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="31234-131">SignalR</span><span class="sxs-lookup"><span data-stu-id="31234-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="31234-132">SignalR. StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="31234-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="31234-133">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31234-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="31234-134">Startup.cs에 다음 코드를 추가 하 여 후면판을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="31234-135">Hyper-v의 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="31234-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="31234-136">Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="31234-137">[http://www.ubuntu.com](http://www.ubuntu.com/)에서 Ubuntu ISO를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="31234-138">Hyper-v에서 새 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="31234-139">**가상 하드 디스크 연결** 단계에서 **가상 하드 디스크 만들기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="31234-140">**설치 옵션** 단계에서 **이미지 파일 (.iso)** 을 선택 하 고 **찾아보기**를 클릭 한 다음 Ubuntu 설치 iso로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="31234-141">Redis 설치</span><span class="sxs-lookup"><span data-stu-id="31234-141">Install Redis</span></span>

<span data-ttu-id="31234-142">[http://redis.io/download](http://redis.io/download) 의 단계에 따라 Redis를 다운로드 하 고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="31234-143">그러면 `src` 디렉터리에 Redis 바이너리가 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="31234-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="31234-144">기본적으로 Redis에는 암호가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="31234-145">암호를 설정 하려면 소스 코드의 루트 디렉터리에 있는 `redis.conf` 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="31234-146">편집 하기 전에 파일의 백업 복사본을 만듭니다. `redis.conf`에 다음 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="31234-147">이제 Redis 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="31234-148">Redis에서 수신 대기 하는 기본 포트인 포트 6379를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31234-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="31234-149">구성 파일에서 포트 번호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="31234-150">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="31234-150">Create the SignalR Application</span></span>

<span data-ttu-id="31234-151">다음 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31234-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="31234-152">SignalR 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="31234-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="31234-153">SignalR 2.0 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="31234-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="31234-154">다음으로, Redis와의 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="31234-155">먼저 `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="31234-156">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="31234-157">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="31234-158">그런 다음 Startup.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31234-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="31234-159">**구성** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="31234-160">"server"는 Redis를 실행 하는 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="31234-161">*포트* 는 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-161">*port* is the port number</span></span>
- <span data-ttu-id="31234-162">"password"는 redis 파일에서 정의한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="31234-163">"AppName"은 임의의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-163">"AppName" is any string.</span></span> <span data-ttu-id="31234-164">SignalR는이 이름을 사용 하 여 Redis pub/sub 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31234-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="31234-165">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="31234-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="31234-166">응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="31234-166">Deploy and Run the Application</span></span>

<span data-ttu-id="31234-167">Windows Server 인스턴스를 준비 하 여 SignalR 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="31234-168">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-168">Add the IIS role.</span></span> <span data-ttu-id="31234-169">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="31234-170">관리 서비스 ("관리 도구" 아래에 나열 됨)도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="31234-171">**웹 배포 3.0을 설치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="31234-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="31234-172">IIS 관리자를 실행 하는 경우 Microsoft 웹 플랫폼을 설치 하 라는 메시지가 표시 되거나 [설치 관리자를 다운로드할](https://go.microsoft.com/fwlink/?LinkId=255386)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="31234-173">플랫폼 설치 관리자에서 웹 배포을 검색 하 고 웹 배포 3.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="31234-174">웹 관리 서비스가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="31234-175">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-175">If not, start the service.</span></span> <span data-ttu-id="31234-176">Windows 서비스 목록에 웹 관리 서비스가 표시 되지 않으면 IIS 역할을 추가할 때 관리 서비스를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="31234-177">기본적으로 웹 관리 서비스는 TCP 포트 8172에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="31234-178">Windows 방화벽에서 포트 8172에 TCP 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31234-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="31234-179">자세한 내용은 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="31234-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="31234-180">(Azure에서 Vm을 호스트 하는 경우 Azure Portal에서 직접 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="31234-181">[가상 컴퓨터에 대 한 끝점을 설정 하는 방법을](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="31234-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="31234-182">이제 개발 컴퓨터의 Visual Studio 프로젝트를 서버에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="31234-183">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="31234-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="31234-184">웹 배포에 대 한 자세한 설명서는 [Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="31234-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="31234-185">두 개의 서버에 응용 프로그램을 배포 하는 경우 별도의 브라우저 창에서 각 인스턴스를 열 수 있으며 각 인스턴스는 서로 SignalR 메시지를 수신 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="31234-186">물론 프로덕션 환경에서는 두 서버가 부하 분산 장치 뒤에 앉아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="31234-187">Redis로 전송 되는 메시지를 확인 하는 방법에 대 한 자세한 내용은 Redis와 함께 설치 되는 **Redis cli** 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31234-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
