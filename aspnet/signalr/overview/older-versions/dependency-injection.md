---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR에서 종속성 주입 1.x | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 311976a9d0e79083e02231ab056af3537a3d3d25
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58420805"
---
<a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="81c0b-102">SignalR 1.x에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="81c0b-102">Dependency Injection in SignalR 1.x</span></span>
====================
<span data-ttu-id="81c0b-103">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="81c0b-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="81c0b-104">종속성 주입은 쉽게 (모의 개체를 사용 하 여) 테스트에 대 한 중 하나는 개체의 종속성, 대체 또는 런타임 동작을 변경 하려면 개체 간에 하드 코드 된 종속성을 제거 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="81c0b-105">이 자습서에는 signalr에서 종속성 주입을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="81c0b-106">또한 SignalR을 사용 하 여 IoC 컨테이너를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="81c0b-107">IoC 컨테이너는 종속성 주입을 위한 범용 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="81c0b-108">종속성 주입 이란?</span><span class="sxs-lookup"><span data-stu-id="81c0b-108">What is Dependency Injection?</span></span>

<span data-ttu-id="81c0b-109">종속성 주입을 사용 하 여 이미 익숙한 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="81c0b-110">*종속성 주입* (DI)은 개체 자체 종속성 생성을 담당 하지는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="81c0b-111">DI를 유도 하 여 간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="81c0b-112">메시지를 기록 하는 개체를 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="81c0b-113">로깅 인터페이스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="81c0b-114">개체를 만들 수 있습니다는 `ILogger` 메시지를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="81c0b-115">가장 적합 한 디자인 것만이 방법이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-115">This works, but it's not the best design.</span></span> <span data-ttu-id="81c0b-116">대체 하려는 경우 `FileLogger` 상호 `ILogger` 수정 해야 구현 `SomeComponent`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="81c0b-117">다른 많은 개체가 사용 하는 예 `FileLogger`, 이들 모두를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="81c0b-118">확인 하려는 경우 또는 `FileLogger` 단일 해야 응용 프로그램 전체에서 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="81c0b-119">"삽입" 하는 것이 좋습니다는 `ILogger` 개체로-예를 들어, 생성자 인수를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="81c0b-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="81c0b-120">개체는 선택 하 여 처리 하지 않습니다 이제 `ILogger` 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="81c0b-121">전환할 수 있습니다 `ILogger` 에 종속 된 개체를 변경 하지 않고 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="81c0b-122">이 패턴 이라고 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="81c0b-123">또 다른 패턴은 setter 메서드 또는 속성을 통해 종속성을 설정한 setter 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="81c0b-124">SignalR에서 간단한 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="81c0b-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="81c0b-125">이 자습서에서 채팅 응용 프로그램을 고려해 야 [SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="81c0b-126">해당 응용 프로그램에서 허브 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="81c0b-127">채팅 메시지를 보내기 전에 서버에 저장 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="81c0b-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="81c0b-128">이 기능을 추상화 하는 인터페이스를 정의 하 고 DI를 사용 하 여 인터페이스에 삽입할 수 있습니다는 `ChatHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="81c0b-129">문제는이 SignalR 응용 프로그램을 직접 만들지 않습니다 hubs; SignalR에서이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="81c0b-130">기본적으로 SignalR 허브 클래스에 매개 변수가 없는 생성자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="81c0b-131">그러나 쉽게 허브 인스턴스를 만드는 함수를 등록 하 고 수 DI를 수행 하려면이 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="81c0b-132">함수를 호출 하 여 등록 **GlobalHost.DependencyResolver.Register**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="81c0b-133">사이트를 만드는 데 필요한 때마다 SignalR는이 익명 함수를 호출 하는 이제는 `ChatHub` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="81c0b-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="81c0b-134">IoC 컨테이너</span><span class="sxs-lookup"><span data-stu-id="81c0b-134">IoC Containers</span></span>

<span data-ttu-id="81c0b-135">위의 코드는 간단한 사례에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="81c0b-136">하지만이 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="81c0b-137">많은 종속성이 있는 복잡 한 응용 프로그램에서는이 "연결" 코드를 많이 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="81c0b-138">이 코드는 종속성 중첩 된 경우에 특히을 유지 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="81c0b-139">또한 단위 테스트 하는 것이 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-139">It is also hard to unit test.</span></span>

<span data-ttu-id="81c0b-140">하나의 솔루션 IoC 컨테이너를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="81c0b-141">IoC 컨테이너는 종속성을 관리 하는 일을 담당 하는 소프트웨어 구성 요소입니다. 컨테이너로 형식을 등록 하 고이 정보를 개체를 만드는 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="81c0b-142">컨테이너는 자동으로 종속성 관계를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="81c0b-143">많은 IoC 컨테이너를 사용 하면 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="81c0b-144">"IoC"는 "제어 반전"에 대 한 일반적인 패턴을 설정 하는 프레임 워크 응용 프로그램 코드를 호출 하는 경우이 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="81c0b-145">IoC 컨테이너 생성 개체를 "반전" 컨트롤의 일반적인 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="81c0b-146">SignalR의 IoC 컨테이너 사용</span><span class="sxs-lookup"><span data-stu-id="81c0b-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="81c0b-147">채팅 응용 프로그램 IoC 컨테이너에서 에게도 너무 간단 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="81c0b-148">대신 살펴보겠습니다 합니다 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="81c0b-149">StockTicker 샘플 두 가지 주요 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="81c0b-150">`StockTickerHub`: 클라이언트 연결을 관리 하는 허브 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="81c0b-151">`StockTicker`: 주식 시세를 보유 하 고 정기적으로 새 레코드를 업데이트 하는 단일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="81c0b-152">`StockTickerHub` 에 대 한 참조를 보유 합니다 `StockTicker` singleton을 하는 동안 `StockTicker` 에 대 한 참조를 보유 합니다 **IHubConnectionContext** 에 대 한를 `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="81c0b-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="81c0b-153">이 인터페이스를 사용 하 여 통신할 `StockTickerHub` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="81c0b-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="81c0b-154">(자세한 내용은 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md).)</span><span class="sxs-lookup"><span data-stu-id="81c0b-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="81c0b-155">이러한 종속성을 약간 분리 IoC 컨테이너를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="81c0b-156">먼저 간소화 합니다 `StockTickerHub` 및 `StockTicker` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="81c0b-157">다음 코드에서 필자 했습니다 주석 부분에서는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="81c0b-158">매개 변수가 없는 생성자를 제거 `StockTicker`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="81c0b-159">대신 항상 DI 허브를 만들려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="81c0b-160">StockTicker, singleton 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="81c0b-161">나중에, StockTicker 수명을 제어 하려면 IoC 컨테이너를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="81c0b-162">또한 생성자는 공용 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="81c0b-163">에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다 다음으로, `StockTicker`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="81c0b-164">이 인터페이스 사용 하 여 분리 된 `StockTickerHub` 에서 `StockTicker` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="81c0b-165">Visual Studio를 사용 하면이 종류의 리팩터링 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="81c0b-166">StockTicker.cs 파일을 열고 마우스 오른쪽 단추로 클릭 합니다 `StockTicker` 선택한 클래스 선언인 **리팩터링** ... **인터페이스 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="81c0b-167">에 **인터페이스 추출** 대화 상자에서 클릭 **모두 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="81c0b-168">다른 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-168">Leave the other defaults.</span></span> <span data-ttu-id="81c0b-169">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="81c0b-170">Visual Studio 이라는 새 인터페이스를 만들고 `IStockTicker`, 변경 및 `StockTicker` 에서 파생 `IStockTicker`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="81c0b-171">IStockTicker.cs 파일을 열고 인터페이스를 변경 **공용**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="81c0b-172">에 `StockTickerHub` 클래스의 두 인스턴스를 변경 합니다 `StockTicker` 에 `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="81c0b-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="81c0b-173">만들기는 `IStockTicker` 인터페이스 반드시 필요 하지 않지만 응용 프로그램의 구성 요소 간의 결합을 줄이는 데 DI 유용한 방법을 보여 주려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="81c0b-174">Ninject 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="81c0b-174">Add the Ninject Library</span></span>

<span data-ttu-id="81c0b-175">.NET에 대 한 많은 공개 소스 IoC 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="81c0b-176">이 자습서에서는 사용 하 여 [Ninject](http://www.ninject.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="81c0b-177">(다른 인기 있는 라이브러리 포함 [Castle Windsor](http://www.castleproject.org/)를 [Spring.Net](http://www.springframework.net/)를 [Autofac](https://code.google.com/p/autofac/)를 [Unity](https://github.com/unitycontainer/unity), 및 [StructureMap ](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="81c0b-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="81c0b-178">NuGet 패키지 관리자 설치를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="81c0b-179">Visual Studio에서에서 합니다 **도구가** 메뉴 선택 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="81c0b-180">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="81c0b-181">SignalR 종속성 확인자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="81c0b-182">SignalR 내 Ninject를 사용 하려면에서 파생 된 클래스를 만듭니다 **DefaultDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="81c0b-183">이 클래스는 재정의 **GetService** 하 고 **GetServices** 메서드 **DefaultDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="81c0b-184">SignalR 허브 인스턴스 뿐만 아니라 SignalR에서 내부적으로 사용 하는 다양 한 서비스를 포함 하 여 런타임 시 다양 한 개체를 만들려면 이러한 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="81c0b-185">합니다 **GetService** 메서드 형식의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="81c0b-186">Ninject 커널의 호출 하려면이 메서드를 재정의 **TryGet** 메서드.</span><span class="sxs-lookup"><span data-stu-id="81c0b-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="81c0b-187">해당 메서드가 null을 반환 하는 경우 기본 확인자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="81c0b-188">합니다 **GetServices** 메서드는 지정 된 형식의 개체의 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="81c0b-189">기본 해결 프로그램에서 결과 사용 하 여 Ninject에서 결과 연결 하려면이 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="81c0b-190">Ninject 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="81c0b-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="81c0b-191">이제 형식 바인딩을 선언 하 Ninject 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="81c0b-192">RegisterHubs.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="81c0b-193">에 `RegisterHubs.Start` 메서드를 Ninject 호출 Ninject 컨테이너를 만들어야 합니다 *커널*.</span><span class="sxs-lookup"><span data-stu-id="81c0b-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="81c0b-194">이 사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="81c0b-195">에 대 한 바인딩을 만들 `IStockTicker` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="81c0b-196">이 코드는 두 가지 라는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-196">This code is saying two things.</span></span> <span data-ttu-id="81c0b-197">응용 프로그램에서 필요할 때마다 첫 번째는 `IStockTicker`, 커널의 인스턴스를 만들도록 `StockTicker`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="81c0b-198">두 번째는 `StockTicker` 클래스는 단일 개체로 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="81c0b-199">Ninject 개체의 인스턴스를 하나 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="81c0b-200">에 대 한 바인딩을 만들 **IHubConnectionContext** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="81c0b-201">이 코드를 반환 하는 익명 함수를 만듭니다는 **IHubConnection**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="81c0b-202">합니다 **WhenInjectedInto** 메서드를 만들 때만이 함수를 사용 하려면 Ninject 지시 `IStockTicker` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="81c0b-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="81c0b-203">이유는 SignalR 만들어지는 **IHubConnectionContext** 내부적으로 인스턴스 SignalR을 만드는 방법을 재정의를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="81c0b-204">이 함수에만 적용 됩니다는 `StockTicker` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="81c0b-205">종속성 확인자에 전달 된 **MapHubs** 메서드:</span><span class="sxs-lookup"><span data-stu-id="81c0b-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="81c0b-206">SignalR은에 지정 된 해결 프로그램을 사용 하는 이제 **MapHubs**, 기본 해결 프로그램 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="81c0b-207">전체 코드 목록은 다음과 같습니다 `RegisterHubs.Start`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="81c0b-208">Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 f5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="81c0b-209">브라우저 창에서 이동 `http://localhost:*port*/SignalR.Sample/StockTicker.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="81c0b-210">응용 프로그램에 정확히 동일한 기능을 전 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="81c0b-211">(에 대 한 참조 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md).) 아직 변경 되었습니다. 테스트, 유지 및 발전을 쉽게 코드를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="81c0b-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
