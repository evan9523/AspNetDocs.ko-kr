---
uid: webhooks/receiving/dependencies
title: ASP.NET 웹후크 수신기 종속성 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET WebHooks에서 수신기 종속성 및 종속성 주입.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675204"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks 수신기 종속성

Microsoft ASP.NET WebHooks는 종속성 주입을 염두에 두고 설계되었습니다. 시스템의 대부분의 종속성은 종속성 주입 엔진을 사용하여 대체 구현으로 대체할 수 있습니다.

수신기 종속성 목록은 [종속성ScopeExtension을](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 참조하십시오. 종속성이 등록되지 않은 경우 기본 구현이 사용됩니다. 기본 구현 목록은 [ReceiverServices를](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 참조하십시오.
