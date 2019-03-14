---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
title: ASP.NET 호스팅 옵션 (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 응용 프로그램은 일반적으로 설계, 생성 및 로컬 개발 환경에서 테스트 및 프로덕션 환경 o에 배포 해야 하는 중...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 89a1d2bc-fdfd-4c5c-a3b0-49a08baaf63a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
msc.type: authoredcontent
ms.openlocfilehash: 3adad579c5893fb4f40e7043b9ece78740080f65
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061390"
---
<a name="aspnet-hosting-options-c"></a><span data-ttu-id="2dd49-103">ASP.NET 호스팅 옵션(C#)</span><span class="sxs-lookup"><span data-stu-id="2dd49-103">ASP.NET Hosting Options (C#)</span></span>
====================
<span data-ttu-id="2dd49-104">[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="2dd49-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

[<span data-ttu-id="2dd49-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="2dd49-105">Download PDF</span></span>](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_cs.pdf)

> <span data-ttu-id="2dd49-106">ASP.NET 웹 응용 프로그램은 일반적으로 디자인, 생성 및 테스트 로컬 개발 환경 및 릴리스에 대 한 준비가 되 면 프로덕션 환경에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-106">ASP.NET web applications are typically designed, created, and tested in a local development environment and need to be deployed to a production environment once it is ready for release.</span></span> <span data-ttu-id="2dd49-107">이 자습서 배포 프로세스의 상위 수준 개요를 제공 하 고이 자습서 시리즈에 대 한 기본적인 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-107">This tutorial provides a high-level overview of the deployment process and serves as an introduction to this tutorial series.</span></span>


## <a name="introduction"></a><span data-ttu-id="2dd49-108">소개</span><span class="sxs-lookup"><span data-stu-id="2dd49-108">Introduction</span></span>

<span data-ttu-id="2dd49-109">웹 응용 프로그램은 일반적으로 디자인, 생성 및 사이트에서 작업 하는 프로그래머에만 액세스할 수 있는 개발 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="2dd49-109">Web applications are typically designed, created, and tested in a development environment that is accessible only to the programmers working on the site.</span></span> <span data-ttu-id="2dd49-110">응용 프로그램을 릴리스할 준비가 되 면 이동 프로덕션 환경에 인터넷에서 누구나 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-110">Once the application is ready to be released, it is moved to a production environment where the site can be accessed by anyone on the Internet.</span></span> <span data-ttu-id="2dd49-111">이 배포 프로세스는 많은 문제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-111">This deployment process introduces a number of challenges:</span></span>

- <span data-ttu-id="2dd49-112">프로덕션 환경에 존재 해야 하며 적절 하 게 설치 전에 ASP.NET 응용 프로그램을 배포할 수 있습니다. 또한 프로덕션 환경 최신 보안 패치를 사용 하 여 최신 상태로 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-112">A production environment must exist and be properly setup before an ASP.NET application can be deployed; moreover, the production environment must be kept up to date with the latest security patches.</span></span>
- <span data-ttu-id="2dd49-113">태그 파일과 코드 파일 지원 파일의 올바른 집합 개발 환경에서 프로덕션 환경에 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-113">The correct set of markup files, code files, and support files must be copied from the development environment to the production environment.</span></span> <span data-ttu-id="2dd49-114">데이터 기반 응용 프로그램에 대 한 데이터베이스 스키마 및/또는 데이터를 복사 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-114">For data-driven applications, this might require copying the database schema and/or data, as well.</span></span>
- <span data-ttu-id="2dd49-115">두 환경 간의 구성 차이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-115">There may be configuration differences between the two environments.</span></span> <span data-ttu-id="2dd49-116">개발 환경에서 사용 되는 데이터베이스 연결 문자열 또는 전자 메일 서버에서 프로덕션 환경과 다를 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-116">The database connection string or email server used in the development environment will likely be different than the production environment.</span></span> <span data-ttu-id="2dd49-117">게다가 환경에 응용 프로그램의 동작은 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-117">What's more, the behavior of the application may depend on the environment.</span></span> <span data-ttu-id="2dd49-118">예를 들어, 개발에서 오류가 발생 하는 경우 오류 세부 정보 화면에서 표시할 수 있습니다 않으며 프로덕션 환경에서 오류가 발생 하는 경우 친숙 한 오류 페이지가 대신 표시 됩니다. 오류 세부 정보를 개발자에 게 전자 메일로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-118">For example, when an error occurs in development the error's details can be displayed on screen, but when an error occurs in production, a user-friendly error page should be displayed instead, and the error details emailed to the developers.</span></span>

<span data-ttu-id="2dd49-119">여러 개인 사용자와 비즈니스 아웃소싱를 프로덕션 환경-설정 및 프로덕션 환경을 유지 관리-첫 번째 질문을 제거 하려면 *웹 호스팅 공급자*합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-119">To obviate the first challenge - setting up and maintaining a production environment - many individuals and businesses outsource their production environments to *web hosting providers*.</span></span> <span data-ttu-id="2dd49-120">웹 호스팅 공급자에는 사용자를 대신해 프로덕션 환경을 관리 하는 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-120">A web hosting provider is a company that manages the production environment on your behalf.</span></span> <span data-ttu-id="2dd49-121">수많은 웹 호스트 공급자를 사용 하 여 다양 한 가격 및 서비스 수준을; 각각 가지 이러한 서비스 공급자 찾기에 대 한 팁 "호스트 웹 공급자 찾기" 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2dd49-121">There are countless web host providers, each with varying prices and service levels; see the "Finding a Web Host Provider" section for tips on locating such a service provider.</span></span>

<span data-ttu-id="2dd49-122">이 웹 호스트 공급자가 관리 되는 프로덕션 환경에 ASP.NET 웹 응용 프로그램을 배포 하는 단계를 확인 하는 자습서 시리즈의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-122">This is the first in a series of tutorials that look at the steps involved in deploying an ASP.NET web application to a production environment managed by a web host provider.</span></span> <span data-ttu-id="2dd49-123">이 자습서의 과정을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-123">Over the course of these tutorials we will examine:</span></span>

- <span data-ttu-id="2dd49-124">파일 웹 호스트 공급자에 게 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-124">What files need to be deployed to the web host provider.</span></span>
- <span data-ttu-id="2dd49-125">배포 프로세스를 간소화 하는 것에 대 한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-125">Tools for streamlining the deployment process.</span></span>
- <span data-ttu-id="2dd49-126">데이터베이스를 배포 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-126">How to deploy a database.</span></span>
- <span data-ttu-id="2dd49-127">사용 하는 데이터베이스를 배포 하기 위한 팁 [SQL 기반 멤버 자격 및 역할 공급자를](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md), 프로덕션 환경에서 웹 사이트 관리 도구를 모방 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-127">Tips for deploying a database that uses [the SQL-based Membership and Roles provider](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md), along with ways to mimic the Website Administration Tool in a production environment.</span></span>
- <span data-ttu-id="2dd49-128">원활 하 게 개발 하는 동안 변경 내용으로 프로덕션 환경에서 데이터베이스를 업데이트 하기 위한 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-128">Strategies for smoothly updating the database in production with changes made during development.</span></span>
- <span data-ttu-id="2dd49-129">프로덕션 및 오류가 발생할 때 개발자에 알리는 방법에서 발생 하는 오류를 기록에 대 한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-129">Techniques for logging errors that occur on production, and ways to notify developers when an error occurs.</span></span>

<span data-ttu-id="2dd49-130">간결 하 고 프로세스를 안내 하는 시각적으로 스크린 샷을 많은 단계별 지침을 제공 하려면이 자습서에 맞게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-130">These tutorials are geared to be concise and to provide step-by-step instructions with plenty of screen shots to walk you through the process visually.</span></span> <span data-ttu-id="2dd49-131">이 첫 자습서 찾기 웹 호스팅 공급자에 조언을 고 ASP.NET 배포 프로세스의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-131">This inaugural tutorial provides an overview of the ASP.NET deployment process and advice on finding a web hosting provider.</span></span> <span data-ttu-id="2dd49-132">이제 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-132">Let's get started!</span></span>

## <a name="an-overview-of-the-aspnet-deployment-process"></a><span data-ttu-id="2dd49-133">ASP.NET 배포 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="2dd49-133">An Overview of the ASP.NET Deployment Process</span></span>

<span data-ttu-id="2dd49-134">간단히 말해 ASP.NET 응용 프로그램 배포는 다음 세 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-134">In a nutshell, deploying an ASP.NET application involves the following three steps:</span></span>

1. <span data-ttu-id="2dd49-135">프로덕션 환경에서 웹 응용 프로그램, 웹 서버 및 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-135">Configure the web application, web server, and database in the production environment.</span></span>
2. <span data-ttu-id="2dd49-136">ASP.NET 페이지, 코드 파일, 어셈블리에 동기화 된 `Bin` 폴더 및 CSS 및 JavaScript 파일과 같은 HTML 관련 지원 파일.</span><span class="sxs-lookup"><span data-stu-id="2dd49-136">Synchronize the ASP.NET pages, code files, the assemblies in the `Bin` folder, and HTML-related support files like CSS and JavaScript files.</span></span>
3. <span data-ttu-id="2dd49-137">데이터베이스 스키마 및/또는 데이터를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-137">Synchronize the database schema and/or data.</span></span>

<span data-ttu-id="2dd49-138">일반적으로 웹 응용 프로그램에 대 한 구성 정보에는 `Web.config` 파일 및 데이터베이스 연결 문자열, 오류 처리 조건 URL 재작성 규칙 및 전자 메일 서버 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-138">The configuration information for a web application is typically located in the `Web.config` file, and includes database connection strings, error handling criteria, URL rewriting rules, and email server information.</span></span> <span data-ttu-id="2dd49-139">종종이 정보는 응용 프로그램 개발 및 프로덕션 환경에서 동일한 응용 프로그램의에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-139">Oftentimes this information is different for an application in development versus the same application in production.</span></span> <span data-ttu-id="2dd49-140">예를 들어, 응용 프로그램을 개발 하는 경우 프로덕션 데이터베이스에 대해 테스트할 수 있도록 개발 데이터베이스를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-140">For instance, when developing an application it's best to use a development database so that you're not testing against the production database.</span></span> <span data-ttu-id="2dd49-141">결과적으로, 데이터베이스 연결 문자열을 일반적으로 개발 및 프로덕션 응용 프로그램 간에 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-141">As a result, the database connection strings typically differ between development and production applications.</span></span> <span data-ttu-id="2dd49-142">이러한 차이로 인해 배포의 일부로 웹 응용 프로그램의 구성 정보를 변경 하는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-142">Due to these differences, part of deployment involves making changes to the web application's configuration information.</span></span>

<span data-ttu-id="2dd49-143">1 단계는 웹 응용 프로그램 구성 변경 하는 것 외에도 웹 서버 및 데이터베이스에 대 한 구성도 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-143">In addition to web application configuration changes, Step 1 also may entail configuration for the web server and database.</span></span> <span data-ttu-id="2dd49-144">예를 들어, ASP.NET 페이지를 만들거나 웹 서버의 디렉터리에서 파일을 삭제 하는 경우 다음 웹 서버 해야 이러한 파일 시스템 수정 허용 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-144">For example, if an ASP.NET page creates or deletes files from a directory on the web server then the web server needs to be configured to permit these file system modifications.</span></span> <span data-ttu-id="2dd49-145">마찬가지로 데이터베이스에 대 한 필요한 사용 권한 또는 인증 설정 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-145">Similarly, there may be permission or authentication settings that need to be made to the database.</span></span>


<span data-ttu-id="2dd49-146">2 단계에서는 essential ASP.NET 페이지 및 개발 및 프로덕션 환경 간에 지원 파일 집합을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-146">Step 2 involves synchronizing the set of essential ASP.NET pages and support files between the development and production environments.</span></span> <span data-ttu-id="2dd49-147">특정은 ASP의 집합입니다. 두 환경 간의 동기화 해야 하는 NET 관련 파일 다음 자습서의 설명을 이며 Visual Studio에서 만든 프로젝트의 유형에 따라 달라 집니다 [ *확인 파일 필요한배포할*](determining-what-files-need-to-be-deployed-cs.md).</span><span class="sxs-lookup"><span data-stu-id="2dd49-147">The particular set of ASP.NET-related files that need to be synchronized between the two environments depends on the type of project you created in Visual Studio, and is the discussion in the next tutorial, [*Determining What Files Need to Be Deployed*](determining-what-files-need-to-be-deployed-cs.md).</span></span> <span data-ttu-id="2dd49-148">세 번째와 네 번째 자습서- [ *Your 사이트를 사용 하 여 FTP 배포* ](deploying-your-site-using-an-ftp-client-cs.md) 하 고 [ *배포 사이트를 사용 하 여 Visual Studio* ](deploying-your-site-using-visual-studio-cs.md) -검사 다양 한 도구 및 기술을 이러한 파일을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-148">The third and fourth tutorials - [*Deploying Your Site Using FTP*](deploying-your-site-using-an-ftp-client-cs.md) and [*Deploying Your Site Using Visual Studio*](deploying-your-site-using-visual-studio-cs.md) - examine different tools and techniques for syncing these files.</span></span>

<span data-ttu-id="2dd49-149">사용 중인 일반적으로 두 데이터베이스는 데이터 기반 응용 프로그램을 빌드할 때: 개발 및 프로덕션에 각각 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-149">When building data-driven applications there are typically two databases being used: one for development and one on production.</span></span> <span data-ttu-id="2dd49-150">개발 하는 동안 개발 데이터베이스의 스키마를 새 테이블, 열, 저장된 프로시저 및 트리거를 포함 하도록 수정할 수 있습니다 또는 제거 하거나 기존 데이터베이스 개체 이름을 바꾸기로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-150">During development, the development database's schema may be modified to include new tables, columns, stored procedures, and triggers, or may be modified to remove or rename existing database objects.</span></span> <span data-ttu-id="2dd49-151">이러한 변경 내용이 적용 될 당시와 응용 프로그램이 프로덕션으로 배포 될 때 개발 및 프로덕션 데이터베이스에 동기화 되지 않습니다. 이 비동기 배포 프로세스 중 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-151">Between the time that these changes are made and the time the application is deployed to production, the development and production databases are out of sync. This asynchrony needs to be fixed during the deployment process.</span></span> <span data-ttu-id="2dd49-152">이후 자습서에서 이러한 문제를 검사할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-152">These challenges will be examined in future tutorials.</span></span>

## <a name="finding-a-web-host-provider"></a><span data-ttu-id="2dd49-153">웹 호스트 공급자 찾기</span><span class="sxs-lookup"><span data-stu-id="2dd49-153">Finding a Web Host Provider</span></span>

<span data-ttu-id="2dd49-154">.NET Framework 및 인터넷 정보 서비스 (IIS)가 설치 되어 있는 모든 웹 서버에 ASP.NET 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-154">ASP.NET applications can be deployed to any web server that has the .NET Framework and Internet Information Services (IIS) installed.</span></span> <span data-ttu-id="2dd49-155">개인 컴퓨터에서 인터넷 및 파악 하는 광대역 연결 들어오는 웹 요청을 허용 하도록 라우터를 구성 하는 방법으로 열었던 가정 하 고 사이트를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-155">You could host a site from your personal computer, assuming you had a broadband connection to the Internet and the know how to configure your router to allow incoming web requests.</span></span> <span data-ttu-id="2dd49-156">또한 대부분의 회사와 마찬가지로 인트라넷 컴퓨터에서 사이트를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-156">You could also host a site from a computer in an intranet, as many companies do.</span></span> <span data-ttu-id="2dd49-157">그러나이 자습서의 포커스를 웹 호스트 공급자를 사용 하 여 웹 사이트를 호스팅입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-157">The focus of these tutorials, however, is hosting your website with a web host provider.</span></span>

> [!NOTE]
> <span data-ttu-id="2dd49-158">[IIS](https://www.iis.net/) Microsoft의 엔터프라이즈 수준 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-158">[IIS](https://www.iis.net/) is Microsoft's enterprise-grade web server.</span></span> <span data-ttu-id="2dd49-159">Windows, Windows Server 2008 등 특정 버전의 Windows Vista-홈 버전을 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-159">It ships with the non-Home editions of Windows, such as Windows Server 2008 and certain editions of Windows Vista.</span></span> <span data-ttu-id="2dd49-160">Visual Studio ASP.NET 개발 웹 서버를 포함 하는 대로 개발 환경에서 ASP.NET 응용 프로그램을 작동 하려면 IIS를 설치 하려면 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-160">You do not need to install IIS to serve ASP.NET applications in a development environment, as Visual Studio includes the ASP.NET Development Web Server.</span></span> <span data-ttu-id="2dd49-161">그러나 ASP.NET 개발 웹 서버를 로컬 연결만 허용 하 고 프로덕션 환경에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-161">However, the ASP.NET Development Web Server only accepts local connections and therefore cannot be used in a production environment.</span></span>


<span data-ttu-id="2dd49-162">웹 호스트 공급자에 사이트를 배포 하기 전에 사용 하 여 업무에 어떤 회사를 먼저 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-162">Before you can deploy your site to a web host provider you must first decide what company to do business with.</span></span> <span data-ttu-id="2dd49-163">수많은 웹 호스팅 회사 marketplace에는 "웹 호스팅 회사를"에 대 한 검색을 5 백만 개 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-163">There are countless web hosting companies in the marketplace; a search for "web hosting company" returns more than five million results.</span></span> <span data-ttu-id="2dd49-164">적합 한 하나 하려면 어떻게 해야 하십니까?</span><span class="sxs-lookup"><span data-stu-id="2dd49-164">How do you find the one that's right for you?</span></span> <span data-ttu-id="2dd49-165">원하는 검색 엔진이 좋은 시작 위치와 같은 웹 사이트 [TopHosts](http://www.tophosts.com/) 하 고 [HostCritique](http://www.hostcritique.net/)를 비교 하 고 다양 한 호스팅 서비스를 대조 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-165">Your favorite search engine is a good starting place, as are websites like [TopHosts](http://www.tophosts.com/) and [HostCritique](http://www.hostcritique.net/), which compare and contrast various hosting services.</span></span> <span data-ttu-id="2dd49-166">또한는 것이 좋습니다으로 동료와 동료 모든 권장 사항을 요청 권장 사항에 대 한 문의할 수도 있습니다는 [Open Forum 호스팅](https://forums.asp.net/158.aspx) 여기에 [ASP.NET 포럼](https://forums.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="2dd49-166">I also advise asking your colleagues and coworkers for any recommendations; you can also ask for recommendations at the [Hosting Open Forum](https://forums.asp.net/158.aspx) here at the [ASP.NET Forums](https://forums.asp.net/).</span></span>

<span data-ttu-id="2dd49-167">일반적으로 웹 호스팅 회사는 공유 호스팅 계획을 제공 하 고 전용 호스팅 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-167">Web hosting companies typically offer shared hosting plans and dedicated hosting plans.</span></span> <span data-ttu-id="2dd49-168">사용 하 여 공유는 단일 웹 서버 호스트 수백 없으면 수십 서로 다른 웹 사이트의 호스팅.</span><span class="sxs-lookup"><span data-stu-id="2dd49-168">With shared hosting a single web server hosts dozens if not hundreds of different websites.</span></span> <span data-ttu-id="2dd49-169">전용 호스팅 사용 하 여 사이트와 사이트를 단독으로 사용 되는 회사에서 컴퓨터를 임대 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-169">With dedicated hosting you lease a computer from the company that serves your site and your site alone.</span></span> <span data-ttu-id="2dd49-170">공유 호스팅 계획을 $9.95/월에 대 한 Microsoft Access 데이터베이스, 5GB의 디스크 공간 및 100GB의 월간 대역폭 트래픽에 사용할 수 있게 ASP.NET 페이지에 대 한 지원이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-170">A shared hosting plan might include support for ASP.NET pages, the ability to work with Microsoft Access databases, 5 GB of disk space, and 100 GB of monthly bandwidth traffic for $9.95 per month.</span></span> <span data-ttu-id="2dd49-171">다른 공유 호스팅 계획에는 $19.95 / 월에 대 한 Microsoft SQL Server 2008 데이터베이스 서버, 10GB의 디스크 공간 및 250GB의 월간 대역폭 트래픽에 액세스 ASP.NET 페이지에 대 한 지원을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-171">Another shared hosting plan might include support for ASP.NET pages, access to the Microsoft SQL Server 2008 database server, 10 GB of disk space and 250 GB of monthly bandwidth traffic for $19.95 per month.</span></span> <span data-ttu-id="2dd49-172">전용 호스팅 계획은 일반적으로 훨씬 더 비용이 많이 드는, 비용 몇 백 달러 월 하지만 더 나은 성능을 제공 하 고 공유 보다 세부적인 제어가 호스팅 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-172">Dedicated hosting plans are usually much more expensive, costing several hundred dollars per month, but offer better performance and more control than shared hosting options.</span></span> <span data-ttu-id="2dd49-173">어떤 계획을 선택 하면 예산에 따라 달라 집니다, 얼마나 많은 트래픽을 웹 사이트를 받고 기능 수를 예상 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-173">What plan you choose depends on your budget, how much traffic your website receives, and the features you anticipate you'll need.</span></span>

<span data-ttu-id="2dd49-174">웹 호스트 공급자를 선택할 때 두 가지 중요 한 고려 사항에는 고객 서비스 및 서비스 품질입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-174">Two important considerations when choosing a web host provider are customer service and quality of service.</span></span> <span data-ttu-id="2dd49-175">질문 또는 구성 문제가 있는 경우이 얼마를 응답에 도달할 때까지 기술 지원팀 웹 호스트의 문제를 제출?</span><span class="sxs-lookup"><span data-stu-id="2dd49-175">If you have a question or a configuration problem, how long does it take from submitting your problem to the web host's helpdesk until you get a response?</span></span> <span data-ttu-id="2dd49-176">회사의 서비스 안정성을 파악할?</span><span class="sxs-lookup"><span data-stu-id="2dd49-176">How reliable are the company's services?</span></span> <span data-ttu-id="2dd49-177">데이터베이스 작동 중단을 자주 이러한가지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2dd49-177">Do they frequently have database outages?</span></span> <span data-ttu-id="2dd49-178">자신의 전자 메일 서버는 얼마나 자주 오프 라인으로 전환?</span><span class="sxs-lookup"><span data-stu-id="2dd49-178">How often does their email server go offline?</span></span> <span data-ttu-id="2dd49-179">가 작동 하는 방법에 대 한 세부 정보를 제공 하 고 해당 고객 서비스 정책에 대 한 질의 시에 회사를 항상 확인 수 이지만 더 있으리라는 온라인 포럼, 뉴스 그룹 및 메일 listservs를 통해 수행할 수 있는 현재 및 과거 고객의 피드백을 .</span><span class="sxs-lookup"><span data-stu-id="2dd49-179">You can always ask a company to provide details about their uptime and inquire about their customer service policy, but a more surefire way is to solicit the feedback of current and past customers, which you can do through online forums, newsgroups, and email listservs.</span></span>

> [!NOTE]
> <span data-ttu-id="2dd49-180">일부 웹 호스팅 회사 업무를.NET과 같은 특정 기술 스택에서 집중 또는 [LAMP](http://en.wikipedia.org/wiki/LAMP_stack) (**L** inux 합니다 **A** pache, **M** ySQL, 및 **P** HP)를 선택 하면 회사 ASP.NET 응용 프로그램을 호스트 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-180">Some web hosting companies focus their business on a particular technology stack, such as .NET or [LAMP](http://en.wikipedia.org/wiki/LAMP_stack) (**L** inux, **A** pache, **M** ySQL, and **P** HP), so make sure that the company you select hosts ASP.NET applications.</span></span> <span data-ttu-id="2dd49-181">또한 응용 프로그램을 빌드하는 데 사용할 ASP.NET 버전 지 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-181">Also check to ensure that they support the version of ASP.NET you are using to build your application.</span></span> <span data-ttu-id="2dd49-182">및 데이터 기반 응용 프로그램을 작성 하는 경우 웹 호스트는 동일한 데이터베이스 서버 및 사용 중인 버전을 제공 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-182">And if you are building a data-driven application, make sure that the web host offers the same database server and version that you are using.</span></span>


## <a name="summary"></a><span data-ttu-id="2dd49-183">요약</span><span class="sxs-lookup"><span data-stu-id="2dd49-183">Summary</span></span>

<span data-ttu-id="2dd49-184">ASP.NET 웹 응용 프로그램은 일반적으로 디자인, 생성 및 로컬 개발 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="2dd49-184">ASP.NET web applications are typically designed, created, and tested in a local development environment.</span></span> <span data-ttu-id="2dd49-185">버전을 릴리스할 준비가 되 면 프로덕션 환경으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-185">Once a version is ready for release, it is moved to a production environment.</span></span> <span data-ttu-id="2dd49-186">호스트 ASP.NET 웹 사이트 또는 회사 내 서버 개인용 컴퓨터에서 수 있지만, 많은 기업 및 개인 웹 호스트 공급자에 해당 호스트를 아웃소싱하는 데 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-186">While it is possible to host ASP.NET websites on your personal computer or on servers within your company, many businesses and individuals choose to outsource their hosting to a web host provider.</span></span>

<span data-ttu-id="2dd49-187">이 자습서 시리즈에서는 일반적인 문제를 탐색 하는 웹 호스트 공급자를 ASP.NET 응용 프로그램을 배포 하는 단계를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-187">This tutorial series examines the steps for deploying an ASP.NET application to a web host provider, exploring common challenges.</span></span> <span data-ttu-id="2dd49-188">이 자습서는 ASP.NET 배포 프로세스의 상위 수준 개요를 제공 하 고 적합 한 웹 호스트 공급자를 찾기 위한 팁을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-188">This tutorial offered a high-level overview of the ASP.NET deployment process and gave tips for finding a suitable web host provider.</span></span> <span data-ttu-id="2dd49-189">다음 자습서 웹 사이트를 배포 하는 경우 프로덕션 환경에 복사 해야 하는 ASP.NET 관련 파일에 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-189">The next tutorial looks at what ASP.NET-related files need to be copied to the production environment when deploying your website.</span></span>

<span data-ttu-id="2dd49-190">즐거운 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="2dd49-190">Happy Programming!</span></span>

### <a name="special-thanks-to"></a><span data-ttu-id="2dd49-191">특별히 감사 하는 중...</span><span class="sxs-lookup"><span data-stu-id="2dd49-191">Special Thanks To…</span></span>

<span data-ttu-id="2dd49-192">이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-192">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="2dd49-193">이 자습서에 대 한 선행 검토자 Teresa Murphy 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-193">Lead reviewer for this tutorial was Teresa Murphy.</span></span> <span data-ttu-id="2dd49-194">내 향후 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="2dd49-194">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="2dd49-195">그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd49-195">If so, drop me a line at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2dd49-196">다음</span><span class="sxs-lookup"><span data-stu-id="2dd49-196">Next</span></span>](determining-what-files-need-to-be-deployed-cs.md)