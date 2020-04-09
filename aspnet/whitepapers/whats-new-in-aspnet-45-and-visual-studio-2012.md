---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 와 비주얼 스튜디오 2012의 새로운 내용 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 ASP.NET 4.5에 도입되는 새로운 기능과 향상된 기능에 대해 설명합니다. 또한 웹 개발을 위해 개선된 사항에 대해서도 설명합니다...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675888"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="7b3ce-104">ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7b3ce-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="7b3ce-105">이 문서에서는 ASP.NET 4.5에 도입되는 새로운 기능과 향상된 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="7b3ce-106">또한 Visual Studio 2012의 웹 개발을 위해 개선된 사항에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="7b3ce-107">이 문서는 원래 2012년 2월 29일에 게시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="7b3ce-108">ASP.NET 코어 런타임 및 프레임워크</span><span class="sxs-lookup"><span data-stu-id="7b3ce-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="7b3ce-109">비동기적으로 HTTP 요청 및 응답 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="7b3ce-110">HttpRequest 처리 개선 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="7b3ce-111">비동기적으로 응답 플러시</span><span class="sxs-lookup"><span data-stu-id="7b3ce-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="7b3ce-112">*대기* 및 *작업*기반 비동기 모듈 및 처리기 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="7b3ce-113">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="7b3ce-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="7b3ce-114">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="7b3ce-115">새로운 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="7b3ce-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="7b3ce-116">지연된("지연") 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7b3ce-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="7b3ce-117">검증되지 않은 요청에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="7b3ce-118">안티XSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7b3ce-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="7b3ce-119">웹 소켓 프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="7b3ce-120">번들 및 미니화</span><span class="sxs-lookup"><span data-stu-id="7b3ce-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="7b3ce-121">웹 호스팅을 위한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="7b3ce-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="7b3ce-122">주요 성능 요소</span><span class="sxs-lookup"><span data-stu-id="7b3ce-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="7b3ce-123">새로운 성능 기능에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="7b3ce-124">공통 어셈블리 공유</span><span class="sxs-lookup"><span data-stu-id="7b3ce-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="7b3ce-125">더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용</span><span class="sxs-lookup"><span data-stu-id="7b3ce-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="7b3ce-126">메모리에 최적화하기 위한 가비지 콜렉션 튜닝</span><span class="sxs-lookup"><span data-stu-id="7b3ce-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="7b3ce-127">웹 응용 프로그램에 대한 프리페칭</span><span class="sxs-lookup"><span data-stu-id="7b3ce-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="7b3ce-128">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="7b3ce-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="7b3ce-129">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="7b3ce-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="7b3ce-130">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7b3ce-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="7b3ce-131">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="7b3ce-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="7b3ce-132">가치 공급자</span><span class="sxs-lookup"><span data-stu-id="7b3ce-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="7b3ce-133">컨트롤의 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="7b3ce-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="7b3ce-134">HTML 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="7b3ce-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="7b3ce-135">눈에 거슬리지 않는 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7b3ce-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="7b3ce-136">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="7b3ce-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="7b3ce-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="7b3ce-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="7b3ce-138">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="7b3ce-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="7b3ce-139">비주얼 스튜디오 2012 릴리스 후보</span><span class="sxs-lookup"><span data-stu-id="7b3ce-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="7b3ce-140">비주얼 스튜디오 2010과 비주얼 스튜디오 2012 릴리스 후보 간의 프로젝트 공유(프로젝트 호환성)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="7b3ce-141">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="7b3ce-142">ASP.NET 라우팅을 위한 IIS 7의 기본 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="7b3ce-143">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="7b3ce-144">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="7b3ce-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="7b3ce-145">와이 아리아 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="7b3ce-146">새로운 HTML5 스니펫</span><span class="sxs-lookup"><span data-stu-id="7b3ce-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="7b3ce-147">사용자 제어로 추출</span><span class="sxs-lookup"><span data-stu-id="7b3ce-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="7b3ce-148">속성의 코드 너겟에 대한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7b3ce-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="7b3ce-149">개폐 태그의 이름을 바꿀 때 일치하는 태그의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="7b3ce-150">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="7b3ce-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="7b3ce-151">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="7b3ce-152">명령문 자동 축소 완료</span><span class="sxs-lookup"><span data-stu-id="7b3ce-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="7b3ce-153">자바 스크립트 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="7b3ce-154">코드 개요</span><span class="sxs-lookup"><span data-stu-id="7b3ce-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="7b3ce-155">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="7b3ce-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="7b3ce-156">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="7b3ce-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="7b3ce-157">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="7b3ce-158">돔 인텔리센스</span><span class="sxs-lookup"><span data-stu-id="7b3ce-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="7b3ce-159">VSDOC 서명 오버로드</span><span class="sxs-lookup"><span data-stu-id="7b3ce-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="7b3ce-160">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="7b3ce-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="7b3ce-161">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="7b3ce-162">명령문 자동 축소 완료</span><span class="sxs-lookup"><span data-stu-id="7b3ce-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="7b3ce-163">계층적 들여쓰기.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="7b3ce-164">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="7b3ce-165">공급업체 별 스키마(-moz-,-web킷)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="7b3ce-166">댓글 달기 및 댓글 달기 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="7b3ce-167">색 선택</span><span class="sxs-lookup"><span data-stu-id="7b3ce-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="7b3ce-168">조각</span><span class="sxs-lookup"><span data-stu-id="7b3ce-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="7b3ce-169">사용자 지정 지역</span><span class="sxs-lookup"><span data-stu-id="7b3ce-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="7b3ce-170">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="7b3ce-171">게시</span><span class="sxs-lookup"><span data-stu-id="7b3ce-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="7b3ce-172">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="7b3ce-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="7b3ce-173">사전 컴파일 및 병합ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7b3ce-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="7b3ce-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="7b3ce-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="7b3ce-175">고지 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="7b3ce-176">ASP.NET 코어 런타임 및 프레임워크</span><span class="sxs-lookup"><span data-stu-id="7b3ce-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="7b3ce-177">비동기적으로 HTTP 요청 및 응답 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="7b3ce-178">ASP.NET 4는 *HttpRequest.GetBufferlessInputStream* 메서드를 사용하여 HTTP 요청 엔터티를 스트림으로 읽는 기능을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="7b3ce-179">이 메서드는 요청 엔터티에 대한 스트리밍 액세스를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="7b3ce-180">그러나 요청 기간 동안 스레드를 묶는 동기적으로 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="7b3ce-181">ASP.NET 4.5는 HTTP 요청 엔터티에서 비동기적으로 스트림을 읽는 기능과 비동기적으로 플러시하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="7b3ce-182">ASP.NET 4.5는 또한 .aspx 페이지 처리기 및 ASP.NET MVC 컨트롤러와 같은 다운스트림 HTTP 처리기와의 보다 쉽게 통합할 수 있는 HTTP 요청 엔터티를 두 번 버퍼링할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="7b3ce-183">HttpRequest 처리 개선 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="7b3ce-184">*httpRequest.GetBufferlessInputStream에서* ASP.NET 4.5에 의해 반환 된 스트림 참조는 동기 및 비동기 읽기 메서드를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="7b3ce-185">*GetBufferlessInputStream에서* 반환된 *스트림* 개체는 이제 BeginRead 및 EndRead 메서드를 모두 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="7b3ce-186">비동기 *Stream* 메서드를 사용하면 요청 엔터티를 청크로 비동기적으로 읽을 수 있으며 ASP.NET 비동기 읽기 루프의 각 반복 간에 현재 스레드를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="7b3ce-187">ASP.NET 4.5 또한 버퍼링 된 방법으로 요청 엔터티를 읽기 위한 컴패니언 *메서드를*추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="7b3ce-188">이 새 오버로드는 *GetBufferlessInputStream처럼*작동하여 동기 및 비동기 읽기를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="7b3ce-189">그러나 *GetBufferedInputStream은* 엔터티 바이트를 ASP.NET 내부 버퍼로 복사하여 다운스트림 모듈과 처리기가 요청 엔터티에 계속 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="7b3ce-190">예를 들어 파이프라인의 일부 업스트림 코드가 *GetBufferedInputStream을*사용하여 요청 엔터티를 이미 읽은 경우에도 *HttpRequest.Form* 또는 *HttpRequest.Files*를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="7b3ce-191">이렇게 하면 요청(예: 대용량 파일 업로드를 데이터베이스에 스트리밍)에서 비동기 처리를 수행할 수 있지만 나중에 .aspx 페이지 및 MVC ASP.NET 컨트롤러를 계속 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="7b3ce-192">비동기적으로 응답 플러시</span><span class="sxs-lookup"><span data-stu-id="7b3ce-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="7b3ce-193">클라이언트가 멀리 떨어져 있거나 대역폭이 낮은 연결이 있는 경우 HTTP 클라이언트에 응답을 보내는 데 상당한 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="7b3ce-194">일반적으로 ASP.NET 응용 프로그램에서 만들 때 응답 바이트를 버퍼링합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="7b3ce-195">그런 다음 ASP.NET 요청 처리의 맨 끝에서 누적된 버퍼의 단일 송신 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="7b3ce-196">버퍼링된 응답이 큰 경우(예: 대용량 파일을 클라이언트로 스트리밍) *주기적으로 HttpResponse.Flush를* 호출하여 버퍼링된 출력을 클라이언트에 보내고 메모리 사용량을 제어해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="7b3ce-197">그러나 *Flush는* 동기 호출이므로 반복적으로 *플러시를* 호출하면 잠재적으로 장기 실행되는 요청 동안 스레드가 계속 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="7b3ce-198">ASP.NET 4.5는 HttpResponse 클래스의 *BeginFlush* 및 *EndFlush* 메서드를 사용하여 비동기적으로 플러시 수행에 대한 지원을 *추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="7b3ce-199">이러한 메서드를 사용하면 운영 체제 스레드를 연결하지 않고 클라이언트에 데이터를 점진적으로 보내는 비동기 모듈 및 비동기 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="7b3ce-200">*BeginFlush* 호출과 *EndFlush* 호출 사이에 ASP.NET 현재 스레드를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="7b3ce-201">이렇게 하면 장기 실행 HTTP 다운로드를 지원하기 위해 필요한 총 활성 스레드 수가 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="7b3ce-202">*대기* 및 *작업* 지원 - 기반 비동기 모듈 및 처리기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="7b3ce-203">.NET Framework 4는 *작업이라고*하는 비동기 프로그래밍 개념을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="7b3ce-204">작업은 *System.Threading.Task* 네임스페이스의 *작업* 유형 및 관련 유형으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="7b3ce-205">.NET Framework 4.5는 *작업* 개체 작업을 간단하게 만드는 컴파일러 향상 기능을 통해 이를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="7b3ce-206">.NET Framework 4.5에서 컴파일러는 *await* 및 *async라는*두 가지 새 키워드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="7b3ce-207">*await* 키워드는 코드 조각이 다른 코드 에서 비동기적으로 기다려야 한다는 것을 나타내는 구문적 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="7b3ce-208">*비동기* 키워드는 메서드를 작업 기반 비동기 메서드로 표시하는 데 사용할 수 있는 힌트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="7b3ce-209">*await*, *비동기*및 *작업* 개체의 조합을 사용하면 .NET 4.5에서 비동기 코드를 훨씬 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="7b3ce-210">ASP.NET 4.5는 새로운 컴파일러 향상 을 사용하여 비동기 HTTP 모듈 및 비동기 HTTP 처리기를 작성할 수 있는 새 API를 사용하여 이러한 단순화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="7b3ce-211">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="7b3ce-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="7b3ce-212">*Task* 개체를 반환하는 메서드 내에서 비동기 작업을 수행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="7b3ce-213">다음 코드 예제는 Microsoft 홈 페이지를 다운로드하기 위해 비동기 호출을 하는 비동기 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="7b3ce-214">메서드 시그니처에서 *비동기* 키워드를 사용하고 *다운로드StringTaskAsync에*대한 *대기* 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="7b3ce-215">.NET Framework는 다운로드가 완료될 때까지 기다리는 동안 호출 스택 해제를 자동으로 처리하고 다운로드가 완료된 후 호출 스택을 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="7b3ce-216">이제 비동기 ASP.NET HTTP 모듈에서 이 비동기 메서드를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="7b3ce-217">ASP.NET 4.5에는 ASP.NET HTTP 파이프라인에서 노출된 이전 비동기 프로그래밍 모델과 작업 기반 비동기 메서드를 통합하는 데 사용할 수 있는 도우미*메서드(EventHandlerTaskAsyncHelper)와*새 대리자*유형(TaskEventHandler)이*포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="7b3ce-218">이 예제에서는 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 이 예제</span><span class="sxs-lookup"><span data-stu-id="7b3ce-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="7b3ce-219">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="7b3ce-220">ASP.NET 비동기 처리기를 작성하는 기존의 방법은 *IHttpAsyncHandler* 인터페이스를 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="7b3ce-221">ASP.NET 4.5에서 파생할 수 있는 *HttpTaskAsyncHandler* 비동기 기본 형식을 도입하므로 비동기 처리기를 훨씬 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="7b3ce-222">*HttpTaskAsyncHandler* 형식은 추상적이며 *ProcessRequestAsync* 메서드를 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="7b3ce-223">내부적으로 ASP.NET *ProcessRequestAsync의* 반환 *서명(작업* 개체)을 ASP.NET 파이프라인에서 사용하는 이전 비동기 프로그래밍 모델과 통합하는 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="7b3ce-224">다음 예제에서는 비동기 HTTP 처리기 구현의 일부로 Task 및 *await를* 사용하는 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주시면 *됩니다.*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="7b3ce-225">새로운 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="7b3ce-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="7b3ce-226">기본적으로 ASP.NET 요청 유효성 검사를 수행하며 필드, 헤더, 쿠키 등에서 태그 또는 스크립트를 찾는 요청을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="7b3ce-227">검색된 경우 ASP.NET 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="7b3ce-228">이는 잠재적인 교차 사이트 스크립팅 공격에 대한 첫 번째 방어선 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="7b3ce-229">ASP.NET 4.5를 사용하면 유효성이 검사되지 않은 요청 데이터를 쉽게 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="7b3ce-230">ASP.NET 4.5는 또한 이전에 외부 라이브러리였던 인기있는 AntiXSS 라이브러리를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="7b3ce-231">개발자는 응용 프로그램에 대한 요청 유효성 검사를 선택적으로 해제할 수 있는 기능을 자주 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="7b3ce-232">예를 들어 응용 프로그램이 포럼 소프트웨어인 경우 사용자가 HTML 형식의 포럼 게시물및 주석을 제출하도록 허용하지만 요청 유효성 검사가 다른 모든 것을 검사하고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="7b3ce-233">ASP.NET 4.5에서는 지연된("지연") 요청 유효성 검사 및 유효성이 검사되지 않은 요청 데이터에 대한 액세스등 유효성이 검사되지 않은 입력으로 선택적으로 작업할 수 있는 두 가지 기능이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="7b3ce-234">지연된("지연") 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7b3ce-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="7b3ce-235">ASP.NET 4.5에서는 기본적으로 모든 요청 데이터가 요청 유효성 검사의 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="7b3ce-236">그러나 실제로 요청 데이터에 액세스할 때까지 요청 유효성 검사를 연기하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="7b3ce-237">(특정 데이터 시나리오에 대한 지연 로드와 같은 용어를 기반으로 지연 요청 유효성 검사라고도 합니다.) 다음 예제와 같이 *httpRUntime* 요소에서 *requestValidationMode* 특성을 4.5로 설정하여 Web.config 파일에서 지연된 유효성 검사를 사용하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="7b3ce-238">요청 유효성 검사 모드가 4.5로 설정된 경우 요청 유효성 검사는 특정 요청 값에 대해서만 트리거되며 코드가 해당 값에 액세스하는 경우에만 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="7b3ce-239">예를 들어 코드가 Request.Form["포럼\_게시물"]의 값을 얻는 경우 요청 유효성 검사는 양식 컬렉션의 해당 요소에 대해서만 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="7b3ce-240">*양식* 컬렉션의 다른 요소는 유효성이 검사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="7b3ce-241">이전 버전의 ASP.NET 컬렉션의 모든 요소에 액세스할 때 전체 요청 컬렉션에 대 한 요청 유효성 검사가 트리거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="7b3ce-242">새 동작을 사용하면 다른 응용 프로그램 구성 요소가 다른 부분에 대한 요청 유효성 검사를 트리거하지 않고도 다양한 요청 데이터를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="7b3ce-243">검증되지 않은 요청에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-243">Support for unvalidated requests</span></span>

<span data-ttu-id="7b3ce-244">지연된 요청 유효성 검사만으로는 요청 유효성 검사를 선택적으로 우회하는 문제를 해결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="7b3ce-245">Request.Form["포럼\_게시물"]에 대한 호출은 여전히 특정 요청 값에 대한 요청 유효성 검사를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="7b3ce-246">그러나 해당 필드에서 태그를 허용하려는 경우 유효성 검사를 트리거하지 않고 이 필드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="7b3ce-247">이를 위해 ASP.NET 4.5는 이제 요청 데이터에 대한 유효성이 검사되지 않은 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="7b3ce-248">ASP.NET 4.5는 *HttpRequest* 클래스에 새 *유효성이 검사되지 않은* 컬렉션 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="7b3ce-249">이 컬렉션은 *양식,* *쿼리 문자열,* *쿠키*및 *URL*과 같은 요청 데이터의 모든 공통 값에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="7b3ce-250">유효성이 검사되지 않은 요청 데이터를 읽을 수 있도록 포럼 예제를 사용하면 먼저 새 요청 유효성 검사 모드를 사용하도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="7b3ce-251">그런 다음 *HttpRequest.Unvalidated* 속성을 사용하여 유효성이 검사되지 않은 양식 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="7b3ce-252">보안 - *유효성이 검사되지 않은 요청 데이터를 주의하여 사용하십시오!*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="7b3ce-253">ASP.NET 4.5는 유효성이 검사되지 않은 요청 속성 및 컬렉션을 추가하여 매우 구체적인 유효성이 검사되지 않은 요청 데이터에 쉽게 액세스할 수 있도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="7b3ce-254">그러나 위험한 텍스트가 사용자에게 렌더링되지 않도록 원시 요청 데이터에 대한 사용자 지정 유효성 검사를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="7b3ce-255">안티XSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7b3ce-255">AntiXSS Library</span></span>

<span data-ttu-id="7b3ce-256">Microsoft AntiXSS 라이브러리의 인기로 인해 ASP.NET 4.5는 이제 해당 라이브러리의 버전 4.0의 핵심 인코딩 루틴을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="7b3ce-257">인코딩 루틴은 새로운 *System.Web.Security.AntiXss* 네임스페이스의 *AntiXssEncoder* 형식에 의해 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="7b3ce-258">*AntiXssEncoder* 형식을 사용 하 여 형식에 구현 되는 정적 인코딩 메서드를 호출 하 여 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="7b3ce-259">그러나 새 안티 XSS 루틴을 사용하는 가장 쉬운 방법은 기본적으로 *AntiXssEncoder* 클래스를 사용하도록 ASP.NET 응용 프로그램을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="7b3ce-260">이렇게 하려면 Web.config 파일에 다음 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="7b3ce-261">*인코더Type* 특성이 *AntiXssEncoder* 형식을 사용하도록 설정되면 ASP.NET 모든 출력 인코딩이 새 인코딩 루틴을 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="7b3ce-262">다음은 ASP.NET 4.5에 통합 된 외부 AntiXSS 라이브러리의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="7b3ce-263">*HtmlEncode,* *HtmlFormUrlEncode*및 *Html속성 Encode*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="7b3ce-264">*Xml속성 엔코드* 및 *XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="7b3ce-265">*UrlEncode* 및 *UrlPathEncode* (새)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="7b3ce-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="7b3ce-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="7b3ce-267">웹 소켓 프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="7b3ce-268">WebSockets 프로토콜은 HTTP를 통해 클라이언트와 서버 간에 안전한 실시간 양방향 통신을 설정하는 방법을 정의하는 표준 기반 네트워크 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="7b3ce-269">Microsoft는 프로토콜을 정의하는 데 도움을 주기 위해 IETF 및 W3C 표준 기관과 협력해 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="7b3ce-270">WebSockets 프로토콜은 브라우저뿐만 아니라 모든 클라이언트에서 지원되며 Microsoft는 클라이언트 및 모바일 운영 체제모두에 WebSockets 프로토콜을 지원하는 상당한 리소스를 투자합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="7b3ce-271">WebSockets 프로토콜을 사용하면 클라이언트와 서버 간에 장기 실행 데이터 전송을 훨씬 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="7b3ce-272">예를 들어 클라이언트와 서버 간에 진정한 장기 실행 연결을 설정할 수 있으므로 채팅 응용 프로그램을 작성하는 것이 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="7b3ce-273">소켓의 동작을 시뮬레이션하기 위해 정기적인 폴링 또는 HTTP 긴 폴링과 같은 해결 방법을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="7b3ce-274">ASP.NET 4.5 및 IIS 8에는 하위 수준의 WebSockets 지원이 포함되어 있으므로 ASP.NET 개발자가 WebSockets 개체에서 문자열 및 이진 데이터를 비동기적으로 읽고 쓰는 데 관리되는 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="7b3ce-275">ASP.NET 4.5의 경우 WebSockets 프로토콜작업에 대한 형식을 포함하는 새로운 *System.Web.WebSockets* 네임스페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="7b3ce-276">브라우저 클라이언트는 다음 예제와 같이 ASP.NET 응용 프로그램의 URL을 가리키는 DOM *WebSocket* 개체를 만들어 WebSockets 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="7b3ce-277">모든 종류의 모듈 또는 처리기를 사용하여 ASP.NET WebSockets 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="7b3ce-278">이전 예제에서는 .ashx 파일이 처리기를 만드는 빠른 방법이기 때문에 .ashx 파일이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="7b3ce-279">WebSockets 프로토콜에 따라 ASP.NET 응용 프로그램은 HTTP GET 요청에서 WebSockets 요청으로 요청을 업그레이드해야 한다는 표시로 클라이언트의 WebSockets 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="7b3ce-280">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="7b3ce-281">*AcceptWebSocketRequest* 메서드는 ASP.NET 현재 HTTP 요청을 해제 한 다음 컨트롤을 함수 대리자로 전송하기 때문에 함수 대리자를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="7b3ce-282">개념적으로 이 방법은 백그라운드 작업이 수행되는 스레드 시작 대리자를 정의하는 *System.Threading.Thread를*사용하는 방법과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="7b3ce-283">ASP.NET 클라이언트가 WebSockets 핸드셰이크를 성공적으로 완료한 후 ASP.NET 대리인을 호출하고 WebSockets 응용 프로그램이 실행시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="7b3ce-284">다음 코드 예제에서는 ASP.NET 기본 제공 WebSockets 지원을 사용하는 간단한 에코 응용 프로그램을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="7b3ce-285">*await* 키워드 및 비동기 작업 기반 작업에 대한 .NET 4.5의 지원은 WebSockets 응용 프로그램을 작성하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="7b3ce-286">코드 예제에서는 WebSockets 요청이 ASP.NET 내에서 완전히 비동기적으로 실행되는 것을 보여 주어집니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="7b3ce-287">응용 프로그램은 await 소켓을 호출하여 클라이언트에서 메시지가 전송될 때까지 비동기적으로 *대기합니다. 수신Async*.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="7b3ce-288">마찬가지로 await 소켓을 호출하여 클라이언트에 비동기 메시지를 보낼 수 *있습니다. 센드애싱크*.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="7b3ce-289">브라우저에서 응용 프로그램은 *메시지 온 메시지* 기능을 통해 WebSockets 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="7b3ce-290">브라우저에서 메시지를 보내려면 이 예제와 같이 *WebSocket* DOM 형식의 *send* 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="7b3ce-291">나중에 WebSockets 응용 프로그램에 대해 이 릴리스에 필요한 하위 수준 코딩 중 일부를 추상화하는 이 기능에 대한 업데이트를 릴리스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="7b3ce-292">묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="7b3ce-292">Bundling and Minification</span></span>

<span data-ttu-id="7b3ce-293">번들을 사용하면 개별 JavaScript 및 CSS 파일을 단일 파일처럼 취급할 수 있는 번들로 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="7b3ce-294">축소는 필요하지 않은 공백 및 기타 문자를 제거하여 JavaScript 및 CSS 파일을 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="7b3ce-295">이러한 기능은 웹 양식, ASP.NET MVC 및 웹 페이지에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="7b3ce-296">번들은 번들 클래스 또는 자식 클래스 중 하나인 스크립트번들 및 스타일번들을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="7b3ce-297">번들의 인스턴스를 구성한 후, 번들은 단순히 전역 번들컬렉션 인스턴스에 추가하기만 하면 들어오는 요청에 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="7b3ce-298">기본 템플릿에서 번들 구성은 번들구성 파일에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="7b3ce-299">이 기본 구성은 템플릿에서 사용하는 모든 핵심 스크립트 및 css 파일에 대한 번들을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="7b3ce-300">번들은 몇 가지 가능한 도우미 방법 중 하나를 사용하여 뷰 내에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="7b3ce-301">디버그 대 릴리스 모드에서 번들에 대해 다른 태그 렌더링을 지원하기 위해 ScriptBundle 및 StyleBundle 클래스에는 도우미 메서드인 Render가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="7b3ce-302">디버그 모드에서 렌더는 번들의 각 리소스에 대한 태그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="7b3ce-303">릴리스 모드에서 Render는 전체 번들에 대해 단일 태그 요소를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="7b3ce-304">아래와 같이 web.config에서 컴파일 요소의 디버그 특성을 수정하여 디버그 모드와 릴리스 모드 간의 전환작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="7b3ce-305">또한 번들Table.Enable최적화 속성을 통해 최적화를 활성화하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="7b3ce-306">파일이 번들로 묶이면 먼저 사전순으로 정렬됩니다(솔루션 **탐색기에서**표시되는 방식).</span><span class="sxs-lookup"><span data-stu-id="7b3ce-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="7b3ce-307">그런 다음 알려진 라이브러리와 사용자 지정 확장(예: jQuery, MooTools 및 Dojo)이 먼저 로드되도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="7b3ce-308">예를 들어, 위에 표시된 스크립트 폴더의 번들의 최종 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="7b3ce-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="7b3ce-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="7b3ce-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="7b3ce-310">jquery-ui.js</span></span>
3. <span data-ttu-id="7b3ce-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="7b3ce-311">jquery.tools.js</span></span>
4. <span data-ttu-id="7b3ce-312">a.js</span><span class="sxs-lookup"><span data-stu-id="7b3ce-312">a.js</span></span>

<span data-ttu-id="7b3ce-313">CSS 파일은 또한 사전순으로 정렬된 다음 reset.css 및 normalize.css가 다른 파일보다 앞서 오게 되도록 재구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="7b3ce-314">위에 표시된 스타일 폴더의 번들의 최종 정렬은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="7b3ce-315">리셋.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-315">reset.css</span></span>
2. <span data-ttu-id="7b3ce-316">콘텐츠.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-316">content.css</span></span>
3. <span data-ttu-id="7b3ce-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-317">forms.css</span></span>
4. <span data-ttu-id="7b3ce-318">글로벌.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-318">globals.css</span></span>
5. <span data-ttu-id="7b3ce-319">메뉴.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-319">menu.css</span></span>
6. <span data-ttu-id="7b3ce-320">스타일.css</span><span class="sxs-lookup"><span data-stu-id="7b3ce-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="7b3ce-321">웹 호스팅을 위한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="7b3ce-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="7b3ce-322">.NET Framework 4.5 및 Windows 8에는 웹 서버 워크로드에 대한 성능이 크게 향상되는 데 도움이 되는 기능이 소개되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="7b3ce-323">여기에는 감소(최대 35%) 시작 시간 및 ASP.NET 사용하는 웹 호스팅 사이트의 메모리 공간 모두에서</span><span class="sxs-lookup"><span data-stu-id="7b3ce-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="7b3ce-324">주요 성능 요소</span><span class="sxs-lookup"><span data-stu-id="7b3ce-324">Key performance factors</span></span>

<span data-ttu-id="7b3ce-325">이상적으로는 모든 웹 사이트가 언제든지 다음 요청에 대한 빠른 응답을 보장하기 위해 활성화되고 메모리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="7b3ce-326">사이트 응답성에 영향을 줄 수 있는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="7b3ce-327">앱 풀이 재활용된 후 사이트를 다시 시작하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="7b3ce-328">사이트 어셈블리가 더 이상 메모리에 없을 때 사이트에 대한 웹 서버 프로세스를 시작하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="7b3ce-329">플랫폼 어셈블리는 다른 사이트에서 사용되므로 여전히 메모리에 있습니다. 이러한 상황을 "콜드 사이트, 웜 프레임워크 시작" 또는 "콜드 사이트 시작"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="7b3ce-330">사이트가 차지하는 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-330">How much memory the site occupies.</span></span> <span data-ttu-id="7b3ce-331">이에 대한 용어는 "사이트당 메모리 사용량" 또는 "공유되지 않은 작업 집합"입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="7b3ce-332">새로운 성능 향상은 이 두 가지 요인모두에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="7b3ce-333">새로운 성능 기능에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="7b3ce-334">새 기능에 대한 요구 사항은 다음 범주로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="7b3ce-335">.NET 프레임워크 4에서 실행되는 개선 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="7b3ce-336">.NET Framework 4.5가 필요하지만 모든 버전의 Windows에서 실행할 수 있는 개선 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="7b3ce-337">Windows 8에서 실행되는 .NET Framework 4.5에서만 사용할 수 있는 향상된 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="7b3ce-338">활성화할 수 있는 각 개선 수준에 따라 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="7b3ce-339">.NET Framework 4.5 개선 사항 중 일부는 다른 시나리오에도 적용되는 광범위한 성능 기능을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="7b3ce-340">공통 어셈블리 공유</span><span class="sxs-lookup"><span data-stu-id="7b3ce-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="7b3ce-341">**요구 사항**: .NET 프레임 워크 4 및 비주얼 스튜디오 11 개발자 미리보기 SDK</span><span class="sxs-lookup"><span data-stu-id="7b3ce-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="7b3ce-342">서버의 다른 사이트는 종종 동일한 도우미 어셈블리(예: 시작 키트 또는 샘플 응용 프로그램의 어셈블리)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="7b3ce-343">각 사이트에는 Bin 디렉터리에서 이러한 어셈블리의 고유한 복사본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="7b3ce-344">어셈블리의 개체 코드는 동일하지만 물리적으로 분리된 어셈블리이므로 콜드 사이트 시작 중에 각 어셈블리를 별도로 읽고 메모리에 별도로 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="7b3ce-345">새로운 인턴닝 기능은 이러한 비효율성을 해결하고 RAM 요구 사항과 로드 시간을 모두 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="7b3ce-346">인턴링을 사용하면 Windows에서 파일 시스템에 각 어셈블리의 단일 복사본을 유지할 수 있으며 사이트 Bin 폴더의 개별 어셈블리는 단일 복사본에 대한 기호 링크로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="7b3ce-347">개별 사이트에 고유한 버전의 어셈블리가 필요한 경우 기호 링크는 새 버전의 어셈블리로 대체되고 해당 사이트만 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="7b3ce-348">기호 링크를 사용하여 어셈블리를 공유하려면\_aspnet intern.exe라는 새 도구가 필요하므로 인턴어 의 저장소를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="7b3ce-349">그것은 비주얼 스튜디오의 일부로 제공됩니다 11 개발자 미리보기 SDK.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="7b3ce-350">그러나 최신 [업데이트를](https://support.microsoft.com/kb/2468871)설치했다고 가정할 때 .NET Framework 4만 설치된 시스템에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="7b3ce-351">자격을 갖춘 모든 어셈블리가 인턴으로 등록되었는지\_확인하려면 aspnet intern.exe를 주기적으로 실행합니다(예: 예약된 작업으로 일주일에 한 번).</span><span class="sxs-lookup"><span data-stu-id="7b3ce-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="7b3ce-352">일반적인 용도는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="7b3ce-353">모든 옵션을 보려면 인수 없이 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="7b3ce-354">더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용</span><span class="sxs-lookup"><span data-stu-id="7b3ce-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="7b3ce-355">**요구 사항**: .NET 프레임 워크 4.5</span><span class="sxs-lookup"><span data-stu-id="7b3ce-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="7b3ce-356">콜드 사이트 시작의 경우 어셈블리를 디스크에서 읽어야 할 뿐만 아니라 사이트를 JIT 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="7b3ce-357">복잡한 사이트의 경우 이로 인해 상당한 지연이 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="7b3ce-358">.NET Framework 4.5의 새로운 범용 기술은 사용 가능한 프로세서 코어 에 JIT 컴파일을 분산하여 이러한 지연을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="7b3ce-359">그것은 사이트의 이전 출시 중에 수집 된 정보를 사용하여 가능한 한 빨리이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="7b3ce-360">[System.Runtime.Profile 최적화.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드에 의해 구현 된이 기능.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="7b3ce-361">여러 코어를 사용하는 JIT 컴파일은 ASP.NET 기본적으로 활성화되므로 이 기능을 활용하기 위해 아무 작업도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="7b3ce-362">이 기능을 사용하지 않도록 설정하려면 Web.config 파일에서 다음 설정을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="7b3ce-363">메모리에 최적화하기 위한 가비지 콜렉션 튜닝</span><span class="sxs-lookup"><span data-stu-id="7b3ce-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="7b3ce-364">**요구 사항**: .NET 프레임 워크 4.5</span><span class="sxs-lookup"><span data-stu-id="7b3ce-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="7b3ce-365">사이트가 실행되면 GC(가비지 수집기) 힙을 사용하는 것이 메모리 소비에 중요한 요소가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="7b3ce-366">모든 가비지 수집기와 마찬가지로 .NET Framework GC는 CPU 시간(컬렉션의 빈도 및 중요성)과 메모리 소비(새 개체, 해제된 개체 또는 사용 가능한 개체에 사용되는 추가 공간) 간의 장단점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="7b3ce-367">이전 릴리스의 경우 적절한 균형을 이루도록 GC를 구성하는 방법에 대한 지침을 제공했습니다(예: [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)참조).</span><span class="sxs-lookup"><span data-stu-id="7b3ce-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="7b3ce-368">.NET Framework 4.5의 경우 여러 독립 실행형 설정 대신 이전에 권장하는 모든 GC 설정을 사용할 수 있는 워크로드 정의 구성 설정을 사용할 수 있을 뿐만 아니라 사이트별 작업 집합에 대한 추가 성능을 제공하는 새 튜닝을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="7b3ce-369">GC 메모리 튜닝을 사용하려면 다음 설정을 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="7b3ce-370">aspnet.config에 대한 변경에 대한 이전 지침에 익숙한 경우 이 설정이 이전 설정을 대체합니다(예: gcServer, gcConcurrent 등을 설정할 필요가 없습니다). 이전 설정을 제거할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="7b3ce-371">웹 응용 프로그램에 대한 프리페칭</span><span class="sxs-lookup"><span data-stu-id="7b3ce-371">Prefetching for web applications</span></span>

<span data-ttu-id="7b3ce-372">**요구 사항**: .NET 프레임 워크 4.5 윈도우 8에서 실행</span><span class="sxs-lookup"><span data-stu-id="7b3ce-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="7b3ce-373">여러 릴리스의 경우 Windows에는 응용 프로그램 시작의 디스크 읽기 비용을 줄이는 [프리페처라는](http://en.wikipedia.org/wiki/Prefetcher) 기술이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="7b3ce-374">콜드 시작은 주로 클라이언트 응용 프로그램의 문제이므로 이 기술은 서버에 필수적인 구성 요소만 포함하는 Windows Server에 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="7b3ce-375">이제 개별 웹 사이트의 출시를 최적화할 수 있는 최신 버전의 Windows Server에서 프리페칭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="7b3ce-376">Windows 서버의 경우 프리페처는 기본적으로 활성화되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="7b3ce-377">고밀도 웹 호스팅을 위해 프리페처를 활성화하고 구성하려면 명령줄에서 다음 명령 집합을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="7b3ce-378">그런 다음 prefetcher를 ASP.NET 응용 프로그램과 통합하려면 Web.config 파일에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="7b3ce-379">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="7b3ce-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="7b3ce-380">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="7b3ce-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="7b3ce-381">ASP.NET 4.5에서 Web Forms에는 데이터 작업에 대한 몇 가지 개선 사항이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="7b3ce-382">첫 번째 개선 사항은 강력하게 입력된 데이터 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="7b3ce-383">이전 버전의 ASP.NET Web Forms 컨트롤의 경우 *Eval* 및 데이터 바인딩 식을 사용하여 데이터 바인딩값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="7b3ce-384">양방향 데이터 바인딩의 경우 *바인딩을*사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="7b3ce-385">런타임에 이러한 호출은 리플렉션을 사용하여 지정된 멤버의 값을 읽은 다음 결과를 태그에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="7b3ce-386">이 방법을 사용하면 모양이 없는 임의의 데이터에 대해 데이터를 쉽게 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="7b3ce-387">그러나 이와 같은 데이터 바인딩 식은 멤버 이름에 대한 IntelliSense, 탐색(예: 정의로 이동) 또는 이러한 이름을 확인하는 컴파일 타임 검사와 같은 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="7b3ce-388">이 문제를 해결하기 위해 ASP.NET 4.5는 컨트롤이 바인딩된 데이터의 데이터 형식을 선언하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="7b3ce-389">새 *ItemType* 속성을 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="7b3ce-390">이 속성을 설정하면 데이터 바인딩 식의 범위에서 두 개의 새 형식변수를 사용할 수 있습니다: *Item* 및 *BindItem*.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="7b3ce-391">변수는 강력하게 입력되므로 Visual Studio 개발 환경의 모든 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="7b3ce-392">양방향 데이터 바인딩 식의 경우 *BindItem* 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="7b3ce-393">데이터 바인딩을 지원하는 ASP.NET Web Forms 프레임워크의 대부분의 컨트롤이 *ItemType* 속성을 지원하도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="7b3ce-394">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7b3ce-394">Model Binding</span></span>

<span data-ttu-id="7b3ce-395">모델 바인딩은 ASP.NET Web Forms 컨트롤에서 데이터 바인딩을 확장하여 코드 중심 데이터 액세스와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="7b3ce-396">*ObjectDataSource* 컨트롤과 ASP.NET MVC의 모델 바인딩의 개념을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="7b3ce-397">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="7b3ce-397">Selecting data</span></span>

<span data-ttu-id="7b3ce-398">모델 바인딩을 사용하여 데이터를 선택하도록 데이터 컨트롤을 구성하려면 컨트롤의 *SelectMethod* 속성을 페이지 코드의 메서드 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="7b3ce-399">데이터 컨트롤은 페이지 수명 주기에서 적절한 시간에 메서드를 호출하고 반환된 데이터를 자동으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="7b3ce-400">*DataBind* 메서드를 명시적으로 호출할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="7b3ce-401">다음 예제에서 *GridView* 컨트롤은 *Get범주:* 라는 메서드를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="7b3ce-402">페이지 코드에서 *GetCategories* 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="7b3ce-403">간단한 선택 작업의 경우 메서드는 매개 변수가 필요하지 않으며 *IEnumerable* 또는 *IQueryable* 개체를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="7b3ce-404">새 *ItemType* 속성이 설정된 경우(앞에서 설명한 대로 강력한 형식의 데이터 바인딩 식에서 설명한 대로 강력한 [형식의 데이터](#_Toc318097386) 바인딩 식을 사용 함) 이러한 인터페이스의 일반 버전(IEnumerable \*&lt;T&gt; \* 또는 *IQueryable&lt;T)&gt;* 및 *ItemType* 속성의 형식과 일치하는 *T* 매개 변수(예: *&lt;IQueryable&gt;범주)가*반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="7b3ce-405">다음 예제에서는 *GetCategories* 메서드에 대 한 코드를 보여 주다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="7b3ce-406">이 예제에서는 Northwind 샘플 데이터베이스와 함께 엔터티 프레임워크 코드 첫 번째 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="7b3ce-407">코드는 쿼리가 *Include* 메서드를 통해 각 범주에 대한 관련 제품의 세부 정보를 반환하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="7b3ce-408">이렇게 하면 태그의 *TemplateField* 요소가 [n+1 선택을](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)요구하지 않고 각 범주의 제품 수를 표시합니다.)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="7b3ce-409">페이지가 실행되면 *GridView* 컨트롤은 *GetCategories* 메서드를 자동으로 호출하고 구성된 필드를 사용하여 반환된 데이터를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="7b3ce-410">select 메서드는 *IQueryable* 개체를 반환하므로 *GridView* 컨트롤은 쿼리를 실행하기 전에 쿼리를 추가로 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="7b3ce-411">예를 들어 *GridView* 컨트롤은 실행되기 전에 반환된 *IQueryable* 개체를 정렬하고 페이징하기 위한 쿼리 식을 추가하여 기본 LINQ 공급자에 의해 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="7b3ce-412">이 경우 Entity Framework는 이러한 작업이 데이터베이스에서 수행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="7b3ce-413">다음 예제에서는 정렬 및 페이징을 허용하도록 수정된 *GridView* 컨트롤을 보여 주며 다음과 같은 예제를 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="7b3ce-414">이제 페이지가 실행되면 컨트롤은 데이터의 현재 페이지만 표시되고 선택한 열에서 정렬되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="7b3ce-415">반환된 데이터를 필터링하려면 매개 변수를 select 메서드에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="7b3ce-416">이러한 매개 변수는 런타임에 모델 바인딩에 의해 채워지며 데이터를 반환하기 전에 쿼리를 변경하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="7b3ce-417">예를 들어 쿼리 문자열에 키워드를 입력하여 사용자가 제품을 필터링하도록 할 것이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="7b3ce-418">메서드에 매개 변수를 추가하고 매개 변수 값을 사용하도록 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="7b3ce-419">이 코드에는 *키워드에* 대한 값이 제공된 다음 쿼리 결과를 반환하는 경우 *Where* 식이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="7b3ce-420">가치 공급자</span><span class="sxs-lookup"><span data-stu-id="7b3ce-420">Value providers</span></span>

<span data-ttu-id="7b3ce-421">이전 예제에서는 *키워드* 매개 변수의 값이 어디에서 왔는지에 대해 구체적으로 언급하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="7b3ce-422">이 정보를 나타내려면 매개 변수 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="7b3ce-423">이 예제에서는 *System.Web.ModelBinding* 네임스페이스에 있는 *QueryStringAttribute* 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="7b3ce-424">이렇게 하면 모델 바인딩에서 쿼리 문자열에서 런타임에 *키워드* 매개 변수에 값을 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="7b3ce-425">형식 변환을 수행해야 할 수 있지만 이 경우에는 변환하지 않습니다. 값을 제공할 수 없고 형식이 null이 아닌 경우 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="7b3ce-426">이러한 메서드의 값 소스를 값 공급자라고 하며 사용할 값 공급자를 나타내는 매개 변수 특성을 값 공급자 특성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="7b3ce-427">Web Forms에는 쿼리 문자열, 쿠키, 양식 값, 컨트롤, 보기 상태, 세션 상태 및 프로필 속성과 같은 Web Forms 응용 프로그램의 모든 일반적인 사용자 입력 소스에 대한 값 공급자 및 해당 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="7b3ce-428">사용자 지정 값 공급자를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-428">You can also write custom value providers.</span></span>

<span data-ttu-id="7b3ce-429">기본적으로 매개 변수 이름은 값 공급자 컬렉션에서 값을 찾기 위한 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="7b3ce-430">이 예제에서 코드는 키워드라는 쿼리 문자열 값(예: ~/default.aspx?keyword=chef)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="7b3ce-431">사용자 지정 키를 매개 변수 특성에 인수로 전달하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="7b3ce-432">예를 들어 q라는 쿼리 문자열 변수의 값을 사용하려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="7b3ce-433">이 메서드가 페이지 코드에 있는 경우 사용자는 쿼리 문자열을 사용하여 키워드를 전달하여 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="7b3ce-434">모델 바인딩은 값 읽기, null 값 확인, 적절한 유형으로 변환 시도, 변환이 성공했는지 확인, 마지막으로 쿼리의 값을 사용하여 직접 코딩해야 하는 많은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="7b3ce-435">모델 바인딩으로 인해 코드가 훨씬 줄어들고 응용 프로그램 전체에서 기능을 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="7b3ce-436">컨트롤의 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="7b3ce-436">Filtering by values from a control</span></span>

<span data-ttu-id="7b3ce-437">사용자가 드롭다운 목록에서 필터 값을 선택할 수 있도록 예제를 확장한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="7b3ce-438">태그에 다음 드롭다운 목록을 추가하고 *SelectMethod* 속성을 사용하여 다른 메서드에서 데이터를 얻도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="7b3ce-439">일반적으로 일치하는 제품이 없는 경우 컨트롤에 메시지가 표시되도록 *GridView* 컨트롤에 *EmptyDataTemplate* 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="7b3ce-440">페이지 코드에서 드롭다운 목록에 대한 새 선택 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="7b3ce-441">마지막으로 *GetProducts* select 메서드를 업데이트하여 드롭다운 목록에서 선택한 범주의 ID를 포함하는 새 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="7b3ce-442">이제 페이지가 실행되면 사용자는 드롭다운 목록에서 범주를 선택할 수 있으며 *GridView* 컨트롤이 자동으로 다시 바인딩되어 필터링된 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="7b3ce-443">이는 모델 바인딩이 선택 메서드에 대한 매개 변수 값을 추적하고 포스트백 후 매개 변수 값이 변경되었는지 여부를 감지하기 때문에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="7b3ce-444">이 경우 모델 바인딩은 연결된 데이터 컨트롤을 강제로 데이터에 다시 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="7b3ce-445">HTML 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="7b3ce-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="7b3ce-446">이제 데이터 바인딩 식의 결과를 HTML로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="7b3ce-447">콜론 추가(:) 데이터 바인딩 식을 &lt;표시하는 %# 접두사 끝에 는</span><span class="sxs-lookup"><span data-stu-id="7b3ce-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="7b3ce-448">눈에 거슬리지 않는 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7b3ce-448">Unobtrusive Validation</span></span>

<span data-ttu-id="7b3ce-449">이제 클라이언트 측 유효성 검사 논리에 눈에 거슬리지 않는 JavaScript를 사용하도록 기본 제공 유효성 검사기 컨트롤을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="7b3ce-450">이렇게 하면 페이지 태그에서 인라인으로 렌더링되는 JavaScript의 양이 크게 줄어들고 전체 페이지 크기가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="7b3ce-451">다음과 같은 방법으로 유효성 검사기 컨트롤에 대한 눈에 거슬리지 않는 JavaScript를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="7b3ce-452">Web.config 파일의 \* &lt;appSettings&gt; \* 요소에 다음 설정을 추가하여 전역적으로:</span><span class="sxs-lookup"><span data-stu-id="7b3ce-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="7b3ce-453">전역적으로 정적 *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* 속성을 *눈에 띄지 않는 유효성 검사Mode.WebForms(일반적으로* Global.asax 파일의 *응용 프로그램\_시작* 메서드)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="7b3ce-454">페이지 클래스의 새 눈에 *띄지 않는 유효성 검사 유효성 검사 모드* 속성을 눈에 띄지 않는 유효성 검사 유효성 검사 *모드.WebForms로*설정 하여 개별적으로 *페이지에* 대 한 .</span><span class="sxs-lookup"><span data-stu-id="7b3ce-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="7b3ce-455">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="7b3ce-455">HTML5 Updates</span></span>

<span data-ttu-id="7b3ce-456">HTML5의 새로운 기능을 활용하기 위해 Web Forms 서버 컨트롤이 일부 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="7b3ce-457">*TextBox* 컨트롤의 *TextMode* 속성은 *전자 메일,* *datetime*등과 같은 새 HTML5 입력 형식을 지원하도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="7b3ce-458">*FileUpload* 컨트롤은 이제 이 HTML5 기능을 지원하는 브라우저의 여러 파일 업로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="7b3ce-459">유효성 검사기 컨트롤은 이제 HTML5 입력 요소의 유효성 을 검사하는 것을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="7b3ce-460">URL을 나타내는 특성이 있는 새 HTML5 요소는 이제 runat="서버"를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="7b3ce-461">따라서 ~ 연산자처럼 URL 경로에서 ASP.NET 규칙을 사용하여 응용 프로그램 루트를 나타낼 &lt;수 있습니다(예: 비디오 runat="서버" src="~/myVideo.wmv" /&gt;).</span><span class="sxs-lookup"><span data-stu-id="7b3ce-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="7b3ce-462">*UpdatePanel* 컨트롤은 HTML5 입력 필드 게시를 지원하도록 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="7b3ce-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="7b3ce-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="7b3ce-464">ASP.NET MVC 4 베타는 이제 비주얼 스튜디오 11 베타에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="7b3ce-465">ASP.NET MVC는 MVC(모델 뷰 컨트롤러) 패턴을 활용하여 테스트가 용이하고 유지 관리 가능한 웹 응용 프로그램을 개발하기 위한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="7b3ce-466">ASP.NET MVC 4를 사용하면 모바일 웹용 응용 프로그램을 쉽게 빌드할 수 있으며 모든 장치에 연결할 수 있는 HTTP 서비스를 빌드하는 데 도움이 되는 ASP.NET 웹 API가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="7b3ce-467">자세한 내용은 ASP.NET [MVC 4 릴리스 정보를](mvc4-release-notes.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="7b3ce-468">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="7b3ce-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="7b3ce-469">새로운 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-469">New features include the following:</span></span>

- <span data-ttu-id="7b3ce-470">새 사이트 템플릿 및 업데이트된 사이트 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-470">New and updated site templates.</span></span>
- <span data-ttu-id="7b3ce-471">*유효성 검사* 도우미를 사용하여 서버 측 및 클라이언트 측 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="7b3ce-472">자산 관리자를 사용하여 스크립트를 등록하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="7b3ce-473">OAuth 및 OpenID를 사용하여 페이스 북과 다른 사이트에서 로그인을 활성화.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="7b3ce-474">*지도* 도우미를 사용하여 맵 추가</span><span class="sxs-lookup"><span data-stu-id="7b3ce-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="7b3ce-475">웹 페이지 응용 프로그램을 나란히 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="7b3ce-476">모바일 장치의 페이지 렌더링.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="7b3ce-477">이러한 기능 및 전체 페이지 코드 예제에 대한 자세한 내용은 [웹 페이지 2 베타의 주요 기능을](https://go.microsoft.com/fwlink/?LinkID=227824)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="7b3ce-478">비주얼 웹 개발자 11 베타</span><span class="sxs-lookup"><span data-stu-id="7b3ce-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="7b3ce-479">이 섹션에서는 Visual Web Developer 11 베타 및 Visual Studio 2012 릴리스 후보의 웹 개발 개선 사항에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="7b3ce-480">비주얼 스튜디오 2010과 비주얼 스튜디오 2012 릴리스 후보 간의 프로젝트 공유(프로젝트 호환성)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="7b3ce-481">Visual Studio 2012 릴리스 후보까지, 비주얼 스튜디오의 최신 버전에서 기존 프로젝트를 열고 변환 마법사를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="7b3ce-482">이로 인해 프로젝트의 콘텐츠(자산)를 이전 버전과 호환되지 않는 새 형식으로 업그레이드해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="7b3ce-483">따라서 변환 후 이전 버전의 Visual Studio에서 프로젝트를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="7b3ce-484">많은 고객이 이것이 올바른 접근 방식이 아니라고 말했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="7b3ce-485">Visual Studio 11 베타에서는 이제 Visual Studio 2010 SP1을 통해 프로젝트 및 솔루션 공유를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="7b3ce-486">즉, Visual Studio 2012 릴리스 후보에서 2010 프로젝트를 열더라도 Visual Studio 2010 SP1에서 프로젝트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3ce-487">몇 가지 유형의 프로젝트는 Visual Studio 2010 SP1과 Visual Studio 2012 릴리스 후보 간에 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="7b3ce-488">여기에는 일부 이전 프로젝트(예: ASP.NET MVC 2 프로젝트) 또는 특수 목적(예: 설치 프로젝트)을 위한 프로젝트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="7b3ce-489">Visual Studio 11 베타에서 처음으로 Visual Studio 2010 SP1 웹 프로젝트를 열면 다음 속성이 프로젝트 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="7b3ce-490">파일 업그레이드 플래그</span><span class="sxs-lookup"><span data-stu-id="7b3ce-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="7b3ce-491">업그레이드백업위치</span><span class="sxs-lookup"><span data-stu-id="7b3ce-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="7b3ce-492">올드툴스버전</span><span class="sxs-lookup"><span data-stu-id="7b3ce-492">OldToolsVersion</span></span>
- <span data-ttu-id="7b3ce-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="7b3ce-493">VisualStudioVersion</span></span>
- <span data-ttu-id="7b3ce-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="7b3ce-494">VSToolsPath</span></span>

<span data-ttu-id="7b3ce-495">파일 업그레이드플래그, 업그레이드백업위치 및 OldToolsVersion은 프로젝트 파일을 업그레이드하는 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="7b3ce-496">Visual Studio 2010에서 프로젝트 작업에 아무런 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="7b3ce-497">VisualStudioVersion은 MSBuild 4.5에서 현재 프로젝트에 대한 Visual Studio 버전을 나타내는 새 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="7b3ce-498">이 속성은 MSBuild 4.0(Visual Studio 2010 SP1에서 사용하는 MSBuild 버전)에 존재하지 않았기 때문에 프로젝트 파일에 기본값을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="7b3ce-499">VSToolsPath 속성은 MSBuildExtensionsPath32 설정으로 표시되는 경로에서 가져올 올바른 .targets 파일을 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="7b3ce-500">가져오기 요소와 관련된 몇 가지 변경 내용도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="7b3ce-501">두 버전의 Visual Studio 간의 호환성을 지원하려면 이러한 변경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3ce-502">두 대의 서로 다른 컴퓨터에서 Visual Studio 2010 SP1과 Visual Studio 11 Beta 간에 프로젝트를 공유하는\_경우 프로젝트에 앱 데이터 폴더에 로컬 데이터베이스가 포함되어 있는 경우 데이터베이스에서 사용하는 SQL Server 버전이 두 컴퓨터에 설치되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="7b3ce-503">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="7b3ce-504">Visual Studio 2012 릴리스 후보의 웹 사이트 템플릿을 사용하여 만든 사이트의 기본 *Web.config* 파일에 대해 다음과 같은 변경 사항이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="7b3ce-505">`<httpRuntime>` 요소에서 `encoderType` 특성은 이제 ASP.NET 추가된 AntiXSS 형식을 사용하도록 기본적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="7b3ce-506">자세한 내용은 [AntiXSS 라이브러리를](#_Toc318097382)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="7b3ce-507">또한 `<httpRuntime>` 요소에서 `requestValidationMode` 특성은 "4.5"로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="7b3ce-508">즉, 기본적으로 요청 유효성 검사는 지연된("지연") 유효성 검사를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="7b3ce-509">자세한 내용은 [새 ASP.NET 요청 유효성 검사 기능을](#_Toc318097379)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="7b3ce-510">섹션의 `<modules>` 요소에는 특성이 `runAllManagedModulesForAllRequests` 포함되어 있지 않습니다. `<system.webServer>`</span><span class="sxs-lookup"><span data-stu-id="7b3ce-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="7b3ce-511">(기본값은 false입니다.) 즉, SP1로 업데이트되지 않은 IIS 7 버전을 사용하는 경우 새 사이트에서 라우팅에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="7b3ce-512">자세한 내용은 [라우팅에 대한 IIS 7의 기본 지원을](#Native_Support_In_IIS7_For_ASPNET_Routine)ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="7b3ce-513">이러한 변경 사항은 기존 응용 프로그램에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="7b3ce-514">그러나 새 템플릿을 사용하여 ASP.NET 4.5에 대해 만든 기존 웹 사이트와 새 웹 사이트 간의 동작 차이를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="7b3ce-515">ASP.NET 라우팅을 위한 IIS 7의 기본 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="7b3ce-516">이 와 같은 ASP.NET 변경 되지 않습니다., 하지만 SP1 업데이트 적용 되지 않은 IIS 7의 버전을 작업 하는 경우 영향을 미칠 수 있는 새 웹 사이트 프로젝트에 대 한 템플릿변경.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="7b3ce-517">ASP.NET 라우팅을 지원하기 위해 다음 구성 설정을 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="7b3ce-518">**runAllManagedModulesForAllRequests가** true이면 `http://mysite/myapp/home` *URL에 .aspx,* *.mvc*또는 이와 유사한 확장이 없더라도 url과 같은 URL이 ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="7b3ce-519">IIS 7에 대한 업데이트로 인해 **runAllManagedModulesForAllRequests가** 불필요하게 설정되고 기본적으로 라우팅ASP.NET 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="7b3ce-520">업데이트에 대한 자세한 내용은 Microsoft 지원 문서 [특정 IIS 7.0 또는 IIS 7.5 처리기가 기간으로 종료되지 않는 요청을 처리할 수 있는 업데이트를 사용할 수](https://support.microsoft.com/kb/980368)있습니다.)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="7b3ce-521">웹 사이트가 IIS 7에서 실행중이고 IIS가 업데이트된 경우 **runAllManagedModulesForAllRequests를** true로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="7b3ce-522">실제로 요청에 불필요한 처리 오버헤드가 추가되므로 true로 설정하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="7b3ce-523">이 설정이 true이면 *.htm,* *.jpg*및 기타 정적 파일에 대한 요청및 기타 정적 파일을 포함한 모든 요청도 요청 ASP.NET 파이프라인을 거닐게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="7b3ce-524">Visual Studio 2012 RC에서 제공되는 템플릿을 사용하여 새 ASP.NET 4.5 웹 사이트를 만드는 경우 웹 사이트의 구성에는 **runAllManagedModulesForAllRequests** 설정이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="7b3ce-525">즉, 기본적으로 설정이 false입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="7b3ce-526">그런 다음 SP1이 설치되지 않은 Windows 7에서 웹 사이트를 실행하는 경우 IIS 7에는 필요한 업데이트가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="7b3ce-527">결과적으로 라우팅이 작동하지 않으며 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="7b3ce-528">라우팅이 작동하지 않는 문제가 있는 경우 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="7b3ce-529">IIS 7에 업데이트를 추가하는 SP1로 Windows 7을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="7b3ce-530">이전에 나열된 Microsoft 지원 문서에 설명된 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="7b3ce-531">해당 웹 사이트의 Web.config 파일에서 **runAllManagedModulesForAllRequests를** true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="7b3ce-532">이렇게 하면 요청에 약간의 오버헤드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="7b3ce-533">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="7b3ce-534">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="7b3ce-534">Smart Tasks</span></span>

<span data-ttu-id="7b3ce-535">디자인 보기에서 서버 컨트롤의 복잡한 속성에는 쉽게 설정할 수 있도록 대화 상자와 마법사가 연결된 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="7b3ce-536">예를 들어 특수 대화 상자를 사용하여 데이터 원본을 *Repeater* 컨트롤에 추가하거나 *GridView* 컨트롤에 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="7b3ce-537">그러나 복잡한 속성에 대한 이러한 유형의 UI 도움말은 소스 보기에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="7b3ce-538">따라서 Visual Studio 11에서는 소스 보기를 위한 스마트 작업을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="7b3ce-539">스마트 태스크는 C# 및 Visual Basic 편집기에서 일반적으로 사용되는 기능에 대한 컨텍스트 인식 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="7b3ce-540">ASP.NET Web Forms 컨트롤의 경우 삽입 지점이 요소 내부에 있을 때 서버 태그에 작은 글리프로 스마트 작업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="7b3ce-541">글리프를 클릭하거나 CTRL+를 누르면 스마트 작업이 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="7b3ce-542">(점)과 마찬가지로 코드 편집기에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="7b3ce-543">그런 다음 디자인 보기의 스마트 작업과 유사한 바로 가기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="7b3ce-544">예를 들어 이전 그림의 스마트 태스크에는 GridView 작업 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="7b3ce-545">열 편집을 선택하면 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="7b3ce-546">대화 상자에 채우기는 설계 보기에서 설정할 수 있는 것과 동일한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="7b3ce-547">확인을 클릭하면 컨트롤의 태그가 새 설정으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="7b3ce-548">와이 아리아 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-548">WAI-ARIA support</span></span>

<span data-ttu-id="7b3ce-549">액세스 가능한 웹 사이트를 작성하는 것이 점점 더 중요해지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="7b3ce-550">[WAI-ARIA 접근성 표준은](http://www.w3.org/WAI/intro/aria) 개발자가 액세스 가능한 웹 사이트를 작성하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="7b3ce-551">이 표준은 이제 Visual Studio에서 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="7b3ce-552">예를 들어 *역할* 특성에 전체 IntelliSense가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="7b3ce-553">또한 WAI-ARIA 표준은 HTML5 문서에 의미 체계를 추가할 수 있는 *aria가* 접두사에 붙어 있는 특성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="7b3ce-554">비주얼 스튜디오는 또한 완전히 이러한 *aria-속성을* 지원합니다 :</span><span class="sxs-lookup"><span data-stu-id="7b3ce-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="7b3ce-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="7b3ce-556">새로운 HTML5 스니펫</span><span class="sxs-lookup"><span data-stu-id="7b3ce-556">New HTML5 snippets</span></span>

<span data-ttu-id="7b3ce-557">Visual Studio는 일반적으로 사용되는 HTML5 태그를 더 빠르고 쉽게 작성할 수 있도록 여러 스니펫을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="7b3ce-558">예를 들어 비디오 스니펫은 다음과 같은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="7b3ce-559">스니펫을 호출하려면 IntelliSense에서 요소를 선택할 때 탭을 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="7b3ce-560">이렇게 하면 사용자 지정할 수 있는 코드 조각이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="7b3ce-561">사용자 제어로 추출</span><span class="sxs-lookup"><span data-stu-id="7b3ce-561">Extract to user control</span></span>

<span data-ttu-id="7b3ce-562">큰 웹 페이지에서는 개별 조각을 사용자 컨트롤로 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="7b3ce-563">이러한 리팩터링 양식은 페이지의 가독성을 높이고 페이지 구조를 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="7b3ce-564">이를 쉽게 하기 위해 소스 보기에서 웹 양식 페이지를 편집할 때 이제 페이지에서 텍스트를 선택하고 마우스 오른쪽 단추로 클릭한 다음 사용자 컨트롤로 추출을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="7b3ce-565">속성의 코드 너겟에 대한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7b3ce-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="7b3ce-566">Visual Studio는 항상 모든 페이지 또는 컨트롤에서 서버 측 코드 너겟에 대한 IntelliSense를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="7b3ce-567">이제 비주얼 스튜디오뿐만 아니라 HTML 속성의 코드 너겟에 대한 IntelliSense를 포함한다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="7b3ce-568">이렇게 하면 데이터 바인딩 식을 더 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="7b3ce-569">개폐 태그의 이름을 바꿀 때 일치하는 태그의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="7b3ce-570">HTML 요소의 이름을 바꾸면(예: *div* 태그를 *헤더* 태그로 변경) 해당 개폐 태그도 실시간으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="7b3ce-571">이렇게 하면 닫는 태그를 변경하거나 잘못된 태그를 변경하는 것을 잊어버린 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="7b3ce-572">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="7b3ce-572">Event handler generation</span></span>

<span data-ttu-id="7b3ce-573">이제 Visual Studio에는 이벤트 처리기를 작성하고 수동으로 바인딩하는 데 도움이 되는 소스 보기의 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="7b3ce-574">소스 보기에서 이벤트 이름을 편집하는 경우 IntelliSense는&gt;새 이벤트 만들기를 표시하여 &lt;올바른 서명이 있는 페이지 코드에서 이벤트 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="7b3ce-575">기본적으로 이벤트 처리기는 이벤트 처리 메서드의 이름에 컨트롤의 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="7b3ce-576">결과 이벤트 처리기는 다음과 같습니다(이 경우 C#).</span><span class="sxs-lookup"><span data-stu-id="7b3ce-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="7b3ce-577">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-577">Smart indent</span></span>

<span data-ttu-id="7b3ce-578">빈 HTML 요소 안에 있는 동안 Enter를 누르면 편집기에서 삽입 지점을 올바른 위치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="7b3ce-579">이 위치에 Enter를 누르면 닫는 태그가 아래로 이동하고 개구 태그와 일치하도록 들여쓰기됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="7b3ce-580">삽입 점도 들여쓰기됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="7b3ce-581">명령문 자동 축소 완료</span><span class="sxs-lookup"><span data-stu-id="7b3ce-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="7b3ce-582">이제 Visual Studio의 IntelliSense 목록은 입력한 내용에 따라 필터링되므로 관련 옵션만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="7b3ce-583">IntelliSense는 또한 IntelliSense 목록에서 개별 단어의 제목 대/소문자를 기반으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="7b3ce-584">예를 들어 "dl"을 입력하면 dl과 asp:DataList가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="7b3ce-585">이 기능을 사용하면 알려진 요소에 대한 명령문 완성을 더 빠르게 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="7b3ce-586">JavaScript 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-586">JavaScript Editor</span></span>

<span data-ttu-id="7b3ce-587">비주얼 스튜디오 2012 릴리스 후보의 자바 스크립트 편집기는 완전히 새로운 이며 크게 비주얼 스튜디오에서 자바 스크립트와 함께 작업의 경험을 향상.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="7b3ce-588">코드 개요</span><span class="sxs-lookup"><span data-stu-id="7b3ce-588">Code outlining</span></span>

<span data-ttu-id="7b3ce-589">이제 모든 함수에 대해 윤곽영역이 자동으로 생성되므로 현재 포커스와 관련이 없는 파일 의 일부를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="7b3ce-590">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="7b3ce-590">Brace matching</span></span>

<span data-ttu-id="7b3ce-591">삽입 점을 개구부 또는 닫는 중괄호에 놓으면 편집기가 일치하는 중괄호를 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="7b3ce-592">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="7b3ce-592">Go to Definition</span></span>

<span data-ttu-id="7b3ce-593">정의로 이동 명령을 사용하면 함수 또는 변수의 소스로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="7b3ce-594">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-594">ECMAScript5 support</span></span>

<span data-ttu-id="7b3ce-595">편집기는 자바스크립트 언어를 설명하는 표준의 최신 버전인 ECMAScript5의 새 구문 및 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="7b3ce-596">돔 인텔리센스</span><span class="sxs-lookup"><span data-stu-id="7b3ce-596">DOM IntelliSense</span></span>

<span data-ttu-id="7b3ce-597">DOM API에 대한 IntelliSense가 개선되었으며 *쿼리 선택기,* DOM 저장소, 문서 간 메시징 및 *캔버스를*비롯한 많은 새로운 HTML5 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="7b3ce-598">DOM IntelliSense는 이제 네이티브 형식 라이브러리 정의가 아닌 단일 간단한 자바스크립트 파일에 의해 구동됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="7b3ce-599">이렇게 하면 쉽게 확장하거나 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="7b3ce-600">VSDOC 서명 오버로드</span><span class="sxs-lookup"><span data-stu-id="7b3ce-600">VSDOC signature overloads</span></span>

<span data-ttu-id="7b3ce-601">이 예제와 같이 새 \* &lt;서명&gt; \* 요소를 사용하여 JavaScript 함수의 별도의 오버로드에 대해 자세한 IntelliSense 주석을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="7b3ce-602">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="7b3ce-602">Implicit references</span></span>

<span data-ttu-id="7b3ce-603">이제 자바스크립트 파일을 중앙 목록에 추가하여 자바스크립트 파일이나 블록 레퍼런스가 포함된 파일 목록에 암시적으로 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="7b3ce-604">예를 들어, 파일의 중앙 목록에 jQuery 파일을 추가할 수 있습니다., 그리고 당신은 얻을 거 야 질의 함수에 대 한 모든 자바 스크립트 블록파일, 명시적으로 참조 했 든 여부 (사용 하 여 /// &lt;참조/)&gt;.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="7b3ce-605">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="7b3ce-606">명령문 자동 축소 완료</span><span class="sxs-lookup"><span data-stu-id="7b3ce-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="7b3ce-607">CSS의 IntelliSense 목록은 이제 선택한 스키마에서 지원하는 CSS 속성 및 값을 기반으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="7b3ce-608">IntelliSense는 타이틀 케이스 검색도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="7b3ce-609">계층적 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-609">Hierarchical indentation</span></span>

<span data-ttu-id="7b3ce-610">CSS 편집기는 들여쓰기를 사용하여 계층 적 규칙을 표시하므로 계단식 규칙이 논리적으로 구성되는 방법에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="7b3ce-611">다음 예제에서 선택기 #list 목록의 계단식 자식이므로 들여쓰기됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="7b3ce-612">다음 예제에서는 보다 복잡한 상속을 보여 주며 다음과 같은 보다 복잡한 상속을 보여 주며 다음과 같은 보다 복잡한 상속을 보여</span><span class="sxs-lookup"><span data-stu-id="7b3ce-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="7b3ce-613">규칙의 들여쓰기는 상위 규칙에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="7b3ce-614">계층 적 들여쓰기는 기본적으로 활성화되어 있지만 옵션 대화 상자 (도구, 메뉴 모음의 옵션)를 비활성화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="7b3ce-615">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-615">CSS hacks support</span></span>

<span data-ttu-id="7b3ce-616">수백 개의 실제 CSS 파일을 분석하면 CSS 해킹이 매우 일반적이며 이제 Visual Studio가 가장 널리 사용되는 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="7b3ce-617">이 지원에는 IntelliSense 및 별\*() 및\_밑줄 () 속성 해킹의 유효성 검사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="7b3ce-618">일반적인 선택기 해킹도 지원되므로 계층적 들여쓰기가 적용될 때도 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="7b3ce-619">인터넷 익스플로러 7을 대상으로하는 데 사용되는 일반적인 선택기 해킹은 \* \*:첫 번째 자식 + HTML로\*선택기를 준비하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="7b3ce-620">이 규칙을 사용하면 계층적 들여쓰기가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="7b3ce-621">공급업체 별 스키마(-moz-, -웹킷)</span><span class="sxs-lookup"><span data-stu-id="7b3ce-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="7b3ce-622">CSS3는 서로 다른 시간에 다른 브라우저에서 구현된 많은 속성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="7b3ce-623">이전에는 개발자가 공급업체별 구문을 사용하여 특정 브라우저에 대해 코딩해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="7b3ce-624">이러한 브라우저별 속성은 이제 IntelliSense에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="7b3ce-625">댓글 달기 및 댓글 달기 지원</span><span class="sxs-lookup"><span data-stu-id="7b3ce-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="7b3ce-626">이제 코드 편집기에서 사용하는 것과 동일한 바로 가기(Ctrl+K, C에 주석을 달고 Ctrl+K, 주석 을 해제할 수 있음)를 사용하여 CSS 규칙에 주석을 달고 주석을 달 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="7b3ce-627">색 선택</span><span class="sxs-lookup"><span data-stu-id="7b3ce-627">Color picker</span></span>

<span data-ttu-id="7b3ce-628">이전 버전의 Visual Studio에서는 색상 관련 특성에 대한 IntelliSense가 명명된 색상 값의 드롭다운 목록으로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="7b3ce-629">이 목록은 모든 기능을 갖춘 컬러 선택으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="7b3ce-630">색상 값을 입력하면 색상 선택기가 자동으로 표시되고 이전에 사용한 색상 목록이 표시되고 기본 색상 팔레트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="7b3ce-631">마우스 나 키보드를 사용하여 색상을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="7b3ce-632">목록을 전체 색상 선택기로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="7b3ce-633">불투명도 슬라이더를 이동할 때 모든 색상을 RGBA로 자동으로 변환하여 알파 채널을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="7b3ce-634">코드 조각</span><span class="sxs-lookup"><span data-stu-id="7b3ce-634">Snippets</span></span>

<span data-ttu-id="7b3ce-635">CSS 편집기의 스니펫을 통해 브라우저 간 스타일을 더 쉽고 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="7b3ce-636">브라우저별 설정이 필요한 많은 CSS3 속성이 이제 코드 조각으로 롤백되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="7b3ce-637">CSS 스니펫은 IntelliSense 목록을 보여 주면 at-symbol(@를 입력하여 CSS3 미디어 쿼리와 같은 고급 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="7b3ce-638">값을 선택하고 @media 탭을 누르면 CSS 편집기에서 다음 스니펫을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="7b3ce-639">코드용 코드 조각과 마찬가지로 사용자 고유의 CSS 스니펫을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="7b3ce-640">사용자 지정 지역</span><span class="sxs-lookup"><span data-stu-id="7b3ce-640">Custom regions</span></span>

<span data-ttu-id="7b3ce-641">코드 편집기에서 이미 사용할 수 있는 명명된 코드 영역은 이제 CSS 편집에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="7b3ce-642">이렇게 하면 관련 스타일 블록을 쉽게 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="7b3ce-643">영역이 축소되면 영역 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="7b3ce-644">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="7b3ce-644">Page Inspector</span></span>

<span data-ttu-id="7b3ce-645">페이지 검사기는 Visual Studio IDE에서 웹 페이지(HTML, 웹 양식, ASP.NET MVC 또는 웹 페이지)를 렌더링하고 소스 코드와 결과 출력을 모두 검사할 수 있는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="7b3ce-646">ASP.NET 페이지의 경우 Page Inspector를 사용하면 브라우저에 렌더링되는 HTML 태그를 생성한 서버 측 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="7b3ce-647">페이지 관리자에 대한 자세한 내용은 다음 자습서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="7b3ce-648">[ASP.NET MVC에서](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md) 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="7b3ce-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="7b3ce-649">ASP.NET 웹 [양식에서](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md) 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="7b3ce-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="7b3ce-650">게시</span><span class="sxs-lookup"><span data-stu-id="7b3ce-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="7b3ce-651">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="7b3ce-651">Publish profiles</span></span>

<span data-ttu-id="7b3ce-652">Visual Studio 2010에서는 웹 응용 프로그램 프로젝트에 대한 게시 정보가 버전 제어에 저장되지 않으며 다른 사람과 공유하도록 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="7b3ce-653">Visual Studio 2012 릴리스 후보에서 게시 프로필의 형식이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="7b3ce-654">팀 아티팩트가 만들어졌으며 이제 MSBuild를 기반으로 빌드에서 쉽게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="7b3ce-655">빌드 구성 정보는 게시 대화 상자에 있으므로 게시하기 전에 빌드 구성을 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="7b3ce-656">게시 프로필은 PublishProfiles 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="7b3ce-657">폴더의 위치는 사용 중인 프로그래밍 언어에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="7b3ce-658">C#: 속성\게시 프로필</span><span class="sxs-lookup"><span data-stu-id="7b3ce-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="7b3ce-659">비주얼 기본: 내 프로젝트\게시프로필</span><span class="sxs-lookup"><span data-stu-id="7b3ce-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="7b3ce-660">각 프로필은 MSBuild 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="7b3ce-661">게시하는 동안 이 파일은 프로젝트의 MSBuild 파일로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="7b3ce-662">Visual Studio 2010에서 게시 또는 패키지 프로세스를 변경하려면 **ProjectName**.wpp.targets라는 파일에 사용자 지정을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="7b3ce-663">이 지원은 계속 지원되지만 이제 게시 프로필 자체에 사용자 지정을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="7b3ce-664">이렇게 하면 사용자 지정은 해당 프로필에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="7b3ce-665">이제 MSBuild의 게시 프로필을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="7b3ce-666">이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="7b3ce-667">project.csproj 값은 프로젝트의 경로이며 ProfileName은 게시할 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="7b3ce-668">또는 *PublishProfile* 속성의 프로필 이름을 전달하는 대신 전체 경로를 게시 프로필에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="7b3ce-669">사전 컴파일 및 병합ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7b3ce-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="7b3ce-670">웹 응용 프로그램 프로젝트의 경우 Visual Studio 2012 릴리스 후보는 프로젝트를 게시하거나 패키지할 때 사이트의 콘텐츠를 미리 컴파일하고 병합할 수 있는 패키지/게시 웹 속성 페이지에 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="7b3ce-671">이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 패키지/웹 속성 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="7b3ce-672">다음 그림에서는 옵션을 게시하기 전에 이 응용 프로그램을 미리 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="7b3ce-673">이 옵션을 선택하면 웹 응용 프로그램을 게시하거나 패키지할 때마다 Visual Studio에서 응용 프로그램을 미리 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="7b3ce-674">사이트가 미리 컴파일되는 방법 또는 어셈블리병합 방법을 제어하려면 고급 단추를 클릭하여 해당 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="7b3ce-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="7b3ce-675">IIS Express</span></span>

<span data-ttu-id="7b3ce-676">비주얼 스튜디오에서 웹 프로젝트를 테스트하기위한 기본 웹 서버는 이제 IIS 익스프레스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="7b3ce-677">Visual Studio 개발 서버는 개발 중에도 로컬 웹 서버의 옵션이지만 IIS Express는 이제 권장 서버가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="7b3ce-678">비주얼 스튜디오 11 베타에서 IIS Express를 사용하는 경험은 Visual Studio 2010 SP1에서 사용하는 것과 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="7b3ce-679">고지 사항</span><span class="sxs-lookup"><span data-stu-id="7b3ce-679">Disclaimer</span></span>

<span data-ttu-id="7b3ce-680">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="7b3ce-681">이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="7b3ce-682">Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="7b3ce-683">이 백서는 정보 제공만을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="7b3ce-684">Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="7b3ce-685">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="7b3ce-686">저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="7b3ce-687">Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="7b3ce-688">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="7b3ce-689">달리 명시되지 않는 한, 예를 들어 회사, 조직, 제품, 도메인 이름, 이메일 주소, 로고, 로고, 장소 또는 이벤트는 가상이며 실제 회사, 조직, 제품, 도메인 이름, 이메일 주소, 로고, 사람, 장소 또는 이벤트와 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="7b3ce-690">© 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="7b3ce-691">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-691">All rights reserved.</span></span>

<span data-ttu-id="7b3ce-692">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="7b3ce-693">여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b3ce-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
