---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 시작 | Microsoft Docs
author: Rick-Anderson
description: WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다. Visual Studio 또는 Visual Studio Code를 사용 합니다. 이 지침
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240762"
---
# <a name="getting-started"></a><span data-ttu-id="fe1cb-105">시작</span><span class="sxs-lookup"><span data-stu-id="fe1cb-105">Getting Started</span></span>

<span data-ttu-id="fe1cb-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fe1cb-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="fe1cb-107">WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="fe1cb-108">[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="fe1cb-109">이 지침 및 응용 프로그램은 동적 웹 사이트를 만들기 위한 간단한 프레임 워크로 ASP.NET 웹 페이지 (버전 2 이상) 및 Razor 구문에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="fe1cb-110">또한 페이지 및 사이트를 만들기 위한 도구인 WebMatrix를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="fe1cb-111">**수준**: ASP.NET 웹 페이지를 새로 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="fe1cb-112">**가정**하는 기술: HTML, 기본 css 스타일 시트 (css).</span><span class="sxs-lookup"><span data-stu-id="fe1cb-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="fe1cb-113">집합의 첫 번째 자습서에서 학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="fe1cb-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="fe1cb-114">ASP.NET 웹 페이지 기술의 정의와 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="fe1cb-115">WebMatrix는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="fe1cb-116">모든 항목을 설치 하는 방법</span><span class="sxs-lookup"><span data-stu-id="fe1cb-116">How to install everything.</span></span>
> - <span data-ttu-id="fe1cb-117">WebMatrix를 사용 하 여 웹 사이트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="fe1cb-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="fe1cb-118">설명 하는 기능/기술:</span><span class="sxs-lookup"><span data-stu-id="fe1cb-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="fe1cb-119">Microsoft 웹 플랫폼 설치 관리자.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="fe1cb-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-120">WebMatrix.</span></span>
> - <span data-ttu-id="fe1cb-121">*. cshtml* 페이지</span><span class="sxs-lookup"><span data-stu-id="fe1cb-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="fe1cb-122">Mike Pope는 원래이 자습서를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="fe1cb-123">Microsoft WebMatrix 3 용으로 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fe1cb-124">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="fe1cb-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fe1cb-125">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="fe1cb-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="fe1cb-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="fe1cb-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="fe1cb-127">무엇을 알아야 하나요?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-127">What Should You Know?</span></span>

<span data-ttu-id="fe1cb-128">다음에 대해 잘 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="fe1cb-129">**HTML**.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-129">**HTML**.</span></span> <span data-ttu-id="fe1cb-130">심층적인 전문 지식이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-130">No in-depth expertise is required.</span></span> <span data-ttu-id="fe1cb-131">HTML에 대해서는 설명 하지 않지만 복잡 한 항목은 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="fe1cb-132">유용 하다 고 생각 되는 HTML 자습서에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="fe1cb-133">**Css 스타일 시트**입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="fe1cb-134">HTML과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-134">Same as with HTML.</span></span>
- <span data-ttu-id="fe1cb-135">**기본 데이터베이스 아이디어**.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-135">**Basic database ideas**.</span></span> <span data-ttu-id="fe1cb-136">데이터에 스프레드시트를 사용 하 여 데이터를 정렬 하 고 필터링 한 경우이 자습서를 일반적으로이 자습서로 가정 하는 전문 지식 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="fe1cb-137">또한 기본적인 프로그래밍을 배우는 데 관심이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="fe1cb-138">C # 이라는 프로그래밍 언어를 사용 ASP.NET 웹 페이지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="fe1cb-139">프로그래밍에 대 한 배경 지식이 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="fe1cb-140">이전에 웹 페이지에서 JavaScript를 작성 한 적이 있다면 많은 배경을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="fe1cb-141">프로그래밍에 대해 잘 알고 있는 경우에는이 자습서 집합을 처음부터 빠르게 이동 하는 동안 새 프로그래머가 빠르게 이동 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="fe1cb-142">처음에는 몇 가지 자습서를 수행 하는 것 처럼 간단 하 게 설명할 수 있으며 더 빠른 클립으로 이동 하는 것도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="fe1cb-143">무엇이 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-143">What Do You Need?</span></span>

<span data-ttu-id="fe1cb-144">다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-144">Here's what you'll need:</span></span>

- <span data-ttu-id="fe1cb-145">Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="fe1cb-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="fe1cb-146">라이브 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-146">A live internet connection.</span></span>
- <span data-ttu-id="fe1cb-147">관리자 권한 (설치 프로세스에 필요)</span><span class="sxs-lookup"><span data-stu-id="fe1cb-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="fe1cb-148">ASP.NET 웹 페이지 이란?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="fe1cb-149">ASP.NET 웹 페이지는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="fe1cb-150">간단한 HTML 웹 페이지는 정적입니다. 해당 콘텐츠는 페이지에 있는 고정 HTML 태그에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="fe1cb-151">ASP.NET 웹 페이지를 사용 하 여 만든 것과 같은 동적 페이지를 통해 코드를 사용 하 여 즉시 페이지 콘텐츠를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="fe1cb-152">동적 페이지를 사용 하면 모든 종류의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="fe1cb-153">양식을 사용 하 여 사용자에 게 입력 하 라는 메시지를 표시 한 다음 페이지가 표시 되는 내용과 표시 되는 모양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="fe1cb-154">사용자의 정보를 가져와서 데이터베이스에 저장 한 다음 나중에 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="fe1cb-155">사이트에서 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-155">You can send email from your site.</span></span> <span data-ttu-id="fe1cb-156">웹의 다른 서비스 (예: 매핑 서비스)와 상호 작용 하 고 이러한 원본의 정보를 통합 하는 페이지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="fe1cb-157">WebMatrix 란?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-157">What is WebMatrix?</span></span>

<span data-ttu-id="fe1cb-158">WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 테스트 페이지에 대 한 웹 서버 및 웹 사이트를 인터넷에 게시 하기 위한 기능을 통합 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="fe1cb-159">WebMatrix는 무료 이며 쉽게 설치 하 고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="fe1cb-160">(PHP와 같은 기타 기술 뿐만 아니라 일반 HTML 페이지에도 적용 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="fe1cb-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="fe1cb-161">실제로 *는* WebMatrix를 사용 하 여 ASP.NET 웹 페이지 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="fe1cb-162">텍스트 편집기 (예:)를 사용 하 여 페이지를 만들고, 액세스 권한이 있는 웹 서버를 사용 하 여 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="fe1cb-163">그러나 WebMatrix를 사용 하면 모든 것이 매우 쉽지만 이러한 자습서에서는 전체에서 WebMatrix를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="fe1cb-164">이러한 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="fe1cb-164">About These Tutorials</span></span>

<span data-ttu-id="fe1cb-165">이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법에 대 한 소개입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="fe1cb-166">이 소개 자습서 집합에는 9 개의 자습서 합계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="fe1cb-167">ASP.NET 웹 페이지 초보자가 전문적이 고 전문적인 웹 사이트를 만드는 과정을 안내 하는 일련의 자습서 집합의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="fe1cb-168">이 첫 번째 자습서에서는 ASP.NET 웹 페이지 작업 하는 방법에 대 한 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="fe1cb-169">완료 되 면이를 선택 하 고 웹 페이지를 더 자세히 탐색 하는 추가 자습서 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="fe1cb-170">이에 대 한 자세한 설명은 의도적으로 쉽게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="fe1cb-171">무엇을 보여줄 때마다이 자습서를 설정 하는 것이 가장 쉽게 이해 하는 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="fe1cb-172">이후 자습서에서는 더 깊이 있게 전환 하 고 더 효율적이 고 유연한 접근 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="fe1cb-173">그러나 이러한 자습서에서는 먼저 기본 사항을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="fe1cb-174">방금 시작한 자습서 집합은 다음과 같은 ASP.NET 웹 페이지 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="fe1cb-175">설치를 소개 하 고 모든 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="fe1cb-176">(여기서는 읽고 있는 자습서에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="fe1cb-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="fe1cb-177">ASP.NET 웹 페이지 프로그래밍에 대 한 기본 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="fe1cb-178">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fe1cb-178">Creating a database.</span></span>
- <span data-ttu-id="fe1cb-179">사용자 입력 폼 만들기 및 처리</span><span class="sxs-lookup"><span data-stu-id="fe1cb-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="fe1cb-180">데이터베이스에서 데이터를 추가, 업데이트 및 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="fe1cb-181">무엇을 만드시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-181">What Will You Create?</span></span>

<span data-ttu-id="fe1cb-182">이 자습서를 설정 하 고 이후에 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="fe1cb-183">영화를 입력 하 고, 편집 하 고, 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="fe1cb-184">이 자습서 집합에서 만들 두 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="fe1cb-185">첫 번째는 만들 동영상 목록 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-185">The first one shows the movie listing page that you'll create:</span></span>

![영화 목록을 보여 주는 finshed 영화 앱](getting-started/_static/image1.png)

<span data-ttu-id="fe1cb-187">사이트에 새 영화 정보를 추가할 수 있는 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-187">And here's the page that lets you add new movie information to your site:</span></span>

![동영상 추가 페이지를 표시 하는 완료 된 동영상 앱](getting-started/_static/image2.png)

<span data-ttu-id="fe1cb-189">이후 자습서에서는이 집합에 빌드를 설정 하 고 그림 업로드, 사용자의 로그인, 전자 메일 보내기, 소셜 미디어와의 통합 등의 추가 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="fe1cb-190">Azure에서 실행 되는이 앱 확인</span><span class="sxs-lookup"><span data-stu-id="fe1cb-190">See this App Running on Azure</span></span>

<span data-ttu-id="fe1cb-191">완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fe1cb-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="fe1cb-192">다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="fe1cb-193">Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="fe1cb-194">계정이 아직 없는 경우 다음과 같은 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="fe1cb-195">[무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="fe1cb-196">[Msdn 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -msdn 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="fe1cb-197">모든 항목 설치</span><span class="sxs-lookup"><span data-stu-id="fe1cb-197">Installing Everything</span></span>

<span data-ttu-id="fe1cb-198">Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="fe1cb-199">실제로 설치 관리자를 설치 하 고이를 사용 하 여 다른 모든 항목을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="fe1cb-200">웹 페이지를 사용 하려면 Windows XP SP3 이상이 설치 되어 있거나 Windows Server 2008 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="fe1cb-201">ASP.NET 웹 사이트의 [웹 페이지 페이지](../../../index.md) 에서 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![&quot;WebMatrix 설치 단추를 표시 하는 ASP.NET 웹 사이트 &quot;](getting-started/_static/image3.png)

<span data-ttu-id="fe1cb-203">WebMatrix를 설치 하기 전에 사용 조건 및 개인정보 처리 방침에 동의 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![약관에 동의 하 여 설치 시작](getting-started/_static/image4.png)

<span data-ttu-id="fe1cb-205">**실행** 을 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="fe1cb-206">설치 관리자를 저장 하려면 **저장** 을 클릭 한 다음 저장 한 폴더에서 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="fe1cb-207">웹 플랫폼 설치 관리자가 WebMatrix를 설치할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="fe1cb-208">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="fe1cb-209">설치 과정에서 컴퓨터에 설치 해야 하는 사항을 파악 하 고 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="fe1cb-210">설치 해야 하는 항목에 따라 프로세스는 몇 분에서 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="fe1cb-211">**동의** 함을 선택 하 여 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="fe1cb-212">Hello, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="fe1cb-212">Hello, WebMatrix</span></span>

<span data-ttu-id="fe1cb-213">설치가 완료 되 면 설치 프로세스에서 WebMatrix를 자동으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="fe1cb-214">그렇지 않으면 Windows의 **시작** 메뉴에서 **Microsoft WebMatrix**를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="fe1cb-215">WebMatrix를 처음 시작 하는 경우 Microsoft 계정 Microsoft Azure에 로그인 할 수 있는 기회가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="fe1cb-216">로그인 하면 Azure를 통해 10 개의 무료 웹 앱을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="fe1cb-217">이러한 무료 웹 앱은 앱을 테스트 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="fe1cb-218">Azure 계정이 아직 없지만 MSDN 구독이 있는 경우 [msdn subscription 혜택을 활성화할](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="fe1cb-219">그렇지 않으면 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fe1cb-220">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/free/dotnet/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="fe1cb-221">이 자습서를 계속 진행 하기 위해 지금 로그인 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="fe1cb-222">지금 로그인 하지 않으면 나중에 로그인 할 수 있는 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="fe1cb-223">이 자습서 시리즈의 마지막 [항목](publishing.md) 에서는 Azure에 웹 사이트를 배포 하는 방법을 설명 합니다. 따라서이 항목을 완료 하려면 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="fe1cb-224">**이제** Microsoft 계정를 사용 하 여 로그인 하거나, 오른쪽 아래 모서리에서 아니요를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![링크를](getting-started/_static/image7.png)

<span data-ttu-id="fe1cb-226">시작 하려면 빈 웹 사이트를 만들고 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="fe1cb-227">이 집합의 이후 자습서에서는 기본 제공 웹 사이트 템플릿 중 하나를 사용 하 여 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="fe1cb-228">시작 창에서 **새로 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-228">In the start window, click **New**.</span></span>

![WebMatrix 시작 화면](getting-started/_static/image8.png)

<span data-ttu-id="fe1cb-230">템플릿은 다양 한 유형의 웹 사이트에 대해 미리 작성 된 파일 및 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="fe1cb-231">기본적으로 사용할 수 있는 모든 템플릿을 보려면 템플릿 갤러리 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![템플릿 갤러리 선택](getting-started/_static/image9.png)

<span data-ttu-id="fe1cb-233">**빠른 시작** 창의 **ASP.NET** 그룹에서 **빈 사이트** 를 선택 하 고 새 사이트의 이름을 "webpagesmovies"로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![빈 사이트 템플릿이 선택 된 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

<span data-ttu-id="fe1cb-235">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-235">Click **Next**.</span></span>

<span data-ttu-id="fe1cb-236">Microsoft 계정에 로그인 한 경우 Azure에서 사이트를 만들 수 있는 기회가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="fe1cb-237">사이트 이름에 따라 **WebPagesMovies.azurewebsites.net** 의 기본 이름이 제안 됩니다. 그러나 느낌표는이 이름을 Windows Azure에서 사용할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="fe1cb-238">간단히 하기 위해 **건너뛰기** 를 선택 하 여 지금 Azure에서 웹 사이트 만들기를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="fe1cb-239">이 시리즈의 뒷부분에서 Azure에 사이트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-239">Later in this series, we will publish the site to Azure.</span></span>

![azure 사이트 만들기](getting-started/_static/image11.png)

<span data-ttu-id="fe1cb-241">WebMatrix에서 사이트를 만들고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-241">WebMatrix creates and opens the site:</span></span>

![WebMatrix에서 새 웹 사이트 동영상 사이트 열기](getting-started/_static/image12.png)

<span data-ttu-id="fe1cb-243">위쪽에는 빠른 액세스 도구 모음과 리본 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="fe1cb-244">왼쪽 아래에서 작업 (**사이트**, **파일**, **데이터베이스**, **보고서**) 사이를 전환 하는 작업 영역 선택 기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="fe1cb-245">오른쪽에는 편집기 및 보고서에 대 한 내용 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="fe1cb-246">아래쪽에서 메시지에 대 한 알림 표시줄을 가끔 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="fe1cb-247">WebMatrix 및 해당 기능에 대 한 자세한 내용은이 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="fe1cb-248">웹 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="fe1cb-248">Creating a Web Page</span></span>

<span data-ttu-id="fe1cb-249">WebMatrix 및 ASP.NET 웹 페이지에 익숙해질 수 있도록 간단한 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="fe1cb-250">작업 영역 선택기에서 **파일** 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="fe1cb-251">이 작업 영역에서는 파일 및 폴더 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="fe1cb-252">왼쪽 창에는 사이트의 파일 구조가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="fe1cb-253">리본은 파일 관련 작업을 표시 하도록 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix의 파일 작업 영역](getting-started/_static/image13.png)

<span data-ttu-id="fe1cb-255">리본 메뉴에서 **새로 만들기** 아래에 있는 화살표를 클릭 한 다음 **새 파일**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![&quot;리본에서 새 명령을 사용 하 여 &quot; 새 파일 만들기](getting-started/_static/image14.png)

<span data-ttu-id="fe1cb-257">WebMatrix 파일 형식 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="fe1cb-258">**CSHTML**를 선택 하 고 **이름** 상자에 "HelloWorld"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="fe1cb-259">CSHTML 페이지는 ASP.NET 웹 페이지 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![HelloWorld. cshtml 라는 새 CSHTML 페이지를 만듭니다.](getting-started/_static/image15.png)

<span data-ttu-id="fe1cb-261">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-261">Click **OK**.</span></span>

<span data-ttu-id="fe1cb-262">WebMatrix가 페이지를 만들고 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 편집기의 새 HelloWorld 페이지](getting-started/_static/image16.png)

<span data-ttu-id="fe1cb-264">여기에서 볼 수 있듯이 페이지는 위쪽에 있는 블록을 제외 하 고 다음과 같은 일반적인 HTML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="fe1cb-265">잠시 후에 코드를 추가 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="fe1cb-266">페이지의 &mdash; 요소 이름, 특성, 텍스트 및 위쪽의 블록은 모두 다른 색으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="fe1cb-267">이를 *구문 강조 표시*라고 하며 모든 것을 명확 하 게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="fe1cb-268">WebMatrix에서 웹 페이지를 쉽게 사용할 수 있도록 하는 기능 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="fe1cb-269">`<head>`다음 예제와 같이 및 요소에 대 한 콘텐츠를 추가 `<body>` 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="fe1cb-270">(원하는 경우 다음 블록을 복사 하 고 기존 전체 페이지를이 코드로 바꿀 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="fe1cb-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="fe1cb-271">빠른 실행 도구 모음 또는 **파일** 메뉴에서 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix 빠른 실행 도구 모음의 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="fe1cb-273">페이지 테스트</span><span class="sxs-lookup"><span data-stu-id="fe1cb-273">Testing the Page</span></span>

<span data-ttu-id="fe1cb-274">**파일** 작업 영역에서 *HelloWorld. cshtml* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix 리본에서 실행 단추를 사용 하 여 페이지 실행](getting-started/_static/image18.png)

<span data-ttu-id="fe1cb-276">WebMatrix는 컴퓨터에서 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="fe1cb-277">(WebMatrix에서 IIS Express 하지 않고 웹 서버를 테스트 하기 전에 웹 서버에 페이지를 게시 해야 합니다.) 페이지가 기본 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;&quot;브라우저에서 실행 중인 Hello World 페이지](getting-started/_static/image19.png)

<span data-ttu-id="fe1cb-279">WebMatrix에서 페이지를 테스트 하는 경우 브라우저의 URL은 `http://localhost:33651/HelloWorld.cshtml.` 로컬 서버를 참조 하는 이름입니다 *localhost* . 즉, 사용자 컴퓨터에 있는 웹 서버에서 페이지를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="fe1cb-280">앞서 설명한 것 처럼 WebMatrix에는 페이지를 시작할 때 실행 되는 IIS Express 이라는 웹 서버 프로그램이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="fe1cb-281">*Localhost* (예 *: localhost: 33651*) 다음의 번호는 컴퓨터의 *포트 번호* 를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="fe1cb-282">이 특정 웹 사이트에 IIS Express 사용 하는 "채널"의 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="fe1cb-283">포트 번호는 사이트를 만들 때 1024 ~ 65536 범위의 임의로 선택 되며, 사용자가 만드는 모든 사이트 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="fe1cb-284">사용자 고유의 사이트를 테스트 하는 경우 포트 번호는 거의 33561 보다 다른 숫자입니다. 각 웹 사이트에 대해 서로 다른 포트를 사용 하 여 통신 하 고 있는 사이트를 바로 IIS Express 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="fe1cb-285">나중에 사이트를 공용 웹 서버에 게시할 때 URL에 *localhost* 가 더 이상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="fe1cb-286">이 시점에서 또는 페이지와 같은 일반적인 URL을 볼 수 있습니다 `http://myhostingsite/mywebsite/HelloWorld.cshtml` .</span><span class="sxs-lookup"><span data-stu-id="fe1cb-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="fe1cb-287">이 자습서 시리즈의 뒷부분에서 사이트를 게시 하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="fe1cb-288">서버 쪽 코드 추가</span><span class="sxs-lookup"><span data-stu-id="fe1cb-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="fe1cb-289">브라우저를 닫고 WebMatrix의 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="fe1cb-290">코드 블록에 다음 코드와 같이 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="fe1cb-291">약간 약간의 Razor 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="fe1cb-292">현재 날짜와 시간을 가져오고 해당 값을 라는 *변수에* 배치 한다는 것을 분명 하 게 알 수 있습니다 `currentDateTime` .</span><span class="sxs-lookup"><span data-stu-id="fe1cb-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="fe1cb-293">다음 자습서의 Razor 구문에 대 한 자세한 내용을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="fe1cb-294">페이지의 본문에서 요소 뒤에 `<p>Hello World!</p>` 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="fe1cb-295">이 코드는 `currentDateTime` 위쪽의 변수에 입력 한 값을 가져와 페이지의 태그에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="fe1cb-296">`@`문자는 페이지의 ASP.NET 웹 페이지 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="fe1cb-297">페이지를 다시 실행 합니다. WebMatrix는 페이지를 실행 하기 전에 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="fe1cb-298">이번에는 페이지에 날짜 및 시간이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-298">This time you see the date and time in the page.</span></span>

![&quot;&quot;동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 중인 Hello World 페이지](getting-started/_static/image20.png)

<span data-ttu-id="fe1cb-300">잠시 기다렸다가 브라우저에서 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="fe1cb-301">날짜 및 시간 표시가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-301">The date and time display is updated.</span></span>

<span data-ttu-id="fe1cb-302">브라우저에서 페이지 소스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-302">In the browser, look at the page source.</span></span> <span data-ttu-id="fe1cb-303">이 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="fe1cb-304">위쪽에 있는 `@{ }` 블록은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="fe1cb-305">또한 날짜 및 시간 표시에는의 실제 문자열 (또는 모든 항목)이 표시 됩니다. `1/18/2012 2:49:50 PM` `@currentDateTime` *.cshtml*</span><span class="sxs-lookup"><span data-stu-id="fe1cb-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="fe1cb-306">여기서는 페이지를 실행 했을 때 ASP.NET로 표시 된 모든 코드 (이 경우에는 거의 없음)를 처리 했음을 의미 `@` 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="fe1cb-307">코드가 출력을 생성 하 고 해당 출력이 페이지에 삽입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="fe1cb-308">이 ASP.NET 웹 페이지에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="fe1cb-309">ASP.NET 웹 페이지에서 동적 웹 콘텐츠를 생성 하는 것을 읽을 때 여기에 표시 되는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="fe1cb-310">방금 만든 페이지에는 앞서 살펴본 것과 동일한 HTML 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="fe1cb-311">또한 모든 종류의 작업을 수행할 수 있는 코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="fe1cb-312">이 예에서는 현재 날짜 및 시간을 가져오는 간단한 작업을 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="fe1cb-313">앞서 살펴본 것 처럼 HTML로 코드를 섞어서 하 여 페이지에서 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="fe1cb-314">사용자가 브라우저에서 *cshtml* 페이지를 요청 하면 ASP.NET는 웹 서버를 계속 사용할 때 페이지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="fe1cb-315">ASP.NET 코드의 출력 (있는 경우)을 HTML로 페이지에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="fe1cb-316">코드 처리가 완료 되 면 ASP.NET는 결과 페이지를 브라우저로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="fe1cb-317">모든 브라우저는 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="fe1cb-318">다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-318">Here's a diagram:</span></span>

![ASP.NET에서 HTML을 동적으로 생성 하는 방법의 개념적 흐름](getting-started/_static/image21.png)

<span data-ttu-id="fe1cb-320">개념은 간단 하지만, 코드에서 수행할 수 있는 많은 흥미로운 작업이 있으며, 페이지에 HTML 콘텐츠를 동적으로 추가할 수 있는 여러 가지 흥미로운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="fe1cb-321">또한 HTML 페이지와 *같은 ASP.NET 페이지* 에는 브라우저 자체에서 실행 되는 코드 (JavaScript 및 jQuery 코드)가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="fe1cb-322">이 자습서 집합과 이후의 모든 항목을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="fe1cb-323">다음에서 시작</span><span class="sxs-lookup"><span data-stu-id="fe1cb-323">Coming Up Next</span></span>

<span data-ttu-id="fe1cb-324">이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍에 대해 좀 더 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe1cb-325">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fe1cb-325">Additional Resources</span></span>

<span data-ttu-id="fe1cb-326">[ASP.NET 웹 사이트를 처음부터 새로 만듭니다](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span><span class="sxs-lookup"><span data-stu-id="fe1cb-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="fe1cb-327">WebMatrix를 사용 하는 방법에 대 한 자습서입니다 (ASP.NET 웹 페이지는 아님).</span><span class="sxs-lookup"><span data-stu-id="fe1cb-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="fe1cb-328">이 자습서 집합에 포함 되지 않는 WebMatrix의 일부 추가 기능에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe1cb-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fe1cb-329">다음</span><span class="sxs-lookup"><span data-stu-id="fe1cb-329">Next</span></span>](intro-to-web-pages-programming.md)
