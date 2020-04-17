---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Windows 인증(C#)으로 사용자 인증 | 마이크로 소프트 문서
author: rick-anderson
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법에 대해 알아봅니다. 응용 프로그램의 웹 에서 Windows 인증을 사용 하는 방법을 알아봅니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540742"
---
# <a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="62fd7-104">Windows 인증으로 사용자 인증(C#)</span><span class="sxs-lookup"><span data-stu-id="62fd7-104">Authenticating Users with Windows Authentication (C#)</span></span>

<span data-ttu-id="62fd7-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="62fd7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="62fd7-106">MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="62fd7-107">응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용하도록 설정하는 방법과 IIS를 사용하여 인증을 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="62fd7-108">마지막으로 [권한 부여] 특성을 사용하여 특정 Windows 사용자 또는 그룹에 대한 컨트롤러 작업에 대한 액세스를 제한하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="62fd7-109">이 자습서의 목표는 인터넷 정보 서비스에 내장된 보안 기능을 활용하여 MVC 응용 프로그램의 보기를 암호로 보호하는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="62fd7-110">컨트롤러 작업을 특정 Windows 사용자 또는 특정 Windows 그룹의 구성원인 사용자만 호출하도록 허용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="62fd7-111">Windows 인증을 사용하는 것은 내부 회사 웹 사이트(인트라넷 사이트)를 구축하고 사용자가 웹 사이트에 액세스할 때 표준 Windows 사용자 이름과 암호를 사용할 수 있도록 하려는 경우에 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="62fd7-112">바깥쪽을 향한 웹 사이트(인터넷 웹 사이트)를 빌드하는 경우 폼 인증을 대신 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="62fd7-113">Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="62fd7-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="62fd7-114">새 ASP.NET MVC 응용 프로그램을 만들 때 Windows 인증은 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="62fd7-115">양식 인증은 MVC 응용 프로그램에 대해 사용할 수 있는 기본 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="62fd7-116">MVC 응용 프로그램의 웹 구성(web.config) 파일을 수정하여 Windows 인증을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="62fd7-117">&lt;다음과 같이&gt; 인증 섹션을 찾아 서폼 인증 대신 Windows를 사용하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="62fd7-118">Windows 인증을 사용하도록 설정하면 웹 서버에서 사용자 인증에 대한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="62fd7-119">일반적으로 ASP.NET MVC 응용 프로그램을 만들고 배포할 때 사용하는 웹 서버유형에는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="62fd7-120">먼저 MVC 응용 프로그램을 개발하는 동안 Visual Studio에 포함된 ASP.NET 개발 웹 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="62fd7-121">기본적으로 ASP.NET 개발 웹 서버는 현재 Windows 계정의 컨텍스트에서 모든 페이지를 실행합니다(Windows에 로그인하는 데 사용한 계정).</span><span class="sxs-lookup"><span data-stu-id="62fd7-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="62fd7-122">ASP.NET 개발 웹 서버는 NTLM 인증도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="62fd7-123">솔루션 탐색기 창에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택하여 NTLM 인증을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="62fd7-124">그런 다음 웹 탭을 선택하고 NTLM 확인란을 선택합니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="62fd7-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="62fd7-125">**그림 1 – ASP.NET 개발 웹 서버에 대한 NTLM 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="62fd7-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="62fd7-127">프로덕션 웹 응용 프로그램의 경우 IIS를 웹 서버로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="62fd7-128">IIS는 다음과 같은 여러 유형의 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="62fd7-129">기본 인증 - HTTP 1.0 프로토콜의 일부로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="62fd7-130">사용자 이름과 암호를 인터넷을 통해 일반 텍스트(Base64 인코딩)로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="62fd7-131">- 다이제스트 인증 - 인터넷을 통해 암호 자체 대신 암호 해시를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="62fd7-132">- 통합 윈도우 (NTLM) 인증 - 창을 사용하여 인트라넷 환경에서 사용하는 인증의 가장 좋은 유형.</span><span class="sxs-lookup"><span data-stu-id="62fd7-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="62fd7-133">- 인증서 인증 - 클라이언트 측 인증서를 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="62fd7-134">인증서는 Windows 사용자 계정에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="62fd7-135">이러한 다양한 유형의 인증에 대한 자세한 [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)개요는 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="62fd7-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="62fd7-136">인터넷 정보 서비스 관리자를 사용하여 특정 유형의 인증을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="62fd7-137">모든 운영 체제의 경우 모든 유형의 인증을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="62fd7-138">또한 Windows Vista에서 IIS 7.0을 사용하는 경우 인터넷 정보 서비스 관리자에 나타나기 전에 다양한 유형의 Windows 인증을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="62fd7-139">**제어판, 프로그램, 프로그램 및 기능을 열고 Windows 기능을 켜거나 끄고**인터넷 정보 서비스 노드를 확장합니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="62fd7-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="62fd7-140">**그림 2 – Windows IIS 기능 활성화**</span><span class="sxs-lookup"><span data-stu-id="62fd7-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="62fd7-142">인터넷 정보 서비스를 사용하면 다양한 유형의 인증을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="62fd7-143">예를 들어 그림 3에서는 IIS 7.0을 사용할 때 익명 인증을 사용하지 않도록 설정하고 NTLM(통합 Windows) 인증을 사용하도록 설정하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="62fd7-144">**그림 3 – 통합 윈도우 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="62fd7-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="62fd7-146">Windows 사용자 및 그룹 권한 부여</span><span class="sxs-lookup"><span data-stu-id="62fd7-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="62fd7-147">Windows 인증을 사용하도록 설정하면 [권한 부여] 특성을 사용하여 컨트롤러 또는 컨트롤러 작업에 대한 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="62fd7-148">이 특성은 전체 MVC 컨트롤러 또는 특정 컨트롤러 작업에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="62fd7-149">예를 들어 목록 1의 홈 컨트롤러는 Index(), CompanySecrets() 및 StephenSecrets()라는 세 가지 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="62fd7-150">누구나 Index() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="62fd7-151">그러나 Windows 로컬 관리자 그룹의 구성원만 CompanySecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="62fd7-152">마지막으로, Redmond 도메인에서 Stephen이라는 Windows 도메인 사용자만 StephenSecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="62fd7-153">**목록 1 – 컨트롤러\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="62fd7-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="62fd7-154">UAC(Windows 사용자 계정 제어)로 인해 Windows Vista 또는 Windows Server 2008로 작업할 때 로컬 관리자 그룹은 다른 그룹과 다르게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="62fd7-155">컴퓨터의 UAC 설정을 수정하지 않으면 [권한 부여] 특성이 로컬 관리자 그룹의 구성원을 올바르게 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="62fd7-156">올바른 사용 권한이 없는 컨트롤러 작업을 호출하려고 할 때 정확히 발생하는 작업은 사용 가능한 인증 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="62fd7-157">기본적으로 ASP.NET 개발 서버를 사용할 때빈 페이지만 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="62fd7-158">이 페이지는 **401 승인되지 않은** HTTP 응답 상태와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="62fd7-159">반면에 익명 인증을 사용하지 않도록 설정하고 기본 인증을 사용하도록 설정한 경우 보호된 페이지를 요청할 때마다 로그인 대화 상자 메시지가 계속 표시됩니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="62fd7-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="62fd7-160">**그림 4 - 기본 인증 로그인 대화 상자**</span><span class="sxs-lookup"><span data-stu-id="62fd7-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="62fd7-162">요약</span><span class="sxs-lookup"><span data-stu-id="62fd7-162">Summary</span></span>

<span data-ttu-id="62fd7-163">이 자습서에서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="62fd7-164">응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용하도록 설정하는 방법과 IIS를 사용하여 인증을 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="62fd7-165">마지막으로 [권한 부여] 특성을 사용하여 특정 Windows 사용자 또는 그룹에 대한 컨트롤러 작업에 대한 액세스를 제한하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd7-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62fd7-166">[이전](authenticating-users-with-forms-authentication-cs.md)
> [다음](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="62fd7-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>
