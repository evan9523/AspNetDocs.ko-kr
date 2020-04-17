---
uid: visual-studio/overview/2013/release-notes
title: 비주얼 스튜디오 2013 릴리스 노트를 위한 ASP.NET 및 웹 도구 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구 릴리스에 대해 설명합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543498"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="70bfb-103">Visual Studio 2013용 ASP.NET 및 Web Tools 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="70bfb-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="70bfb-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="70bfb-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="70bfb-105">이 문서에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구 릴리스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="70bfb-106">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="70bfb-106">Contents</span></span>

- [<span data-ttu-id="70bfb-107">설치 노트</span><span class="sxs-lookup"><span data-stu-id="70bfb-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="70bfb-108">문서</span><span class="sxs-lookup"><span data-stu-id="70bfb-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="70bfb-109">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="70bfb-110">비주얼 스튜디오 2013을 위한 ASP.NET 및 웹 도구의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="70bfb-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="70bfb-111">ASP.NET 1개</span><span class="sxs-lookup"><span data-stu-id="70bfb-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="70bfb-112">새로운 웹 프로젝트 환경</span><span class="sxs-lookup"><span data-stu-id="70bfb-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="70bfb-113">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="70bfb-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="70bfb-114">브라우저 링크</span><span class="sxs-lookup"><span data-stu-id="70bfb-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="70bfb-115">비주얼 스튜디오 웹 에디터 개선 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="70bfb-116">비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="70bfb-117">웹 게시 개선 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="70bfb-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="70bfb-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="70bfb-119">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="70bfb-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="70bfb-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="70bfb-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="70bfb-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="70bfb-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="70bfb-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="70bfb-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="70bfb-123">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="70bfb-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="70bfb-124">마이크로 소프트 오윈 구성 요소</span><span class="sxs-lookup"><span data-stu-id="70bfb-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="70bfb-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="70bfb-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="70bfb-126">ASP.NET 면도기 3</span><span class="sxs-lookup"><span data-stu-id="70bfb-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="70bfb-127">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="70bfb-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="70bfb-128">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="70bfb-129">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-129">Installation Notes</span></span>

<span data-ttu-id="70bfb-130">ASP.NET 및 Visual Studio 2013용 웹 도구는 기본 설치 관리자에 번들로 [제공됩니다.](https://www.asp.net/downloads)</span><span class="sxs-lookup"><span data-stu-id="70bfb-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="70bfb-131">문서화</span><span class="sxs-lookup"><span data-stu-id="70bfb-131">Documentation</span></span>

<span data-ttu-id="70bfb-132">Visual Studio 2013을 위한 ASP.NET 및 웹 도구에 대한 자습서 및 기타 정보는 [ASP.NET 웹 사이트에서](https://www.asp.net/)확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="70bfb-133">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-133">Software Requirements</span></span>

<span data-ttu-id="70bfb-134">ASP.NET 및 웹 도구에는 Visual Studio 2013이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="70bfb-135">비주얼 스튜디오 2013을 위한 ASP.NET 및 웹 도구의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="70bfb-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="70bfb-136">다음 섹션에서는 릴리스에서 도입된 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="70bfb-137">ASP.NET 1개</span><span class="sxs-lookup"><span data-stu-id="70bfb-137">One ASP.NET</span></span>

<span data-ttu-id="70bfb-138">Visual Studio 2013의 출시와 함께, 우리는 당신이 쉽게 혼합하고 당신이 원하는 것들을 일치시킬 수 있도록, ASP.NET 기술을 사용하는 경험을 통합하는 쪽으로 단계를 촬영하고있다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="70bfb-139">예를 들어 MVC를 사용하여 프로젝트를 시작하고 나중에 프로젝트에 웹 양식 페이지를 쉽게 추가하거나 웹 폼 프로젝트에서 웹 API를 스캐폴드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="70bfb-140">한 가지 ASP.NET 개발자가 ASP.NET 좋아하는 일을 더 쉽게 할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="70bfb-141">어떤 기술을 선택하든 One ASP.NET 신뢰할 수 있는 기본 프레임워크를 구축하고 있다는 확신을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="70bfb-142">새로운 웹 프로젝트 환경</span><span class="sxs-lookup"><span data-stu-id="70bfb-142">New Web Project Experience</span></span>

<span data-ttu-id="70bfb-143">Visual Studio 2013에서 새로운 웹 프로젝트를 만드는 경험을 향상시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="70bfb-144">새 **ASP.NET 웹 프로젝트** 대화 상자에서 원하는 프로젝트 유형을 선택하고, 기술 조합(웹 양식, MVC, 웹 API)을 구성하고, 인증 옵션을 구성하고, 단위 테스트 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

<span data-ttu-id="70bfb-146">새 대화 상자를 사용하면 많은 템플릿에 대한 기본 인증 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="70bfb-147">예를 들어 ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="70bfb-148">인증 없음</span><span class="sxs-lookup"><span data-stu-id="70bfb-148">No Authentication</span></span>
- <span data-ttu-id="70bfb-149">개인 사용자 계정(ASP.NET 멤버십 또는 소셜 공급자 로그인)</span><span class="sxs-lookup"><span data-stu-id="70bfb-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="70bfb-150">조직 계정(인터넷 응용 프로그램의 활성 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="70bfb-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="70bfb-151">Windows 인증(인트라넷 응용 프로그램의 활성 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="70bfb-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![인증 옵션](release-notes/_static/image2.png)

<span data-ttu-id="70bfb-153">웹 프로젝트를 만드는 새로운 프로세스에 대한 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기를](creating-web-projects-in-visual-studio.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="70bfb-154">새 인증 옵션에 대한 자세한 내용은 이 문서의 ASP.NET [ID를](#TOC8) 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="70bfb-155">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="70bfb-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="70bfb-156">ASP.NET 스캐폴딩은 ASP.NET 웹 응용 프로그램을 위한 코드 생성 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="70bfb-157">데이터 모델과 상호 작용하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="70bfb-158">이전 버전의 Visual Studio에서는 스캐폴딩이 ASP.NET MVC 프로젝트로 제한되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="70bfb-159">Visual Studio 2013을 사용하면 이제 웹 양식을 비롯한 모든 ASP.NET 프로젝트에 스캐폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="70bfb-160">Visual Studio 2013은 현재 Web Forms 프로젝트에 대한 페이지 생성을 지원하지 않지만 프로젝트에 MVC 종속성을 추가하여 웹 양식과 함께 스캐폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="70bfb-161">웹 양식에 대한 페이지 생성에 대한 지원은 향후 업데이트에 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="70bfb-162">스캐폴딩을 사용할 때 필요한 모든 종속성이 프로젝트에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="70bfb-163">예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스캐폴딩을 사용하여 웹 API 컨트롤러를 추가하는 경우 필요한 NuGet 패키지 및 참조가 프로젝트에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="70bfb-164">웹 양식 프로젝트에 MVC 스캐폴딩을 추가하려면 **새 스캐폴드 항목을** 추가하고 대화 상자 창에서 **MVC 5 종속성을** 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="70bfb-165">스캐폴딩 MVC에는 두 가지 옵션이 있습니다. 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="70bfb-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="70bfb-166">최소를 선택하면 ASP.NET MVC에 대한 NuGet 패키지 및 참조만 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="70bfb-167">전체 옵션을 선택하면 MVC 프로젝트에 필요한 콘텐츠 파일뿐만 아니라 최소 종속성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="70bfb-168">비동기 컨트롤러 스캐폴딩에 대한 지원은 엔터티 프레임워크 6의 새 비동기 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="70bfb-169">자세한 정보 및 자습서는 [ASP.NET 스캐폴딩 개요를](aspnet-scaffolding-overview.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="70bfb-170">브라우저 링크 - 브라우저와 비주얼 스튜디오 사이의 신호 채널</span><span class="sxs-lookup"><span data-stu-id="70bfb-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="70bfb-171">새로운 [브라우저 링크](using-browser-link.md) 기능을 사용하면 도구 모음에서 단추를 클릭하여 여러 브라우저를 Visual Studio에 연결하고 모두 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="70bfb-172">모바일 에뮬레이터를 포함하여 여러 브라우저를 개발 사이트에 연결하고 새로 고침을 클릭하여 모든 브라우저를 동시에 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="70bfb-173">또한 브라우저 링크는 개발자가 브라우저 링크 확장을 작성할 수 있도록 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="70bfb-174">개발자가 브라우저 링크 API를 활용할 수 있도록 하면 Visual Studio와 연결된 브라우저 간의 경계를 넘나들 수 있는 매우 진보된 시나리오를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="70bfb-175">Web Essentials는 API를 활용하여 Visual Studio와 브라우저의 개발자 도구, 원격 제어 모바일 에뮬레이터 및 기타 여러 가지 통합 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="70bfb-176">비주얼 스튜디오 웹 에디터 개선 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="70bfb-177">Visual Studio 2013에는 Razor 파일및 웹 애플리케이션의 HTML 파일에 대한 새로운 HTML 편집기가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="70bfb-178">새 HTML 편집기는 HTML5를 기반으로 하는 단일 통합 스키마를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="70bfb-179">그것은 자동 중괄호 완료, jQuery UI 및 AngularJS 속성 IntelliSense, 속성 IntelliSense 그룹화, ID 및 클래스 이름 Intellisense, 그리고 더 나은 성능을 포함 하 여 다른 개선, 서식 및 SmartTags.</span><span class="sxs-lookup"><span data-stu-id="70bfb-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="70bfb-180">다음 스크린샷은 HTML 편집기에서 부트스트랩 속성 IntelliSense를 사용하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 편집기의 인텔리센스](release-notes/_static/image4.png)

<span data-ttu-id="70bfb-182">비주얼 스튜디오 2013 또한 함께 제공 커피 스크립트와 LESS 편집기 내장.</span><span class="sxs-lookup"><span data-stu-id="70bfb-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="70bfb-183">LESS 편집기는 CSS 편집기의 모든 멋진 기능과 함께 제공되며 체인의 모든 LESS 문서에 걸쳐 @import 변수와 혼합에 대한 특정 Intellisense가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="70bfb-184">비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="70bfb-185">.NET 2.2에 대한 Azure SDK를 사용하는 Visual Studio 2013에서는 **서버 탐색기를** 사용하여 원격 웹 앱과 직접 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="70bfb-186">Azure 계정에 로그인하고, 새 웹 앱을 만들고, 앱을 구성하고, 실시간 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="70bfb-187">SDK 2.2가 출시된 후 곧 Azure에서 디버그 모드에서 원격으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="70bfb-188">Azure App Service 웹 앱에 대한 대부분의 새로운 기능은 .NET에 대한 Azure SDK의 현재 릴리스를 설치할 때 Visual Studio 2012에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="70bfb-189">자세한 내용은 다음 자료를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70bfb-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="70bfb-190">Azure 앱 서비스에서 ASP.NET 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="70bfb-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="70bfb-191">Visual Studio를 사용하여 Azure App Service에서 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="70bfb-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="70bfb-192">웹 게시 개선 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-192">Web Publish Enhancements</span></span>

<span data-ttu-id="70bfb-193">Visual Studio 2013에는 새롭고 향상된 웹 게시 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="70bfb-194">다음은 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-194">Here are a few of them:</span></span>

- <span data-ttu-id="70bfb-195">[Web.config 파일 암호화를](https://go.microsoft.com/fwlink/?LinkId=325529)쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="70bfb-196">(이 링크와 다음 두 가지 는 MSDN에 대한 설명서를 10/17에 늦게까지 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="70bfb-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="70bfb-197">배포 하는 동안 응용 프로그램을 오프라인으로 전환하는 것을 쉽게 [자동화할 수 있습니다.](https://go.microsoft.com/fwlink/?LinkId=325530)</span><span class="sxs-lookup"><span data-stu-id="70bfb-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="70bfb-198">서버에 복사할 파일을 결정하기 위해 [마지막으로 변경된 날짜 대신 파일 체크섬을 사용하도록](https://go.microsoft.com/fwlink/?LinkId=325531) 웹 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="70bfb-199">FTP 또는 파일 시스템 게시 메서드와 웹 배포를 사용할 때 선택한 개별 파일(Web.config 포함)을 빠르게 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="70bfb-200">ASP.NET 웹 배포에 대한 자세한 내용은 [ASP.NET 사이트를](https://go.microsoft.com/fwlink/?LinkId=322027)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="70bfb-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="70bfb-201">NuGet 2.7</span></span>

<span data-ttu-id="70bfb-202">NuGet 2.7에는 [NuGet 2.7 릴리스 노트에서](http://docs.nuget.org/docs/release-notes/nuget-2.7)자세히 설명하는 풍부한 새로운 기능 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="70bfb-203">또한 이 버전의 NuGet은 패키지를 다운로드하기 위해 NuGet의 패키지 복원 기능에 대한 명시적인 동의를 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="70bfb-204">NuGet의 기본 설정 대화 상자에서 연결된 확인란에 대한 동의가 이제 NuGet을 설치하여 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="70bfb-205">이제 패키지 복원은 기본적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="70bfb-206">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="70bfb-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="70bfb-207">ASP.NET 1개</span><span class="sxs-lookup"><span data-stu-id="70bfb-207">One ASP.NET</span></span>

<span data-ttu-id="70bfb-208">Web Forms 프로젝트 템플릿은 새로운 One ASP.NET 환경과 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="70bfb-209">Web Forms 프로젝트에 MVC 및 웹 API 지원을 추가할 수 있으며 One ASP.NET 프로젝트 만들기 마법사를 사용하여 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="70bfb-210">자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기를](creating-web-projects-in-visual-studio.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="70bfb-211">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="70bfb-211">ASP.NET Identity</span></span>

<span data-ttu-id="70bfb-212">Web Forms 프로젝트 템플릿은 새 ASP.NET ID 프레임워크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="70bfb-213">또한 이제 템플릿이 웹 양식 인트라넷 프로젝트 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="70bfb-214">자세한 내용은 Visual Studio **2013에서 ASP.NET 웹 프로젝트 만들기의** [인증 방법을](creating-web-projects-in-visual-studio.md#auth) 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="70bfb-215">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="70bfb-215">Bootstrap</span></span>

<span data-ttu-id="70bfb-216">Web Forms 템플릿은 [부트스트랩을](http://twitter.github.io/bootstrap/) 사용하여 매끄럽고 반응성이 뛰어난 모양과 느낌을 쉽게 사용자 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="70bfb-217">자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿의 부트스트랩을](creating-web-projects-in-visual-studio.md#bootstrap)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="70bfb-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="70bfb-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="70bfb-219">ASP.NET 1개</span><span class="sxs-lookup"><span data-stu-id="70bfb-219">One ASP.NET</span></span>

<span data-ttu-id="70bfb-220">Web MVC 프로젝트 템플릿은 새로운 One ASP.NET 환경과 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="70bfb-221">MVC 프로젝트를 사용자 지정하고 One ASP.NET 프로젝트 만들기 마법사를 사용하여 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="70bfb-222">MVC 5를 ASP.NET 입문 튜토리얼은 [ASP.NET MVC 5로 시작하기에서](../../../mvc/overview/getting-started/introduction/getting-started.md)찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="70bfb-223">MVC 4 프로젝트를 MVC 5로 업그레이드하는 방법에 대한 자세한 내용은 [MVC 5 및 웹 API 2를 ASP.NET ASP.NET MVC 4 및 웹 API 프로젝트를 업그레이드하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="70bfb-224">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="70bfb-224">ASP.NET Identity</span></span>

<span data-ttu-id="70bfb-225">MVC 프로젝트 템플릿이 ASP.NET ID를 인증 및 ID 관리에 사용하도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="70bfb-226">페이스북과 구글 인증 및 새로운 멤버십 API를 특징으로 하는 튜토리얼은 [페이스북과 구글 OAuth2, OpenID 사인온을 통해 ASP.NET MVC 5 앱 만들기에서](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 찾을 수 있으며, [인증 및 SQL DB가 있는 ASP.NET MVC 앱을 생성하고 Azure 앱 서비스에 배포할](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="70bfb-227">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="70bfb-227">Bootstrap</span></span>

<span data-ttu-id="70bfb-228">MVC 프로젝트 템플릿은 부트 [스트랩을](http://getbootstrap.com/) 사용하여 매끄럽고 반응성이 뛰어난 모양과 느낌을 쉽게 사용자 정의 할 수 있도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="70bfb-229">자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿의 부트스트랩을](creating-web-projects-in-visual-studio.md#bootstrap)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="70bfb-230">인증 필터</span><span class="sxs-lookup"><span data-stu-id="70bfb-230">Authentication filters</span></span>

<span data-ttu-id="70bfb-231">인증 필터는 ASP.NET MVC 파이프라인에서 권한 부여 필터 이전에 실행되고 모든 컨트롤러에 대해 작업당 인증 논리, 컨트롤러별 또는 전역을 지정할 수 있는 ASP.NET MVC의 새로운 종류의 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="70bfb-232">인증 필터는 요청에서 자격 증명을 처리하고 해당 보안 주체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="70bfb-233">인증 필터는 승인되지 않은 요청에 대한 응답으로 인증 문제를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="70bfb-234">필터 재정의</span><span class="sxs-lookup"><span data-stu-id="70bfb-234">Filter overrides</span></span>

<span data-ttu-id="70bfb-235">이제 재정의 필터를 지정하여 지정된 작업 메서드 또는 컨트롤러에 적용되는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="70bfb-236">필터 재정의는 지정된 범위(작업 또는 컨트롤러)에 대해 실행해서는 안 되는 필터 유형 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="70bfb-237">이렇게 하면 전역적으로 적용되는 필터를 구성한 다음 특정 전역 필터가 특정 작업 또는 컨트롤러에 적용되지 않도록 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="70bfb-238">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="70bfb-238">Attribute routing</span></span>

<span data-ttu-id="70bfb-239">ASP.NET MVC는 이제 [http://attributerouting.net](http://attributerouting.net)의 저자 팀 맥콜의 기여 덕분에 특성 라우팅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="70bfb-240">특성 라우팅을 사용하면 작업 및 컨트롤러에 추가하여 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="70bfb-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="70bfb-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="70bfb-242">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="70bfb-242">Attribute routing</span></span>

<span data-ttu-id="70bfb-243">ASP.NET 웹 API는 이제 의 작성자인 Tim McCall의 기여 [http://attributerouting.net](http://attributerouting.net)덕분에 특성 라우팅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="70bfb-244">특성 라우팅을 사용하면 다음과 같이 작업 및 컨트롤러에 추가하여 Web API 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="70bfb-245">특성 라우팅을 사용하면 웹 API의 URI를 보다 세한 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="70bfb-246">예를 들어 단일 API 컨트롤러를 사용하여 리소스 계층 구조를 쉽게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="70bfb-247">특성 라우팅은 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정하기 위한 편리한 구문도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="70bfb-248">특성 라우팅에 대한 자세한 내용은 [웹 API 2의 특성 라우팅을](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="70bfb-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="70bfb-249">OAuth 2.0</span></span>

<span data-ttu-id="70bfb-250">이제 웹 API 및 단일 페이지 응용 프로그램 응용 프로그램 템플릿은 OAuth 2.0을 사용하여 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="70bfb-251">OAuth 2.0은 보호된 리소스에 대한 클라이언트 액세스 권한을 부여하기 위한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="70bfb-252">그것은 브라우저와 모바일 장치를 포함한 클라이언트의 다양한 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="70bfb-253">OAuth 2.0에 대한 지원은 권한을 부여 서버 역할을 구현하기 위해 Microsoft OWIN 구성 요소에서 제공하는 새로운 보안 미들웨어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="70bfb-254">또는 Windows Server 2012 R2의 Azure Active Directory 또는 ADFS와 같은 조직 권한 부여 서버를 사용하여 클라이언트를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="70bfb-255">O데이터 개선 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-255">OData Improvements</span></span>

<span data-ttu-id="70bfb-256">**$select, $expand, $batch 및 $value 지원**</span><span class="sxs-lookup"><span data-stu-id="70bfb-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="70bfb-257">ASP.NET 웹 API OData는 이제 $select, $expand 및 $value 대한 완전한 지원을 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="70bfb-258">변경 집합의 일괄 처리 및 처리 요청에 $batch 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="70bfb-259">$select 및 $expand 옵션을 사용하면 OData 끝점에서 반환되는 데이터의 모양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="70bfb-260">자세한 내용은 [웹 API OData에서 $select 및 $expand 지원 소개를](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="70bfb-261">**향상된 확장성**</span><span class="sxs-lookup"><span data-stu-id="70bfb-261">**Improved extensibility**</span></span>

<span data-ttu-id="70bfb-262">이제 OData 포터가 확장가능해졌습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="70bfb-263">Atom 항목 메타데이터를 추가하고, 명명된 스트림 및 미디어 링크 항목을 지원하고, 인스턴스 주석을 추가하고, 링크가 생성되는 방식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="70bfb-264">**유형 없는 지원**</span><span class="sxs-lookup"><span data-stu-id="70bfb-264">**Type-less support**</span></span>

<span data-ttu-id="70bfb-265">이제 엔터티 형식에 대한 CLR 형식을 정의할 필요 없이 OData 서비스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="70bfb-266">대신 OData 컨트롤러는 직렬화/역직렬화에 대한 OData formatters인 **IEdmObject의**인스턴스를 사용하거나 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="70bfb-267">**기존 모델 재사용**</span><span class="sxs-lookup"><span data-stu-id="70bfb-267">**Reuse an existing model**</span></span>

<span data-ttu-id="70bfb-268">이미 EDM(기존 엔터티 데이터 모델)이 있는 경우 새 엔터티 데이터 모델을 빌드하는 대신 직접 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="70bfb-269">예를 들어 엔터티 프레임워크를 사용하는 경우 EF가 빌드하는 EDM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="70bfb-270">일괄 처리 요청</span><span class="sxs-lookup"><span data-stu-id="70bfb-270">Request Batching</span></span>

<span data-ttu-id="70bfb-271">요청 일괄 처리는 여러 작업을 단일 HTTP POST 요청으로 결합하여 네트워크 트래픽을 줄이고 보다 원활하고 덜 수다스러운 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="70bfb-272">ASP.NET 웹 API는 이제 요청 일괄 처리에 대한 몇 가지 전략을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="70bfb-273">OData 서비스의 $batch 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="70bfb-274">여러 요청을 단일 MIME 다중 파트 요청으로 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="70bfb-275">사용자 지정 일괄 처리 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-275">Use a custom batching format.</span></span>

<span data-ttu-id="70bfb-276">요청 일괄 처리를 사용하려면 일괄 처리기가 있는 경로를 웹 API 구성에 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="70bfb-277">요청 또는 순차적 또는 임의의 순서로 실행할지 여부를 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="70bfb-278">휴대용 ASP.NET 웹 API 클라이언트</span><span class="sxs-lookup"><span data-stu-id="70bfb-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="70bfb-279">이제 ASP.NET 웹 API 클라이언트를 사용하여 Windows 스토어 및 Windows Phone 8 응용 프로그램에서 작동하는 이식 가능한 클래스 라이브러리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="70bfb-280">클라이언트와 서버 간에 공유할 수 있는 이식 가능한 포matters를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="70bfb-281">향상된 테스트 용이성</span><span class="sxs-lookup"><span data-stu-id="70bfb-281">Improved Testability</span></span>

<span data-ttu-id="70bfb-282">웹 API 2를 사용하면 API 컨트롤러를 훨씬 쉽게 단위 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="70bfb-283">요청 메시지 및 구성으로 API 컨트롤러를 인스턴스화한 다음 테스트하려는 작업 메서드를 호출하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="70bfb-284">링크 생성을 수행하는 작업 메서드에 대해 **UrlHelper** 클래스를 조롱하는 것도 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="70bfb-285">IHttpAction결과</span><span class="sxs-lookup"><span data-stu-id="70bfb-285">IHttpActionResult</span></span>

<span data-ttu-id="70bfb-286">이제 IHttpActionResult를 구현하여 웹 API 작업 메서드의 결과를 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="70bfb-287">웹 API 작업 메서드에서 반환된 IHttpActionResult는 ASP.NET 웹 API 런타임에 의해 실행되어 결과 응답 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="70bfb-288">IHttpActionResult 웹 API 구현의 단위 테스트를 단순화 하기 위해 모든 웹 API 작업에서 반환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="70bfb-289">편의를 위해 특정 상태 코드, 서식이 지정된 콘텐츠 또는 콘텐츠 협상 응답을 반환하는 결과를 포함하여 여러 IHttpActionResult 구현이 즉시 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="70bfb-290">HttpRequest컨텍스트</span><span class="sxs-lookup"><span data-stu-id="70bfb-290">HttpRequestContext</span></span>

<span data-ttu-id="70bfb-291">새 **HttpRequestContext는** 요청에 연결되지만 요청에서 즉시 사용할 수 없는 모든 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="70bfb-292">예를 들어 **HttpRequestContext를** 사용하여 경로 데이터, 요청과 연결된 주 서버, 클라이언트 인증서, **UrlHelper** 및 가상 경로 루트를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="70bfb-293">단위 테스트를 위해 **HttpRequestContext를** 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="70bfb-294">요청에 대한 주 서버는 **Thread.CurrentPrincipal에**의존하는 대신 요청과 함께 흐르므로 웹 API 파이프라인에 있는 동안 요청의 수명 동안 보안 주체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="70bfb-295">CORS</span><span class="sxs-lookup"><span data-stu-id="70bfb-295">CORS</span></span>

<span data-ttu-id="70bfb-296">브록 앨런의 또 다른 큰 기여 덕분에, ASP.NET 이제 완전히 크로스 오리진 요청 공유 (CORS)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="70bfb-297">브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="70bfb-298">[CORS는](http://www.w3.org/TR/cors/) 서버가 동일한 원본 정책을 완화할 수 있는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="70bfb-299">CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="70bfb-300">이제 웹 API 2는 사전 비행 요청의 자동 처리를 포함하여 CORS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="70bfb-301">자세한 내용은 [ASP.NET 웹 API에서 크로스-원본 리소스 요청 사용](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70bfb-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="70bfb-302">인증 필터</span><span class="sxs-lookup"><span data-stu-id="70bfb-302">Authentication Filters</span></span>

<span data-ttu-id="70bfb-303">인증 필터는 ASP.NET 웹 API 파이프라인의 권한 부여 필터 이전에 실행되고 모든 컨트롤러에 대해 작업당 인증 논리, 컨트롤러별 또는 전역을 지정할 수 있는 ASP.NET 웹 API의 새로운 종류의 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="70bfb-304">인증 필터는 요청에서 자격 증명을 처리하고 해당 보안 주체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="70bfb-305">인증 필터는 승인되지 않은 요청에 대한 응답으로 인증 문제를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="70bfb-306">필터 재정의</span><span class="sxs-lookup"><span data-stu-id="70bfb-306">Filter Overrides</span></span>

<span data-ttu-id="70bfb-307">이제 재정의 필터를 지정하여 지정된 작업 메서드 또는 컨트롤러에 적용되는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="70bfb-308">필터 재정의는 지정된 범위(작업 또는 컨트롤러)에 대해 실행되지 않아야 하는 필터 유형 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="70bfb-309">이렇게 하면 전역 필터를 추가한 다음 특정 작업 또는 컨트롤러에서 일부를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="70bfb-310">오윈 통합</span><span class="sxs-lookup"><span data-stu-id="70bfb-310">OWIN Integration</span></span>

<span data-ttu-id="70bfb-311">ASP.NET 웹 API는 이제 OWIN을 완벽하게 지원하며 OWIN 가능한 호스트에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="70bfb-312">OWIN 인증 시스템과의 통합을 제공하는 **호스트 인증 필터도** 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="70bfb-313">OWIN 통합을 사용하면 SignalR과 같은 다른 OWIN 미들웨어와 함께 자체 프로세스에서 웹 API를 자체 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="70bfb-314">자세한 내용은 [OWIN에서 셀프 호스트ASP.NET 웹 API를 참조하십시오.](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)</span><span class="sxs-lookup"><span data-stu-id="70bfb-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="70bfb-315">ASP.NET 시그널R 2.0</span><span class="sxs-lookup"><span data-stu-id="70bfb-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="70bfb-316">다음 섹션에서는 SignalR 2.0의 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="70bfb-317">오윈에 내장</span><span class="sxs-lookup"><span data-stu-id="70bfb-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="70bfb-318">맵허브와 맵연결이 이제 맵시널R로 바됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="70bfb-319">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="70bfb-320">모노 터치와 모노 드로이드를 통해 아이폰 OS와 안드로이드 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="70bfb-321">휴대용 .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="70bfb-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="70bfb-322">새로운 셀프 호스트 패키지</span><span class="sxs-lookup"><span data-stu-id="70bfb-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="70bfb-323">이전 버전과 호환되는 서버 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="70bfb-324">.NET 4.0에 대한 서버 지원 제거</span><span class="sxs-lookup"><span data-stu-id="70bfb-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="70bfb-325">클라이언트 및 그룹 목록에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="70bfb-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="70bfb-326">특정 사용자에게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="70bfb-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="70bfb-327">더 나은 오류 처리 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="70bfb-328">허브의 간편한 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="70bfb-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="70bfb-329">자바 스크립트 오류 처리</span><span class="sxs-lookup"><span data-stu-id="70bfb-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="70bfb-330">기존 1.x 프로젝트를 SignalR 2.0으로 업그레이드하는 방법의 예는 [SignalR 1.x 프로젝트 업그레이드를](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="70bfb-331">오윈에 내장</span><span class="sxs-lookup"><span data-stu-id="70bfb-331">Built on OWIN</span></span>

<span data-ttu-id="70bfb-332">SignalR 2.0은 [OWIN(.NET용 개방형 웹 인터페이스)에](http://owin.org/)완전히 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="70bfb-333">이러한 변경으로 인해 SignalR에 대한 설정 프로세스가 웹 호스팅 및 자체 호스팅 SignalR 응용 프로그램 간에 훨씬 더 일관되게 유지되지만 여러 API 변경이 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="70bfb-334">맵허브와 맵연결이 이제 맵시널R로 바됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="70bfb-335">OWIN 표준과의 호환성을 위해 이러한 메서드의 이름이 로 `MapSignalR`변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="70bfb-336">`MapSignalR`매개 변수없이 호출 (버전 1.x에서와 같이) `MapHubs` 모든 허브를 매핑합니다; 개별 **PersistentConnection** 개체를 매핑하려면 연결 형식을 형식 매개 변수로 지정하고 연결에 대한 URL 확장을 첫 번째 인수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="70bfb-337">메서드는 `MapSignalR` Owin 시작 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="70bfb-338">Visual Studio 2013에는 Owin 시작 클래스에 대한 새 템플릿이 포함되어 있습니다. 이 템플릿을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="70bfb-339">프로젝트를 마우스 오른쪽 버튼으로 클릭</span><span class="sxs-lookup"><span data-stu-id="70bfb-339">Right-click on the project</span></span>
2. <span data-ttu-id="70bfb-340">추가 , **새 항목 선택...** **Add**</span><span class="sxs-lookup"><span data-stu-id="70bfb-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="70bfb-341">**오윈 시작 클래스를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="70bfb-342">새 클래스의 이름을 **Startup.cs.**</span><span class="sxs-lookup"><span data-stu-id="70bfb-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="70bfb-343">웹 **응용 프로그램에서** 메서드를 `MapSignalR` 포함하는 Owin 시작 클래스는 아래와 같이 Web.Config 파일의 응용 프로그램 설정 노드에 있는 항목을 사용하여 Owin의 시작 프로세스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="70bfb-344">자체 **호스팅 응용 프로그램에서**시작 클래스는 `WebApp.Start` 메서드의 형식 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="70bfb-345">**SignalR 1.x의 허브 및 연결 매핑(웹 응용 프로그램의 전역 응용 프로그램 파일에서):**</span><span class="sxs-lookup"><span data-stu-id="70bfb-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="70bfb-346">**SignalR 2.0의 허브 및 연결 매핑(Owin Startup 클래스 파일에서):**</span><span class="sxs-lookup"><span data-stu-id="70bfb-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="70bfb-347">자체 **호스팅 응용 프로그램에서**Startup 클래스는 아래와 같이 `WebApp.Start` 메서드의 형식 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="70bfb-348">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-348">Cross-Domain Support</span></span>

<span data-ttu-id="70bfb-349">SignalR 1.x에서 교차 도메인 요청은 단일 EnableCrossDomain 플래그에 의해 제어되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="70bfb-350">이 플래그는 JSONP 및 CORS 요청을 모두 제어했습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="70bfb-351">유연성을 높이기 위해 모든 CORS 지원이 SignalR의 서버 구성 요소에서 제거되었습니다(JavaScript 클라이언트는 브라우저가 지원하는 것으로 감지되는 경우 CORS를 정상적으로 사용함) 이러한 시나리오를 지원하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="70bfb-352">SignalR 2.0에서 JSONP가 클라이언트에 필요한 경우(이전 브라우저에서 도메인 간 요청을 지원하려면) 아래와 `EnableJSONP` 같이 `HubConfiguration` 개체를 `true`설정하여 명시적으로 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="70bfb-353">JSONP는 CORS보다 안전하지 때문에 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="70bfb-354">SignalR 2.0에 새 CORS 미들웨어를 `Microsoft.Owin.Cors` 추가하려면 아래 섹션과 `UseCors` 같이 프로젝트에 라이브러리를 추가하고 SignalR 미들웨어 전에 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="70bfb-355">**프로젝트에 Microsoft.Owin.Cors 추가**: 이 라이브러리를 설치하려면 패키지 관리자 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="70bfb-356">이 명령은 2.0.0 버전의 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="70bfb-357">**유즈코르 스**</span><span class="sxs-lookup"><span data-stu-id="70bfb-357">**Calling UseCors**</span></span>

<span data-ttu-id="70bfb-358">다음 코드 조각은 SignalR 1.x 및 2.0에서 도메인 간 연결을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="70bfb-359">**SignalR 1.x에서 도메인 간 요청 구현(글로벌 응용 프로그램 파일에서)**</span><span class="sxs-lookup"><span data-stu-id="70bfb-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="70bfb-360">**SignalR 2.0에서 도메인 간 요청 구현(C# 코드 파일)에서**</span><span class="sxs-lookup"><span data-stu-id="70bfb-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="70bfb-361">다음 코드는 SignalR 2.0 프로젝트에서 CORS 또는 JSONP를 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="70bfb-362">이 코드 `Map` 샘플은 `RunSignalR` `MapSignalR`CORS 미들웨어가 CORS 지원이 필요한 SignalR 요청에 대해서만 실행되도록 을 대신 사용하며 `MapSignalR`.에 지정된 경로의 모든 트래픽에 대해 실행됩니다. `Map` 또한 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행해야 하는 다른 미들웨어에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="70bfb-363">모노 터치와 모노 드로이드를 통해 아이폰 OS와 안드로이드 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="70bfb-364">[자마린 라이브러리에서](https://xamarin.com/)모노터치 및 MonoDroid 구성 요소를 사용하여 iOS 및 Android 클라이언트에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="70bfb-365">사용 방법에 대한 자세한 내용은 [Xamarin 구성 요소 사용을](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="70bfb-366">이러한 구성 요소는 SignalR RTW 릴리스를 사용할 수 있을 때 [Xamarin 스토어에서](https://store.xamarin.com/) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="70bfb-367">### 휴대용 .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="70bfb-367">### Portable .NET client</span></span>

<span data-ttu-id="70bfb-368">플랫폼 간 개발을 보다 용이하게 하기 위해 Silverlight, WinRT 및 Windows Phone 클라이언트는 다음 플랫폼을 지원하는 단일 휴대용 .NET 클라이언트로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="70bfb-369">순 4.5</span><span class="sxs-lookup"><span data-stu-id="70bfb-369">NET 4.5</span></span>
- <span data-ttu-id="70bfb-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="70bfb-370">Silverlight 5</span></span>
- <span data-ttu-id="70bfb-371">WinRT (윈도우 스토어 앱용.NET)</span><span class="sxs-lookup"><span data-stu-id="70bfb-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="70bfb-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="70bfb-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="70bfb-373">새로운 셀프 호스트 패키지</span><span class="sxs-lookup"><span data-stu-id="70bfb-373">New Self-Host Package</span></span>

<span data-ttu-id="70bfb-374">이제 SignalR 셀프 호스트(웹 서버에서 호스팅되는 대신 프로세스 또는 다른 응용 프로그램에서 호스팅되는 SignalR 응용 프로그램)를 더 쉽게 시작할 수 있도록 NuGet 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="70bfb-375">SignalR 1.x로 빌드된 자체 호스트 프로젝트를 업그레이드하려면 Microsoft.AspNet.SignalR.Owin 패키지를 제거하고 Microsoft.AspNet.SignalR.SelfHost 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="70bfb-376">셀프 호스트 패키지 시작에 대한 자세한 내용은 [자습서: SignalR 셀프 호스트](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="70bfb-377">이전 버전과 호환되는 서버 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-377">Backward-compatible server support</span></span>

<span data-ttu-id="70bfb-378">이전 버전의 SignalR에서는 클라이언트와 서버에서 사용되는 SignalR 패키지 버전이 동일해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="70bfb-379">업데이트하기 어려운 두꺼운 클라이언트 응용 프로그램을 지원하기 위해 SignalR 2.0은 이제 이전 클라이언트와 함께 최신 서버 버전을 사용할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="70bfb-380">**참고: SignalR 2.0은 최신 클라이언트로 이전 버전으로 빌드된 서버를 지원하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="70bfb-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="70bfb-381">.NET 4.0에 대한 서버 지원 제거</span><span class="sxs-lookup"><span data-stu-id="70bfb-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="70bfb-382">SignalR 2.0은 .NET 4.0을 통해 서버 상호 운용성에 대한 지원을 중단했습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="70bfb-383">.NET 4.5는 SignalR 2.0 서버에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="70bfb-384">SignalR 2.0에 대한 .NET 4.0 클라이언트는 여전히 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="70bfb-385">클라이언트 및 그룹 목록에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="70bfb-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="70bfb-386">SignalR 2.0에서는 클라이언트 및 그룹 아이디 목록을 사용하여 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="70bfb-387">다음 코드 조각에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="70bfb-388">**영구 연결을 사용하여 클라이언트 및 그룹 목록에 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="70bfb-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="70bfb-389">**Hubs를 사용하여 클라이언트 및 그룹 목록에 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="70bfb-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="70bfb-390">특정 사용자에게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="70bfb-390">Sending a message to a specific user</span></span>

<span data-ttu-id="70bfb-391">이 기능을 사용하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 userId를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="70bfb-392">**IUserIdProvider 인터페이스**</span><span class="sxs-lookup"><span data-stu-id="70bfb-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="70bfb-393">기본적으로 사용자의 IPrincipal.Identity.Name 사용자 이름으로 사용하는 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="70bfb-394">허브에서는 새 API를 통해 이러한 사용자에게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="70bfb-395">**클라이언트 사용.사용자 API**</span><span class="sxs-lookup"><span data-stu-id="70bfb-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="70bfb-396">더 나은 오류 처리 지원</span><span class="sxs-lookup"><span data-stu-id="70bfb-396">Better Error Handling Support</span></span>

<span data-ttu-id="70bfb-397">이제 사용자는 모든 허브 호출에서 **HubException을** throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="70bfb-398">**HubException의** 생성자는 문자열 메시지와 개체 추가 오류 데이터를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="70bfb-399">SignalR은 예외를 자동으로 직렬화하고 허브 메서드 호출을 거부/실패하는 데 사용되는 클라이언트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="70bfb-400">**쇼 자세한 허브 예외** 설정은 **HubException클라이언트로** 다시 전송되거나 하지 않는 것에 아무런 영향을 미치지 않습니다. 항상 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="70bfb-401">**클라이언트에 HubException을 보내는 것을 보여 주는 서버 측 코드**</span><span class="sxs-lookup"><span data-stu-id="70bfb-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="70bfb-402">**서버에서 보낸 HubException에 응답하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="70bfb-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="70bfb-403">**서버에서 보낸 HubException에 응답하는 것을 보여 주는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="70bfb-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="70bfb-404">허브의 간편한 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="70bfb-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="70bfb-405">SignalR 2.0에는 모의 클라이언트 측 호출을 쉽게 만들 수 있는 Hubs에 호출된 `IHubCallerConnectionContext` 인터페이스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="70bfb-406">다음 코드 조각은 xUnit.net [moq에서](https://code.google.com/p/moq/)인기 [xUnit.net](https://github.com/xunit/xunit) 있는 테스트 하네스와 함께 이 인터페이스를 사용하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="70bfb-407">**xUnit.net 가진 단위 테스트 신호**</span><span class="sxs-lookup"><span data-stu-id="70bfb-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="70bfb-408">**단위 테스트 시그널R 와 moq**</span><span class="sxs-lookup"><span data-stu-id="70bfb-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="70bfb-409">자바 스크립트 오류 처리</span><span class="sxs-lookup"><span data-stu-id="70bfb-409">JavaScript error handling</span></span>

<span data-ttu-id="70bfb-410">SignalR 2.0에서 모든 JavaScript 오류 처리 콜백은 원시 문자열 대신 JavaScript 오류 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="70bfb-411">이를 통해 SignalR은 오류 처리기로 풍부한 정보를 플로우할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="70bfb-412">오류의 속성에서 내부 `source` 예외를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="70bfb-413">**시작.Fail 예외를 처리하는 자바스크립트 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="70bfb-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="70bfb-414">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="70bfb-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="70bfb-415">새로운 ASP.NET 멤버십 시스템</span><span class="sxs-lookup"><span data-stu-id="70bfb-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="70bfb-416">ASP.NET ID는 ASP.NET 응용 프로그램에 대한 새로운 회원 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="70bfb-417">ASP.NET ID를 사용하면 사용자별 프로필 데이터를 응용 프로그램 데이터와 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="70bfb-418">ASP.NET ID를 사용하면 응용 프로그램에서 사용자 프로필에 대한 지속성 모델을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="70bfb-419">NoSQL 데이터 저장소(예: Azure Storage 테이블)를 비롯하여 SQL Server 데이터베이스나 다른 데이터 저장소에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="70bfb-420">자세한 내용은 **Visual Studio 2013에서 웹 프로젝트 만들기의** [개별 사용자 계정을](creating-web-projects-in-visual-studio.md#indauth) ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="70bfb-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="70bfb-421">클레임 기반 인증</span><span class="sxs-lookup"><span data-stu-id="70bfb-421">Claims-based authentication</span></span>

<span data-ttu-id="70bfb-422">ASP.NET 이제 사용자의 ID가 신뢰할 수 있는 발급자의 클레임 집합으로 표시되는 클레임 기반 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="70bfb-423">사용자는 응용 프로그램 데이터베이스에 유지 관리되는 사용자 이름과 암호를 사용하거나 소셜 ID 공급자(예: Microsoft 계정, Facebook, Google, Twitter)를 사용하거나 Azure Active Directory 또는 ADFS(Active Directory Federation Services)를 통해 조직 계정을 사용하여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="70bfb-424">Azure Active 디렉터리 및 Windows 서버 활성 디렉터리와의 통합</span><span class="sxs-lookup"><span data-stu-id="70bfb-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="70bfb-425">이제 인증을 위해 Azure Active Directory 또는 Windows 서버 활성 디렉터리(AD)를 사용하는 ASP.NET 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="70bfb-426">자세한 내용은 **Visual Studio 2013에서 웹 프로젝트 만들기에서 ASP.NET**구성 [계정을](creating-web-projects-in-visual-studio.md#orgauth) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70bfb-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="70bfb-427">오윈 통합</span><span class="sxs-lookup"><span data-stu-id="70bfb-427">OWIN Integration</span></span>

<span data-ttu-id="70bfb-428">ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="70bfb-429">OWIN에 대한 자세한 내용은 다음 [Microsoft OWIN 구성 요소](#TOC7) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="70bfb-430">Microsoft OWIN 구성 요소</span><span class="sxs-lookup"><span data-stu-id="70bfb-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="70bfb-431">[.NET(OWIN)에 대한 개방형 웹 인터페이스는](http://owin.org/) .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="70bfb-432">OWIN은 서버에서 웹 응용 프로그램을 분리하여 웹 응용 프로그램을 호스트에 구애받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="70bfb-433">예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스팅하거나 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="70bfb-434">Microsoft OWIN 구성 요소(카타나 프로젝트라고도 함)에 도입된 변경 사항에는 새 서버 및 호스트 구성 요소, 새 도우미 라이브러리 및 미들웨어 및 새 인증 미들웨어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="70bfb-435">OWIN과 카타나에 대한 자세한 내용은 [OWIN과 카타나에서 새로운 정보를](../../../aspnet/overview/owin-and-katana/index.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="70bfb-436">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드에서 실행되어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70bfb-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="70bfb-437">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 완전 신뢰로 실행되어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70bfb-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="70bfb-438">새 서버 및 호스트</span><span class="sxs-lookup"><span data-stu-id="70bfb-438">New Servers and Hosts</span></span>

<span data-ttu-id="70bfb-439">이 릴리스에서는 자체 호스트 시나리오를 사용하도록 새 구성 요소가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="70bfb-440">이러한 구성 요소에는 다음 NuGet 패키지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="70bfb-441">**마이크로소프트.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="70bfb-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="70bfb-442">**HttpListener를** 사용하여 HTTP 요청을 수신하고 OWIN 파이프라인으로 안내하는 OWIN 서버를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="70bfb-443">**Microsoft.Owin.Hosting** 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 OWIN 파이프라인을 자체 호스트하려는 개발자를 위한 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="70bfb-444">**오윈호스트**.</span><span class="sxs-lookup"><span data-stu-id="70bfb-444">**OwinHost**.</span></span> <span data-ttu-id="70bfb-445">사용자 지정 호스트 응용 프로그램을 작성하지 `Microsoft.Owin.Hosting` 않고도 OWIN 파이프라인을 랩핑하고 자체 호스트할 수 있는 독립 실행 형 실행 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="70bfb-446">또한 `Microsoft.Owin.Host.SystemWeb` 이제 패키지를 사용하면 미들웨어가 **SystemWeb** 서버에 힌트를 제공할 수 있으므로 특정 ASP.NET 파이프라인 단계에서 미들웨어를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="70bfb-447">이 기능은 ASP.NET 파이프라인의 초기에 실행되어야 하는 인증 미들웨어에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="70bfb-448">도우미 라이브러리 및 미들웨어</span><span class="sxs-lookup"><span data-stu-id="70bfb-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="70bfb-449">OWIN 사양의 함수 및 형식 정의만 사용하여 OWIN 구성 요소를 `Microsoft.Owin` 작성할 수 있지만 새 패키지는 보다 사용자 친화적인 추상화 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="70bfb-450">이 패키지는 여러 이전 패키지(예: `Owin.Extensions`, `Owin.Types`)를 다른 OWIN 구성 요소에서 쉽게 사용할 수 있는 잘 구성된 단일 개체 모델로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="70bfb-451">실제로 대부분의 Microsoft OWIN 구성 요소는 이제 이 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="70bfb-452">[OWIN](http://www.owin.org) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="70bfb-453">[OWIN](http://www.owin.org) 응용 프로그램은 완전 신뢰로 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="70bfb-454">이 릴리스에는 실행 중인 OWIN 응용 프로그램의 유효성을 검사하는 미들웨어와 오류를 조사하는 데 도움이 되는 오류 페이지 미들웨어가 포함된 Microsoft.Owin.Diagnostics 패키지도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="70bfb-455">인증 구성 요소</span><span class="sxs-lookup"><span data-stu-id="70bfb-455">Authentication Components</span></span>

<span data-ttu-id="70bfb-456">다음 인증 구성 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-456">The following authentication components are available.</span></span>

- <span data-ttu-id="70bfb-457">**마이크로소프트.오윈.시큐리티.액티브 디렉토리**.</span><span class="sxs-lookup"><span data-stu-id="70bfb-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="70bfb-458">온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="70bfb-459">**Microsoft.Owin.Security.쿠키** 쿠키를 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="70bfb-460">이 패키지는 `Microsoft.Owin.Security.Forms`이전에 이름이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="70bfb-461">**Microsoft.Owin.Security.Facebook은** 페이스북의 OAuth 기반 서비스를 사용하여 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="70bfb-462">**Microsoft.Owin.Security.Google은** 구글의 OpenID 기반 서비스를 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="70bfb-463">**Microsoft.Owin.Security.Jwt** JWT 토큰을 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="70bfb-464">**Microsoft.Owin.Security.Microsoft계정에서** 마이크로소프트 계정을 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="70bfb-465">**마이크로소프트.오윈.시큐리티.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="70bfb-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="70bfb-466">보유자 토큰을 인증하기 위한 미들웨어뿐만 아니라 OAuth 권한 부여 서버를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="70bfb-467">**Microsoft.Owin.Security.Twitter** 트위터의 OAuth 기반 서비스를 사용하여 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="70bfb-468">이 릴리스에는 `Microsoft.Owin.Cors` 원본 간 HTTP 요청을 처리하기 위한 미들웨어가 포함된 패키지도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="70bfb-469">JWT 서명에 대한 지원은 Visual Studio 2013의 최종 버전에서 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="70bfb-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="70bfb-470">Entity Framework 6</span></span>

<span data-ttu-id="70bfb-471">엔터티 프레임워크 6의 새 기능 및 기타 변경 사항 목록은 [엔터티 프레임워크 버전 기록을](https://msdn.com/data/jj574253)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="70bfb-472">ASP.NET 면도기 3</span><span class="sxs-lookup"><span data-stu-id="70bfb-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="70bfb-473">ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="70bfb-474">탭 편집 지원.</span><span class="sxs-lookup"><span data-stu-id="70bfb-474">Support for Tab editing.</span></span> <span data-ttu-id="70bfb-475">이전에는 **탭 유지** 옵션을 사용할 때 Visual Studio의 **형식 문서** 명령, 자동 들여쓰기 및 자동 서식이 제대로 작동하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="70bfb-476">이 변경 사항은 탭 서식지정을 위해 Razor 코드에 대한 Visual Studio 서식을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="70bfb-477">링크를 생성할 때 URL 다시 쓰기 규칙에 대한 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="70bfb-478">보안 투명 특성 제거.</span><span class="sxs-lookup"><span data-stu-id="70bfb-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="70bfb-479">이것은 주요 변경, 그리고 면도기 3 MVC4 이전 호환 되지 않습니다., 면도기 2 MVC5 또는 MVC5에 대 한 컴파일 된 어셈블리와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="70bfb-480">시험판 버전에서 Visual Studio 2013에서 수정된 Razor 3 문제는 [여기에서](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="70bfb-481">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="70bfb-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="70bfb-482">ASP.NET App Suspend는 .NET Framework 4.5.1의 판도를 바꾸는 기능으로, 단일 컴퓨터에서 많은 수의 ASP.NET 사이트를 호스팅하기 위한 사용자 경험과 경제 모델을 근본적으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="70bfb-483">자세한 내용은 앱 일시 중단 ASP.NET 참조 [- 응답 공유 .NET 웹 호스팅.](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)</span><span class="sxs-lookup"><span data-stu-id="70bfb-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="70bfb-484">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="70bfb-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="70bfb-485">이 섹션에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구의 알려진 문제 및 주요 변경 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="70bfb-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="70bfb-486">NuGet</span></span>

- <span data-ttu-id="70bfb-487">[SLN 파일을 사용할 때 새 패키지 복원](https://nuget.codeplex.com/workitem/3596) 은 모노에서 작동하지 않습니다 - 곧 nuget.exe 다운로드 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="70bfb-488">[새로운 패키지 복원 Wix 프로젝트와 함께 작동 하지 않습니다-곧](https://nuget.codeplex.com/workitem/3598) nuget.exe 다운로드 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="70bfb-489">[자동 패키지 복원 솔루션 폴더 아래 프로젝트에 대 한 작동 하지](https://nuget.codeplex.com/workitem/3625) 않습니다-NuGet2.8에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="70bfb-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="70bfb-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="70bfb-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`에 대한 `IQueryable<T>` `$select` 지원을 추가했기 때문에 항상 `$expand`반환되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="70bfb-492">항상 에 반환 `ODataQueryOptions<T>` 값을 `ApplyTo` 캐스팅에 대한 `IQueryable<T>`이전 샘플 .</span><span class="sxs-lookup"><span data-stu-id="70bfb-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="70bfb-493">`$filter`앞에서 지원한 `$orderby` `$skip` `$top`쿼리 옵션은 쿼리의 모양을 변경하지 않기 때문에 이전에 작동했습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="70bfb-494">이제 우리는 `$select` 지원하고 `$expand` 반환 값에서 `ApplyTo` 항상되지 않습니다. `IQueryable<T>`</span><span class="sxs-lookup"><span data-stu-id="70bfb-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="70bfb-495">이전의 샘플 코드를 사용하는 경우 클라이언트가 보내고 `$select` `$expand`를 보내지 않으면 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="70bfb-496">그러나 지원하려는 `$select` `$expand` 경우 해당 코드를 이 것으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="70bfb-497">**Request.Url 또는 RequestContext.Url일괄 처리 요청 중에 null입니다.**</span><span class="sxs-lookup"><span data-stu-id="70bfb-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="70bfb-498">일괄 처리 시나리오에서 **UrlHelper는** **Request.Url** 또는 **RequestContext.Url**에서 액세스할 때 null입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="70bfb-499">이 문제는 현재 여기에서 추적됩니다: [BatchRequestContext.Url 일괄 처리 요청에 대 한 null입니다.](http://aspnetwebstack.codeplex.com/workitem/1301)</span><span class="sxs-lookup"><span data-stu-id="70bfb-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="70bfb-500">이 문제의 해결 방법은 다음 예제와 같이 **UrlHelper의**새 인스턴스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="70bfb-501">**UrlHelper의 새 인스턴스 만들기**</span><span class="sxs-lookup"><span data-stu-id="70bfb-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="70bfb-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="70bfb-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="70bfb-503">MVC5 및 OrgAuth를 사용하는 경우 AntiForgerToken 유효성 검사를 수행하는 뷰가 있는 경우 뷰에 데이터를 게시할 때 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="70bfb-504">**오류**:</span><span class="sxs-lookup"><span data-stu-id="70bfb-504">**Error**:</span></span>

    <span data-ttu-id="70bfb-505">*'/' 애플리케이션의 서버 오류.*</span><span class="sxs-lookup"><span data-stu-id="70bfb-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="70bfb-506"><em>제공된 클레임ID에<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'또는'<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>유형의 클레임이 존재하지 않았습니다. 클레임 기반 인증을 사용하여 위조 방지 토큰 지원을 활성화하려면 구성된 클레임 공급자가 생성한 ClaimsIdentity 인스턴스에서 이러한 클레임을 모두 제공하고 있는지 확인하십시오. 구성된 클레임 공급자가 대신 다른 클레임 형식을 고유 식별자로 사용하는 경우 정적 속성 AntiForgeryConfig.UniqueClaimTypeIdentifier를 설정하여 구성할 수 있습니다.</em></span><span class="sxs-lookup"><span data-stu-id="70bfb-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="70bfb-507">**해결 방법**:</span><span class="sxs-lookup"><span data-stu-id="70bfb-507">**Workaround**:</span></span>

    <span data-ttu-id="70bfb-508">Global.asax에서 다음 줄을 추가하여 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="70bfb-509">이 문제는 다음 릴리스에 대해 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="70bfb-510">MVC4 앱을 MVC5로 업그레이드한 후 솔루션을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="70bfb-511">다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-511">You should see the following error:</span></span>

    <span data-ttu-id="70bfb-512">[A] System.Web.WebPages.Razor.Configuration.HostSection은 [B]System.Web.WebPages.Razor.Configuration.HostSection에 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="70bfb-513">유형 A는 'System.Web.WebPages.Razor, 버전=2.0.0.0, 문화권=중립, PublicKeyToken=31bf3856ad364e35'\_위치 'C:\windows\Microsoft.Net\어셈블리\GAC MSIL\System.WebPages.Razor\v4.0\_2.0.0.0.0.0.0.0.0\_\_31bf3855ad364e35\System.WebPages.WebPages.Razor에서 '기본값'.</span><span class="sxs-lookup"><span data-stu-id="70bfb-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="70bfb-514">유형 B는 'System.Web.WebPages.Razor, 버전=3.0.0.0, 문화권=중립, PublicKeyToken=31bf3856ad364e35' 위치 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\임시 ASP.NET 파일\root\6에서 '기본값' d05bbd0\e8b5908e\어셈블리\dl3\c9cbca63\f8910382\_6273ce01\System.WebPages.Razor.dll..</span><span class="sxs-lookup"><span data-stu-id="70bfb-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="70bfb-515">위의 오류를 해결하려면 프로젝트의 *모든* Web.config 파일(보기 폴더에 있는 파일 포함)을 열고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="70bfb-516">"System.Web.Mvc"의 버전 "4.0.0.0"의 모든 발생을 "5.0.0.0"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="70bfb-517">"System.Web.helpers", &quot;System.Web.WebPages 및&quot; &quot;System.Web.WebPages.Razor의&quot; 모든 버전 "2.0.0.0"을 "3.0.0.0"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="70bfb-518">예를 들어 위의 내용을 변경한 후 어셈블리 바인딩은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="70bfb-519">MVC 4 프로젝트를 MVC 5로 업그레이드하는 방법에 대한 자세한 내용은 [MVC 5 및 웹 API 2를 ASP.NET ASP.NET MVC 4 및 웹 API 프로젝트를 업그레이드하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="70bfb-520">jQuery 눈에 거슬리지 없는 유효성 검사와 클라이언트 측 유효성 검사를 사용 하는 경우 유효성 검사 메시지가 경우에 올바르지 않은 HTML 입력 요소에 대 한 type='number'.</span><span class="sxs-lookup"><span data-stu-id="70bfb-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="70bfb-521">필요한 값에 대한 유효성 검사 오류("연령 필드가 필요")는 유효한 번호가 필요하다는 올바른 메시지 대신 잘못된 번호를 입력할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="70bfb-522">이 문제는 일반적으로 뷰 만들기 및 편집뷰에 정수 속성이 있는 모델에 대한 스캐폴드코드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="70bfb-523">이 문제를 해결하려면 편집기 도우미를 다음에서 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="70bfb-524">아래와 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="70bfb-525">ASP.NET MVC 5는 더 이상 부분 신뢰를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="70bfb-526">MVC 또는 WebAPI 바이너리에 연결하는 프로젝트는 [보안투명](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성과 [허용부분적으로 신뢰할 수 있는 호출자 특성을](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="70bfb-527">이러한 특성을 제거하면 다음과 같은 컴파일러 오류가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="70bfb-528">이 것의 부작용으로 동일한 응용 프로그램에서 4.0 및 5.0 어셈블리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="70bfb-529">모든 것을 5.0으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="70bfb-530">웹 사이트가 인트라넷 영역에서 호스팅되는 동안 Facebook 권한 부여가 있는 SPA 템플릿은 IE에서 불안정을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="70bfb-531">SPA 템플릿은 Facebook에서 외부 로그인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="70bfb-532">템플릿으로 만든 프로젝트가 로컬로 실행중일 때 로그인하면 IE가 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="70bfb-533">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="70bfb-533">Solution:</span></span>

1. <span data-ttu-id="70bfb-534">인터넷 영역에서 웹 사이트를 호스팅합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="70bfb-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="70bfb-535">IE 가 아닌 다른 브라우저에서 시나리오를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="70bfb-536">Web Forms 스캐폴딩</span><span class="sxs-lookup"><span data-stu-id="70bfb-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="70bfb-537">웹 양식 스캐폴딩은 VS2013에서 제거되었으며 향후 Visual Studio 업데이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="70bfb-538">그러나 MVC 종속성을 추가하고 MVC에 대한 스캐폴딩을 생성하여 웹 폼 프로젝트 내에서 스캐폴딩을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="70bfb-539">프로젝트에는 웹 양식과 MVC의 조합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="70bfb-540">웹 양식 프로젝트에 MVC를 추가하려면 새 스캐폴드된 항목을 추가하고 **MVC 5 종속성을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="70bfb-541">스크립트와 같은 모든 콘텐츠 파일이 필요한지 여부에 따라 최소 또는 전체 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="70bfb-542">그런 다음 프로젝트에서 뷰와 컨트롤러를 만드는 MVC용 스캐폴드 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="70bfb-543">MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류</span><span class="sxs-lookup"><span data-stu-id="70bfb-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="70bfb-544">프로젝트에 스캐폴드된 항목을 추가할 때 오류가 발생하면 프로젝트가 일관되지 않은 상태로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="70bfb-545">스캐폴딩으로 변경된 변경 사항 중 일부는 롤백되지만 설치된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="70bfb-546">라우팅 구성 변경 내용이 롤백되면 스캐폴드된 항목으로 탐색할 때 HTTP 404 오류가 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="70bfb-547">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="70bfb-547">Workaround:</span></span>

- <span data-ttu-id="70bfb-548">MVC에 대해 이 오류를 해결하려면 새 스캐폴드된 항목을 추가하고 MVC 5 종속성(최소 또는 전체)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="70bfb-549">이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="70bfb-550">웹 API에 대해 이 오류를 수정하려면 다음을 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="70bfb-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="70bfb-551">프로젝트에 WebApiConfig 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="70bfb-552">WebApiConfig.등록을 Global.asax의 응용 프로그램\_시작 메서드에 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="70bfb-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
