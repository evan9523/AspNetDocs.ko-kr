---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: '자습서: SignalR 자체 호스트 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 자체 호스트 된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트를 사용 하 여이 서버에 연결 하는 방법을 보여 줍니다. 자습서 V에서 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450167"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="10c45-104">자습서: SignalR 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="10c45-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="10c45-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="10c45-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="10c45-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="10c45-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="10c45-107">이 자습서에서는 자체 호스트 된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트를 사용 하 여이 서버에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="10c45-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="10c45-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="10c45-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="10c45-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="10c45-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="10c45-110">.NET 4.5</span></span>
> - <span data-ttu-id="10c45-111">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="10c45-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="10c45-112">이 자습서에서는 Visual Studio 2012 사용</span><span class="sxs-lookup"><span data-stu-id="10c45-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="10c45-113">이 자습서에서 Visual Studio 2012을 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="10c45-114">[패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="10c45-115">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="10c45-116">웹 플랫폼 설치 관리자에서 **Visual Studio 2012 용 ASP.NET 및 Web Tools 2013.1**를 검색 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="10c45-117">그러면 **허브**와 같은 SignalR 클래스에 대 한 Visual Studio 템플릿이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="10c45-118">일부 템플릿 (예: **OWIN 시작 클래스**)은 사용할 수 없습니다. 이러한 경우 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="10c45-119">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="10c45-119">Questions and comments</span></span>
>
> <span data-ttu-id="10c45-120">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="10c45-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="10c45-121">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="10c45-122">개요</span><span class="sxs-lookup"><span data-stu-id="10c45-122">Overview</span></span>

<span data-ttu-id="10c45-123">SignalR 서버는 일반적으로 IIS의 ASP.NET 응용 프로그램에서 호스트 되지만 자체 호스트 (예: 콘솔 응용 프로그램 또는 Windows 서비스)는 자체 호스트 라이브러리를 사용 하 여 호스트 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="10c45-124">SignalR 2와 같은이 라이브러리는 OWIN ([Open Web Interface for .net](http://owin.org))를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="10c45-125">OWIN는 .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="10c45-126">OWIN는 서버에서 웹 응용 프로그램을 분리 IIS 외부의 자체 프로세스에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="10c45-127">IIS에서를 호스팅하지 않는 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="10c45-128">Iis가 없는 기존 서버 팜과 같이 IIS를 사용할 수 없거나 바람직하지 않은 환경</span><span class="sxs-lookup"><span data-stu-id="10c45-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="10c45-129">IIS의 성능 오버 헤드를 방지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="10c45-130">SignalR 기능은 Windows 서비스, Azure 작업자 역할 또는 다른 프로세스에서 실행 되는 기존 응용 프로그램에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="10c45-131">성능상의 이유로 자체 호스트로 솔루션을 개발 하는 경우에는 IIS에서 호스트 되는 응용 프로그램을 테스트 하 여 성능상의 이점을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="10c45-132">이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="10c45-133">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="10c45-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="10c45-134">JavaScript 클라이언트를 사용 하 여 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="10c45-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="10c45-135">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="10c45-135">Creating the server</span></span>

<span data-ttu-id="10c45-136">이 자습서에서는 콘솔 응용 프로그램에서 호스트 되는 서버를 만들지만 Windows 서비스 또는 Azure 작업자 역할과 같은 모든 종류의 프로세스에서 서버를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="10c45-137">Windows 서비스에서 SignalR 서버를 호스트 하는 샘플 코드는 [Windows 서비스의 자체 호스팅 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10c45-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="10c45-138">관리자 권한으로 Visual Studio 2013를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="10c45-139">**파일**, **새 프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="10c45-140">**템플릿** 창의 **시각적 C#**  노드에서 **창** 을 선택 하 고 **콘솔 응용 프로그램** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="10c45-141">새 프로젝트의 이름을 "SignalRSelfHost"로 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="10c45-142">**도구** > **nuget** 패키지 관리자 > **패키지 관리자 콘솔**을 선택 하 여 nuget 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="10c45-143">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="10c45-144">이 명령은 SignalR 2 자체 호스트 라이브러리를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="10c45-145">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="10c45-146">이 명령은 Owin 라이브러리를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="10c45-147">이 라이브러리는 SignalR를 호스트 하는 응용 프로그램 및 다른 도메인의 웹 페이지 클라이언트에 필요한 도메인 간 지원에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="10c45-148">SignalR 서버와 웹 클라이언트를 서로 다른 포트에 호스트할 것 이므로 이러한 구성 요소 간 통신을 위해 도메인 간 사용을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="10c45-149">Program.cs 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="10c45-150">위의 코드는 세 가지 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="10c45-151">기본 실행 경로를 정의 하는 **Main** 메서드를 포함 하는 **프로그램**입니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="10c45-152">이 메서드에서 **Startup** 유형의 웹 응용 프로그램은 지정 된 URL (`http://localhost:8080`)에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="10c45-153">끝점에 보안을 설정 해야 하는 경우 SSL을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="10c45-154">자세한 내용은 [방법: SSL 인증서로 포트 구성](https://msdn.microsoft.com/library/ms733791.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10c45-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="10c45-155">**시작**, SignalR 서버에 대 한 구성 (이 자습서에서는 `UseCors`에 대 한 호출)을 포함 하는 클래스는 프로젝트의 모든 허브 개체에 대 한 경로를 만드는 `MapSignalR`에 대 한 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="10c45-156">**Myhub**-응용 프로그램이 클라이언트에 제공 하는 SignalR hub 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="10c45-157">이 클래스에는 클라이언트에서 연결 된 다른 모든 클라이언트에 메시지를 브로드캐스트하는를 호출 하는 단일 메서드인 **Send**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="10c45-158">애플리케이션을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-158">Compile and run the application.</span></span> <span data-ttu-id="10c45-159">서버에서 실행 중인 주소가 콘솔 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="10c45-160">`System.Reflection.TargetInvocationException was unhandled`예외로 인해 실행이 실패 하면 관리자 권한으로 Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="10c45-161">다음 섹션으로 진행 하기 전에 응용 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="10c45-162">JavaScript 클라이언트를 사용 하 여 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="10c45-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="10c45-163">이 섹션에서는 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 동일한 JavaScript 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="10c45-164">클라이언트에 대해 한 번만 수정 하면 됩니다 .이는 허브 URL을 명시적으로 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="10c45-165">자체 호스팅 응용 프로그램을 사용 하는 경우 서버는 역방향 프록시와 부하 분산 장치 때문에 연결 URL과 동일한 주소에 있을 수 없으므로 URL을 명시적으로 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="10c45-166">**솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="10c45-167">**웹** 노드를 선택 하 고 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="10c45-168">프로젝트 이름을 "JavascriptClient"로 선택 하 고 **확인을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="10c45-169">**빈** 템플릿을 선택 하 고 나머지 옵션은 선택 하지 않은 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="10c45-170">**프로젝트 만들기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="10c45-171">패키지 관리자 콘솔의 **기본 프로젝트** 드롭다운에서 "JavascriptClient" 프로젝트를 선택 하 고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="10c45-172">이 명령은 클라이언트에 필요한 SignalR 및 JQuery 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="10c45-173">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="10c45-174">**웹** 노드를 선택 하 고 HTML 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="10c45-175">페이지의 이름을 **default.aspx**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="10c45-176">새 HTML 페이지의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="10c45-177">여기에서 스크립트 참조가 프로젝트의 Scripts 폴더에 있는 스크립트와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="10c45-178">위의 코드 샘플에 강조 표시 된 다음 코드는 시작 자습서에서 사용 되는 클라이언트에 대 한 추가 작업 (코드를 SignalR 버전 2 베타로 업그레이드 하는 것 외에)입니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="10c45-179">이 코드 줄은 서버에서 SignalR에 대 한 기본 연결 URL을 명시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="10c45-180">솔루션을 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트 설정**...을 선택 합니다. **여러 개의 시작 프로젝트** 라디오 단추를 선택 하 고 두 프로젝트의 **작업** 을 **시작**으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="10c45-181">"Default .html"을 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="10c45-182">애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-182">Run the application.</span></span> <span data-ttu-id="10c45-183">서버와 페이지가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-183">The server and page will launch.</span></span> <span data-ttu-id="10c45-184">서버를 시작 하기 전에 페이지를 로드 하는 경우 웹 페이지를 다시 로드 하거나 디버거에서 **계속** 을 선택 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="10c45-185">브라우저에서 메시지가 표시 되 면 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="10c45-186">페이지의 URL을 다른 브라우저 탭 또는 창에 복사 하 고 다른 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="10c45-187">시작 자습서에서와 같이 브라우저 창 간에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10c45-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
