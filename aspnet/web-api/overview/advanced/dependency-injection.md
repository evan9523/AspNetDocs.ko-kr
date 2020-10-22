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
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 종속성 주입

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 삽입 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - [Unity 응용 프로그램 블록](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (버전 5도 작동 함)

## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

‘종속성’은 다른 개체에 필요한 모든 개체입니다. 예를 들어 데이터 액세스를 처리 하는 [리포지토리](http://martinfowler.com/eaaCatalog/repository.html) 를 정의 하는 것이 일반적입니다. 예를 들어 살펴보겠습니다. 먼저 도메인 모델을 정의 합니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

다음은 Entity Framework를 사용 하 여 데이터베이스에 항목을 저장 하는 간단한 리포지토리 클래스입니다.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

이제 엔터티에 대 한 GET 요청을 지 원하는 Web API 컨트롤러를 정의 해 보겠습니다 `Product` . (간단 하 게 게시 및 기타 메서드를 종료 합니다.) 첫 번째 시도는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

컨트롤러 클래스는에 종속 `ProductRepository` 되며 컨트롤러에서 인스턴스를 만들도록 허용 `ProductRepository` 합니다. 그러나 이러한 방식으로 종속성을 하드 코딩 하는 것은 여러 가지 이유로 잘못 된 개념입니다.

- 다른 구현으로 대체 하려는 경우에 `ProductRepository` 는 컨트롤러 클래스도 수정 해야 합니다.
- 에 종속성이 있는 경우 `ProductRepository` 컨트롤러 내에서이를 구성 해야 합니다. 여러 컨트롤러가 있는 규모가 많은 프로젝트의 경우, 구성 코드는 프로젝트 전체에 분산 됩니다.
- 컨트롤러는 데이터베이스를 쿼리하도록 하드 코딩 되기 때문에 단위 테스트는 어렵습니다. 단위 테스트의 경우 현재 디자인에서 사용할 수 없는 모의 또는 스텁 리포지토리를 사용 해야 합니다.

리포지토리를 컨트롤러에 *삽입* 하 여 이러한 문제를 해결할 수 있습니다. 먼저 클래스를 인터페이스로 리팩터링 합니다 `ProductRepository` .

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

그런 다음을 `IProductRepository` 생성자 매개 변수로 제공 합니다.

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

이 예제에서는 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)을 사용 합니다. Setter *주입*을 사용 하 여 setter 메서드 또는 속성을 통해 종속성을 설정할 수도 있습니다.

하지만 이제 응용 프로그램에서 컨트롤러를 직접 만들지 않기 때문에 문제가 발생 합니다. 웹 API는 요청을 라우팅할 때 컨트롤러를 만들며 Web API는에 대해 알지 못합니다 `IProductRepository` . 웹 API 종속성 해결 프로그램이 제공 되는 위치입니다.

## <a name="the-web-api-dependency-resolver"></a>Web API 종속성 확인자

Web API는 종속성을 확인 하기 위한 **되며 idependencyresolver** 인터페이스를 정의 합니다. 인터페이스에 대 한 정의는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope** 인터페이스에는 두 가지 방법이 있습니다.

- **GetService** 는 형식의 인스턴스를 하나 만듭니다.
- **Getservices** 는 지정 된 형식의 개체 컬렉션을 만듭니다.

**되며 idependencyresolver** 메서드는 **IDependencyScope** 를 상속 하 고 **beginscope** 메서드를 추가 합니다. 이 자습서의 뒷부분에서는 범위에 대해 설명 합니다.

Web API는 컨트롤러 인스턴스를 만들 때 먼저 **되며 idependencyresolver. GetService**를 호출 하 여 컨트롤러 유형을 전달 합니다. 이 확장성 후크를 사용 하 여 모든 종속성을 해결 하는 컨트롤러를 만들 수 있습니다. **GetService** 가 null을 반환 하는 경우 Web API는 컨트롤러 클래스에서 매개 변수가 없는 생성자를 찾습니다.

## <a name="dependency-resolution-with-the-unity-container"></a>Unity 컨테이너를 사용 하 여 종속성 확인

완전 한 **되며 idependencyresolver** 구현을 처음부터 작성할 수 있지만이 인터페이스는 Web API와 기존 IoC 컨테이너 간의 브리지 역할을 하기 위해 실제로 설계 되었습니다.

IoC 컨테이너는 종속성 관리를 담당 하는 소프트웨어 구성 요소입니다. 컨테이너를 사용 하 여 형식을 등록 한 다음 컨테이너를 사용 하 여 개체를 만듭니다. 컨테이너는 종속성 관계를 자동으로 출력 합니다. 많은 IoC 컨테이너를 사용 하 여 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"는 프레임 워크가 응용 프로그램 코드를 호출 하는 일반적인 패턴 인 "제어 반전"을 의미 합니다. IoC 컨테이너는 사용자에 대 한 개체를 생성 하 여 일반적인 제어 흐름을 "반전" 합니다.

이 자습서에서는 Microsoft 패턴 방법의 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) 를 사용 &amp; 합니다. 기타 인기 있는 라이브러리에는 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/)및 [StructureMap](http://structuremap.github.io/documentation/)가 포함 됩니다. NuGet 패키지 관리자를 사용 하 여 Unity를 설치할 수 있습니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

다음은 Unity 컨테이너를 래핑하는 **되며 idependencyresolver** 의 구현입니다.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

## <a name="configuring-the-dependency-resolver"></a>종속성 확인자 구성

전역 **Httpconfiguration** 개체의 **DependencyResolver** 속성에서 종속성 해결 프로그램을 설정 합니다.

다음 코드에서는 Unity를 `IProductRepository` 사용 하 여 인터페이스를 등록 한 다음를 만듭니다 `UnityResolver` .

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>종속성 범위 및 컨트롤러 수명

컨트롤러가 요청당 생성 됩니다. 개체 수명을 관리 하기 위해 **되며 idependencyresolver** 는 *범위의*개념을 사용 합니다.

**Httpconfiguration** 개체에 연결 된 종속성 확인자에 전역 범위가 있습니다. Web API는 컨트롤러를 만들 때 **Beginscope**를 호출 합니다. 이 메서드는 자식 범위를 나타내는 **IDependencyScope** 를 반환 합니다.

Web API는 자식 범위에 대해 **GetService** 를 호출 하 여 컨트롤러를 만듭니다. 요청이 완료 되 면 Web API는 자식 범위에서 **Dispose** 를 호출 합니다. **Dispose** 메서드를 사용 하 여 컨트롤러의 종속성을 삭제 합니다.

**Beginscope** 를 구현 하는 방법은 IoC 컨테이너에 따라 다릅니다. Unity의 경우 범위는 자식 컨테이너에 해당 합니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

대부분의 IoC 컨테이너는 이와 유사 합니다.
