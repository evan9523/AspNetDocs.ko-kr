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
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="6850a-103">ASP.NET 웹후크 로깅</span><span class="sxs-lookup"><span data-stu-id="6850a-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="6850a-104">Microsoft ASP.NET WebHooks는 로깅을 문제와 문제를 보고하는 방법으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6850a-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="6850a-105">기본적으로 로그는 다른 로그 스트림과 마찬가지로 [추적 리스너를](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 사용하여 관리 할 수있는 [System.Diagnostics.Trace를](https://msdn.microsoft.com/library/system.diagnostics.trace) 사용하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6850a-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="6850a-106">웹 응용 프로그램을 Azure 웹 앱으로 배포할 때 로그가 자동으로 선택되며 다른 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 로깅과 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6850a-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="6850a-107">자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 진단 로깅 활성화를](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/) 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6850a-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="6850a-108">또한 Visual Studio를 사용하여 Azure 앱 서비스의 웹 [앱 문제 해결에](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)설명된 대로 Visual Studio 내부에서 바로 로그를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6850a-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="6850a-109">로그 리디렉션</span><span class="sxs-lookup"><span data-stu-id="6850a-109">Redirecting Logs</span></span>

<span data-ttu-id="6850a-110">[System.Diagnostics.Trace에](https://msdn.microsoft.com/library/system.diagnostics.trace)로그를 작성하는 대신 [Log4Net](http://logging.apache.org/log4net/) 및 [NLog](http://nlog-project.org/)와 같은 로그 관리자에 직접 로그할 수 있는 대체 로깅 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6850a-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="6850a-111">단순히 [ILogger의](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 구현을 제공하고 당신의 선택의 종속성 주입 엔진에 등록하고 마이크로 소프트 ASP.NET WebHooks에 의해 포착 얻을 것이다.</span><span class="sxs-lookup"><span data-stu-id="6850a-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="6850a-112">자세한 내용은 [ASP.NET 웹 API 2의 종속성 주입을](https://www.asp.net/web-api/overview/advanced/dependency-injection) 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6850a-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
