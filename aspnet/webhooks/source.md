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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET 웹후크 소스 코드 및 NuGet 패키지

마이크로 소프트 ASP.NET WebHooks 는 마이크로 소프트 ASP.NET 모듈 제품군의 일부이며 [GitHub에서 오픈 소스 프로젝트로](https://github.com/aspnet/WebHooks)호스팅됩니다. 즉, 기부를 수락하지만 끌어오기 요청을 제출하기 전에 [기여 가이드라인을](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 확인하십시오.

현재 읽고 있는 이 온라인 문서는 [GitHub의 오픈 소스로도](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 호스팅되며 기여도 수락합니다.

## <a name="nuget-packages"></a>NuGet 패키지

[NuGet 패키지는](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 나뉩니다.

* [공통](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유되는 공통 패키지입니다.

* [보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사람에게 자신의 WebHooks를 보내는 것을 지원하는 패키지 집합입니다. WebHook을 보내는 기능은 [웹후크 전송에](sending/senders.md)대해 자세히 설명합니다.

* [수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 다른 사람으로부터 WebHooks를 수신하는 것을 지원하는 패키지 집합입니다. WebHook을 수신하는 기능은 [웹후크 수신에](receiving/index.md)대해 자세히 설명합니다.
