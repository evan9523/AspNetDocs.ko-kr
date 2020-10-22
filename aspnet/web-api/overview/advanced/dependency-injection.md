---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2-ASP.NET 4.x의 종속성 주입
author: MikeWasson
description: 이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API 컨트롤러에 종속성을 삽입 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 3342d93340215d937cf7161ee1c4b32931d516a3
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345263"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="5c28d-103">ASP.NET Web API 2에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="5c28d-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="5c28d-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5c28d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5c28d-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="5c28d-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="5c28d-106">이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 삽입 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5c28d-107">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="5c28d-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5c28d-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="5c28d-108">Web API 2</span></span>
> - [<span data-ttu-id="5c28d-109">Unity 응용 프로그램 블록</span><span class="sxs-lookup"><span data-stu-id="5c28d-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="5c28d-110">Entity Framework 6 (버전 5도 작동 함)</span><span class="sxs-lookup"><span data-stu-id="5c28d-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="5c28d-111">종속성 주입 이란?</span><span class="sxs-lookup"><span data-stu-id="5c28d-111">What is Dependency Injection?</span></span>

<span data-ttu-id="5c28d-112">‘종속성’은 다른 개체에 필요한 모든 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="5c28d-113">예를 들어 데이터 액세스를 처리 하는 [리포지토리](http://martinfowler.com/eaaCatalog/repository.html) 를 정의 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="5c28d-114">예를 들어 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-114">Let's illustrate with an example.</span></span> <span data-ttu-id="5c28d-115">먼저 도메인 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="5c28d-116">다음은 Entity Framework를 사용 하 여 데이터베이스에 항목을 저장 하는 간단한 리포지토리 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="5c28d-117">이제 엔터티에 대 한 GET 요청을 지 원하는 Web API 컨트롤러를 정의 해 보겠습니다 `Product` .</span><span class="sxs-lookup"><span data-stu-id="5c28d-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="5c28d-118">(간단 하 게 게시 및 기타 메서드를 종료 합니다.) 첫 번째 시도는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="5c28d-119">컨트롤러 클래스는에 종속 `ProductRepository` 되며 컨트롤러에서 인스턴스를 만들도록 허용 `ProductRepository` 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="5c28d-120">그러나 이러한 방식으로 종속성을 하드 코딩 하는 것은 여러 가지 이유로 잘못 된 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="5c28d-121">다른 구현으로 대체 하려는 경우에 `ProductRepository` 는 컨트롤러 클래스도 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="5c28d-122">에 종속성이 있는 경우 `ProductRepository` 컨트롤러 내에서이를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="5c28d-123">여러 컨트롤러가 있는 규모가 많은 프로젝트의 경우, 구성 코드는 프로젝트 전체에 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="5c28d-124">컨트롤러는 데이터베이스를 쿼리하도록 하드 코딩 되기 때문에 단위 테스트는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="5c28d-125">단위 테스트의 경우 현재 디자인에서 사용할 수 없는 모의 또는 스텁 리포지토리를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="5c28d-126">리포지토리를 컨트롤러에 *삽입* 하 여 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="5c28d-127">먼저 클래스를 인터페이스로 리팩터링 합니다 `ProductRepository` .</span><span class="sxs-lookup"><span data-stu-id="5c28d-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="5c28d-128">그런 다음을 `IProductRepository` 생성자 매개 변수로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="5c28d-129">이 예제에서는 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="5c28d-130">Setter *주입*을 사용 하 여 setter 메서드 또는 속성을 통해 종속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="5c28d-131">하지만 이제 응용 프로그램에서 컨트롤러를 직접 만들지 않기 때문에 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="5c28d-132">웹 API는 요청을 라우팅할 때 컨트롤러를 만들며 Web API는에 대해 알지 못합니다 `IProductRepository` .</span><span class="sxs-lookup"><span data-stu-id="5c28d-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="5c28d-133">웹 API 종속성 해결 프로그램이 제공 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="5c28d-134">Web API 종속성 확인자</span><span class="sxs-lookup"><span data-stu-id="5c28d-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="5c28d-135">Web API는 종속성을 확인 하기 위한 **되며 idependencyresolver** 인터페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="5c28d-136">인터페이스에 대 한 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="5c28d-137">**IDependencyScope** 인터페이스에는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="5c28d-138">**GetService** 는 형식의 인스턴스를 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="5c28d-139">**Getservices** 는 지정 된 형식의 개체 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="5c28d-140">**되며 idependencyresolver** 메서드는 **IDependencyScope** 를 상속 하 고 **beginscope** 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="5c28d-141">이 자습서의 뒷부분에서는 범위에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="5c28d-142">Web API는 컨트롤러 인스턴스를 만들 때 먼저 **되며 idependencyresolver. GetService**를 호출 하 여 컨트롤러 유형을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="5c28d-143">이 확장성 후크를 사용 하 여 모든 종속성을 해결 하는 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="5c28d-144">**GetService** 가 null을 반환 하는 경우 Web API는 컨트롤러 클래스에서 매개 변수가 없는 생성자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="5c28d-145">Unity 컨테이너를 사용 하 여 종속성 확인</span><span class="sxs-lookup"><span data-stu-id="5c28d-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="5c28d-146">완전 한 **되며 idependencyresolver** 구현을 처음부터 작성할 수 있지만이 인터페이스는 Web API와 기존 IoC 컨테이너 간의 브리지 역할을 하기 위해 실제로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="5c28d-147">IoC 컨테이너는 종속성 관리를 담당 하는 소프트웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="5c28d-148">컨테이너를 사용 하 여 형식을 등록 한 다음 컨테이너를 사용 하 여 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="5c28d-149">컨테이너는 종속성 관계를 자동으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="5c28d-150">많은 IoC 컨테이너를 사용 하 여 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="5c28d-151">"IoC"는 프레임 워크가 응용 프로그램 코드를 호출 하는 일반적인 패턴 인 "제어 반전"을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="5c28d-152">IoC 컨테이너는 사용자에 대 한 개체를 생성 하 여 일반적인 제어 흐름을 "반전" 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="5c28d-153">이 자습서에서는 Microsoft 패턴 방법의 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) 를 사용 &amp; 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="5c28d-154">기타 인기 있는 라이브러리에는 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/)및 [StructureMap](http://structuremap.github.io/documentation/)가 포함 됩니다. NuGet 패키지 관리자를 사용 하 여 Unity를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="5c28d-155">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="5c28d-156">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="5c28d-157">다음은 Unity 컨테이너를 래핑하는 **되며 idependencyresolver** 의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="5c28d-158">종속성 확인자 구성</span><span class="sxs-lookup"><span data-stu-id="5c28d-158">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="5c28d-159">전역 **Httpconfiguration** 개체의 **DependencyResolver** 속성에서 종속성 해결 프로그램을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-159">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="5c28d-160">다음 코드에서는 Unity를 `IProductRepository` 사용 하 여 인터페이스를 등록 한 다음를 만듭니다 `UnityResolver` .</span><span class="sxs-lookup"><span data-stu-id="5c28d-160">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="5c28d-161">종속성 범위 및 컨트롤러 수명</span><span class="sxs-lookup"><span data-stu-id="5c28d-161">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="5c28d-162">컨트롤러가 요청당 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-162">Controllers are created per request.</span></span> <span data-ttu-id="5c28d-163">개체 수명을 관리 하기 위해 **되며 idependencyresolver** 는 *범위의*개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-163">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="5c28d-164">**Httpconfiguration** 개체에 연결 된 종속성 확인자에 전역 범위가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-164">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="5c28d-165">Web API는 컨트롤러를 만들 때 **Beginscope**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-165">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="5c28d-166">이 메서드는 자식 범위를 나타내는 **IDependencyScope** 를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-166">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="5c28d-167">Web API는 자식 범위에 대해 **GetService** 를 호출 하 여 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-167">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="5c28d-168">요청이 완료 되 면 Web API는 자식 범위에서 **Dispose** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-168">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="5c28d-169">**Dispose** 메서드를 사용 하 여 컨트롤러의 종속성을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-169">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="5c28d-170">**Beginscope** 를 구현 하는 방법은 IoC 컨테이너에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-170">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="5c28d-171">Unity의 경우 범위는 자식 컨테이너에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-171">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="5c28d-172">대부분의 IoC 컨테이너는 이와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c28d-172">Most IoC containers have similar equivalents.</span></span>
