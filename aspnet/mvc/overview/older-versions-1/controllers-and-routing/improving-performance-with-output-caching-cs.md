---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 출력 캐싱(C#)으로 성능 향상 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 출력 캐싱을 활용하여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 알아봅니다. 당신은 ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542718"
---
# <a name="improving-performance-with-output-caching-c"></a>출력 캐싱을 통한 성능 향상(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> 이 자습서에서는 출력 캐싱을 활용하여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 알아봅니다. 컨트롤러 작업에서 반환된 결과를 캐시하여 새 사용자가 작업을 호출할 때마다 동일한 콘텐츠를 만들 필요가 없도록 하는 방법을 알아봅니다.

이 자습서의 목표는 출력 캐시를 활용하여 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시킬 수 있는 방법을 설명하는 것입니다. 출력 캐시를 사용하면 컨트롤러 작업에서 반환되는 콘텐츠를 캐시할 수 있습니다. 이렇게 하면 동일한 컨트롤러 작업이 호출될 때마다 동일한 콘텐츠를 생성할 필요가 없습니다.

예를 들어 ASP.NET MVC 응용 프로그램이 Index라는 보기의 데이터베이스 레코드 목록을 표시한다고 가정해 보겠습니다. 일반적으로 사용자가 Index 뷰를 반환하는 컨트롤러 작업을 호출할 때마다 데이터베이스 쿼리를 실행하여 데이터베이스 레코드 집합을 데이터베이스에서 검색해야 합니다.

반면에 출력 캐시를 활용하면 사용자가 동일한 컨트롤러 작업을 호출할 때마다 데이터베이스 쿼리를 실행하지 않을 수 있습니다. 컨트롤러 작업에서 재생성되는 대신 캐시에서 뷰를 검색할 수 있습니다. 캐싱을 사용하면 서버에서 중복 작업을 수행하지 않도록 할 수 있습니다.

## <a name="enabling-output-caching"></a>출력 캐싱 사용

개별 컨트롤러 작업 또는 전체 컨트롤러 클래스에 [OutputCache] 특성을 추가하여 출력 캐싱을 사용하도록 설정합니다. 예를 들어 목록 1의 컨트롤러는 Index()라는 작업을 노출합니다. Index() 작업의 출력은 10초 동안 캐시됩니다.

**목록 1 – 컨트롤러\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

ASP.NET MVC의 베타 버전에서는 출력 캐싱이 와 같은 [http://www.MySite.com/](http://www.mysite.com/)URL에 대해 작동하지 않습니다. 대신 에 대한 [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)URL을 입력해야 합니다. 

목록 1에서 Index() 작업의 출력은 10초 동안 캐시됩니다. 원하는 경우 훨씬 더 긴 캐시 기간을 지정할 수 있습니다. 예를 들어 컨트롤러 작업의 출력을 하루 동안 캐시하려는 경우 86400초(60초 \* 60분 \* 24시간)의 캐시 기간을 지정할 수 있습니다.

지정한 시간 동안 콘텐츠가 캐시된다는 보장은 없습니다. 메모리 리소스가 부족해지면 캐시가 자동으로 콘텐츠를 제거하기 시작합니다.

목록 1의 홈 컨트롤러는 목록 2의 인덱스 보기를 반환합니다. 이 보기에 대해 특별한 것은 없습니다. 색인 보기에는 단순히 현재 시간이 표시됩니다(그림 1 참조).

**목록 2 – 보기\홈\인덱스.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**그림 1 – 캐시된 인덱스 보기**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

브라우저의 주소 표시줄에 URL /Home/Index를 입력하고 브라우저에서 새로 고침/다시로드 버튼을 반복적으로 눌러 Index() 작업을 여러 번 호출하면 인덱스 보기에 표시되는 시간이 10초 동안 변경되지 않습니다. 뷰가 캐시되므로 동시에 표시됩니다.

응용 프로그램을 방문하는 모든 사람에게 동일한 보기가 캐시된다는 점을 이해하는 것이 중요합니다. Index() 작업을 호출하는 모든 사용자는 인덱스 보기의 캐시된 버전과 동일한 캐시된 버전을 받게 됩니다. 즉, 인덱스 보기를 제공하기 위해 웹 서버가 수행해야 하는 작업량이 크게 줄어듭니다.

목록 2의 보기는 정말 간단한 일을하는 일이. 뷰에 현재 시간이 표시됩니다. 그러나 데이터베이스 레코드 집합을 표시하는 뷰를 쉽게 캐시할 수 있습니다. 이 경우 뷰를 반환하는 컨트롤러 작업이 호출될 때마다 데이터베이스 레코드 집합을 데이터베이스에서 검색할 필요가 없습니다. 캐싱을 사용하면 웹 서버와 데이터베이스 서버가 모두 수행해야 하는 작업량을 줄일 수 있습니다.

MVC 보기에서 &lt;페이지 %@&gt; OutputCache % 지시문을 사용하지 마십시오. 이 지시문은 Web Forms 세계에서 흘러넘치며 ASP.NET MVC 응용 프로그램에서 사용해서는 안 됩니다.

## <a name="where-content-is-cached"></a>콘텐츠가 캐시되는 위치

기본적으로 [OutputCache] 특성을 사용하면 콘텐츠가 웹 서버, 프록시 서버 및 웹 브라우저의 세 위치에 캐시됩니다. [OutputCache] 특성의 위치 속성을 수정하여 콘텐츠가 캐시되는 위치를 정확하게 제어할 수 있습니다.

위치 속성을 다음 값 중 하나로 설정할 수 있습니다.

> · 어떤
> 
> · 클라이언트
> 
> · 다운스트림
> 
> · 서버
> 
> · 없음
> 
> · 서버앤클라이언트

기본적으로 Location 속성에는 Any 값이 있습니다. 그러나 브라우저에서만 캐시하거나 서버에서만 캐시하려는 상황이 있습니다. 예를 들어 각 사용자에 대해 개인 설정된 정보를 캐싱하는 경우 서버의 정보를 캐시해서는 안 됩니다. 다른 사용자에게 다른 정보를 표시하는 경우 클라이언트에서만 정보를 캐시해야 합니다.

예를 들어 목록 3의 컨트롤러는 현재 사용자 이름을 반환하는 GetName() 이라는 작업을 노출합니다. 잭이 웹 사이트에 로그인하여 GetName() 작업을 호출하면 작업이 "Hi Jack"문자열을 반환합니다. 그 후 Jill이 웹 사이트에 로그인하여 GetName() 작업을 호출하면 "Hi Jack"이라는 문자열도 받게 됩니다. Jack이 처음에 컨트롤러 작업을 호출한 후 모든 사용자에 대해 문자열이 웹 서버에 캐시됩니다.

**목록 3 – 컨트롤러\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

대부분의 경우 목록 3의 컨트롤러가 원하는 방식으로 작동하지 않습니다. Jill에 "Hi Jack"이라는 메시지를 표시하고 싶지 는 않습니다.

서버 캐시에서 개인 설정된 콘텐츠를 캐시해서는 안 됩니다. 그러나 성능을 향상시키기 위해 브라우저 캐시에서 개인 설정된 콘텐츠를 캐시할 수 있습니다. 브라우저에서 콘텐츠를 캐시하고 사용자가 동일한 컨트롤러 작업을 여러 번 호출하면 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.

목록 4의 수정된 컨트롤러는 GetName() 작업의 출력을 캐시합니다. 그러나 콘텐츠는 서버가 아닌 브라우저에서만 캐시됩니다. 이렇게 하면 여러 사용자가 GetName() 메서드를 호출할 때 각 사용자는 다른 사용자의 사용자 이름이 아닌 자신의 사용자 이름을 가져옵니다.

**목록 4 – 컨트롤러\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

목록 4의 [OutputCache] 특성에는 ValueCacheLocation.Client 값으로 설정된 위치 속성이 포함되어 있습니다. [OutputCache] 특성에는 NoStore 속성도 포함됩니다. NoStore 속성은 프록시 서버와 브라우저에 캐시된 콘텐츠의 영구 복사본을 저장하지 않도록 알리는 데 사용됩니다.

## <a name="varying-the-output-cache"></a>출력 캐시 변경

경우에 따라 동일한 콘텐츠의 다른 캐시 된 버전을 원할 수 있습니다. 예를 들어 마스터/세부 정보 페이지를 만드는 경우를 가정해 보겠습니다. 마스터 페이지에는 영화 제목 목록이 표시됩니다. 제목을 클릭하면 선택한 동영상에 대한 세부 정보가 표시됩니다.

세부 정보 페이지를 캐시하면 클릭한 동영상에 관계없이 동일한 동영상에 대한 세부 정보가 표시됩니다. 첫 번째 사용자가 선택한 첫 번째 동영상이 모든 향후 사용자에게 표시됩니다.

[OutputCache] 특성의 VaryByParam 속성을 활용하여 이 문제를 해결할 수 있습니다. 이 속성을 사용하면 양식 매개 변수 또는 쿼리 문자열 매개 변수가 다를 때 동일한 콘텐츠의 다른 캐시된 버전을 만들 수 있습니다.

예를 들어 목록 5의 컨트롤러는 Master() 및 Details()라는 두 개의 작업을 노출합니다. 마스터() 작업은 동영상 제목 목록을 반환하고 세부 정보() 작업은 선택한 동영상에 대한 세부 정보를 반환합니다.

**목록 5 – 컨트롤러\영화Controller.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

마스터() 작업에는 값이 "none"인 VaryByParam 속성이 포함됩니다. Master() 작업이 호출되면 동일한 캐시된 버전의 마스터 뷰가 반환됩니다. 모든 양식 매개 변수 또는 쿼리 문자열 매개 변수는 무시됩니다(그림 2 참조).

**그림 2 – /영화/마스터 보기**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**그림 3 – /영화/세부 정보 보기**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

세부 정보() 작업에는 값 "Id"가 있는 VaryByParam 속성이 포함됩니다. Id 매개 변수의 다른 값이 컨트롤러 작업에 전달되면 세부 정보 보기의 다른 캐시된 버전이 생성됩니다.

VarByParam 속성을 사용하면 캐싱이 더 많아지고 더 적지 않다는 것을 이해하는 것이 중요합니다. 세부 정보 보기의 다른 캐시된 버전이 Id 매개 변수의 각 다른 버전에 대해 만들어집니다.

[바바이파라임] 속성을 다음 값으로 설정할 수 있습니다.

> \*= 양식 또는 쿼리 문자열 매개 변수가 다를 때마다 다른 캐시된 버전을 만듭니다.
> 
> 없음 = 다른 캐시된 버전을 만들지 마십시오.
> 
> 세미콜론 매개 변수 목록 = 목록의 양식 또는 쿼리 문자열 매개 변수가 다를 때마다 다른 캐시된 버전 만들기

## <a name="creating-a-cache-profile"></a>캐시 프로필 만들기

[OutputCache] 특성의 속성을 수정하여 출력 캐시 속성을 구성하는 대신 웹 구성(web.config) 파일에서 캐시 프로필을 만들 수 있습니다. 웹 구성 파일에 캐시 프로필을 만들면 몇 가지 중요한 이점이 있습니다.

먼저 웹 구성 파일에서 출력 캐싱을 구성하여 컨트롤러 작업이 한 중앙 위치에서 콘텐츠를 캐시하는 방법을 제어할 수 있습니다. 하나의 캐시 프로필을 만들고 프로파일을 여러 컨트롤러 또는 컨트롤러 작업에 적용할 수 있습니다.

둘째, 응용 프로그램을 다시 컴파일하지 않고 웹 구성 파일을 수정할 수 있습니다. 프로덕션에 이미 배포된 응용 프로그램에 대해 캐싱을 사용하지 않도록 설정해야 하는 경우 웹 구성 파일에 정의된 캐시 프로필을 수정하기만 하면 됩니다. 웹 구성 파일에 대한 모든 변경 내용이 자동으로 감지되고 적용됩니다.

예를 들어 &lt;목록&gt; 6의 웹 구성 섹션은 Cache1Hour라는 캐시 프로필을 정의합니다. 캐싱 &lt;&gt; 섹션은 웹 &lt;구성 파일의 system.web&gt; 섹션내에 나타나야 합니다.

**목록 6 – web.config에 대 한 캐싱 섹션**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

목록 7의 컨트롤러는 [OutputCache] 특성을 사용하여 컨트롤러 작업에 Cache1Hour 프로파일을 적용하는 방법을 보여 줍니다.

**목록 7 – 컨트롤러\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

목록 7의 컨트롤러가 노출한 Index() 작업을 호출하면 동일한 시간이 1시간 동안 반환됩니다.

## <a name="summary"></a>요약

출력 캐싱은 ASP.NET MVC 응용 프로그램의 성능을 크게 향상시키는 매우 쉬운 방법을 제공합니다. 이 자습서에서는 [OutputCache] 특성을 사용하여 컨트롤러 작업의 출력을 캐시하는 방법을 배웠습니다. 또한 기간 및 [OutputCache] 특성의 속성을 수정하여 콘텐츠가 캐시되는 방식을 수정하는 방법도 배웠습니다. 마지막으로 웹 구성 파일에서 캐시 프로필을 정의하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](understanding-action-filters-cs.md)
> [다음](adding-dynamic-content-to-a-cached-page-cs.md)
