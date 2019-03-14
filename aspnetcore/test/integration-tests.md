---
title: ASP.NET Core에서 통합 테스트
author: guardrex
description: 통합 테스트를 사용하여 앱의 구성 요소가 데이터베이스, 파일 시스템 및 네트워크를 비롯한 인프라 수준에서 제대로 작동하는지 확인하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/25/2019
uid: test/integration-tests
ms.openlocfilehash: 053713e148df70b0be6bb567b55b2381a78d6c3e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029340"
---
# <a name="integration-tests-in-aspnet-core"></a><span data-ttu-id="2986d-103">ASP.NET Core에서 통합 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-103">Integration tests in ASP.NET Core</span></span>

<span data-ttu-id="2986d-104">하 여 [Luke Latham](https://github.com/guardrex) 고 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="2986d-104">By [Luke Latham](https://github.com/guardrex) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="2986d-105">통합 테스트 데이터베이스, 파일 시스템 및 네트워크와 같은 앱의 지원 인프라를 포함 하는 수준에서 앱의 구성 요소가 제대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-105">Integration tests ensure that an app's components function correctly at a level that includes the app's supporting infrastructure, such as the database, file system, and network.</span></span> <span data-ttu-id="2986d-106">ASP.NET Core는 테스트 웹 호스트와 메모리 내 테스트 서버를 사용 하 여 단위 테스트 프레임 워크를 사용 하 여 통합 테스트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-106">ASP.NET Core supports integration tests using a unit test framework with a test web host and an in-memory test server.</span></span>

<span data-ttu-id="2986d-107">이 항목에서는 단위 테스트의 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-107">This topic assumes a basic understanding of unit tests.</span></span> <span data-ttu-id="2986d-108">테스트 개념을 잘 알 수 없는 경우 참조를 [Unit Testing.NET Core 및.NET Standard](/dotnet/core/testing/) 항목 및 해당 연결 된 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-108">If unfamiliar with test concepts, see the [Unit Testing in .NET Core and .NET Standard](/dotnet/core/testing/) topic and its linked content.</span></span>

<span data-ttu-id="2986d-109">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="2986d-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="2986d-110">샘플 앱은 Razor 페이지 앱 및 Razor 페이지의 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-110">The sample app is a Razor Pages app and assumes a basic understanding of Razor Pages.</span></span> <span data-ttu-id="2986d-111">Razor 페이지를 사용 하 여 알 수 없는 경우 다음 항목을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-111">If unfamiliar with Razor Pages, see the following topics:</span></span>

* [<span data-ttu-id="2986d-112">Razor 페이지 소개</span><span class="sxs-lookup"><span data-stu-id="2986d-112">Introduction to Razor Pages</span></span>](xref:razor-pages/index)
* [<span data-ttu-id="2986d-113">Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="2986d-113">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="2986d-114">Razor 페이지 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-114">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)

> [!NOTE]
> <span data-ttu-id="2986d-115">Spa를 테스트 하는 것에 대 한 것이 좋습니다는 도구와 같은 [Selenium](https://www.seleniumhq.org/)는 브라우저를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-115">For testing SPAs, we recommended a tool such as [Selenium](https://www.seleniumhq.org/), which can automate a browser.</span></span>

## <a name="introduction-to-integration-tests"></a><span data-ttu-id="2986d-116">통합 테스트 소개</span><span class="sxs-lookup"><span data-stu-id="2986d-116">Introduction to integration tests</span></span>

<span data-ttu-id="2986d-117">보다 광범위 한 수준에서 앱의 구성 요소를 평가 하는 통합 테스트 [단위 테스트](/dotnet/core/testing/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-117">Integration tests evaluate an app's components on a broader level than [unit tests](/dotnet/core/testing/).</span></span> <span data-ttu-id="2986d-118">단위 테스트는 개별 클래스 메서드와 같은 격리 된 소프트웨어 구성 요소를 테스트 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-118">Unit tests are used to test isolated software components, such as individual class methods.</span></span> <span data-ttu-id="2986d-119">통합 테스트는 두 개 이상의 앱 구성 요소 수 있는 완벽 하 게 요청을 처리 하는 데 필요한 모든 구성 요소를 포함 하 여 예상된 결과 생성 하기 위해 함께 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-119">Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.</span></span>

<span data-ttu-id="2986d-120">이러한 광범위 한 테스트는 앱의 인프라 및 종종 다음 구성 요소를 포함 하는 전체 프레임 워크를 테스트 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-120">These broader tests are used to test the app's infrastructure and whole framework, often including the following components:</span></span>

* <span data-ttu-id="2986d-121">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="2986d-121">Database</span></span>
* <span data-ttu-id="2986d-122">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="2986d-122">File system</span></span>
* <span data-ttu-id="2986d-123">네트워크 어플라이언스</span><span class="sxs-lookup"><span data-stu-id="2986d-123">Network appliances</span></span>
* <span data-ttu-id="2986d-124">요청-응답 파이프라인</span><span class="sxs-lookup"><span data-stu-id="2986d-124">Request-response pipeline</span></span>

<span data-ttu-id="2986d-125">단위 테스트 라고 위조 사용 하 여 구성 요소 *fakes* 하거나 *모의 개체*, 인프라 구성 요소 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-125">Unit tests use fabricated components, known as *fakes* or *mock objects*, in place of infrastructure components.</span></span>

<span data-ttu-id="2986d-126">단위 테스트와 달리 통합 테스트.</span><span class="sxs-lookup"><span data-stu-id="2986d-126">In contrast to unit tests, integration tests:</span></span>

* <span data-ttu-id="2986d-127">앱이 프로덕션 환경에서 사용 하는 실제 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-127">Use the actual components that the app uses in production.</span></span>
* <span data-ttu-id="2986d-128">자세한 코드 및 데이터 처리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-128">Require more code and data processing.</span></span>
* <span data-ttu-id="2986d-129">실행 하는 데 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-129">Take longer to run.</span></span>

<span data-ttu-id="2986d-130">따라서 가장 중요 한 인프라 시나리오에 대 한 통합 테스트의 사용을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-130">Therefore, limit the use of integration tests to the most important infrastructure scenarios.</span></span> <span data-ttu-id="2986d-131">단위 테스트 또는 통합 테스트를 사용 하 여 동작을 테스트할 수, 하는 경우 단위 테스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-131">If a behavior can be tested using either a unit test or an integration test, choose the unit test.</span></span>

> [!TIP]
> <span data-ttu-id="2986d-132">데이터베이스 및 파일 시스템을 사용 하 여 데이터 및 파일 액세스의 모든 가능한 순열에 대 한 통합 테스트를 작성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2986d-132">Don't write integration tests for every possible permutation of data and file access with databases and file systems.</span></span> <span data-ttu-id="2986d-133">앱에서 얼마나 많은 배치에 관계 없이 데이터베이스 및 파일 시스템, 읽기, 쓰기, 업데이트 및 삭제 통합 테스트는 일반적으로 적절 하 게 테스트 데이터베이스 수 및 파일 시스템 구성 요소 집합을 집중된 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-133">Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components.</span></span> <span data-ttu-id="2986d-134">이러한 구성 요소 상호 작용 하는 방법 논리의 일상적인 테스트에 대 한 사용 하 여 단위 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-134">Use unit tests for routine tests of method logic that interact with these components.</span></span> <span data-ttu-id="2986d-135">단위 테스트에서 인프라를 사용 하 여 fakes/mock 결과 테스트 실행이 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-135">In unit tests, the use of infrastructure fakes/mocks result in faster test execution.</span></span>

> [!NOTE]
> <span data-ttu-id="2986d-136">테스트 프로젝트는 자주 통합 테스트의 토론에서 호출 합니다 *테스트 대상 시스템*, 또는 줄여서 "SUT"입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-136">In discussions of integration tests, the tested project is frequently called the *system under test*, or "SUT" for short.</span></span>

## <a name="aspnet-core-integration-tests"></a><span data-ttu-id="2986d-137">ASP.NET Core 통합 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-137">ASP.NET Core integration tests</span></span>

<span data-ttu-id="2986d-138">ASP.NET Core에서 통합 테스트 하려면 다음 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-138">Integration tests in ASP.NET Core require the following:</span></span>

* <span data-ttu-id="2986d-139">테스트 프로젝트를 포함 하 고 테스트를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-139">A test project is used to contain and execute the tests.</span></span> <span data-ttu-id="2986d-140">테스트 프로젝트에 호출 테스트 ASP.NET Core 프로젝트에 대 한 참조를 *테스트 중인 시스템* (SUT).</span><span class="sxs-lookup"><span data-stu-id="2986d-140">The test project has a reference to the tested ASP.NET Core project, called the *system under test* (SUT).</span></span> <span data-ttu-id="2986d-141">_"SUT" 테스트 앱을 가리키도록이 항목 전체에서 사용 됩니다._</span><span class="sxs-lookup"><span data-stu-id="2986d-141">_"SUT" is used throughout this topic to refer to the tested app._</span></span>
* <span data-ttu-id="2986d-142">테스트 프로젝트는 SUT에 대 한 테스트 웹 호스트를 만들고 요청 및 응답을 SUT 처리 하기 위해 테스트 서버 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-142">The test project creates a test web host for the SUT and uses a test server client to handle requests and responses to the SUT.</span></span>
* <span data-ttu-id="2986d-143">테스트 결과 테스트와 보고서를 실행 하는 test runner는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-143">A test runner is used to execute the tests and report the test results.</span></span>

<span data-ttu-id="2986d-144">통합 테스트는 일반적인 포함 하는 이벤트의 순서에 따라 *정렬*하십시오 *Act*, 및 *Assert* 테스트 단계:</span><span class="sxs-lookup"><span data-stu-id="2986d-144">Integration tests follow a sequence of events that include the usual *Arrange*, *Act*, and *Assert* test steps:</span></span>

1. <span data-ttu-id="2986d-145">SUT의 웹 호스트 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-145">The SUT's web host is configured.</span></span>
1. <span data-ttu-id="2986d-146">앱에 대 한 요청을 제출 하는 테스트 서버 클라이언트 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-146">A test server client is created to submit requests to the app.</span></span>
1. <span data-ttu-id="2986d-147">합니다 *정렬* 테스트 단계가 실행 됩니다. 테스트 응용 프로그램 요청을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-147">The *Arrange* test step is executed: The test app prepares a request.</span></span>
1. <span data-ttu-id="2986d-148">합니다 *Act* 테스트 단계가 실행 됩니다. 클라이언트 요청을 제출 하 고 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-148">The *Act* test step is executed: The client submits the request and receives the response.</span></span>
1. <span data-ttu-id="2986d-149">합니다 *Assert* 테스트 단계가 실행 됩니다. *실제* 응답으로 유효성을 검사를 *전달* 또는 *실패* 기반을 *예상* 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-149">The *Assert* test step is executed: The *actual* response is validated as a *pass* or *fail* based on an *expected* response.</span></span>
1. <span data-ttu-id="2986d-150">프로세스가 모든 테스트 실행 될 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-150">The process continues until all of the tests are executed.</span></span>
1. <span data-ttu-id="2986d-151">테스트 결과 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-151">The test results are reported.</span></span>

<span data-ttu-id="2986d-152">일반적으로 테스트에 대 한 앱의 일반적인 웹 호스트를 실행 하는 보다 테스트 웹 호스트를 다르게 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-152">Usually, the test web host is configured differently than the app's normal web host for the test runs.</span></span> <span data-ttu-id="2986d-153">예를 들어, 다른 데이터베이스 또는 다른 앱 설정을 테스트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-153">For example, a different database or different app settings might be used for the tests.</span></span>

<span data-ttu-id="2986d-154">테스트 웹 호스트 및 메모리 내 테스트 서버와 같은 인프라 구성 요소 ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)), 제공 또는 관리 하는 [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-154">Infrastructure components, such as the test web host and in-memory test server ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)), are provided or managed by the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package.</span></span> <span data-ttu-id="2986d-155">이 패키지의 사용 하 여 테스트 만들기 및 실행을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-155">Use of this package streamlines test creation and execution.</span></span>

<span data-ttu-id="2986d-156">`Microsoft.AspNetCore.Mvc.Testing` 패키지에는 다음 작업을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-156">The `Microsoft.AspNetCore.Mvc.Testing` package handles the following tasks:</span></span>

* <span data-ttu-id="2986d-157">종속성 파일을 복사 (*\*.deps*)에서 테스트 프로젝트의 SUT *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-157">Copies the dependencies file (*\*.deps*) from the SUT into the test project's *bin* folder.</span></span>
* <span data-ttu-id="2986d-158">정적 파일 및 페이지/뷰 테스트를 실행 하는 경우 찾을 수 있도록 SUT의 프로젝트 루트 콘텐츠 루트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-158">Sets the content root to the SUT's project root so that static files and pages/views are found when the tests are executed.</span></span>
* <span data-ttu-id="2986d-159">제공 된 [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) 클래스를 사용 하 여 SUT 부트스트래핑 간단 하 게 `TestServer`합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-159">Provides the [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) class to streamline bootstrapping the SUT with `TestServer`.</span></span>

<span data-ttu-id="2986d-160">합니다 [단위 테스트](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) 설명서에는 테스트 프로젝트 및 테스트 러너, 테스트 및 방법에 대 한 권장 사항을 이름 테스트를 실행 하 여 클래스를 테스트 하는 방법에 자세한 지침과 함께 설정 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-160">The [unit tests](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) documentation describes how to set up a test project and test runner, along with detailed instructions on how to run tests and recommendations for how to name tests and test classes.</span></span>

> [!NOTE]
> <span data-ttu-id="2986d-161">앱에 대 한 테스트 프로젝트를 만들 때 다른 프로젝트에 통합 테스트에서 단위 테스트를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-161">When creating a test project for an app, separate the unit tests from the integration tests into different projects.</span></span> <span data-ttu-id="2986d-162">이렇게 하면 단위 테스트에 포함 된 테스트 구성 요소 인프라 되지 실수로.</span><span class="sxs-lookup"><span data-stu-id="2986d-162">This helps ensure that infrastructure testing components aren't accidently included in the unit tests.</span></span> <span data-ttu-id="2986d-163">분리 단위 및 통합 테스트에서는 실행 되는 테스트 집합을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-163">Separation of unit and integration tests also allows control over which set of tests are run.</span></span>

<span data-ttu-id="2986d-164">차이가 거의 없는 Razor 페이지 앱의 테스트에 대 한 구성 및 MVC 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-164">There's virtually no difference between the configuration for tests of Razor Pages apps and MVC apps.</span></span> <span data-ttu-id="2986d-165">유일한 차이점은 테스트의 이름을 지정 하는 방법의 경우</span><span class="sxs-lookup"><span data-stu-id="2986d-165">The only difference is in how the tests are named.</span></span> <span data-ttu-id="2986d-166">Razor 페이지 앱에서 페이지 끝점의 테스트는 일반적으로 명명 된 페이지 모델 클래스 (예를 들어 `IndexPageTests` 인덱스 페이지에 대 한 구성 요소 통합을 테스트).</span><span class="sxs-lookup"><span data-stu-id="2986d-166">In a Razor Pages app, tests of page endpoints are usually named after the page model class (for example, `IndexPageTests` to test component integration for the Index page).</span></span> <span data-ttu-id="2986d-167">MVC 앱에서 테스트는 일반적으로 컨트롤러 클래스 별로 구성 및 테스트 컨트롤러의 이름을 딴 (예를 들어 `HomeControllerTests` 홈 컨트롤러에 대 한 구성 요소 통합을 테스트).</span><span class="sxs-lookup"><span data-stu-id="2986d-167">In an MVC app, tests are usually organized by controller classes and named after the controllers they test (for example, `HomeControllerTests` to test component integration for the Home controller).</span></span>

## <a name="test-app-prerequisites"></a><span data-ttu-id="2986d-168">테스트 앱 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2986d-168">Test app prerequisites</span></span>

<span data-ttu-id="2986d-169">테스트 프로젝트는 다음 작업을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-169">The test project must:</span></span>

* <span data-ttu-id="2986d-170">다음 패키지를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-170">Reference the following packages:</span></span>
  * [<span data-ttu-id="2986d-171">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="2986d-171">Microsoft.AspNetCore.App</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)
  * [<span data-ttu-id="2986d-172">Microsoft.AspNetCore.Mvc.Testing</span><span class="sxs-lookup"><span data-stu-id="2986d-172">Microsoft.AspNetCore.Mvc.Testing</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing/)
* <span data-ttu-id="2986d-173">Web SDK 프로젝트 파일에 지정 (`<Project Sdk="Microsoft.NET.Sdk.Web">`).</span><span class="sxs-lookup"><span data-stu-id="2986d-173">Specify the Web SDK in the project file (`<Project Sdk="Microsoft.NET.Sdk.Web">`).</span></span> <span data-ttu-id="2986d-174">웹 SDK를 참조할 때 필요 합니다 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-174">The Web SDK is required when referencing the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

<span data-ttu-id="2986d-175">이러한 필수 구성이 요소에서 볼 수 있습니다 합니다 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-175">These prerequisites can be seen in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/).</span></span> <span data-ttu-id="2986d-176">검사는 *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-176">Inspect the *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj* file.</span></span> <span data-ttu-id="2986d-177">샘플 앱에서는 합니다 [xUnit](https://xunit.github.io/) 테스트 프레임 워크와 [AngleSharp](https://anglesharp.github.io/) 파서 라이브러리, 샘플 앱 참조 하므로:</span><span class="sxs-lookup"><span data-stu-id="2986d-177">The sample app uses the [xUnit](https://xunit.github.io/) test framework and the [AngleSharp](https://anglesharp.github.io/) parser library, so the sample app also references:</span></span>

* [<span data-ttu-id="2986d-178">xunit</span><span class="sxs-lookup"><span data-stu-id="2986d-178">xunit</span></span>](https://www.nuget.org/packages/xunit/)
* [<span data-ttu-id="2986d-179">xunit.runner.visualstudio</span><span class="sxs-lookup"><span data-stu-id="2986d-179">xunit.runner.visualstudio</span></span>](https://www.nuget.org/packages/xunit.runner.visualstudio/)
* [<span data-ttu-id="2986d-180">AngleSharp</span><span class="sxs-lookup"><span data-stu-id="2986d-180">AngleSharp</span></span>](https://www.nuget.org/packages/AngleSharp/)

## <a name="sut-environment"></a><span data-ttu-id="2986d-181">SUT 환경</span><span class="sxs-lookup"><span data-stu-id="2986d-181">SUT environment</span></span>

<span data-ttu-id="2986d-182">경우는 SUT [환경](xref:fundamentals/environments) 설정 되지 않은 환경에 대 한 기본값으로 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-182">If the SUT's [environment](xref:fundamentals/environments) isn't set, the environment defaults to Development.</span></span>

## <a name="basic-tests-with-the-default-webapplicationfactory"></a><span data-ttu-id="2986d-183">Basic는 WebApplicationFactory 기본값을 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-183">Basic tests with the default WebApplicationFactory</span></span>

<span data-ttu-id="2986d-184">[WebApplicationFactory&lt;TEntryPoint&gt; ](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) 만드는 데 사용 되는 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) 통합 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-184">[WebApplicationFactory&lt;TEntryPoint&gt;](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) is used to create a [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) for the integration tests.</span></span> <span data-ttu-id="2986d-185">`TEntryPoint` SUT의 진입점 클래스는 일반적으로 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-185">`TEntryPoint` is the entry point class of the SUT, usually the `Startup` class.</span></span>

<span data-ttu-id="2986d-186">테스트 클래스 구현 된 *클래스 fixture* 인터페이스 ([IClassFixture](https://xunit.github.io/docs/shared-context#class-fixture))를 나타내고 클래스 테스트가 포함 된 클래스에서 테스트 간에 공유 개체 인스턴스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-186">Test classes implement a *class fixture* interface ([IClassFixture](https://xunit.github.io/docs/shared-context#class-fixture)) to indicate the class contains tests and provide shared object instances across the tests in the class.</span></span>

### <a name="basic-test-of-app-endpoints"></a><span data-ttu-id="2986d-187">앱 끝점의 기본 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-187">Basic test of app endpoints</span></span>

<span data-ttu-id="2986d-188">클래스를 테스트 `BasicTests`를 사용 하 여는 `WebApplicationFactory` 는 SUT 부트스트랩 제공 하는 [HttpClient](/dotnet/api/system.net.http.httpclient) 테스트 메서드에 `Get_EndpointsReturnSuccessAndCorrectContentType`합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-188">The following test class, `BasicTests`, uses the `WebApplicationFactory` to bootstrap the SUT and provide an [HttpClient](/dotnet/api/system.net.http.httpclient) to a test method, `Get_EndpointsReturnSuccessAndCorrectContentType`.</span></span> <span data-ttu-id="2986d-189">메서드가 성공한 경우 응답 상태 코드를 검사 (범위 200-299 상태 코드) 및 `Content-Type` 헤더는 `text/html; charset=utf-8` 여러 앱 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-189">The method checks if the response status code is successful (status codes in the range 200-299) and the `Content-Type` header is `text/html; charset=utf-8` for several app pages.</span></span>

<span data-ttu-id="2986d-190">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) 의 인스턴스를 만들고 `HttpClient` 자동 리디렉션을 따릅니다를 쿠키를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-190">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) creates an instance of `HttpClient` that automatically follows redirects and handles cookies.</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet1)]

### <a name="test-a-secure-endpoint"></a><span data-ttu-id="2986d-191">보안 끝점을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-191">Test a secure endpoint</span></span>

<span data-ttu-id="2986d-192">다른 테스트는 `BasicTests` 보안 끝점을 인증 되지 않은 사용자를 앱의 로그인 페이지로 리디렉션하는 클래스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-192">Another test in the `BasicTests` class checks that a secure endpoint redirects an unauthenticated user to the app's Login page.</span></span>

<span data-ttu-id="2986d-193">SUT에서 `/SecurePage` 사용 하 여 페이지를 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 적용 하기 위한 규칙을 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 페이지로.</span><span class="sxs-lookup"><span data-stu-id="2986d-193">In the SUT, the `/SecurePage` page uses an [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention to apply an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page.</span></span> <span data-ttu-id="2986d-194">자세한 내용은 [Razor 페이지 권한 부여 규칙](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-194">For more information, see [Razor Pages authorization conventions](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page).</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet1)]

<span data-ttu-id="2986d-195">에 `Get_SecurePageRequiresAnAuthenticatedUser` 테스트를 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) 리디렉션을 허용 하지 않도록 설정 하 여 설정 됩니다 [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) 에 `false`:</span><span class="sxs-lookup"><span data-stu-id="2986d-195">In the `Get_SecurePageRequiresAnAuthenticatedUser` test, a [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) is set to disallow redirects by setting [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) to `false`:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet2)]

<span data-ttu-id="2986d-196">리디렉션에 따라 클라이언트를 허용 하지 않습니다, 다음 확인을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-196">By disallowing the client to follow the redirect, the following checks can be made:</span></span>

* <span data-ttu-id="2986d-197">SUT에서 반환 된 상태 코드를 확인할 수 있습니다 예상에 대 한 [HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode) 결과 만드는 것이 로그인 페이지로 리디렉션 후 최종 상태 코드가 아닌 [HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span><span class="sxs-lookup"><span data-stu-id="2986d-197">The status code returned by the SUT can be checked against the expected [HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode) result, not the final status code after the redirect to the Login page, which would be [HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span></span>
* <span data-ttu-id="2986d-198">합니다 `Location` 응답 헤더에 헤더 값이 시작 하는 것인지 확인 됩니다 `http://localhost/Identity/Account/Login`, 하지 최종 로그인 페이지 응답 위치를 `Location` 헤더 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-198">The `Location` header value in the response headers is checked to confirm that it starts with `http://localhost/Identity/Account/Login`, not the final Login page response, where the `Location` header wouldn't be present.</span></span>

<span data-ttu-id="2986d-199">에 대 한 자세한 `WebApplicationFactoryClientOptions`를 참조 합니다 [클라이언트 옵션](#client-options) 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-199">For more information on `WebApplicationFactoryClientOptions`, see the [Client options](#client-options) section.</span></span>

## <a name="customize-webapplicationfactory"></a><span data-ttu-id="2986d-200">WebApplicationFactory 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2986d-200">Customize WebApplicationFactory</span></span>

<span data-ttu-id="2986d-201">웹 호스트 구성에서 상속 하 여 테스트 클래스와 독립적으로 만들 수 있습니다 `WebApplicationFactory` 하나 이상의 사용자 지정 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-201">Web host configuration can be created independently of the test classes by inheriting from `WebApplicationFactory` to create one or more custom factories:</span></span>

1. <span data-ttu-id="2986d-202">상속 `WebApplicationFactory` 시키고 [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-202">Inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost).</span></span> <span data-ttu-id="2986d-203">합니다 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 사용 하 여 서비스 컬렉션의 구성을 허용 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span><span class="sxs-lookup"><span data-stu-id="2986d-203">The [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) allows the configuration of the service collection with [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/CustomWebApplicationFactory.cs?name=snippet1)]

   <span data-ttu-id="2986d-204">데이터베이스에서 시드를 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 의해 수행 되는 `InitializeDbForTests` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2986d-204">Database seeding in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is performed by the `InitializeDbForTests` method.</span></span> <span data-ttu-id="2986d-205">메서드는에 설명 되어는 [통합 테스트 샘플: 테스트 앱 조직을](#test-app-organization) 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-205">The method is described in the [Integration tests sample: Test app organization](#test-app-organization) section.</span></span>

2. <span data-ttu-id="2986d-206">사용자 지정을 사용 하 여 `CustomWebApplicationFactory` 테스트 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-206">Use the custom `CustomWebApplicationFactory` in test classes.</span></span> <span data-ttu-id="2986d-207">다음 예제에서는에서 팩터리를 `IndexPageTests` 클래스:</span><span class="sxs-lookup"><span data-stu-id="2986d-207">The following example uses the factory in the `IndexPageTests` class:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet1)]

   <span data-ttu-id="2986d-208">방지 하도록 구성 된 샘플 앱의 클라이언트는 `HttpClient` 에서 다음 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-208">The sample app's client is configured to prevent the `HttpClient` from following redirects.</span></span> <span data-ttu-id="2986d-209">에 설명 된 대로 합니다 [보안 끝점을 테스트](#test-a-secure-endpoint) 섹션에서는 앱의 첫 번째 응답의 결과 확인 하는 테스트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-209">As explained in the [Test a secure endpoint](#test-a-secure-endpoint) section, this permits tests to check the result of the app's first response.</span></span> <span data-ttu-id="2986d-210">첫 번째 응답은 리디렉션을 사용 하 여 이러한 테스트의 대부분을 `Location` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-210">The first response is a redirect in many of these tests with a `Location` header.</span></span>

3. <span data-ttu-id="2986d-211">일반적인 테스트를 사용 하는 `HttpClient` 및 요청 및 응답을 처리 하기 위해 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="2986d-211">A typical test uses the `HttpClient` and helper methods to process the request and the response:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet2)]

<span data-ttu-id="2986d-212">SUT 대 한 모든 POST 요청에는 앱의 자동으로 수행 하는 위조 방지 검사를 충족 해야 합니다 [데이터 보호 위조 방지 시스템](xref:security/data-protection/introduction)입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-212">Any POST request to the SUT must satisfy the antiforgery check that's automatically made by the app's [data protection antiforgery system](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="2986d-213">테스트의 POST 요청을 정렬 하기 위해 앱 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-213">In order to arrange for a test's POST request, the test app must:</span></span>

1. <span data-ttu-id="2986d-214">페이지에 대 한 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-214">Make a request for the page.</span></span>
1. <span data-ttu-id="2986d-215">위조 방지 쿠키 및 응답에서 요청 유효성 검사 토큰을 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-215">Parse the antiforgery cookie and request validation token from the response.</span></span>
1. <span data-ttu-id="2986d-216">현재 위치에서 위조 방지 쿠키 및 요청 유효성 검사를 사용 하 여 POST 요청 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-216">Make the POST request with the antiforgery cookie and request validation token in place.</span></span>

<span data-ttu-id="2986d-217">합니다 `SendAsync` 도우미 확장 메서드 (*Helpers/HttpClientExtensions.cs*) 및 `GetDocumentAsync` 도우미 메서드 (*Helpers/HtmlHelpers.cs*)에 [샘플앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/) 를 사용 합니다 [AngleSharp](https://anglesharp.github.io/) 다음 메서드를 사용 하 여 위조 방지 검사를 처리 하는 파서:</span><span class="sxs-lookup"><span data-stu-id="2986d-217">The `SendAsync` helper extension methods (*Helpers/HttpClientExtensions.cs*) and the `GetDocumentAsync` helper method (*Helpers/HtmlHelpers.cs*) in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/) use the [AngleSharp](https://anglesharp.github.io/) parser to handle the antiforgery check with the following methods:</span></span>

* <span data-ttu-id="2986d-218">`GetDocumentAsync` &ndash; 수신 합니다 [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) 반환 하 고는 `IHtmlDocument`합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-218">`GetDocumentAsync` &ndash; Receives the [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) and returns an `IHtmlDocument`.</span></span> <span data-ttu-id="2986d-219">`GetDocumentAsync` 준비 하는 팩터리를 사용 하는 *가상 응답* 원본을 `HttpResponseMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-219">`GetDocumentAsync` uses a factory that prepares a *virtual response* based on the original `HttpResponseMessage`.</span></span> <span data-ttu-id="2986d-220">자세한 내용은 참조는 [AngleSharp 설명서](https://github.com/AngleSharp/AngleSharp#documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-220">For more information, see the [AngleSharp documentation](https://github.com/AngleSharp/AngleSharp#documentation).</span></span>
* <span data-ttu-id="2986d-221">`SendAsync` 에 대 한 확장 메서드는 `HttpClient` compose는 [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage) 호출 [SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) 는 SUT에 요청을 제출 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-221">`SendAsync` extension methods for the `HttpClient` compose an [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage) and call [SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) to submit requests to the SUT.</span></span> <span data-ttu-id="2986d-222">에 대 한 오버 로드가 `SendAsync` HTML 양식을 수락 (`IHtmlFormElement`) 및 다음:</span><span class="sxs-lookup"><span data-stu-id="2986d-222">Overloads for `SendAsync` accept the HTML form (`IHtmlFormElement`) and the following:</span></span>
  * <span data-ttu-id="2986d-223">폼의 단추를 제출 (`IHtmlElement`)</span><span class="sxs-lookup"><span data-stu-id="2986d-223">Submit button of the form (`IHtmlElement`)</span></span>
  * <span data-ttu-id="2986d-224">폼 값 컬렉션 (`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="2986d-224">Form values collection (`IEnumerable<KeyValuePair<string, string>>`)</span></span>
  * <span data-ttu-id="2986d-225">제출 단추 (`IHtmlElement`) 값을 구성 하 고 (`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="2986d-225">Submit button (`IHtmlElement`) and form values (`IEnumerable<KeyValuePair<string, string>>`)</span></span>

> [!NOTE]
> <span data-ttu-id="2986d-226">[AngleSharp](https://anglesharp.github.io/) 타사 구문 분석 하는 데모용으로이 항목에서는 샘플 앱에 사용 되는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-226">[AngleSharp](https://anglesharp.github.io/) is a third-party parsing library used for demonstration purposes in this topic and the sample app.</span></span> <span data-ttu-id="2986d-227">AngleSharp는 ASP.NET Core 앱의 통합 테스트에 필요한 또는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-227">AngleSharp isn't supported or required for integration testing of ASP.NET Core apps.</span></span> <span data-ttu-id="2986d-228">다른 파서 사용할 수와 같은 합니다 [Html 민첩성 팩 (HAP)](http://html-agility-pack.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-228">Other parsers can be used, such as the [Html Agility Pack (HAP)](http://html-agility-pack.net/).</span></span> <span data-ttu-id="2986d-229">다른 방법은 위조 방지 시스템의 요청 확인 토큰 및 위조 방지 쿠키를 직접 처리 하는 코드를 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-229">Another approach is to write code to handle the antiforgery system's request verification token and antiforgery cookie directly.</span></span>

## <a name="customize-the-client-with-withwebhostbuilder"></a><span data-ttu-id="2986d-230">WithWebHostBuilder 사용 하 여 클라이언트를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2986d-230">Customize the client with WithWebHostBuilder</span></span>

<span data-ttu-id="2986d-231">추가 구성 된 테스트 메서드 내에서 필요한 경우 [WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder) 만듭니다 `WebApplicationFactory` 와 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 추가로 구성 하 여 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-231">When additional configuration is required within a test method, [WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder) creates a new `WebApplicationFactory` with an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) that is further customized by configuration.</span></span>

<span data-ttu-id="2986d-232">합니다 `Post_DeleteMessageHandler_ReturnsRedirectToRoot` 의 메서드를 테스트 합니다 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 의 사용을 보여 줍니다 `WithWebHostBuilder`합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-232">The `Post_DeleteMessageHandler_ReturnsRedirectToRoot` test method of the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) demonstrates the use of `WithWebHostBuilder`.</span></span> <span data-ttu-id="2986d-233">이 테스트는 SUT에서 양식을 제출 하 여을 트리거하여 데이터베이스에서 레코드 삭제를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-233">This test performs a record delete in the database by triggering a form submission in the SUT.</span></span>

<span data-ttu-id="2986d-234">다른 테스트 하기 때문에 `IndexPageTests` 클래스의 모든 데이터베이스에 레코드를 삭제 하 고 전에 실행할 수는 작업을 수행 합니다 `Post_DeleteMessageHandler_ReturnsRedirectToRoot` 메서드, 데이터베이스 레코드를 삭제 하려면 SUT에 있는지 확인 하기 위해이 테스트 메서드에 시드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-234">Because another test in the `IndexPageTests` class performs an operation that deletes all of the records in the database and may run before the `Post_DeleteMessageHandler_ReturnsRedirectToRoot` method, the database is seeded in this test method to ensure that a record is present for the SUT to delete.</span></span> <span data-ttu-id="2986d-235">선택 하는 `deleteBtn1` 단추는 `messages` 는 SUT 요청에는 SUT 형태로 시뮬레이션 됩니다:</span><span class="sxs-lookup"><span data-stu-id="2986d-235">Selecting the `deleteBtn1` button of the `messages` form in the SUT is simulated in the request to the SUT:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet3)]

## <a name="client-options"></a><span data-ttu-id="2986d-236">클라이언트 옵션</span><span class="sxs-lookup"><span data-stu-id="2986d-236">Client options</span></span>

<span data-ttu-id="2986d-237">다음 표에서 기본 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) 를 만들 때 사용할 수 있는 `HttpClient` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2986d-237">The following table shows the default [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) available when creating `HttpClient` instances.</span></span>

| <span data-ttu-id="2986d-238">옵션</span><span class="sxs-lookup"><span data-stu-id="2986d-238">Option</span></span> | <span data-ttu-id="2986d-239">설명</span><span class="sxs-lookup"><span data-stu-id="2986d-239">Description</span></span> | <span data-ttu-id="2986d-240">기본</span><span class="sxs-lookup"><span data-stu-id="2986d-240">Default</span></span> |
| ------ | ----------- | ------- |
| [<span data-ttu-id="2986d-241">AllowAutoRedirect</span><span class="sxs-lookup"><span data-stu-id="2986d-241">AllowAutoRedirect</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) | <span data-ttu-id="2986d-242">가져오거나 여부 `HttpClient` 인스턴스 리디렉션 응답을 자동으로 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-242">Gets or sets whether or not `HttpClient` instances should automatically follow redirect responses.</span></span> | `true` |
| [<span data-ttu-id="2986d-243">BaseAddress</span><span class="sxs-lookup"><span data-stu-id="2986d-243">BaseAddress</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.baseaddress) | <span data-ttu-id="2986d-244">기본 주소를 가져오거나 설정 합니다. `HttpClient` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2986d-244">Gets or sets the base address of `HttpClient` instances.</span></span> | `http://localhost` |
| [<span data-ttu-id="2986d-245">HandleCookies</span><span class="sxs-lookup"><span data-stu-id="2986d-245">HandleCookies</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.handlecookies) | <span data-ttu-id="2986d-246">가져오거나 여부를 `HttpClient` 인스턴스 쿠키를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-246">Gets or sets whether `HttpClient` instances should handle cookies.</span></span> | `true` |
| [<span data-ttu-id="2986d-247">MaxAutomaticRedirections</span><span class="sxs-lookup"><span data-stu-id="2986d-247">MaxAutomaticRedirections</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.maxautomaticredirections) | <span data-ttu-id="2986d-248">최대 리디렉션 응답 수를 가져오거나 `HttpClient` 인스턴스 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-248">Gets or sets the maximum number of redirect responses that `HttpClient` instances should follow.</span></span> | <span data-ttu-id="2986d-249">7</span><span class="sxs-lookup"><span data-stu-id="2986d-249">7</span></span> |

<span data-ttu-id="2986d-250">만들기는 `WebApplicationFactoryClientOptions` 클래스를 전달 하는 [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) 메서드 (값이 코드 예제에 표시 되어 기본값):</span><span class="sxs-lookup"><span data-stu-id="2986d-250">Create the `WebApplicationFactoryClientOptions` class and pass it to the [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) method (default values are shown in the code example):</span></span>

```csharp
// Default client option values are shown
var clientOptions = new WebApplicationFactoryClientOptions();
clientOptions.AllowAutoRedirect = true;
clientOptions.BaseAddress = new Uri("http://localhost");
clientOptions.HandleCookies = true;
clientOptions.MaxAutomaticRedirections = 7;

_client = _factory.CreateClient(clientOptions);
```

## <a name="inject-mock-services"></a><span data-ttu-id="2986d-251">모의 서비스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-251">Inject mock services</span></span>

<span data-ttu-id="2986d-252">서비스에 대 한 호출을 사용 하 여 테스트에서 재정의할 수 있습니다 [ConfigureTestServices](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.configuretestservices) 호스트 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-252">Services can be overridden in a test with a call to [ConfigureTestServices](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.configuretestservices) on the host builder.</span></span> <span data-ttu-id="2986d-253">**모의 서비스를 삽입할는 SUT 있어야를 `Startup` 클래스는 `Startup.ConfigureServices` 메서드.**</span><span class="sxs-lookup"><span data-stu-id="2986d-253">**To inject mock services, the SUT must have a `Startup` class with a `Startup.ConfigureServices` method.**</span></span>

<span data-ttu-id="2986d-254">샘플 SUT 견적을 반환 하는 범위가 지정 된 서비스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-254">The sample SUT includes a scoped service that returns a quote.</span></span> <span data-ttu-id="2986d-255">견적은 인덱스 페이지가 요청 될 때 인덱스 페이지의 숨겨진된 필드에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-255">The quote is embedded in a hidden field on the Index page when the Index page is requested.</span></span>

<span data-ttu-id="2986d-256">*Services/IQuoteService.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-256">*Services/IQuoteService.cs*:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Services/IQuoteService.cs?name=snippet1)]

<span data-ttu-id="2986d-257">*Services/QuoteService.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-257">*Services/QuoteService.cs*:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Services/QuoteService.cs?name=snippet1)]

<span data-ttu-id="2986d-258">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-258">*Startup.cs*:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet2)]

<span data-ttu-id="2986d-259">*Pages/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-259">*Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Pages/Index.cshtml.cs?name=snippet1&highlight=4,9,20,26)]

<span data-ttu-id="2986d-260">*Pages/Index.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-260">*Pages/Index.cs*:</span></span>

[!code-cshtml[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Pages/Index.cshtml?name=snippet_Quote)]

<span data-ttu-id="2986d-261">다음 태그는 SUT 앱이 실행 될 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-261">The following markup is generated when the SUT app is run:</span></span>

```html
<input id="quote" type="hidden" value="Come on, Sarah. We&#x27;ve an appointment in 
    London, and we&#x27;re already 30,000 years late.">
```

<span data-ttu-id="2986d-262">서비스 및 견적 주입 통합 테스트에서를 테스트 하려면 테스트에서 모의 서비스는는 SUT에 주입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-262">To test the service and quote injection in an integration test, a mock service is injected into the SUT by the test.</span></span> <span data-ttu-id="2986d-263">모의 서비스 응용 프로그램의 대체 `QuoteService` 테스트 앱에서 제공 하는 서비스를 사용 하 여 호출 `TestQuoteService`:</span><span class="sxs-lookup"><span data-stu-id="2986d-263">The mock service replaces the app's `QuoteService` with a service provided by the test app, called `TestQuoteService`:</span></span>

<span data-ttu-id="2986d-264">*IntegrationTests.IndexPageTests.cs*:</span><span class="sxs-lookup"><span data-stu-id="2986d-264">*IntegrationTests.IndexPageTests.cs*:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet4)]

<span data-ttu-id="2986d-265">`ConfigureTestServices` 호출 되 고 범위가 지정 된 서비스에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-265">`ConfigureTestServices` is called, and the scoped service is registered:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet5&highlight=7-10,17,20-21)]

<span data-ttu-id="2986d-266">테스트의 실행 중에 생성 된 태그를 반영 하 여 제공 된 견적 텍스트 `TestQuoteService`, 따라서 어설션 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-266">The markup produced during the test's execution reflects the quote text supplied by `TestQuoteService`, thus the assertion passes:</span></span>

```html
<input id="quote" type="hidden" value="Something&#x27;s interfering with time, 
    Mr. Scarman, and time is my business.">
```

## <a name="how-the-test-infrastructure-infers-the-app-content-root-path"></a><span data-ttu-id="2986d-267">테스트 인프라에서 앱 콘텐츠 루트 경로 유추 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2986d-267">How the test infrastructure infers the app content root path</span></span>

<span data-ttu-id="2986d-268">합니다 `WebApplicationFactory` 생성자에 대 한 검색 하 여 앱 콘텐츠 루트 경로 유추를 [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute) 같은 키를 사용 하 여 통합 테스트를 포함 하는 어셈블리에는 `TEntryPoint` 어셈블리`System.Reflection.Assembly.FullName`.</span><span class="sxs-lookup"><span data-stu-id="2986d-268">The `WebApplicationFactory` constructor infers the app content root path by searching for a [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute) on the assembly containing the integration tests with a key equal to the `TEntryPoint` assembly `System.Reflection.Assembly.FullName`.</span></span> <span data-ttu-id="2986d-269">경우 올바른 키를 사용 하 여 특성을 찾을 수 없으면 `WebApplicationFactory` 대체 솔루션 파일을 검색 합니다 (*\*.sln*) 추가 하 고는 `TEntryPoint` 솔루션 디렉터리에 어셈블리 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-269">In case an attribute with the correct key isn't found, `WebApplicationFactory` falls back to searching for a solution file (*\*.sln*) and appends the `TEntryPoint` assembly name to the solution directory.</span></span> <span data-ttu-id="2986d-270">응용 프로그램 루트 디렉터리 (콘텐츠 루트 경로) 뷰 및 콘텐츠 파일을 검색할 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-270">The app root directory (the content root path) is used to discover views and content files.</span></span>

<span data-ttu-id="2986d-271">대부분의 경우에서 필요는 없습니다 앱 콘텐츠 루트를 명시적으로 설정 검색 논리는 일반적으로 런타임 시 올바른 콘텐츠 루트를 찾으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-271">In most cases, it isn't necessary to explicitly set the app content root, as the search logic usually finds the correct content root at runtime.</span></span> <span data-ttu-id="2986d-272">콘텐츠 루트는 없는 특별 한 시나리오에서 기본 제공 검색 알고리즘을 명시적으로 또는 사용자 지정 논리를 사용 하 여 루트를 지정할 수 있습니다 콘텐츠 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-272">In special scenarios where the content root isn't found using the built-in search algorithm, the app content root can be specified explicitly or by using custom logic.</span></span> <span data-ttu-id="2986d-273">이러한 시나리오에서 앱 콘텐츠 루트를 설정 하려면 호출을 `UseSolutionRelativeContentRoot` 에서 확장 메서드는 [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-273">To set the app content root in those scenarios, call the `UseSolutionRelativeContentRoot` extension method from the [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost) package.</span></span> <span data-ttu-id="2986d-274">솔루션의 상대 경로 및 선택적 솔루션 파일 이름 또는 와일드 카드 사용 패턴을 제공 (기본값 = `*.sln`).</span><span class="sxs-lookup"><span data-stu-id="2986d-274">Supply the solution's relative path and optional solution file name or glob pattern (default = `*.sln`).</span></span>

<span data-ttu-id="2986d-275">호출 된 [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot) 확장 메서드를 사용 하 여 *하나* 다음 방법 중:</span><span class="sxs-lookup"><span data-stu-id="2986d-275">Call the [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot) extension method using *ONE* of the following approaches:</span></span>

* <span data-ttu-id="2986d-276">테스트 클래스를 구성할 때 `WebApplicationFactory`를 사용 하 여 사용자 지정 구성 정보를 제공 합니다 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span><span class="sxs-lookup"><span data-stu-id="2986d-276">When configuring test classes with `WebApplicationFactory`, provide a custom configuration with the [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span></span>

   ```csharp
   public IndexPageTests(
       WebApplicationFactory<RazorPagesProject.Startup> factory)
   {
       var _factory = factory.WithWebHostBuilder(builder =>
       {
           builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

           ...
       });
   }
   ```

* <span data-ttu-id="2986d-277">사용자 지정을 사용 하 여 테스트 클래스를 구성할 때 `WebApplicationFactory`에서 상속 `WebApplicationFactory` 시키고 [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span><span class="sxs-lookup"><span data-stu-id="2986d-277">When configuring test classes with a custom `WebApplicationFactory`, inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span></span>

   ```csharp
   public class CustomWebApplicationFactory<TStartup>
       : WebApplicationFactory<RazorPagesProject.Startup>
   {
       protected override void ConfigureWebHost(IWebHostBuilder builder)
       {
           builder.ConfigureServices(services =>
           {
               builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

               ...
           });
       }
   }
   ```

## <a name="disable-shadow-copying"></a><span data-ttu-id="2986d-278">섀도 복사를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="2986d-278">Disable shadow copying</span></span>

<span data-ttu-id="2986d-279">출력 폴더와 다른 폴더에서 실행할 테스트를 사용 하면 섀도 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-279">Shadow copying causes the tests to execute in a different folder than the output folder.</span></span> <span data-ttu-id="2986d-280">제대로 작동 하려면 테스트에 대 한 섀도 복사를 비활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-280">For tests to work properly, shadow copying must be disabled.</span></span> <span data-ttu-id="2986d-281">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) xUnit을 사용 하 고 포함 하 여 xunit 섀도 복사를 사용 하지 않도록 설정 된 *xunit.runner.json* 올바른 구성 설정 사용 하 여 파일.</span><span class="sxs-lookup"><span data-stu-id="2986d-281">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) uses xUnit and disables shadow copying for xUnit by including an *xunit.runner.json* file with the correct configuration setting.</span></span> <span data-ttu-id="2986d-282">자세한 내용은 [JSON을 사용 하 여 xUnit.net 구성](https://xunit.github.io/docs/configuring-with-json.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-282">For more information, see [Configuring xUnit.net with JSON](https://xunit.github.io/docs/configuring-with-json.html).</span></span>

<span data-ttu-id="2986d-283">추가 된 *xunit.runner.json* 다음 콘텐츠를 사용 하 여 테스트 프로젝트의 루트에 파일:</span><span class="sxs-lookup"><span data-stu-id="2986d-283">Add the *xunit.runner.json* file to root of the test project with the following content:</span></span>

```json
{
  "shadowCopy": false
}
```

## <a name="disposal-of-objects"></a><span data-ttu-id="2986d-284">개체 삭제</span><span class="sxs-lookup"><span data-stu-id="2986d-284">Disposal of objects</span></span>

<span data-ttu-id="2986d-285">테스트 후 합니다 `IClassFixture` 구현을 실행 됩니다 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) 및 [HttpClient](/dotnet/api/system.net.http.httpclient) xUnit 삭제 될 때 삭제 됩니다 합니다 [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) .</span><span class="sxs-lookup"><span data-stu-id="2986d-285">After the tests of the `IClassFixture` implementation are executed, [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) and [HttpClient](/dotnet/api/system.net.http.httpclient) are disposed when xUnit disposes of the [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1).</span></span> <span data-ttu-id="2986d-286">개발자가 인스턴스화된 개체 삭제에 필요한 경우에 삭제 된 `IClassFixture` 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-286">If objects instantiated by the developer require disposal, dispose of them in the `IClassFixture` implementation.</span></span> <span data-ttu-id="2986d-287">자세한 내용은 [Dispose 메서드 구현](/dotnet/standard/garbage-collection/implementing-dispose)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-287">For more information, see [Implementing a Dispose method](/dotnet/standard/garbage-collection/implementing-dispose).</span></span>

## <a name="integration-tests-sample"></a><span data-ttu-id="2986d-288">통합 테스트 샘플</span><span class="sxs-lookup"><span data-stu-id="2986d-288">Integration tests sample</span></span>

<span data-ttu-id="2986d-289">합니다 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 두 개의 앱으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-289">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is composed of two apps:</span></span>

| <span data-ttu-id="2986d-290">앱</span><span class="sxs-lookup"><span data-stu-id="2986d-290">App</span></span> | <span data-ttu-id="2986d-291">프로젝트 폴더</span><span class="sxs-lookup"><span data-stu-id="2986d-291">Project folder</span></span> | <span data-ttu-id="2986d-292">설명</span><span class="sxs-lookup"><span data-stu-id="2986d-292">Description</span></span> |
| --- | -------------- | ----------- |
| <span data-ttu-id="2986d-293">메시지 앱 (SUT)</span><span class="sxs-lookup"><span data-stu-id="2986d-293">Message app (the SUT)</span></span> | <span data-ttu-id="2986d-294">*src/RazorPagesProject*</span><span class="sxs-lookup"><span data-stu-id="2986d-294">*src/RazorPagesProject*</span></span> | <span data-ttu-id="2986d-295">추가, 하나를 삭제, all, 삭제 및 메시지를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-295">Allows a user to add, delete one, delete all, and analyze messages.</span></span> |
| <span data-ttu-id="2986d-296">테스트 앱</span><span class="sxs-lookup"><span data-stu-id="2986d-296">Test app</span></span> | <span data-ttu-id="2986d-297">*tests/RazorPagesProject.Tests*</span><span class="sxs-lookup"><span data-stu-id="2986d-297">*tests/RazorPagesProject.Tests*</span></span> | <span data-ttu-id="2986d-298">통합 테스트는 SUT 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-298">Used to integration test the SUT.</span></span> |

<span data-ttu-id="2986d-299">와 같은 기본 제공 테스트에 대 한 기능의 IDE 사용 하 여 테스트를 실행할 수 있습니다 [Visual Studio](https://www.visualstudio.com/vs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-299">The tests can be run using the built-in test features of an IDE, such as [Visual Studio](https://www.visualstudio.com/vs/).</span></span> <span data-ttu-id="2986d-300">사용 하는 경우 [Visual Studio Code](https://code.visualstudio.com/) 또는 명령줄에서 명령 프롬프트에서 다음 명령을 실행 합니다 *tests/RazorPagesProject.Tests* 폴더:</span><span class="sxs-lookup"><span data-stu-id="2986d-300">If using [Visual Studio Code](https://code.visualstudio.com/) or the command line, execute the following command at a command prompt in the *tests/RazorPagesProject.Tests* folder:</span></span>

```console
dotnet test
```

### <a name="message-app-sut-organization"></a><span data-ttu-id="2986d-301">메시지 앱 (SUT) 조직</span><span class="sxs-lookup"><span data-stu-id="2986d-301">Message app (SUT) organization</span></span>

<span data-ttu-id="2986d-302">SUT는 다음 특성을 사용 하 여 Razor 페이지 메시지 시스템:</span><span class="sxs-lookup"><span data-stu-id="2986d-302">The SUT is a Razor Pages message system with the following characteristics:</span></span>

* <span data-ttu-id="2986d-303">앱의 인덱스 페이지 (*pages/Index.cshtml* 하 고 *Pages/Index.cshtml.cs*) UI 및 페이지 추가, 삭제 및 메시지 (메시지 당 평균 단어) 분석을 제어 하려면 모델 메서드 제공 .</span><span class="sxs-lookup"><span data-stu-id="2986d-303">The Index page of the app (*Pages/Index.cshtml* and *Pages/Index.cshtml.cs*) provides a UI and page model methods to control the addition, deletion, and analysis of messages (average words per message).</span></span>
* <span data-ttu-id="2986d-304">메시지에서 설명 합니다 `Message` 클래스 (*Data/Message.cs*) 두 가지 속성을 사용 하 여: `Id` (키) 및 `Text` (메시지).</span><span class="sxs-lookup"><span data-stu-id="2986d-304">A message is described by the `Message` class (*Data/Message.cs*) with two properties: `Id` (key) and `Text` (message).</span></span> <span data-ttu-id="2986d-305">`Text` 속성 필요 하 고 200 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-305">The `Text` property is required and limited to 200 characters.</span></span>
* <span data-ttu-id="2986d-306">메시지를 사용 하 여 저장 됩니다 [Entity Framework의 메모리 내 데이터베이스](/ef/core/providers/in-memory/)&#8224;합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-306">Messages are stored using [Entity Framework's in-memory database](/ef/core/providers/in-memory/)&#8224;.</span></span>
* <span data-ttu-id="2986d-307">해당 데이터베이스 컨텍스트 클래스의를 DAL (데이터 액세스 계층)를 포함 하는 앱 `AppDbContext` (*Data/AppDbContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="2986d-307">The app contains a data access layer (DAL) in its database context class, `AppDbContext` (*Data/AppDbContext.cs*).</span></span>
* <span data-ttu-id="2986d-308">데이터베이스 앱 시작 시 비어 있으면 메시지 저장소는 세 개의 메시지를 사용 하 여 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-308">If the database is empty on app startup, the message store is initialized with three messages.</span></span>
* <span data-ttu-id="2986d-309">앱 포함을 `/SecurePage` 인증 된 사용자만 액세스할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-309">The app includes a `/SecurePage` that can only be accessed by an authenticated user.</span></span>

<span data-ttu-id="2986d-310">&#8224;EF 항목인 [inmemory 테스트](/ef/core/miscellaneous/testing/in-memory), MSTest 사용한 테스트에 대 한 메모리 내 데이터베이스를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-310">&#8224;The EF topic, [Test with InMemory](/ef/core/miscellaneous/testing/in-memory), explains how to use an in-memory database for tests with MSTest.</span></span> <span data-ttu-id="2986d-311">이 항목에서는 사용 된 [xUnit](https://xunit.github.io/) 테스트 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-311">This topic uses the [xUnit](https://xunit.github.io/) test framework.</span></span> <span data-ttu-id="2986d-312">테스트 개념 다른 테스트 프레임 워크에서 구현 테스트와 유사 하지만 동일 하지입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-312">Test concepts and test implementations across different test frameworks are similar but not identical.</span></span>

<span data-ttu-id="2986d-313">앱 리포지토리 패턴을 사용 하지 않습니다 하 고 효과적인 예가 없습니다 있지만 합니다 [작업 단위 (UoW) 패턴](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor 페이지는 이러한 패턴을 개발을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-313">Although the app doesn't use the repository pattern and isn't an effective example of the [Unit of Work (UoW) pattern](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor Pages supports these patterns of development.</span></span> <span data-ttu-id="2986d-314">자세한 내용은 [인프라 지 속성 계층 디자인](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design) 하 고 [컨트롤러 논리 테스트](/aspnet/core/mvc/controllers/testing) (샘플 리포지토리 패턴을 구현 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="2986d-314">For more information, see [Designing the infrastructure persistence layer](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design) and [Test controller logic](/aspnet/core/mvc/controllers/testing) (the sample implements the repository pattern).</span></span>

### <a name="test-app-organization"></a><span data-ttu-id="2986d-315">테스트 앱 구성</span><span class="sxs-lookup"><span data-stu-id="2986d-315">Test app organization</span></span>

<span data-ttu-id="2986d-316">테스트 앱 내에서 콘솔 앱은는 *tests/RazorPagesProject.Tests* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-316">The test app is a console app inside the *tests/RazorPagesProject.Tests* folder.</span></span>

| <span data-ttu-id="2986d-317">테스트 앱 폴더</span><span class="sxs-lookup"><span data-stu-id="2986d-317">Test app folder</span></span> | <span data-ttu-id="2986d-318">설명</span><span class="sxs-lookup"><span data-stu-id="2986d-318">Description</span></span> |
| --------------- | ----------- |
| <span data-ttu-id="2986d-319">*BasicTests*</span><span class="sxs-lookup"><span data-stu-id="2986d-319">*BasicTests*</span></span> | <span data-ttu-id="2986d-320">*BasicTests.cs* 라우팅, 인증 되지 않은 사용자, 보안 페이지에 액세스 하 고 GitHub 사용자 프로필 및 프로필의 사용자 로그인을 확인 하는 것에 대 한 테스트 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-320">*BasicTests.cs* contains test methods for routing, accessing a secure page by an unauthenticated user, and obtaining a GitHub user profile and checking the profile's user login.</span></span> |
| <span data-ttu-id="2986d-321">*IntegrationTests*</span><span class="sxs-lookup"><span data-stu-id="2986d-321">*IntegrationTests*</span></span> | <span data-ttu-id="2986d-322">*IndexPageTests.cs* 사용자 지정을 사용 하 여 인덱스 페이지에 대 한 통합 테스트를 포함 `WebApplicationFactory` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-322">*IndexPageTests.cs* contains the integration tests for the Index page using custom `WebApplicationFactory` class.</span></span> |
| <span data-ttu-id="2986d-323">*도우미/유틸리티*</span><span class="sxs-lookup"><span data-stu-id="2986d-323">*Helpers/Utilities*</span></span> | <ul><li><span data-ttu-id="2986d-324">*Utilities.cs* 포함 된 `InitializeDbForTests` 테스트 데이터로 데이터베이스 시드를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-324">*Utilities.cs* contains the `InitializeDbForTests` method used to seed the database with test data.</span></span></li><li><span data-ttu-id="2986d-325">*HtmlHelpers.cs* AngleSharp를 반환 하는 방법을 제공 `IHtmlDocument` 테스트 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-325">*HtmlHelpers.cs* provides a method to return an AngleSharp `IHtmlDocument` for use by the test methods.</span></span></li><li><span data-ttu-id="2986d-326">*HttpClientExtensions.cs* 에 대 한 오버 로드를 제공 `SendAsync` 는 SUT에 요청을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-326">*HttpClientExtensions.cs* provide overloads for `SendAsync` to submit requests to the SUT.</span></span></li></ul> |

<span data-ttu-id="2986d-327">테스트 프레임 워크 [xUnit](https://xunit.github.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-327">The test framework is [xUnit](https://xunit.github.io/).</span></span> <span data-ttu-id="2986d-328">통합 테스트를 사용 하 여 수행 되는 [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost)를 포함 하는 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver).</span><span class="sxs-lookup"><span data-stu-id="2986d-328">Integration tests are conducted using the [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost), which includes the [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver).</span></span> <span data-ttu-id="2986d-329">때문에 합니다 [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) 패키지는 테스트 호스트 및 테스트 서버를 구성 하는 데 사용 되는 `TestHost` 및 `TestServer` 패키지 테스트 앱의 프로젝트 파일에서 직접 패키지 참조가 필요 하지 않습니다 또는 테스트 앱의 개발자 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-329">Because the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package is used to configure the test host and test server, the `TestHost` and `TestServer` packages don't require direct package references in the test app's project file or developer configuration in the test app.</span></span>

<span data-ttu-id="2986d-330">**테스트에 대 한 데이터베이스 시드**</span><span class="sxs-lookup"><span data-stu-id="2986d-330">**Seeding the database for testing**</span></span>

<span data-ttu-id="2986d-331">통합 테스트는 테스트 실행 하기 전에 데이터베이스의 작은 데이터 집합을 일반적으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-331">Integration tests usually require a small dataset in the database prior to the test execution.</span></span> <span data-ttu-id="2986d-332">예를 들어 삭제 하므로 데이터베이스 delete 요청이 성공할 수에 대 한 레코드를 하나 이상 있어야 합니다. 데이터베이스 레코드 삭제에 대 한 호출을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2986d-332">For example, a delete test calls for a database record deletion, so the database must have at least one record for the delete request to succeed.</span></span>

<span data-ttu-id="2986d-333">샘플 앱에서 세 개의 메시지를 사용 하 여 데이터베이스를 시드합니다 *Utilities.cs* 테스트를 실행할 때 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="2986d-333">The sample app seeds the database with three messages in *Utilities.cs* that tests can use when they execute:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/Helpers/Utilities.cs?name=snippet1)]

## <a name="additional-resources"></a><span data-ttu-id="2986d-334">추가 자료</span><span class="sxs-lookup"><span data-stu-id="2986d-334">Additional resources</span></span>

* [<span data-ttu-id="2986d-335">단위 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-335">Unit tests</span></span>](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [<span data-ttu-id="2986d-336">Razor 페이지 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="2986d-336">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)
* [<span data-ttu-id="2986d-337">미들웨어</span><span class="sxs-lookup"><span data-stu-id="2986d-337">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="2986d-338">테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="2986d-338">Test controllers</span></span>](xref:mvc/controllers/testing)
