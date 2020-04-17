---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 비주얼 스튜디오를 사용하여 웹 페이지(Razor)ASP.NET 프로그래밍 | 마이크로 소프트 문서
author: Rick-Anderson
description: 이 부록에서는 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용하여 ASP.NET 웹 페이지를 Razor 구문으로 프로그래밍하는 방법을 설명합니다.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542900"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="68e21-103">비주얼 스튜디오를 사용하여 웹 페이지(Razor)ASP.NET 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="68e21-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="68e21-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="68e21-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="68e21-105">이 문서에서는 Visual Studio 또는 Visual Web Developer Express를 사용하여 ASP.NET 웹 페이지(Razor) 웹 사이트를 프로그래밍하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="68e21-106">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="68e21-106">What you'll learn</span></span>
>
> - <span data-ttu-id="68e21-107">Visual Studio 버전의 ASP.NET 웹 페이지로 작업하려면 설치해야 하는 사항(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="68e21-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="68e21-108">비주얼 웹 개발자 2010 익스프레스에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="68e21-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="68e21-109">IntelliSense 및 디버거를 포함하여 ASP.NET Razor 페이지와 함께 작업하는 비주얼 스튜디오에서 기능을 사용하는 방법.</span><span class="sxs-lookup"><span data-stu-id="68e21-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="68e21-110">튜토리얼에 사용되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="68e21-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="68e21-111">ASP.NET 웹 페이지 (면도기) 3</span><span class="sxs-lookup"><span data-stu-id="68e21-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="68e21-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="68e21-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="68e21-113">웹 매트릭스 3</span><span class="sxs-lookup"><span data-stu-id="68e21-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="68e21-114">이 자습서에서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="68e21-115">WebMatrix 또는 다른 많은 코드 편집기에서 Razor 구문으로 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="68e21-116">또한 웹 사이트뿐만 아니라 다양한 유형의 응용 프로그램을 만들기 위한 강력한 도구 집합을 제공하는 IDE(모든 기능을 갖춘 통합 개발 환경)인 Microsoft Visual Studio를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="68e21-117">ASP.NET Razor 페이지로 작업하려면 [Visual Studio 2017을](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="68e21-118">Visual Studio에서 Razor 웹 페이지를 ASP.NET 프로그래밍에 제공하는 두 가지 유용한 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="68e21-119">*인텔리센스*.</span><span class="sxs-lookup"><span data-stu-id="68e21-119">*IntelliSense*.</span></span> <span data-ttu-id="68e21-120">비주얼 스튜디오에 내장 된 IntelliSense 기능은 웹 매트릭스에서 IntelliSense보다 더 포괄적이다.</span><span class="sxs-lookup"><span data-stu-id="68e21-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="68e21-121">*디버거*.</span><span class="sxs-lookup"><span data-stu-id="68e21-121">*Debugger*.</span></span> <span data-ttu-id="68e21-122">디버거를 사용하면 프로그램을 실행하는 동안 중지하고, 변수를 검사하고, 코드 줄을 한 줄씩 단계별로 단계별로 실행하여 코드 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="68e21-123">ASP.NET 웹 페이지의 다른 버전과 함께 Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="68e21-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="68e21-124">Visual Studio 2017에서 ASP.NET 웹 앱을 개발하려면 **ASP.NET 및 웹 개발** 워크로드를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="68e21-125">Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대한 지원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="68e21-126">(ASP.NET 웹 페이지를 지원하기 위해 필요한 패키지는 Visual Studio를 설치할 때 설치됩니다.)</span><span class="sxs-lookup"><span data-stu-id="68e21-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="68e21-127">Visual Studio 2010에는 ASP.NET 웹 페이지에 대한 지원이 기본적으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="68e21-128">Visual Studio 2010에서 ASP.NET 웹 페이지를 사용하려면 ASP.NET MVC 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="68e21-129">웹 페이지 2를 ASP.NET 위해 MVC 4를 ASP.NET 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="68e21-130">다음 표에는 여러 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대한 지원이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="68e21-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="68e21-131">Visual Studio 2010</span></span> | <span data-ttu-id="68e21-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="68e21-132">Visual Studio 2012</span></span> | <span data-ttu-id="68e21-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="68e21-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68e21-134">**ASP.NET 웹 페이지 2**</span><span class="sxs-lookup"><span data-stu-id="68e21-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="68e21-135">MVC 4에 ASP.NET 설치</span><span class="sxs-lookup"><span data-stu-id="68e21-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="68e21-136">(포함)</span><span class="sxs-lookup"><span data-stu-id="68e21-136">(Included)</span></span> | <span data-ttu-id="68e21-137">(포함)</span><span class="sxs-lookup"><span data-stu-id="68e21-137">(Included)</span></span> |
| <span data-ttu-id="68e21-138">**ASP.NET 웹 페이지 3**</span><span class="sxs-lookup"><span data-stu-id="68e21-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="68e21-139">NuGet을 통해 ASP.NET 웹 페이지 3으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="68e21-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="68e21-140">(포함)</span><span class="sxs-lookup"><span data-stu-id="68e21-140">(Included)</span></span> |

<span data-ttu-id="68e21-141">Visual Studio 2010에서 작업하려면 [Visual Studio 2010의 ASP.NET 웹 페이지에 대한 지원 설치를](#vs2010support)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="68e21-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="68e21-142">웹매트릭스에서 비주얼 스튜디오 시작</span><span class="sxs-lookup"><span data-stu-id="68e21-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="68e21-143">WebMatrix에서 프로젝트를 시작하고 Visual Studio로 전환하려는 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 열 수 있는 단추를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="68e21-144">이 단추를 사용하려면 컴퓨터에 Visual Studio가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="68e21-145">다음 이미지는 WebMatrix의 단추를 보여 주며,</span><span class="sxs-lookup"><span data-stu-id="68e21-145">The following image shows the button in WebMatrix.</span></span>

![비주얼 스튜디오 시작](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="68e21-147">단추를 클릭하면 프로젝트가 Visual Studio에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="68e21-148">WebMatrix와 Visual Studio 간에 아무런 문제 없이 앞뒤로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="68e21-149">다른 환경에서 파일이 변경되었으며 최신 변경 내용을 얻으려면 다시 로드해야 하는 경우 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="68e21-150">비주얼 스튜디오에서 ASP.NET 면도기 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="68e21-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="68e21-151">Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면 다음 단계를 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="68e21-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="68e21-152">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="68e21-153">**파일** 메뉴에서 **새 웹 사이트를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-153">In the **File** menu, click **New Web Site**.</span></span>

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="68e21-155">새 **웹 사이트** 대화 상자에서 사용할 언어(Visual C# 또는 Visual Basic)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="68e21-156">ASP.NET **웹 사이트(Razor)** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![면도기 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="68e21-158">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-158">Click **OK**.</span></span>

<span data-ttu-id="68e21-159">새 프로젝트가 존재하며 시작하는 데 도움이 되는 몇 가지 기본 웹 페이지가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="68e21-160">IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="68e21-160">Using IntelliSense</span></span>

<span data-ttu-id="68e21-161">이제 사이트를 만들었으니 Visual Studio에서 IntelliSense가 어떻게 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="68e21-162">방금 만든 웹 사이트에서 *Default.cshtml* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="68e21-163">페이지의 `<h3>` 태그 후 점 포함을 입력합니다. `@ServerInfo.`</span><span class="sxs-lookup"><span data-stu-id="68e21-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="68e21-164">IntelliSense가 드롭다운 목록에서 `ServerInfo` 도우미에 사용할 수 있는 메서드를 표시하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="68e21-166">목록에서 `GetHtml` 메서드를 선택한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="68e21-167">IntelliSense는 자동으로 메서드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="68e21-168">C#의 모든 메서드와 마찬가지로 메서드 `()` 다음의 문자를 추가해야 합니다. 메서드에 `GetHtml` 대 한 완료 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="68e21-169">페이지를 실행하려면 Ctrl+F5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="68e21-170">브라우저에 표시될 때 페이지의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-170">This is what the page looks like when displayed in a browser:</span></span>

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="68e21-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="68e21-173">디버거 사용</span><span class="sxs-lookup"><span data-stu-id="68e21-173">Using the Debugger</span></span>

1. <span data-ttu-id="68e21-174">*Default.cshtml* 페이지 의 맨 위에 는 `Page.Title`로 시작하는 줄 다음에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="68e21-175">코드 왼쪽에 있는 편집기의 회색 여백에서 이 새 줄 옆을 클릭하여 *중단점을 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="68e21-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="68e21-176">중단점은 디버거에게 해당 시점에서 프로그램 실행을 중지하도록 지시하는 마커이므로 무슨 일이 일어나고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="68e21-178">`ServerInfo.GetHtml` 메서드에 대한 호출을 제거하고 해당 위치에 `@myTime` 있는 변수에 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="68e21-179">이 호출은 새 코드 줄에서 반환되는 현재 시간 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="68e21-180">F5를 눌러 디버거에서 페이지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="68e21-181">페이지는 설정한 중단점에서 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="68e21-182">다음 이미지는 중단점(노란색)이 있는 편집기에서 페이지의 모양을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="68e21-184">디버그 도구 모음에서 **단계 입력** 단추(또는 F11 를 누르기)를 클릭하여 다음 코드 줄을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="68e21-185">이 단추를 클릭할 때마다 다음 코드 줄로 실행을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![버튼으로 단계](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="68e21-187">마우스 포인터를 `myTime` 위에 놓거나 **지역 변수** 및 **콜 스택** 창에 표시된 값을 검사하여 변수값을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="68e21-188">Visual Studio는 변수의 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-188">Visual Studio display the value of the variable.</span></span>

    ![시간 값 표시](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="68e21-190">변수를 검사하고 코드를 단계별로 실행하면 F5를 눌러 각 줄에서 멈추지 않고 페이지를 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="68e21-191">모든 코드를 단계적 단계적 단계로 완료하면 브라우저에 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="68e21-192">디버거 및 Visual Studio에서 코드를 디버깅하는 방법에 대한 자세한 내용은 [연습: 비주얼 웹 개발자의 웹 페이지 디버깅을](https://msdn.microsoft.com/library/z9e7w6cs.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="68e21-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="68e21-193">비주얼 스튜디오와 ASP.NET MVC 프로젝트에서 면도기 사용</span><span class="sxs-lookup"><span data-stu-id="68e21-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="68e21-194">Razor 구문은 ASP.NET MVC 프로젝트에서도 광범위하게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="68e21-195">MVC는 동적 웹 사이트를 구축하는 강력한 패턴 기반 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="68e21-196">ASP.NET 웹 페이지 사이트를 유지 관리하기 어려워지면 ASP.NET MVC 응용 프로그램으로 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="68e21-197">MVC 응용 프로그램을 만드는 예제는 [ASP.NET MVC 5로 시작하기 를](../../../mvc/overview/getting-started/introduction/getting-started.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="68e21-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="68e21-198">Visual Studio 2010에서 ASP.NET 웹 페이지에 대한 지원 설치</span><span class="sxs-lookup"><span data-stu-id="68e21-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="68e21-199">이 섹션에서는 Visual Web Developer Express 2010 및 ASP.NET 웹 페이지 도구를 시각적 스튜디오용으로 설치하는 방법을 보여 주며, 이 섹션에서는 다음과 같은 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="68e21-200">웹 플랫폼 설치 관리자가 아직 없는 경우 다음 URL에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="68e21-201">웹 플랫폼 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="68e21-202">**제품** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-202">Click the **Products** tab.</span></span>

    ![웹PI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="68e21-204">ASP.NET **MVC 4(ASP.NET** 웹 페이지 2의 경우)를 검색한 다음 **에 추가를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="68e21-205">이러한 제품에는 ASP.NET Razor 웹 사이트를 구축하기 위한 Visual Studio 도구가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="68e21-207">설치를 **Install** 클릭하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="68e21-207">Click **Install** to complete the installation.</span></span>
