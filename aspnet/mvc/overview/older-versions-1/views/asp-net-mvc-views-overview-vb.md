---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 뷰 개요 (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 뷰는 무엇 이며 HTML 페이지와 어떻게 다릅니까? 이 자습서에서는 Stephen Walther가 보기를 소개 하 고, 다음을 수행할 수 있는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044668"
---
# <a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="47a5c-104">ASP.NET MVC 보기 개요(VB)</span><span class="sxs-lookup"><span data-stu-id="47a5c-104">ASP.NET MVC Views Overview (VB)</span></span>

<span data-ttu-id="47a5c-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="47a5c-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="47a5c-106">ASP.NET MVC 뷰는 무엇 이며 HTML 페이지와 어떻게 다릅니까?</span><span class="sxs-lookup"><span data-stu-id="47a5c-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="47a5c-107">이 자습서에서 Stephen Walther는 뷰를 소개 하 고 뷰 내에서 뷰 데이터 및 HTML 도우미를 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="47a5c-108">이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="47a5c-109">이 자습서의 끝 부분에서는 새 뷰를 만들고, 컨트롤러에서 뷰로 데이터를 전달 하 고, HTML 도우미를 사용 하 여 보기에서 콘텐츠를 생성 하는 방법을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="47a5c-110">뷰 이해</span><span class="sxs-lookup"><span data-stu-id="47a5c-110">Understanding Views</span></span>

<span data-ttu-id="47a5c-111">ASP.NET 또는 Active Server 페이지와 달리 ASP.NET MVC에는 페이지에 직접 해당 하는 항목이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="47a5c-112">ASP.NET MVC 응용 프로그램에서 브라우저의 주소 표시줄에 입력 하는 URL의 경로에 해당 하는 페이지가 디스크에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="47a5c-113">ASP.NET MVC 응용 프로그램의 페이지에 가장 가까운 항목은 *뷰*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="47a5c-114">ASP.NET MVC 응용 프로그램에서 들어오는 브라우저 요청은 컨트롤러 작업에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="47a5c-115">컨트롤러 작업에서 뷰를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-115">A controller action might return a view.</span></span> <span data-ttu-id="47a5c-116">그러나 컨트롤러 작업은 다른 유형의 작업 (예: 다른 컨트롤러 작업으로 리디렉션)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="47a5c-117">목록 1은 HomeController 라는 간단한 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="47a5c-118">HomeController는 Index () 및 Details () 라는 두 개의 컨트롤러 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="47a5c-119">**목록 1-HomeController**</span><span class="sxs-lookup"><span data-stu-id="47a5c-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="47a5c-120">브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 작업 인 Index () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="47a5c-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="47a5c-121">/Home/Index</span></span>

<span data-ttu-id="47a5c-122">브라우저에이 주소를 입력 하 여 두 번째 작업 인 Details () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="47a5c-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="47a5c-123">/Home/Details</span></span>

<span data-ttu-id="47a5c-124">Index () 작업은 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-124">The Index() action returns a view.</span></span> <span data-ttu-id="47a5c-125">사용자가 만드는 대부분의 작업은 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-125">Most actions that you create will return views.</span></span> <span data-ttu-id="47a5c-126">그러나 작업은 다른 유형의 작업 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="47a5c-127">예를 들어 Details () 작업은 들어오는 요청을 Index () 작업으로 리디렉션하는 RedirectToActionResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="47a5c-128">Index () 작업에는 다음 코드 줄 하나가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="47a5c-129">보기 ()</span><span class="sxs-lookup"><span data-stu-id="47a5c-129">View()</span></span>

<span data-ttu-id="47a5c-130">이 코드 줄은 웹 서버의 다음 경로에 있어야 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="47a5c-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="47a5c-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="47a5c-132">뷰의 경로는 컨트롤러 이름 및 컨트롤러 작업의 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="47a5c-133">선호 하는 경우 보기에 대해 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="47a5c-134">다음 코드 줄은 Fred 라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="47a5c-135">보기 (Fred)</span><span class="sxs-lookup"><span data-stu-id="47a5c-135">View( Fred )</span></span>

<span data-ttu-id="47a5c-136">이 코드 줄을 실행 하면 다음 경로에서 뷰가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="47a5c-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="47a5c-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47a5c-138">ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들려는 경우 뷰 이름에 대해 명시적으로 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="47a5c-139">이렇게 하면 단위 테스트를 만들어 컨트롤러 작업에서 예상한 뷰가 반환 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="47a5c-140">뷰에 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="47a5c-140">Adding Content to a View</span></span>

<span data-ttu-id="47a5c-141">뷰는 스크립트를 포함할 수 있는 표준 (X) HTML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="47a5c-142">스크립트를 사용 하 여 동적 콘텐츠를 뷰에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="47a5c-143">예를 들어 목록 2의 보기는 현재 날짜 및 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="47a5c-144">**목록 2-\Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="47a5c-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="47a5c-145">목록 2에 있는 HTML 페이지의 본문에는 다음 스크립트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="47a5c-146">&lt;% Response. Write (DateTime. Now)%&gt;</span><span class="sxs-lookup"><span data-stu-id="47a5c-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="47a5c-147">스크립트 구분 기호% 및%를 사용 하 여 &lt; &gt; 스크립트의 시작과 끝을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="47a5c-148">이 스크립트는 Visual basic으로 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-148">This script is written in Visual basic.</span></span> <span data-ttu-id="47a5c-149">브라우저에 콘텐츠를 렌더링 하는 Write () 메서드를 호출 하 여 현재 날짜 및 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="47a5c-150">스크립트 구분 기호 &lt; % 및%는 &gt; 하나 이상의 문을 실행 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="47a5c-151">자주 Write ()를 호출 하므로 Microsoft는 Response () 메서드를 호출 하는 바로 가기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="47a5c-152">목록 3의 뷰에서는 &lt; % = 및% 구분 기호를 &gt; 호출 하 여 Write () 호출을 위한 바로 가기로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="47a5c-153">**목록 3-Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="47a5c-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="47a5c-154">모든 .NET 언어를 사용 하 여 뷰에서 동적 콘텐츠를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="47a5c-155">일반적으로 Visual Basic .NET 또는 c #을 사용 하 여 컨트롤러 및 뷰를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-155">Normally, you'll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="47a5c-156">HTML 도우미를 사용 하 여 뷰 콘텐츠 생성</span><span class="sxs-lookup"><span data-stu-id="47a5c-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="47a5c-157">보기에 콘텐츠를 더 쉽게 추가할 수 있도록 *HTML 도우미*라는 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="47a5c-158">일반적으로 HTML 도우미는 문자열을 생성 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="47a5c-159">HTML 도우미를 사용 하 여 텍스트 상자, 링크, 드롭다운 목록 및 목록 상자와 같은 표준 HTML 요소를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="47a5c-160">예를 들어 목록 4의 뷰는 세 가지 HTML 도우미 인 Html.beginform (), TextBox () 및 Password () 도우미를 사용 하 여 로그인 폼을 생성 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="47a5c-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="47a5c-161">**목록 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="47a5c-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

<span data-ttu-id="47a5c-162">[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47a5c-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="47a5c-163">**그림 01**: 표준 로그인 양식 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="47a5c-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="47a5c-164">모든 HTML 도우미 메서드는 뷰의 Html 속성에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="47a5c-165">예를 들어, Html. TextBox () 메서드를 호출 하 여 텍스트 상자를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="47a5c-166">&lt; &gt; Html. TextBox () 및 Html. Password () 도우미를 모두 호출할 때 스크립트 구분 기호% = 및%를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="47a5c-167">이러한 도우미는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-167">These helpers simply return a string.</span></span> <span data-ttu-id="47a5c-168">브라우저에 문자열을 렌더링 하기 위해 Write ()를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="47a5c-169">HTML 도우미 메서드 사용은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="47a5c-170">이러한 작업을 수행 하면 작성 해야 하는 HTML 및 스크립트의 양이 줄어들어 더 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="47a5c-171">목록 5의 뷰는 HTML 도우미를 사용 하지 않고 목록 4의 뷰와 정확히 동일한 폼을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="47a5c-172">**목록 5--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="47a5c-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="47a5c-173">사용자 고유의 HTML 도우미를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="47a5c-174">예를 들어, HTML 테이블에 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView () 도우미 메서드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="47a5c-175">**사용자 지정 HTML 도우미 만들기**자습서의이 항목을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="47a5c-176">뷰 데이터를 사용 하 여 보기에 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="47a5c-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="47a5c-177">데이터 보기를 사용 하 여 컨트롤러에서 보기로 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="47a5c-178">메일을 통해 보내는 패키지와 같은 뷰 데이터를 생각해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="47a5c-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="47a5c-179">컨트롤러에서 뷰로 전달 된 모든 데이터는이 패키지를 사용 하 여 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="47a5c-180">예를 들어 목록 6의 컨트롤러는 데이터를 볼 수 있도록 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="47a5c-181">**목록 6-제품 컨트롤러 .vb**</span><span class="sxs-lookup"><span data-stu-id="47a5c-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="47a5c-182">Controller ViewData 속성은 이름/값 쌍의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="47a5c-183">목록 6에서 Index () 메서드는 값이 Hello World! 인 message 라는 뷰 데이터 컬렉션에 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="47a5c-184">Index () 메서드에서 뷰를 반환 하는 경우 뷰 데이터는 뷰에 자동으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="47a5c-185">목록 7의 뷰는 보기 데이터에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="47a5c-186">**목록 7--\Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="47a5c-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="47a5c-187">뷰에서는 메시지를 렌더링할 때 Html 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="47a5c-188">Html. 인코드 () HTML 도우미는 및와 같은 특수 문자 &lt; 를 &gt; 웹 페이지에 표시 하기에 안전한 문자로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="47a5c-189">사용자가 웹 사이트로 전송 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="47a5c-190">(제품 컨트롤러에서 메시지를 직접 만들었기 때문에 메시지를 인코딩할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-190">(Because we created the message ourselves in the ProductController, we don't really need to encode the message.</span></span> <span data-ttu-id="47a5c-191">그러나 뷰 내의 뷰 데이터에서 검색 된 콘텐츠를 표시 하는 경우 항상 Html. 인코드 () 메서드를 호출 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="47a5c-192">목록 7에서는 보기 데이터를 활용 하 여 컨트롤러에서 뷰로 간단한 문자열 메시지를 전달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="47a5c-193">데이터 보기를 사용 하 여 컨트롤러에서 보기에 데이터베이스 레코드 컬렉션과 같은 다른 유형의 데이터를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="47a5c-194">예를 들어 Products 데이터베이스 테이블의 내용을 뷰에 표시 하려면 데이터 보기에서 데이터베이스 레코드의 컬렉션을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="47a5c-195">또한 컨트롤러에서 뷰로 강력한 형식의 뷰 데이터를 전달 하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="47a5c-196">**강력한 형식의 뷰 데이터 및 뷰 이해**자습서의이 항목을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="47a5c-197">요약</span><span class="sxs-lookup"><span data-stu-id="47a5c-197">Summary</span></span>

<span data-ttu-id="47a5c-198">이 자습서에서는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="47a5c-199">첫 번째 섹션에서는 프로젝트에 새 뷰를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="47a5c-200">특정 컨트롤러에서 호출 하려면 보기를 오른쪽 폴더에 추가 해야 한다는 것을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="47a5c-201">다음으로 HTML 도우미 항목에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="47a5c-202">HTML 도우미를 사용 하 여 표준 HTML 콘텐츠를 쉽게 생성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="47a5c-203">마지막으로, 보기 데이터를 활용 하 여 컨트롤러에서 보기로 데이터를 전달 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="47a5c-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="47a5c-204">[이전](passing-data-to-view-master-pages-cs.md)
> [다음](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="47a5c-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>
