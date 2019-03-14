---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056490"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="43469-101">ASP.NET Core 백그라운드 작업 샘플(일반 호스트)</span><span class="sxs-lookup"><span data-stu-id="43469-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="43469-102">이 샘플은 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)의 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="43469-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="43469-103">이 샘플에서는 [ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) 토픽에서 설명된 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43469-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="43469-104">[Visual Studio Code](https://code.visualstudio.com/)에서 샘플을 실행할 때 *.vscode/launch.json*에서 콘솔 구성의 **콘솔** 값을 `externalTerminal` 또는 `integratedTerminal`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="43469-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="43469-105">`internalConsole` 사용은 앱이 백그라운드 작업 항목을 큐에 넣는 데 사용하는 콘솔 키 입력과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43469-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
