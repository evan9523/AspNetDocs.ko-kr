---
uid: overview
title: ASP.NET 개요 | Microsoft Docs
author: rick-anderson
description: 웹 사이트, 웹 애플리케이션 및 Web API를 만들 수 있는 무료 프레임워크 ASP.NET을 소개합니다.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 03/12/2010
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: d4b96bd2ff99bb30ff59b9697a27e33acb0f719d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65120089"
---
# <a name="aspnet-overview"></a><span data-ttu-id="1a8bd-103">ASP.NET 개요</span><span class="sxs-lookup"><span data-stu-id="1a8bd-103">ASP.NET overview</span></span>

<span data-ttu-id="1a8bd-104">ASP.NET은 HTML, CSS 및 JavaScript를 사용하여 유용한 웹 사이트와 웹 애플리케이션을 작성할 수 있는 무료 웹 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-104">ASP.NET is a free web framework for building great websites and web applications using HTML, CSS, and JavaScript.</span></span> <span data-ttu-id="1a8bd-105">Web API를 만들고 웹 소켓 같은 실시간 기술도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-105">You can also create Web APIs and use real-time technologies like Web Sockets.</span></span>

<span data-ttu-id="1a8bd-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)는 ASP.NET의 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) is an alternative to ASP.NET.</span></span>  <span data-ttu-id="1a8bd-107">[ASP.NET 및 ASP.NET Core 중에서 선택](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-107">See the [guidance on how to choose between ASP.NET and ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).</span></span>

## <a name="get-started"></a><span data-ttu-id="1a8bd-108">시작</span><span class="sxs-lookup"><span data-stu-id="1a8bd-108">Get started</span></span>

<span data-ttu-id="1a8bd-109">ASP.NET용 무료 IDE인 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-109">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition, a free IDE for ASP.NET on Windows.</span></span>

## <a name="websites-and-web-applications"></a><span data-ttu-id="1a8bd-110">웹 사이트 및 웹 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="1a8bd-110">Websites and web applications</span></span>

 <span data-ttu-id="1a8bd-111">ASP.NET 웹 응용 프로그램을 만들기 위한 세 가지 프레임 워크를 제공 합니다. Web Forms, ASP.NET MVC 및 ASP.NET 웹 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-111">ASP.NET offers three frameworks for creating web applications: Web Forms, ASP.NET MVC, and ASP.NET Web Pages.</span></span> <span data-ttu-id="1a8bd-112">세 프레임워크 모두 안정적이고 완성된 기술이며, 어떤 것을 사용해도 멋진 웹 애플리케이션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-112">All three frameworks are stable and mature, and you can create great web applications with any of them.</span></span> <span data-ttu-id="1a8bd-113">또, 어떤 프레임워크를 선택하더라도 어디에서나 ASP.NET의 모든 장점과 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-113">No matter what framework you choose, you will get all the benefits and features of ASP.NET everywhere.</span></span>

<span data-ttu-id="1a8bd-114">각 프레임워크는 서로 다른 개발 스타일을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-114">Each framework targets a different development style.</span></span> <span data-ttu-id="1a8bd-115">어떤 프레임워크를 선택해야 하는지는 프로그래밍 자산(지식, 기술 및 개발 경험), 만들려는 애플리케이션 종류, 익숙한 개발 방식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-115">The one you choose depends on a combination of your programming assets (knowledge, skills, and development experience), the type of application you're creating, and the development approach you're comfortable with.</span></span>

<span data-ttu-id="1a8bd-116">아래는 각 프레임워크의 개요와 프레임워크 선택 요령입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-116">Below is an overview of each of the frameworks and some ideas for how to choose between them.</span></span> <span data-ttu-id="1a8bd-117">비디오를 선호하는 경우 [ASP.NET으로 웹 사이트 만들기](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) 및 [웹 도구란?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-117">If you prefer a video introduction, see [Making Websites with ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) and [What is Web Tools?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span></span>

|   | <span data-ttu-id="1a8bd-118">다음 분야에 대한 경험이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="1a8bd-118">If you have experience in</span></span> | <span data-ttu-id="1a8bd-119">개발 스타일</span><span class="sxs-lookup"><span data-stu-id="1a8bd-119">Development style</span></span> | <span data-ttu-id="1a8bd-120">전문 지식</span><span class="sxs-lookup"><span data-stu-id="1a8bd-120">Expertise</span></span> |
|-----------|----------------------|-----------------------------------------------------|----------------|
| <span data-ttu-id="1a8bd-121">Web Forms</span><span class="sxs-lookup"><span data-stu-id="1a8bd-121">Web Forms</span></span> | <span data-ttu-id="1a8bd-122">Win Forms, WPF, .NET</span><span class="sxs-lookup"><span data-stu-id="1a8bd-122">Win Forms, WPF, .NET</span></span> | <span data-ttu-id="1a8bd-123">HTML 태그를 캡슐화하는 풍부한 컨트롤 라이브러리를 사용하여 신속하게 개발</span><span class="sxs-lookup"><span data-stu-id="1a8bd-123">Rapid development using a rich library of controls that encapsulate HTML markup</span></span> | <span data-ttu-id="1a8bd-124">중간 수준, 고급 RAD</span><span class="sxs-lookup"><span data-stu-id="1a8bd-124">Mid-Level, Advanced RAD</span></span> |
| <span data-ttu-id="1a8bd-125">MVC</span><span class="sxs-lookup"><span data-stu-id="1a8bd-125">MVC</span></span>       | <span data-ttu-id="1a8bd-126">Ruby on Rails, .NET</span><span class="sxs-lookup"><span data-stu-id="1a8bd-126">Ruby on Rails, .NET</span></span>  | <span data-ttu-id="1a8bd-127">HTML 태그를 완벽하게 제어할 수 있고, 코드와 태그가 분리되고, 테스트를 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-127">Full control over HTML markup, code and markup separated, and easy to write tests.</span></span> <span data-ttu-id="1a8bd-128">모바일 및 단일 페이지 애플리케이션(SPA)에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-128">The best choice for mobile and single-page applications (SPA).</span></span> | <span data-ttu-id="1a8bd-129">중간 수준, 고급</span><span class="sxs-lookup"><span data-stu-id="1a8bd-129">Mid-Level, Advanced</span></span> |
| <span data-ttu-id="1a8bd-130">Web Pages</span><span class="sxs-lookup"><span data-stu-id="1a8bd-130">Web Pages</span></span>  | <span data-ttu-id="1a8bd-131">클래식 ASP, PHP</span><span class="sxs-lookup"><span data-stu-id="1a8bd-131">Classic ASP, PHP</span></span>     | <span data-ttu-id="1a8bd-132">HTML 태그와 코드가 같은 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-132">HTML markup and your code together in the same file</span></span> | <span data-ttu-id="1a8bd-133">최신, 중간 수준</span><span class="sxs-lookup"><span data-stu-id="1a8bd-133">New, Mid-Level</span></span> |

### <a name="web-forms"></a><span data-ttu-id="1a8bd-134">Web Forms</span><span class="sxs-lookup"><span data-stu-id="1a8bd-134">Web Forms</span></span>

<span data-ttu-id="1a8bd-135">ASP.NET Web Forms를 사용하면 익숙한 끌어서 놓기, 이벤트 중심 모델을 사용하여 동적 웹 사이트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-135">With ASP.NET Web Forms, you can build dynamic websites using a familiar drag-and-drop, event-driven model.</span></span> <span data-ttu-id="1a8bd-136">디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 데이터 액세스를 지원하는 정교하고 강력한 UI 중심 사이트를 신속하게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-136">A design surface and hundreds of controls and components let you rapidly build sophisticated, powerful UI-driven sites with data access.</span></span>

[<span data-ttu-id="1a8bd-137">Web Forms에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-137">Learn more about Web Forms</span></span>](web-forms/index.md)

### <a name="mvc"></a><span data-ttu-id="1a8bd-138">MVC</span><span class="sxs-lookup"><span data-stu-id="1a8bd-138">MVC</span></span>

<span data-ttu-id="1a8bd-139">ASP.NET MVC는 즐겁고, 민첩한 개발을 위해 관점을 명확하게 분리할 수 있으며 마크업을 완벽하게 제어할 수 있는 강력한 패턴 기반의 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-139">ASP.NET MVC gives you a powerful, patterns-based way to build dynamic websites that enables a clean separation of concerns and that gives you full control over markup for enjoyable, agile development.</span></span> <span data-ttu-id="1a8bd-140">또한, 최신 웹 표준을 사용하는 정교한 응용 프로그램을 만들기 위한 TDD 친화적 개발을 지원하는 여러 가지 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-140">ASP.NET MVC includes many features that enable fast, TDD-friendly development for creating sophisticated applications that use the latest web standards.</span></span>

[<span data-ttu-id="1a8bd-141">MVC에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-141">Learn more about MVC</span></span>](mvc/index.md)

### <a name="aspnet-web-pages"></a><span data-ttu-id="1a8bd-142">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="1a8bd-142">ASP.NET Web Pages</span></span>

<span data-ttu-id="1a8bd-143">ASP.NET Web Pages 및 Razor 구문은 서버 코드를 HTML과 결합하여 동적 웹 콘텐츠를 만들 수 있는 빠르고 간단하며 사용하기 쉬운 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-143">ASP.NET Web Pages and the Razor syntax provide a fast, approachable, and lightweight way to combine server code with HTML to create dynamic web content.</span></span> <span data-ttu-id="1a8bd-144">데이터베이스에 연결하고, 비디오를 추가하고, 소셜 네트워킹 사이트에 연결하고, 최신 웹 표준을 준수하는 멋진 사이트를 만드는 데 도움이 되는 여러 가지 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-144">Connect to databases, add video, link to social networking sites, and include many more features that help you create beautiful sites that conform to the latest web standards.</span></span>

[<span data-ttu-id="1a8bd-145">Web Pages에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-145">Learn more about Web Pages</span></span>](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a><span data-ttu-id="1a8bd-146">Web Forms, MVC 및 Web Pages에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="1a8bd-146">Notes about Web Forms, MVC, and Web Pages</span></span>

<span data-ttu-id="1a8bd-147">세 ASP.NET 프레임워크는 모두 .NET Framework를 기반으로 하고 .NET 및 ASP.NET의 핵심 기능을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-147">All three ASP.NET frameworks are based on the .NET Framework and share core functionality of .NET and of ASP.NET.</span></span> <span data-ttu-id="1a8bd-148">예를 들어 세 프레임워크 모두 멤버 자격 기반의 로그인 보안 모델을 제공하며, 요청을 관리하고 세션을 처리하기 위한 기능과 그 밖의 핵심 ASP.NET 기능을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-148">For example, all three frameworks offer a login security model based around membership, and all three share the same facilities for managing requests, handling sessions, and so on that are part of the core ASP.NET functionality.</span></span>

<span data-ttu-id="1a8bd-149">뿐만 아니라 세 프레임워크가 완전히 독립적인 것은 아니기 때문에 한 프레임워크를 선택한다고 해서 나머지 두 프레임워크를 사용할 수 없는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-149">In addition, the three frameworks are not entirely independent, and choosing one does not preclude using another.</span></span> <span data-ttu-id="1a8bd-150">여러 프레임워크가 동일한 웹 애플리케이션에서 공존할 수 있으므로 애플리케이션의 개별 구성 요소가 서로 다른 프레임워크를 사용하여 작성된 것을 어렵지 않게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-150">Since the frameworks can coexist in the same web application, it's not uncommon to see individual components of applications written using different frameworks.</span></span> <span data-ttu-id="1a8bd-151">예를 들어 앱에서 고객 응대 부분은 MVC에서 개발하여 표시를 최적화하고, 데이터 및 관리 부분은 Web Forms로 개발하여 데이터 제어 및 간단한 데이터 액세스를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-151">For example, customer-facing portions of an app might be developed in MVC to optimize the markup, while the data access and administrative portions are developed in Web Forms to take advantage of data controls and simple data access.</span></span>

## <a name="web-apis"></a><span data-ttu-id="1a8bd-152">Web API</span><span class="sxs-lookup"><span data-stu-id="1a8bd-152">Web APIs</span></span>

<span data-ttu-id="1a8bd-153">ASP.NET Web API는 브라우저 및 모바일 디바이스를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-153">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="1a8bd-154">ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-154">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

[<span data-ttu-id="1a8bd-155">Web API에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-155">Learn more about Web API</span></span>](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a><span data-ttu-id="1a8bd-156">실시간 기술</span><span class="sxs-lookup"><span data-stu-id="1a8bd-156">Real-time technologies</span></span>

<span data-ttu-id="1a8bd-157">ASP.NET SignalR은 실시간 웹 기능을 좀 더 쉽게 개발할 수 있도록 도와주는 새로운 ASP.NET 개발자용 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-157">ASP.NET SignalR is a new library for ASP.NET developers that makes developing real-time web functionality easier.</span></span> <span data-ttu-id="1a8bd-158">SignalR을 사용하면 서버와 클라이언트 간에 양방향 통신이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-158">SignalR allows bi-directional communication between server and client.</span></span> <span data-ttu-id="1a8bd-159">클라이언트를 사용할 수 있게 되면 서버는 그 즉시 연결된 클라이언트로 콘텐츠를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-159">Servers can push content to connected clients instantly as it becomes available.</span></span> <span data-ttu-id="1a8bd-160">SignalR은 웹 소켓을 지원하며, 이전 버전의 브라우저와 호환되는 다른 기술로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-160">SignalR supports Web Sockets, and falls back to other compatible techniques for older browsers.</span></span> <span data-ttu-id="1a8bd-161">SignalR은 연결 관리(예: 이벤트 연결 및 연결 끊기), 연결 그룹화 및 권한 부여를 위한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-161">SignalR includes APIs for connection management (for instance, connect and disconnect events), grouping connections, and authorization.</span></span>

[<span data-ttu-id="1a8bd-162">SignalR에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-162">Learn more about SignalR</span></span>](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a><span data-ttu-id="1a8bd-163">모바일 앱 및 사이트</span><span class="sxs-lookup"><span data-stu-id="1a8bd-163">Mobile apps and sites</span></span>

<span data-ttu-id="1a8bd-164">ASP.NET은 Web API 백 엔드로 네이티브 모바일 앱을 활용할 수 있을 뿐 아니라 Twitter Bootstrap 같은 반응형 디자인 프레임워크를 사용하여 모바일 웹 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-164">ASP.NET can power native mobile apps with a Web API back end, as well as mobile web sites using responsive design frameworks like Twitter Bootstrap.</span></span> <span data-ttu-id="1a8bd-165">네이티브 모바일 앱을 빌드하는 경우 데이터 액세스, 인증, 앱의 푸시 알림을 처리하는 JSON 기반 Web API를 손쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-165">If you are building a native mobile app, it's easy to create a JSON-based Web API to handle data access, authentication, and push notifications for your app.</span></span> <span data-ttu-id="1a8bd-166">반응형 모바일 사이트를 빌드하는 경우 선호하는 CSS 프레임워크 또는 오픈 그리드 시스템을 사용해도 되고, jQuery Mobile 또는 Sencha 같은 강력한 모바일 시스템과 PhoneGap 같은 뛰어난 모바일 애플리케이션을 선택해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-166">If you are building a responsive mobile site, you can use any CSS framework or open grid system you prefer, or select a powerful mobile system like jQuery Mobile or Sencha and great mobile applications with PhoneGap.</span></span>

[<span data-ttu-id="1a8bd-167">모바일 앱 및 사이트 개발에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-167">Learn more about mobile app and site development</span></span>](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a><span data-ttu-id="1a8bd-168">단일 페이지 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="1a8bd-168">Single-page applications</span></span>

<span data-ttu-id="1a8bd-169">ASP.NET SPA(단일 페이지 애플리케이션)는 HTML 5, CSS 3 및 JavaScript를 사용하여 중요한 클라이언트 쪽 상호 작용을 포함하는 애플리케이션을 빌드할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-169">ASP.NET Single Page Application (SPA) helps you build applications that include significant client-side interactions using HTML 5, CSS 3 and JavaScript.</span></span> <span data-ttu-id="1a8bd-170">Visual Studio에는 knockout.js 및 ASP.NET Web API를 사용하여 단일 페이지 애플리케이션을 구축할 수 있는 템플릿이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-170">Visual Studio includes a template for building single page applications using knockout.js and ASP.NET Web API.</span></span> <span data-ttu-id="1a8bd-171">기본 제공 SPA 템플릿 외에도 커뮤니티에서 만든 SPA 템플릿을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-171">In addition to the built-in SPA template, community-created SPA templates are also available for download.</span></span>

[<span data-ttu-id="1a8bd-172">단일 페이지 앱 개발에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-172">Learn more about single-page app development</span></span>](single-page-application/index.md)

## <a name="webhooks"></a><span data-ttu-id="1a8bd-173">웹후크</span><span class="sxs-lookup"><span data-stu-id="1a8bd-173">WebHooks</span></span>

<span data-ttu-id="1a8bd-174">WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-174">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="1a8bd-175">서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-175">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="1a8bd-176">POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-176">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="1a8bd-177">Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello를 포함한 여러 서비스에 WebHook가 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-177">WebHooks are exposed by a large number of services including Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello, and many more.</span></span> <span data-ttu-id="1a8bd-178">예를 들어 WebHook는 Dropbox에서 파일이 변경되었거나, GitHub에서 코드가 변경되었거나, PayPal에서 대금 결제가 시작되었거나, Trello에서 카드가 생성되었음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8bd-178">For example, a WebHook can indicate that a file has changed in Dropbox, or a code change has been committed in GitHub, or a payment has been initiated in PayPal, or a card has been created in Trello.</span></span>

[<span data-ttu-id="1a8bd-179">WebHook에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1a8bd-179">Learn more about WebHooks</span></span>](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
