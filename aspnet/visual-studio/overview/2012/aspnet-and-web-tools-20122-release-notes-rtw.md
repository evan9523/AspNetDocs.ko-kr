---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 및 웹 도구 2012.2 릴리스 노트 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 및 웹 도구 2012.2에 대한 릴리스 정보.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675906"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="1b76c-103">ASP.NET 및 Web Tools 2012.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="1b76c-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>

> <span data-ttu-id="1b76c-104">이 문서에서는 ASP.NET 및 웹 도구 2012.2의 릴리스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="1b76c-105">그것은 비주얼 스튜디오 웹 도구 및 ASP.NET 대한 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>

- [<span data-ttu-id="1b76c-106">설치 노트</span><span class="sxs-lookup"><span data-stu-id="1b76c-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="1b76c-107">문서</span><span class="sxs-lookup"><span data-stu-id="1b76c-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="1b76c-108">지원</span><span class="sxs-lookup"><span data-stu-id="1b76c-108">Support</span></span>](#_Support)
- [<span data-ttu-id="1b76c-109">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1b76c-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="1b76c-110">ASP.NET 및 웹 도구 2012.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="1b76c-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="1b76c-111">도구</span><span class="sxs-lookup"><span data-stu-id="1b76c-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="1b76c-112">웹 게시</span><span class="sxs-lookup"><span data-stu-id="1b76c-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="1b76c-113">ASP.NET MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="1b76c-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="1b76c-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="1b76c-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="1b76c-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="1b76c-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="1b76c-116">ASP.NET URL</span><span class="sxs-lookup"><span data-stu-id="1b76c-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="1b76c-117">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="1b76c-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="1b76c-118">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="1b76c-118">Installation Notes</span></span>

<span data-ttu-id="1b76c-119">ASP.NET 및 웹 도구 2012 Visual Studio 2012용 웹 [플랫폼 설치 관리자를](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="1b76c-120">이 업데이트는 웹용 Visual Studio 2012 또는 Visual Studio Express 2012에 대한 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="1b76c-121">Visual Studio가 설치되어 있지 않으면 웹용 Visual Studio Express 2012가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="1b76c-122">ASP.NET 및 웹 도구 2012.2를 수동으로 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="1b76c-123">웹에 대해 Visual Studio 2012 또는 Visual Studio Express 2012가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="1b76c-124">그런 다음 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="1b76c-125">다운로드 센터에서 [ASP.NET 및 웹 프레임워크 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 설치 프로그램을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="1b76c-126">메시지가 표시되면 실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-126">When prompted click Run.</span></span> <span data-ttu-id="1b76c-127">파일을 저장하여 나중에 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="1b76c-128">업데이트할 Visual Studio 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="1b76c-129">업데이트하려는 Visual Studio를 실행하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="1b76c-130">그런 다음 도움말 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="1b76c-131">웹용 Microsoft Visual &quot;Studio 2012에 대한&quot; 메뉴 항목이 표시되면 [웹 개발자 도구 2012.2 - Visual Studio Express 2012 웹을](https://go.microsoft.com/fwlink/?LinkID=282228)다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="1b76c-132">그렇지 않으면 [다운로드 웹 개발자 도구 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span><span class="sxs-lookup"><span data-stu-id="1b76c-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="1b76c-133">메시지가 표시되면 실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-133">When prompted click Run.</span></span> <span data-ttu-id="1b76c-134">파일을 저장하여 나중에 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="1b76c-135">ASP.NET 및 웹 도구 2012.2 릴리스에는 SQL Server 데이터 도구가 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="1b76c-136">SQL Server 및 Windows Azure SQL Databases는 오프라인 프로젝트 지원 개발, 스키마 비교 및 향상된 데이터베이스 배포 기능을 비롯한 다양한 데이터베이스 도구 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="1b76c-137">자세한 내용은 또는 SQL Server 데이터 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)도구를 설치하려면 을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="1b76c-138">문서화</span><span class="sxs-lookup"><span data-stu-id="1b76c-138">Documentation</span></span>

<span data-ttu-id="1b76c-139">ASP.NET 및 웹 도구 2012.2에 대한 자습서 및 기타 https://www.asp.net)정보는 ASP.NET 웹 사이트 (.</span><span class="sxs-lookup"><span data-stu-id="1b76c-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="1b76c-140">고객 지원팀</span><span class="sxs-lookup"><span data-stu-id="1b76c-140">Support</span></span>

<span data-ttu-id="1b76c-141">ASP.NET 및 웹 도구 2012.2는 공식적으로 릴리스 및 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="1b76c-142">일반 지원 채널을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-142">You can use your normal support channel.</span></span> <span data-ttu-id="1b76c-143">ASP.NET 커뮤니티 구성원이 자주 비공식적인[https://forums.asp.net/](https://forums.asp.net/)지원을 제공할 수 있는 ASP.NET 포럼()에 질문을 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="1b76c-144">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1b76c-144">Software Requirements</span></span>

<span data-ttu-id="1b76c-145">ASP.NET 및 웹 도구 2012.2에는 웹용 Visual Studio 2012 또는 Visual Studio Express 2012가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="1b76c-146">ASP.NET 및 웹 도구 2012.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="1b76c-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="1b76c-147">이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에서 소개된 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="1b76c-148">도구</span><span class="sxs-lookup"><span data-stu-id="1b76c-148">Tooling</span></span>

- <span data-ttu-id="1b76c-149">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="1b76c-149">Page Inspector</span></span> 

    - <span data-ttu-id="1b76c-150">페이지 검사기에서 페이지에 동적으로 추가된 항목을 해당 JavaScript 코드로 다시 매핑할 수 있도록 JavaScript 선택 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="1b76c-151">CSS업데이트를 실시간으로 확인할 수 있는 기능.</span><span class="sxs-lookup"><span data-stu-id="1b76c-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="1b76c-152">자세한 내용은 [페이지 검사기에서 CSS 자동 동기화 및 자바 스크립트 선택 매핑을](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="1b76c-153">편집기</span><span class="sxs-lookup"><span data-stu-id="1b76c-153">Editor</span></span> 

    - <span data-ttu-id="1b76c-154">커피스크립트, 콧수염, 핸들바 및 JSRender에 대한 강조 표시 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="1b76c-155">HTML 편집기는 녹아웃 바인딩에 대한 Intellisense를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="1b76c-156">LESS를 사용하여 동적 CSS를 구축할 수 있도록 적은 편집 및 컴파일러 지원.</span><span class="sxs-lookup"><span data-stu-id="1b76c-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="1b76c-157">JSON을 .NET 클래스로 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="1b76c-158">이 특수 붙여넣기 명령을 사용하여 JSON을 C# 또는 VB.NET 코드 파일에 붙여 넣으며 Visual Studio는 JSON에서 유추된 .NET 클래스를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="1b76c-159">모바일 에뮬레이터 지원은 확장성 후크를 추가하여 타사 에뮬레이터를 VSIX로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="1b76c-160">설치된 에뮬레이터는 F5 드롭다운에 표시되므로 개발자는 다양한 모바일 장치에서 웹 사이트를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="1b76c-161">이 기능에 대한 자세한 내용은 [Visual Studio와의 새로운 BrowserStack 통합에](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)대한 Scott Hanselman의 블로그 항목에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="1b76c-162">웹 게시</span><span class="sxs-lookup"><span data-stu-id="1b76c-162">Web Publishing</span></span>

- <span data-ttu-id="1b76c-163">이제 웹 사이트 프로젝트에 Windows Azure 웹 사이트에 게시하는 것을 비롯한 웹 응용 프로그램 프로젝트와 동일한 게시 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="1b76c-164">하나 이상의 파일에 대해 선택적 게시 &#8211; 다음 작업을 수행할 수 있습니다(웹 배포 끝점에 게시한 후):.</span><span class="sxs-lookup"><span data-stu-id="1b76c-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="1b76c-165">선택한 파일을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-165">Publish selected files.</span></span>
    - <span data-ttu-id="1b76c-166">로컬 파일과 원격 파일의 차이점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="1b76c-167">원격 파일로 로컬 파일을 업데이트하거나 로컬 파일로 원격 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="1b76c-168">ASP.NET MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="1b76c-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="1b76c-169">새로운 Facebook 응용 프로그램 템플릿 덕분에 Facebook Canvas 응용 프로그램을 쉽게 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="1b76c-170">간단한 몇 단계 만에 로그인한 사용자로부터 데이터를 가져오고 해당 사용자의 친구와 통합하는 Facebook 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="1b76c-171">템플릿에는 인증, 사용 권한, Facebook 데이터 액세스 등을 비롯하여 Facebook 응용 프로그램 작성과 관련된 모든 배관을 처리하기 위한 새 라이브러리가 포함되어 있어</span><span class="sxs-lookup"><span data-stu-id="1b76c-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="1b76c-172">Facebook 응용 프로그램 템플릿 사용에 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)대한 자세한 내용은 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="1b76c-173">새로운 단일 페이지 응용 프로그램 MVC 템플릿을 통해 개발자는 ASP.NET Web API뿐 아니라 HTML 5, CSS 3, 잘 알려진 Knockout 및 jQuery JavaScript 라이브러리를 사용하여 대화형 클라이언트 쪽 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="1b76c-174">템플릿에는 RESTful 서버 API를 사용하는 JavaScript HTML5 응용 프로그램을 빌드하는 일반적인 방법을 보여 주는 "할 일" 목록 응용 프로그램이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="1b76c-175">자세한 내용은 에서 [https://www.asp.net/single-page-application](../../../single-page-application/index.md)확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="1b76c-176">이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가하는 VSIX를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="1b76c-177">여기에서 방법을 알아보십시오.[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="1b76c-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="1b76c-178">FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿은 새로운 'FixedDisplayModes' NuGet 패키지를 포함 하도록 업데이트 되었습니다., MVC 4에서 버그에 대 한 해결 방법을 포함 하는.</span><span class="sxs-lookup"><span data-stu-id="1b76c-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="1b76c-179">패키지에 포함된 수정 문서에 대한 자세한 내용은 MVC[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)팀의 이 블로그 게시물()을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="1b76c-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="1b76c-180">ASP.NET Web API</span></span>

<span data-ttu-id="1b76c-181">ASP.NET 웹 API는 다음과 같은 몇 가지 새로운 기능으로 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="1b76c-182">ASP.NET 웹 API OData</span><span class="sxs-lookup"><span data-stu-id="1b76c-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="1b76c-183">ASP.NET 웹 API 추적</span><span class="sxs-lookup"><span data-stu-id="1b76c-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="1b76c-184">ASP.NET 웹 API 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="1b76c-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="1b76c-185">ASP.NET 웹 API OData</span><span class="sxs-lookup"><span data-stu-id="1b76c-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="1b76c-186">ASP.NET 웹 API OData는 모든 데이터 원본에 대한 풍부한 비즈니스 논리를 사용하여 OData 끝점을 구축하는 데 필요한 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="1b76c-187">ASP.NET 웹 API OData를 사용하면 노출하려는 OData 의미 체계의 양을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="1b76c-188">ASP.NET 웹 API OData는 ASP.NET MVC 4 프로젝트 템플릿에 포함되어[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)있으며 NuGet ()에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="1b76c-189">ASP.NET 웹 API OData는 현재 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="1b76c-190">[쿼리 가능] 특성을 적용하여 OData 쿼리 의미 체계를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="1b76c-191">OData 쿼리의 유효성을 쉽게 검사하고 지원되는 쿼리 옵션, 연산자 및 함수 집합을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="1b76c-192">매개 변수는 ODataQueryOptions에 직접 바인딩하여 IQueryable 또는 IEnumerable에 유효성을 검사하고 적용할 수 있는 쿼리의 추상 구문 트리 표현을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="1b76c-193">[쿼리 가능] 특성에 결과 제한을 지정하여 서비스 기반 페이징 및 다음 페이지 링크 생성을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="1b76c-194">$inlinecount 사용하여 일치하는 총 리소스 수의 인라인 된 수를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="1b76c-195">null 전파를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-195">Control null propagation.</span></span>
- <span data-ttu-id="1b76c-196">$filter 모든 연산자.</span><span class="sxs-lookup"><span data-stu-id="1b76c-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="1b76c-197">규칙에 따라 엔터티 데이터 모델을 추론하거나 엔터티 프레임워크 코드-First와 유사한 방식으로 모델을 명시적으로 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="1b76c-198">EntitySetController에서 파생 하여 엔터티 집합을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="1b76c-199">탐색 속성을 노출하고 링크를 조작하며 OData 작업을 구현하기 위한 간단하고 사용자 지정 가능한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="1b76c-200">MapODataRoute 확장 방법을 사용하여 간소화된 라우팅입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="1b76c-201">여러 EDM 모델을 노출하여 버전 전환 지원</span><span class="sxs-lookup"><span data-stu-id="1b76c-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="1b76c-202">웹 API에 대한 클라이언트(.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있도록 서비스 문서 및 $metadata 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="1b76c-203">OData 원자, JSON 및 JSON 자세한 형식에 대한 지원.</span><span class="sxs-lookup"><span data-stu-id="1b76c-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="1b76c-204">엔터티를 생성, 업데이트, 부분적으로 업데이트(PATCH) 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="1b76c-205">엔터티 간의 관계를 쿼리하고 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="1b76c-206">경로에 연결되는 관계 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="1b76c-207">복합 형식</span><span class="sxs-lookup"><span data-stu-id="1b76c-207">Complex types.</span></span>
- <span data-ttu-id="1b76c-208">엔터티 형식 상속입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="1b76c-209">컬렉션 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-209">Collection properties.</span></span>
- <span data-ttu-id="1b76c-210">열거형.</span><span class="sxs-lookup"><span data-stu-id="1b76c-210">Enums.</span></span>
- <span data-ttu-id="1b76c-211">OData 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-211">OData actions.</span></span>
- <span data-ttu-id="1b76c-212">WCF 데이터 서비스와 동일한 기반, 즉 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)()에 구축.</span><span class="sxs-lookup"><span data-stu-id="1b76c-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="1b76c-213">ASP.NET 웹 API OData에 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)대한 자세한 내용은 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="1b76c-214">ASP.NET 웹 API 추적</span><span class="sxs-lookup"><span data-stu-id="1b76c-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="1b76c-215">ASP.NET 웹 API 추적은 웹 API의 추적 데이터를 .NET 추적과 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="1b76c-216">이제 웹 API 프로젝트 템플릿에서 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="1b76c-217">웹 API에 대한 추적 데이터는 출력 창으로 전송되며 IntelliTrace를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="1b76c-218">ASP.NET 웹 API 추적을 사용하면 Windows Azure 진단과의 통합을 통해 Windows Azure에서 호스팅될 때 웹 API에 대한 정보를 [추적할 수 있습니다.](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)</span><span class="sxs-lookup"><span data-stu-id="1b76c-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="1b76c-219">ASP.NET 웹 API 추적 NuGet 패키지()를[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)사용하여 모든 응용 프로그램에서 ASP.NET 웹 API 추적을 설치하고 활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="1b76c-220">웹 API 추적을 구성하고 사용하는 방법에 대한 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)자세한 내용은 ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1b76c-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="1b76c-221">ASP.NET 웹 API 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="1b76c-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="1b76c-222">이제 ASP.NET 웹 API 도움말 페이지가 기본적으로 웹 API 프로젝트 템플릿에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="1b76c-223">ASP.NET 웹 API 도움말 페이지는 HTTP 끝점, 지원되는 HTTP 메서드, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함한 웹 API에 대한 설명서를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="1b76c-224">코드의 주석에서 설명서가 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="1b76c-225">ASP.NET 웹 API 도움말 페이지 NuGet 패키지 ()를[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)사용하여 모든 응용 프로그램에 ASP.NET 웹 API 도움말 페이지를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="1b76c-226">ASP.NET 웹 API 도움말 페이지를 설정하고 사용자 지정하는 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)방법에 대한 자세한 내용은 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="1b76c-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="1b76c-227">ASP.NET SignalR</span></span>

<span data-ttu-id="1b76c-228">ASP.NET SignalR을 사용하면 사용 가능한 경우 WebSockets를 사용하여 ASP.NET 응용 프로그램에 실시간 웹 기능을 쉽게 추가할 수 있으며 그렇지 않을 경우 자동으로 다른 기술로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="1b76c-229">ASP.NET 신호기 사용에 대한 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)자세한 내용은 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="1b76c-230">ASP.NET URL</span><span class="sxs-lookup"><span data-stu-id="1b76c-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="1b76c-231">ASP.NET FriendlyURLs를 사용하면 웹 양식 개발자가 .aspx 확장 없이 도서 URL을 더욱 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="1b76c-232">구성이 거의 또는 전혀 필요하지 않으며 기존 ASP.NET v4.0 응용 프로그램과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="1b76c-233">또한 FriendlyURLs 기능을 사용하면 데스크톱과 모바일 보기 간의 전환을 지원하여 개발자가 응용 프로그램에 모바일 지원을 더 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="1b76c-234">ASP.NET 사용 친화적 인 URL을 설치및 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)사용하는 방법에 대한 자세한 내용은 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="1b76c-235">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="1b76c-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="1b76c-236">이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에 있는 알려진 문제 및 주요 변경 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="1b76c-237">설치 이슈</span><span class="sxs-lookup"><span data-stu-id="1b76c-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="1b76c-238">비주얼 스튜디오 2012의 순서 에서 설치</span><span class="sxs-lookup"><span data-stu-id="1b76c-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="1b76c-239">ASP.NET 및 웹 도구 2012.2를 설치한 후 Visual Studio 2012의 SKU를 추가로 설치하려면 복구 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="1b76c-240">다음과 같은 시퀀스를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1b76c-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="1b76c-241">웹용 비주얼 스튜디오 2012 익스프레스 설치</span><span class="sxs-lookup"><span data-stu-id="1b76c-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="1b76c-242">ASP.NET 및 웹 도구 설치 2012.2</span><span class="sxs-lookup"><span data-stu-id="1b76c-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="1b76c-243">비주얼 스튜디오 설치 2012 전문가, 프리미엄 또는 궁극적 인</span><span class="sxs-lookup"><span data-stu-id="1b76c-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="1b76c-244">2단계는 웹용 Express용 업데이트만 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="1b76c-245">3단계에서 설치된 추가 SKU에 업데이트가 포함되어 있는지 확인하려면 ASP.NET 및 웹 도구 2012.2를 복구하여 마지막으로 설치된 SKU에 대한 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="1b76c-246">이는 1단계와 3단계의 SCO가 역전되는 경우에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="1b76c-247">Visual Studio가 열려 있을 때 Microsoft ASP.NET 및 웹 도구 설치 2012.2</span><span class="sxs-lookup"><span data-stu-id="1b76c-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="1b76c-248">MICROSOFT ASP.NET 및 웹 도구 2012.2를 설치하는 동안 VS가 열려 있으면 Visual Studio가 불량 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="1b76c-249">설치를 진행하기 전에 Visual Studio의 모든 인스턴스를 닫는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="1b76c-250">설치 중에 ASP.NET 및 웹 도구 2012.2 설치 취소</span><span class="sxs-lookup"><span data-stu-id="1b76c-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="1b76c-251">설치 중에 ASP.NET 및 웹 도구 2012.2 설정을 취소하면 Visual Studio가 불량 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="1b76c-252">이 문제를 해결하려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="1b76c-253">프로그램 추가/제거로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="1b76c-254">제거 마이크로 소프트 ASP.NET 웹 도구 2012.2, 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="1b76c-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="1b76c-255">마이크로소프트 ASP.NET 및 웹 도구 2012.2 다시 설치</span><span class="sxs-lookup"><span data-stu-id="1b76c-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="1b76c-256">ASP.NET 및 웹 도구 2012.2를 제거 한 후 ASP.NET MVC 4 템플릿 및 Razor v2 웹 사이트 템플릿이 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="1b76c-257">ASP.NET 및 웹 도구 2012.2를 제거하면 Visual Studio 2012에서 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿도 모두 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="1b76c-258">해결 방법은 Visual Studio 2012 설치를 복구하여 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿을 다시 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="1b76c-259">툴링 문제</span><span class="sxs-lookup"><span data-stu-id="1b76c-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="1b76c-260">NuGet 프로젝트 생성 중에 보고된 오류</span><span class="sxs-lookup"><span data-stu-id="1b76c-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="1b76c-261">ASP.NET 및 웹 도구 2012.2를 설치한 후 MVC 4 프로젝트를 만들 때 다음과 같은 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="1b76c-262">ASP.NET 및 웹 도구 2012.2는 NuGet 2.1을 제공하며 Visual Studio 2012에서 확장을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="1b76c-263">경우에 따라 VSIX 설치 프로그램이 VSIX를 올바르게 업데이트하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="1b76c-264">다음 단계를 통해 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="1b76c-265">관리자로 Visual Studio 2012 시작</span><span class="sxs-lookup"><span data-stu-id="1b76c-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="1b76c-266">도구-&gt;확장 및 업데이트로 이동하여 NuGet을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="1b76c-267">Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-267">Close Visual Studio</span></span>
4. <span data-ttu-id="1b76c-268">ASP.NET 및 웹 도구 2012.2 설치 폴더로 이동:</span><span class="sxs-lookup"><span data-stu-id="1b76c-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="1b76c-269">비주얼 스튜디오 2012: **프로그램 파일\마이크로소프트 ASP.NET\ASP.NET 웹 스택\비주얼 스튜디오 2012**</span><span class="sxs-lookup"><span data-stu-id="1b76c-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="1b76c-270">웹용 비주얼 스튜디오 2012 익스프레스: **프로그램 파일\Microsoft ASP.NET\ASP.NET 웹 스택\비주얼 스튜디오 익스프레스 2012 웹용**</span><span class="sxs-lookup"><span data-stu-id="1b76c-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="1b76c-271">NuGet.Tools.v6를 두 번 클릭하여 NuGet을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="1b76c-272">웹 API 문제</span><span class="sxs-lookup"><span data-stu-id="1b76c-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="1b76c-273">$filter 및 DateTime 리터럴의 구문 분석 문제</span><span class="sxs-lookup"><span data-stu-id="1b76c-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="1b76c-274">OData URI 파서는 부분 datetime 리터럴을 제대로 구문 분석하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="1b76c-275">예를 들어 $filter=시작 eq datetime'2012-12-31T12:00'이 제대로 구문 분석되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="1b76c-276">해결 방법은 전체 리터럴 $filter=start eq datetime'2012-12-31T12:00:00'를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="1b76c-277">OData대/소문자를 구분하지 않는 속성 이름을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="1b76c-278">OData는 OData 쿼리 및 odata 경로에서 대/소문자를 구분하지 않는 속성 이름을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="1b76c-279">작업 항목 보기:</span><span class="sxs-lookup"><span data-stu-id="1b76c-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="1b76c-280">사용자가 자바 스크립트 클라이언트 측과 서버 측에서 다른 대/소문자를 가지고 있다면 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="1b76c-281">이 문제는 odata 프로토콜의 설계에 의한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="1b76c-282">그러나 많은 사용자가이 문제를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-282">However, many users reports this issue.</span></span> <span data-ttu-id="1b76c-283">이 방법을 해결하려면 사용자가 URL에서 서비스 케이스를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="1b76c-284">기본 OData 라우팅 규칙은 탐색 속성에 POST/PUT을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="1b76c-285">기본 OData 라우팅 규칙은 탐색 속성에 POST/PUT을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="1b76c-286">작업 항목 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="1b76c-287">기본 규칙에서 일반적으로 사용되는 이 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="1b76c-288">이 방법을 해결하려면 이를 지원하기 위해 새 라우팅 규칙을 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="1b76c-289">페이스 북 템플릿 문제</span><span class="sxs-lookup"><span data-stu-id="1b76c-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="1b76c-290">페이스 북 응용 프로그램 템플릿은 .NET 4.5를 사용하여 작동</span><span class="sxs-lookup"><span data-stu-id="1b76c-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="1b76c-291">새 프로젝트 대화 상자의 프레임워크 드롭다운 목록에서 .NET 4.5를 선택하여 MVC 4에서 Facebook 응용 프로그램 템플릿을 ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1b76c-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="1b76c-292">실시간 업데이트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b76c-292">Real-time Update Controller</span></span>

<span data-ttu-id="1b76c-293">페이스 북 응용 프로그램 템플릿은 사용자가 쉽게 페이스 북에서 실시간 업데이트를 처리하는 웹 API 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="1b76c-294">개발 컴퓨터가 NAT 뒤에 있는 경우 추가 네트워크 구성 없이 컨트롤러가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="1b76c-295">자세한 내용은 여기를 참조하십시오.[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="1b76c-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="1b76c-296">쿼리 문자열 값은 Facebook OAuth 매개 변수와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="1b76c-297">다음 필드는 Facebook OAuth 대화 상자의 호출 다시 URL과 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="1b76c-298">코드, 오류, 오류\_설명, 오류\_이유 : 다음 이름으로 자신의 쿼리 문자열 값을 추가하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1b76c-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="1b76c-299">페이스 북 템플릿페이지 관리자를 사용하여</span><span class="sxs-lookup"><span data-stu-id="1b76c-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="1b76c-300">Facebook 응용 프로그램을 디버깅하는 동안 Visual Studio 2012의 페이지 검사기 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="1b76c-301">페이지 검사기는 현재 iframes를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="1b76c-302">단일 페이지 응용 프로그램 템플릿 문제</span><span class="sxs-lookup"><span data-stu-id="1b76c-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="1b76c-303">JQuery 1.9/녹아웃 2.2.1 업데이트를 사용하면 기본 MVC SPA 프로젝트를 실행할 때 새 할 일 항목 편집 enter 포커스 이벤트가 제대로 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="1b76c-304">JQuery 1.9/녹아웃 2.2.1 업데이트를 통해 기본 MVC SPA 프로젝트를 실행할 때 새로운 할 일 항목 편집이 더 이상 새 할 일 항목을 할 일 목록에 입력한 후 새 할 일 항목 편집 상자에 다시 초점을 맞추지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="1b76c-305">해결 방법 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)참조 및 다음 샘플 코드와 유사한 수정을 수행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="1b76c-306">파일 todo.model.js</span><span class="sxs-lookup"><span data-stu-id="1b76c-306">File todo.model.js</span></span>  
 <span data-ttu-id="1b76c-307">함수 todolist(데이터)를 추가하고 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="1b76c-308">**self.is선택 = ko.관찰 가능(false);**</span><span class="sxs-lookup"><span data-stu-id="1b76c-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="1b76c-309">함수 todoList.prototype.addTodo, 다음 검게 칠한 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="1b76c-310">**self.is선택됨(true);**</span><span class="sxs-lookup"><span data-stu-id="1b76c-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="1b76c-311">self.newTodoTitle&quot;&quot;();</span><span class="sxs-lookup"><span data-stu-id="1b76c-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="1b76c-312">File index.cshtml을 추가하고 다음 검정 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b76c-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="1b76c-313">&lt;양식 데이터 바인딩=&quot;제출: addTodo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="1b76c-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="1b76c-314">&lt;입력 클래스&quot;=&quot; addTodo&quot; type =&quot;&quot;텍스트 데이터 바인딩 = 값: newTodoTitle, 자리 표시자: '추가하려면 여기 입력', blurOnEnter: true, **hasfocus: 선택됨**, 이벤트: { 흐림: addTodo }&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="1b76c-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="1b76c-315">&lt;/양식&gt;</span><span class="sxs-lookup"><span data-stu-id="1b76c-315">&lt;/form&gt;</span></span>
