---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용한 안전한 응용 프로그램 | 마이크로 소프트 문서
author: rick-anderson
description: 9단계는 NerdDinner 응용 프로그램을 보호하기 위해 인증 및 인증을 추가하는 방법을 보여 주므로 사용자가 사이트에 등록하고 로그인하여 만들 수 있습니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542575"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="0a487-103">인증 및 권한 부여를 사용하여 애플리케이션 보호</span><span class="sxs-lookup"><span data-stu-id="0a487-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="0a487-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0a487-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0a487-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0a487-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="0a487-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 9단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="0a487-107">9단계는 사용자가 새 저녁 식사를 만들기 위해 사이트에 등록하고 로그인해야 하며 저녁 식사를 주최하는 사용자만 나중에 편집할 수 있도록 NerdDinner 응용 프로그램을 보호하기 위해 인증 및 권한 부여를 추가하는 방법을 보여 주며, 이 에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="0a487-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="0a487-109">NerdDinner 단계 9: 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0a487-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="0a487-110">지금 우리의 NerdDinner 응용 프로그램은 사이트를 방문하는 모든 사람에게 모든 저녁 식사의 세부 사항을 만들고 편집 할 수있는 기능을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="0a487-111">사용자가 새 저녁 식사를 만들기 위해 사이트에 등록하고 로그인해야 하고, 저녁 식사를 주최하는 사용자만 나중에 편집할 수 있도록 제한을 추가해야 하도록 이 변경을 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="0a487-112">이를 위해 인증 및 인증을 사용하여 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="0a487-113">인증 및 권한 부여 이해</span><span class="sxs-lookup"><span data-stu-id="0a487-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="0a487-114">*인증은* 응용 프로그램에 액세스하는 클라이언트의 ID를 식별하고 유효성을 검사하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="0a487-115">간단히 말해서, 최종 사용자가 웹 사이트를 방문 할 때 "누가"를 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="0a487-116">ASP.NET 브라우저 사용자를 인증하는 여러 가지 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="0a487-117">인터넷 웹 응용 프로그램의 경우 가장 일반적인 인증 방법을 "양식 인증"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="0a487-118">양식 인증을 사용하면 개발자가 응용 프로그램 내에서 HTML 로그인 양식을 작성한 다음 최종 사용자가 데이터베이스 또는 다른 암호 자격 증명 저장소에 대해 제출하는 사용자 이름/암호의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="0a487-119">사용자 이름/암호 조합이 올바른 경우 개발자는 ASP.NET 암호화된 HTTP 쿠키를 발급하여 향후 요청에서 사용자를 식별하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="0a487-120">우리는 우리의 NerdDinner 응용 프로그램과 양식 인증을 사용하여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="0a487-121">*권한 부여는* 인증된 사용자가 특정 URL/리소스에 액세스하거나 일부 작업을 수행할 수 있는 권한이 있는지 여부를 결정하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="0a487-122">예를 들어 NerdDinner 응용 프로그램 내에서 로그인한 사용자만 */Dinners/Create* URL에 액세스하고 새 Dinners를 만들 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="0a487-123">또한 저녁 식사를 주최하는 사용자만 편집하고 다른 모든 사용자에 대한 편집 액세스를 거부할 수 있도록 권한 부여 논리를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="0a487-124">양식 인증 및 계정 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="0a487-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="0a487-125">ASP.NET MVC에 대한 기본 Visual Studio 프로젝트 템플릿은 새 ASP.NET MVC 응용 프로그램을 만들 때 양식 인증을 자동으로 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="0a487-126">또한 미리 빌드된 계정 로그인 페이지 구현을 프로젝트에 자동으로 추가하여 사이트 내에서 보안을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="0a487-127">기본 Site.master 마스터 페이지에는 사용자가 인증되지 않을 때 사이트의 오른쪽 상단에 "로그온" 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="0a487-128">"로그온" 링크를 클릭하면 사용자가 */계정/로그온* URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="0a487-129">등록하지 않은 방문자는 "등록" 링크를 클릭하여 */Account/Register* URL로 이동하여 계정 세부 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="0a487-130">"등록" 버튼을 클릭하면 ASP.NET 멤버십 시스템 내에서 새 사용자가 생성되고 양식 인증을 사용하여 사이트에 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="0a487-131">사용자가 로그인하면 Site.master가 페이지의 오른쪽 상단을 변경하여 "환영[사용자 이름]"을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="0a487-132">"로그온" 링크 대신 "로그오프" 링크를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="0a487-133">"로그 오프" 링크를 클릭하면 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="0a487-134">위의 로그인, 로그아웃 및 등록 기능은 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가한 AccountController 클래스 내에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="0a487-135">AccountController의 UI는 \Views\Account 디렉터리 내의 보기 템플릿을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="0a487-136">AccountController 클래스는 ASP.NET 양식 인증 시스템을 사용하여 암호화된 인증 쿠키를 발급하고 ASP.NET 멤버 자격 API를 사용하여 사용자 이름/암호를 저장하고 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="0a487-137">ASP.NET 멤버 자격 API는 확장 가능하며 모든 암호 자격 증명 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="0a487-138">ASP.NET SQL 데이터베이스 또는 Active Directory 내에서 사용자 이름/암호를 저장하는 기본 제공 멤버 자격 공급자 구현과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="0a487-139">NerdDinner 응용 프로그램이 프로젝트의 루트에서 "web.config" 파일을 열고 그 안에 있는 멤버십 섹션을 &lt;&gt; 찾아서 사용해야 하는 멤버십 공급자를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="0a487-140">프로젝트를 만들 때 추가된 기본 web.config는 SQL 멤버 자격 공급자를 등록하고 데이터베이스 위치를 지정하기 위해 "ApplicationServices"라는 연결 문자열을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="0a487-141">기본 "ApplicationServices" 연결 &lt;문자열(web.config 파일의 연결 Strings&gt; 섹션 내에 지정됨)은 SQL Express를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="0a487-142">"ASPNETDB"라는 SQL Express 데이터베이스를 가리킵니다. 응용 프로그램의 "앱\_데이터" 디렉토리 아래에 있는 MDF"입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="0a487-143">이 데이터베이스가 응용 프로그램 내에서 처음으로 멤버 자격 API를 사용할 때 존재하지 않는 경우 ASP.NET 자동으로 데이터베이스를 만들고 해당 데이터베이스 내에 적절한 멤버 자격 데이터베이스 스키마를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="0a487-144">SQL Express를 사용하는 대신 전체 SQL Server 인스턴스를 사용하거나 원격 데이터베이스에 연결하려는 경우 web.config 파일 내의 "ApplicationServices" 연결 문자열을 업데이트하고 해당 구성 설정 스키마가 가리키는 데이터베이스에 추가되었는지 확인하는 것만하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="0a487-145">\Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 "aspnet\_regsql.exe" 유틸리티를 실행하여 멤버 자격및 기타 ASP.NET 응용 프로그램 서비스에 적합한 스키마를 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="0a487-146">[권한 부여] 필터를 사용하여 /Dinners/URL 만들기 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0a487-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="0a487-147">NerdDinner 응용 프로그램에 대한 보안 인증 및 계정 관리 구현을 활성화하기 위해 코드를 작성할 필요가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="0a487-148">사용자는 당사의 애플리케이션에 새 계정을 등록하고 사이트의 로그인/로그아웃을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="0a487-149">이제 응용 프로그램에 권한 부여 논리를 추가하고 방문자의 인증 상태 및 사용자 이름을 사용하여 사이트 내에서 수행할 수 있는 것과 수행할 수 없는 작업을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="0a487-150">먼저 DinnersController 클래스의 "만들기" 작업 메서드에 권한 부여 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="0a487-151">특히 */Dinners/Create* URL에 액세스하는 사용자가 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="0a487-152">로그인하지 않은 경우 로그인할 수 있도록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="0a487-153">이 논리를 구현하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="0a487-154">우리가해야 할 일은 다음과 같은 작업 메서드 만들기에 [권한 부여] 필터 특성을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="0a487-155">ASP.NET MVC는 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현하는 데 사용할 수 있는 "작업 필터"를 만드는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="0a487-156">[권한 부여] 필터는 ASP.NET MVC에서 제공하는 기본 제공 작업 필터 중 하나이며 개발자가 작업 메서드 및 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="0a487-157">[위와 같은) 매개 변수 없이 적용하면 [권한 부여] 필터는 작업 메서드 요청을 하는 사용자가 로그인해야 하며 그렇지 않은 경우 자동으로 로그인 URL로 브라우저를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="0a487-158">이 작업을 수행 할 때 원래 요청된 URL은 쿼리 문자열 인수로 전달됩니다 (예 : /Account / LogOn? ReturnUrl =%2fDinners%2fCreate).</span><span class="sxs-lookup"><span data-stu-id="0a487-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="0a487-159">그러면 AccountController는 사용자가 로그인한 후 원래 요청한 URL로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="0a487-160">[권한 부여] 필터는 선택적으로 사용자가 로그인하고 허용된 사용자 또는 허용된 보안 역할의 구성원 목록에 로그인하도록 요구하는 데 사용할 수 있는 "사용자" 또는 "역할" 속성을 지정하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="0a487-161">예를 들어 아래 코드는 "scottgu" 및 "billg"이라는 두 명의 특정 사용자만 /Dinners/Create URL에 액세스할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="0a487-162">코드 내에 특정 사용자 이름을 포함시키는 것은 유지 관리가 불가능한 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="0a487-163">더 나은 방법은 코드가 검사하는 상위 수준 "역할"을 정의한 다음 데이터베이스 또는 활성 디렉터리 시스템을 사용하여 사용자를 역할에 매핑하는 것입니다(실제 사용자 매핑 목록을 코드에서 외부로 저장할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="0a487-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="0a487-164">ASP.NET 기본 제공 역할 관리 API뿐만 아니라 이 사용자/역할 매핑을 수행하는 데 도움이 되는 기본 제공 역할 공급자(SQL 및 Active Directory용 역할 공급자 포함)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="0a487-165">그런 다음 코드를 업데이트하여 특정 "관리자" 역할 내의 사용자가 /Dinners/Create URL에 액세스할 수 있도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="0a487-166">저녁 식사 만들기 시 User.Identity.Name 속성 사용</span><span class="sxs-lookup"><span data-stu-id="0a487-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="0a487-167">Controller 기본 클래스에 노출된 User.Identity.Name 속성을 사용하여 현재 로그인한 요청 사용자의 사용자 이름을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="0a487-168">이전에 Create() 작업 메서드의 HTTP-POST 버전을 구현할 때 Dinner의 "HostedBy" 속성을 정적 문자열로 하드 코딩했습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="0a487-169">이제 이 코드를 업데이트하여 User.Identity.Name 속성을 사용하고 Dinner를 만드는 호스트에 대한 RSVP를 자동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="0a487-170">Create() 메서드에 [권한 부여] 특성을 추가했기 때문에 mVC를 ASP.NET 사용자가 /Dinners/Create URL을 방문하는 사용자가 사이트에 로그인한 경우에만 작업 메서드가 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="0a487-171">따라서 User.Identity.Name 속성 값에는 항상 유효한 사용자 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="0a487-172">저녁 식사 편집 시 User.Identity.Name 속성 사용</span><span class="sxs-lookup"><span data-stu-id="0a487-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="0a487-173">이제 사용자가 호스팅하는 저녁 식사의 속성만 편집할 수 있도록 사용자를 제한하는 권한 부여 논리를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="0a487-174">이를 위해 먼저 Dinner 개체에 "IsHostedBy(사용자 이름)" 도우미 메서드를 추가합니다(이전에 빌드한 Dinner.cs 부분 클래스 내에서).</span><span class="sxs-lookup"><span data-stu-id="0a487-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="0a487-175">이 도우미 메서드는 제공된 사용자 이름이 Dinner HostedBy 속성과 일치하는지 여부에 따라 true 또는 false를 반환하고 대/소문자를 구분하지 않음 문자열 비교를 수행하는 데 필요한 논리를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="0a487-176">그런 다음 DinnersController 클래스 내에서 편집() 작업 메서드에 [권한 부여] 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="0a487-177">이렇게 하면 *사용자가 /Dinners/편집/[id] URL을* 요청하기 위해 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="0a487-178">그런 다음 Dinner.IsHostedBy(사용자 이름) 도우미 메서드를 사용하는 편집 메서드에 코드를 추가하여 로그인한 사용자가 Dinner 호스트와 일치하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="0a487-179">사용자가 호스트가 아닌 경우 "잘못된 소유자" 보기가 표시되고 요청을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="0a487-180">이 작업을 수행하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="0a487-181">그런 다음 \View\Dinners 디렉토리를 마우스 오른쪽 단추로 클릭하고 추가&gt;보기 메뉴 명령을 선택하여 새 "잘못된 소유자" 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="0a487-182">아래 오류 메시지로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="0a487-183">이제 사용자가 소유하지 않은 저녁 식사를 편집하려고 하면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="0a487-184">컨트롤러 내에서 Delete() 작업 메서드에 대해 동일한 단계를 반복하여 Dinners를 삭제할 수 있는 권한도 잠그고 Dinner의 호스트만 삭제할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="0a487-185">링크 표시/숨기기 편집 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0a487-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="0a487-186">세부 정보 URL에서 DinnersController 클래스의 편집 및 삭제 작업 메서드에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="0a487-187">현재 세부 정보 URL에 대한 방문자가 저녁 식사의 호스트인지 여부에 관계없이 편집 및 삭제 작업 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="0a487-188">방문 하는 사용자가 dinner의 소유자 인 경우에 링크 표시 되도록이 변경 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="0a487-189">DinnersController 내의 Details() 작업 메서드는 Dinner 개체를 검색한 다음 뷰 템플릿에 모델 개체로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="0a487-190">아래와 같은 Dinner.IsHostedBy() 도우미 방법을 사용하여 보기 템플릿을 업데이트하여 편집 및 삭제 링크를 조건부로 표시/숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="0a487-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a487-191">Next Steps</span></span>

<span data-ttu-id="0a487-192">이제 인증된 사용자가 AJAX를 사용하여 저녁 식사를 위해 RSVP로 사용할 수 있는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a487-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a487-193">[이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="0a487-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
