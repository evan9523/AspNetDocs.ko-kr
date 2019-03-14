---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045600"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a><span data-ttu-id="7712a-101">ASP.NET Core 미들웨어 확장성 샘플</span><span class="sxs-lookup"><span data-stu-id="7712a-101">ASP.NET Core Middleware Extensibility Sample</span></span>

<span data-ttu-id="7712a-102">이 샘플에서는 [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) 및 [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)를 타사 종속성 주입 컨테이너인 [간단한 인젝터](https://simpleinjector.org)와 함께 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7712a-102">This sample illustrates the use of [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) and [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) with a 3rd party dependency injection container, [Simple Injector](https://simpleinjector.org).</span></span> <span data-ttu-id="7712a-103">이 샘플에서는 [ASP.NET Core에서 타사 컨테이너를 사용하여 미들웨어 활성화](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container)에 설명된 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7712a-103">This sample demonstrates the features described in [Middleware activation with a third-party container in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span></span>
