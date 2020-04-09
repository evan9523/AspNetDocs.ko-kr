---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '튜토리얼: SignalR 2로 서버 브로드캐스트 | 마이크로 소프트 문서'
author: tdykstra
description: 이 자습서에서는 ASP.NET SignalR 2를 사용하여 서버 브로드캐스트 기능을 제공하는 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675726"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="72b42-103">자습서: SignalR 2를 통해 서버 브로드캐스트</span><span class="sxs-lookup"><span data-stu-id="72b42-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="72b42-104">이 자습서에서는 ASP.NET SignalR 2를 사용하여 서버 브로드캐스트 기능을 제공하는 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="72b42-105">서버 브로드캐스트는 서버가 클라이언트에 전송된 통신을 시작한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="72b42-106">이 자습서에서 만드는 응용 프로그램은 서버 브로드캐스트 기능에 대한 일반적인 시나리오인 주식 시세를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="72b42-107">주기적으로 서버는 주가를 임의로 업데이트하고 연결된 모든 클라이언트에 업데이트를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="72b42-108">브라우저에서 **변경** 및 **%** 열의 숫자와 기호는 서버의 알림에 대한 응답으로 동적으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="72b42-109">동일한 URL에 추가 브라우저를 열면 모두 동일한 데이터와 동일한 데이터 변경 내용이 동시에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="72b42-111">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72b42-112">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-112">Create the project</span></span>
> * <span data-ttu-id="72b42-113">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-113">Set up the server code</span></span>
> * <span data-ttu-id="72b42-114">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-114">Examine the server code</span></span>
> * <span data-ttu-id="72b42-115">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-115">Set up the client code</span></span>
> * <span data-ttu-id="72b42-116">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-116">Examine the client code</span></span>
> * <span data-ttu-id="72b42-117">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="72b42-117">Test the application</span></span>
> * <span data-ttu-id="72b42-118">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="72b42-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b42-119">응용 프로그램을 빌드하는 단계를 거치지 않으려면 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR.Sample 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="72b42-120">이 자습서의 단계를 수행하지 않고 NuGet 패키지를 설치하는 경우 *readme.txt* 파일의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="72b42-121">패키지를 실행하려면 설치된 패키지에서 `ConfigureSignalR` 메서드를 호출하는 OWIN 시작 클래스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="72b42-122">OWIN 시작 클래스를 추가 하지 않으면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="72b42-123">이 문서의 [StockTicker 설치 샘플](#install-the-stockticker-sample) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b42-124">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="72b42-124">Prerequisites</span></span>

* <span data-ttu-id="72b42-125">**ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="72b42-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="72b42-126">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-126">Create the project</span></span>

<span data-ttu-id="72b42-127">이 섹션에서는 Visual Studio 2017을 사용하여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="72b42-128">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="72b42-130">새 **ASP.NET 웹 응용 프로그램 - SignalR.StockTicker** 창에서 **빈 을** 선택하고 **확인을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="72b42-131">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-131">Set up the server code</span></span>

<span data-ttu-id="72b42-132">이 섹션에서는 서버에서 실행되는 코드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="72b42-133">주식 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-133">Create the Stock class</span></span>

<span data-ttu-id="72b42-134">먼저 *주식에* 대한 정보를 저장하고 전송하는 데 사용할 Stock 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="72b42-135">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**클래스** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="72b42-136">클래스 스톡의 이름을 지정하고 프로젝트에 *추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="72b42-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="72b42-137">*Stock.cs* 파일의 코드를 이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="72b42-138">주식을 만들 때 설정하는 두 속성은 `Symbol` (예 : Microsoft의 MSFT) 및 `Price`.</span><span class="sxs-lookup"><span data-stu-id="72b42-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="72b42-139">다른 속성은 설정 `Price`하는 방법 및 시기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="72b42-140">처음 설정하면 `Price`값이 `DayOpen`에 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="72b42-141">그런 다음 설정하면 `Price` `Change` 앱에서 및 의 `PercentChange` 차이를 기준으로 속성 `Price` 값과 `DayOpen`을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="72b42-142">스톡티커허브 및 스톡티커 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="72b42-143">SignalR 허브 API를 사용하여 서버 간 상호 작용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="72b42-144">SignalR `StockTickerHub` `Hub` 클래스에서 파생 된 클래스는 클라이언트에서 받는 연결 및 메서드 호출을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="72b42-145">또한 스톡 데이터를 유지하고 개체를 `Timer` 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="72b42-146">개체는 `Timer` 클라이언트 연결과 관계없이 가격 업데이트를 주기적으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="72b42-147">허브는 일시적이기 때문에 이러한 `Hub` 함수를 클래스에 넣을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="72b42-148">앱은 클라이언트에서 서버로의 `Hub` 연결 및 호출과 같은 허브의 각 작업에 대한 클래스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="72b42-149">따라서 재고 데이터를 유지하고 가격을 업데이트하며 가격 업데이트를 브로드캐스트하는 메커니즘은 별도의 클래스에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="72b42-150">클래스의 `StockTicker`이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-150">You'll name the class `StockTicker`.</span></span>

![스톡티커에서 방송](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="72b42-152">`StockTicker` 서버에서 클래스의 인스턴스가 하나만 실행되도록 하려면 각 `StockTickerHub` 인스턴스에서 단일 `StockTicker` 인스턴스에 대한 참조를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="72b42-153">클래스는 `StockTicker` 스톡 데이터를 가지고 있고 업데이트를 트리거하기 때문에 클라이언트에 브로드캐스트해야 하지만 `StockTicker` 클래스는 `Hub` 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="72b42-154">클래스는 `StockTicker` SignalR 허브 연결 컨텍스트 개체에 대한 참조를 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="72b42-155">그런 다음 SignalR 연결 컨텍스트 개체를 사용하여 클라이언트에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="72b42-156">StockTickerHub.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="72b42-157">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**새 항목** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="72b42-158">**새 항목 추가 - SignalR.StockTicker에서** **설치된** > **시각적 C#** > **웹** > **신호기를** 선택한 다음 **SignalR 허브 클래스(v2)를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="72b42-159">*클래스 StockTickerHub의* 이름을 지정하고 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="72b42-160">이 단계는 *StockTickerHub.cs* 클래스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="72b42-161">동시에 SignalR을 지원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="72b42-162">*StockTickerHub.cs* 파일의 코드를 이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="72b42-163">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-163">Save the file.</span></span>

<span data-ttu-id="72b42-164">앱은 [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스를 사용하여 클라이언트가 서버에서 호출할 수 있는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="72b42-165">한 가지 방법을 정의하고 `GetAllStocks()`있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="72b42-166">클라이언트가 처음에 서버에 연결하면 이 메서드를 호출하여 현재 가격으로 모든 주식 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="72b42-167">메서드는 메모리에서 데이터를 반환하기 `IEnumerable<Stock>` 때문에 동기적으로 실행되고 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="72b42-168">데이터베이스 조회 또는 웹 서비스 호출과 같이 대기가 필요한 작업을 수행하여 메서드가 데이터를 `Task<IEnumerable<Stock>>` 얻어야 하는 경우 비동기 처리를 활성화하기 위해 반환 값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="72b42-169">자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - 비동기적으로 실행되는 경우를](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="72b42-170">속성은 `HubName` 앱이 클라이언트의 JavaScript 코드에서 허브를 참조하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="72b42-171">이 특성을 사용하지 않는 경우 클라이언트의 기본 이름은 클래스 이름의 camelCase 버전이며 이 경우 `stockTickerHub`는 .입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="72b42-172">클래스를 만들 `StockTicker` 때 나중에 볼 수 있듯이 앱은 정적 `Instance` 속성에서 해당 클래스의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="72b42-173">그 단일 `StockTicker` 인스턴스는 얼마나 많은 클라이언트가 연결되거나 연결을 끊는지에 관계없이 메모리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="72b42-174">이 인스턴스는 `GetAllStocks()` 메서드가 현재 주식 정보를 반환하는 데 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="72b42-175">StockTicker.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="72b42-176">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**클래스** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="72b42-177">*클래스 StockTicker의* 이름을 지정하고 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="72b42-178">*StockTicker.cs* 파일의 코드를 이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="72b42-179">모든 스레드는 StockTicker 코드의 동일한 인스턴스를 실행하므로 StockTicker 클래스는 스레드가 안전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="72b42-180">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-180">Examine the server code</span></span>

<span data-ttu-id="72b42-181">서버 코드를 검사하면 앱의 작동 방식을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="72b42-182">정적 필드에 싱글톤 인스턴스 저장</span><span class="sxs-lookup"><span data-stu-id="72b42-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="72b42-183">코드는 클래스의 인스턴스를 통해 `_instance` `Instance` 속성을 백업하는 정적 필드를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="72b42-184">생성자는 비공개이므로 앱에서 만들 수 있는 클래스의 유일한 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="72b42-185">앱은 `_instance` 필드에 대해 [지연 초기화를](/dotnet/framework/performance/lazy-initialization) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="72b42-186">성능상의 이유가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-186">It's not for performance reasons.</span></span> <span data-ttu-id="72b42-187">인스턴스 생성이 스레드에서 안전한지 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="72b42-188">클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행되는 StockTickerHub 클래스의 새 인스턴스는 클래스의 앞에서 보았듯이 `StockTicker.Instance` 정적 속성에서 StockTicker 싱글톤 인스턴스를 `StockTickerHub` 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="72b42-189">주식 데이터를 동시 사전에 저장</span><span class="sxs-lookup"><span data-stu-id="72b42-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="72b42-190">생성자는 일부 샘플 `_stocks` 스톡 데이터로 컬렉션을 초기화하고 `GetAllStocks` 주식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="72b42-191">앞에서 보았듯이 이 stocks 컬렉션은 `StockTickerHub.GetAllStocks`클라이언트가 호출할 수 `Hub` 있는 클래스의 서버 메서드인 에 의해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="72b42-192">stocks 컬렉션은 스레드 안전을 위한 [동시사전](https://msdn.microsoft.com/library/dd287191.aspx) 유형으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="72b42-193">또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용하고 변경할 때 사전을 명시적으로 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="72b42-194">이 샘플 응용 프로그램의 경우 응용 프로그램 데이터를 메모리에 저장하고 앱이 `StockTicker` 인스턴스를 삭제할 때 데이터를 손실해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="72b42-195">실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용하여 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="72b42-196">주기적으로 주가 업데이트</span><span class="sxs-lookup"><span data-stu-id="72b42-196">Periodically updating stock prices</span></span>

<span data-ttu-id="72b42-197">생성자는 주기적으로 `Timer` 주가를 임의로 업데이트하는 메서드를 호출하는 개체를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="72b42-198">`Timer`을 `UpdateStockPrices`호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="72b42-199">가격을 업데이트하기 전에 앱은 개체에 `_updateStockPricesLock` 대한 잠금을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="72b42-200">코드는 다른 스레드가 이미 가격을 업데이트하고 있는지 `TryUpdateStockPrice` 확인한 다음 목록의 각 주식을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="72b42-201">이 `TryUpdateStockPrice` 방법은 주가를 변경할지 여부와 변경 정도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="72b42-202">주가가 변경되면 앱은 `BroadcastStockPrice` 연결된 모든 클라이언트에게 주가 변동을 브로드캐스트하기 위해 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="72b42-203">플래그는 `_updatingStockPrices` [스레드가](https://msdn.microsoft.com/library/x13ttww7.aspx) 안전한지 확인하기 위해 휘발성으로 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="72b42-204">실제 응용 프로그램에서 `TryUpdateStockPrice` 메서드는 가격을 조회하기 위해 웹 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="72b42-205">이 코드에서 앱은 난수 생성기를 사용하여 임의로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="72b42-206">StockTicker 클래스가 고객에게 브로드캐스트할 수 있도록 SignalR 컨텍스트 를 가져오는 것</span><span class="sxs-lookup"><span data-stu-id="72b42-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="72b42-207">가격 변경은 `StockTicker` 개체에서 여기에서 시작되므로 연결된 모든 클라이언트에서 메서드를 `updateStockPrice` 호출해야 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="72b42-208">`Hub` 클래스에서 클라이언트 메서드를 호출하는 API가 `StockTicker` 있지만 `Hub` 클래스에서 파생되지 않으며 `Hub` 개체에 대한 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="72b42-209">연결된 클라이언트로 브로드캐스트하려면 `StockTicker` 클래스에서 클래스에 대한 SignalR 컨텍스트 인스턴스를 `StockTickerHub` 얻고 이를 사용하여 클라이언트에서 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="72b42-210">코드는 싱글톤 클래스 인스턴스를 만들고 생성자를 참조하는 암호를 전달하고 생성자가 속성에 넣을 때 SignalR `Clients` 컨텍스트에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="72b42-211">컨텍스트를 한 번만 가져오는 데는 두 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="72b42-212">컨텍스트의 `Clients` 속성을 가져오는 다음 `StockTickerClient` 속성에 넣으면 클래스와 동일하게 보이는 클라이언트 메서드를 호출하는 `Hub` 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="72b42-213">예를 들어 모든 클라이언트에 브로드캐스트하려면 을 작성할 `Clients.All.updateStockPrice(stock)`수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="72b42-214">호출하는 메서드는 `updateStockPrice` 아직 `BroadcastStockPrice` 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="72b42-215">클라이언트에서 실행되는 코드를 작성할 때 나중에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="72b42-216">앱이 런타임시 식을 `updateStockPrice` 평가한다는 의미동적이기 때문에 `Clients.All` 여기에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="72b42-217">이 메서드 호출이 실행되면 SignalR은 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트에 라는 `updateStockPrice`메서드가 있는 경우 앱은 해당 메서드를 호출하고 매개 변수 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="72b42-218">`Clients.All`즉, 모든 클라이언트에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="72b42-219">SignalR은 보낼 클라이언트 또는 클라이언트 그룹을 지정하는 다른 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="72b42-220">자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="72b42-221">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="72b42-221">Register the SignalR route</span></span>

<span data-ttu-id="72b42-222">서버는 어떤 URL을 가로채서 SignalR로 전달할지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="72b42-223">이렇게 하려면 OWIN 시작 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="72b42-224">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**새 항목** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="72b42-225">**새 항목 추가 - SignalR.StockTicker** **설치된** > **시각적 C#** > **웹을** 선택한 다음 **OWIN 시작 클래스를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="72b42-226">*클래스* 시작 이름을 지정하고 **확인을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="72b42-227">*Startup.cs* 파일의 기본 코드를 이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="72b42-228">이제 서버 코드 설정이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="72b42-229">다음 섹션에서는 클라이언트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="72b42-230">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-230">Set up the client code</span></span>

<span data-ttu-id="72b42-231">이 섹션에서는 클라이언트에서 실행되는 코드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="72b42-232">HTML 페이지 및 자바스크립트 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="72b42-233">HTML 페이지에 데이터가 표시되고 JavaScript 파일이 데이터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="72b42-234">스톡티커 만들기.html</span><span class="sxs-lookup"><span data-stu-id="72b42-234">Create StockTicker.html</span></span>

<span data-ttu-id="72b42-235">먼저 HTML 클라이언트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="72b42-236">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**HTML 페이지** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="72b42-237">파일 *스톡티커의* 이름을 지정하고 **확인을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="72b42-238">*StockTicker.html* 파일의 기본 코드를 이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="72b42-239">HTML은 5개의 열, 헤더 행 및 5개의 열모두에 걸쳐 있는 단일 셀이 있는 데이터 행이 있는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="72b42-240">데이터 행에 "로드..."가 표시됩니다. 앱이 시작될 때 순간적으로</span><span class="sxs-lookup"><span data-stu-id="72b42-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="72b42-241">JavaScript 코드는 해당 행을 제거하고 서버에서 검색된 스톡 데이터가 있는 해당 자리 행에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="72b42-242">스크립트 태그는 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-242">The script tags specify:</span></span>

    * <span data-ttu-id="72b42-243">jQuery 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-243">The jQuery script file.</span></span>

    * <span data-ttu-id="72b42-244">SignalR 코어 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="72b42-245">SignalR 프록시 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="72b42-246">나중에 만들 스톡티커 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="72b42-247">앱은 SignalR 프록시 스크립트 파일을 동적으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="72b42-248">"/signalr/hubs" URL을 지정 하 고 Hub 클래스의 메서드에 대 한 프록시 `StockTickerHub.GetAllStocks`메서드를 정의 합니다.이 경우 에 대 한 입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="72b42-249">원하는 경우 [SignalR 유틸리티를](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)사용하여 이 JavaScript 파일을 수동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="72b42-250">메서드 호출에서 동적 파일 생성을 `MapHubs` 사용하지 않도록 설정하는 것을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="72b42-251">**솔루션 탐색기에서** **스크립트를 확장합니다.**</span><span class="sxs-lookup"><span data-stu-id="72b42-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="72b42-252">jQuery 및 SignalR에 대한 스크립트 라이브러리는 프로젝트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72b42-253">패키지 관리자는 SignalR 스크립트의 이후 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="72b42-254">프로젝트의 스크립트 파일 버전에 해당하도록 코드 블록의 스크립트 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="72b42-255">**솔루션 탐색기에서** *StockTicker.html을*마우스 오른쪽 단추로 클릭한 다음 **시작 페이지로 설정을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="72b42-256">스톡티커 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-256">Create StockTicker.js</span></span>

<span data-ttu-id="72b42-257">이제 자바 스크립트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="72b42-258">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**JavaScript 파일** **추가를** > 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="72b42-259">파일 *스톡티커의* 이름을 지정하고 **확인을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="72b42-260">이 코드를 *StockTicker.js* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="72b42-261">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-261">Examine the client code</span></span>

<span data-ttu-id="72b42-262">클라이언트 코드를 검사하면 클라이언트 코드가 서버 코드와 상호 작용하여 앱이 작동하는 방법을 알아보는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="72b42-263">연결 시작</span><span class="sxs-lookup"><span data-stu-id="72b42-263">Starting the connection</span></span>

<span data-ttu-id="72b42-264">`$.connection`는 SignalR 프록시를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="72b42-265">코드는 클래스의 프록시에 대한 `StockTickerHub` 참조를 얻고 `ticker` 변수에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="72b42-266">프록시 이름은 `HubName` 특성에 의해 설정된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="72b42-267">모든 변수와 함수를 정의한 후 파일의 마지막 코드 줄은 SignalR 함수를 호출하여 `start` SignalR 연결을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="72b42-268">함수는 `start` 비동기적으로 실행되고 [jQuery 지연 된 개체를](http://api.jquery.com/category/deferred-object/)반환합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="72b42-269">done 함수를 호출하여 앱이 비동기 작업을 완료할 때 호출할 함수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="72b42-270">모든 주식 얻기</span><span class="sxs-lookup"><span data-stu-id="72b42-270">Getting all the stocks</span></span>

<span data-ttu-id="72b42-271">이 `init` 함수는 `getAllStocks` 서버의 함수를 호출하고 서버가 반환하는 정보를 사용하여 스톡 테이블을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="72b42-272">기본적으로 메서드 이름이 서버에서 파스칼 대/소문자인 경우에도 클라이언트에서 camelCasing을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="72b42-273">낙타 선 규칙은 개체가 아닌 메서드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="72b42-274">예를 들어, `stock.Symbol` 및 `stock.Price`을 `stock.symbol` 참조합니다. `stock.price`</span><span class="sxs-lookup"><span data-stu-id="72b42-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="72b42-275">메서드에서 `init` 앱은 개체의 형식 속성을 호출한 다음 변수의 자리 `formatStock` 표시자를 `stock` 개체 `stock` 속성 값으로 `supplant` 바꾸기 위해 호출하여 `rowTemplate` 서버에서 받은 각 stock 개체에 대한 테이블 행에 대한 HTML을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="72b42-276">그런 다음 결과 HTML이 주식 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="72b42-277">비동기 `init` `callback` `start` 함수가 완료된 후 실행되는 함수로 전달하여 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="72b42-278">호출 `start`후 `init` 별도의 JavaScript 문으로 호출하면 시작 함수가 연결 설정이 완료될 때까지 기다리지 않고 즉시 실행되므로 함수가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="72b42-279">이 경우 함수는 앱이 `init` `getAllStocks` 서버 연결을 설정하기 전에 함수를 호출하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="72b42-280">주가 업데이트</span><span class="sxs-lookup"><span data-stu-id="72b42-280">Getting updated stock prices</span></span>

<span data-ttu-id="72b42-281">서버가 주식 가격을 변경하면 연결된 클라이언트를 호출합니다. `updateStockPrice`</span><span class="sxs-lookup"><span data-stu-id="72b42-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="72b42-282">앱은 `stockTicker` 프록시의 클라이언트 속성에 함수를 추가하여 서버에서 호출할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="72b42-283">함수는 `updateStockPrice` 서버에서 받은 스톡 개체를 `init` 함수와 동일한 방식으로 테이블 행에 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="72b42-284">테이블에 행을 넣는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="72b42-285">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="72b42-285">Test the application</span></span>

<span data-ttu-id="72b42-286">앱이 작동하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="72b42-287">모든 브라우저 창이 주가 변동과 함께 라이브 주식 테이블을 표시 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="72b42-288">도구 모음에서 스크립트 **디버깅을** 켜고 재생 버튼을 선택하여 디버그 모드에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![사용자가 디버깅 모드를 켜고 재생을 선택하는 스크린샷입니다.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="72b42-290">**라이브 스톡 테이블을**표시하는 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="72b42-291">주식 테이블에는 처음에 "로드..."가 표시됩니다. 그런 다음 짧은 시간 후에 앱에 초기 주식 데이터가 표시되고 주가가 변경되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="72b42-292">브라우저에서 URL을 복사하고 다른 두 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="72b42-293">초기 재고 표시는 첫 번째 브라우저와 동일하며 변경 사항이 동시에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="72b42-294">모든 브라우저를 닫고 새 브라우저를 열고 동일한 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="72b42-295">StockTicker 싱글톤 개체는 서버에서 계속 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="72b42-296">**라이브 주식 테이블은** 주식이 계속 변화하고 있음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="72b42-297">변경 수치가 0인 초기 테이블이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="72b42-298">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="72b42-299">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="72b42-299">Enable logging</span></span>

<span data-ttu-id="72b42-300">SignalR에는 클라이언트에서 문제 해결을 돕기 위해 활성화할 수 있는 기본 제공 로깅 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="72b42-301">이 섹션에서는 로깅을 사용하도록 설정하고 로그가 SignalR에서 사용하는 다음 전송 방법을 알려주는 방법을 보여 주는 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="72b42-302">[웹 소켓](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 현재 브라우저에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="72b42-303">[서버 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), 인터넷 익스플로러 이외의 브라우저에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="72b42-304">[영원히 프레임,](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)인터넷 익스플로러에 의해 지원.</span><span class="sxs-lookup"><span data-stu-id="72b42-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="72b42-305">모든 브라우저에서 지원하는 [Ajax 긴 폴링.](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)</span><span class="sxs-lookup"><span data-stu-id="72b42-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="72b42-306">지정된 연결에 대해 SignalR은 서버와 클라이언트가 지원하는 최상의 전송 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="72b42-307">오픈 *스톡티커.js*.</span><span class="sxs-lookup"><span data-stu-id="72b42-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="72b42-308">이 강조 표시된 코드 줄을 추가하면 파일 끝에 연결을 초기화하는 코드 바로 앞에서 로깅을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="72b42-309">**F5를** 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="72b42-310">브라우저의 개발자 도구 창을 열고 콘솔을 선택하여 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="72b42-311">새 연결에 대 한 전송 메서드를 협상 하는 SignalR의 로그를 보려면 페이지를 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="72b42-312">Windows 8(IIS 8)에서 Internet Explorer 10을 실행하는 경우 전송 방법은 **WebSockets**입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="72b42-313">Windows 7(IIS 7.5)에서 인터넷 익스플로러 10을 실행하는 경우 전송 방법은 **iframe**입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="72b42-314">Windows 8(IIS 8)에서 Firefox 19를 실행하는 경우 전송 방법은 **WebSockets**입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="72b42-315">파이어 폭스에서, 콘솔 창을 얻기 위해 파이어 버그 추가 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="72b42-316">Windows 7(IIS 7.5)에서 Firefox 19를 실행하는 경우 전송 방법은 **서버에서 전송하는** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="72b42-317">스톡티커 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="72b42-317">Install the StockTicker sample</span></span>

<span data-ttu-id="72b42-318">[Microsoft.AspNet.SignalR.샘플은](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="72b42-319">NuGet 패키지에는 처음부터 만든 단순화된 버전보다 더 많은 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="72b42-320">자습서의 이 섹션에서는 NuGet 패키지를 설치하고 새 기능과 이를 구현하는 코드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b42-321">이 자습서의 이전 단계를 수행하지 않고 패키지를 설치하는 경우 프로젝트에 OWIN 시작 클래스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="72b42-322">NuGet 패키지에 대한 이 readme.txt 파일은 이 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="72b42-323">SignalR.샘플 NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="72b42-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="72b42-324">**솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리를 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="72b42-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="72b42-325">**NuGet 패키지 관리자: SignalR.StockTicker,** 찾아보기 를 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="72b42-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="72b42-326">**패키지 소스에서** **nuget.org**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="72b42-327">검색 상자에 *SignalR.Sample을* 입력하고 **Microsoft.AspNet.SignalR.샘플** > **설치를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="72b42-328">**솔루션 탐색기에서** *SignalR.Sample* 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="72b42-329">SignalR.Sample 패키지를 설치하면 폴더와 해당 내용이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="72b42-330">*SignalR.Sample* 폴더에서 *StockTicker.html을*마우스 오른쪽 단추로 클릭한 다음 **시작 페이지로 설정 옵션을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72b42-331">SignalR.Sample NuGet 패키지를 설치하면 스크립트 폴더에 있는 jQuery 버전이 변경될 수 *있습니다.*</span><span class="sxs-lookup"><span data-stu-id="72b42-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="72b42-332">패키지가 *SignalR.Sample* 폴더에 설치하는 새 *StockTicker.html* 파일은 패키지가 설치하는 jQuery 버전과 동기화되지만 원래 *StockTicker.html* 파일을 다시 실행하려면 먼저 스크립트 태그에서 jQuery 참조를 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="72b42-333">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="72b42-333">Run the application</span></span>

 <span data-ttu-id="72b42-334">첫 번째 앱에서 본 테이블에는 유용한 기능이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="72b42-335">전체 주식 시세 응용 프로그램은 새로운 기능을 보여줍니다: 주식 데이터와 상승 및 하락으로 색상을 변경 하는 주식을 표시 하는 가로 스크롤 창.</span><span class="sxs-lookup"><span data-stu-id="72b42-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="72b42-336">**F5를** 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="72b42-337">앱을 처음 실행하면 "시장"이 "닫혀"되고 정적 테이블과 스크롤되지 않는 티커 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="72b42-338">**오픈 마켓을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-338">Select **Open Market**.</span></span>

    ![라이브 시세의 스크린 샷.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="72b42-340">**라이브 주식 시세** 상자는 가로로 스크롤하기 시작하고 서버는 주기적으로 무작위로 주가 변동을 방송하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="72b42-341">주가가 매번 변경될 때마다 앱은 **라이브 스톡 테이블과** **라이브 스톡 시세를**모두 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="72b42-342">주식의 가격 변화가 긍정적이면 앱은 녹색 배경의 주식을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="72b42-343">변경이 음수이면 앱에 빨간색 배경이 있는 주식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="72b42-344">**시장 닫기**선택.</span><span class="sxs-lookup"><span data-stu-id="72b42-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="72b42-345">테이블 업데이트가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-345">The table updates stop.</span></span>

    * <span data-ttu-id="72b42-346">시세 차면 스크롤이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="72b42-347">**재설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-347">Select **Reset**.</span></span>

    * <span data-ttu-id="72b42-348">모든 재고 데이터가 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-348">All stock data is reset.</span></span>

    * <span data-ttu-id="72b42-349">가격 변경이 시작되기 전에 앱이 초기 상태를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="72b42-350">브라우저에서 URL을 복사하고 다른 두 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="72b42-351">각 브라우저에서 동일한 데이터가 동시에 동적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="72b42-352">컨트롤을 선택하면 모든 브라우저가 동시에 동일한 방식으로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="72b42-353">라이브 스톡 티커 디스플레이</span><span class="sxs-lookup"><span data-stu-id="72b42-353">Live Stock Ticker display</span></span>

<span data-ttu-id="72b42-354">**라이브 스톡 티커** 디스플레이는 CSS `<div>` 스타일에 의해 한 줄로 포맷된 요소의 정렬되지 않은 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="72b42-355">앱은 `<li>` 템플릿 문자열의 자리 표시자를 대체하고 `<li>` `<ul>` 요소를 동적으로 추가하여 테이블과 동일한 방식으로 티커를 초기화하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="72b42-356">응용 프로그램은 에서 정렬되지 않은 `animate` 목록의 여백 왼쪽을 변경하려면 jQuery 함수를 사용하여 스크롤을 포함합니다. `<div>`</span><span class="sxs-lookup"><span data-stu-id="72b42-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="72b42-357">시그널R.샘플 스톡티커.html</span><span class="sxs-lookup"><span data-stu-id="72b42-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="72b42-358">주식 시세 HTML 코드 :</span><span class="sxs-lookup"><span data-stu-id="72b42-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="72b42-359">시그널R.샘플 스톡티커.css</span><span class="sxs-lookup"><span data-stu-id="72b42-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="72b42-360">주식 시세 CSS 코드 :</span><span class="sxs-lookup"><span data-stu-id="72b42-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="72b42-361">시그널R.샘플 시그널R.스톡티커.js</span><span class="sxs-lookup"><span data-stu-id="72b42-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="72b42-362">스크롤할 수 있는 jQuery 코드는 다음과 같은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="72b42-363">클라이언트가 호출할 수 있는 서버의 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="72b42-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="72b42-364">앱에 유연성을 추가하려면 앱에서 호출할 수 있는 추가 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="72b42-365">시그널R.샘플 StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="72b42-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="72b42-366">클래스는 `StockTickerHub` 클라이언트가 호출할 수 있는 네 가지 추가 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="72b42-367">앱은 `OpenMarket`페이지 `CloseMarket`상단의 단추에 대한 응답으로 를 `Reset` 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="72b42-368">한 클라이언트가 모든 클라이언트에 즉시 전파되는 상태의 변경을 트리거하는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="72b42-369">이러한 각 메서드는 시장 `StockTicker` 상태 변경을 일으키는 클래스의 메서드를 호출한 다음 새 상태를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="72b42-370">시그널R.샘플 StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="72b42-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="72b42-371">`StockTicker` 클래스에서 앱은 `MarketState` 열거형 값을 반환하는 `MarketState` 속성으로 시장 상태를 유지관리합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="72b42-372">`StockTicker` 시장 상태를 변경하는 각 메서드는 클래스가 스레드로 안전해야 하기 때문에 잠금 블록 내에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="72b42-373">이 코드가 스레드에서 안전한지 확인하려면 지정된 `_marketState` `MarketState` `volatile`속성을 백업하는 필드:</span><span class="sxs-lookup"><span data-stu-id="72b42-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="72b42-374">`BroadcastMarketStateChange` 및 `BroadcastMarketReset` 메서드는 클라이언트에서 정의된 다른 메서드를 호출하는 것을 제외하고 이미 본 BroadcastStockPrice 메서드와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="72b42-375">서버가 호출할 수 있는 클라이언트의 추가 기능</span><span class="sxs-lookup"><span data-stu-id="72b42-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="72b42-376">이제 `updateStockPrice` 이 함수는 테이블과 티커 디스플레이를 모두 `jQuery.Color` 처리하며 빨간색과 녹색으로 깜박이는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="72b42-377">*SignalR.StockTicker.js의* 새로운 기능은 시장 상태에 따라 버튼을 활성화하고 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="72b42-378">또한 라이브 스톡 **시세** 수평 스크롤을 중지하거나 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="72b42-379">많은 함수가 추가되고 `ticker.client`있기 때문에 앱은 [jQuery 확장 함수를](http://api.jquery.com/jQuery.extend/) 사용하여 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="72b42-380">연결을 설정한 후 추가 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="72b42-381">클라이언트가 연결을 설정한 후 수행할 몇 가지 추가 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="72b42-382">시장이 열려 있거나 닫혀 있는지 확인하여 `marketOpened` `marketClosed` 적절한 기능을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="72b42-383">서버 메서드 호출을 단추에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="72b42-384">앱이 연결을 설정할 때까지 서버 메서드는 단추에 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="72b42-385">따라서 코드에서 서버 메서드를 사용할 수 있게 되기 전에 서버 메서드를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72b42-386">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="72b42-386">Additional resources</span></span>

<span data-ttu-id="72b42-387">이 자습서에서는 서버에서 연결된 모든 클라이언트로 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="72b42-388">이제 모든 클라이언트의 알림에 대한 응답으로 정기적으로 메시지를 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="72b42-389">다중 스레드 싱글톤 인스턴스의 개념을 사용하여 다중 플레이어 온라인 게임 시나리오에서 서버 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="72b42-390">예를 들어 [SignalR을 기반으로 하는 ShootR 게임을](https://github.com/NTaylorMullen/ShootR)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="72b42-391">피어 투 피어 통신 시나리오를 보여 주는 자습서의 경우 SignalR 및 [SignalR로 실시간](tutorial-high-frequency-realtime-with-signalr.md) [업데이트시작](introduction-to-signalr.md) 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="72b42-392">SignalR에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="72b42-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="72b42-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="72b42-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="72b42-394">시그널R 프로젝트</span><span class="sxs-lookup"><span data-stu-id="72b42-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="72b42-395">시그널R GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="72b42-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="72b42-396">시그널러 위키</span><span class="sxs-lookup"><span data-stu-id="72b42-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="72b42-397">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72b42-397">Next steps</span></span>

<span data-ttu-id="72b42-398">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72b42-399">프로젝트 생성</span><span class="sxs-lookup"><span data-stu-id="72b42-399">Created the project</span></span>
> * <span data-ttu-id="72b42-400">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-400">Set up the server code</span></span>
> * <span data-ttu-id="72b42-401">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-401">Examined the server code</span></span>
> * <span data-ttu-id="72b42-402">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="72b42-402">Set up the client code</span></span>
> * <span data-ttu-id="72b42-403">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="72b42-403">Examined the client code</span></span>
> * <span data-ttu-id="72b42-404">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="72b42-404">Tested the application</span></span>
> * <span data-ttu-id="72b42-405">사용 가능한 로깅</span><span class="sxs-lookup"><span data-stu-id="72b42-405">Enabled logging</span></span>

<span data-ttu-id="72b42-406">다음 문서로 이동하여 ASP.NET SignalR 2를 사용하는 실시간 웹 응용 프로그램을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72b42-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="72b42-407">SignalR로 실시간 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="72b42-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
