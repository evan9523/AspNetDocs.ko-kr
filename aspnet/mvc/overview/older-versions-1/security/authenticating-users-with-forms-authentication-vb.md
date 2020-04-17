---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 양식 인증(VB)으로 사용자 인증 | 마이크로 소프트 문서
author: rick-anderson
description: MVC 응용 프로그램의 특정 페이지를 암호로 보호하는 [권한 부여] 특성을 사용하는 방법을 알아봅니다. 웹 사이트 관리도 사용하는 방법을 배웁니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540820"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="a4556-104">폼 인증으로 사용자 인증(VB)</span><span class="sxs-lookup"><span data-stu-id="a4556-104">Authenticating Users with Forms Authentication (VB)</span></span>

<span data-ttu-id="a4556-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a4556-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a4556-106">MVC 응용 프로그램의 특정 페이지를 암호로 보호하는 [권한 부여] 특성을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="a4556-107">웹 사이트 관리 도구를 사용하여 사용자 및 역할을 만들고 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="a4556-108">또한 사용자 계정 및 역할 정보가 저장되는 위치를 구성하는 방법에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="a4556-109">이 자습서의 목표는 폼 인증을 사용하여 ASP.NET MVC 응용 프로그램의 보기를 암호로 보호하는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="a4556-110">웹 사이트 관리 도구를 사용하여 사용자 및 역할을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="a4556-111">또한 권한이 있는 사용자가 컨트롤러 작업을 호출하지 못하도록 하는 방법에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="a4556-112">마지막으로 사용자 이름과 암호가 저장되는 위치를 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="a4556-113">웹 사이트 관리 도구 사용</span><span class="sxs-lookup"><span data-stu-id="a4556-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="a4556-114">다른 작업을 수행하기 전에 일부 사용자와 역할을 만드는 것부터 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="a4556-115">새 사용자와 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 활용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="a4556-116">이 도구를 실행하려면 구성을 ASP.NET 메뉴 옵션 **프로젝트.를**선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="a4556-117">또는 솔루션 탐색기 창 상단에 나타나는 세계를 치는 망치의 (다소 무서운) 아이콘을 클릭하여 웹 사이트 관리 도구를 시작할 수 있습니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="a4556-118">**그림 1 – 웹 사이트 관리 도구 시작**</span><span class="sxs-lookup"><span data-stu-id="a4556-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="a4556-120">웹 사이트 관리 도구 내에서 보안 탭을 선택하여 새 사용자 **Create user** 및 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="a4556-121">Stephen 사용자에게 원하는 암호(예: *비밀)를*제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="a4556-122">**그림 2 - 새 사용자 만들기**</span><span class="sxs-lookup"><span data-stu-id="a4556-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="a4556-124">먼저 역할을 사용하도록 설정하고 하나 이상의 역할을 정의하여 새 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="a4556-125">역할 활성화 링크를 클릭하여 **역할을 활성화합니다.**</span><span class="sxs-lookup"><span data-stu-id="a4556-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="a4556-126">다음으로 **역할 만들기 또는 관리** 링크를 클릭하여 *관리자라는* 역할을 만듭니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="a4556-127">**그림 3 - 새 역할 만들기**</span><span class="sxs-lookup"><span data-stu-id="a4556-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="a4556-129">마지막으로, 샐리라는 새 사용자를 만들고 사용자 만들기 링크를 클릭하고 샐리를 만들 때 관리자를 선택하여 샐리역할을 연결합니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="a4556-130">**그림 4 - 역할에 사용자 추가**</span><span class="sxs-lookup"><span data-stu-id="a4556-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="a4556-132">모든 말과 완료되면, 당신은 스티븐과 샐리라는 두 개의 새로운 사용자가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="a4556-133">관리자라는 새 역할도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="a4556-134">샐리는 관리자 역할의 일원이며 스티븐은 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="a4556-135">승인 필요</span><span class="sxs-lookup"><span data-stu-id="a4556-135">Requiring Authorization</span></span>

<span data-ttu-id="a4556-136">사용자가 작업에 [권한 부여] 특성을 추가하여 컨트롤러 작업을 호출하기 전에 사용자를 인증하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="a4556-137">개별 컨트롤러 작업에 [권한 부여] 특성을 적용하거나 이 특성을 전체 컨트롤러 클래스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="a4556-138">예를 들어 목록 1의 컨트롤러는 CompanySecrets()라는 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="a4556-139">이 작업은 [권한 부여] 특성으로 장식되므로 사용자가 인증되지 않는 한 이 작업을 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="a4556-140">**목록 1 – 컨트롤러\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="a4556-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="a4556-141">브라우저의 주소 표시줄에 URL /Home/CompanySecrets를 입력하여 CompanySecrets() 작업을 호출하고 인증된 사용자가 아닌 경우 자동으로 로그인 보기로 리디렉션됩니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="a4556-142">**그림 5 – 로그인 보기**</span><span class="sxs-lookup"><span data-stu-id="a4556-142">**Figure 5 – The Login view**</span></span>

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="a4556-144">로그인 보기를 사용하여 사용자 이름과 암호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="a4556-145">등록된 사용자가 아닌 경우 **레지스터** 링크를 클릭하여 레지스터 보기로 이동할 수 있습니다(그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="a4556-146">등록 보기를 사용하여 새 사용자 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="a4556-147">**그림 6 – 레지스터 보기**</span><span class="sxs-lookup"><span data-stu-id="a4556-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="a4556-149">성공적으로 로그인하면 CompanySecrets 보기를 볼 수 있습니다(그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="a4556-150">기본적으로 브라우저 창을 닫을 때까지 계속 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="a4556-151">**그림 7 – 회사 비밀 보기**</span><span class="sxs-lookup"><span data-stu-id="a4556-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="a4556-153">사용자 이름 또는 사용자 역할에 의해 권한 부여</span><span class="sxs-lookup"><span data-stu-id="a4556-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="a4556-154">[권한 부여] 특성을 사용하여 컨트롤러 작업에 대한 액세스를 특정 사용자 집합 또는 특정 사용자 역할 집합으로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="a4556-155">예를 들어 목록 2의 수정된 홈 컨트롤러에는 StephenSecrets() 및 AdministratorSecrets()라는 두 개의 새 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="a4556-156">**목록 2 – 컨트롤러\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="a4556-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="a4556-157">사용자 이름 인 Stephen만 StephenSecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="a4556-158">다른 모든 사용자는 로그인 보기로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="a4556-159">Users 속성은 사용자 계정 이름의 쉼표로 분리된 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="a4556-160">관리자 역할의 사용자만 AdministratorSecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="a4556-161">예를 들어 Sally는 관리자 그룹의 구성원이므로 AdministratorSecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="a4556-162">다른 모든 사용자는 로그인 보기로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="a4556-163">Roles 속성은 역할 이름의 쉼표로 구분된 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="a4556-164">인증 구성</span><span class="sxs-lookup"><span data-stu-id="a4556-164">Configuring Authentication</span></span>

<span data-ttu-id="a4556-165">이 시점에서 사용자 계정 및 역할 정보가 저장되는 위치가 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="a4556-166">기본적으로 정보는 MVC 응용 프로그램의 앱\_데이터 폴더에 있는 ASPNETDB.mdf라는 (RANU) SQL Express 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="a4556-167">이 데이터베이스는 멤버 자격 사용을 시작할 때 ASP.NET 프레임워크에 의해 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="a4556-168">솔루션 탐색기 창에서 ASPNETDB.mdf 데이터베이스를 보려면 먼저 메뉴 옵션 프로젝트, 모든 파일 표시를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="a4556-169">응용 프로그램을 개발할 때 기본 SQL Express 데이터베이스를 사용하는 것은 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="a4556-170">그러나 프로덕션 응용 프로그램에 는 기본 ASPNETDB.mdf 데이터베이스를 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="a4556-171">이 경우 다음 두 단계를 완료하여 사용자 계정 정보가 저장되는 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="a4556-172">프로덕션 데이터베이스에 응용 프로그램 서비스 데이터베이스 개체 추가 - 프로덕션 데이터베이스를 가리키도록 응용 프로그램 연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="a4556-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="a4556-173">첫 번째 단계는 프로덕션 데이터베이스에 필요한 모든 데이터베이스 개체(테이블 및 저장 프로시저)를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="a4556-174">이러한 개체를 새 데이터베이스에 추가하는 가장 쉬운 방법은 ASP.NET SQL Server 설치 마법사를 활용하는 것입니다(그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="a4556-175">Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 열고 명령 프롬프트에서 다음 명령을 실행하여 이 도구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="a4556-176">아스프넷\_레그SQL</span><span class="sxs-lookup"><span data-stu-id="a4556-176">aspnet\_regsql</span></span>

<span data-ttu-id="a4556-177">**그림 8 - ASP.NET SQL 서버 설치 마법사**</span><span class="sxs-lookup"><span data-stu-id="a4556-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="a4556-179">ASP.NET SQL Server 설치 마법사를 사용하면 네트워크에서 SQL Server 데이터베이스를 선택하고 ASP.NET 응용 프로그램 서비스에 필요한 모든 데이터베이스 개체를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="a4556-180">데이터베이스 서버가 로컬 컴퓨터에 있을 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="a4556-181">ASP.NET SQL Server 설치 마법사를 사용하지 않으려면 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가하기 위한 SQL 스크립트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="a4556-182">C:\윈도우\마이크로소프트.NET 프레임 워크\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="a4556-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="a4556-183">필요한 데이터베이스 개체를 만든 후 MVC 응용 프로그램에서 사용하는 데이터베이스 연결을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="a4556-184">프로덕션 데이터베이스를 가리키도록 웹 구성(web.config) 파일에서 ApplicationServices 연결 문자열을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="a4556-185">예를 들어, MyProductionDB라는 데이터베이스에 3 점 나열에서 수정 된 연결 (원래 ApplicationServices 연결 문자열이 주석이 없습니다).</span><span class="sxs-lookup"><span data-stu-id="a4556-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="a4556-186">**목록 3 – Web.config**</span><span class="sxs-lookup"><span data-stu-id="a4556-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="a4556-187">데이터베이스 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="a4556-187">Configuring Database Permissions</span></span>

<span data-ttu-id="a4556-188">통합 보안을 사용하여 데이터베이스에 연결하는 경우 데이터베이스에 로그인할 때 올바른 Windows 사용자 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="a4556-189">올바른 계정은 ASP.NET 개발 서버 또는 인터넷 정보 서비스를 웹 서버로 사용하는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="a4556-190">올바른 사용자 계정은 운영 체제에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="a4556-191">ASP.NET 개발 서버(Visual Studio에서 사용하는 기본 웹 서버)를 사용하는 경우 응용 프로그램이 Windows 사용자 계정의 컨텍스트 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="a4556-192">이 경우 Windows 사용자 계정을 데이터베이스 서버 로그인으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="a4556-193">또는 인터넷 정보 서비스를 사용하는 경우 ASPNET 계정 또는 NT AUTHORITY/NETWORK SERVICE 계정을 데이터베이스 서버 로그인으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="a4556-194">Windows XP를 사용하는 경우 데이터베이스에 ASPNET 계정을 로그인으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="a4556-195">Windows Vista 또는 Windows Server 2008과 같은 최신 운영 체제를 사용하는 경우 NT AUTHORITY/NETWORK SERVICE 계정을 데이터베이스 로그인으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="a4556-196">Microsoft SQL Server 관리 스튜디오를 사용하여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다(그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="a4556-197">**그림 9 – 새 Microsoft SQL Server 로그인 만들기**</span><span class="sxs-lookup"><span data-stu-id="a4556-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="a4556-199">필요한 로그인을 만든 후에는 올바른 데이터베이스 역할을 가진 데이터베이스 사용자에게 로그인을 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="a4556-200">로그인을 두 번 클릭하고 사용자 매핑 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="a4556-201">예를 들어 사용자를 인증하려면 aspnet\_멤버 자격\_BasicAccess 데이터베이스 역할을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="a4556-202">새 사용자를 만들려면 aspnet\_멤버 자격\_FullAccess 데이터베이스 역할을 사용하도록 설정해야 합니다(그림 10 참조).</span><span class="sxs-lookup"><span data-stu-id="a4556-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="a4556-203">**그림 10 – 응용 프로그램 서비스 데이터베이스 역할 추가**</span><span class="sxs-lookup"><span data-stu-id="a4556-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="a4556-205">요약</span><span class="sxs-lookup"><span data-stu-id="a4556-205">Summary</span></span>

<span data-ttu-id="a4556-206">이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드할 때 폼 인증을 사용하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="a4556-207">먼저 웹 사이트 관리 도구를 활용하여 새 사용자와 역할을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="a4556-208">다음으로 권한이 없는 사용자가 컨트롤러 작업을 호출하지 못하도록 [권한 부여] 특성을 사용하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="a4556-209">마지막으로 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장하도록 MVC 응용 프로그램을 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4556-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4556-210">[이전](preventing-javascript-injection-attacks-cs.md)
> [다음](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a4556-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>
