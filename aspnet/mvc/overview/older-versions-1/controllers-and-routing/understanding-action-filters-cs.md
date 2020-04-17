---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 이해 (C#) | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서의 목표는 작업 필터를 설명하는 것입니다. 작업 필터는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542185"
---
# <a name="understanding-action-filters-c"></a>작업 필터 이해(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 이 자습서의 목표는 작업 필터를 설명하는 것입니다. 작업 필터는 작업이 실행되는 방식을 수정하는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.

## <a name="understanding-action-filters"></a>작업 필터 이해

이 자습서의 목표는 작업 필터를 설명하는 것입니다. 작업 필터는 작업이 실행되는 방식을 수정하는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다. ASP.NET MVC 프레임워크에는 다음과 같은 몇 가지 작업 필터가 포함되어 있습니다.

- OutputCache - 이 작업 필터는 지정된 시간 동안 컨트롤러 작업의 출력을 캐시합니다.
- HandleError - 이 작업 필터는 컨트롤러 작업이 실행될 때 발생하는 오류를 처리합니다.
- 권한 부여 - 이 작업 필터를 사용하면 특정 사용자 또는 역할에 대한 액세스를 제한할 수 있습니다.

사용자 지정 작업 필터를 직접 만들 수도 있습니다. 예를 들어 사용자 지정 인증 시스템을 구현하기 위해 사용자 지정 작업 필터를 만들 수 있습니다. 또는 컨트롤러 작업에서 반환되는 뷰 데이터를 수정하는 작업 필터를 만들 수 있습니다.

이 자습서에서는 처음부터 작업 필터를 빌드하는 방법을 배웁니다. 작업 처리의 여러 단계를 Visual Studio 출력 창에 기록하는 로그 작업 필터를 만듭니다.

### <a name="using-an-action-filter"></a>작업 필터 사용

작업 필터는 특성입니다. 대부분의 작업 필터를 개별 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있습니다.

예를 들어 목록 1의 데이터 컨트롤러는 `Index()` 현재 시간을 반환하는 작업을 노출합니다. 이 작업은 `OutputCache` 작업 필터로 장식됩니다. 이 필터를 사용하면 작업에서 반환되는 값이 10초 동안 캐시됩니다.

**리스팅 1 –`Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

URL /Data/Index를 `Index()` 브라우저의 주소 표시줄에 입력하고 새로 고침 단추를 여러 번 누르면 10초 동안 동일한 시간이 표시됩니다. `Index()` 작업의 출력은 10초 동안 캐시됩니다(그림 1 참조).

[![캐시된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**그림 01**: 캐시 된 시간[(전체 크기 이미지를 보려면 클릭)](understanding-action-filters-cs/_static/image3.png)

목록 1에서 작업 필터인 `OutputCache` 단일 작업 필터가 `Index()` 메서드에 적용됩니다. 필요한 경우 동일한 작업에 여러 작업 필터를 적용할 수 있습니다. 예를 들어 `OutputCache` 동일한 작업에 및 `HandleError` 작업 필터를 모두 적용할 수 있습니다.

목록 1에서 `OutputCache` 작업 필터가 `Index()` 작업에 적용됩니다. 이 특성을 `DataController` 클래스 자체에 적용할 수도 있습니다. 이 경우 컨트롤러에서 노출된 모든 작업에서 반환되는 결과는 10초 동안 캐시됩니다.

### <a name="the-different-types-of-filters"></a>다양한 유형의 필터

ASP.NET MVC 프레임워크는 다음과 같은 네 가지 유형의 필터를 지원합니다.

1. 권한 부여 필터 - `IAuthorizationFilter` 특성을 구현합니다.
2. 작업 필터 - 특성을 `IActionFilter` 구현합니다.
3. 결과 필터 - 특성을 `IResultFilter` 구현합니다.
4. 예외 필터 - 특성을 `IExceptionFilter` 구현합니다.

필터는 위에 나열된 순서대로 실행됩니다. 예를 들어 권한 부여 필터는 항상 작업 필터 앞에 실행되고 예외 필터는 다른 모든 유형의 필터 후에 항상 실행됩니다.

권한 부여 필터는 컨트롤러 작업에 대한 인증 및 권한 부여를 구현하는 데 사용됩니다. 예를 들어 권한 부여 필터는 권한 부여 필터의 예입니다.

작업 필터에는 컨트롤러 작업이 실행되기 전과 후에 실행되는 논리가 포함되어 있습니다. 예를 들어 작업 필터를 사용하여 컨트롤러 작업이 반환하는 뷰 데이터를 수정할 수 있습니다.

결과 필터에는 뷰 결과가 실행되기 전과 후에 실행되는 논리가 포함되어 있습니다. 예를 들어 뷰가 브라우저에 렌더링되기 직전에 뷰 결과를 수정할 수 있습니다.

예외 필터는 실행할 마지막 필터 유형입니다. 예외 필터를 사용하여 컨트롤러 작업 또는 컨트롤러 작업 결과에서 발생하는 오류를 처리할 수 있습니다. 예외 필터를 사용하여 오류를 기록할 수도 있습니다.

각 필터 유형은 특정 순서로 실행됩니다. 동일한 유형의 필터가 실행되는 순서를 제어하려면 필터의 Order 속성을 설정할 수 있습니다.

모든 작업 필터의 기본 클래스는 `System.Web.Mvc.FilterAttribute` 클래스입니다. `IAuthorizationFilter`특정 유형의 필터를 구현하려면 기본 Filter 클래스에서 상속되고 하나 이상의 을 `IActionFilter`구현하는 클래스를 `IResultFilter` `IExceptionFilter` 만들어야 합니다.

### <a name="the-base-actionfilterattribute-class"></a>기본 작업필터특성 클래스

사용자 지정 작업 필터를 보다 쉽게 구현할 수 있도록 ASP.NET MVC 프레임워크에는 기본 `ActionFilterAttribute` 클래스가 포함됩니다. 이 클래스는 `IActionFilter` 클래스와 `IResultFilter` 인터페이스를 모두 구현하고 `Filter` 클래스에서 상속합니다.

여기서 용어는 완전히 일치하지 않습니다. 기술적으로 ActionFilterAttribute 클래스에서 상속하는 클래스는 작업 필터와 결과 필터입니다. 그러나 느슨한 의미에서 단어 작업 필터는 ASP.NET MVC 프레임워크의 모든 유형의 필터를 참조하는 데 사용됩니다.

기본 `ActionFilterAttribute` 클래스에는 재정의할 수 있는 다음 메서드가 있습니다.

- OnAction실행 - 컨트롤러 작업이 실행되기 전에 이 메서드가 호출됩니다.
- OnActionExecuted - 컨트롤러 작업이 실행된 후 이 메서드가 호출됩니다.
- OnResult 실행 - 컨트롤러 작업 결과가 실행되기 전에 이 메서드가 호출됩니다.
- OnResultExecuted - 컨트롤러 작업 결과가 실행된 후 이 메서드가 호출됩니다.

다음 섹션에서는 이러한 각 다른 메서드를 구현하는 방법을 살펴보겠습니다.

### <a name="creating-a-log-action-filter"></a>로그 작업 필터 만들기

사용자 지정 작업 필터를 빌드하는 방법을 설명하기 위해 컨트롤러 작업을 처리하는 단계를 Visual Studio 출력 창에 기록하는 사용자 지정 작업 필터를 만듭니다. 우리는 `LogActionFilter` 리스팅 2에 포함되어 있습니다.

**리스팅 2 –`ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

목록 2에서 `OnActionExecuting()`에서 `OnActionExecuted()` `OnResultExecuting()`" `OnResultExecuted()` 및 메서드는 `Log()` 모두 메서드를 호출합니다. 메서드의 이름과 현재 경로 데이터가 `Log()` 메서드에 전달됩니다. 메서드는 `Log()` Visual Studio 출력 창에 메시지를 씁니다(그림 2 참조).

[![비주얼 스튜디오 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**그림 02**: 비주얼 스튜디오 출력 창에 쓰기[(전체 크기 이미지를 보려면 클릭)](understanding-action-filters-cs/_static/image6.png)

목록 3의 홈 컨트롤러는 전체 컨트롤러 클래스에 로그 작업 필터를 적용하는 방법을 보여 줍니다. 홈 컨트롤러에서 노출되는 작업이 호출될 때마다 `Index()` 메서드 또는 `About()` 메서드 - 작업 처리 단계는 Visual Studio 출력 창에 기록됩니다.

**리스팅 3 –`Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>요약

이 자습서에서는 MVC 작업 필터를 ASP.NET 소개했습니다. 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터의 네 가지 유형의 필터에 대해 배웠습니다. 기본 `ActionFilterAttribute` 클래스에 대해서도 배웠습니다.

마지막으로 간단한 작업 필터를 구현하는 방법을 배웠습니다. 컨트롤러 작업을 처리하는 단계를 Visual Studio 출력 창에 기록하는 로그 작업 필터를 만들었습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)
