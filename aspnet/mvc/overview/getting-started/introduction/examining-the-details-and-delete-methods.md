---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: 세부 정보 및 삭제 메서드 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 9c4e66454d6995bd750b62ef8b461bcfbdfb4b4f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045093"
---
# <a name="examining-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드 검사

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

자습서의이 부분에서는 자동으로 생성 된 및 메서드를 검사 `Details` 합니다 `Delete` .

## <a name="examining-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드 검사

컨트롤러를 열고 `Movie` 메서드를 검사 `Details` 합니다.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

이 작업 메서드를 만든 MVC 스 캐 폴딩 엔진은 메서드를 호출 하는 HTTP 요청을 보여 주는 주석을 추가 합니다. 이 경우 `GET` 세 개의 URL 세그먼트 ( `Movies` 컨트롤러, 메서드 및 값)가 포함 된 요청 `Details` `ID` 입니다.

Code First를 사용 하면 메서드를 사용 하 여 데이터를 쉽게 검색할 수 `Find` 있습니다. 메서드에 기본 제공 되는 중요 한 보안 기능은 코드가 `Find` 코드에서 작업을 수행 하려고 시도 하기 전에 메서드가 영화를 발견 했는지 확인 하는 것입니다. 예를 들어 해커는 링크로 만든 URL을에서 `http://localhost:xxxx/Movies/Details/1` `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화를 나타내지 않는 다른 값)로 변경 하 여 사이트에 오류를 발생 시킬 수 있습니다. Null 동영상을 검사 하지 않은 경우에는 null 영화에서 데이터베이스 오류가 발생 합니다.

`Delete` 및 `DeleteConfirmed` 메서드를 검토합니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

HTTP GET `Delete` 메서드는 지정 된 동영상을 삭제 하지 않으며 삭제를 제출 () 할 수 있는 동영상 뷰를 반환 합니다 `HttpPost` . GET 요청에 대한 응답에서 삭제 작업을 수행하는 것은(또는 해당 문제에 대한 편집 작업, 만들기 작업 또는 데이터를 변경하는 기타 작업을 수행하는 것은) 보안 허점을 야기합니다. 이에 대 한 자세한 내용은 Stephen Walther의 블로그 항목 [ASP.NET MVC 팁 #46를 참조 하세요. 보안 허점을 만들기 때문에 Delete 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

데이터를 삭제하는 `HttpPost` 메서드의 이름은 HTTP POST 메서드에 고유한 서명 또는 이름을 부여하기 위해 `DeleteConfirmed`로 지정됩니다. 두 메서드의 서명은 다음과 같습니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

CLR(공용 언어 런타임)은 고유한 매개 변수 서명을 갖기 위해 오버로드된 메서드가 필요합니다(동일한 메서드 이름이지만 다른 매개 변수의 목록). 그러나 여기에서 두 개의 Delete 메서드 (GET의 경우 하나, POST의 경우 one)는 동일한 매개 변수 시그니처를 갖고 있어야 합니다. (모두 매개 변수로 단일 정수를 허용해야 합니다.)

이를 정렬 하기 위해 몇 가지 작업을 수행할 수 있습니다. 하나는 메서드에 다른 이름을 지정 하는 것입니다. 앞의 예에서 스캐폴딩 메커니즘이 수행한 것입니다. 그러나 이는 작은 문제를 야기합니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다. 솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다. 이렇게 하면 POST 요청에 대 한 */Delete/* 포함 된 URL에서 메서드를 찾을 수 있도록 라우팅 시스템에 대 한 매핑이 효과적으로 수행 됩니다 `DeleteConfirmed` .

동일한 이름 및 서명을 가진 메서드의 문제를 방지 하는 또 다른 일반적인 방법은 사용 하지 않는 매개 변수를 포함 하도록 POST 메서드의 서명을 인위적으로 변경 하는 것입니다. 예를 들어, 일부 개발자는 POST 메서드로 전달 되는 매개 변수 형식을 추가한 `FormCollection` 다음 매개 변수를 사용 하지 않습니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>요약

이제 로컬 DB 데이터베이스에 데이터를 저장 하는 완전 한 ASP.NET MVC 응용 프로그램이 있습니다. 영화를 만들고, 읽고, 업데이트 하 고, 삭제 하 고, 검색할 수 있습니다.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>다음 단계

웹 응용 프로그램을 빌드 및 테스트 한 후에는 다른 사용자가 인터넷을 통해 사용할 수 있도록 다음 단계를 수행 합니다. 이렇게 하려면 웹 호스팅 공급자에 배포 해야 합니다. Microsoft는 [무료 Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)에 최대 10 개의 웹 사이트를 제공 하는 무료 웹 호스팅을 제공 합니다. 다음에 나오는 자습서에 따라 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure에 보안 ASP.NET MVC 앱을 배포 하는 것이](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)좋습니다. 뛰어난 자습서는 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Tom Dykstra의 중간 수준입니다. [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 은 질문을 할 수 있는 좋은 장소입니다. twitter에서 [저](https://twitter.com/RickAndMSFT)를 팔로우하시면 최신 자습서 업데이트를 받으실 수 있습니다.

사용자 의견을 환영 합니다.

- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
- [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [이전](adding-validation.md)
