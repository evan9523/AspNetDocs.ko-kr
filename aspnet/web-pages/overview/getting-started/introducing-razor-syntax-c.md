---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 구문 (C#)를 사용 하 여 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장의 개요를 제공 프로그래밍의 ASP.NET 웹 페이지를 사용 하 여 Razor 구문을 사용 합니다. ASP.NET은 동적 웹 pa를 실행 하기 위한 Microsoft의 기술 하는 중...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: 8237dc6b925ccefc5b411aebc8e7c399dcdc6746
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59407356"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>Razor 구문 (C#)를 사용 하 여 ASP.NET 웹 프로그래밍 소개

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 프로그래밍 개요 ASP.NET 웹 페이지 Razor 구문을 사용 합니다. ASP.NET은 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft의 기술입니다. 이 문서는 C# 프로그래밍 언어를 사용 하 여 포커스입니다.
> 
> **학습할**:
> 
> - 프로그래밍 팁 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍 시작 하기 위한 상위 8입니다.
> - 기본 프로그래밍 개념을 해야 합니다.
> - 어떤 ASP.NET 서버 코드 및 Razor 구문에 대 한 all입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="the-top-8-programming-tips"></a>상위 8 프로그래밍 팁

이 섹션에서는 반드시 알아야 할 Razor 구문을 사용 하 여 ASP.NET 서버 코드 작성을 시작 하는 몇 가지 팁을 나열 합니다.

> [!NOTE]
> Razor 구문을 C# 프로그래밍 언어를 기준으로 하며는 ASP.NET 웹 페이지를 사용 하 여 가장 자주 사용 되는 언어입니다. 그러나 Razor 구문을 Visual Basic 언어 및 Visual Basic에서도 수행할 수 있는 모든 지원 합니다. 자세한 내용은 부록을 참조 하세요 [Visual Basic 언어와 구문이](https://go.microsoft.com/fwlink/?LinkId=202908)합니다.


대부분의 이러한 프로그래밍 기법에 대 한 자세한 내용은 문서의 뒷부분에서 찾을 수 있습니다.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 코드를 사용 하 여 페이지를 추가 하 여 @ 문자

`@` 문자 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

다음은 이러한 문이 페이지를 브라우저에서 실행할 때 모양을입니다.

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 인코딩**
> 
> 사용 하 여 페이지의 콘텐츠를 표시 하는 `@` 문자를 앞의 예에서 같이 ASP.NET을 HTML로 인코딩하고 출력 합니다. 이 예약 된 HTML 문자를 대체 (같은 `<` 하 고 `>` 및 `&`) 문자가 HTML 태그 또는 엔터티로 해석 되지 않고 웹 페이지에 표시할 문자를 사용 하도록 설정 하는 코드를 사용 하 여 합니다. HTML 인코딩하지 않고 서버 코드의 출력을 올바르게 표시 되지 않 및 페이지 보안 위험에 노출 될 수 있습니다.
> 
> 목표는 태그로 태그를 렌더링 하는 HTML 태그를 출력 하는 경우 (예를 들어 `<p></p>` 단락 또는 `<em></em>` 텍스트를 강조 하기 위해), 섹션을 참조 하세요 [결합 텍스트, 태그 및 코드 블록의 코드](#BM_CombiningTextMarkupAndCode) 이 문서의 뒷부분에 나오는.
> 
> 읽어보세요에서 HTML 인코딩에 대 한 [양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)합니다.


### <a name="2-you-enclose-code-blocks-in-braces"></a>2. 코드 블록을 중괄호로 묶습니다.

A *코드 블록* 하나 이상의 코드 문을 포함 하 고 중괄호로 묶입니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

브라우저에 표시 된 결과:

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. 세미콜론을 사용 하 여 각 코드 문 블록 내 종료

코드 블록 내 각 전체 코드 문은 세미콜론으로 끝나야 합니다. 인라인 식 세미콜론으로 끝나지 않습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. 변수를 사용 하 여 값을 저장 하려면

값을 저장할 수 있습니다는 *변수*, 문자열, 숫자 및 날짜 등을 포함 합니다. 사용 하 여 새 변수를 만든를 `var` 키워드입니다. 사용 하 여 페이지에서 직접 변수 값을 삽입할 수는 있지만 `@`합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

브라우저에 표시 된 결과:

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 리터럴 문자열 값 큰따옴표로 묶어야

A *문자열* 텍스트로 처리 되는 문자 시퀀스입니다. 문자열을 지정 하려면 묶습니다 큰따옴표:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

표시 하려는 문자열 백슬래시 문자를 포함 하는 경우 ( `\` ) 큰따옴표 또는 ( `"` )를 사용 하 여를 *축 자 문자열 리터럴은* 접두사로 하는 `@` 연산자. (C#의 경우에 \ 축 자 문자열 리터럴을 사용 하지 않는 한 문자에 특별 한 의미가 있습니다.)

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

큰따옴표를 포함 하려면 축 자 문자열 리터럴을 사용 하 여 및 따옴표를 반복 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

두이 예제 모두를 사용 하 여 페이지에서 결과 다음과 같습니다.

![Razor Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> 에 `@` 문자는 C#에서 축 자 문자열 리터럴은 표시 하 고 ASP.NET 페이지에서 코드를 표시 하기 위해 사용 됩니다.


### <a name="6-code-is-case-sensitive"></a>6. 코드는 대/소문자 구분

C#에서는 키워드 (같은 `var`, `true`, 및 `if`) 변수 이름은 대/소문자 구분 및 합니다. 코드의 다음 줄은 두 개의 다른 변수를 만듭니다 `lastName` 및 `LastName.`

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

변수를 선언 하는 경우 `var lastName = "Smith";` 페이지에서 해당 변수를 참조 하려는 경우 `@LastName`, 오류가 발생 하기 때문에 `LastName` 인식할 수 없습니다.

> [!NOTE]
> 키워드 및 변수는 Visual basic에서는 *되지* 대 소문자를 구분 합니다.


### <a name="7-much-of-your-coding-involves-objects"></a>7. 개체를 포함 하는 대부분의 코딩

*개체* 사용 하 여 프로그래밍할 수 있는 것을 나타내는 &#8212; 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등입니다. 개체 특징을 설명 하는 속성이 있고 읽기 또는 변경할 수 있습니다 &#8212; 텍스트 상자 개체의를 `Text` 등 속성인 요청 개체에는 `Url` 속성인 전자 메일 메시지에는 `From` 속성 고객 개체에는 `FirstName` 속성입니다. 개체 수도 있는 메서드를 &quot;동사&quot; 을 수행할 수 있습니다. 파일 개체의 예로 `Save` 메서드를 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드.

자주 사용 하는 `Request` 개체를 텍스트 상자 (폼 필드)의 값과 같은 정보를 제공 하는 브라우저 종류 요청, 페이지, 사용자 id 등의 URL을 한 페이지에서. 다음 예제에서는 속성에 액세스 하는 방법을 보여 줍니다는 `Request` 개체와 호출 하는 방법을 합니다 `MapPath` 메서드의 `Request` 서버의 페이지의 절대 경로 제공 하는 개체:

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

브라우저에 표시 된 결과:

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 의사 결정 하는 코드를 작성할 수 있습니다.

동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 확인할 수 있습니다. 이 작업을 수행 하는 가장 일반적인 방법은 된 합니다 `if` 문 (및 선택적 `else` 문).

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

문이 `if(IsPost)` 작성 하는 약식 방법 `if(IsPost == true)`합니다. 와 함께 `if` 문 다양 한 조건에서 반복 코드 블록을 테스트 하는 방법 및 등과이 문서의 뒷부분에서 설명 합니다.

브라우저에 표시 된 결과 (클릭 한 후 **제출**):

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET 및 POST 메서드는 IsPost 속성
> 
> 웹 페이지 (HTTP)에 사용 된 프로토콜 매우 제한 된 수의 서버에 요청을 확인 하는 데 사용 되는 메서드 (동사)를 지원 합니다. 두 가지 자주 사용 되는 가져오기에 사용 되는 페이지를 읽으려는 및 페이지를 제출 하는 데 사용 되는 게시물입니다. 일반적으로 사용자가 페이지를 요청할 처음 페이지가 요청 될 GET을 사용 하 여 합니다. 사용자 양식을 채우고 다음 제출 단추를 클릭을 하는 경우 브라우저는 서버에는 POST 요청을 만듭니다.
> 
> 웹 프로그래밍에서 유용 여부는 페이지 요청 POST 또는 GET으로 페이지를 처리 하는 방법을 알 수 있도록 알아야 합니다. ASP.NET 웹 페이지에서 사용할 수는 `IsPost` 속성 GET 또는 POST 요청 인지 여부를 확인 합니다. 요청을 POST 이면는 `IsPost` 속성은 true를 반환 하 고 폼의 입력란의 값 등 읽기를 수행할 수 있습니다. 표시 되는 많은 예제 값에 따라 다르게 페이지를 처리 하는 방법을 보여 줍니다. `IsPost`합니다.


## <a name="a-simple-code-example"></a>간단한 코드 예제

이 절차에서는 기본적인 프로그래밍 기술을 설명 하는 페이지를 만드는 방법을 보여 줍니다. 예제에서는 입력 하 고 두 숫자를 추가 하 고 결과 표시 하는 사용자가 수 있는 페이지를 만듭니다.

1. 편집기에서 새 파일을 만들고 이름을 *AddNumbers.cshtml*합니다.
2. 페이지에 이미 아무 것도 대체 페이지에 다음 코드와 태그를 복사 합니다.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    알아두어야 할 몇 가지는 다음과 같습니다.

    - 합니다 `@` 문자 페이지에서 첫 번째 코드 블록을 시작 하 고 뒤에 나오는 `totalMessage` 페이지 하단에 있는 포함 된 변수입니다.
    - 페이지의 맨 위에 있는 블록은 중괄호로 구분 됩니다.
    - 맨 위에 있는 블록의 모든 줄은 세미콜론으로 끝납니다.
    - 변수 `total`, `num1`를 `num2`, 및 `totalMessage` 여러 숫자 및 문자열을 저장 합니다.
    - 에 할당 된 리터럴 문자열 값을 `totalMessage` 큰따옴표로 변수가 합니다.
    - 코드는 경우 대/소문자를 구분 하기 때문에 `totalMessage` 변수를 사용 하 여 페이지 아래쪽에 있는, 이름과 맨 위에 있는 변수를 정확 하 게 일치 해야 합니다.
    - 식 `num1.AsInt() + num2.AsInt()` 개체 및 메서드를 사용 하는 방법을 보여 줍니다. `AsInt` 메서드 각 변수에 대해에서 산술을 수행할 수 있도록 수 (정수)는 사용자가 입력 한 문자열을 변환 합니다.
    - `<form>` 태그를 포함 한 `method="post"` 특성입니다. 사용자가 지정 하는 **추가**, 페이지 HTTP POST 메서드를 사용 하 여 서버에 전송 됩니다. 페이지가 제출 되 면는 `if(IsPost)` true 및 조건부 테스트로 코드 실행, 숫자를 더한 결과 표시 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 두 정수를 입력 한 다음 클릭 합니다 **추가** 단추입니다. 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>기본 프로그래밍 개념

이 문서에서는 ASP.NET 웹 프로그래밍 개요를 제공 합니다. 철저 한 검사를 자주 사용 됩니다 프로그래밍 개념을 통해 둘러보기 방금 없습니다. 이 경우에 설명 거의 모든 ASP.NET Web Pages 시작 해야 합니다.

첫 번째 하지만 거의 기술적 배경입니다.

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 구문, 서버 코드 및 ASP.NET

Razor 구문은 웹 페이지에서 서버 기반 코드를 포함 하기 위한 단순 프로그래밍 구문입니다. Razor 구문을 사용 하 여 웹 페이지에는 두 종류의 콘텐츠: 클라이언트가 콘텐츠 및 서버 코드입니다. 클라이언트 콘텐츠는 웹 페이지에는 항목: HTML 태그 (요소), CSS, JavaScript 및 일반 텍스트와 같은 일부 클라이언트 스크립트 아마도 등 스타일 정보입니다.

Razor 구문에는이 클라이언트 콘텐츠 서버 코드를 추가할 수 있습니다. 서버는 페이지를 브라우저로 보내기 전에 페이지에서 서버 코드를 코드 먼저 실행 됩니다. 서버를 실행 하 여 코드를 단독으로 서버 기반 데이터베이스 액세스와 같은 클라이언트 콘텐츠를 사용 하 여 작업을 수행 하는 훨씬 더 복잡 해질 수 있는 작업을 수행할 수 있습니다. 가장 중요 한 점은 서버 코드가 동적으로 만들 수 클라이언트 콘텐츠 &#8212; 수 HTML 태그나 기타 콘텐츠를 즉석에서 생성 하 고 다음 페이지를 포함할 수 있는 정적 HTML과 함께 브라우저에 보냅니다. 브라우저의 관점에서 서버 코드에 의해 생성 되는 콘텐츠를 클라이언트가 콘텐츠를 다른 모든 클라이언트가 다르지 않습니다. 이미 살펴보았듯이, 필요한 서버 코드는 매우 간단 합니다.

ASP.NET 웹 페이지 Razor 구문을 포함 하는 특수 한 파일 확장명이 (*.cshtml* 하거나 *.vbhtml*). 서버는 이러한 확장을 인식, Razor 구문을 사용 하 여 표시 되 고 페이지에서 브라우저로 보내는 코드를 실행 합니다.

### <a name="where-does-aspnet-fit-in"></a>ASP.NET 적합 하는 위치

Razor 구문은 ASP.NET에 기반으로 하는 Microsoft.NET Framework를 호출 하는 Microsoft 기술을 기반으로 합니다. .NET Framework는 모든 유형의 응용 프로그램 컴퓨터 거의 개발 하기 위한 Microsoft의 빅, 포괄적인 프로그래밍 프레임 워크입니다. ASP.NET은 웹 응용 프로그램을 만들기 위한 특별히 설계 된.NET Framework의 일부입니다. 개발자가 전 세계의 다양 한 가장 크고 가장 트래픽이 많은 웹 사이트를 만드는 ASP.NET을 사용 합니다. (언제 든 지 표시 파일 이름 확장명 *.aspx* 사이트에서 URL의 일부로, 알 수 있습니다 사이트 ASP.NET을 사용 하 여 작성 되었습니다.)

Razor 구문에도 쉽게 배울 초보자 생산성가 있는 경우 본인이 전문가일 경우는 간소화 된 구문을 사용 하는 ASP.NET의 모든 기능을 제공 합니다. 이 구문은 간단 하 게 사용 하는 경우에 ASP.NET 및.NET Framework 제품군의 관계가 웹 사이트 보다 정교 해지면 있다고 할 수 있는 더 큰 프레임 워크의 기능을 의미 합니다.

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **클래스 및 인스턴스**
> 
> ASP.NET 서버 코드 클래스의 개념을 이해에 기본 제공 되는 개체를 사용 합니다. 클래스 정의 또는 템플릿 개체입니다. 예를 들어, 응용 프로그램에 포함 될 수 있습니다는 `Customer` 속성 및 메서드는 모든 customer 개체를 정의 하는 클래스입니다.
> 
> 인스턴스를 만들고 응용 프로그램을 실제 고객 정보를 사용 하 여 작동 해야 하는 경우 (또는 *인스턴스화합니다*) customer 개체입니다. 각 개별 고객은 별도의 인스턴스는 `Customer` 클래스입니다. 모든 인스턴스가 동일한 속성 및 메서드를 지원 하지만 각 customer 개체가 고유 하므로 각 인스턴스에 대 한 속성 값은 일반적으로 다른 합니다. 한 고객 개체에는 `LastName` 속성에는 "Smith" 수 있습니다 다른 고객 개체에서는 `LastName` 속성 "Jones." 수 있습니다
> 
> 마찬가지로 모든 개별 웹 페이지 사이트에서이 `Page` 의 인스턴스인 개체를 `Page` 클래스. 페이지의 단추를 `Button` 개체의 인스턴스를는 `Button` 클래스 및 등입니다. 각 인스턴스는 고유한 특징이 있지만 모든 기반으로 하는 개체의 클래스 정의에 지정 된 것입니다.


## <a name="basic-syntax"></a>기본 구문

이전 기본 예제는 ASP.NET 웹 페이지의 페이지를 만드는 방법 및 서버 코드는 HTML 태그를 추가 하는 방법을 살펴보았습니다. 다음 Razor 구문을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다 &#8212; , 프로그래밍 언어 규칙입니다.

프로그래밍 경험이 있는 경우 (C를 사용한 경우에 특히 C++, C#, Visual Basic 또는 JavaScript)를 읽는 여기의 대부분에 게 익숙할 것입니다. 기능을 살펴보고 서버 코드가 태그에 추가 하는 방법을 익히는 필요할 것 *.cshtml* 파일입니다.

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>텍스트, 태그 및 코드 블록의 코드를 결합합니다.

서버 코드 블록에서 하려는 경우가 많습니다 출력 텍스트 또는 태그 (또는 둘 다) 페이지. 서버 코드 블록을 텍스트 코드 없는 하는 대신 렌더링할지 그대로 있으면 ASP.NET 코드에서 해당 텍스트를 구분할 수 해야 합니다. 다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.

- 와 같은 HTML 요소에 텍스트를 묶으십시오 `<p></p>` 또는 `<em></em>`:   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 요소는 텍스트, HTML 요소 추가 및 서버 코드 식에 포함할 수 있습니다. ASP.NET에서 여는 HTML 태그를 표시 하는 경우 (예를 들어 `<p>`), 요소를 포함 한 모든 렌더링 및으로 해당 콘텐츠 브라우저 네요 서버 코드 식을 확인 하는 것입니다.
- 사용 된 `@:` 연산자 또는 `<text>` 요소입니다. 합니다 `@:` 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 콘텐츠의 단일 줄을 출력 합니다 `<text>` 요소 출력에 여러 줄을 포함 합니다. 이러한 옵션은 출력의 일부로 HTML 요소를 렌더링 하지 않을 때 유용 합니다.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    여러 줄 텍스트 또는 일치 하지 않는 HTML 태그를 출력 하려는 경우 사용 하 여 각 줄 앞 `@:`에서 줄을 묶을 수 있습니다 또는 `<text>` 요소입니다. 같은 합니다 `@:` 연산자를`<text>` 태그는 텍스트 콘텐츠를 ASP.NET에 사용 되며 페이지 출력에는 렌더링 되지 않습니다.

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    첫 번째 예제에서는 앞의 예제를 반복 하지만 단일 쌍을 사용 하 여 `<text>` 태그를 렌더링할 텍스트를 묶으십시오. 두 번째 예제에서는 합니다 `<text>` 하 고 `</text>` 태그는 모두 일부 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 세 줄을 묶습니다 (`<br />`), 서버 코드와 일치 하는 HTML 태그와 함께 합니다. 마찬가지로 수도 앞에 개별적으로 각 줄은 `@:` 연산자; 둘 다 방식으로 작동 합니다.

    > [!NOTE]
    > 이 섹션에 표시 된 대로 텍스트를 출력할 때 &#8212; HTML 요소를 사용 하는 `@:` 연산자와 `<text>` 요소 &#8212; ASP.NET 하지 HTML 인코딩 출력 합니다. (ASP.NET 서버 코드 식 및 서버 코드 블록 뒤에 나오는의 출력을 인코딩하는 앞에서 설명한 대로 `@`를 제외 하 고이 섹션에서 설명 하는 특수 한 현상.)

### <a name="whitespace"></a>Whitespace

문에서 (및 문자열 리터럴 외부에서) 공백이 문이 영향을 주지 않습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

문의 줄 바꿈을 문에서 영향을 주지 않습니다 개이고 가독성을 위해 문을 래핑할 수 있습니다. 다음 문은 동일합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

그러나 문자열 리터럴로 중간 줄을 둘러쌀 수 없습니다. 다음 예제에서는 작동 하지 않습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

위의 코드와 같이 여러 줄으로 줄 바꿈되는 긴 문자열을 결합 하려면 두 가지 옵션이 있습니다. 연결 연산자를 사용할 수 있습니다 (`+`),이 문서의 뒷부분에서 살펴보겠습니다. 사용할 수도 있습니다는 `@` 만들려면 축 자 문자열 리터럴,이 문서의 앞부분에서 본 것 처럼 문자입니다. 여러 줄 축 자 문자열 리터럴은 중단할 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>코드 (및 태그) 주석

주석 자신 또는 다른 사용자에 대 한 정보를 그대로 수 있습니다. 사용 하지 않도록 할 수 있습니다 (*주석*) 코드 또는 태그를 시간에 대 한 페이지에 유지 하려고 하지만 실행 하지 않으려는의 섹션입니다.

다양 한 구문 및 HTML 태그에 대 한 Razor 코드의 주석 처리 있습니다. 모든 Razor 코드에서와 마찬가지로 Razor 주석은 처리 (및 제거) 페이지를 브라우저로 전송 되기 전에 서버에서. 따라서 Razor 주석 구문을 파일을 편집 하지만 페이지의 소스에도 사용자가 표시 되지 경우 볼 수 있는 주석을 코드에 (또는 태그에도)를 추가할 수 있습니다.

ASP.NET Razor 주석에 대 한로 주석을 시작 하기 `@*` 사용 하 여 종료 및 `*@`합니다. 주석 줄 또는 여러 줄에 있을 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

다음은 코드 블록 내에서 주석이입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

다음 코드 줄을 사용 하 여 코드의 동일한 블록 주석 처리 되어 실행 되지 않습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

Razor 주석 구문을 사용 하는 대신 코드 블록 내부의 C#과 같은 사용 중인 프로그래밍 언어의 주석 구문을 사용할 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

C#에서는 단일 줄 주석 앞에 `//` 로 시작 하는 문자 및 여러 줄 주석 `/*` 하 고 끝나야 `*/`합니다. (Razor 주석은와 마찬가지로 C# 주석 렌더링 되지 않습니다 브라우저로.)

이미 알고 계시 겠지만, 태그에 대 한 HTML 주석을 만들 수 있습니다.

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML 주석 시작 `<!--` 문자와 끝나는 `-->`합니다. HTML 주석 텍스트 뿐 아니라도 페이지에 유지 하려고 하지만 렌더링 하지 않으려는 모든 HTML 태그를 사용할 수 있습니다. 이 HTML 주석 태그와 포함 된 텍스트의 전체 내용을 숨겨집니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

Razor 주석, HTML 주석 달리 *는* 페이지로 렌더링 사용자 페이지의 소스를 확인 하 여 볼 수 있습니다.

Razor C#의 중첩 된 블록에 제약이 따릅니다. 자세한 내용은 참조 하세요. [라는 C# 변수와 중첩 블록 손상 코드 생성](http://aspnetwebstack.codeplex.com/workitem/1914)

## <a name="variables"></a>변수

변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다. 변수를 아무 것도 이름을 지정할 수 있습니다 하지만 이름은 영문자로 시작 해야 하 고 공백 또는 예약 된 문자를 포함할 수 없습니다.

### <a name="variables-and-data-types"></a>변수 및 데이터 형식

변수는 어떤 종류의 데이터를 변수에 저장 됨을 나타내는 특정 데이터 형식에 있을 수 있습니다. 문자열 값을 저장 하는 문자열 변수를 할 수 있습니다 (같은 &quot;Hello world&quot;), 다양 한 형식 (예: 2012/4/12 또는 2009 년 3 월의에서 날짜 값을 저장 하는 정수 값 (예: 3 또는 79)를 저장 하는 정수 변수 및 날짜 ). 및 다른 여러 데이터 형식을 사용할 수 있습니다.

그러나 일반적으로 필요가 변수의 형식을 지정 합니다. 대부분의 경우 ASP.NET의 변수 데이터를 어떻게 사용 되 고 있는지에 따라 형식을 알아낼 수 있습니다. (형식을 지정 해야 하는 경우에 따라,이 참 이어야 하는 예제 표시 됩니다.)

사용 하는 변수를 선언 합니다 `var` 키워드 (형식 지정 않으려는) 하는 경우 또는 형식의 이름을 사용 하 여:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

다음 예제에서는 웹 페이지에서 변수의 몇 가지 일반적인 사용을 보여 줍니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

페이지에서 이전 예제와 결합 하면 브라우저에 표시 된이 확인할 수 있습니다.

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>변환 및 데이터 형식 테스트

일반적으로 ASP.NET 데이터 형식을 자동으로 확인할 수 있습니다, 있지만 경우에 따라 만들 수 없습니다. 따라서 명시적 변환을 수행 하 여 ASP.NET을 도와줄 해야 합니다. 형식을 변환 하는 것이 없는, 하는 경우에 때때로 것이 좋습니다 테스트 하려는 어떤 유형의 데이터를 작업할 수 있습니다.

가장 일반적인 경우는 정수 또는 날짜와 같은 다른 형식으로 문자열을 변환 해야 합니다. 다음 예제에서는 문자열을 숫자로 변환 해야 여기서는 일반적인 경우를 보여 줍니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

일반적으로 사용자 입력을 문자열로 제공 합니다. 사용자 번호를 입력 하 라는 메시지가 표시 한 경우에을 때 사용자 입력을 제출 하 고 코드에서 읽을 때 숫자를 입력 한 경우에 데이터를 문자열 형식입니다. 따라서 문자열을 숫자로 변환 해야 합니다. 예에서를 변환 하지 않고 값에 산술 연산을 수행 하려는 경우 다음 오류가 발생을 ASP.NET 두 문자열을 추가할 수 없습니다.

*'Int' ' string '를 암시적으로 변환할 수 없습니다.*

정수 값으로 변환 하려면 호출을 `AsInt` 메서드. 변환이 성공한 경우에 다음 숫자를 추가할 수 있습니다.

다음 표에서 변수에 대 한 몇 가지 일반적인 변환 및 테스트 메서드를 나열합니다.

:::row:::
    :::column:::
    <strong>메서드</strong>
    :::column-end:::
    :::column:::
    <strong>설명</strong>
    :::column-end:::
    :::column:::
    <strong>예제</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    정수 (예: "593") 정수를 나타내는 문자열을 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    와 같은 문자열 변환 &quot;true&quot; 또는 &quot;false&quot; 부울 형식입니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    와 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 부동 소수점 수입니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    와 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 하거나 &quot;7.439&quot; 소수입니다. (ASP.NET, 10 진수는 부동 소수점 숫자를 보다 정확 합니다.)
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    Asp.net은 날짜 및 시간 값을 나타내는 문자열을 변환 `DateTime` 형식입니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    다른 데이터 형식 문자열로 변환합니다.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>연산자

연산자는 키워드 또는 식에서 수행할 수 있는 명령의 종류를 ASP.NET에 지시 하는 문자입니다. C# 언어 (및 Razor 구문을 기반으로 하는) 다양 한 연산자를 지원 하지만 시작 하려면 몇 가지를 인식 해야 합니다. 다음 표에서 가장 일반적인 연산자를 보여 줍니다.


:::row:::
    :::column:::
    <strong>연산자</strong>
    :::column-end:::
    :::column:::
    <strong>설명</strong>
    :::column-end:::
    :::column:::
    <strong>예제</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    숫자 식에 사용 되는 수학 연산자.
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    할당. 왼쪽에 있는 개체 문의 오른쪽에 값을 할당합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    같음 반환 `true` 값이 같으면 합니다. (의 차이 확인 합니다 `=` 연산자 및 `==` 연산자입니다.)
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    같지 않음 반환 `true` 값 같지 않은 경우.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    작은-큰 보다-보다 작음-보다-또는-같음 및 크거나 같음.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    연결 문자열을 조인 하는 데 사용 됩니다. ASP.NET이이 연산자는 식의 데이터 형식을 기반으로 하는 더하기 연산자 간의 차이점을 알고 있습니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    증가 및 감소 연산자의 추가 하 고 변수에서 각각 1을 뺍니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    점입니다. 개체 및 해당 속성 및 메서드를 구분 하는 데 사용 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    괄호입니다. 그룹 식 및 매개 변수를 전달할 메서드를 사용 하는 합니다.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    대괄호입니다. 배열 또는 컬렉션의 값에 액세스 하기 위해 사용 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    되지 않습니다. 반대로 `true` 값을 `false` 그 반대로 가능 합니다. 일반적으로 테스트 하는 약식 방법으로 사용 `false` (즉,에 대 한 없습니다 `true`).
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    논리적 AND 또는 및 연결 하는 데 사용 되는 조건 그룹화 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a>파일 및 코드의 폴더 경로 사용 하 여 작업

종종 코드에서 파일 및 폴더 경로 작업할 수 있습니다. 개발 컴퓨터에 나타나는 웹 사이트에 대 한 실제 폴더 구조의 예 다음과 같습니다.

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Url 및 경로 대 한 몇 가지 필수 세부 정보는 다음과 같습니다.

- 도메인 이름을 사용 하 여 시작 URL (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`).
- URL은 호스트 컴퓨터의 실제 경로에 해당합니다. 예를 들어 `http://myserver` 폴더에 해당할 수 있습니다 *C:\websites\mywebsite* 서버의 합니다.
- 가상 경로 전체 경로 지정 하지 않고도 코드에서 경로 나타내는 축약형입니다. 도메인 또는 서버 이름 다음에 나오는 URL 부분을 포함 합니다. 가상 경로 사용 하는 경우에 경로 업데이트 하지 않고도 다른 도메인 또는 서버에 코드를 이동할 수 있습니다.

차이점을 이해 하는 데 예는 다음과 같습니다.

| 전체 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 서버 이름 | *mycompanyserver* |
| 가상 경로 | */humanresources/CompanyPolicy.htm* |
| 실제 경로 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

가상 루트가 / 드라이브는 c:의 루트와 마찬가지로 \입니다. (가상 폴더 경로 항상 슬래시를 사용 합니다.) 폴더의 가상 경로 실제 폴더 이름이 같은 필요가 없습니다. 별칭 수 있습니다. (프로덕션 서버에서 가상 경로 거의 일치 하는 실제 경로 정확 하 게 합니다.)

코드에서 파일 및 폴더를 사용 하 여 작업할 때의 실제 경로 및 경우에 따라 사용 하는 개체에 따라 가상 경로 참조 해야 경우가 있습니다. ASP.NET이 도구를 제공 하면 이러한 코드에서 파일 및 폴더 경로 사용 하 여 작업에 대 한: 합니다 `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>실제 가상 경로로 변환: Server.MapPath 메서드

합니다 `Server.MapPath` 메서드는 가상 경로 변환 (같은 */default.cshtml*) 절대 실제 경로에 (같은 *C:\WebSites\MyWebSiteFolder\default.cshtml*). 전체 실제 경로 필요할 때 언제 든이이 메서드를 사용 합니다. 일반적인 예로 읽거나 텍스트 파일 또는 웹 서버의 이미지 파일을 작성 하는 경우입니다.

일반적으로 알 수 없는 호스팅 사이트 서버의 사이트의 절대 실제 경로 알고이 메서드는 경로 변환할 수 있도록-가상 경로-를 서버에 해당 경로에 있습니다. 파일 또는 폴더 메서드에 가상 경로 전달 하 고 실제 경로 반환 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>가상 루트 참조:는 ~ 연산자 및 Href 메서드

에 *.cshtml* 또는 *.vbhtml* 파일을 사용 하 여 가상 루트 경로 참조할 수 있습니다는 `~` 연산자입니다. 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크는 손상 되지 때문에 매우 유용 합니다. 그 어느 때 다른 위치로 웹 사이트를 이동 하는 경우에 유용 합니다. 다음은 몇 가지 예입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

웹 사이트가 `http://myserver/myapp`, 이러한 경로 페이지가 실행 될 때 ASP.NET에서 어떻게 처리 다음과 같습니다.

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

(실제로 이러한 경로 변수 값으로 표시 되지 않습니다 하지만 어떤는 처럼 ASP.NET 경로 처리 합니다.)

사용할 수는 `~` 연산자 위와 같이 서버 코드와 같이 태그에서:

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

태그를 사용 하 여는 `~` 연산자를 이미지 파일, 다른 웹 페이지 및 CSS 파일 같은 리소스에 대 한 경로 만듭니다. ASP.NET 페이지 (코드 및 태그)를 통해 찾아 해결 하는 모든 페이지를 실행 하는 경우는 `~` 적절 한 경로에 대 한 참조입니다.

## <a name="conditional-logic-and-loops"></a>조건부 논리 및 루프

ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 만큼 명령문을 반복 하는 코드를 작성할 수 있습니다 (즉, 루프를 실행 하는 코드).

### <a name="testing-conditions"></a>테스트 조건

사용할 간단한 조건을 테스트 하는 `if` 지정한 테스트를 기반으로 true 또는 false를 반환 하는 문:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` 키워드는 블록을 시작 합니다. 실제 테스트 (조건) 괄호로 이며 true 또는 false를 반환 합니다. 테스트가 true 인 경우를 실행 하는 문은 중괄호로 묶습니다. `if` 문을 포함할 수는 `else` 조건이 false 인 경우 실행할 문을 지정 하는 블록:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

사용 하 여 여러 조건을 추가할 수 있습니다는 `else if` 블록:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

이 예제에서는 첫 번째 조건이 if 블록이 true가 아니면는 `else if` 조건이 확인 됩니다. 조건이 충족 될 경우의 문에서 `else if` 블록이 실행 됩니다. 어떤 조건 충족 되 면의 문에서 `else` 블록이 실행 됩니다. 다른 경우 원하는 만큼 추가할 수 있습니다 블록 및를 사용 하 여 닫습니다는 `else` 으로 차단 합니다 &quot;등등&quot; 조건.

많은 수의 조건 테스트 하려면 사용을 `switch` 블록:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

괄호 안에 테스트할 값입니다 (예에서는 `weekday` 변수). 각 개별 테스트를 사용 하는 `case` 콜론 (:)로 끝나는 문의 합니다. 하는 경우의 값을 `case` 테스트 값과 일치 하는 문, 해당 case 블록의 코드가 실행 됩니다. 각 case 문을 사용 하 여 닫을 `break` 문입니다. (각 나누기를 포함 해야 하는 경우 `case` 블록에서 다음 코드를 `case` 문을 에서도 실행 됩니다.) A `switch` 블록 같으며를 `default` 에 대 한 마지막 경우로 문은 &quot;등등&quot; 다른 경우에 없는 경우 실행 되는 옵션입니다.

브라우저에 표시 된 마지막 두 조건부 블록의 결과:

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>코드를 반복합니다.

자주 반복적으로 동일한 문을 실행 해야 합니다. 반복 하 여이 작업을 수행 합니다. 예를 들어, 종종 문을 실행 하면 동일한 각 항목에 대 한 데이터의 컬렉션에서입니다. 사용할 수 있습니다 정확 하 게 하는 횟수를 반복 하려면를 알고 있는 경우는 `for` 루프입니다. 이러한 종류의 루프까지 셈 카운트다운에 특히 유용 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

로 시작 하는 루프를 `for` 세미콜론으로 종료 각 키워드 뒤에 괄호로 세 문입니다.

- 첫 번째 문은 괄호 안에 (`var i=10;`) 카운터를 만들고 10으로 초기화 합니다. 카운터 이름 필요가 `i` &#8212; 모든 변수를 사용할 수 있습니다. 경우는 `for` 루프가 실행, 카운터가 자동으로 증가 합니다.
- 두 번째 문은 (`i < 21;`) 개수를 계산 하려면 정도 대 한 조건을 설정 합니다. 최대 20으로 이동 하려는 경우 (즉, 계속 해 서이 카운터는 21 보다 작거나 동안).
- 세 번째 문은 (`i++` ) 카운터는 루프가 실행 될 때마다 추가 1 있어야 함을 지정 하는 증분 연산자를 사용 합니다.

중괄호 안의 루프의 각 반복에 대해 실행 되는 코드입니다. 태그 새 단락을 만듭니다 (`<p>` 요소) 각 시간 및의 값을 표시할 출력에 줄을 추가 `i` (카운터). 이 페이지를 실행 하면 항목 수를 나타내는 각 줄의 텍스트를 사용 하 여 출력을 표시 하는 11 줄을 만듭니다.

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

컬렉션 또는 배열을 사용 하 여 작업할 경우 자주 사용 하는 `foreach` 루프입니다. 컬렉션은 유사한 개체의 그룹 및 `foreach` 루프는 컬렉션의 각 항목에서 작업을 수행할 수 있습니다. 이 유형의 루프는 컬렉션에 대 한 편리한 있으므로 달리는 `for` 루프 필요가 카운터를 증가 시키거나 제한을 설정 합니다. 대신는 `foreach` 루프 코드 컬렉션을 통해 완료 될 때까지 간단히 진행 합니다.

다음 코드의 항목을 반환 하는 예를 들어를 `Request.ServerVariables` 은 웹 서버에 대 한 정보를 포함 하는 개체 컬렉션입니다. 사용 하 여는 `foreac` 각 항목의 이름을 새 표시할 h 루프 `<li>` HTML 글머리 기호 목록의 요소에에서 있습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` 키워드 뒤에 괄호가 컬렉션의 단일 항목을 나타내는 변수를 선언 하는 위치가 (예에서 `var item`) 뒤를 `in` 키워드를 반복 하려는 컬렉션에 따라 합니다. 본문에는 `foreach` 루프 앞에서 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

보다 일반적인 루프를 만들려면 사용 합니다 `while` 문:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

`while` 루프 시작 합니다 `while` 키워드 뒤에 괄호 루프가 계속 되는 기간을 지정 하는 (여기에 대 한으로 `countNum` 경우 50 미만), then 블록을 반복 합니다. 루프는 일반적으로 증가 (추가) 또는 감소 (에서 빼기) 변수 또는 계산에 사용 되는 개체입니다. 예에서는 `+=` 연산자에는 1을 더하여 `countNum` 루프가 실행 될 때마다 합니다. (카운트다운 되는 루프에서 변수를 감소 시키기 위해 감소 연산자를 사용 하는 `-=`).

## <a name="objects-and-collections"></a>개체 및 컬렉션

ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지 자체를 포함 하 여 개체입니다. 이 섹션에서는 자주 사용 하 여 코드에서 몇 가지 중요 한 개체를 설명 합니다.

### <a name="page-objects"></a>Page 개체

ASP.NET에서 가장 기본적인 개체는 페이지입니다. 조건에 맞는 개체 없이 직접 page 개체의 속성에 액세스할 수 있습니다. 다음 코드는 페이지의 파일 경로 가져오고 사용 하는 `Request` 페이지의 개체:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

있도록 명확 현재 페이지 개체에 메서드와 속성을 참조 하는 선택적으로 사용할 수 키워드 `this` 코드에서 페이지 개체를 나타내는입니다. 사용 하 여 이전 코드 예제와 같습니다 `this` 추가 페이지를 나타냅니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

속성을 사용할 수는 `Page` 와 같은 많은 정보를 가져올 개체입니다.

- `Request`. 이미 살펴보았듯이, 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류를 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.
- `Response`. 서버 코드 실행이 완료 된 경우 브라우저에 보낼 응답 (페이지)에 대 한 정보 컬렉션입니다. 예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다. 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>컬렉션 개체 (배열 및 사전을)

A *컬렉션* 컬렉션과 같은 동일한 유형의 개체의 그룹인 `Customer` 데이터베이스에서 개체입니다. ASP.NET와 같은 많은 기본 제공 컬렉션을 포함 합니다 `Request.Files` 컬렉션입니다.

컬렉션의 데이터를 자주 사용 됩니다. 두 가지 일반적인 컬렉션 형식은 합니다 *배열* 하며 *사전*합니다. 배열 유사 항목 컬렉션을 저장 하 고 싶지만를 각 항목을 보유 하는 별도 변수를 만들지 않으려는 경우에 유용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

배열에서 특정 데이터 형식을 선언와 같은 `string`, `int`, 또는 `DateTime`합니다. 변수 배열을 포함할 수 있습니다, 선언에 대괄호를 추가 하 (같은 `string[]` 또는 `int[]`). 항목의 위치 (인덱스)를 사용 하는 배열 또는 사용 하 여 액세스할 수 있습니다는 `foreach` 문입니다. 배열 인덱스는 0부터 시작 &#8212; 즉, 첫 번째 항목은에서 위치 0, 두 번째 항목은 위치 1입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

시작 하 여 배열에 있는 항목의 수를 확인할 수 있습니다 해당 `Length` 속성입니다. 배열 검색) (배열에서 특정 항목의 위치를 가져오려면는 `Array.IndexOf` 메서드. 수행할 수도 있습니다 역방향 등 배열의 내용을 (합니다 `Array.Reverse` 메서드) 또는 콘텐츠를 정렬 (합니다 `Array.Sort` 메서드).

브라우저에 표시 하는 문자열 배열 코드의 출력:

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

사전이 같습니다 키/값 쌍의 컬렉션을 설정 하거나 해당 값을 검색 키 (또는 이름)을 제공 하는 위치

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

사용할 사전을 만들려면는 `new` 키워드를 새 사전 개체를 만드는 동안 있습니다. 사용 하 여 변수를 사전에 할당할 수 있습니다는 `var` 키워드입니다. 꺾쇠 괄호를 사용 하 여 사전에 있는 항목의 데이터 형식을 ( `< >` ). 선언의 끝 실제로 새 사전을 만듭니다 하는 방법 이기 때문에 괄호의 쌍을 추가 해야 합니다.

사전에 항목을 추가 하려면 호출할 수 있습니다 합니다 `Add` 사전 변수의 메서드 (`myScores` 이 경우), 키 및 값을 지정 합니다. 또는 키를 나타내고 다음 예제와 같이 단순한 할당을 수행 하려면 대괄호를 사용할 수 있습니다.

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

사전에서 값을 가져오려면 대괄호로 키를 지정 합니다.

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>매개 변수를 사용 하 여 메서드를 호출합니다.

이 문서의 앞부분에서 읽은 것 처럼 개체를 사용 하 여 프로그래밍 메서드를 사용할 수 있습니다. 예를 들어, 한 `Database` 개체에 있을 `Database.Connect` 메서드. 여러 방법에는 하나 이상의 매개 변수 수도 있습니다. A *매개 변수* 메서드에 전달 하는 값은 해당 작업을 완료 하는 메서드를 사용 하도록 설정 합니다. 예를 들어,에 대 한 선언을 확인 된 `Request.MapPath` 세 개의 매개 변수를 사용 하는 메서드:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

(줄 읽기 쉽게 표시 하였습니다. 기억 하는 내부 문자열 제외 하 고 배치 하는 거의 모든 줄 바꿈을 넣을 수 있습니다 따옴표에 포함 됩니다.)

이 메서드는 지정된 된 가상 경로에 해당 하는 서버의 실제 경로 반환 합니다. 메서드에 대 한 세 가지 매개 변수는 `virtualPath`하십시오 `baseVirtualDir`, 및 `allowCrossAppMapping`합니다. (알 수 있습니다 선언 매개 변수를 수락 하 게 하는 데이터의 데이터 형식으로 나열 됩니다.) 이 메서드를 호출 하는 경우 모든 세 매개 변수에 대 한 값을 제공 해야 합니다.

Razor 구문을 메서드에 매개 변수를 전달 하기 위한 두 가지 옵션을 제공 합니다. *위치 매개 변수* 하 고 *명명 된 매개 변수*합니다. 위치 매개 변수를 사용 하 여 메서드를 호출 하는 엄격한 순서를 메서드 선언에 지정 된 매개 변수를 전달 합니다. (일반적으로 알 수이 순서 메서드에 대 한 설명서를 참조 하 여.) 순서를 따라야 하며 매개 변수를 건너뛸 수 없습니다 &#8212; 하는 경우 필요한 전달 하면 빈 문자열 (`""`) 또는 `null` 에 대 한 값이 없는 위치 매개 변수에 대해 합니다.

다음 예제에서는 라는 폴더가 있다고 가정 *스크립트* 웹 사이트입니다. 호출 된 `Request.MapPath` 메서드와 전달 올바른 순서로 세 가지 매개 변수 값입니다. 다음의 결과 매핑된 경로가 표시 됩니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

경우는 메서드가 여러 매개 변수를 유지할 수 있습니다 코드 보다 읽기 쉬운 명명 된 매개 변수를 사용 하 여 합니다. 명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 콜론 (:) 및 값을 지정 합니다. 명명 된 매개 변수의 장점은 원하는 순서에 관계 없이 전달할 수 있습니다. (단점은 메서드 호출으로 compact 아닙니다.)

다음 예제에서는 위와 같은 메서드를 호출 하지만 명명 된 값을 제공 하는 매개 변수를 사용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

알 수 있듯이 다른 순서로 매개 변수 전달 됩니다. 그러나 앞의 예제 및이 예제를 실행 하는 경우 동일한 값을 반환 됩니다.

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>오류 처리

### <a name="try-catch-statements"></a>Try / Catch 문

종종 컨트롤 외부 이유로 실패할 수 있는 코드에 문의 해야 합니다. 예를 들어:

- 코드를 만들거나 파일에 액세스 하려고 하면, 모든 종류의 오류가 발생할 수 있습니다. 원하는 파일이 존재 하지 않을, 잠긴 상태일 수 있습니다, 그리고 코드 수 하지 권한이 등.
- 마찬가지로 코드에는 데이터베이스의 레코드를 업데이트 하려고 하는 경우 사용 권한 문제가 발생할 수, 데이터베이스에 연결이 삭제 될 수 있습니다, 그리고 잘못 된 경우 등에 데이터를 저장할 수 있습니다.

프로그래밍 측면에서 이러한 상황 이라고 *예외*합니다. 코드에서 예외가 발생 (throw)를 생성 오류 메시지, 사용자에 게 기껏해야 성가 시 거:

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

사용할 수 있는 코드 예외가 발생할 수 있는 경우에서 및이 유형의 오류 메시지를 방지 하기 위해 `try/catch` 문입니다. 에 `try` 문을 체크 인하는 코드를 실행 합니다. 하나 이상의 `catch` 문을 찾을 수 있습니다 특정 발생 했을 수 있는 오류 (특정 유형의 예외). 만큼 포함할 수 있습니다 `catch` 문을 때 예상 하는 오류에 대 한 확인 해야 합니다.

> [!NOTE]
> 사용 하지 않는 것이 좋습니다 합니다 `Response.Redirect` 의 메서드 `try/catch` 문을 페이지에서 예외가 발생할 수 있기 때문에 합니다.


다음 예제에서는 첫 번째 요청에서 텍스트 파일을 만들고 다음 사용자가 파일을 열 수 있는 단추를 표시 하는 페이지를 보여 줍니다. 이 예제에서는 예외가 하면 있도록 의도적으로 잘못 된 파일 이름을 사용 합니다. 코드에 포함 되어 `catch` 두 가지 가능한 예외에 대 한 문을: `FileNotFoundException`, 파일 이름에 잘못 된 경우 발생 하는 및 `DirectoryNotFoundException`, ASP.NET 폴더를도 찾을 수 없는 경우 발생 합니다. (모든 항목이 제대로 작동 하는 경우 실행 방식을 확인 하기 위해이 예에서 문은 주석 수 있습니다.)

코드에서 예외를 처리 하지 않은 경우 이전 스크린 샷에서 처럼 오류 페이지가 표시 됩니다. 그러나는 `try/catch` 섹션은 사용자가 이러한 종류의 오류를 표시 하지 못하도록 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>추가 리소스

**Visual Basic을 사용한 프로그래밍**


[부록: Visual Basic 언어 및 구문](https://go.microsoft.com/fwlink/?LinkId=202908)


**참조 설명서**


[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C# 언어](https://msdn.microsoft.com/library/kx37x362.aspx)
