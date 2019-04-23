---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '실습: SignalR 사용 하 여 실시간 웹 응용 프로그램 | Microsoft Docs'
author: bradygaster
description: 실시간 웹 응용 프로그램 기능을 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠 서버 쪽을 푸시할 수 있습니다. ASP.NET 개발자에 게 ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9904582450d4386ef8b8656078f6d40dbd1e10be
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59412010"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="3e149-104">실습: SignalR을 사용하는 실시간 웹 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="3e149-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>


<span data-ttu-id="3e149-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="3e149-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="3e149-106">웹 캠프 학습 키트, 2015 년 10 월 릴리스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="3e149-107">실시간 웹 응용 프로그램 기능을 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠 서버 쪽을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="3e149-108">ASP.NET 개발자에 게 **ASP.NET SignalR** 응용 프로그램에 실시간 웹 기능을 추가 하려면 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="3e149-109">이 여러 전송, 클라이언트 및 서버의 가장 사용 가능한 전송 가장 사용 가능한 전송 선택 하면 자동으로 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="3e149-110">활용 **WebSocket**, 브라우저와 서버 간의 양방향 통신을 사용 하도록 설정 하는 HTML5 API.</span><span class="sxs-lookup"><span data-stu-id="3e149-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="3e149-111">**SignalR** 클라이언트 RPC 서버 작업을 수행 하는 간단 하 고 상위 수준 API도 제공 (서버 쪽.NET 코드에서 클라이언트의 브라우저에서 JavaScript 함수 호출) 연결 관리에 대 한 유용한 후크 추가 뿐만 아니라 ASP.NET 응용 프로그램 연결/연결 끊기 이벤트, 연결 그룹화 및 권한 부여와 같은</span><span class="sxs-lookup"><span data-stu-id="3e149-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="3e149-112">**SignalR** 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송의 몇 가지 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="3e149-113">A **SignalR** 연결 HTTP로 시작 하 고 다음 수준으로 올린를 **WebSocket** 사용 가능한 경우 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="3e149-114">**WebSocket** 에 대 한 이상적인 전송이 **SignalR**서버 메모리의 가장 효율적으로 사용 하기 때문에, 가장 낮은 대기 시간에이 있고 대부분의 기본 기능 (클라이언트 간의 전이중 통신 등 및 server), 하지만 가장 엄격한 요구 사항이 있습니다. **WebSocket** 서버를 사용 해야 **Windows Server 2012** 하거나 **Windows 8**를 함께 **.NET Framework 4.5**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="3e149-115">이러한 요구 사항을 충족 되지 않는 경우 **SignalR** 와 연결을 확인 하려면 다른 전송을 사용 하려고 합니다 (같은 *긴 폴링 Ajax*).</span><span class="sxs-lookup"><span data-stu-id="3e149-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="3e149-116">합니다 **SignalR** API 클라이언트와 서버 간의 통신을 위한 두 가지 모델을 포함 합니다. **영구 연결** 하 고 **Hubs**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="3e149-117">A **연결** -받는 사람, 단일 그룹화 보내거나 메시지를 브로드캐스트에 대 한 간단한 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="3e149-118">A **허브** 보다 높은 수준의 파이프라인 클라이언트 및 서버에서 서로 다른 메서드를 직접 호출할 수 있도록 연결 API를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="3e149-120">모든 샘플 코드 및 코드 조각 포함 됩니다. 웹 캠프 Training Kit를 2015 년 10 월 릴리스에서에서 사용할 수 있습니다 [ https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b ](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="3e149-121">해당 페이지에서 설치 관리자 링크를 더 이상 작동 하지 않으면를 note 하십시오. 대신 링크 중 하나는 자산 섹션</span><span class="sxs-lookup"><span data-stu-id="3e149-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="3e149-122">개요</span><span class="sxs-lookup"><span data-stu-id="3e149-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3e149-123">목표</span><span class="sxs-lookup"><span data-stu-id="3e149-123">Objectives</span></span>

<span data-ttu-id="3e149-124">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="3e149-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="3e149-125">서버에서 SignalR을 사용 하 여 클라이언트 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="3e149-126">사용 하 여 SignalR 응용 프로그램 확장 **SQL Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3e149-127">전제 조건</span><span class="sxs-lookup"><span data-stu-id="3e149-127">Prerequisites</span></span>

<span data-ttu-id="3e149-128">다음는이 실습을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="3e149-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="3e149-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3e149-130">설정</span><span class="sxs-lookup"><span data-stu-id="3e149-130">Setup</span></span>

<span data-ttu-id="3e149-131">이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="3e149-132">Windows 탐색기 창을 열고 랩의 이동할 **원본** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="3e149-133">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="3e149-134">사용자 계정 컨트롤 대화 상자를 표시 하는 경우 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="3e149-135">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="3e149-136">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="3e149-136">Using the Code Snippets</span></span>

<span data-ttu-id="3e149-137">랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="3e149-138">사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="3e149-139">각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="3e149-140">주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="3e149-141">연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="3e149-142">이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3e149-143">연습</span><span class="sxs-lookup"><span data-stu-id="3e149-143">Exercises</span></span>

<span data-ttu-id="3e149-144">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="3e149-145">SignalR을 사용 하 여 실시간 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="3e149-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="3e149-146">SQL Server를 사용 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="3e149-147">이 랩을 완료 하는 시간을 예상 합니다. **60 분**</span><span class="sxs-lookup"><span data-stu-id="3e149-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="3e149-148">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="3e149-149">미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="3e149-150">이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="3e149-151">개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="3e149-152">연습 1: SignalR을 사용 하 여 실시간 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="3e149-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="3e149-153">예를 들어 채팅 흔히 하는 동안 전체를 수행할 수 있습니다 실시간 웹 기능을 사용 하 여 더 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="3e149-154">사용자를 새 데이터 또는 긴 폴링 새 데이터를 검색 하려면 Ajax 페이지 구현 하는 웹 페이지를 새로 고칩니다. 언제 든 지 SignalR을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="3e149-155">SignalR을 지 원하는 **서버 푸시** 또는 **브로드캐스팅** 기능 연결 관리 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="3e149-156">클라이언트-서버 통신에 대 한 클래식 HTTP 연결에서 각 요청에 대 한 연결이 다시 설정 하지만 SignalR 클라이언트와 서버 간에 영구 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="3e149-157">서버 코드를 원격 프로시저 호출 (RPC)을 사용 하 여 브라우저에서 클라이언트 코드를 호출 하는 signalr에서 요청-응답 모델 대신 알게 지금 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="3e149-158">이 연습에서 구성한 합니다 **Geek 퀴즈** SignalR을 사용 하 여 전체 페이지를 새로 고칠 필요 없이 업데이트 된 메트릭 사용 하 여 통계 대시보드를 표시 하도록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="3e149-159">작업 1-Geek 퀴즈 통계 페이지 탐색</span><span class="sxs-lookup"><span data-stu-id="3e149-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="3e149-160">이 작업에서는 응용 프로그램을 통해 이동 되며 통계 페이지가 어떻게 표시 되는지 확인 하 고 서 정보를 개선 하는 방법을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="3e149-161">엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **GeekQuiz.sln** 솔루션을 **Source\Ex1 WorkingWithRealTimeData\Begin** 폴더.</span><span class="sxs-lookup"><span data-stu-id="3e149-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="3e149-162">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="3e149-163">합니다 **로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="3e149-164">![솔루션을 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="3e149-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="3e149-165">*솔루션 실행*</span><span class="sxs-lookup"><span data-stu-id="3e149-165">*Running the solution*</span></span>
3. <span data-ttu-id="3e149-166">클릭 **등록** 응용 프로그램에서 새 사용자 페이지의 오른쪽 위 모퉁이에서.</span><span class="sxs-lookup"><span data-stu-id="3e149-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="3e149-167">![등록 링크](real-time-web-applications-with-signalr/_static/image3.png "등록 링크")</span><span class="sxs-lookup"><span data-stu-id="3e149-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="3e149-168">*등록 링크*</span><span class="sxs-lookup"><span data-stu-id="3e149-168">*Register link*</span></span>
4. <span data-ttu-id="3e149-169">에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="3e149-170">![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")</span><span class="sxs-lookup"><span data-stu-id="3e149-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="3e149-171">*사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="3e149-171">*Registering a user*</span></span>
5. <span data-ttu-id="3e149-172">응용 프로그램에 새 계정을 등록 하 고 사용자가 인증 하 고 첫 번째 퀴즈 질문을 보여 주는 홈 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="3e149-173">엽니다는 **통계** 넣은 새 창에서 페이지를 **홈** 페이지 및 **통계** side-by-side-페이지.</span><span class="sxs-lookup"><span data-stu-id="3e149-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="3e149-174">![Side-by-side-windows](real-time-web-applications-with-signalr/_static/image5.png "쪽 windows 쪽")</span><span class="sxs-lookup"><span data-stu-id="3e149-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="3e149-175">*Side-by-side-windows*</span><span class="sxs-lookup"><span data-stu-id="3e149-175">*Side-by-side windows*</span></span>
7. <span data-ttu-id="3e149-176">에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="3e149-177">![정보를 파악 하기가](real-time-web-applications-with-signalr/_static/image6.png "질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="3e149-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="3e149-178">*질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="3e149-178">*Answering a question*</span></span>
8. <span data-ttu-id="3e149-179">단추 중 하나를 클릭 한 후 답변 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="3e149-180">![올바른 질문에 대답할](real-time-web-applications-with-signalr/_static/image7.png "올바른 질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="3e149-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="3e149-181">*정확 하 게 대답 하는 질문*</span><span class="sxs-lookup"><span data-stu-id="3e149-181">*Question answered correctly*</span></span>
9. <span data-ttu-id="3e149-182">오래 된 통계 페이지에서 제공 하는 정보 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="3e149-183">업데이트 된 결과 확인 하기 위해 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="3e149-184">![통계 페이지가](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")</span><span class="sxs-lookup"><span data-stu-id="3e149-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="3e149-185">*통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="3e149-185">*Statistics page*</span></span>
10. <span data-ttu-id="3e149-186">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="3e149-187">작업 2-Geek 퀴즈 온라인 차트를 표시 하려면 추가 SignalR</span><span class="sxs-lookup"><span data-stu-id="3e149-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="3e149-188">이 태스크에서는 SignalR 솔루션에 추가 하 고 업데이트를 보내는 클라이언트에 자동으로 새 응답을 서버에 전송 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="3e149-189">**도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="3e149-190">에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="3e149-191">![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="3e149-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="3e149-192">*SignalR 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="3e149-192">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="3e149-193">설치할 때 **SignalR** 수동으로 업데이트 해야 새 MVC 5 응용 프로그램에서 NuGet 패키지 버전 2.0.2를 **OWIN** 버전 2.0.1 패키지 (또는 이상) SignalR을 설치 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="3e149-194">이 작업을 수행 하려면 다음 스크립트를 실행할 수 있습니다 합니다 **패키지 관리자 콘솔**:</span><span class="sxs-lookup"><span data-stu-id="3e149-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="3e149-195">SignalR의 향후 릴리스에서 OWIN 종속성 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="3e149-196">**솔루션 탐색기**를 확장 합니다 **스크립트** 폴더 및 알림은 SignalR *js* 솔루션에 추가 된 파일이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="3e149-197">![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")</span><span class="sxs-lookup"><span data-stu-id="3e149-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="3e149-198">*SignalR JavaScript 참조*</span><span class="sxs-lookup"><span data-stu-id="3e149-198">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="3e149-199">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **GeekQuiz** 프로젝트를 **추가** | **새 폴더**, 이름을 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="3e149-200">마우스 오른쪽 단추로 클릭 합니다 **Hubs** 선택한 폴더 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="3e149-201">![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="3e149-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="3e149-202">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="3e149-202">*Add new item*</span></span>
6. <span data-ttu-id="3e149-203">에 **새 항목 추가** 대화 상자는 **Visual C# | 웹 | SignalR** 의 왼쪽된 창에서 노드 **SignalR 허브 클래스 (v2)** 가운데 창에서 파일 이름을 **StatisticsHub.cs** 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="3e149-204">![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="3e149-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="3e149-205">*새 항목 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="3e149-205">*Add new item dialog box*</span></span>
7. <span data-ttu-id="3e149-206">코드를 대체 합니다 **StatisticsHub** 다음 코드를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="3e149-207">(코드 조각- *RealTimeSignalR-e x 1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="3e149-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="3e149-208">오픈 **Startup.cs** 끝에 다음 줄을 추가 합니다 **구성** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e149-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="3e149-209">(코드 조각- *RealTimeSignalR-e x 1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="3e149-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="3e149-210">열기는 **StatisticsService.cs** 내에서 페이지를 **서비스** 폴더 추가한 다음 지시문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="3e149-211">(코드 조각- *RealTimeSignalR-e x 1-UsingDirectives*)</span><span class="sxs-lookup"><span data-stu-id="3e149-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="3e149-212">업데이트의 연결 된 클라이언트 알림 먼저 검색 한 **상황에 맞는** 현재 연결에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="3e149-213">합니다 **허브** 단일 클라이언트 또는 연결 된 모든 브로드캐스트 클라이언트에 메시지를 보내는 메서드를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="3e149-214">다음 메서드를 추가 합니다 **StatisticsService** 통계 데이터를 브로드캐스트하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="3e149-215">(코드 조각- *RealTimeSignalR-e x 1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="3e149-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="3e149-216">위의 코드에서 클라이언트에서 함수를 호출 하는 임의의 메서드 이름이 사용 중이거나 (예: *updateStatistics*).</span><span class="sxs-lookup"><span data-stu-id="3e149-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="3e149-217">지정 하는 메서드 이름에 대 한 컴파일 시간 유효성 검사 나 IntelliSense 즉 동적 개체로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="3e149-218">식은 런타임에 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="3e149-219">메서드 호출이 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="3e149-220">클라이언트 이름이 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="3e149-221">일치 하는 메서드가 없는 클라이언트에 있으면 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="3e149-222">자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드](../guide-to-the-api/hubs-api-guide-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="3e149-223">열기는 **TriviaController.cs** 내에서 페이지를 **컨트롤러** 폴더 추가한 다음 지시문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="3e149-224">다음 강조 표시 된 코드를 추가 합니다 **Post** 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e149-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="3e149-225">(코드 조각- *RealTimeSignalR-e x 1-NotifyUpdatesCall*)</span><span class="sxs-lookup"><span data-stu-id="3e149-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="3e149-226">엽니다는 **Statistics.cshtml** 내에서 페이지를 **보기 | 홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="3e149-227">찾을 합니다 **스크립트** 섹션 및 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="3e149-228">(코드 조각- *RealTimeSignalR-e x 1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="3e149-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="3e149-229">SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 최신 SignalR 스크립트 파일의 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="3e149-230">코드에서 스크립트 참조를 프로젝트에 설치 스크립트 라이브러리의 버전과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="3e149-231">SignalR 허브에 클라이언트를 연결 하 고 허브에서 새 메시지를 받으면 통계 데이터를 업데이트 하려면 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="3e149-232">(코드 조각- *RealTimeSignalR-e x 1-SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="3e149-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="3e149-233">이 코드에서는 허브 프록시를 만들고 서버에서 보낸 메시지를 수신할 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="3e149-234">이 경우 메시지를 수신 대기를 통해 전송 합니다 *updateStatistics* 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e149-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="3e149-235">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="3e149-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="3e149-236">이 태스크에서는 자동으로 SignalR을 사용 하 여 새로운 질문에 답변 한 후 통계 보기 업데이트 되었는지 확인 하려면 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="3e149-237">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e149-238">아직 응용 프로그램에 로그인 하는 경우 작업 1에서 만든 사용자로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="3e149-239">엽니다는 **통계** 넣은 새 창에서 페이지를 **홈** 페이지 및 **통계** 작업 1에서 수행한 것 처럼 side-by-side-페이지.</span><span class="sxs-lookup"><span data-stu-id="3e149-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="3e149-240">에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="3e149-241">![다른 질문에 답하려면](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 답하려면")</span><span class="sxs-lookup"><span data-stu-id="3e149-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="3e149-242">*다른 질문에 답*</span><span class="sxs-lookup"><span data-stu-id="3e149-242">*Answering another question*</span></span>
4. <span data-ttu-id="3e149-243">단추 중 하나를 클릭 한 후 답변 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="3e149-244">알림 페이지의 통계 정보를 전체 페이지를 새로 고칠 필요 없이 업데이트 된 정보를 사용 하 여 질문에 답변 한 후 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="3e149-245">![응답 한 후 통계 페이지가 새로 고쳐지고](real-time-web-applications-with-signalr/_static/image14.png "응답 후 통계 페이지 새로 고침")</span><span class="sxs-lookup"><span data-stu-id="3e149-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="3e149-246">*응답 한 후 새로 고침된 통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="3e149-246">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="3e149-247">연습 2: SQL Server를 사용 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="3e149-248">웹 응용 프로그램의 크기를 조정할 때 일반적으로 간에 선택할 수 있습니다 *강화* 하 고 *규모* 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="3e149-249">*강화* 하는 동안 더 많은 리소스 (CPU, RAM, 등)를 사용 하 여 더 큰 서버를 사용 하 여 의미 *규모* 로드를 처리 하려면 더 많은 서버를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="3e149-250">후자를 사용 하 여 문제를 다른 서버는 클라이언트 수 라우팅됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="3e149-251">하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="3e149-252">라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 있습니다 *백플레인*, 서버 간에 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="3e149-253">활성화 백 블 레인에를 사용 하 여 각 응용 프로그램 인스턴스가 메시지를 백플레인에 보냅니다 및 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="3e149-254">현재 세 가지 유형의 SignalR에 대 한 백플레인</span><span class="sxs-lookup"><span data-stu-id="3e149-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="3e149-255">**Windows Azure Service Bus**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="3e149-256">Service Bus는 메시징 인프라를 통해 느슨하게 결합 된 메시지를 보내도록 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="3e149-257">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3e149-257">**SQL Server**.</span></span> <span data-ttu-id="3e149-258">SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="3e149-259">백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="3e149-260">그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="3e149-261">**Redis**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-261">**Redis**.</span></span> <span data-ttu-id="3e149-262">Redis는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="3e149-263">Redis는 메시지를 보내기 위한 ("pub/sub") 게시/구독 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="3e149-264">모든 메시지가 메시지 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="3e149-265">메시지 버스 구현 된 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 게시/구독 추상화를 제공 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="3e149-266">기본 대체 하 여 작업의 백플레인 **IMessageBus** 해당 백플레인 위한 버스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="3e149-267">각 서버 인스턴스에 백플레인에서 버스를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="3e149-268">메시지를 보낼 때 백 블 레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="3e149-269">서버 백플레인에서에서 메시지를 받으면 해당 로컬 캐시에서 메시지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="3e149-270">서버는 다음 로컬 캐시에서 클라이언트로 메시지를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="3e149-271">SignalR 백플레인으로 작동 원리,이 대 한 자세한 내용은 [문서](../performance/scaleout-in-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3e149-272">가지를 백플레인으로 병목 현상이 발생할 수 있는 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="3e149-273">몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="3e149-274">[서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 시세 표시기): 백플레인 서버 메시지가 전송 되는 속도 제어 하므로이 시나리오에 대 한 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="3e149-275">[클라이언트-](tutorial-getting-started-with-signalr.md) (채팅 예): 이 시나리오에서는 클라이언트의 수를 사용 하 여 메시지 수가 조정 하는 경우 백플레인에서 병목 지점이 될 수 있습니다. 즉, 메시지의 속도 증가 함에 따라 비례적으로 더 많은 클라이언트 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="3e149-276">[고주파수](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 이 시나리오를 백플레인으로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>


<span data-ttu-id="3e149-277">이 연습에서는 사용할지 **SQL Server** 간에 메시지를 분산 하는 **Geek 퀴즈** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="3e149-278">전체 효과 얻기 위해 있지만 구성을 설정 하는 방법은 단일 테스트 컴퓨터에서 이러한 작업을 실행 하는, 두 개 이상의 서버에 SignalR 응용 프로그램을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="3e149-279">서버 중 하나에서 또는 별도 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![SQL Server 다이어그램을 사용 하 여 확장](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="3e149-281">작업 1-시나리오 이해</span><span class="sxs-lookup"><span data-stu-id="3e149-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="3e149-282">이 태스크에서는 2 인스턴스의 실행될지 **Geek 퀴즈** 로컬 컴퓨터의 인스턴스를 여러 IIS를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="3e149-283">이 시나리오에서는 응용 프로그램에 대 한 기타 정보 질문 하는 경우, 업데이트는 두 번째 인스턴스의 통계 페이지에 알림이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="3e149-284">이 시뮬레이션 유사한 여러 인스턴스에서 응용 프로그램을 배포 하는 위치 environment 부하 분산 장치를 사용 하 여 통신 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="3e149-285">엽니다는 **Begin.sln** 솔루션에는 **소스/e x 2-ScalingOutWithSQLServer/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="3e149-286">로드 되 면에서 알 수 있습니다 합니다 **서버 탐색기** 다른 이름을 구조 솔루션에 동일한 두 개의 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="3e149-287">이에서는 로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스 실행을 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="3e149-288">![Geek 퀴즈의 2 개의 인스턴스를 시뮬레이션 솔루션 시작](real-time-web-applications-with-signalr/_static/image16.png "2 인스턴스의 Geek 퀴즈 시뮬레이션 솔루션 시작")</span><span class="sxs-lookup"><span data-stu-id="3e149-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="3e149-289">*Geek 퀴즈의 2 개의 인스턴스를 시뮬레이션 솔루션 시작*</span><span class="sxs-lookup"><span data-stu-id="3e149-289">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="3e149-290">솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 솔루션의 속성 페이지를 열려면 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="3e149-291">아래 **시작 프로젝트**를 선택 **여러 개의 시작 프로젝트** 변경 하 고는 **작업** 두 프로젝트에 대 한 값 *시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="3e149-292">![여러 프로젝트를 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트 시작")</span><span class="sxs-lookup"><span data-stu-id="3e149-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="3e149-293">*여러 프로젝트 시작*</span><span class="sxs-lookup"><span data-stu-id="3e149-293">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="3e149-294">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="3e149-295">응용 프로그램의 두 인스턴스가 시작 됩니다 **Geek 퀴즈** 서로 다른 포트에서 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="3e149-296">왼쪽 및 오른쪽 화면에 다른 브라우저 중 하나를 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="3e149-297">자격 증명으로 로그인 하거나 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="3e149-298">일단 로그인 하면 왼쪽의 기타 정보 페이지를 유지 하 고로 이동 합니다 **통계** 오른쪽 브라우저의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![Geek 퀴즈 나란히](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="3e149-300">*Geek 퀴즈 나란히*</span><span class="sxs-lookup"><span data-stu-id="3e149-300">*Geek Quiz Side by Side*</span></span>

    ![서로 다른 포트에서 geek 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="3e149-302">*서로 다른 포트에서 geek 퀴즈*</span><span class="sxs-lookup"><span data-stu-id="3e149-302">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="3e149-303">왼쪽된 브라우저에서 질문에 응답을 시작 하 고는 합니다 **통계** 오른쪽 브라우저에서 페이지 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="3e149-304">왜냐하면 **SignalR** 해당 클라이언트에 메시지를 분산 하는 로컬 캐시를 사용 하 여가이 시나리오는 여러 인스턴스를 시뮬레이션 하 고 따라서 캐시 간에 공유 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="3e149-305">중인지 확인할 수 있습니다 **SignalR** 동일한 단계를 테스트 하지만 단일 앱을 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="3e149-306">다음 태스크에서는 인스턴스 간에 메시지를 복제할 백플레인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="3e149-307">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="3e149-308">작업 2-SQL Server 백플레인에서 만들기</span><span class="sxs-lookup"><span data-stu-id="3e149-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="3e149-309">이 작업에서는 데이터베이스에 대 한 백플레인으로 사용할 만들어집니다 합니다 **Geek 퀴즈** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="3e149-310">사용할지 **SQL Server 개체 탐색기** 서버를 찾아보고 데이터베이스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="3e149-311">또한를 사용 하도록 설정한 합니다 **Service Broker**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="3e149-312">**Visual Studio**오픈 메뉴 **뷰** 선택한 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="3e149-313">마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 합니다 **SQL Server** 노드와 선택 **SQL Server 추가...**  옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="3e149-314">![SQL Server 인스턴스를 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="3e149-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="3e149-315">*SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*</span><span class="sxs-lookup"><span data-stu-id="3e149-315">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="3e149-316">설정 합니다 **서버 이름** 하 *(localdb) \v11.0* 두고 **Windows 인증** 을 인증 모드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="3e149-317">클릭 **Connect** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="3e149-318">![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="3e149-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="3e149-319">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="3e149-319">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="3e149-320">LocalDB 인스턴스를 연결한 했으므로 나타내는 SQL Server 백플레인에서 SignalR에 대 한 데이터베이스를 만들려고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="3e149-321">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드와 선택 **새 데이터베이스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="3e149-322">![새 데이터베이스 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스 추가")</span><span class="sxs-lookup"><span data-stu-id="3e149-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="3e149-323">*새 데이터베이스 추가*</span><span class="sxs-lookup"><span data-stu-id="3e149-323">*Adding a new database*</span></span>
5. <span data-ttu-id="3e149-324">데이터베이스 이름으로 설정 *SignalR* 클릭 **확인** 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="3e149-325">![SignalR 데이터베이스를 만드는](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스 만들기")</span><span class="sxs-lookup"><span data-stu-id="3e149-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="3e149-326">*SignalR 데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="3e149-326">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e149-327">데이터베이스의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="3e149-328">백플레인에서 보다 효율적으로 업데이트를 받으려면, 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="3e149-329">Service Broker는 메시징 및 SQL Server의 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="3e149-330">백플레인에서는 Service Broker 없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="3e149-331">선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여 새 쿼리를 엽니다 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="3e149-332">![새 쿼리를 열어](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")</span><span class="sxs-lookup"><span data-stu-id="3e149-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="3e149-333">*새 쿼리 열기*</span><span class="sxs-lookup"><span data-stu-id="3e149-333">*Opening a New Query*</span></span>
7. <span data-ttu-id="3e149-334">Service Broker 사용 되는지 여부를 확인, 쿼리를 **은\_broker\_사용 하도록 설정** 열에는 **sys.databases** 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="3e149-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="3e149-335">최근에 열린된 쿼리 창에서 다음 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="3e149-336">![Service Broker 상태를 쿼리할](real-time-web-applications-with-signalr/_static/image25.png "서비스 Broker 상태를 쿼리 합니다.")</span><span class="sxs-lookup"><span data-stu-id="3e149-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="3e149-337">*Service Broker 상태를 쿼리합니다.*</span><span class="sxs-lookup"><span data-stu-id="3e149-337">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="3e149-338">경우 값을 **은\_broker\_사용 하도록 설정** 데이터베이스의 열은 &quot;0&quot;, 사용 하도록 설정 하려면 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="3e149-339">바꿉니다 **&lt;YOUR DATABASE&gt;** 데이터베이스를 만들 때 설정한 이름 (예: SignalR)입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="3e149-340">![Service Broker를 사용 하도록 설정](real-time-web-applications-with-signalr/_static/image26.png "Service Broker를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="3e149-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="3e149-341">*Service Broker를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="3e149-341">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e149-342">교착 상태가 발생 했는지를이 쿼리가 나타납니다 경우 DB에 연결 하는 응용 프로그램이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="3e149-343">작업 3 – SignalR 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="3e149-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="3e149-344">이 작업에서 구성한 **Geek 퀴즈** SQL Server 백플레인에서 연결할 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="3e149-345">먼저 추가 합니다 **SignalR.SqlServer** 백플레인 데이터베이스에 NuGet 패키지 및 연결 집합 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="3e149-346">엽니다는 **패키지 관리자 콘솔** 에서 **도구** > **NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="3e149-347">했는지 **GeekQuiz** 에서 프로젝트를 선택 합니다 **기본 프로젝트** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="3e149-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="3e149-348">설치 하려면 다음 명령을 입력 합니다 **Microsoft.AspNet.SignalR.SqlServer** NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="3e149-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="3e149-349">프로젝트에 대해 이전 단계 이번 반복 **GeekQuiz2**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="3e149-350">구성 하려면 SQL Server 백플레인에서 엽니다는 **Startup.cs** 파일의는 **GeekQuiz** 프로젝트 및 다음 코드를 추가 합니다 **구성** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e149-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="3e149-351">바꿉니다 **&lt;YOUR DATABASE&gt;** SQL Server 백플레인에서 만들 때 사용한 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="3e149-352">이 단계를 반복 합니다 **GeekQuiz2** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="3e149-353">(코드 조각- *RealTimeSignalR-e x 2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="3e149-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="3e149-354">키를 눌러 두 프로젝트는 SQL Server 백플레인에서 사용 하도록 구성 된, 했으므로 **F5** 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="3e149-355">마찬가지로 **Visual Studio** 의 두 인스턴스가 시작 됩니다 **매니아 퀴즈** 서로 다른 포트에서.</span><span class="sxs-lookup"><span data-stu-id="3e149-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="3e149-356">왼쪽 및 오른쪽 화면에 다른 브라우저 중 하나를 고정 하 고 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="3e149-357">왼쪽의 기타 정보 페이지를 유지 하 고 이동할 **통계** pagein 오른쪽 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="3e149-358">왼쪽된 브라우저에서 질문을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="3e149-359">이 이번에는 **통계** 백플레인에서 덕분에 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="3e149-360">응용 프로그램 간 전환 (**통계** 왼쪽에 이제 및 **퀴즈** 오른쪽에 표시 됩니다) 인스턴스 모두에 대해 작동 하는지 유효성을 검사 하려면 테스트를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="3e149-361">백플레인에서 역할도 *캐시 공유* 연결 된 클라이언트에 배포 하는 자체 로컬 캐시에서 메시지 저장은 각 연결 된 서버 및 각 서버에 대 한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="3e149-362">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="3e149-363">SQL Server 백플레인 구성 요소는 자동으로 지정된 된 데이터베이스에 필요한 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="3e149-364">에 **SQL Server 개체 탐색기** 패널에서 백플레인에서 대해 만든 데이터베이스를 엽니다 (예: SignalR) 해당 테이블을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="3e149-365">다음 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-365">You should see the following tables:</span></span>

    ![백플레인에서 테이블 생성](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="3e149-367">*백플레인에서 테이블 생성*</span><span class="sxs-lookup"><span data-stu-id="3e149-367">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="3e149-368">마우스 오른쪽 단추로 클릭 합니다 **SignalR.Messages\_0** 선택한 테이블 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![SignalR 백플레인으로 메시지 테이블 보기](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="3e149-370">*SignalR 백플레인으로 메시지 테이블 보기*</span><span class="sxs-lookup"><span data-stu-id="3e149-370">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="3e149-371">전송할 다양 한 메시지를 볼 수는 **허브** 퀴즈 질문에 답변 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3e149-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="3e149-372">백플레인에서 연결 인스턴스에 이러한 메시지를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-372">The backplane distributes these messages to any connected instance.</span></span>

    ![백플레인에서 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="3e149-374">*백플레인에서 메시지 테이블*</span><span class="sxs-lookup"><span data-stu-id="3e149-374">*Backplane Messages Table*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3e149-375">요약</span><span class="sxs-lookup"><span data-stu-id="3e149-375">Summary</span></span>

<span data-ttu-id="3e149-376">이 실습에서는 추가 하는 방법을 익 혔 **SignalR** 사용 하 여 연결 된 클라이언트에 서버에서 응용 프로그램 및 송신 알림에 **Hubs**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="3e149-377">사용 하 여 응용 프로그램을 확장 하는 방법과 또한을 *백플레인* 여러 IIS 인스턴스에 응용 프로그램을 배포할 때 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e149-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
