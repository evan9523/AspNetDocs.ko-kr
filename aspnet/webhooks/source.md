---
uid: webhooks/source
title: ASP.NET 웹후크 소스 코드 및 NuGet 패키지 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 웹후크 소스 코드 및 NuGet 패키지에 대한 링크
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675317"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="c25b6-103">ASP.NET 웹후크 소스 코드 및 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="c25b6-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="c25b6-104">마이크로 소프트 ASP.NET WebHooks 는 마이크로 소프트 ASP.NET 모듈 제품군의 일부이며 [GitHub에서 오픈 소스 프로젝트로](https://github.com/aspnet/WebHooks)호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="c25b6-105">즉, 기부를 수락하지만 끌어오기 요청을 제출하기 전에 [기여 가이드라인을](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="c25b6-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="c25b6-106">현재 읽고 있는 이 온라인 문서는 [GitHub의 오픈 소스로도](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 호스팅되며 기여도 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="c25b6-107">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="c25b6-107">NuGet packages</span></span>

<span data-ttu-id="c25b6-108">[NuGet 패키지는](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="c25b6-109">[공통](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유되는 공통 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="c25b6-110">[보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사람에게 자신의 WebHooks를 보내는 것을 지원하는 패키지 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="c25b6-111">WebHook을 보내는 기능은 [웹후크 전송에](sending/senders.md)대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="c25b6-112">[수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 다른 사람으로부터 WebHooks를 수신하는 것을 지원하는 패키지 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="c25b6-113">WebHook을 수신하는 기능은 [웹후크 수신에](receiving/index.md)대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c25b6-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
