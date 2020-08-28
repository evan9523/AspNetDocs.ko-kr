---
uid: mvc/overview/getting-started/introduction/adding-search
title: 검색 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044923"
---
# <a name="search"></a>검색

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 보기 추가

이 섹션에서는 `Index` 장르 또는 이름을 기준으로 영화를 검색할 수 있는 작업 메서드에 검색 기능을 추가 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 섹션의 스크린샷을 일치 시키려면 응용 프로그램을 실행 (F5) 하 고 다음 영화를 데이터베이스에 추가 해야 합니다.

| 제목 | 릴리스 날짜: | Genre | 가격 |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | 코미디 | 6.99 |
| Ghostbusters II | 6/16/1989 | 코미디 | 6.99 |
| Apes의 행성 | 3/27/1986 | 작업 | 5.99 |

## <a name="updating-the-index-form"></a>인덱스 폼 업데이트

먼저 `Index` 작업 메서드를 기존 `MoviesController` 클래스로 업데이트 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

메서드의 첫 번째 줄에서는 `Index` 다음 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리를 만들어 영화를 선택 합니다.

[!code-csharp[Main](adding-search/samples/sample2.cs)]

쿼리가이 시점에 정의 되었지만 아직 데이터베이스에 대해 실행 되지 않았습니다.

`searchString`매개 변수에 문자열이 포함 된 경우 다음 코드를 사용 하 여 검색 문자열의 값을 필터링 하도록 동영상 쿼리를 수정 합니다.

[!code-csharp[Main](adding-search/samples/sample3.cs)]

위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다. 람다 식은 메서드 기반 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리에서 위의 코드에서 사용 된 [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 메서드와 같은 표준 쿼리 연산자 메서드의 인수로 사용 됩니다. LINQ 쿼리는 정의 될 때 또는 또는와 같은 메서드를 호출 하 여 수정 될 때 실행 되지 `Where` 않습니다 `OrderBy` . 대신 쿼리 실행이 지연 됩니다. 즉, 실현 된 값이 실제로 반복 되거나 메서드가 호출 될 때까지 식의 계산이 지연 됩니다 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `Search`이 샘플에서 쿼리는 *인덱스. cshtml* 뷰에서 실행 됩니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

> [!NOTE]
> [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 메서드는 위의 c # 코드가 아닌 데이터베이스에서 실행 됩니다. 데이터베이스에서 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 는 대/소문자를 구분 하지 않는 [SQL과](https://msdn.microsoft.com/library/ms179859.aspx)매핑됩니다.

이제 `Index` 사용자에 게 폼을 표시 하는 뷰를 업데이트할 수 있습니다.

응용 프로그램을 실행 하 고 */Movies/Index*로 이동 합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 영화가 표시됩니다.

![SearchQryStr](adding-search/_static/image1.png)

`Index`이라는 매개 변수를 포함 하도록 메서드의 시그니처를 변경 하는 경우 `id` `id` 매개 변수는 `{id}` *App \_ Start\RouteConfig.cs* 파일에 설정 된 기본 경로에 대 한 자리 표시자와 일치 합니다.

[!code-json[Main](adding-search/samples/sample4.txt)]

원래 메서드는 다음과 같습니다 `Index` .

[!code-csharp[Main](adding-search/samples/sample5.cs)]

수정 된 메서드는 다음과 같습니다 `Index` .

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

이제 쿼리 문자열 값 대신 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

![](adding-search/_static/image2.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하리라고 기대하지는 않을 것입니다. 따라서 이제 영화를 필터링하는 데 도움이 되는 UI를 추가합니다. 메서드의 서명을 변경 하 여 `Index` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 경우 `Index` 메서드가 라는 문자열 매개 변수를 사용 하도록 다시 변경 합니다 `searchString` .

[!code-csharp[Main](adding-search/samples/sample7.cs)]

*Views\Movies\Index.cshtml* 파일을 열고 바로 뒤에 `@Html.ActionLink("Create New", "Create")` 아래에 강조 표시 된 폼 태그를 추가 합니다.

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

`Html.BeginForm`도우미는 여는 태그를 만듭니다 `<form>` . 도우미를 사용 하면 `Html.BeginForm` 사용자가 **필터** 단추를 클릭 하 여 양식을 전송할 때 폼이 자신에 게 게시 됩니다.

Visual Studio 2013 보기 파일을 표시 하 고 편집할 때 향상 된 기능이 있습니다. 뷰 파일이 열려 있는 상태에서 응용 프로그램을 실행 하면 Visual Studio 2013 올바른 컨트롤러 작업 메서드를 호출 하 여 뷰를 표시 합니다.

![](adding-search/_static/image3.png)

위의 이미지에 표시 된 것 처럼 Visual Studio에서 인덱스 뷰가 열린 상태에서 Ctr F5 또는 F5 키를 눌러 응용 프로그램을 실행 한 다음 영화 검색을 시도 합니다.

![](adding-search/_static/image4.png)

`HttpPost`메서드의 오버 로드가 없습니다 `Index` . 메서드가 응용 프로그램의 상태를 변경 하는 것이 아니라 데이터만 필터링 하기 때문에 필요 하지 않습니다.

다음 `HttpPost Index` 메서드를 추가할 수 있습니다. 이 경우 작업 호출자는 `HttpPost Index` 메서드와 일치 하 고 `HttpPost Index` 메서드는 아래 이미지와 같이 실행 됩니다.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

그러나 이 `HttpPost` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST 요청에 대 한 URL은 GET 요청 (localhost: xxxxx/영화/인덱스)의 URL과 동일 합니다. URL 자체에는 검색 정보가 없습니다. 지금은 검색 문자열 정보가 양식 필드 값으로 서버에 전송 됩니다. 즉, 책갈피에 대 한 검색 정보를 캡처하거나 URL의 친구에 게 보낼 수 없습니다.

이 솔루션은 `BeginForm` POST 요청에서 검색 정보를 URL에 추가 하 고이를 메서드 버전으로 라우팅해야 함을 지정 하는의 오버 로드를 사용 하는 것입니다 `HttpGet` `Index` . 매개 변수가 없는 기존 `BeginForm` 메서드를 다음 태그로 바꿉니다.

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

이제 검색을 제출할 때 URL에 검색 쿼리 문자열이 포함 됩니다. `HttpPost Index` 메서드가 존재하더라도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>장르 별 검색 추가

`HttpPost`메서드 버전을 추가한 경우 `Index` 지금 삭제 합니다.

다음으로, 사용자가 장르로 영화를 검색할 수 있는 기능을 추가 합니다. `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-search/samples/sample11.cs)]

이 버전의 `Index` 메서드는 추가 매개 변수를 사용 `movieGenre` 합니다. 즉, 코드의 처음 몇 줄은 개체를 만들어 `List` 데이터베이스에서 영화 장르를 보관 합니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

코드는 `AddRange` 제네릭 컬렉션의 메서드를 사용 하 여 `List` 모든 고유 장르를 목록에 추가 합니다. 한정자를 사용 하지 않고 `Distinct` 중복 장르를 추가 합니다. 예를 들어 코미디는 샘플에서 두 번 추가 됩니다. 그런 다음 코드는 장르 목록을 개체에 저장 합니다 `ViewBag.MovieGenre` . 에서 범주 데이터 (예: 영화 장르)를 [selectlist](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 개체로 저장 `ViewBag` 한 다음 드롭다운 목록 상자에서 범주 데이터에 액세스 하는 것은 MVC 응용 프로그램에 대 한 일반적인 방법입니다.

다음 코드에서는 매개 변수를 확인 하는 방법을 보여 줍니다 `movieGenre` . 비어 있지 않은 경우 코드는 선택한 영화를 지정 된 장르로 제한 하도록 동영상 쿼리를 추가로 제한 합니다.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

앞에서 설명한 것 처럼, 작업 메서드가 반환 된 후 보기에서 발생 하는 동영상 목록이 반복 될 때까지 데이터베이스에서 쿼리가 실행 되지 않습니다 `Index` .

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>장르 검색을 지원 하기 위해 인덱스 뷰에 태그 추가

도우미 `Html.DropDownList` 바로 앞에 *Views\Movies\Index.cshtml* 파일에 도우미를 추가 `TextBox` 합니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

다음 코드에서:

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

"MovieGenre" 매개 변수는 `DropDownList` 도우미가에서을 찾을 수 있는 키를 제공 합니다 `IEnumerable<SelectListItem>` `ViewBag` . `ViewBag`작업 메서드에서가 입력 되었습니다.

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

"All" 매개 변수는 옵션 레이블을 제공 합니다. 브라우저에서 해당 선택을 검사 하면 해당 "value" 특성이 비어 있는 것을 볼 수 있습니다. 컨트롤러는 문자열을 필터링 `if` 하거나 비어 있지 않으므로 `null` 에 대해 빈 값을 제출 하면 `movieGenre` 모든 장르를 표시 합니다.

옵션이 기본적으로 선택 되도록 설정할 수도 있습니다. 기본 옵션으로 "코미디"을 원하는 경우 컨트롤러의 코드를 다음과 같이 변경 합니다.

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

응용 프로그램을 실행 하 고 */Movies/Index*로 이동 합니다. 장르, 영화 이름 및 두 조건에 따라 검색을 수행 합니다.

![](adding-search/_static/image8.png)

이 섹션에서는 사용자가 영화 제목 및 장르로 검색할 수 있는 검색 작업 메서드 및 보기를 만들었습니다. 다음 섹션에서는 모델에 속성을 추가 하는 방법 `Movie` 및 테스트 데이터베이스를 자동으로 만드는 이니셜라이저를 추가 하는 방법을 살펴봅니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-a-new-field.md)
