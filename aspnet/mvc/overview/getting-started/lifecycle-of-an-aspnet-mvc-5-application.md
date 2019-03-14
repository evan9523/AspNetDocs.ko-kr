---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 애플리케이션의 수명 주기 | Microsoft Docs
author: cephalin
description: ASP.NET MVC 5 애플리케이션의 수명 주기를 차트로 보여주는 PDF 문서를 다운로드합니다. 이 수명 주기 문서는 MVC 수명 주기에 대한 개요를 제공합니다.
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 5523217ae5674ac4e5898a150f9e5f0ae3a70d26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046620"
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="b7787-104">ASP.NET MVC 5 애플리케이션의 수명 주기</span><span class="sxs-lookup"><span data-stu-id="b7787-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>
====================
<span data-ttu-id="b7787-105">작성자: [Cephas Lin](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="b7787-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="b7787-106">PDF 문서 다운로드</span><span class="sxs-lookup"><span data-stu-id="b7787-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="b7787-107">HTTP 요청을 받고 HTTP 요청을 다시 클라이언트로 보내는 ASP.NET MVC 5 애플리케이션의 수명 주기를 차트로 보여주는 PDF 문서를 여기서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="b7787-108">이 문서는 ASP.NET MVC를 처음 접하는 분들을 위한 교육 도구이자 애플리케이션의 특정 기능을 자세히 알아보려는 분들을 위한 참조 자료로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="b7787-109">PDF 문서의 특징은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="b7787-110">MVC가 [ASP.NET 애플리케이션 수명 주기](https://msdn.microsoft.com/library/bb470252.aspx)의 어느 부분에 통합되는지 이해를 도와주는 관련 [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) 단계.</span><span class="sxs-lookup"><span data-stu-id="b7787-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="b7787-111">요청 처리 파이프라인에서 모든 MVC 애플리케이션이 통과하는 주요 단계를 이해할 수 있는 MVC 애플리케이션 수명 주기에 대한 개요 보기.</span><span class="sxs-lookup"><span data-stu-id="b7787-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="b7787-112">요청 처리 파이프라인의 세부 정보를 보여주는 세부 정보 보기.</span><span class="sxs-lookup"><span data-stu-id="b7787-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="b7787-113">개요 보기와 세부 정보 보기를 비교하여 수명 주기에 대한 상세 정보가 다양한 단계로 수집되는 원리를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="b7787-114">더 크게 보려면 [PDF를 다운로드](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)하세요.</span><span class="sxs-lookup"><span data-stu-id="b7787-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="b7787-115">요청 처리 파이프라인의 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) 개체에서 재정의 가능한 모든 메서드의 배치 및 목적.</span><span class="sxs-lookup"><span data-stu-id="b7787-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="b7787-116">어떤 메서드를 재정의해야 할 수도 있고 재정의할 필요가 없을 수도 있지만, 애플리케이션 수명 주기에서 메서드가 하는 역할을 이해하면 적절한 수명 주기 단계에서 코드를 작성하여 원하는 효과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="b7787-117">각 필터 유형(예: 인증, 권한 부여, 작업, 결과)이 호출되는 방식을 보여주는 확대 다이어그램.</span><span class="sxs-lookup"><span data-stu-id="b7787-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="b7787-118">세부 정보 보기의 각 관심 지점에 제공되는 유용한 문서 또는 블로그.</span><span class="sxs-lookup"><span data-stu-id="b7787-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b7787-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7787-119">Next Steps</span></span>

<span data-ttu-id="b7787-120">이 문서로 요구 사항이 충족되었습니까?</span><span class="sxs-lookup"><span data-stu-id="b7787-120">Does this document meet your need?</span></span> <span data-ttu-id="b7787-121">소중한 의견에 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="b7787-122">애플리케이션의 ASP.NET MVC 수명 주기에 대해 궁금한 사항이 있는 경우 [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx)에 질문을 올려주세요.</span><span class="sxs-lookup"><span data-stu-id="b7787-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="b7787-123">twitter에서 [저](https://twitter.com/Cephas_MSFT)를 팔로우하시면 최신 자습서 업데이트를 받으실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7787-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
