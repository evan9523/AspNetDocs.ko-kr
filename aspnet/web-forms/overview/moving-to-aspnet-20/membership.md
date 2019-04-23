---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 멤버 자격 | Microsoft Docs
author: microsoft
description: ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다. ASP.NET 폼 인증 incorp 하는 편리한 방법을 제공 하는 중...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: f3f8c649932682fd96e0640ddf4595c19c755909
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408188"
---
# <a name="membership"></a><span data-ttu-id="6d038-104">멤버 자격입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-104">Membership</span></span>

<span data-ttu-id="6d038-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6d038-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6d038-106">ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="6d038-107">ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 여 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>


<span data-ttu-id="6d038-108">ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="6d038-109">ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 여 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="6d038-110">FormsAuthentication 클래스의 멤버 수 있도록 인증에 대 한 쿠키를 처리, 유효한 로그인에 대 한 확인, 등으로 사용자를 로그 합니다. 그러나 ASP.NET 1.x 응용 프로그램에서 폼 인증을 구현 하면 많은 양의 코드가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="6d038-111">ASP.NET 2.0의 멤버 자격만 폼 인증을 사용 하 여 주요 advancement 경우</span><span class="sxs-lookup"><span data-stu-id="6d038-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="6d038-112">(멤버는 폼 인증을 함께 사용 하면 가장 강력한 있지만 폼 인증을 사용 하 여 필요 하지 않습니다.) 곧 보게 되겠지만 사용할 수 있습니다 ASP.NET 멤버 자격 및 로그인 컨트롤 ASP.NET 2.0의 많은 코드를 전혀 작성 하지 않고도 강력한 멤버 자격 시스템을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="6d038-113">ASP.NET 2.0의에서 멤버 자격 구현</span><span class="sxs-lookup"><span data-stu-id="6d038-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="6d038-114">멤버 자격 네 단계를 수행 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="6d038-115">도 구현할 수 있는 선택적 구성 뿐만 아니라 관련 된 여러 하위 단계는 것을 염두에 두십시오.</span><span class="sxs-lookup"><span data-stu-id="6d038-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="6d038-116">멤버 자격을 구성 하는 상황을 큰 그림을 보여 주기 위해 다음이 단계는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="6d038-117">멤버 자격 데이터베이스 만들기 (SQL Server 멤버 자격 저장소로 사용 됩니다.) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="6d038-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="6d038-118">응용 프로그램 구성 파일에서 멤버 자격 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="6d038-119">(멤버 자격 기본으로 사용 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="6d038-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="6d038-120">사용 하려는 멤버 자격이 저장소 유형을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="6d038-121">옵션은</span><span class="sxs-lookup"><span data-stu-id="6d038-121">Options are:</span></span> 

    - <span data-ttu-id="6d038-122">Microsoft SQL Server (버전 7.0 이상)</span><span class="sxs-lookup"><span data-stu-id="6d038-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="6d038-123">Active Directory Store</span><span class="sxs-lookup"><span data-stu-id="6d038-123">Active Directory Store</span></span>
    - <span data-ttu-id="6d038-124">사용자 지정 멤버 자격 공급자</span><span class="sxs-lookup"><span data-stu-id="6d038-124">Custom membership provider</span></span>
4. <span data-ttu-id="6d038-125">ASP.NET 폼 인증을 위해 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="6d038-126">이번에 멤버 자격 폼 인증을 활용 하기 위해 설계 되어 있지만 폼 인증을 사용 하 여 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="6d038-127">멤버 자격에 대 한 사용자 계정을 정의 하 고 필요한 경우 역할을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="6d038-128">멤버 자격 데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="6d038-128">Creating the Membership Database</span></span>

<span data-ttu-id="6d038-129">SQL Server 7.0을 사용 하는 경우 aspnet을 나중에 멤버 자격이 저장소로 사용할 수\_regsql 유틸리티 (사용 가능한 가장 쉽게 Visual Studio.NET 2005 명령 프롬프트에서) 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-129">If you're using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="6d038-130">Aspnet\_regsql 유틸리티 명령 프롬프트 도구 또는 GUI 마법사를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="6d038-131">마법사 방법은 데이터베이스를 구성 하는 가장 쉬운 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="6d038-132">마법사에 액세스 하려면 다음 명령을 실행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="6d038-133">해당 명령으로 실행 되 면 아래와 같이 ASP.NET SQL Server 설치 마법사를 사용 하 여 표시 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>


![](membership/_static/image1.jpg)

<span data-ttu-id="6d038-134">**그림 1**</span><span class="sxs-lookup"><span data-stu-id="6d038-134">**Figure 1**</span></span>


<span data-ttu-id="6d038-135">ASP.NET SQL Server 설치 마법사는 마법사에서 지정한 인스턴스에서 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="6d038-136">그러나 ASP.NET은 machine.config 파일에 데이터베이스에 연결할 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="6d038-137">기본적으로이 연결 문자열은 SQL Server 2005 인스턴스를 가리키게 됩니다 있도록 SQL Server 2000 또는 SQL Server 7.0 인스턴스를 사용 하는 경우 machine.config 파일의 연결 문자열을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="6d038-138">다음 연결 문자열 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="6d038-139">그러나 연결 문자열을 수정 하지 ASP.NET 제공 되지 않습니다 오류를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-139">Unfortunately, if you don't modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="6d038-140">방금 라는 데이터베이스를 만들지 불만을 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-140">It will just continue to complain saying that you haven't created the database.</span></span> <span data-ttu-id="6d038-141">위의 예에서 내 로컬 SQL Server 2000 인스턴스를 가리키도록 연결 문자열을 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="6d038-142">지정 하 여 구성 하 고 추가 사용자 및 역할</span><span class="sxs-lookup"><span data-stu-id="6d038-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="6d038-143">멤버 자격 구성의 다음 단계에서는 응용 프로그램의 web.config 파일에 필요한 정보를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="6d038-144">Asp.net에서 1.x에서 web.config 파일 수정 어려웠습니다 때로는 lowerCamelCase 사용 및 Intellisense의 부족으로 인해.</span><span class="sxs-lookup"><span data-stu-id="6d038-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="6d038-145">Visual Studio.NET 2005 작업 구성 파일에 Intellisense를 사용 하 여 훨씬 더 쉽게 하지만 ASP.NET 2.0 구성 파일 편집에 대 한 웹 인터페이스를 제공 하 여 한 단계 더 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="6d038-146">솔루션 탐색기 도구 모음 아래와 같이 ASP.NET 구성 단추를 클릭 하 여 웹 인터페이스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="6d038-147">또한 로그인 컨트롤을 삽입할 때 표시 되는 팝업을 통해 웹 인터페이스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>


![](membership/_static/image2.jpg)

<span data-ttu-id="6d038-148">**그림 2**</span><span class="sxs-lookup"><span data-stu-id="6d038-148">**Figure 2**</span></span>


<span data-ttu-id="6d038-149">그러면 아래에 표시 된 ASP.NET 웹 사이트 관리 도구를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="6d038-150">ASP.NET 웹 사이트 관리에는 손쉽게 응용 프로그램 설정을 관리할 수 있는 4 개의 탭 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="6d038-151">다음 탭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-151">The following tabs are available:</span></span>

- <span data-ttu-id="6d038-152">**Home**</span><span class="sxs-lookup"><span data-stu-id="6d038-152">**Home**</span></span>
- <span data-ttu-id="6d038-153">**보안** 사용자, 역할 및 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="6d038-154">**응용 프로그램** 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="6d038-155">**공급자** 구성 하 고 응용 프로그램 멤버 자격 공급자를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="6d038-156">웹 사이트 관리 도구를 사용 하면 사용자 및 역할 관리를 간편 하 게 새 사용자 만들기, 새 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="6d038-157">이 기능은 사용할 수 없는 경우 Windows 인터페이스에서</span><span class="sxs-lookup"><span data-stu-id="6d038-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="6d038-158">Windows 인터페이스를 사용 하면 권한 부여 설정을 쉽게 정의할 수 및 추가, 삭제 및 공급자, 웹 사이트 관리 도구에 없는 기능을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="6d038-159">Windows 인터페이스를 시작 하려면 인터넷 정보 서비스 스냅인을 열고 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다. 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="6d038-160">ASP.NET 탭을 클릭 하 고 구성 편집 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="6d038-161">(응용 프로그램을 사용할 구성 편집 단추에 대 한 ASP.NET 2.0에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="6d038-162">물론 ASP.NET 대화 상자에서 ASP.NET 버전을 구성할 수 있습니다) ASP.NET 구성 설정 대화 상자는 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>


![](membership/_static/image3.jpg)

<span data-ttu-id="6d038-163">**그림 3**</span><span class="sxs-lookup"><span data-stu-id="6d038-163">**Figure 3**</span></span>


<span data-ttu-id="6d038-164">일반 탭의 연결 문자열 및 응용 프로그램 설정을 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="6d038-165">기울임꼴로 표시 설정을 상위 구성 파일 (machine.config 또는 높은 수준에서 web.config)에 정의 된 및 기울임꼴에 없는 설정은 응용 프로그램 구성 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="6d038-166">설정이 추가 된 경우 제거 되거나 응용 프로그램 수준에서 편집 ASP.NET은 추가, 제거 또는 상속 된 구성 파일에서 설정을 제거 하는 대신 응용 프로그램 수준 web.config에서 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="6d038-167">인증 탭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="6d038-168">이 멤버 자격 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="6d038-169">인증 설정, 멤버 자격 공급자를 구성 하 고 역할 공급자를 여기서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>


![](membership/_static/image4.jpg)

<span data-ttu-id="6d038-170">**그림 4**</span><span class="sxs-lookup"><span data-stu-id="6d038-170">**Figure 4**</span></span>


## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="6d038-171">멤버 자격 응용 프로그램에서 구현</span><span class="sxs-lookup"><span data-stu-id="6d038-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="6d038-172">응용 프로그램에서 ASP.NET 2.0 멤버 자격을 구현 하는 가장 쉬운 방법은 제공 된 로그온 컨트롤을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="6d038-173">이 메서드를 사용 하면 모든 코드를 전혀 작성 하지 않고도 ASP.NET 2.0 멤버 자격의 기본 사항을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="6d038-174">다음 로그온 컨트롤은 ASP.NET 2.0에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="6d038-175">로그인 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-175">Login Control</span></span>

<span data-ttu-id="6d038-176">Login 컨트롤 멤버 자격 시스템에 로그인 할 사용자 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="6d038-177">사용자 이름 및 암호 텍스트 상자와 로그인 단추를 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-177">It provides you with a username and password textbox and a login button.</span></span> <span data-ttu-id="6d038-178">권한이 있는 사용자에 대 한 등록에 대 한 링크와 같은 기타 일반적인 여러 기능 수행 되므로 확인란을 허용 하는 자동으로 로그인 하면 후속 아직 방문 등 암호 힌트에 대 한 링크입니다. Login 컨트롤의 모든 기능을 컨트롤의 속성을 통해 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="6d038-179">Asp.net에서 1.x에서 개발자는 상당한 양의 폼 인증을 사용 하는 경우 조회를 수행 하는 코드를 작성 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="6d038-180">ASP.NET 2.0 멤버 자격을 사용 하 여 코드를 전혀 작성 하지 않고 사용자를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="6d038-181">ASP.NET는 수에 자동으로 사용자의 조회를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="6d038-182">(ASP.NET 멤버 자격을 사용 하지 않고 로그인 컨트롤을 사용 중인 경우 사용할 수 있습니다 합니다 **OnAuthenticate** 사용자의 유효성을 검사 하는 방법입니다.)</span><span class="sxs-lookup"><span data-stu-id="6d038-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="6d038-183">LoginView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-183">LoginView Control</span></span>

<span data-ttu-id="6d038-184">LoginView 컨트롤은 기본적으로 두 개의 템플릿이 제공 하는 템플릿 기반 컨트롤 AnonymousTemplate 및 LoggedInTemplate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="6d038-185">표시 되는 템플릿은 사용자가 멤버 자격 시스템에 로그인 여부 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="6d038-186">이 컨트롤은 사용자가 로그인 하는 경우 사용자가 아직 로그인 하지 않은 경우 로그인 컨트롤 및 LoginStatus 컨트롤 및/또는 다른 로그인 컨트롤을 표시 하려면 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="6d038-187">역할 관리를 ASP.NET 응용 프로그램에서 사용 하는 경우 사용자 역할에 따라 특정 템플릿을 LoginView 컨트롤에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="6d038-188">(더 asp.net 역할 관리 다룰 나중.)</span><span class="sxs-lookup"><span data-stu-id="6d038-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="6d038-189">PasswordRecovery 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-189">PasswordRecovery Control</span></span>

<span data-ttu-id="6d038-190">PasswordRecovery 컨트롤을 사용 하면 자신의 현재 암호를 사용 하 여 전자 메일을 받거나 자신의 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="6d038-191">일반 텍스트 및 암호화 된 암호 복구 하 고 사용자에 게 메일로 전송 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="6d038-192">해시 된 암호는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="6d038-193">대신 사용자 암호 재설정을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="6d038-194">LoginStatus 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-194">LoginStatus Control</span></span>

<span data-ttu-id="6d038-195">LoginStatus 컨트롤에는 현재 로그인 한 사용자에 게 로그인 하지 않은 사용자는 로그인 표시기 및 로그 아웃 표시기 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="6d038-196">Request.IsAuthenticated 속성을 표시 하는 표시기를 확인 하려면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="6d038-197">LoginStatus 컨트롤에서 표시 하는 표시기 텍스트일 수 있습니다 (를 통해 구현 된 **LoginText** 및 **LogoutText** 속성) 또는 이미지 (통해 구현를 **LoginImageUrl**하 고 **LogoutImageUrl** 속성입니다.)</span><span class="sxs-lookup"><span data-stu-id="6d038-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="6d038-198">자신이 지정 된 URL로 리디렉션되면 사용자가 LoginStatus 컨트롤을 통해 로그 아웃할 때 합니다 **LogoutPageUrl** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="6d038-199">해당 속성을 설정 하지 않으면 하는 경우 현재 페이지 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="6d038-200">사이트는 Forms 인증으로 보호 가능성이 있으므로 현재 페이지의 새로 고침이 사이트에 대 한 로그인 페이지로 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="6d038-201">LoginName 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-201">LoginName Control</span></span>

<span data-ttu-id="6d038-202">LoginName 컨트롤 사이트에 현재 로그인 한 사용자의 사용자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="6d038-203">CreateUserWizard 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-203">CreateUserWizard Control</span></span>

<span data-ttu-id="6d038-204">CreateUserWizard 컨트롤은 멤버 자격 시스템에 등록 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="6d038-205">아래에 표시 된 인터페이스를 통해 (WizardSteps 컬렉션으로 구현 됨) 하는 단계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>


![](membership/_static/image5.jpg)

<span data-ttu-id="6d038-206">**그림 5**</span><span class="sxs-lookup"><span data-stu-id="6d038-206">**Figure 5**</span></span>


<span data-ttu-id="6d038-207">CreateUserWizard는 마법사 클래스에서 파생 되 고 다음 템플릿을 제공 하는 템플릿 기반 컨트롤은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="6d038-208">**머리글 템플릿의** 이 템플릿 마법사의 헤더의 모양을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="6d038-209">**SidebarTemplate** 이 템플릿 마법사의 세로 막대의 모양을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="6d038-210">**StartNavigationTemplate** 탐색의 모양을 시작 단계에서 마법사는이 템플릿 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="6d038-211">**StepNavigationTemplate** 이 템플릿은 시작 또는 완료 단계에 없는 경우 탐색 영역의 모양을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="6d038-212">**FinishNavigationTemplate** 이 서식 파일 마침 단계에서 작업 하는 경우 탐색 영역의 모양을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="6d038-213">또한 마법사에 추가한 각 단계에서는 ASP.NET을 ContentTemplate 및 해당 단계에 대 한 CustomNavigationTemplate 모두 포함 하는 사용자 지정 템플릿을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="6d038-214">CreateUserWizard 사용자 지정에 대 한 전체 내용은 VS.NET 2005 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d038-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="6d038-215">ChangePassword 컨트롤</span><span class="sxs-lookup"><span data-stu-id="6d038-215">ChangePassword Control</span></span>

<span data-ttu-id="6d038-216">ChangePassword 컨트롤에는 사용자를 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="6d038-217">DisplayUserName 속성 (기본적으로 false 임) true 인 경우에 기록 되지 않습니다 하는 경우 사용자가 자신의 암호를 변경할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="6d038-218">하는 경우 사용자 *는* 이미 로그인 DisplayUserName 속성이 true를 사용자가 해당 사용자의 사용자 ID를 알고 있는 제공 로그인 하지 않은 다른 사용자의 암호를 변경 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="6d038-219">사용자가 로그인 하지 않고도 암호를 변경할 수 있도록 원한다 면 해야 ChangePassword 컨트롤 표시 되는 페이지 익명 액세스를 허용 하는지 확인 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="6d038-220">물론 사용자가 자신의 암호를 변경 하기 위해 이전 암호를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="6d038-221">역할 관리</span><span class="sxs-lookup"><span data-stu-id="6d038-221">Role Management</span></span>

<span data-ttu-id="6d038-222">역할 관리를 사용 하면 특정 역할에 사용자를 할당 하 고 한 특정 파일 또는 폴더는 역할 기반 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="6d038-223">역할 관리는 또한 프로그래밍 방식으로 someones 역할 확인 또는 특정 역할에는 모든 사용자를 적절 하 게 대응할 수 있도록 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="6d038-224">역할 관리 ASP.NET 멤버 자격에 필요 하지 않은 멤버 자격 역할 관리를 사용 하려면 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="6d038-225">그러나 두 원활 하 게 서로 보완 하며는 개발자는 함께 사용할 서로 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="6d038-226">응용 프로그램에서 역할 관리를 사용 하려면 web.config 파일에 다음 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="6d038-227">경우는 **cacheRolesInCookie** 특성이로 설정 된 물론 ASP.NET 캐시 클라이언트의 쿠키에 사용자 역할 멤버 자격.</span><span class="sxs-lookup"><span data-stu-id="6d038-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="6d038-228">이 역할 공급자를 호출 하지 않고 역할 조회 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="6d038-229">개발자는 되도록 하려면이 특성을 사용 하는 경우는 **cookieProtection** 특성 All로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="6d038-230">(기본 설정입니다.) 이렇게 하면 쿠키 데이터를 암호화 된 쿠키 내용을 변경 하지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents haven't been altered.</span></span> <span data-ttu-id="6d038-231">웹 사이트 관리 도구를 사용 하 여 역할을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="6d038-232">쉽게 역할 정의 해당 역할에 기반 하 여 사이트의 부분에 대 한 액세스를 구성 하 고 역할에 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>


![](membership/_static/image6.jpg)

<span data-ttu-id="6d038-233">**그림 6**</span><span class="sxs-lookup"><span data-stu-id="6d038-233">**Figure 6**</span></span>


<span data-ttu-id="6d038-234">위와 같이 역할의 이름을 입력 하는 것 다음 역할 추가 클릭 하 여 새 역할을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="6d038-235">기존 역할을 관리 하거나 기존 역할 목록에서 적절 한 링크를 클릭 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="6d038-236">역할을 관리 하는 경우에 추가 하거나 아래와 같이 사용자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-236">When you manage a role, you can add or remove users as shown below.</span></span>


![](membership/_static/image7.jpg)

<span data-ttu-id="6d038-237">**그림 7**</span><span class="sxs-lookup"><span data-stu-id="6d038-237">**Figure 7**</span></span>


<span data-ttu-id="6d038-238">확인란 역할에 사용자를 특정 역할에 사용자를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="6d038-239">ASP.NET에 적절 한 항목을 사용 하 여 멤버 자격 데이터베이스를 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="6d038-240">응용 프로그램에 대 한 액세스 규칙을 구성 하려고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="6d038-241">ASP.NET 1.x 개발자가이 통해 작업을 수행 합니다 &lt;권한 부여&gt; web.config 파일에서 해당 옵션에는 요소는 ASP.NET 2.0에서 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="6d038-242">그러나 것 액세스를 관리 하는 것이 더 쉬워졌습니다 규칙은 웹 사이트 관리 도구 표시 된 것 처럼 다음을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>


![](membership/_static/image8.jpg)

<span data-ttu-id="6d038-243">**그림 8**</span><span class="sxs-lookup"><span data-stu-id="6d038-243">**Figure 8**</span></span>


<span data-ttu-id="6d038-244">이 경우 관리 폴더 강조 표시 됩니다 (해당 고급 도구 밝은 회색으로 강조 표시 되므로 보려는) 및 관리자 역할에 액세스할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="6d038-245">다른 모든 사용자는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-245">All other users are denied.</span></span> <span data-ttu-id="6d038-246">규칙을 선택한 다음 위로 및 아래로 이동 단추를 사용 하 여 규칙을 정렬 하려면 헤드 아이콘을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="6d038-247">ASP.NET과 마찬가지로 &lt;권한 부여&gt; 요소 규칙은 나타나는 순서 대로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="6d038-248">즉, 위의 샷에 규칙의 순서 반전 된 경우 되므로 ASP.NET 발생 하 게 하는 첫 번째 규칙 폴더에 모든 사용자를 거부 하는 규칙 관리 폴더에 액세스할을 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="6d038-249">ASP.NET 2.0는 액세스 규칙을 지정 하는 폴더에 web.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="6d038-250">구성 파일 또는 웹 사이트 관리 도구를 통해 액세스 규칙을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="6d038-251">즉, 웹 사이트 관리 도구는 인터페이스는 구성 파일 친숙 한 환경에서 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="6d038-252">코드에서 역할 사용</span><span class="sxs-lookup"><span data-stu-id="6d038-252">Using Roles in Code</span></span>

<span data-ttu-id="6d038-253">역할 관리에 대 한 API 버전 이후 변경 되지 않은 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="6d038-254">**IsInRole** 메서드는 하는 데 사용자가 특정 역할에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="6d038-255">또한 ASP.NET 현재 컨텍스트의 멤버로 파트너가 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="6d038-256">파트너가 개체는 사용자가 속한 역할을 다음과 같이 모든를 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="6d038-257">RoleGroups LoginView 컨트롤 사용</span><span class="sxs-lookup"><span data-stu-id="6d038-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="6d038-258">멤버 자격 및 역할 관리 이해 했으므로 통해 LoginView 컨트롤은 ASP.NET 2.0에서이 기능을 사용 하는 방법을 간략하게 설명 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="6d038-259">앞에서 설명한 대로 LoginView 컨트롤은 기본적으로 두 개의 템플릿이 포함 된 템플릿 기반 컨트롤 AnonymousTemplate 및 LoggedInTemplate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="6d038-260">내 LoginView 대화 상자는 아래와 같이 링크는 작업 RoleGroups 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>


![](membership/_static/image9.jpg)

<span data-ttu-id="6d038-261">**그림 9**</span><span class="sxs-lookup"><span data-stu-id="6d038-261">**Figure 9**</span></span>


<span data-ttu-id="6d038-262">각 RoleGroup 개체 RoleGroup 적용 되는 역할을 정의 하는 문자열의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="6d038-263">새 RoleGroup LoginView 컨트롤에 추가 하려면 RoleGroups 편집 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="6d038-264">위의 이미지에서 추가한 것 관리자에 대 한 새 RoleGroup 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="6d038-265">해당 RoleGroup를 선택 하 여 (RoleGroup[0]) 뷰 드롭다운 목록에서 있습니까 템플릿을 구성할 수만 관리자 역할의 멤버에 게 표시 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="6d038-266">아래 이미지에서는 Sales 역할 및 배포 역할의 멤버에 적용 되는 새 RoleGroup 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="6d038-267">두 번째 RoleGroup LoginView 작업 대화 상자에서 뷰 드롭다운 목록에 추가 하 고 해당 템플릿을 추가할 모든 판매 또는 배포의 모든 사용자가 볼 수 있습니다 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>


![](membership/_static/image10.jpg)

<span data-ttu-id="6d038-268">**그림 10**</span><span class="sxs-lookup"><span data-stu-id="6d038-268">**Figure 10**</span></span>


## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="6d038-269">기존 멤버 자격 공급자를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="6d038-270">ASP.NET 멤버 자격의 기능을 확장 하는 방법의 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="6d038-271">먼저,에서 상속 하 고 해당 메서드를 재정의 하 여 SqlMembershipProvider 클래스의 기존 기능을 확실히 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="6d038-272">예를 들어, 사용자를 만들 때 고유한 기능을 구현 하려는 경우에 다음과 같이 SqlMembershipProvider에서 상속 되는 고유한 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="6d038-273">공급자 (예를 들어 Access 데이터베이스에 멤버 자격 정보를 저장)를 직접 만들려면 하려는 다른 한편으로, 경우에 고유한 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="6d038-274">직접 멤버 자격 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="6d038-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="6d038-275">직접 멤버 자격 공급자를 만들려면 먼저 해야 MembershipProvider 클래스에서 상속 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="6d038-276">VB.NET를 사용 하는 경우 Visual Studio 2005는 모든 메서드를 재정의 해야 하는 한 스텁이 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="6d038-277">C#에서는 해당 최대 스텁이 추가할 수 있습니다 사용 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="6d038-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="6d038-278">다음 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-278">You will need to override the following:</span></span>

- <span data-ttu-id="6d038-279">ApplicationName 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-279">ApplicationName property</span></span>
- <span data-ttu-id="6d038-280">ChangePassword 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-280">ChangePassword function</span></span>
- <span data-ttu-id="6d038-281">ChangePasswordQuestionAndAnswer 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="6d038-282">CreateUser 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-282">CreateUser function</span></span>
- <span data-ttu-id="6d038-283">DeleteUser 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-283">DeleteUser function</span></span>
- <span data-ttu-id="6d038-284">EnablePasswordReset 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="6d038-285">EnablePasswordRetrieval 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="6d038-286">FindUsersByEmail 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="6d038-287">FindUsersByName 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-287">FindUsersByName function</span></span>
- <span data-ttu-id="6d038-288">GetAllUsers 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-288">GetAllUsers function</span></span>
- <span data-ttu-id="6d038-289">GetNumberOfUsersOnline 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="6d038-290">GetPassword 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-290">GetPassword function</span></span>
- <span data-ttu-id="6d038-291">GetUser 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-291">GetUser function</span></span>
- <span data-ttu-id="6d038-292">GetUserNameByEmail 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="6d038-293">MaxInvalidPasswordAttempts 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="6d038-294">MinRequiredNonAlphanumericCharacters 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="6d038-295">MinRequiredPasswordLength 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="6d038-296">PasswordAttemptWindow 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="6d038-297">PasswordFormat 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-297">PasswordFormat property</span></span>
- <span data-ttu-id="6d038-298">PasswordStrengthRegularExpression 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="6d038-299">RequiresQuestionAndAnswer 속성이</span><span class="sxs-lookup"><span data-stu-id="6d038-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="6d038-300">RequiresUniqueEmail 속성</span><span class="sxs-lookup"><span data-stu-id="6d038-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="6d038-301">ResetPassword 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-301">ResetPassword function</span></span>
- <span data-ttu-id="6d038-302">사용자 함수를 잠금 해제</span><span class="sxs-lookup"><span data-stu-id="6d038-302">Unlock user function</span></span>
- <span data-ttu-id="6d038-303">하기 위한 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-303">UpdateUser function</span></span>
- <span data-ttu-id="6d038-304">ValidateUser 함수</span><span class="sxs-lookup"><span data-stu-id="6d038-304">ValidateUser function</span></span>

<span data-ttu-id="6d038-305">Thats C# 개발자로 서 구현 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="6d038-306">Vb.net에서 구현을 제외한 클래스를 만들고 다음 C# 코드를 변환할.NET Reflector 또는 유사한 도구를 사용 하는 작업을 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="6d038-307">연결 문자열 및 기타 속성을 기본값으로 초기화 메서드에서 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="6d038-308">(Initialize 메서드는 발생 공급자가 런타임에 로드 합니다.) Initialize 메서드의 두 번째 매개 변수 형식이 System.Collections.Specialized.NameValueCollection 며에 대 한 참조를 &lt;추가&gt; web.config 파일에서 사용자 지정 공급자와 연결 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="6d038-309">해당 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="6d038-310">Initialize 메서드의 예로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="6d038-311">사용자의 로그인 양식을 제출할 때 유효성을 검사 하기 위해 ValidateUser 메서드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="6d038-312">이 메서드는 사용자 로그인 컨트롤의 로그인 단추를 클릭할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="6d038-313">이 메서드에서 사용자 조회를 수행 하는 코드를 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="6d038-314">알 수 있듯이 직접 멤버 자격 공급자를 작성은 어렵지 않습니다 하 고 ASP.NET 2.0의이 강력한 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d038-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
