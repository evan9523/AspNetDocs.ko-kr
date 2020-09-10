---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012의 페이지 검사기는 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 합니다.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 42d5683ce75467a159c9d13edf302bd6bf24a11d
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643695"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="fa63d-104">ASP.NET MVC에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="fa63d-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="fa63d-105">사람, Tim Am마나트 n</span><span class="sxs-lookup"><span data-stu-id="fa63d-105">by Tim Ammann</span></span>

> <span data-ttu-id="fa63d-106">Visual Studio 2012의 페이지 검사기는 통합 브라우저를 사용 하는 웹 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="fa63d-107">통합 브라우저에서 요소를 선택 하 고 페이지 검사기 요소의 원본 및 CSS를 즉시 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="fa63d-108">MVC 뷰를 찾아보고, 렌더링 된 태그의 소스를 빠르게 찾고, Visual Studio 환경 내에서 브라우저 도구를 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="fa63d-109">비디오 시청</span><span class="sxs-lookup"><span data-stu-id="fa63d-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="fa63d-110">이 자습서에서는 검사 모드을 사용 하도록 설정한 다음 웹 프로젝트 내에서 태그 및 CSS를 빠르게 찾고 편집 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="fa63d-111">이 자습서에서는 MVC 프로젝트를 사용 하지만 [Web Forms](https://go.microsoft.com/?linkid=9802001) 및 기타 ASP.NET 응용 프로그램에도 페이지 검사기을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="fa63d-112">이 자습서에는 다음과 같은 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="fa63d-113">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="fa63d-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="fa63d-114">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fa63d-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="fa63d-115">페이지 검사기를 사용 하 여 뷰 찾아보기</span><span class="sxs-lookup"><span data-stu-id="fa63d-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="fa63d-116">검사 모드 사용</span><span class="sxs-lookup"><span data-stu-id="fa63d-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="fa63d-117">페이지 검사기를 사용 하 여 태그 변경</span><span class="sxs-lookup"><span data-stu-id="fa63d-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="fa63d-118">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="fa63d-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="fa63d-119">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fa63d-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="fa63d-120">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="fa63d-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="fa63d-121">CSS 색 선택 사용</span><span class="sxs-lookup"><span data-stu-id="fa63d-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="fa63d-122">JavaScript에 동적 페이지 요소 매핑</span><span class="sxs-lookup"><span data-stu-id="fa63d-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="fa63d-123">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="fa63d-123">Prerequisites</span></span>

- <span data-ttu-id="fa63d-124">웹 용 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web)</span><span class="sxs-lookup"><span data-stu-id="fa63d-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="fa63d-125">최신 버전의 페이지 검사기을 다운로드 하려면 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) 를 사용 하 여 WINDOWS Azure SDK for .net 2.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="fa63d-126">페이지 검사기 Microsoft Web 개발자 도구와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="fa63d-127">최신 버전은 1.3입니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-127">The latest version is 1.3.</span></span> <span data-ttu-id="fa63d-128">보유 한 버전을 확인 하려면 Visual Studio를 실행 하 고 **도움말** 메뉴에서 **정보 Microsoft Visual Studio** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="fa63d-129">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fa63d-129">Create a Web Application</span></span>

<span data-ttu-id="fa63d-130">먼저 페이지 검사기 사용할 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="fa63d-131">Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="fa63d-132">왼쪽에서 **Visual c #** 을 확장 하 고 **웹**을 선택한 다음 **ASP.NET MVC4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="fa63d-134">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-134">Click **OK**.</span></span>

<span data-ttu-id="fa63d-135">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="fa63d-136">기본 뷰 엔진으로 **Razor** 를 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-136">Leave **Razor** as the default view engine.</span></span>

![새 ASP.NET MVC 프로젝트-인터넷 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="fa63d-138">응용 프로그램이 **소스** 뷰에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-138">The application opens in **Source** view.</span></span>

![소스 뷰의 새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="fa63d-140">이제 작업할 응용 프로그램이 있으므로 페이지 검사기를 사용 하 여 검사 하 고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="fa63d-141">페이지 검사기를 사용 하 여 뷰 찾아보기</span><span class="sxs-lookup"><span data-stu-id="fa63d-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="fa63d-142">Visual Studio 2012에서 프로젝트의 뷰를 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 하면 페이지 검사기 경로를 파악 하 고 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="fa63d-143">**솔루션 탐색기**에서 **Views** 폴더를 확장 한 다음 **Home** 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="fa63d-144">Index cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![View Index. cshtml in 페이지 검사기](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="fa63d-146">기본적으로 페이지 검사기는 Visual Studio 환경의 왼쪽에 창으로 도킹 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="fa63d-147">원하는 경우 다른 곳에 도킹 하거나 창의 도킹을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="fa63d-148">[방법: 창 정렬 및 도킹을](https://msdn.microsoft.com/library/z4y0hsax.aspx)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fa63d-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="fa63d-149">페이지 검사기 창의 위쪽 창에는 브라우저 창의 현재 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="fa63d-150">아래쪽 창에는 페이지의 다양 한 측면을 검사할 수 있는 몇 가지 탭과 함께 HTML 태그의 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="fa63d-151">아래쪽 창은 Internet Explorer의 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) 와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![페이지 검사기 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="fa63d-153">이 자습서에서는 **HTML** 및 **스타일** 탭을 사용 하 여 신속 하 게 탐색 하 고 응용 프로그램을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="fa63d-154">EnableInspection 모드</span><span class="sxs-lookup"><span data-stu-id="fa63d-154">EnableInspection Mode</span></span>

<span data-ttu-id="fa63d-155">검사 모드에 페이지 검사기을 추가 하려면 **검사** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="fa63d-156">검사 모드에서 렌더링 된 페이지의 일부에 마우스 포인터를 놓으면 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![전환 검사 모드](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="fa63d-158">이제 페이지 검사기 내에서 페이지의 서로 다른 부분으로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="fa63d-159">이렇게 하면 마우스 포인터가 큼 더하기 기호로 바뀌고 아래 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="fa63d-161">마우스 포인터를 이동 하면 Visual Studio는 소스 파일에서 해당 Razor 구문를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="fa63d-162">HTML 요소가 다른 소스 파일에서 제공 되는 경우 Visual Studio에서 자동으로 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="fa63d-163">페이지 검사기에서 **html** 탭에는 Razor 구문에서 생성 된 html이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="fa63d-164">마우스 포인터를 움직이면 HTML 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="fa63d-165">**스타일** 탭에는 요소에 대 한 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="fa63d-166">페이지 검사기를 사용 하 여 태그 변경</span><span class="sxs-lookup"><span data-stu-id="fa63d-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="fa63d-167">페이지 검사기를 사용 하면 위치가 명확 하지 않을 수 있는 태그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="fa63d-168">그런 다음 태그를 수정 하 고 결과 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="fa63d-169">이를 확인 하려면 **검사** 를 클릭 한 다음 페이지 검사기 창에서 페이지 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="fa63d-170">마우스 포인터를 바닥글 영역으로 이동 하면 페이지 검사기 \_ layout 파일이 열리고 선택한 레이아웃 페이지의 섹션이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="fa63d-171">여기에서 볼 수 있듯이 바닥글 영역은 뷰 자체가 아니라 레이아웃 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-171">As you can see, the footer area is defined in the layout file, and not the view itself.</span></span>

![바닥글](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="fa63d-173">이제 저작권 표시를 사용 하 여 줄 위로 마우스 포인터를 이동 <a id="a"></a> 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="fa63d-174">\_Layout. cshtml 페이지에서 해당 줄이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![바닥글 저작권 선이 강조 표시 됨](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="fa63d-176">레이아웃 cshtml 파일의 줄 끝에 일부 텍스트를 추가 \_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="fa63d-177">&lt;p &gt; &amp; copy; @DateTime.Now.Year -My ASP.NET MVC 응용 프로그램 바위! &lt; /p&gt;</span><span class="sxs-lookup"><span data-stu-id="fa63d-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="fa63d-178">이제 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 하 여 페이지 검사기 브라우저 창에 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![내 ASP.NET 응용 프로그램 돌!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="fa63d-180">Index는 footer에 정의 되어 있지만 페이지 검사기 레이아웃에 포함 된 것으로 표시 된 것으로 간주 될 수 있습니다. \_</span><span class="sxs-lookup"><span data-stu-id="fa63d-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="fa63d-181">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="fa63d-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="fa63d-182">다음으로 HTML 창 및이 창에서 요소를 매핑하는 방법에 대해 간략히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="fa63d-183">**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa63d-184">"여기에 로고가 있습니다." 라는 페이지의 위쪽 부분을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="fa63d-185">특정 요소를 자세히 검사 하 고 있으므로 마우스 포인터를 이동할 때 브라우저 창에 표시 되는 내용이 더 이상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="fa63d-186">이제 마우스 포인터를 **HTML** 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="fa63d-187">마우스 포인터를 움직이면 페이지 검사기 **HTML** 창에서 요소를 윤곽선으로 표시 하 고 브라우저 창에서 해당 요소를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 창](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="fa63d-189">이전 처럼 페이지 검사기 \_ 임시 탭에서 layout. cshtml 파일을 엽니다. \_ layout. cshtml 임시 탭을 클릭 &lt; 하면 헤더 섹션에서 해당 태그가 강조 표시 됩니다. &gt;</span><span class="sxs-lookup"><span data-stu-id="fa63d-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![강조 표시 된 태그](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="fa63d-191">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fa63d-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="fa63d-192">다음으로 페이지 검사기 **스타일** 창을 사용 하 여 CSS에 대 한 변경 내용을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="fa63d-193">**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa63d-194">페이지 검사기 브라우저 창에서 **div. 콘텐츠-래퍼** 레이블이 나타날 때까지 마우스 포인터를 "홈 페이지" 섹션으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="fa63d-196">Div. 콘텐츠-래퍼 섹션 내에서 한 번 클릭 한 다음 마우스 포인터를 **스타일** 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="fa63d-197">**스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="fa63d-198">아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="fa63d-199">이제 배경 색 속성에 대 한 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-199">Now clear the checkbox for the background-color property.</span></span>

![배경색 지우기](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="fa63d-201">페이지 검사기 브라우저 창에서 변경 내용이 즉시 미리 보기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="fa63d-202">확인란을 다시 선택 하 고 속성 값을 두 번 클릭 한 다음 빨강으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="fa63d-203">변경 내용이 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-203">The change shows immediately:</span></span>

![빨강 배경색](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="fa63d-205">스타일 **창을 사용** 하면 스타일 시트 자체에 변경 내용을 커밋하기 전에 CSS 변경을 쉽게 테스트 하 고 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="fa63d-206">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="fa63d-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="fa63d-207">이 기능을 사용 하려면 1.3 버전의 페이지 검사기 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="fa63d-208">CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="fa63d-209">**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa63d-210">페이지 검사기 브라우저에서 ' 홈 페이지 ' 섹션 위로 마우스 포인터를 이동 합니다. **콘텐츠-래퍼** 레이블이 나타날 때까지 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="fa63d-211">한 번 클릭 하 여이 요소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-211">Click once to select this element.</span></span>

<span data-ttu-id="fa63d-212">**스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="fa63d-213">아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="fa63d-214">"주요. 콘텐츠-래퍼"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="fa63d-215">페이지 검사기이 스타일 (.css)을 정의 하는 CSS 파일을 열고 해당 CSS 스타일을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="fa63d-216">이제의 값을 `background-color` "red"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="fa63d-217">변경 내용은 페이지 검사기 브라우저에 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="fa63d-218">CSS 색 선택 사용</span><span class="sxs-lookup"><span data-stu-id="fa63d-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="fa63d-219">Visual Studio 2012의 CSS 편집기에는 색을 쉽게 선택 하 고 삽입할 수 있는 색 선택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="fa63d-220">색 선택기는 색의 표준 색상표를 포함 하 고, 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며, 문서에서 가장 최근에 사용한 색의 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="fa63d-221">이전 섹션에서는 속성의 값을 변경 했습니다 `background-color` .</span><span class="sxs-lookup"><span data-stu-id="fa63d-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="fa63d-222">색 선택기를 호출 하려면 속성 이름 뒤에 삽입 지점을 놓고 **#** 또는 **rgb (**.</span><span class="sxs-lookup"><span data-stu-id="fa63d-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 색 선택 막대입니다.](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="fa63d-224">색을 클릭 하 여 선택 하거나 아래쪽 화살표 키를 누른 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="fa63d-225">색을 방문할 때 해당 16 진수 값을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![배경 색 속성 값 미리 보기](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="fa63d-227">색 막대에 원하는 정확한 색이 없으면 색 선택 팝업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="fa63d-228">이를 열려면 색 막대의 오른쪽 끝에 있는 이중 갈매기형 펼침 단추를 클릭 하거나 키보드에서 아래쪽 화살표를 한 번 또는 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 색 선택 팝업](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="fa63d-230">오른쪽의 세로 막대에서 색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="fa63d-231">이렇게 하면 주 창에 해당 색의 그라데이션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="fa63d-232">Enter 키를 눌러 세로 막대에서 색을 직접 선택 하거나 주 창에서 아무 점이 나 클릭 하 여 더 높은 정밀도로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="fa63d-233">사용 하려는 컴퓨터 화면에 색이 있는 경우 (Visual Studio 사용자 인터페이스 내부에 있을 필요가 없음) 오른쪽 아래에 있는 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="fa63d-234">색 선택 아래쪽의 슬라이더를 움직여 색의 불투명도를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="fa63d-235">이렇게 하면 RGBA 형식이 불투명을 나타낼 수 있기 때문에 색 값이 RGBA 값으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="fa63d-236">색을 선택한 후 Enter 키를 누른 후 세미콜론을 입력 하 여 *사이트 .css* 파일의 배경색 항목을 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="fa63d-237">페이지 검사기 업데이트 표시줄</span><span class="sxs-lookup"><span data-stu-id="fa63d-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="fa63d-238">페이지 검사기는 *사이트 .css* 파일의 변경 내용을 즉시 검색 하 고 업데이트 표시줄에 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![업데이트 표시줄](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="fa63d-240">모든 파일을 저장 하 고 페이지 검사기 브라우저를 새로 고치려면 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="fa63d-241">강조 표시 색의 변경 내용이 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="fa63d-242">JavaScript에 동적 페이지 요소 매핑</span><span class="sxs-lookup"><span data-stu-id="fa63d-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="fa63d-243">최신 웹 응용 프로그램에서는 페이지의 요소가 JavaScript를 사용 하 여 동적으로 생성 되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="fa63d-244">이는 이러한 페이지 요소에 해당 하는 정적 태그 (HTML 또는 Razor)가 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="fa63d-245">1.3 버전을 사용 하면 페이지에 동적으로 추가 된 항목을 해당 JavaScript 코드로 다시 매핑할 수 페이지 검사기.</span><span class="sxs-lookup"><span data-stu-id="fa63d-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="fa63d-246">이 기능을 설명 하기 위해 [SPA (단일 페이지 응용 프로그램) 템플릿을](../../../single-page-application/overview/introduction/knockoutjs-template.md)사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fa63d-247">SPA 템플릿에 [ASP.NET 및 Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 업데이트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="fa63d-248">Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="fa63d-249">왼쪽에서 **Visual c #** 을 확장 하 고 **웹**을 선택한 다음 **ASP.NET MVC4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="fa63d-250">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-250">Click **OK**.</span></span>

<span data-ttu-id="fa63d-251">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **단일 페이지 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="fa63d-252">솔루션 탐색기에서 **Views** 폴더를 확장 한 다음 **Home** 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="fa63d-253">Index cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="fa63d-254">페이지 검사기 브라우저에 표시 되는 첫 번째 작업은 로그인 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="fa63d-255">"등록"을 클릭 하 고 사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="fa63d-256">등록 하면 응용 프로그램은 사용자를 로그인 하 고 몇 가지 샘플 항목을 사용 하 여 할 일 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="fa63d-257">**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="fa63d-258">페이지 검사기 브라우저에서 할 일 항목 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="fa63d-259">파란색으로 강조 표시 되는 대신 요소가 주황색으로 강조 표시 되 고 요소 이름 옆에 "JS"가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="fa63d-260">이는 요소가 스크립트를 통해 동적으로 생성 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="fa63d-261">또한 **호출 스택** 탭에 주황색 밑줄이 표시 됩니다. 이는 **호출 스택** 창에 요소에 대 한 추가 정보가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="fa63d-262">**호출 스택** 탭을 클릭 합니다. **호출 스택** 창에는 요소를 만든 JavaScript 호출에 대 한 호출 스택이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="fa63d-263">JQuery와 같은 외부 라이브러리 호출이 축소 되어 응용 프로그램 스크립트에 대 한 호출을 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="fa63d-264">외부 라이브러리 호출을 포함 하 여 전체 스택을 보려면 "External library" 라는 레이블이 지정 된 노드를 확장 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="fa63d-265">호출 스택의 항목을 클릭 하면 Visual Studio에서 코드 파일을 열고 해당 스크립트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa63d-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="fa63d-266">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fa63d-266">See Also</span></span>

<span data-ttu-id="fa63d-267">[Visual Studio를 사용 하 여 ASP.NET MVC 4 소개](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 웹 사이트)</span><span class="sxs-lookup"><span data-stu-id="fa63d-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="fa63d-268">[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 비디오)</span><span class="sxs-lookup"><span data-stu-id="fa63d-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="fa63d-269">[페이지 검사기 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="fa63d-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
