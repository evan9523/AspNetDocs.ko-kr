---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: '자습서: SignalR 1.x 시작 하기 | Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR를 사용 하 여 HTML 페이지에서 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505751"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="dc8db-103">자습서: SignalR 1.x 시작</span><span class="sxs-lookup"><span data-stu-id="dc8db-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="dc8db-104">[Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="dc8db-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="dc8db-105">이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="dc8db-106">빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="dc8db-107">개요</span><span class="sxs-lookup"><span data-stu-id="dc8db-107">Overview</span></span>

<span data-ttu-id="dc8db-108">이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 SignalR 개발을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="dc8db-109">빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리를 추가 하 고, 클라이언트에 메시지를 보내기 위한 허브 클래스를 만들고, 사용자가 채팅 메시지를 보내고 받을 수 있도록 하는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="dc8db-110">Mvc 뷰를 사용 하 여 MVC 4에서 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서는 [SignalR 및 MVC 4 시작](index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dc8db-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dc8db-111">이 자습서에서는 릴리스 (1.x) 버전의 SignalR를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="dc8db-112">SignalR 1.x와 2.0 간의 변경 내용에 대 한 자세한 내용은 [SignalR 1.X 프로젝트 업그레이드](../releases/upgrading-signalr-1x-projects-to-20.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dc8db-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="dc8db-113">SignalR는 라이브 사용자 상호 작용 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램을 빌드하기 위한 오픈 소스 .NET 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="dc8db-114">예를 들면 소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업, 뉴스, 날씨 또는 재무 업데이트 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="dc8db-115">이러한 응용 프로그램은 종종 실시간 응용 프로그램 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-115">These are often called real-time applications.</span></span>

<span data-ttu-id="dc8db-116">SignalR는 실시간 응용 프로그램을 빌드하는 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="dc8db-117">여기에는 클라이언트-서버 연결을 보다 쉽게 관리 하 고 클라이언트에 콘텐츠 업데이트를 푸시할 수 있도록 하는 ASP.NET 서버 라이브러리와 JavaScript 클라이언트 라이브러리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="dc8db-118">SignalR 라이브러리를 기존 ASP.NET 응용 프로그램에 추가 하 여 실시간 기능을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="dc8db-119">이 자습서에서는 다음과 같은 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="dc8db-120">ASP.NET 웹 응용 프로그램에 SignalR 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="dc8db-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="dc8db-121">클라이언트에 콘텐츠를 푸시하는 허브 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="dc8db-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="dc8db-122">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="dc8db-123">다음 스크린샷은 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="dc8db-124">각 새 사용자는 메모를 게시 하 고 사용자가 채팅에 가입한 후 추가 된 주석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="dc8db-126">섹션이</span><span class="sxs-lookup"><span data-stu-id="dc8db-126">Sections:</span></span>

- [<span data-ttu-id="dc8db-127">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="dc8db-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="dc8db-128">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="dc8db-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="dc8db-129">코드 검사</span><span class="sxs-lookup"><span data-stu-id="dc8db-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="dc8db-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc8db-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="dc8db-131">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="dc8db-131">Set up the Project</span></span>

<span data-ttu-id="dc8db-132">이 섹션에서는 빈 ASP.NET 웹 응용 프로그램을 만들고, SignalR를 추가 하 고, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="dc8db-133">필수 조건:</span><span class="sxs-lookup"><span data-stu-id="dc8db-133">Prerequisites:</span></span>

- <span data-ttu-id="dc8db-134">Visual Studio 2010 SP1 또는 2012.</span><span class="sxs-lookup"><span data-stu-id="dc8db-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="dc8db-135">Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 를 참조 하 여 무료 visual Studio 2012 Express 개발 도구를 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="dc8db-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="dc8db-136">[Microsoft ASP.NET 및 Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span><span class="sxs-lookup"><span data-stu-id="dc8db-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="dc8db-137">Visual Studio 2012의 경우이 설치 관리자는 SignalR 템플릿을 포함 한 새 ASP.NET 기능을 Visual Studio에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="dc8db-138">Visual Studio 2010 s p 1의 경우 설치 관리자를 사용할 수 없지만 설치 단계에 설명 된 대로 SignalR NuGet 패키지를 설치 하 여 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="dc8db-139">다음 단계에서는 Visual Studio 2012을 사용 하 여 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 라이브러리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="dc8db-140">Visual Studio에서 ASP.NET 빈 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="dc8db-142">도구 |를 선택 하 여 **패키지 관리자 콘솔** 을 엽니다.  **NuGet 패키지 관리자 | 패키지 관리자 콘솔**.</span><span class="sxs-lookup"><span data-stu-id="dc8db-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="dc8db-143">콘솔 창에 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="dc8db-144">이 명령은 SignalR 1.x의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="dc8db-145">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스**.</span><span class="sxs-lookup"><span data-stu-id="dc8db-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="dc8db-146">새 클래스의 이름을 **ChatHub**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="dc8db-147">**솔루션 탐색기** 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="dc8db-148">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![라이브러리 참조](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="dc8db-150">**ChatHub** 클래스의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="dc8db-151">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="dc8db-152">**새 항목 추가** 대화 상자에서 **전역 응용 프로그램 클래스** 를 선택 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![전역 추가](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="dc8db-154">Global.asax.cs 클래스에서 제공 된 `using` 문 뒤에 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="dc8db-155">SignalR hubs의 기본 경로를 등록 하려면 전역 클래스의 `Application_Start` 메서드에 다음 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="dc8db-156">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="dc8db-157">**새 항목 추가** 대화 상자에서 Html 페이지를 선택 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="dc8db-158">**솔루션 탐색기**에서 방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="dc8db-159">HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="dc8db-160">프로젝트에 대 한 **모든를 저장** 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="dc8db-161">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="dc8db-161">Run the Sample</span></span>

1. <span data-ttu-id="dc8db-162">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="dc8db-163">HTML 페이지가 브라우저 인스턴스에 로드 되 고 사용자 이름을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="dc8db-165">사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-165">Enter a user name.</span></span>
3. <span data-ttu-id="dc8db-166">브라우저의 주소 줄에서 URL을 복사 하 고이를 사용 하 여 두 개의 브라우저 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="dc8db-167">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="dc8db-168">각 브라우저 인스턴스에서 주석을 추가 하 고 **보내기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="dc8db-169">주석은 모든 브라우저 인스턴스에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc8db-170">이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="dc8db-171">허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="dc8db-172">나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="dc8db-173">다음 스크린샷에서는 세 개의 브라우저 인스턴스에서 실행 되는 채팅 응용 프로그램을 보여 주며,이는 모두 한 인스턴스가 메시지를 보낼 때 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="dc8db-175">**솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="dc8db-176">SignalR 라이브러리가 런타임에 동적으로 생성 하는 **허브** 라는 스크립트 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="dc8db-177">이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="dc8db-179">코드 검사</span><span class="sxs-lookup"><span data-stu-id="dc8db-179">Examine the Code</span></span>

<span data-ttu-id="dc8db-180">SignalR chat 응용 프로그램은 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="dc8db-181">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="dc8db-181">SignalR Hubs</span></span>

<span data-ttu-id="dc8db-182">코드 샘플에서 **ChatHub** 클래스는 **SignalR** 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="dc8db-183">**허브** 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="dc8db-184">허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 jQuery 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="dc8db-185">채팅 코드에서 클라이언트는 **ChatHub** 메서드를 호출 하 여 새 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="dc8db-186">그러면 허브는 **broadcastMessage**를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="dc8db-187">**Send** 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="dc8db-188">클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="dc8db-189">**SignalR** 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="dc8db-190">클라이언트 (예: `broadcastMessage` 함수)에서 jQuery 함수를 호출 하 여 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="dc8db-191">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="dc8db-191">SignalR and jQuery</span></span>

<span data-ttu-id="dc8db-192">코드 샘플의 HTML 페이지에서는 SignalR jQuery 라이브러리를 사용 하 여 SignalR hub와 통신 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="dc8db-193">코드의 필수 작업은 허브를 참조 하도록 프록시를 선언 하 고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="dc8db-194">다음 코드는 허브에 대 한 프록시를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="dc8db-195">JQuery에서 서버 클래스 및 해당 멤버에 대 한 참조는 카멜식 대/소문자로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="dc8db-196">코드 샘플은 jQuery의 C# **ChatHub** 클래스를 **ChatHub**로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="dc8db-197">다음 코드는 스크립트에서 콜백 함수를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="dc8db-198">서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="dc8db-199">콘텐츠를 표시 하기 전에 HTML로 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="dc8db-200">다음 코드에서는 허브와의 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="dc8db-201">이 코드는 연결을 시작한 다음 HTML 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="dc8db-202">이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="dc8db-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc8db-203">Next Steps</span></span>

<span data-ttu-id="dc8db-204">SignalR는 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="dc8db-205">또한 ASP.NET 응용 프로그램에 SignalR를 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 보내고 받는 방법에 대 한 몇 가지 SignalR 개발 작업을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="dc8db-206">이 자습서의 샘플 응용 프로그램 또는 인터넷을 통해 사용할 수 있는 다른 SignalR 응용 프로그램을 호스팅 공급자에 게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="dc8db-207">Microsoft는 무료 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)에 최대 10 개의 웹 사이트를 위한 무료 웹 호스팅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="dc8db-208">샘플 SignalR 응용 프로그램을 배포 하는 방법에 대 한 연습은 [Windows Azure 웹 사이트로 SignalR 시작 샘플 게시](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc8db-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="dc8db-209">Microsoft Azure 웹 사이트에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [Windows Azure 웹 사이트에 ASP.NET 응용 프로그램 배포](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc8db-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="dc8db-210">(참고: WebSocket 전송은 현재 Windows Azure 웹 사이트에 대해 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="dc8db-211">WebSocket 전송을 사용할 수 없는 경우 SignalR는 [SignalR 소개 항목](index.md)의 전송 섹션에 설명 된 대로 사용 가능한 다른 전송을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8db-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="dc8db-212">고급 SignalR 개발 개념에 대 한 자세한 내용은 다음 사이트에서 SignalR 소스 코드 및 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dc8db-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="dc8db-213">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="dc8db-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="dc8db-214">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="dc8db-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="dc8db-215">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="dc8db-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
