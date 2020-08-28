---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2에서 특성 라우팅을 사용 하 여 REST API 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045184"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 특성 라우팅을 사용 하 여 REST API 만들기

[Mike Wasson](https://github.com/MikeWasson)

Web API 2는 *특성 라우팅*이라는 새로운 유형의 라우팅을 지원 합니다. 특성 라우팅에 대 한 일반적인 개요는 [WEB API 2에서 특성 라우팅](attribute-routing-in-web-api-2.md)을 참조 하세요. 이 자습서에서는 특성 라우팅을 사용 하 여 책 컬렉션에 대 한 REST API를 만듭니다. API는 다음 작업을 지원 합니다.

| 작업 | 예제 URI |
| --- | --- |
| 모든 책의 목록을 가져옵니다. | /api/서적 |
| ID 별로 책을 가져옵니다. | /api/books/1 |
| 책의 세부 정보를 가져옵니다. | /api/books/1/details |
| 장르별로 책 목록을 가져옵니다. | /api/books/fantasy |
| 게시 날짜별로 책 목록을 가져옵니다. | /api/books/date/2013-02-16/api/books/date/2013/02/16 (대체 양식) |
| 특정 저자의 책 목록을 가져옵니다. | /api/authors/1/books |

모든 메서드는 읽기 전용입니다 (HTTP GET 요청).

데이터 계층의 경우 Entity Framework를 사용 합니다. 책 레코드에는 다음 필드가 포함 됩니다.

- ID
- 제목
- Genre
- 게시 날짜
- 가격
- 설명
- AuthorID (외래 키를 Authors 테이블로)

그러나 대부분의 요청에서 API는이 데이터의 하위 집합 (제목, 저자 및 장르)을 반환 합니다. 전체 레코드를 가져오기 위해 클라이언트는를 요청 `/api/books/{id}/details` 합니다.

## <a name="prerequisites"></a>필수 구성 요소

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition입니다.

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio를 실행 하 여 시작 합니다. **파일** 메뉴에서 **새로 만들기**를 선택한 후 **프로젝트**를 선택합니다.

**설치 된**  >  **Visual c #** 범주를 확장 합니다. **Visual c #** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 을 선택 합니다. 프로젝트 이름을 &quot; booksapi로 &quot; 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

**새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **빈** 템플릿을 선택 합니다. "에 대 한 폴더 및 핵심 참조 추가"에서 **WEB API** 확인란을 선택 합니다. **확인**을 클릭합니다.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

이렇게 하면 Web API 기능에 대해 구성 된 기본 프로젝트가 생성 됩니다.

### <a name="domain-models"></a>도메인 모델

다음으로 도메인 모델에 대 한 클래스를 추가 합니다. 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가**를 선택한 다음 **클래스**를 선택 합니다. 클래스 `Author` 이름을 지정합니다.

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Author.cs의 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

이제 라는 다른 클래스 `Book` 를 추가 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Web API 컨트롤러 추가

이 단계에서는 Entity Framework를 데이터 계층으로 사용 하는 Web API 컨트롤러를 추가 합니다.

Ctrl+Shift+B를 눌러 프로젝트를 빌드합니다. Entity Framework는 리플렉션을 사용 하 여 모델의 속성을 검색 하므로 데이터베이스 스키마를 만들기 위해 컴파일된 어셈블리가 필요 합니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가**를 선택한 다음 **컨트롤러**를 선택 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

**스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 웹 API 2 컨트롤러 (작업 포함**)를 선택 합니다.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

**컨트롤러 추가** 대화 상자에서 **컨트롤러 이름**에 &quot; bookscontroller를 입력 &quot; 합니다. &quot;비동기 컨트롤러 작업 사용 확인란을 선택 &quot; 합니다. **모델 클래스**에 대해 Book을 선택 &quot; &quot; 합니다. 드롭다운에 나열 된 클래스가 표시 되지 않는 경우 `Book` 프로젝트를 빌드 했는지 확인 합니다. 그런 다음 "+" 단추를 클릭 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

**새 데이터 컨텍스트** 대화 상자에서 **추가** 를 클릭 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

**컨트롤러 추가** 대화 상자에서 **추가** 를 클릭 합니다. 스 캐 폴딩은 `BooksController` API 컨트롤러를 정의 하는 라는 클래스를 추가 합니다. 또한 `BooksAPIContext` Entity Framework의 데이터 컨텍스트를 정의 하는 모델 폴더에 라는 클래스를 추가 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>데이터베이스 시드

도구 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

이 명령은 마이그레이션 폴더를 만들고 Configuration.cs 라는 새 코드 파일을 추가 합니다. 이 파일을 열고 다음 코드를 메서드에 추가 합니다 `Configuration.Seed` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

이러한 명령은 로컬 데이터베이스를 만들고 초기값 메서드를 호출 하 여 데이터베이스를 채웁니다.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>DTO 클래스 추가

지금 응용 프로그램을 실행 하 고/api/books/1에 GET 요청을 보내면 응답이 다음과 같이 표시 됩니다. (가독성을 위해 들여쓰기를 추가 했습니다.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

대신이 요청에서 필드의 하위 집합을 반환 하려고 합니다. 작성자 ID 대신 작성자의 이름도 반환 하려고 합니다. 이를 위해 EF 모델 대신 DTO ( *데이터 전송 개체* )를 반환 하도록 컨트롤러 메서드를 수정 합니다. DTO은 데이터를 전달 하기 위해 디자인 된 개체입니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  |  **새 폴더**를 선택 합니다. 폴더 이름을 &quot; dto로 &quot; 합니다. 다음 정의를 사용 하 여 라는 클래스를 `BookDto` dto 폴더에 추가 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

`BookDetailDto`(이)라는 다른 클래스를 추가합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

그런 다음 인스턴스를 `BooksController` 반환 하도록 클래스를 업데이트 합니다 `BookDto` . 쿼리할 수 있는 [. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 메서드를 사용 하 여 인스턴스 `Book` 를 `BookDto` 인스턴스에 프로젝션 합니다. 컨트롤러 클래스에 대 한 업데이트 된 코드는 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> `PutBook`, `PostBook` 및 `DeleteBook` 메서드는이 자습서에 필요 하지 않기 때문에 삭제 되었습니다.

이제 응용 프로그램을 실행 하 고/api/books/1를 요청 하면 응답 본문은 다음과 같습니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>경로 특성 추가

다음으로, 특성 라우팅을 사용 하도록 컨트롤러를 변환 합니다. 먼저 컨트롤러에 **RoutePrefix** 특성을 추가 합니다. 이 특성은이 컨트롤러의 모든 메서드에 대 한 초기 URI 세그먼트를 정의 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

그런 다음 다음과 같이 **[Route]** 특성을 컨트롤러 작업에 추가 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

각 컨트롤러 메서드의 경로 템플릿은 접두사와 **경로** 특성에 지정 된 문자열입니다. 메서드의 경우 `GetBook` 경로 템플릿에는 &quot; &quot; URI 세그먼트에 정수 값이 포함 된 경우와 일치 하는 매개 변수가 있는 문자열 {id: int}가 포함 됩니다.

| 방법 | 경로 템플릿 | 예제 URI |
| --- | --- | --- |
| `GetBooks` | "api/서적" | `http://localhost/api/books` |
| `GetBook` | "api/books/{id: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>책 정보 가져오기

책 정보를 얻기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/books/{id}/details` . 여기서 *{id}* 는 책의 id입니다.

`BooksController` 클래스에 다음 메서드를 추가합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

를 요청 하 `/api/books/1/details` 는 경우 응답은 다음과 같습니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>장르 별 서적 가져오기

특정 장르에서 책 목록을 가져오기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/books/genre` . 여기서 *장르* 는 장르 이름입니다. (예: `/api/books/fantasy`)

에 다음 메서드를 추가 `BooksController` 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

여기서는 URI 템플릿에서 {장르} 매개 변수를 포함 하는 경로를 정의 합니다. Web API는 이러한 두 Uri를 구분 하 고 다른 메서드로 라우팅할 수 있습니다.

`/api/books/1`

`/api/books/fantasy`

이는 메서드는 `GetBook` "id" 세그먼트가 정수 값 이어야 하는 제약 조건을 포함 하기 때문입니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

/Api/books/fantasy를 요청 하는 경우 응답은 다음과 같습니다.

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>저자 별 책 가져오기

특정 저자에 대 한 책 목록을 가져오기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/authors/id/books` . 여기서 *id* 는 저자의 id입니다.

에 다음 메서드를 추가 `BooksController` 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

이 예제는 &quot; 책 &quot; 이 저자 들의 자식 리소스로 처리 되기 때문에 흥미롭습니다 &quot; &quot; . 이 패턴은 RESTful Api에서 매우 일반적입니다.

경로 템플릿의 물결표 (~)는 **RoutePrefix** 특성의 경로 접두사를 재정의 합니다.

## <a name="get-books-by-publication-date"></a>게시 날짜별 서적 가져오기

게시 날짜별로 책 목록을 가져오려면 클라이언트는에 GET 요청을 보냅니다 `/api/books/date/yyyy-mm-dd` . 여기서 *yyyy-mm-dd* 는 날짜입니다.

이 작업을 수행 하는 한 가지 방법은 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`매개 변수는 **DateTime** 값과 일치 하도록 제한 됩니다. 이는 작동 하지만 실제로는 원하는 것 보다 더 허용 됩니다. 예를 들어 다음 Uri는 경로와 일치 합니다.

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

이러한 Uri를 허용 하는 것이 잘못 되었습니다. 그러나 경로 템플릿에 정규식 제약 조건을 추가 하 여 경로를 특정 형식으로 제한할 수 있습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

이제 &quot; yyyy-mm-dd 형식의 날짜만 &quot; 일치 합니다. 정규식을 사용 하 여 실제 날짜의 유효성을 검사 하지 않습니다. Web API가 URI 세그먼트를 **DateTime** 인스턴스로 변환 하려고 할 때 처리 됩니다. ' 2012-47-99 '과 같은 잘못 된 날짜는 변환 되지 않으므로 클라이언트에서 404 오류가 발생 합니다.

다른 regex를 사용 하 여 `/api/books/date/yyyy/mm/dd` 다른 **[Route]** 특성을 추가 하 여 슬래시 구분 기호 ()를 지원할 수도 있습니다.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

여기에는 미묘한 중요 한 세부 정보가 있습니다. 두 번째 경로 템플릿의 \* {pubdate} 매개 변수 시작 부분에 와일드 카드 문자 ()가 있습니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

이렇게 하면 {pubdate}가 URI의 나머지 부분과 일치 해야 한다는 것을 라우팅 엔진에 알립니다. 기본적으로 템플릿 매개 변수는 단일 URI 세그먼트와 일치 합니다. 이 경우에는 {pubdate}를 여러 개의 URI 세그먼트로 확장 하려고 합니다.

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>컨트롤러 코드

BooksController 클래스에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>요약

특성 라우팅은 API에 대 한 Uri를 설계할 때 더 많은 제어와 유연성을 제공 합니다.
