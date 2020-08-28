---
uid: mvc/overview/getting-started/introduction/adding-validation
title: 유효성 검사 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044352"
---
# <a name="adding-validation"></a>유효성 검사 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 섹션에서는 모델에 유효성 검사 논리를 추가 하 `Movie` 고, 사용자가 응용 프로그램을 사용 하 여 동영상을 만들거나 편집 하려고 할 때마다 유효성 검사 규칙이 적용 되도록 합니다.

## <a name="keeping-things-dry"></a>작업 건조 유지

ASP.NET MVC의 핵심 디자인 개념 중 하나는 [마른](http://en.wikipedia.org/wiki/Don't_repeat_yourself) ( &quot; 반복 금지)입니다 &quot; . ASP.NET MVC는 기능이 나 동작을 한 번만 지정한 다음 응용 프로그램의 모든 위치에 반영 되도록 권장 합니다. 이렇게 하면 작성 해야 하는 코드의 양이 줄어들고 오류가 발생 하기 쉬우며 더 쉽게 유지 관리할 수 있는 코드를 만들 수 있습니다.

ASP.NET MVC 및 Entity Framework Code First에서 제공 하는 유효성 검사 지원은 작동 중인 마른 원칙의 좋은 예입니다. 모델 클래스의 한 위치에서 유효성 검사 규칙을 선언적으로 지정할 수 있으며, 규칙은 응용 프로그램의 모든 위치에서 적용 됩니다.

영화 응용 프로그램에서이 유효성 검사 지원을 활용할 수 있는 방법을 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>무비 모델에 유효성 검사 규칙 추가

먼저 클래스에 유효성 검사 논리를 추가 `Movie` 합니다.

*Movie.cs* 파일을 엽니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)네임 스페이스에가 포함 되어 있지 않습니다 `System.Web` . DataAnnotations은 모든 클래스나 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 집합을 제공 합니다. 서식 지정에 도움이 되 고 유효성 검사를 제공 하지 않는 [데이터](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 형식과 같은 서식 특성도 포함 됩니다.

이제 `Movie` 기본 제공 [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) , [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)및 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성을 활용 하도록 클래스를 업데이트 합니다. 클래스를 `Movie` 다음으로 바꿉니다.

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

[`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)특성은 문자열의 최대 길이를 설정 하 고 데이터베이스에 대해이 제한을 설정 하므로 데이터베이스 스키마가 변경 됩니다. **서버 탐색기** 에서 **영화** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열기**를 클릭 합니다.

![](adding-validation/_static/image1.png)

위의 이미지에서 모든 문자열 필드가 [NVARCHAR (MAX)](https://technet.microsoft.com/library/ms186939.aspx)로 설정 된 것을 볼 수 있습니다. 마이그레이션을 사용 하 여 스키마를 업데이트 합니다. 솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 열고 다음 명령을 입력 합니다.

[!code-console[Main](adding-validation/samples/sample2.cmd)]

이 명령이 완료 되 면 Visual Studio는 지정 된 이름 ()으로 새 파생 클래스를 정의 하는 클래스 파일을 열고 `DbMigration` `DataAnnotations` , `Up` 메서드에서 스키마 제약 조건을 업데이트 하는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

`Genre`이 필드는 더 이상 null을 허용 하지 않습니다. 즉, 값을 입력 해야 합니다. `Rating`필드의 최대 길이는 5이 고 `Title` 최대 길이는 60입니다. 의 최소 길이는 3이 `Title` 고 범위는 `Price` 스키마 변경을 만들지 않습니다.

동영상 스키마를 검사 합니다.

![](adding-validation/_static/image2.png)

문자열 필드는 새 길이 제한을 표시 하 고 `Genre` 더 이상 nullable로 확인 되지 않습니다.

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 및 `MinimumLength` 특성은 속성에 값이 있어야 하지만 사용자가 이 유효성 검사를 만족하기 위해 공백을 입력하는 것을 예방할 수 없다는 것을 나타냅니다. [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성은 입력할 수 있는 문자를 제한 하는 데 사용 됩니다. 위의 코드에서 `Genre` 및 `Rating`은 문자만을 사용해야 합니다(공백, 숫자 및 특수 문자가 허용되지 않음). [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)특성은 지정 된 범위 내에서 값을 제한 합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 그리고 필요에 따라 최소 길이를 설정할 수 있습니다. 값 형식 (예: `decimal, int, float, DateTime` )은 기본적으로 필요 하며 특성은 필요 하지 않습니다 `Required` .

Code First를 사용 하면 응용 프로그램에서 데이터베이스의 변경 내용을 저장 하기 전에 모델 클래스에서 지정 하는 유효성 검사 규칙이 적용 됩니다. 예를 들어, 다음 코드는 메서드가 호출 될 때 [Dbentityvalidationexception](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) 예외를 throw 합니다 `SaveChanges` . 몇 가지 필수 `Movie` 속성 값이 누락 되었기 때문입니다.

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

위의 코드는 다음과 같은 예외를 throw 합니다.

*하나 이상의 엔터티에 대 한 유효성 검사에 실패 했습니다. 자세한 내용은 ' EntityValidationErrors ' 속성을 참조 하세요.*

.NET Framework에 의해 자동으로 적용 되는 유효성 검사 규칙이 있으면 응용 프로그램을 더욱 강력 하 게 만들 수 있습니다. 또한 무언가의 유효성 검사를 잊거나, 실수로 데이터베이스에 불량 데이터가 들어가지 않도록 할 수 있습니다.

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC의 유효성 검사 오류 UI

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다.

새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다. 일부 잘못된 값으로 양식을 기입합니다. jQuery 클라이언트 쪽 유효성 검사가 오류를 감지하자마자 오류 메시지를 표시합니다.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> 소수점에 쉼표 (",")를 사용 하는 영어가 아닌 로캘에서 jQuery 유효성 검사를 지원 하려면이 자습서의 앞부분에서 설명한 대로 NuGet 세계화를 포함 해야 합니다.

양식에서 자동으로 빨간색 테두리 색을 사용 하 여 잘못 된 데이터를 포함 하 고 각 텍스트 상자 옆에 적절 한 유효성 검사 오류 메시지를 내보낸 텍스트 상자를 강조 표시 하는 방법을 확인 합니다. 오류는 클라이언트 쪽(JavaScript 및 jQuery 사용 시) 및 서버 쪽(사용자가 JavaScript를 사용하지 않도록 설정한 경우) 모두에서 발생합니다.

실제 혜택은 `MoviesController` 이 유효성 검사 UI를 사용 하도록 설정 하기 위해 클래스 또는 *Create. cshtml* 뷰에서 한 줄의 코드를 변경 하지 않아도 된다는 것입니다. 이 자습서에서 이전에 만든 컨트롤러 및 보기는 `Movie` 모델 클래스의 속성에 유효성 검사 특성을 사용하여 지정한 유효성 검사 규칙을 자동으로 가져옵니다. `Edit` 작업 메서드로 유효성 검사를 테스트하여 동일한 유효성 검사가 적용되는지 확인해보세요.

양식 데이터는 클라이언트 쪽 유효성 검사 오류가 없을 때까지 서버에 전송되지 않습니다. [Fiddler 도구](http://fiddler2.com/fiddler2/)또는 IE [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478)를 사용 하 여 HTTP Post 메서드에 중단점을 배치 하 여이를 확인할 수 있습니다.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View 및 Create Action 메서드에서 유효성 검사를 수행 하는 방법

컨트롤러나 보기의 코드를 전혀 수정하지 않고도 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록에서는 `Create` 클래스의 메서드 모양을 보여 줍니다 `MovieController` . 이 자습서의 앞부분에서 만든 방법에서 변경 되지 않았습니다.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

첫 번째(HTTP GET) `Create` 작업 메서드는 최초 Create 양식을 표시합니다. 두 번째(`[HttpPost]`) 버전은 양식 게시를 처리합니다. 두 번째 `Create` 메서드 ( `HttpPost` 버전)는 `ModelState.IsValid` 영화에 유효성 검사 오류가 있는지 여부를 확인 합니다. 이 속성을 가져오면 개체에 적용 된 유효성 검사 특성이 평가 됩니다. 개체에 유효성 검사 오류가 있는 경우이 `Create` 메서드는 폼을 보다 합니다. 오류가 없으면 메서드가 데이터베이스에 새 영화를 저장합니다. 이 동영상 예제에서는 **클라이언트 쪽에서 유효성 검사 오류가 발견 되 면 양식이 서버에 게시 되지 않습니다. 두 번째** `Create` **메서드는 호출 되지**않습니다. 브라우저에서 JavaScript를 사용 하지 않도록 설정 하는 경우 클라이언트 유효성 검사가 사용 되지 않도록 설정 되 고 HTTP POST `Create` 메서드는 `ModelState.IsValid` 영화에 유효성 검사 오류가 있는지 여부를 확인 합니다.

`HttpPost Create` 메서드에서 중단점을 설정하고 메서드가 호출되지 않게 확인할 수 있으며, 유효성 검사 오류가 탐지되면 클라이언트 쪽 유효성 검사가 양식 데이터를 제출하지 않습니다. 브라우저에서 JavaScript를 사용하지 않고 오류가 있는 상태로 양식을 제출하면 중단점에 이르게 됩니다. JavaScript 없이도 여전히 완전한 유효성 검사가 가능합니다. 다음 그림에서는 Internet Explorer에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

다음 이미지에서는 FireFox 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여 줍니다.

![](adding-validation/_static/image7.png)

다음 이미지는 Chrome 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여줍니다.

![](adding-validation/_static/image8.png)

다음은이 자습서의 앞부분에서 스 캐 폴드 하는 *Create. cshtml* 보기 템플릿입니다. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

코드에서 도우미를 사용 하 여 `Html.EditorFor` `<input>` 각 속성에 대 한 요소를 출력 하는 방법을 확인 `Movie` 합니다. 이 도우미 옆은 `Html.ValidationMessageFor` 도우미 메서드를 호출 합니다. 이러한 두 도우미 메서드는 컨트롤러에서 뷰 (이 경우 개체)로 전달 되는 모델 개체를 사용 `Movie` 합니다. 모델에 지정 된 유효성 검사 특성을 자동으로 검색 하 고 오류 메시지를 적절 하 게 표시 합니다.

이 방식의 가장 멋진 장점은 컨트롤러나 `Create` 보기 템플릿이 실제 적용되는 유효성 검사 규칙이나 표시되는 특정 오류 메시지에 대해 전혀 알지 못한다는 것입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다. 동일한 유효성 검사 규칙이 `Edit` 보기 및 모델을 편집하는 만들 수 있는 모든 다른 보기 템플릿에 자동으로 적용됩니다.

유효성 검사 논리를 나중에 변경 하려면 모델에 유효성 검사 특성을 추가 하 여 정확히 한 곳에서 (이 예제에서는 클래스) 수행할 수 있습니다 `movie` . 모든 유효성 검사 논리가 한 곳에서 정의되어 모든 곳에서 사용되므로 애플리케이션의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 이는 *마른* 원칙을 완벽 하 게 활용 하는 것을 의미 합니다.

## <a name="using-datatype-attributes"></a>DataType 특성 사용

*Movie.cs* 파일을 열고 `Movie` 클래스를 검토합니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에도 서식 특성을 제공 합니다. [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)릴리스 날짜 및 가격 필드에 열거 값을 이미 적용 했습니다. 다음 코드에서는 `ReleaseDate` `Price` 적절 한 특성이 포함 된 및 속성을 보여 줍니다 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) .

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터의 서식을 지정 하는 뷰 엔진에 대 한 힌트로 제공 하며 `<a>` URL의 및 전자 메일에 대 한 등의 특성을 제공 합니다 `<a href="mailto:EmailAddress.com">` . [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성을 사용 하 여 데이터 형식의 유효성을 검사할 수 있습니다. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 하는 데 사용 되며 유효성 검사 특성이 ***아닙니다*** . 이 경우에는 날짜 및 시간이 아닌 날짜만 추적하고자 합니다. [DataType 열거형](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 은 *날짜, 시간, PhoneNumber, 통화, EmailAddress* 등과 같은 다양 한 데이터 형식을 제공 합니다. `DataType` 특성을 통해 응용 프로그램에서 자동으로 형식별 기능을 제공하도록 설정할 수도 있습니다. 예를 들어 `mailto:` [EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)에 대 한 링크를 만들 수 있으며, [HTML5](http://html5.org/)를 지 원하는 브라우저에서 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 에 대해 날짜 선택기를 제공할 수 있습니다. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 html 5 브라우저에서 이해할 수 있는 html 5 [데이터](http://ejohn.org/blog/html-5-data-attributes/) ( *데이터 대시로*발음) 특성을 내보냅니다. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 유효성 검사를 제공 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 데이터 필드는 서버의 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)를 기준으로 기본 형식에 따라 표시 됩니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

`ApplyFormatInEditMode`설정은 값이 편집을 위해 텍스트 상자에 표시 될 때 지정 된 서식 지정도 적용 되도록 지정 합니다. (예를 들어 통화 값의 경우 텍스트 상자에 통화 기호를 편집 하는 것을 원하지 않을 수 있습니다.

[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성은 단독으로 사용할 수 있지만 일반적으로 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 사용 하는 것이 좋습니다. `DataType`특성은 화면에 렌더링 하는 방법과 반대로 데이터의 *의미 체계* 를 전달 하 고, 다음과 같은 이점을 제공 하지 않습니다 `DisplayFormat` .

- 브라우저는 HTML5 기능을 사용 하도록 설정할 수 있습니다 (예: 달력 컨트롤, 로캘에 적합 한 통화 기호, 전자 메일 링크 등 표시).
- 기본적으로 브라우저는 사용자의 [로캘에](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)따라 올바른 형식을 사용 하 여 데이터를 렌더링 합니다.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 사용 하면 MVC가 데이터를 렌더링할 올바른 필드 템플릿을 선택할 수 있습니다. 단독으로 사용 하는 경우 [displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 은 문자열 템플릿을 사용 합니다. 자세한 내용은 Brad Wilson의 [ASP.NET MVC 2 템플릿](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)을 참조 하세요. (MVC 2 용으로 작성 된 경우에도이 문서는 현재 버전의 ASP.NET MVC에 적용 됩니다.)

`DataType`날짜 필드와 함께 특성을 사용 하는 경우 `DisplayFormat` Chrome 브라우저에서 필드가 올바르게 렌더링 되도록 특성을 지정 해야 합니다. 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)를 참조 하세요.

> [!NOTE]
> jQuery 유효성 검사는 [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성과 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)에서 작동 하지 않습니다. 예를 들어 다음 코드는 날짜가 지정된 범위에 존재할 경우에도 항상 클라이언트 쪽 유효성 검사 오류를 표시합니다.
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)과 함께 [범위](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성을 사용 하려면 jQuery 날짜 유효성 검사를 사용 하지 않도록 설정 해야 합니다. 일반적으로 모델에서 하드 날짜를 컴파일하는 것은 좋지 않으므로 [범위](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성과 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) 을 사용 하지 않는 것이 좋습니다.

다음 코드는 특성을 한 줄로 결합하는 방법을 보여줍니다.

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

이 시리즈의 다음 부분에서는 애플리케이션을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field.md)
> [다음](examining-the-details-and-delete-methods.md)
