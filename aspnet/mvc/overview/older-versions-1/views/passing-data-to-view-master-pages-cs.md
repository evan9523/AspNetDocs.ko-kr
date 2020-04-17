---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: 마스터 페이지 보기로 데이터 전달(C#) | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달하는 방법을 설명하는 것입니다. 뷰 m에 데이터를 전달하기 위한 두 가지 전략을 검토합니다...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a934f93d89e6530becc114fe455c8b3ab2968de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542484"
---
# <a name="passing-data-to-view-master-pages-c"></a>보기 마스터 페이지에 데이터 전달(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> 이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달하는 방법을 설명하는 것입니다. 뷰 마스터 페이지에 데이터를 전달하기 위한 두 가지 전략을 살펴봅니다. 먼저 유지 관리가 어려운 응용 프로그램을 만드는 쉬운 솔루션에 대해 설명합니다. 다음으로, 초기 작업이 좀 더 필요하지만 훨씬 더 유지 관리가 가능한 응용 프로그램을 만드는 훨씬 더 나은 솔루션을 살펴봅습니다.

## <a name="passing-data-to-view-master-pages"></a>마스터 페이지를 보려면 데이터 전달

이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달하는 방법을 설명하는 것입니다. 뷰 마스터 페이지에 데이터를 전달하기 위한 두 가지 전략을 살펴봅니다. 먼저 유지 관리가 어려운 응용 프로그램을 만드는 쉬운 솔루션에 대해 설명합니다. 다음으로, 초기 작업이 좀 더 필요하지만 훨씬 더 유지 관리가 가능한 응용 프로그램을 만드는 훨씬 더 나은 솔루션을 살펴봅습니다.

### <a name="the-problem"></a>문제

동영상 데이터베이스 응용 프로그램을 빌드하고 응용 프로그램의 모든 페이지에 동영상 범주 목록을 표시하려고 한다고 가정합니다(그림 1 참조). 또한 동영상 범주 목록이 데이터베이스 테이블에 저장되어 있다고 가정해 보십시오. 이 경우 데이터베이스에서 범주를 검색하고 뷰 마스터 페이지 내에서 동영상 범주 목록을 렌더링하는 것이 좋습니다.

[![뷰 마스터 페이지에 동영상 범주 표시](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)

**그림 01**: 뷰 마스터 페이지에 동영상 범주 표시[(전체 크기 이미지를 보려면 클릭)](passing-data-to-view-master-pages-cs/_static/image3.png)

여기에 문제가 있습니다. 마스터 페이지에서 동영상 범주 목록을 검색하려면 어떻게 해야 합니까? 마스터 페이지에서 모델 클래스의 메서드를 직접 호출하는 것은 좋습니다. 즉, 마스터 페이지에 데이터베이스에서 데이터를 검색하기 위한 코드를 포함하려는 경우를 고려합니다. 그러나 MVC 컨트롤러를 우회하여 데이터베이스에 액세스하는 것은 MVC 응용 프로그램을 빌드할 때 의주요 이점 중 하나인 문제의 깔끔한 분리를 위반합니다.

MVC 응용 프로그램에서MVC 뷰와 MVC 모델 간의 모든 상호 작용을 MVC 컨트롤러에서 처리하려고 합니다. 이러한 문제 분리는 보다 유지 관리 가능하고 적응가능하며 테스트 가능한 응용 프로그램을 제공합니다.

MVC 응용 프로그램에서 뷰 마스터 페이지를 포함하여 뷰에 전달된 모든 데이터는 컨트롤러 동작에 의해 뷰로 전달되어야 합니다. 또한 뷰 데이터를 활용하여 데이터를 전달해야 합니다. 이 자습서의 나머지 부분에서는 뷰 데이터를 뷰 마스터 페이지로 전달하는 두 가지 방법을 살펴봅니다.

### <a name="the-simple-solution"></a>간단한 솔루션

컨트롤러에서 뷰 마스터 페이지로 뷰 데이터를 전달하는 가장 간단한 솔루션부터 살펴보겠습니다. 가장 간단한 해결 방법은 각 컨트롤러 작업에서 마스터 페이지에 대한 뷰 데이터를 전달하는 것입니다.

목록 1의 컨트롤러를 고려하십시오. 두 개의 작업 `Index()` 이름을 `Details()`지정 하 고 . 작업 `Index()` 메서드는 Movies 데이터베이스 테이블의 모든 동영상을 반환합니다. 작업 `Details()` 메서드는 특정 동영상 범주의 모든 영화를 반환합니다.

**리스팅 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

Index() 및 Details() 작업 모두 데이터를 볼 수 있는 두 개의 항목을 추가합니다. Index() 작업은 범주와 동영상이라는 두 가지 키를 추가합니다. 범주 키는 보기 마스터 페이지에 표시되는 동영상 범주 목록을 나타냅니다. 동영상 키는 색인 보기 페이지에 표시되는 동영상 목록을 나타냅니다.

세부 정보() 작업은 범주와 동영상이라는 두 개의 키도 추가합니다. 범주 키는 다시 한 번 보기 마스터 페이지에 표시되는 동영상 범주 목록을 나타냅니다. 동영상 키는 세부 정보 보기 페이지에 표시되는 특정 범주의 동영상 목록을 나타냅니다(그림 2 참조).

[![세부 정보 보기](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)

**그림 02**: 상세 보기[(전체 크기 이미지를 보려면 클릭)](passing-data-to-view-master-pages-cs/_static/image6.png)

인덱스 보기는 목록 2에 포함되어 있습니다. 보기 데이터에서 동영상 항목으로 표시되는 동영상 목록을 통해 간단히 이월됩니다.

**리스팅 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

뷰 마스터 페이지는 목록 3에 포함되어 있습니다. 뷰 마스터 페이지는 뷰 데이터에서 범주 항목으로 표시되는 모든 동영상 범주를 이기하고 렌더링합니다.

**리스팅 3 –`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

모든 데이터는 뷰 데이터를 통해 뷰 및 뷰 마스터 페이지로 전달됩니다. 이것이 데이터를 마스터 페이지로 전달하는 올바른 방법입니다.

그렇다면 이 솔루션의 문제점은 무엇일까요? 문제는이 솔루션이 DRY (자신을 반복하지 마십시오) 원칙을 위반한다는 것입니다. 모든 컨트롤러 작업은 데이터를 보려면 동일한 영화 범주 목록을 추가해야 합니다. 응용 프로그램에 중복 된 코드를 사용하면 응용 프로그램을 유지 관리, 조정 및 수정하기가 훨씬 더 어려워집니다.

### <a name="the-good-solution"></a>좋은 솔루션

이 섹션에서는 컨트롤러 작업에서 뷰 마스터 페이지로 데이터를 전달하는 대체 솔루션과 더 나은 솔루션을 살펴봅니다. 각 컨트롤러 동작에서 마스터 페이지에 대한 동영상 범주를 추가하는 대신 동영상 범주를 뷰 데이터에 한 번만 추가합니다. 뷰 마스터 페이지에서 사용하는 모든 뷰 데이터는 응용 프로그램 컨트롤러에 추가됩니다.

ApplicationController 클래스는 목록 4에 포함되어 있습니다.

**리스팅 4 –`Controllers\ApplicationController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

목록 4의 응용 프로그램 컨트롤러에 대해 알아두어야 할 세 가지 사항이 있습니다. 먼저 클래스가 기본 System.Web.Mvc.Controller 클래스에서 상속됩니다. 응용 프로그램 컨트롤러는 컨트롤러 클래스입니다.

둘째, 응용 프로그램 컨트롤러 클래스는 추상 클래스입니다. 추상 클래스는 구체적인 클래스에서 구현해야 하는 클래스입니다. 응용 프로그램 컨트롤러는 추상 클래스이므로 클래스에 정의된 메서드를 직접 호출할 수 없습니다. 응용 프로그램 클래스를 직접 호출하려고 하면 리소스를 찾을 수 없는 오류 메시지가 표시됩니다.

셋째, 응용 프로그램 컨트롤러에는 데이터를 볼 수 있는 동영상 범주 목록을 추가하는 생성자가 포함되어 있습니다. 응용 프로그램 컨트롤러에서 상속되는 모든 컨트롤러 클래스는 응용 프로그램 컨트롤러의 생성자가 자동으로 호출됩니다. 응용 프로그램 컨트롤러에서 상속하는 컨트롤러에서 작업을 호출할 때마다 동영상 범주가 뷰 데이터에 자동으로 포함됩니다.

목록 5의 동영상 컨트롤러는 응용 프로그램 컨트롤러에서 상속됩니다.

**리스팅 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

이전 섹션에서 설명한 홈 컨트롤러와 마찬가지로 Movies 컨트롤러는 두 가지 `Index()` `Details()`작업 메서드와 를 노출합니다. 뷰 마스터 페이지에 표시되는 동영상 범주 목록은 `Index()` 또는 `Details()` 메서드의 데이터를 보기 위해 추가되지 않습니다. Movies 컨트롤러는 응용 프로그램 컨트롤러에서 상속되므로 동영상 범주 목록이 추가되어 데이터를 자동으로 볼 수 있습니다.

뷰 마스터 페이지에 대한 보기 데이터를 추가하는 이 솔루션은 DRY(직접 반복하지 않음) 원칙을 위반하지 않습니다. 데이터를 볼 수 있는 동영상 범주 목록을 추가하는 코드는 응용 프로그램 컨트롤러의 생성자인 한 위치에만 포함됩니다.

### <a name="summary"></a>요약

이 자습서에서는 컨트롤러에서 뷰 마스터 페이지로 뷰 데이터를 전달하는 두 가지 방법에 대해 설명했습니다. 첫째, 간단하지만 접근 방식을 유지하기어려운 방법을 검토했습니다. 첫 번째 섹션에서는 응용 프로그램의 각 컨트롤러 작업에서 뷰 마스터 페이지에 대한 보기 데이터를 추가하는 방법에 대해 설명했습니다. 우리는 이것이 DRY (자신을 반복하지 마십시오) 원칙을 위반하기 때문에 나쁜 접근 방식이라고 결론을 내렸습니다.

다음으로 뷰 마스터 페이지에서 데이터를 보는 데 필요한 데이터를 추가하기 위한 훨씬 더 나은 전략을 살펴보겠습니다. 각 컨트롤러 작업에 뷰 데이터를 추가하는 대신 응용 프로그램 컨트롤러 내에서 뷰 데이터를 한 번만 추가했습니다. 이렇게 하면 ASP.NET MVC 응용 프로그램의 뷰 마스터 페이지에 데이터를 전달할 때 중복 된 코드를 방지할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-page-layouts-with-view-master-pages-cs.md)
> [다음](asp-net-mvc-views-overview-vb.md)
