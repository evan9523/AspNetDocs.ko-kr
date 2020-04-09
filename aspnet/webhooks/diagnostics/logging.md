---
uid: webhooks/diagnostics/logging
title: ASP.NET 웹후크 로깅 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET WebHooks에 로그인하는 방법.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675354"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET 웹후크 로깅

Microsoft ASP.NET WebHooks는 로깅을 문제와 문제를 보고하는 방법으로 사용합니다. 기본적으로 로그는 다른 로그 스트림과 마찬가지로 [추적 리스너를](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 사용하여 관리 할 수있는 [System.Diagnostics.Trace를](https://msdn.microsoft.com/library/system.diagnostics.trace) 사용하여 작성됩니다.

웹 응용 프로그램을 Azure 웹 앱으로 배포할 때 로그가 자동으로 선택되며 다른 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 로깅과 함께 관리할 수 있습니다. 자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 진단 로깅 활성화를](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/) 참조하십시오.

또한 Visual Studio를 사용하여 Azure 앱 서비스의 웹 [앱 문제 해결에](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)설명된 대로 Visual Studio 내부에서 바로 로그를 가져올 수 있습니다.

## <a name="redirecting-logs"></a>로그 리디렉션

[System.Diagnostics.Trace에](https://msdn.microsoft.com/library/system.diagnostics.trace)로그를 작성하는 대신 [Log4Net](http://logging.apache.org/log4net/) 및 [NLog](http://nlog-project.org/)와 같은 로그 관리자에 직접 로그할 수 있는 대체 로깅 구현을 제공할 수 있습니다. 단순히 [ILogger의](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 구현을 제공하고 당신의 선택의 종속성 주입 엔진에 등록하고 마이크로 소프트 ASP.NET WebHooks에 의해 포착 얻을 것이다. 자세한 내용은 [ASP.NET 웹 API 2의 종속성 주입을](https://www.asp.net/web-api/overview/advanced/dependency-injection) 참조하십시오.
