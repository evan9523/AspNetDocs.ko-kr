---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamic v. 강력한 형식의 뷰 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702948"
---
# <a name="dynamic-v-strongly-typed-views"></a>Dynamic v. 강력한 형식의 보기

[Rick Anderson](https://twitter.com/RickAndMSFT)

다음 세 가지 방법으로 컨트롤러에서 ASP.NET MVC 3의 뷰로 정보를 전달할 수 있습니다.

1. 강력한 형식의 모델 개체입니다.
2. 동적 형식 ( @model 동적 사용)
3. ViewBag 사용

동적 및 강력한 형식의 뷰를 비교 하 고 대조 하는 간단한 MVC 3 최상위 블로그 응용 프로그램을 작성 했습니다. 컨트롤러는 간단한 블로그 목록으로 시작 합니다.

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

IndexNotStonglyTyped 된 () 메서드를 마우스 오른쪽 단추로 클릭 하 고 Razor 뷰를 추가 합니다.

[![8475 NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

**강력한 형식의 뷰 만들기** 상자가 선택 되어 있지 않은지 확인 합니다. 결과 보기에는 많은 정보가 포함 되지 않습니다.

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

강력한 형식의 뷰가 아닌 동적을 사용 하기 때문에 intellisense는 유용 하지 않습니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646 [1] NotStronglyTypedView_5F00_IE](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

이제 강력한 형식의 뷰를 추가 합니다. 컨트롤러에 다음 코드를 추가 합니다.

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

정확 하 게 동일한 반환 뷰 (topBlogs)를 확인 합니다. 를 비 강력한 형식의 뷰로 호출 합니다. *StonglyTypedIndex ()* 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다. 이번에는 **블로그** 모델 클래스를 선택 하 고 스 캐 폴드 템플릿으로 **목록** 을 선택 합니다.

[![5658 StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

새 보기 템플릿 내에서 intellisense 지원을 받게 됩니다.

[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)
