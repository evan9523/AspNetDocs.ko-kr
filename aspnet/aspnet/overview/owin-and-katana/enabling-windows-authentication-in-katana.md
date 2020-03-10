---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana에서 Windows 인증 사용 | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 보여 줍니다. IIS를 사용 하 여 Katana를 호스트 하 고 HttpListener를 사용 하 여 자체 호스트 하는 두 가지 시나리오를 다룹니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500297"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="acb1d-104">Katana에서 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="acb1d-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="acb1d-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="acb1d-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="acb1d-106">이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="acb1d-107">IIS를 사용 하 여 Katana를 호스트 하 고 HttpListener를 사용 하 여 사용자 지정 프로세스에서 Katana를 호스트 하는 두 가지 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="acb1d-108">Barry Dorrans, David Matson 및 Chris Ross 덕분에이 문서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="acb1d-109">Katana는 .NET 용 개방형 웹 인터페이스인 [OWIN](http://owin.org/)의 Microsoft 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="acb1d-110">[여기](an-overview-of-project-katana.md)에서 OWIN 및 Katana에 대 한 소개를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="acb1d-111">OWIN 아키텍처에는 다음과 같은 여러 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="acb1d-112">Host: OWIN 파이프라인이 실행 되는 프로세스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="acb1d-113">서버: 네트워크 소켓을 열고 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="acb1d-114">미들웨어: HTTP 요청 및 응답을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="acb1d-115">Katana는 현재 두 개의 서버를 제공 하며, 두 서버 모두 Windows 통합 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="acb1d-116">**Owin 웹**입니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="acb1d-117">ASP.NET 파이프라인에서 IIS를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="acb1d-118">**Owin. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="acb1d-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="acb1d-119">[시스템 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="acb1d-120">이 서버는 현재 자체 호스팅 Katana 때 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="acb1d-121">현재 서버에서이 기능을 사용할 수 있기 때문에 Katana는 현재 Windows 인증용 OWIN 미들웨어를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="acb1d-122">IIS의 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="acb1d-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="acb1d-123">Owin를 사용 하 여 IIS에서 Windows 인증을 사용 하도록 설정 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="acb1d-124">먼저 "ASP.NET Empty 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 새 ASP.NET 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="acb1d-125">다음으로 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-125">Next, add NuGet packages.</span></span> <span data-ttu-id="acb1d-126">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="acb1d-127">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="acb1d-128">이제 다음 코드를 사용 하 여 `Startup` 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="acb1d-129">이것은 IIS에서 실행 되는 OWIN에 대 한 "Hello 세계" 응용 프로그램을 만드는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="acb1d-130">F5 키를 눌러 애플리케이션을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-130">Press F5 to debug the application.</span></span> <span data-ttu-id="acb1d-131">콘솔에 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="acb1d-131">You should see "Hello World!"</span></span> <span data-ttu-id="acb1d-132">브라우저 창에서</span><span class="sxs-lookup"><span data-stu-id="acb1d-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="acb1d-133">다음으로 IIS Express에서 Windows 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="acb1d-134">**보기** 메뉴에서 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="acb1d-135">프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="acb1d-136">**속성** 창에서 **익명 인증** 을 **사용 안 함** 으로 설정 하 고 **Windows 인증** 을 **사용**으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="acb1d-137">Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express 사용자의 Windows 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="acb1d-138">[Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구를 사용 하 여이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="acb1d-139">HTTP 응답 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="acb1d-140">이 응답의 WWW-인증 헤더는 서버에서 Kerberos 또는 NTLM을 사용 하는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 프로토콜을 지원함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="acb1d-141">나중에 응용 프로그램을 서버에 배포 하는 경우 [다음 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 에 따라 해당 서버의 IIS에서 Windows 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="acb1d-142">HttpListener의 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="acb1d-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="acb1d-143">Owin를 사용 하 여 Katana를 자체 호스트 하는 경우 **HttpListener** 인스턴스에서 직접 Windows 인증을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="acb1d-144">먼저 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-144">First, create a new console application.</span></span> <span data-ttu-id="acb1d-145">다음으로 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-145">Next, add NuGet packages.</span></span> <span data-ttu-id="acb1d-146">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="acb1d-147">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="acb1d-148">이제 다음 코드를 사용 하 여 `Startup` 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="acb1d-149">이 클래스는 이전에서와 동일한 "Hello 세계" 예제를 구현 하지만 인증 체계로도 Windows 인증을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="acb1d-150">`Main` 함수 내에서 OWIN 파이프라인을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="acb1d-151">Fiddler에서 요청을 보내 응용 프로그램이 Windows 인증을 사용 하 고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb1d-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="acb1d-152">관련 항목</span><span class="sxs-lookup"><span data-stu-id="acb1d-152">Related Topics</span></span>

[<span data-ttu-id="acb1d-153">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="acb1d-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="acb1d-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="acb1d-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="acb1d-155">MVC 5에서 OWIN 폼 인증 이해</span><span class="sxs-lookup"><span data-stu-id="acb1d-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
