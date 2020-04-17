---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 새로운 ASP.NET MVC 프로젝트 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 1단계는 기본 NerdDinner 응용 프로그램 구조를 배치하는 방법을 보여 주며, 이 방법을 보여 주실 수 있습니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541483"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="b3f71-103">새 ASP.NET MVC 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b3f71-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="b3f71-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b3f71-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b3f71-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3f71-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b3f71-106">이것은 ASP.NET MVC 1을 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 1단계입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b3f71-107">1단계는 기본 NerdDinner 응용 프로그램 구조를 배치하는 방법을 보여 주며, 이 방법을 보여 주실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="b3f71-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="b3f71-109">얼간이 디너 1&gt;단계 : 파일 - 새로운 프로젝트</span><span class="sxs-lookup"><span data-stu-id="b3f71-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="b3f71-110">우리는 비주얼 스튜디오 2008 또는 무료 비주얼 웹 개발자 2008 익스프레스 내에서 **파일 -&gt;새로운 프로젝트** 메뉴 항목을 선택하여 우리의 NerdDinner 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="b3f71-111">그러면 "새 프로젝트" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="b3f71-112">새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자왼쪽에 있는 "웹" 노드를 선택한 다음 오른쪽에 있는 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="b3f71-113">*중요: MVC를 ASP.NET 다운로드하여 설치했는지 확인합니다. 아직 설치하지 않은 경우 [Microsoft 웹 플랫폼 설치 관리자의](https://www.microsoft.com/web/downloads/platform.aspx) V2를 사용할 수 ASP.NET"웹&gt;플랫폼 프레임워크 및 런타임 섹션에서 MVC를 사용할 수 있습니다).*</span><span class="sxs-lookup"><span data-stu-id="b3f71-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="b3f71-114">"NerdDinner"를 만들 새 프로젝트의 이름을 지정한 다음 "확인" 단추를 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="b3f71-115">"확인"을 클릭하면 Visual Studio에서 새 응용 프로그램에 대한 단위 테스트 프로젝트를 선택적으로 만들라는 추가 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="b3f71-116">이 단위 테스트 프로젝트를 사용하면 응용 프로그램의 기능과 동작을 확인하는 자동화된 테스트를 만들 수 있습니다(이 자습서의 후반부에서 수행할 방법을 설명합니다).</span><span class="sxs-lookup"><span data-stu-id="b3f71-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="b3f71-117">위의 대화 상자의 "테스트 프레임워크" 드롭다운은 컴퓨터에 설치된 사용 가능한 모든 ASP.NET MVC 단위 테스트 프로젝트 템플릿으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="b3f71-118">버전은 NUnit, MBUnit 및 XUnit에 대해 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="b3f71-119">기본 제공 Visual Studio 단위 테스트 프레임워크도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="b3f71-120">*참고: Visual Studio 단위 테스트 프레임워크는 Visual Studio 2008 전문가 및 상위 버전에서만 사용할 수 있습니다. VS 2008 표준 판 또는 비주얼 웹 개발자 2008 익스프레스를 사용 하는 경우 다운로드 하 고 이 대화 상자를 표시 하려면 ASP.NET MVC에 대 한 NUnit, MBUnit 또는 XUnit 확장을 설치 해야 합니다. 테스트 프레임워크가 설치되어 있지 않으면 대화 상자가 표시되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="b3f71-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="b3f71-121">만드는 테스트 프로젝트에 기본 "NerdDinner.Test" 이름을 사용하고 "Visual Studio 단위 테스트" 프레임워크 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="b3f71-122">"확인" 버튼을 클릭하면 Visual Studio는 웹 응용 프로그램과 단위 테스트용 프로젝트 등 두 개의 프로젝트를 통해 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="b3f71-123">NerdDinner 디렉터리 구조 검사</span><span class="sxs-lookup"><span data-stu-id="b3f71-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="b3f71-124">Visual Studio를 사용하여 새 ASP.NET MVC 응용 프로그램을 만들면 프로젝트에 여러 파일과 디렉터리가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="b3f71-125">기본적으로 ASP.NET MVC 프로젝트에는 6개의 최상위 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="b3f71-126">**디렉터리**</span><span class="sxs-lookup"><span data-stu-id="b3f71-126">**Directory**</span></span> | <span data-ttu-id="b3f71-127">**용도**</span><span class="sxs-lookup"><span data-stu-id="b3f71-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="b3f71-128">**/컨트롤러**</span><span class="sxs-lookup"><span data-stu-id="b3f71-128">**/Controllers**</span></span> | <span data-ttu-id="b3f71-129">URL 요청을 처리하는 컨트롤러 클래스를 배치한 위치</span><span class="sxs-lookup"><span data-stu-id="b3f71-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="b3f71-130">**/모델**</span><span class="sxs-lookup"><span data-stu-id="b3f71-130">**/Models**</span></span> | <span data-ttu-id="b3f71-131">데이터를 나타내고 조작하는 클래스를 배치한 위치</span><span class="sxs-lookup"><span data-stu-id="b3f71-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="b3f71-132">**/보기**</span><span class="sxs-lookup"><span data-stu-id="b3f71-132">**/Views**</span></span> | <span data-ttu-id="b3f71-133">출력 렌더링을 담당하는 UI 템플릿 파일을 넣는 위치</span><span class="sxs-lookup"><span data-stu-id="b3f71-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="b3f71-134">**/스크립트**</span><span class="sxs-lookup"><span data-stu-id="b3f71-134">**/Scripts**</span></span> | <span data-ttu-id="b3f71-135">자바 스크립트 라이브러리 파일 및 스크립트 (.js)를 넣어 위치</span><span class="sxs-lookup"><span data-stu-id="b3f71-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="b3f71-136">**/콘텐츠**</span><span class="sxs-lookup"><span data-stu-id="b3f71-136">**/Content**</span></span> | <span data-ttu-id="b3f71-137">CSS 및 이미지 파일 및 기타 비동적/비자바스크립트 콘텐츠를 넣는 위치</span><span class="sxs-lookup"><span data-stu-id="b3f71-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="b3f71-138">**/앱\_데이터**</span><span class="sxs-lookup"><span data-stu-id="b3f71-138">**/App\_Data**</span></span> | <span data-ttu-id="b3f71-139">읽고 쓰려는 데이터 파일을 저장하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="b3f71-140">ASP.NET MVC는 이 구조를 필요로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="b3f71-141">실제로 대규모 응용 프로그램에서 작업하는 개발자는 일반적으로 응용 프로그램을 여러 프로젝트로 분할하여 보다 관리하기 쉽게 만듭니다(예: 데이터 모델 클래스는 웹 응용 프로그램과 별도의 클래스 라이브러리 프로젝트로 이동하는 경우가 많습니다).</span><span class="sxs-lookup"><span data-stu-id="b3f71-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="b3f71-142">그러나 기본 프로젝트 구조는 응용 프로그램 문제를 깔끔하게 유지하는 데 사용할 수 있는 좋은 기본 디렉터리 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="b3f71-143">/Controllers 디렉토리를 확장하면 Visual Studio에서 기본적으로 프로젝트에 두 개의 컨트롤러 클래스인 HomeController 및 AccountController를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="b3f71-144">/View 디렉터리를 확장하면 세 개의 하위 디렉토리(/Home, Account 및 /Shared)와 그 안에 있는 여러 템플릿 파일이 기본적으로 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="b3f71-145">/Content 및 /Scripts 디렉터리를 확장하면 사이트의 모든 HTML에 스타일을 지정하는 데 사용되는 Site.css 파일과 응용 프로그램 내에서 aJAX 및 jQuery 지원을 ASP.NET 활성화할 수 있는 JavaScript 라이브러리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="b3f71-146">NerdDinner.Test 프로젝트를 확장하면 컨트롤러 클래스에 대한 단위 테스트를 포함하는 두 개의 클래스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="b3f71-147">Visual Studio에서 추가한 이러한 기본 파일은 홈 페이지, 페이지, 계정 로그인/로그아웃/등록 페이지 및 처리되지 않은 오류 페이지(모든 유선 및 작업 상자)가 포함된 작업 응용 프로그램에 대한 기본 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="b3f71-148">얼간이 저녁 식사 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b3f71-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="b3f71-149">**디버그-&gt;디버깅 시작** 또는 **디버깅&gt;** 메뉴 항목 없이 시작 중 하나를 선택하여 프로젝트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="b3f71-150">이렇게 하면 Visual Studio와 함께 제공되는 기본 제공 ASP.NET 웹 서버가 시작되고 응용 프로그램이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="b3f71-151">다음은 새 프로젝트의 홈 페이지(URL: "/")가 실행될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="b3f71-152">"소개" 탭을 클릭하면 페이지가 표시됩니다(URL: "/홈/소개").</span><span class="sxs-lookup"><span data-stu-id="b3f71-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="b3f71-153">오른쪽 상단에 있는 "로그온" 링크를 클릭하면 로그인 페이지로 이동합니다(URL: "/계정/로그온").</span><span class="sxs-lookup"><span data-stu-id="b3f71-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="b3f71-154">로그인 계정이 없는 경우 레지스터 링크(URL: "/계정/등록")를 클릭하여 다음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="b3f71-155">새 프로젝트를 만들 때 위의 홈, 약 및 로그아웃/레지스터 기능을 구현하는 코드가 기본적으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="b3f71-156">우리는 우리의 응용 프로그램의 시작 점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="b3f71-157">얼간이 디너 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="b3f71-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="b3f71-158">프로페셔널 에디션 또는 더 높은 버전의 Visual Studio 2008을 사용하는 경우 Visual Studio 내에서 기본 제공 단위 테스트 IDE 지원을 사용하여 프로젝트를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="b3f71-159">위의 옵션 중 하나를 선택하면 IDE 내에서 "테스트 결과" 창이 열리고 기본 제공 기능을 포함하는 새 프로젝트에 포함된 27개 단위 테스트에서 합격/불합격 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="b3f71-160">이 자습서의 후반부에서는 자동화된 테스트에 대해 자세히 이야기하고 구현한 응용 프로그램 기능을 다루는 추가 단위 테스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="b3f71-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3f71-161">Next Step</span></span>

<span data-ttu-id="b3f71-162">이제 기본 응용 프로그램 구조가 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="b3f71-163">이제 응용 [프로그램 데이터를 저장하는 데이터베이스를 만들어](create-a-database.md)보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f71-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3f71-164">[이전](introducing-the-nerddinner-tutorial.md)
> [다음](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="b3f71-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
