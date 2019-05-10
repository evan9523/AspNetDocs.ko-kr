---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 자습서 소개 | Microsoft Docs
author: shanselman
description: 새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우 이 자습서에서는 ASP.NE를 사용 하 여 완료 하지만 크기가 작은 응용 프로그램을 작성 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122315"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="ff962-104">NerdDinner 자습서 소개</span><span class="sxs-lookup"><span data-stu-id="ff962-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="ff962-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="ff962-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="ff962-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ff962-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ff962-107">새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ff962-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="ff962-108">이 자습서는 작은 빌드만 ASP.NET MVC 1을 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고는 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="ff962-109">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="ff962-110">NerdDinner 자습서</span><span class="sxs-lookup"><span data-stu-id="ff962-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="ff962-111">새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ff962-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="ff962-112">이 자습서는 작은 빌드만 ASP.NET MVC를 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고는 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="ff962-113">빌드 하려는 응용 프로그램 "NerdDinner" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="ff962-114">NerdDinner 쉽게를 찾고 dinners online을 구성 하는 사용자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="ff962-115">NerdDinner 등록 된 사용자를를 만들고, 편집 dinners를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="ff962-116">응용 프로그램 간에 일관 된 유효성 검사 및 비즈니스 규칙 집합을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="ff962-117">방문자는 AJAX 기반 지도 사용 하 여 향후 dinners 가까이 보유 하 고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="ff962-118">클릭 하면는 dinner 이동 해당 세부 정보 페이지를 어디서 알아볼 수 자세히:</span><span class="sxs-lookup"><span data-stu-id="ff962-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="ff962-119">Dinner 참여에 관심이 있는 경우 로그인 하거나 사이트에 등록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="ff962-120">이벤트 참석 RSVP AJAX 기반 링크를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="ff962-121">NerdDinner 구현</span><span class="sxs-lookup"><span data-stu-id="ff962-121">Implementing NerdDinner</span></span>

<span data-ttu-id="ff962-122">파일-를 사용 하 여 NerdDinner 응용 프로그램을 시작 하겠습니다&gt;새로운 ASP.NET MVC 프로젝트를 만들려면 Visual Studio 내에서 새 프로젝트 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="ff962-123">그런 다음 증분 방식으로 추가 기능 및 기능.</span><span class="sxs-lookup"><span data-stu-id="ff962-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="ff962-124">이 과정에서 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="ff962-125">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="ff962-126">데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="ff962-127">비즈니스 규칙 유효성 검사를 사용 하 여 모델을 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="ff962-128">목록/세부 정보 UI 구현 하려면 컨트롤러와 뷰를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="ff962-129">CRUD를 제공 하는 방법 (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원</span><span class="sxs-lookup"><span data-stu-id="ff962-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="ff962-130">ViewData 사용 및 ViewModel 클래스를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="ff962-131">마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="ff962-132">효율적인 데이터 페이징 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="ff962-133">인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="ff962-134">AJAX를 사용 하 여 동적 업데이트를 제공 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="ff962-135">AJAX를 사용 하 여 매핑 시나리오를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="ff962-136">자동화 된 단위 테스트를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff962-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="ff962-137">NerdDinner의 고유한 복사본을 빌드할 수 있습니다 각 완료 하 여 처음부터 단계에서는이 챕터에 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="ff962-138">또는 여기에서 소스 코드의 전체 버전을 다운로드할 수 있습니다. [GitHub에서 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="ff962-139">또한 필요에 따라 수도 있습니다 [이 자습서에서는 무료 PDF 버전을 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) 하려면 오프 라인 자습서를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="ff962-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="ff962-140">응용 프로그램을 빌드하려면 Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="ff962-141">데이터베이스에 대 한 SQL Server 또는 무료 SQL Server Express를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="ff962-142">ASP.NET MVC, Visual Web Developer 2008 Express 및 SQL Server Express (모든 사용 가능)의 V2를 사용 하 여 설치할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="ff962-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="ff962-143">이제 시작 해 보겠습니다...</span><span class="sxs-lookup"><span data-stu-id="ff962-143">Now let's get started....</span></span>

<span data-ttu-id="ff962-144">NerdDinner 란 살펴보았습니다 했으므로 실제로 롤업 하 고 일부 코드를 작성 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="ff962-145">파일-를 사용 하 여 먼저&gt;NerdDinner 응용 프로그램을 만들려면 Visual Studio 내에서 새 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="ff962-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ff962-146">다음</span><span class="sxs-lookup"><span data-stu-id="ff962-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
