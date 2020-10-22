---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345600"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="b4325-103">자습서: SignalR 2를 사용 하 여 서버 브로드캐스트</span><span class="sxs-lookup"><span data-stu-id="b4325-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b4325-104">이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="b4325-105">서버 브로드캐스트는 서버에서 클라이언트로 전송 되는 통신을 시작 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="b4325-106">이 자습서에서 만들 응용 프로그램은 서버 브로드캐스트 기능을 위한 일반적인 시나리오인 주식 시세 표시기를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="b4325-107">정기적으로 서버는 주식 가격을 임의로 업데이트 하 고 연결 된 모든 클라이언트에 업데이트를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="b4325-108">브라우저에서 **변경** 및 열의 숫자 및 기호는 **%** 서버의 알림에 대 한 응답으로 동적으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="b4325-109">동일한 URL에 대 한 추가 브라우저를 열 경우 모두 동일한 데이터 및 동일한 데이터 변경 내용을 동시에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="b4325-111">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4325-112">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-112">Create the project</span></span>
> * <span data-ttu-id="b4325-113">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-113">Set up the server code</span></span>
> * <span data-ttu-id="b4325-114">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="b4325-114">Examine the server code</span></span>
> * <span data-ttu-id="b4325-115">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-115">Set up the client code</span></span>
> * <span data-ttu-id="b4325-116">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="b4325-116">Examine the client code</span></span>
> * <span data-ttu-id="b4325-117">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="b4325-117">Test the application</span></span>
> * <span data-ttu-id="b4325-118">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="b4325-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4325-119">응용 프로그램을 빌드하는 단계를 수행 하지 않으려면 비어 있는 새 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR 패키지를 설치 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="b4325-120">이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하는 경우 *readme.txt* 파일의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="b4325-121">패키지를 실행 하려면 설치 된 패키지에서 메서드를 호출 하는 OWIN startup 클래스를 추가 해야 `ConfigureSignalR` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="b4325-122">OWIN startup 클래스를 추가 하지 않으면 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="b4325-123">이 문서의 [StockTicker 샘플 설치](#install-the-stockticker-sample) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4325-124">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b4325-124">Prerequisites</span></span>

* <span data-ttu-id="b4325-125">**ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b4325-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="b4325-126">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-126">Create the project</span></span>

<span data-ttu-id="b4325-127">이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="b4325-128">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="b4325-130">**새 ASP.NET 웹 응용 프로그램-SignalR. StockTicker** 창에서 선택 된 **상태로 두고** **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="b4325-131">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-131">Set up the server code</span></span>

<span data-ttu-id="b4325-132">이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="b4325-133">스톡 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-133">Create the Stock class</span></span>

<span data-ttu-id="b4325-134">먼저 주식 정보를 저장 하 고 전송 하는 데 사용할 *스톡* 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="b4325-135">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **클래스**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b4325-136">클래스 이름을 *스톡* 으로 만들고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="b4325-137">*Stock.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="b4325-138">주식을 만들 때 설정 하는 두 가지 속성은 `Symbol` (예: MSFT For Microsoft) 및 `Price` 입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="b4325-139">다른 속성은 설정 하는 방법과 시기에 따라 달라 집니다 `Price` .</span><span class="sxs-lookup"><span data-stu-id="b4325-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="b4325-140">처음 설정 하는 경우 `Price` 값이로 전파 `DayOpen` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="b4325-141">그런 다음를 설정 하면 `Price` 앱에서 `Change` 와의 `PercentChange` 차이에 따라 및 속성 값을 계산 합니다 `Price` `DayOpen` .</span><span class="sxs-lookup"><span data-stu-id="b4325-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="b4325-142">StockTickerHub 및 StockTicker 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="b4325-143">SignalR Hub API를 사용 하 여 서버와 클라이언트 간의 상호 작용을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="b4325-144">`StockTickerHub`SignalR 클래스에서 파생 되는 클래스는 `Hub` 클라이언트의 수신 연결 및 메서드 호출을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="b4325-145">또한 주식 데이터를 유지 관리 하 고 개체를 실행 해야 `Timer` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="b4325-146">`Timer`개체는 클라이언트 연결과 무관 하 게 가격 업데이트를 주기적으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="b4325-147">허브가 일시적 이기 때문에 클래스에 이러한 함수를 배치할 수 없습니다 `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b4325-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="b4325-148">앱은 `Hub` 클라이언트에서 서버로의 연결과 같은 허브의 각 태스크에 대 한 클래스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="b4325-149">따라서 주식 데이터를 유지 하 고, 가격을 업데이트 하 고, 가격 업데이트를 브로드캐스팅하는 메커니즘이 별도의 클래스에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="b4325-150">클래스의 이름을로 `StockTicker` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-150">You'll name the class `StockTicker`.</span></span>

![StockTicker에서 브로드캐스팅](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="b4325-152">클래스의 인스턴스 하나를 서버에서 실행 하려는 경우에만 `StockTicker` 각 인스턴스에서 singleton 인스턴스로 참조를 설정 해야 `StockTickerHub` `StockTicker` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="b4325-153">`StockTicker`클래스는 스톡 데이터를 포함 하 고 업데이트를 트리거 하지만 클래스가 아니라 클라이언트에 브로드캐스트합니다 `StockTicker` `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b4325-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="b4325-154">`StockTicker`클래스는 SignalR Hub 연결 컨텍스트 개체에 대 한 참조를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="b4325-155">그런 다음 SignalR 연결 컨텍스트 개체를 사용 하 여 클라이언트에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="b4325-156">StockTickerHub.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="b4325-157">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **새 항목**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b4325-158">**새 항목 추가-SignalR. StockTicker**에서 **설치 됨**  >  **Visual c #**  >  **웹**  >  **SignalR** 를 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="b4325-159">클래스 이름을 *StockTickerHub* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="b4325-160">이 단계에서는 *StockTickerHub.cs* 클래스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="b4325-161">동시에 SignalR를 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="b4325-162">*StockTickerHub.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="b4325-163">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-163">Save the file.</span></span>

<span data-ttu-id="b4325-164">앱은 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스를 사용 하 여 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="b4325-165">메서드 하나를 정의 하 고 있습니다 `GetAllStocks()` .</span><span class="sxs-lookup"><span data-stu-id="b4325-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="b4325-166">클라이언트는 처음 서버에 연결할 때이 메서드를 호출 하 여 현재 가격으로 모든 주식의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="b4325-167">메서드는 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문에 동기적으로 실행 하 고 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="b4325-168">데이터베이스 조회 나 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 하 여 메서드가 데이터를 가져와야 하는 경우 `Task<IEnumerable<Stock>>` 에는를 반환 값으로 지정 하 여 비동기 처리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="b4325-169">자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="b4325-170">`HubName`특성은 앱이 클라이언트의 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="b4325-171">클라이언트의 기본 이름은이 특성을 사용 하지 않는 경우 클래스 이름의 camelCase 버전입니다 .이 경우에는 `stockTickerHub` 입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="b4325-172">나중에 클래스를 만들 때 `StockTicker` 앱은 정적 속성에 해당 클래스의 단일 인스턴스를 만듭니다 `Instance` .</span><span class="sxs-lookup"><span data-stu-id="b4325-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="b4325-173">의 singleton 인스턴스는 `StockTicker` 연결 하거나 연결을 끊는 클라이언트 수에 관계 없이 메모리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="b4325-174">이 인스턴스는 `GetAllStocks()` 메서드가 현재 주식 정보를 반환 하는 데 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="b4325-175">StockTicker.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="b4325-176">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **클래스**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b4325-177">클래스 이름을 *StockTicker* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="b4325-178">*StockTicker.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="b4325-179">모든 스레드가 동일한 StockTicker 코드 인스턴스를 실행 하므로 StockTicker 클래스는 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="b4325-180">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="b4325-180">Examine the server code</span></span>

<span data-ttu-id="b4325-181">서버 코드를 살펴보면 앱이 작동 하는 방식을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="b4325-182">단일 인스턴스를 정적 필드에 저장</span><span class="sxs-lookup"><span data-stu-id="b4325-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="b4325-183">코드는 `_instance` `Instance` 클래스의 인스턴스를 사용 하 여 속성을 백업 하는 정적 필드를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="b4325-184">생성자는 전용 이므로 앱에서 만들 수 있는 클래스의 유일한 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="b4325-185">앱은 필드에 [초기화 지연을](/dotnet/framework/performance/lazy-initialization) 사용 합니다 `_instance` .</span><span class="sxs-lookup"><span data-stu-id="b4325-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="b4325-186">성능상의 이유로는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-186">It's not for performance reasons.</span></span> <span data-ttu-id="b4325-187">인스턴스를 만드는 것은 스레드로부터 안전한 지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="b4325-188">클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행 되는 StockTickerHub 클래스의 새 인스턴스는 `StockTicker.Instance` 이전에 클래스에서 살펴본 것 처럼 정적 속성에서 StockTicker singleton 인스턴스를 가져옵니다 `StockTickerHub` .</span><span class="sxs-lookup"><span data-stu-id="b4325-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="b4325-189">ConcurrentDictionary에 주식 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="b4325-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="b4325-190">생성자는 `_stocks` 일부 샘플 재고 데이터를 사용 하 여 컬렉션을 초기화 하 고 `GetAllStocks` 주식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="b4325-191">앞에서 살펴본 것 처럼이 주식 컬렉션은 `StockTickerHub.GetAllStocks` `Hub` 클라이언트가 호출할 수 있는 클래스의 서버 메서드인에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="b4325-192">스톡 컬렉션은 스레드 보안을 위해 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 형식으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="b4325-193">또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용 하 고 변경할 때 사전을 명시적으로 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="b4325-194">이 샘플 응용 프로그램의 경우 응용 프로그램 데이터를 메모리에 저장 하 고 앱이 인스턴스를 삭제할 때 데이터를 잃지는 것이 좋습니다  `StockTicker` .</span><span class="sxs-lookup"><span data-stu-id="b4325-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="b4325-195">실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="b4325-196">정기적으로 주식 가격 업데이트</span><span class="sxs-lookup"><span data-stu-id="b4325-196">Periodically updating stock prices</span></span>

<span data-ttu-id="b4325-197">생성자는 `Timer` 임의 기준으로 주식 가격을 업데이트 하는 메서드를 주기적으로 호출 하는 개체를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="b4325-198">`Timer``UpdateStockPrices`상태 매개 변수에 null을 전달 하는를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="b4325-199">앱은 가격을 업데이트 하기 전에 개체에 대 한 잠금을 사용 `_updateStockPricesLock` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="b4325-200">코드는 다른 스레드가 이미 가격을 업데이트 하 고 있는지 확인 한 다음 `TryUpdateStockPrice` 목록의 각 재고에 대해를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="b4325-201">`TryUpdateStockPrice`메서드는 주식 가격을 변경할 것인지 여부와 변경 되는 정도를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="b4325-202">주가 변경 되 면 앱은 `BroadcastStockPrice` 를 호출 하 여 주식 가격 변경을 모든 연결 된 클라이언트에 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="b4325-203">`_updatingStockPrices` [일시적](https://msdn.microsoft.com/library/x13ttww7.aspx) 으로 지정 된 플래그는 스레드로부터 안전 하 게 보호 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="b4325-204">실제 응용 프로그램에서 메서드는 `TryUpdateStockPrice` 웹 서비스를 호출 하 여 가격을 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="b4325-205">이 코드에서 앱은 난수 생성기를 사용 하 여 임의로 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="b4325-206">StockTicker 클래스가 클라이언트에 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4325-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="b4325-207">여기서는 가격 변경이 개체에서 발생 하기 때문에 `StockTicker` `updateStockPrice` 연결 된 모든 클라이언트에서 메서드를 호출 해야 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="b4325-208">클래스에는 `Hub` 클라이언트 메서드를 호출 하기 위한 API가 있지만 `StockTicker` 클래스에서 파생 되지 않고 개체에 대 한 `Hub` 참조가 없습니다 `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b4325-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="b4325-209">연결 된 클라이언트에 브로드캐스트하려면 클래스는 `StockTicker` 클래스에 대 한 SignalR context 인스턴스를 가져온 `StockTickerHub` 다음이를 사용 하 여 클라이언트에서 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="b4325-210">이 코드는 singleton 클래스 인스턴스를 만들고 해당 참조를 생성자에 전달 하 고 생성자가이를 속성에 배치 하는 경우 SignalR 컨텍스트에 대 한 참조를 가져옵니다 `Clients` .</span><span class="sxs-lookup"><span data-stu-id="b4325-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="b4325-211">컨텍스트를 한 번만 가져오려고 하는 두 가지 이유는 다음과 같습니다. 컨텍스트 가져오기 작업은 비용이 많이 들고, 한 번 가져오면 앱이 클라이언트에 전송 되는 메시지의 순서를 유지 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="b4325-212">`Clients`컨텍스트의 속성을 가져와서 속성에 배치 `StockTickerClient` 하면 클래스에서와 동일 하 게 보이는 클라이언트 메서드를 호출 하는 코드를 작성할 수 있습니다 `Hub` .</span><span class="sxs-lookup"><span data-stu-id="b4325-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="b4325-213">예를 들어, 작성할 수 있는 모든 클라이언트에 브로드캐스트할 수 있습니다 `Clients.All.updateStockPrice(stock)` .</span><span class="sxs-lookup"><span data-stu-id="b4325-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="b4325-214">`updateStockPrice`에서 호출 하는 메서드가 `BroadcastStockPrice` 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="b4325-215">나중에 클라이언트에서 실행 되는 코드를 작성할 때 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="b4325-216">`updateStockPrice`가 동적 이므로이를 참조할 수 있습니다 `Clients.All` . 즉, 앱이 런타임에 식을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="b4325-217">이 메서드 호출이 실행 되 면 SignalR는 메서드 이름과 매개 변수 값을 클라이언트에 보내고, 클라이언트에 라는 메서드가 있으면 `updateStockPrice` 앱은 해당 메서드를 호출 하 고 매개 변수 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="b4325-218">`Clients.All` 모든 클라이언트에 보내기를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="b4325-219">SignalR는 보낼 클라이언트 또는 클라이언트 그룹을 지정 하는 다른 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="b4325-220">자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="b4325-221">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="b4325-221">Register the SignalR route</span></span>

<span data-ttu-id="b4325-222">서버에서 가로채서 SignalR에 지시할 URL을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="b4325-223">이렇게 하려면 OWIN startup 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="b4325-224">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **새 항목**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b4325-225">**새 항목 추가-SignalR. StockTicker** 에서 **설치 된**  >  **Visual c #**  >  **웹** 을 선택 하 고 **OWIN 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="b4325-226">클래스 이름을 *시작* 으로 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="b4325-227">*Startup.cs* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="b4325-228">이제 서버 코드를 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="b4325-229">다음 섹션에서는 클라이언트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="b4325-230">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-230">Set up the client code</span></span>

<span data-ttu-id="b4325-231">이 섹션에서는 클라이언트에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="b4325-232">HTML 페이지 및 JavaScript 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="b4325-233">HTML 페이지에 데이터가 표시 되 고 JavaScript 파일이 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="b4325-234">StockTicker.html 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-234">Create StockTicker.html</span></span>

<span data-ttu-id="b4325-235">먼저 HTML 클라이언트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="b4325-236">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **HTML 페이지**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="b4325-237">파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b4325-238">*StockTicker.html* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="b4325-239">HTML은 5 개의 열, 머리글 행 및 5 개 열 전체에 걸쳐 있는 단일 셀을 포함 하는 데이터 행을 포함 하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="b4325-240">데이터 행에 "로드 중 ..."이 표시 됩니다. 앱이 시작 되는 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="b4325-241">JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 된 주식 데이터를 사용 하 여 해당 행을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="b4325-242">스크립트 태그는 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-242">The script tags specify:</span></span>

    * <span data-ttu-id="b4325-243">JQuery 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-243">The jQuery script file.</span></span>

    * <span data-ttu-id="b4325-244">SignalR core 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="b4325-245">SignalR 프록시 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="b4325-246">나중에 만들 StockTicker 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="b4325-247">앱은 SignalR 프록시 스크립트 파일을 동적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="b4325-248">"/Signalr/hubs" URL을 지정 하 고 허브 클래스 (이 경우)의 메서드에 대 한 프록시 메서드를 정의 `StockTickerHub.GetAllStocks` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="b4325-249">원한다 면 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)를 사용 하 여이 JavaScript 파일을 수동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="b4325-250">메서드 호출에서 동적 파일 생성을 사용 하지 않도록 설정 하는 것을 잊지 마세요 `MapHubs` .</span><span class="sxs-lookup"><span data-stu-id="b4325-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="b4325-251">**솔루션 탐색기**에서 **스크립트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="b4325-252">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b4325-253">패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="b4325-254">프로젝트의 스크립트 파일 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="b4325-255">**솔루션 탐색기**에서 *StockTicker.html*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="b4325-256">StockTicker.js 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-256">Create StockTicker.js</span></span>

<span data-ttu-id="b4325-257">이제 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="b4325-258">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **JavaScript 파일**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="b4325-259">파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b4325-260">*StockTicker.js* 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="b4325-261">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="b4325-261">Examine the client code</span></span>

<span data-ttu-id="b4325-262">클라이언트 코드를 살펴보면 클라이언트 코드가 서버 코드와 상호 작용 하 여 앱이 작동 하도록 하는 방법을 배우는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="b4325-263">연결 시작</span><span class="sxs-lookup"><span data-stu-id="b4325-263">Starting the connection</span></span>

<span data-ttu-id="b4325-264">`$.connection` SignalR 프록시를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="b4325-265">이 코드는 클래스의 프록시에 대 한 참조를 가져와 `StockTickerHub` `ticker` 변수에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="b4325-266">프록시 이름은 특성에 의해 설정 된 이름입니다 `HubName` .</span><span class="sxs-lookup"><span data-stu-id="b4325-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="b4325-267">모든 변수 및 함수를 정의한 후 파일의 마지막 코드 줄은 SignalR 함수를 호출 하 여 SignalR 연결을 초기화 합니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="b4325-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="b4325-268">`start`함수는 비동기적으로 실행 되 고 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="b4325-269">Done 함수를 호출 하 여 앱이 비동기 작업을 완료할 때 호출할 함수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="b4325-270">모든 주식 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4325-270">Getting all the stocks</span></span>

<span data-ttu-id="b4325-271">`init`함수는 `getAllStocks` 서버에서 함수를 호출 하 고 서버에서 반환 하는 정보를 사용 하 여 스톡 테이블을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="b4325-272">서버에서 메서드 이름이 파스칼식 대/소문자를 사용 하는 경우에도 기본적으로 클라이언트에서 camelCasing를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="b4325-273">CamelCasing 규칙은 개체가 아닌 메서드에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="b4325-274">예를 들어, 또는가 `stock.Symbol` 아닌 and를 참조 `stock.Price` `stock.symbol` `stock.price` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="b4325-275">`init`메서드에서 응용 프로그램은를 호출 하 여 `formatStock` 개체의 속성 형식을 지정 하 `stock` 고,를 호출 하 여 `supplant` 변수의 자리 표시자를 `rowTemplate` `stock` 개체 속성 값으로 대체 하는 방식으로 서버에서 받은 각 스톡 개체의 테이블 행에 대 한 HTML을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="b4325-276">그러면 결과 HTML이 스톡 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="b4325-277">`init` `callback` 비동기 함수가 완료 된 후 실행 되는 함수로에 전달 하 여를 호출 `start` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="b4325-278">`init`를 호출한 후 별도의 JavaScript 문으로 호출한 경우 `start` 함수는 시작 함수가 연결 설정을 완료할 때까지 기다리지 않고 즉시 실행 되기 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="b4325-279">이 경우 `init` 함수는 `getAllStocks` 앱이 서버 연결을 설정 하기 전에 함수를 호출 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="b4325-280">업데이트 된 주식 가격</span><span class="sxs-lookup"><span data-stu-id="b4325-280">Getting updated stock prices</span></span>

<span data-ttu-id="b4325-281">서버에서 주식 시세를 변경 하면 연결 된 클라이언트에서를 호출 합니다 `updateStockPrice` .</span><span class="sxs-lookup"><span data-stu-id="b4325-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="b4325-282">앱은 `stockTicker` 서버에서 호출할 수 있도록 프록시의 client 속성에 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="b4325-283">`updateStockPrice`함수는 함수에서와 동일한 방법으로 서버에서 받은 스톡 개체의 형식을 테이블 행으로 지정 합니다 `init` .</span><span class="sxs-lookup"><span data-stu-id="b4325-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="b4325-284">테이블에 행을 추가 하는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="b4325-285">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="b4325-285">Test the application</span></span>

<span data-ttu-id="b4325-286">앱이 작동 하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="b4325-287">모든 브라우저 창에서 주식 가격이 변동 인 라이브 재고 테이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="b4325-288">도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![디버깅 모드를 켜고 재생을 선택 하는 사용자의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="b4325-290">**라이브 재고 테이블**을 표시 하는 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="b4325-291">Stock 테이블에는 처음에 "로드 중 ..."이 표시 됩니다. 그런 다음, 짧은 시간 후에 앱은 초기 주식 데이터를 표시 한 다음 주가 변경 되기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="b4325-292">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="b4325-293">초기 주식 표시는 첫 번째 브라우저와 동일 하며 변경 내용이 동시에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="b4325-294">모든 브라우저를 닫고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="b4325-295">StockTicker singleton 개체가 서버에서 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="b4325-296">**라이브 스톡 테이블** 은 주가 계속 변경 된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="b4325-297">변경 수치가 0 인 초기 테이블은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="b4325-298">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="b4325-299">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="b4325-299">Enable logging</span></span>

<span data-ttu-id="b4325-300">SignalR에는 문제 해결을 지원 하기 위해 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="b4325-301">이 섹션에서는 로깅을 사용 하도록 설정 하 고 SignalR에서 사용 하는 전송 방법에 대 한 로그를 표시 하는 예제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="b4325-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket)-IIS 8 및 현재 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="b4325-303">Internet Explorer 이외의 브라우저에서 지원 되는 [서버에서 보낸 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)</span><span class="sxs-lookup"><span data-stu-id="b4325-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="b4325-304">[영구적 프레임](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)으로, Internet Explorer에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="b4325-305">모든 브라우저에서 지원 되는 [Ajax 긴 폴링](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).</span><span class="sxs-lookup"><span data-stu-id="b4325-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="b4325-306">SignalR는 지정 된 모든 연결에 대해 서버와 클라이언트가 지 원하는 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="b4325-307">*StockTicker.js*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="b4325-308">이 강조 표시 된 코드 줄을 추가 하 여 파일 끝에서 연결을 초기화 하는 코드 바로 앞에서 로깅을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="b4325-309">**F5** 키를 눌러 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="b4325-310">브라우저의 개발자 도구 창을 열고 콘솔을 선택 하 여 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="b4325-311">새 연결에 대 한 전송 방법을 협상 하는 SignalR의 로그를 확인 하려면 페이지를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="b4325-312">Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **websocket**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="b4325-313">Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **iframe**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="b4325-314">Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 **websocket**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="b4325-315">Firefox에서 Firebug 추가 기능을 설치 하 여 콘솔 창을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="b4325-316">Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 서버에서 **보낸** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="b4325-317">StockTicker 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="b4325-317">Install the StockTicker sample</span></span>

<span data-ttu-id="b4325-318">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 는 StockTicker 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="b4325-319">NuGet 패키지에는 처음부터 만든 단순화 된 버전 보다 더 많은 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="b4325-320">자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새 기능 및이를 구현 하는 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4325-321">이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우 프로젝트에 OWIN startup 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="b4325-322">NuGet 패키지에 대 한이 readme.txt 파일에서는이 단계에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="b4325-323">SignalR NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="b4325-324">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="b4325-325">**NuGet 패키지 관리자: SignalR. StockTicker**에서 **찾아보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="b4325-326">**패키지 원본**에서 **nuget.org**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="b4325-327">검색 상자에 *SignalR* 를 입력 하 고 **SignalR**  >  **설치**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="b4325-328">**솔루션 탐색기**에서 *SignalR* 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="b4325-329">SignalR 패키지를 설치 하면 폴더와 해당 내용이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="b4325-330">*SignalR* 폴더에서 *StockTicker.html*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4325-331">SignalR NuGet 패키지를 설치 하면 *Scripts* 폴더에 있는 jQuery 버전이 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="b4325-332">패키지가 *SignalR* 폴더에 설치 하는 새 *StockTicker.html* 파일은 패키지가 설치 하는 jQuery 버전과 동기화 되지만 원래 *StockTicker.html* 파일을 다시 실행 하려는 경우 먼저 스크립트 태그에서 jquery 참조를 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b4325-333">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="b4325-333">Run the application</span></span>

 <span data-ttu-id="b4325-334">첫 번째 앱에서 살펴본 테이블에는 유용한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="b4325-335">전체 주식 시세 응용 프로그램에는 새 기능이 표시 됩니다. 가로 스크롤 창에서는 주식 데이터 및 주식으로 색을 변경 하는 주가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="b4325-336">**F5** 키를 눌러 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="b4325-337">앱을 처음으로 실행 하는 경우 "market"은 "닫힘" 이며, 스크롤하지 않는 정적 테이블과 표시기 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="b4325-338">**시장 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-338">Select **Open Market**.</span></span>

    ![라이브 표시기의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="b4325-340">**라이브 주식 시세 표시기** 상자를 가로로 스크롤하면 서버에서 정기적으로 주식 시세 변경을 정기적으로 브로드캐스트 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="b4325-341">주가 변경 될 때마다 앱은 **Live Stock 테이블과** **라이브 주식 시세 표시기**를 모두 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="b4325-342">주가 변화 하는 경우 앱은 녹색 배경의 재고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="b4325-343">변경이 음수 이면 앱은 빨간색 배경의 재고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="b4325-344">**시장 종결**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="b4325-345">테이블 업데이트가 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-345">The table updates stop.</span></span>

    * <span data-ttu-id="b4325-346">표시기가 스크롤을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="b4325-347">**재설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-347">Select **Reset**.</span></span>

    * <span data-ttu-id="b4325-348">모든 재고 데이터를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-348">All stock data is reset.</span></span>

    * <span data-ttu-id="b4325-349">앱은 가격 변경이 시작 되기 전에 초기 상태를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="b4325-350">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="b4325-351">각 브라우저에서 동시에 동일한 데이터를 동적으로 업데이트 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="b4325-352">컨트롤 중 하나를 선택 하면 모든 브라우저가 동시에 동일한 방식으로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="b4325-353">라이브 주식 종목 표시</span><span class="sxs-lookup"><span data-stu-id="b4325-353">Live Stock Ticker display</span></span>

<span data-ttu-id="b4325-354">**라이브 주식 시세** 표시는 `<div>` CSS 스타일로 한 줄로 서식 지정 된 요소에서 순서가 지정 되지 않은 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="b4325-355">앱은 템플릿 문자열에서 자리 표시자를 대체 `<li>` 하 고 요소를 `<li>` 요소에 동적으로 추가 하 여 테이블과 동일한 방식으로 종목을 초기화 하 고 업데이트 합니다. `<ul>`</span><span class="sxs-lookup"><span data-stu-id="b4325-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="b4325-356">앱은 jQuery 함수를 사용 하 여에서 순서가 지정 되지 않은 `animate` 목록의 왼쪽 여백을 변경 하는 스크롤을 포함 합니다 `<div>` .</span><span class="sxs-lookup"><span data-stu-id="b4325-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="b4325-357">SignalR StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="b4325-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="b4325-358">주식 시세 HTML 코드:</span><span class="sxs-lookup"><span data-stu-id="b4325-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="b4325-359">SignalR StockTicker</span><span class="sxs-lookup"><span data-stu-id="b4325-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="b4325-360">주식 시세 CSS 코드:</span><span class="sxs-lookup"><span data-stu-id="b4325-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="b4325-361">SignalR SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="b4325-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="b4325-362">스크롤할 수 있도록 하는 jQuery 코드:</span><span class="sxs-lookup"><span data-stu-id="b4325-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="b4325-363">클라이언트에서 호출할 수 있는 서버에 대 한 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="b4325-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="b4325-364">앱에 유연성을 추가 하기 위해 앱에서 호출할 수 있는 추가 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="b4325-365">SignalR StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="b4325-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="b4325-366">`StockTickerHub`클래스는 클라이언트에서 호출할 수 있는 다음 네 가지 메서드를 추가로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="b4325-367">앱은 `OpenMarket` `CloseMarket` `Reset` 페이지 맨 위에 있는 단추에 대 한 응답으로, 및를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="b4325-368">모든 클라이언트에 즉시 전파 되는 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="b4325-369">이러한 각 메서드는 `StockTicker` 시장 상태를 변경 하 고 새 상태를 브로드캐스팅하는 클래스의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="b4325-370">SignalR StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="b4325-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="b4325-371">클래스에서 `StockTicker` 앱은 `MarketState` 열거형 값을 반환 하는 속성을 사용 하 여 시장의 상태를 유지 관리 합니다 `MarketState` .</span><span class="sxs-lookup"><span data-stu-id="b4325-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="b4325-372">`StockTicker`클래스를 스레드로부터 안전 하 게 보호 해야 하므로 시장 상태를 변경 하는 각 메서드는 잠금 블록 내에서이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="b4325-373">이 코드가 스레드로부터 안전 하 게 보호 되도록 하기 위해 `_marketState` 지정 된 속성을 지 원하는 필드는 `MarketState` `volatile` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="b4325-374">`BroadcastMarketStateChange`및 `BroadcastMarketReset` 메서드는 클라이언트에 정의 된 다른 메서드를 호출 하는 것을 제외 하 고 이미 보았던 BroadcastStockPrice 메서드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="b4325-375">서버에서 호출할 수 있는 클라이언트의 추가 함수</span><span class="sxs-lookup"><span data-stu-id="b4325-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="b4325-376">`updateStockPrice`이제 함수는 테이블 및 표시기 표시를 모두 처리 하 고를 사용 하 여 `jQuery.Color` 빨강 및 녹색 색을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="b4325-377">의 새 함수는 시장 상태에 따라 단추를 사용 하거나 사용 하지 않도록 설정 *SignalR.StockTicker.js* 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="b4325-378">또한 **라이브 주식 시세 표시기** 가로 스크롤을 중지 하거나 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="b4325-379">많은 함수가에 추가 되기 때문에 `ticker.client` 앱은 [jQuery extend 함수](http://api.jquery.com/jQuery.extend/) 를 사용 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="b4325-380">연결을 설정한 후 추가 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="b4325-381">클라이언트에서 연결을 설정한 후에는 다음과 같은 몇 가지 추가 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="b4325-382">적절 한 or 함수를 호출 하기 위해 시장이 열려 있는지 또는 닫혀 있는지 확인 `marketOpened` `marketClosed` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="b4325-383">서버 메서드 호출을 단추에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="b4325-384">서버 메서드는 앱이 연결을 설정할 때까지 단추에 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="b4325-385">코드를 사용 하기 전에 서버 메서드를 호출할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4325-386">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b4325-386">Additional resources</span></span>

<span data-ttu-id="b4325-387">이 자습서에서는 서버에서 연결 된 모든 클라이언트로 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="b4325-388">이제 모든 클라이언트의 알림에 대 한 응답으로 메시지를 정기적으로 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="b4325-389">다중 스레드 singleton 인스턴스의 개념을 사용 하 여 다중 플레이어 온라인 게임 시나리오에서 서버 상태를 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="b4325-390">예를 들어 SignalR을 [기반으로 하는 Sho이상 r 게임](https://github.com/NTaylorMullen/ShootR)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="b4325-391">피어 투 피어 통신 시나리오를 보여 주는 자습서는 [SignalR 시작](introduction-to-signalr.md) 하기 및 [SignalR를 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="b4325-392">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4325-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="b4325-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="b4325-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="b4325-394">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="b4325-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="b4325-395">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="b4325-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="b4325-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="b4325-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="b4325-397">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4325-397">Next steps</span></span>

<span data-ttu-id="b4325-398">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4325-399">프로젝트를 만듦</span><span class="sxs-lookup"><span data-stu-id="b4325-399">Created the project</span></span>
> * <span data-ttu-id="b4325-400">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-400">Set up the server code</span></span>
> * <span data-ttu-id="b4325-401">서버 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-401">Examined the server code</span></span>
> * <span data-ttu-id="b4325-402">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="b4325-402">Set up the client code</span></span>
> * <span data-ttu-id="b4325-403">클라이언트 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-403">Examined the client code</span></span>
> * <span data-ttu-id="b4325-404">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="b4325-404">Tested the application</span></span>
> * <span data-ttu-id="b4325-405">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="b4325-405">Enabled logging</span></span>

<span data-ttu-id="b4325-406">ASP.NET SignalR 2를 사용 하는 실시간 웹 응용 프로그램을 만드는 방법에 대해 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4325-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b4325-407">SignalR를 사용 하 여 실시간 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b4325-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
