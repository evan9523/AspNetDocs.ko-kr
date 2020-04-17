---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: 비주얼 스튜디오 2012에 대한 ASP.NET 및 웹 도구 2013.1에 대한 릴리스 정보 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 Visual Studio 2012에 대한 ASP.NET 및 웹 도구 2013.1 릴리스에 대해 설명합니다.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543576"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="24953-103">Visual Studio 2012용 ASP.NET 및 Web Tools 2013.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="24953-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="24953-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="24953-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="24953-105">이 문서에서는 Visual Studio 2012에 대한 ASP.NET 및 웹 도구 2013.1 릴리스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="24953-106">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="24953-106">Contents</span></span>

- [<span data-ttu-id="24953-107">설치 노트</span><span class="sxs-lookup"><span data-stu-id="24953-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="24953-108">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="24953-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="24953-109">ASP.NET 및 웹 도구의 새로운 기능 2013.1 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="24953-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="24953-110">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="24953-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="24953-111">템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="24953-112">ASP.NET MVC 5 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="24953-113">ASP.NET 웹 API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="24953-114">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="24953-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="24953-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="24953-116">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="24953-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="24953-117">면도기 편집기</span><span class="sxs-lookup"><span data-stu-id="24953-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="24953-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="24953-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="24953-119">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="24953-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="24953-120">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="24953-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="24953-121">MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류</span><span class="sxs-lookup"><span data-stu-id="24953-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="24953-122">비계 항목을 추가 한 후 웹 작업을 중지하는 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="24953-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="24953-123">ASP.NET 면도기 3</span><span class="sxs-lookup"><span data-stu-id="24953-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="24953-124">찾아보기 또는 F5로 cshtml 파일을 보는 것은 서버 오류를 발생</span><span class="sxs-lookup"><span data-stu-id="24953-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="24953-125">URL 다시 쓰기 및 틸데(~)</span><span class="sxs-lookup"><span data-stu-id="24953-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="24953-126">템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="24953-127">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="24953-127">Installation Notes</span></span>

<span data-ttu-id="24953-128">[설치 중](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET 및 웹 도구 2013.1 Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="24953-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="24953-129">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="24953-129">Software Requirements</span></span>

<span data-ttu-id="24953-130">웹용 Visual Studio 2012 또는 Visual Studio Express 2012가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="24953-131">ASP.NET 및 웹 도구의 새로운 기능 2013.1 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="24953-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="24953-132">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="24953-132">Bootstrap</span></span>

<span data-ttu-id="24953-133">MVC 5 컨트롤러 및 뷰를 스캐폴드하면 뷰의 태그가 [부트스트랩을](http://getbootstrap.com/)사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="24953-134">템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="24953-135">ASP.NET MVC 5 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="24953-136">새 MVC 5 템플릿을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="24953-137">최신 MVC 5 NuGet 패키지를 참조하며 스캐폴딩을 사용하여 컨트롤러와 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="24953-138">ASP.NET 웹 API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="24953-139">새 웹 API 2 템플릿을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="24953-140">최신 웹 API 2 NuGet 패키지를 참조하며 스캐폴딩을 사용하여 컨트롤러 및 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="24953-141">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-141">Item Templates</span></span>

<span data-ttu-id="24953-142">MVC 5 뷰, 웹 페이지(Razor 3) 및 웹 API 2 컨트롤러에 대한 새 항목 템플릿을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="24953-143">새 항목을 추가하는 동안 프로젝트에 관련 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="24953-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="24953-144">Entity Framework 6</span></span>

<span data-ttu-id="24953-145">엔터티 프레임워크를 사용하여 MVC 또는 웹 API 컨트롤러를 스캐폴드할 때 프레임워크 6를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="24953-146">엔터티 프레임워크에 대한 자세한 내용은 [엔터티 프레임워크 버전 기록을](https://msdn.com/data/jj574253)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24953-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="24953-147">또한 Visual Studio 2012를 위한 엔터티 프레임워크 6 도구를 다운로드하여 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="24953-148">엔터티 [받기 프레임워크](https://msdn.com/data/ee712906#tooling)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24953-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="24953-149">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="24953-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="24953-150">ASP.NET 스캐폴딩은 ASP.NET 웹 응용 프로그램을 위한 코드 생성 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="24953-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="24953-151">데이터 모델과 상호 작용하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="24953-152">이전 버전의 Visual Studio에서는 스캐폴딩이 ASP.NET MVC 프로젝트로 제한되었습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="24953-153">이 업데이트를 통해 이제 웹 양식을 포함한 모든 ASP.NET 프로젝트에 스캐폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="24953-154">이 업데이트는 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않습니다 하지만 여전히 프로젝트에 MVC 종속성을 추가 하 여 웹 폼과 스캐폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="24953-155">웹 양식에 대한 페이지 생성에 대한 지원은 향후 업데이트에 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="24953-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="24953-156">스캐폴딩을 사용할 때 필요한 모든 종속성이 프로젝트에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="24953-157">예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스캐폴딩을 사용하여 웹 API 컨트롤러를 추가하는 경우 필요한 NuGet 패키지 및 참조가 프로젝트에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="24953-158">웹 양식 프로젝트에 MVC 스캐폴딩을 추가하려면 **새 스캐폴드 항목을** 추가하고 대화 상자 창에서 **MVC 5 종속성을** 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="24953-159">스캐폴딩 MVC에는 두 가지 옵션이 있습니다. 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="24953-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="24953-160">최소를 선택하면 ASP.NET MVC에 대한 NuGet 패키지 및 참조만 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="24953-161">전체 옵션을 선택하면 MVC 프로젝트에 필요한 콘텐츠 파일뿐만 아니라 최소 종속성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="24953-162">비동기 컨트롤러 스캐폴딩에 대한 지원은 엔터티 프레임워크 6의 새 비동기 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="24953-163">자세한 정보 및 자습서는 [ASP.NET 스캐폴딩 개요를](../2013/aspnet-scaffolding-overview.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24953-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="24953-164">이 자습서에서는 Visual Studio 2013을 사용하여 스캐폴딩을 보여 주지만 Visual Studio 2012의 ASP.NET 및 웹 도구 2013.1에도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="24953-165">면도기 편집기</span><span class="sxs-lookup"><span data-stu-id="24953-165">Razor Editor</span></span>

<span data-ttu-id="24953-166">이 업데이트와 함께, Visual Studio 2012 지금 지원 면도기 3 툴링/편집.</span><span class="sxs-lookup"><span data-stu-id="24953-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="24953-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="24953-167">NuGet 2.7</span></span>

<span data-ttu-id="24953-168">NuGet 2.7에는 [NuGet 2.7 릴리스 노트에서](http://docs.nuget.org/docs/release-notes/nuget-2.7)자세히 설명하는 풍부한 새로운 기능 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="24953-169">이 버전의 NuGet은 사용자가 NuGet에서 누락된 패키지를 복원하도록 명시적으로 허용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="24953-170">NuGet 2.7을 설치할 때 사용자는 누락된 패키지를 자동으로 복원하는 데 암시적으로 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="24953-171">사용자는 Visual Studio의 NuGet 설정을 통해 패키지 복원을 명시적으로 옵트아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="24953-172">이렇게 변경하면 패키지 복원의 작동 방식이 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="24953-173">알려진 문제 및 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="24953-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="24953-174">ASP.NET 비계</span><span class="sxs-lookup"><span data-stu-id="24953-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="24953-175">MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류</span><span class="sxs-lookup"><span data-stu-id="24953-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="24953-176">프로젝트에 스캐폴드된 항목을 추가할 때 오류가 발생하면 프로젝트가 일관되지 않은 상태로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="24953-177">스캐폴딩으로 변경된 변경 사항 중 일부는 롤백되지만 설치된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="24953-178">라우팅 구성 변경 내용이 롤백되면 스캐폴드된 항목으로 탐색할 때 HTTP 404 오류가 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="24953-179">MVC에 대해 이 오류를 해결하려면 새 스캐폴드된 항목을 추가하고 MVC 5 종속성(최소 또는 전체)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="24953-180">이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="24953-181">웹 API에 대해 이 오류를 수정하려면 다음을 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="24953-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="24953-182">프로젝트에 다음 WebApiConfig 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="24953-183">WebApiConfig.등록을 Global.asax의 응용 프로그램\_시작 메서드에 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="24953-184">비계 항목을 추가 한 후 웹 작업을 중지하는 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="24953-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="24953-185">웹용 Visual Studio Express 2012가 엔터티 프레임워크를 사용하여 스캐폴드된 항목을 추가한 후 작업을 중지하는 경우(예: 엔터티 프레임워크를 사용하는 작업이 있는 웹 API 2 컨트롤러) Visual Studio Express가 System.Web.Extensions에 종속된 어셈블리의 기본 이미지를 로드하지 못했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="24953-186">이 문제를 해결하려면 Visual Studio Express를 구성하여 System.Web.Extensions의 MSIL 이미지로 작업하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="24953-187">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24953-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="24953-188">%ProgramFiles%\마이크로소프트 비주얼 스튜디오 11.0\Common7\IDE 또는 %ProgramFiles (x86)%\마이크로소프트 비주얼 스튜디오 11.0\Common7\IDE (64 비트 윈도우)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="24953-189">텍스트 편집기에서 VWDExpress.exe.config를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24953-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="24953-190">&lt;&gt;구성/런타임&gt; 요소 아래에 다음 줄을 추가합니다.&lt;</span><span class="sxs-lookup"><span data-stu-id="24953-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="24953-191">웹용 비주얼 스튜디오 익스프레스 2012를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="24953-192">ASP.NET 면도기 3</span><span class="sxs-lookup"><span data-stu-id="24953-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="24953-193">찾아보기 또는 F5로 cshtml 파일을 보는 것은 서버 오류를 발생</span><span class="sxs-lookup"><span data-stu-id="24953-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="24953-194">Visual Studio 2012에서 MVC 5 프로젝트를 만들고(또는 Visual Studio 2012에서 열린 Visual Studio 2013에서 열림) 찾아보기 또는 F5를 사용하여 cshtml 파일을 보려고 하면 **'/' 응용 프로그램에서 서버 오류와**같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="24953-195">서버가`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="24953-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="24953-196">이 문제를 해결하려면 프로젝트의 **시작 설정** 설정을 **특정 페이지로**변경합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="24953-197">페이지에 대한 값을 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="24953-198">이 변경 후 F5를 선택하면 응용 프로그램의 루트()로`http://localhost:XXXX`이동합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="24953-199">이 동작은 **현재 페이지** 설정이 열린 페이지를 시작되는 Visual Studio 2013의 MVC 5 프로젝트의 동작과 다름없습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="24953-200">URL 다시 쓰기 및 틸데(~)</span><span class="sxs-lookup"><span data-stu-id="24953-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="24953-201">ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드한 후 URL 다시 쓰기를 사용하는 경우 물결표(~) 표기가 더 이상 제대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="24953-202">URL &lt;다시 쓰기는 A/&gt;및 스크립트/ &lt;&gt;LINK/ &lt;&gt;와 같은 HTML 요소의 표기에 영향을 미치므로 물결표가 더 이상 루트 디렉토리에 매핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="24953-203">예를 들어 **asp.net asp.net/content** 요청을 다시 **asp.net**작성하는 경우 &lt;href="~/content/"//에서&gt; href 특성을 **/content/content/대신 /content/content/로** **/** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="24953-204">이 변경을 억제하려면 **IIS\_WasUrlRewritten** 컨텍스트를 각 웹 페이지 또는 Global.asax의 **응용 프로그램\_BeginRequest에서** false로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="24953-205">템플릿</span><span class="sxs-lookup"><span data-stu-id="24953-205">Templates</span></span>

<span data-ttu-id="24953-206">Windows 8.1 또는 Windows 서버 2012 R2에서 Visual Studio 2012를 사용하여 ASP.NET MVC 프로젝트를 만들 때 Visual Studio는 "ASP.NET 4.5에 대한 웹 [url] 구성 실패"라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="24953-208">Visual Studio 2012는 Windows 릴리스에 설치될 때 ASP.NET 4.5 기능을 사용하지 않으므로 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24953-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="24953-209">ASP.NET 4.5를 사용하려면 Windows 켜기 기능에 설명된 단계를 [수행하거나 끕니다.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)</span><span class="sxs-lookup"><span data-stu-id="24953-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows 기능 켜기 또는 끄기](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="24953-211">또는 명령줄을 통해 ASP.NET 4.5를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24953-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="24953-212">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24953-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="24953-213">다음 명령을 실행하여 ASP.NET 4.5를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="24953-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
