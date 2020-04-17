---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 비즈니스 규칙 유효성 검사를 통해 모델 구축 | 마이크로 소프트 문서
author: rick-anderson
description: 3단계는 NerdDinner 응용 프로그램에 대한 데이터베이스를 쿼리하고 업데이트하는 데 사용할 수 있는 모델을 만드는 방법을 보여 주며, 이 두 가지를 보여 주는 방법을 보여 주입니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541639"
---
# <a name="build-a-model-with-business-rule-validations"></a>비즈니스 규칙 유효성 검사를 사용하여 모델 빌드

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 3단계입니다.
> 
> 3단계는 NerdDinner 응용 프로그램에 대한 데이터베이스를 쿼리하고 업데이트하는 데 사용할 수 있는 모델을 만드는 방법을 보여 주며, 이 두 가지를 보여 주는 방법을 보여 주입니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-3-building-the-model"></a>얼간이 디너 3 단계 : 모델 구축

모델 뷰 컨트롤러 프레임워크에서 "모델"이라는 용어는 유효성 검사 및 비즈니스 규칙을 통합하는 해당 도메인 논리뿐만 아니라 응용 프로그램의 데이터를 나타내는 개체를 나타냅니다. 이 모델은 여러 가지 면에서 MVC 기반 응용 프로그램의 "핵심"이며 나중에 볼 수 있듯이 기본적으로 동작을 구동합니다.

ASP.NET MVC 프레임워크는 모든 데이터 액세스 기술을 사용하여 지원되며, 개발자는 LINQ에서 엔터티로, LINQ에서 SQL로, NHibernate, LLBLGen Pro, SubSonic, WilsonORM 또는 데이터 리더 또는 데이터 집합을 ADO.NET 등 다양한 풍부한 .NET 데이터 옵션을 선택하여 모델을 구현할 수 있습니다.

NerdDinner 응용 프로그램의 경우 LINQ to SQL을 사용하여 데이터베이스 디자인에 매우 밀접하게 대응하고 사용자 지정 유효성 검사 논리 및 비즈니스 규칙을 추가하는 간단한 모델을 만들 려고 합니다. 그런 다음 응용 프로그램의 나머지 부분에서 데이터 지속성 구현을 추상화하는 데 도움이 되는 리포지토리 클래스를 구현하고 쉽게 단위 테스트를 수행할 수 있습니다.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ 에서 SQL은 .NET 3.5의 일부로 제공되는 ORM(개체 관계형 매퍼)입니다.

LINQ to SQL은 데이터베이스 테이블을 코딩할 수 있는 .NET 클래스에 매핑하는 쉬운 방법을 제공합니다. NerdDinner 응용 프로그램의 경우 데이터베이스 내의 Dinners 및 RSVP 테이블을 Dinner 및 RSVP 클래스에 매핑하는 데 사용합니다. Dinners 및 RSVP 테이블의 열은 Dinner 및 RSVP 클래스의 속성에 해당합니다. 각 Dinner 및 RSVP 개체는 데이터베이스의 Dinners 또는 RSVP 테이블 내에서 별도의 행을 나타냅니다.

LINQ to SQL을 사용하면 데이터베이스 데이터로 Dinner 및 RSVP 개체를 검색하고 업데이트하기 위해 SQL 문을 수동으로 생성하지 않아도 됩니다. 대신 Dinner 및 RSVP 클래스, 데이터베이스에서 매핑하는 방법 및 데이터베이스 간의 관계를 정의합니다. 그런 다음 LINQ to SQL은 상호 작용하고 사용할 때 런타임에 사용할 적절한 SQL 실행 논리를 생성합니다.

VB 및 C# 내에서 LINQ 언어 지원을 사용하여 데이터베이스에서 Dinner 및 RSVP 개체를 검색하는 표현 쿼리를 작성할 수 있습니다. 이렇게 하면 작성해야 하는 데이터 코드의 양이 최소화되고 실제로 깨끗한 응용 프로그램을 빌드할 수 있습니다.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>프로젝트에 SQL 클래스에 LINQ 추가

먼저 프로젝트 내의 "모델" 폴더를 마우스 오른쪽 단추로 클릭하고 **&gt;새 항목 추가** 메뉴 명령을 선택합니다.

![](build-a-model-with-business-rule-validations/_static/image1.png)

그러면 "새 항목 추가" 대화 상자가 나타납니다. "데이터" 범주로 필터링하고 그 안에 있는 "LINQ 에서 SQL 클래스로" 템플릿을 선택합니다.

![](build-a-model-with-business-rule-validations/_static/image2.png)

항목의 이름을 "NerdDinner"로 지정하고 "추가" 버튼을 클릭합니다. 비주얼 스튜디오는 우리의 \Model 디렉토리 아래에 NerdDinner.dbml 파일을 추가한 다음 LINQ를 SQL 개체 관계형 디자이너에 엽니다.

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ를 SQL로 사용하여 데이터 모델 클래스 만들기

LINQ to SQL을 사용하면 기존 데이터베이스 스키마에서 데이터 모델 클래스를 빠르게 만들 수 있습니다. 이렇게 하려면 서버 탐색기에서 NerdDinner 데이터베이스를 열고 모델링할 테이블을 선택합니다.

![](build-a-model-with-business-rule-validations/_static/image4.png)

그런 다음 테이블을 LINQ로 SQL 디자이너 표면으로 드래그할 수 있습니다. 이 작업을 수행하면 LINQ to SQL이 테이블의 스키마를 사용하여 Dinner 및 RSVP 클래스를 자동으로 만듭니다(데이터베이스 테이블 열에 매핑되는 클래스 속성).

![](build-a-model-with-business-rule-validations/_static/image5.png)

기본적으로 LINQ to SQL 디자이너는 데이터베이스 스키마를 기반으로 클래스를 만들 때 테이블과 열 이름을 자동으로 "복수화"합니다. 예를 들어 위의 예제의 "Dinners" 테이블은 "Dinner" 클래스로 이어졌습니다. 이 클래스 이름 지정은 모델을 .NET 명명 규칙과 일치시키는 데 도움이 되며, 일반적으로 디자이너가 이 문제를 편리하게 해결하도록 합니다(특히 테이블을 많이 추가할 때). 그러나 디자이너가 생성하는 클래스 또는 속성의 이름이 마음에 들지 않으면 언제든지 재정의하고 원하는 이름으로 변경할 수 있습니다. 디자이너 내에서 인라인 엔터티/속성 이름을 편집하거나 속성 표를 통해 수정하여 이 작업을 수행할 수 있습니다.

기본적으로 LINQ to SQL 디자이너는 테이블의 기본 키/외래 키 관계를 검사하며, 이를 기반으로 자동으로 생성되는 다른 모델 클래스 간에 기본 "관계 연결"을 만듭니다. 예를 들어, Dinners 및 RSVP 테이블을 LINQ에 LINQ로 드래그할 때 RSVP 테이블에 Dinners 테이블에 외래 키가 있다는 사실에 따라 둘 간의 일대일 관계 연결이 유추되었습니다(디자이너의 화살표로 표시됩니다).

![](build-a-model-with-business-rule-validations/_static/image6.png)

위의 연결을 통해 LINQ는 SQL에 개발자가 지정된 RSVP와 연결된 Dinner에 액세스하는 데 사용할 수 있는 RSVP 클래스에 강력하게 입력된 "Dinner" 속성을 추가합니다. 또한 Dinner 클래스에는 개발자가 특정 Dinner와 연결된 RSVP 개체를 검색하고 업데이트할 수 있는 "RSVP" 컬렉션 속성이 있습니다.

아래에서 새 RSVP 개체를 만들고 Dinner의 RSVP 컬렉션에 추가할 때 Visual Studio 내에서 intellisense의 예를 볼 수 있습니다. LINQ to SQL이 Dinner 개체에 "RSV" 컬렉션을 자동으로 추가한 방법을 확인합니다.

![](build-a-model-with-business-rule-validations/_static/image7.png)

Dinner의 RSVP 컬렉션에 RSVP 개체를 추가하여 LINQ를 SQL에 사용하여 데이터베이스의 Dinner와 RSVP 행 간의 외래 키 관계를 연결하도록 지시합니다.

![](build-a-model-with-business-rule-validations/_static/image8.png)

디자이너가 테이블 연결을 모델링하거나 명명하는 방식이 마음에 들지 않으면 이를 재정의할 수 있습니다. 디자이너 내의 연결 화살표를 클릭하고 속성 표를 통해 속성에 액세스하여 이름을 바꾸거나 삭제하거나 수정하면 됩니다. 그러나 NerdDinner 응용 프로그램의 경우 기본 연결 규칙은 빌드중인 데이터 모델 클래스에 적합하며 기본 동작만 사용할 수 있습니다.

### <a name="nerddinnerdatacontext-class"></a>얼간이 디너데이터컨텍스트 클래스

Visual Studio는 LINQ에서 SQL 디자이너로 정의된 모델 및 데이터베이스 관계를 나타내는 .NET 클래스를 자동으로 만듭니다. LINQ에서 SQL DataContext 클래스에 대한 LINQ 는 솔루션에 추가된 각 LINQ에서 SQL 디자이너 파일에 대해서도 생성됩니다. LINQ를 SQL 클래스 항목 "NerdDinner"로 지정했기 때문에 생성된 DataContext 클래스를 "NerdDinnerDataContext"라고 합니다. 이 NerdDinnerDataContext 클래스는 데이터베이스와 상호 작용하는 기본 방법입니다.

NerdDinnerDataContext 클래스는 데이터베이스 내에서 모델링한 두 테이블을 나타내는 "Dinners" 및 "RSVP"라는 두 개의 속성을 노출합니다. C#을 사용하여 해당 속성에 대해 LINQ 쿼리를 작성하여 데이터베이스에서 Dinner 및 RSVP 개체를 쿼리하고 검색할 수 있습니다.

다음 코드는 NerdDinnerDataContext 개체를 인스턴스화하고 LINQ 쿼리를 수행하여 나중에 발생하는 Dinners 시퀀스를 가져오는 방법을 보여 줍니다. Visual Studio는 LINQ 쿼리를 작성할 때 전체 인텔리센스를 제공하며 반환된 개체는 강력한 형식이며 intellisense를 지원합니다.

![](build-a-model-with-business-rule-validations/_static/image9.png)

Dinner 및 RSVP 개체에 대해 쿼리할 수 있도록 허용하는 것 외에도 NerdDinnerDataContext는 이후에 검색하는 Dinner 및 RSVP 개체에 대한 변경 사항을 자동으로 추적합니다. 이 기능을 사용하여 명시적 SQL 업데이트 코드를 작성하지 않고도 변경 내용을 데이터베이스에 쉽게 저장할 수 있습니다.

예를 들어 아래 코드에서는 LINQ 쿼리를 사용하여 데이터베이스에서 단일 Dinner 개체를 검색하고 Dinner 속성 두 개를 업데이트한 다음 변경 내용을 데이터베이스에 다시 저장하는 방법을 보여 줍니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

위의 코드에서 NerdDinnerDataContext 개체는 검색한 Dinner 개체에 대한 속성 변경 내용을 자동으로 추적합니다. "SubmitChanges()" 메서드를 호출하면 업데이트된 값을 다시 유지하도록 데이터베이스에 적절한 SQL "UPDATE" 문을 실행합니다.

### <a name="creating-a-dinnerrepository-class"></a>디너 만들기리포지토리 클래스

작은 응용 프로그램의 경우 컨트롤러가 LINQ에서 SQL DataContext 클래스에 대해 직접 작동하고 컨트롤러 내에 LINQ 쿼리를 포함하도록 하는 것이 좋습니다. 그러나 응용 프로그램이 커지면 이 방법은 유지 관리 및 테스트가 번거로워집니다. 또한 여러 위치에서 동일한 LINQ 쿼리를 복제할 수도 있습니다.

응용 프로그램을 보다 쉽게 유지 관리하고 테스트할 수 있는 한 가지 방법은 "리포지토리" 패턴을 사용하는 것입니다. 리포지토리 클래스는 데이터 쿼리 및 지속성 논리를 캡슐화하고 응용 프로그램에서 데이터 지속성의 구현 세부 정보를 추상화하는 데 도움이 됩니다. 응용 프로그램 코드를 더 깨끗하게 만드는 것 외에도 리포지토리 패턴을 사용하면 나중에 데이터 저장소 구현을 쉽게 변경할 수 있으며 실제 데이터베이스없이 응용 프로그램을 단위 테스트하는 데 도움이 될 수 있습니다.

NerdDinner 응용 프로그램의 경우 아래 서명이 있는 DinnerRepository 클래스를 정의합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*참고: 이 장의 후반부에서는 이 클래스에서 IDinnerRepository 인터페이스를 추출하고 컨트롤러에서 종속성 주입을 사용하도록 설정합니다. 하지만 먼저 간단한 작업을 시작하여 DinnerRepository 클래스와 직접 작업할 것입니다.*

이 클래스를 구현하려면 "모델" 폴더를 마우스 오른쪽 단추로 클릭하고 **&gt;새 항목 추가** 메뉴 명령을 선택합니다. "새 항목 추가" 대화 상자 에서 "클래스" 템플릿을 선택하고 파일이름을 "DinnerRepository.cs"으로 지정합니다.

![](build-a-model-with-business-rule-validations/_static/image10.png)

그런 다음 아래 코드를 사용하여 DinnerRepository 클래스를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>DinnerRepository 클래스를 사용하여 검색, 업데이트, 삽입 및 삭제

DinnerRepository 클래스를 만들었으니, 다음과 같은 일반적인 작업을 보여 주는 몇 가지 코드 예제를 살펴보겠습니다.

#### <a name="querying-examples"></a>쿼리 예제

아래 코드는 DinnerID 값을 사용하여 단일 저녁 식사를 검색합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

아래 코드는 예정된 모든 저녁 식사 및 루프를 검색합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>예제 삽입 및 업데이트

아래 코드는 두 개의 새로운 저녁 식사를 추가하는 것을 보여줍니다. 리포지토리에 대한 추가/수정은 "Save()" 메서드가 호출될 때까지 데이터베이스에 커밋되지 않습니다. LINQ to SQL은 데이터베이스 트랜잭션의 모든 변경 내용을 자동으로 래핑하므로 리포지토리가 저장될 때 모든 변경 내용이 발생하거나 아무 것도 수행하지 않습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

아래 코드는 기존 Dinner 개체를 검색하고 두 속성을 수정합니다. 변경 내용은 리포지토리에서 "Save()" 메서드가 호출될 때 데이터베이스로 다시 커밋됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

아래 코드는 저녁 식사를 검색한 다음 RSVP를 추가합니다. 데이터베이스에서 둘 사이에 기본 키/외래 키 관계가 있기 때문에 LINQto to SQL이 만든 Dinner 개체의 RSVS 컬렉션을 사용하여 이 작업을 수행합니다. 이 변경 내용은 리포지토리에서 "Save()" 메서드가 호출될 때 새 RSVP 테이블 행으로 데이터베이스에 다시 유지됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>예제 삭제

아래 코드는 기존 Dinner 개체를 검색한 다음 삭제됨으로 표시합니다. "Save()" 메서드가 리포지토리에서 호출되면 삭제를 다시 데이터베이스로 커밋합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>유효성 검사 및 비즈니스 규칙 논리를 모델 클래스와 통합

유효성 검사 및 비즈니스 규칙 논리통합은 데이터와 함께 작동하는 모든 응용 프로그램의 핵심 부분입니다.

#### <a name="schema-validation"></a>스키마 유효성 검사

LINQ에서 SQL 디자이너로 모델 클래스를 정의하는 경우 데이터 모델 클래스의 속성 데이터 형식은 데이터베이스 테이블의 데이터 형식과 일치합니다. 예를 들어 Dinners 테이블의 "EventDate" 열이 "datetime"인 경우 LINQ에서 SQL로 만든 데이터 모델 클래스는 "DateTime"(기본 제공 .NET 데이터 형식)입니다. 즉, 코드에서 정수 또는 부울을 할당하려고 하면 컴파일 오류가 발생하며 런타임시 유효하지 않은 문자열 형식을 암시적으로 변환하려고 하면 자동으로 오류가 발생합니다.

또한 LINQ to SQL은 문자열을 사용할 때 SQL 값 이스케이프를 자동으로 처리하므로 SQL 주입 공격으로부터 보호할 수 있습니다.

#### <a name="validation-and-business-rule-logic"></a>유효성 검사 및 비즈니스 규칙 논리

스키마 유효성 검사는 첫 번째 단계로 유용하지만 거의 충분하지 않습니다. 대부분의 실제 시나리오에서는 여러 속성에 걸쳐 코드를 실행하고 종종 모델의 상태를 인식할 수 있는 풍부한 유효성 검사 논리를 지정해야 합니다(예: 생성/업데이트/삭제되거나 "보관됨"과 같은 도메인 별 상태 내에서). 모델 클래스에 유효성 검사 규칙을 정의하고 적용하는 데 사용할 수 있는 다양한 패턴과 프레임워크가 있으며 이를 위해 사용할 수 있는 여러 .NET 기반 프레임워크가 있습니다. ASP.NET MVC 응용 프로그램 내에서 거의 모든 응용 프로그램을 사용할 수 있습니다.

NerdDinner 응용 프로그램의 목적을 위해, 우리는 우리가 우리의 Dinner 모델 개체에 IsValid 속성 및 GetRule위반() 메서드를 노출 하는 비교적 간단 하 고 간단한 패턴을 사용 합니다. IsValid 속성은 유효성 검사 및 비즈니스 규칙이 모두 유효한지 여부에 따라 true 또는 false를 반환합니다. GetRule위반() 메서드는 규칙 오류 목록을 반환합니다.

프로젝트에 "부분 클래스"를 추가하여 저녁 식사 모델에 대해 IsValid 및 GetRule위반()을 구현합니다. 부분 클래스는 VS 디자이너가 유지 관리하는 클래스에 메서드/속성/이벤트를 추가하는 데 사용할 수 있으며(예: LINQ에서 SQL 디자이너로 생성된 Dinner 클래스) 코드가 엉망이 되는 것을 방지할 수 있습니다. \Models 폴더를 마우스 오른쪽 단추로 클릭하여 프로젝트에 새 부분 클래스를 추가한 다음 "새 항목 추가" 메뉴 명령을 선택할 수 있습니다. 그런 다음 "새 항목 추가" 대화 상자에서 "클래스" 템플릿을 선택하고 이름을 Dinner.cs 수 있습니다.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"추가" 버튼을 클릭하면 프로젝트에 Dinner.cs 파일이 추가되고 IDE 내에서 열립니다. 그런 다음 아래 코드를 사용하여 기본 규칙/유효성 검사 적용 프레임워크를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

위의 코드에 대한 몇 가지 참고 사항 :

- Dinner 클래스에는 "부분" 키워드가 서문으로 되어 있는데, 이는 그 안에 포함된 코드가 LINQ에서 SQL 디자이너에 의해 생성/유지 관리되고 단일 클래스로 컴파일되는 클래스와 결합됨을 의미합니다.
- Rule위반 클래스는 규칙 위반에 대한 자세한 내용을 제공할 수 있는 프로젝트에 추가할 도우미 클래스입니다.
- Dinner.GetRule위반() 메서드를 사용하면 유효성 검사 및 비즈니스 규칙이 평가됩니다(곧 구현할 예정). 그런 다음 규칙 오류에 대한 자세한 내용을 제공하는 Rule위반 개체 의 시퀀스를 반환합니다.
- Dinner.IsValid 속성은 Dinner 개체에 활성 Rule위반이 있는지 여부를 나타내는 편리한 도우미 속성을 제공합니다. 언제든지 Dinner 개체를 사용하는 개발자가 사전에 확인할 수 있으며 예외를 발생시키지 않습니다.
- Dinner.OnValidate() 부분 메서드는 LINQ에서 SQL에 제공하는 후크로, Dinner 개체가 데이터베이스 내에서 유지될 때마다 알림을 받을 수 있습니다. 위의 OnValidate() 구현은 Dinner에 규칙 위반이 저장되기 전에 없음을 보장합니다. 잘못된 상태인 경우 예외가 발생하여 LINQ가 SQL로 인해 트랜잭션이 중단됩니다.

이 방법은 유효성 검사 및 비즈니스 규칙을 통합할 수 있는 간단한 프레임워크를 제공합니다. 지금은 GetRule위반() 메서드에 아래 규칙을 추가해 보겠습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

C#의 "수익률 반환" 기능을 사용하여 규칙 위반 시퀀스를 반환합니다. 위의 처음 여섯 가지 규칙 검사는 Dinner의 문자열 속성이 null 또는 비어 있을 수 없음을 적용하기만 하면 됩니다. 마지막 규칙은 좀 더 흥미롭고, ContactPhone 번호 형식이 Dinner의 국가와 일치하는지 확인하기 위해 프로젝트에 추가할 수 있는 PhoneValidator.IsValidNumber() 도우미 메서드를 호출합니다.

사용할 수 있습니다. 이 전화 유효성 검사 지원을 구현하기 위한 NET의 정규식 지원입니다. 다음은 국가별 정규전 패턴 검사를 추가할 수 있도록 프로젝트에 추가할 수 있는 간단한 PhoneValidator 구현입니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>유효성 검사 및 비즈니스 논리 위반 처리

위의 유효성 검사 및 비즈니스 규칙 코드를 추가한 후 Dinner를 만들거나 업데이트하려고 할 때마다 유효성 검사 논리 규칙이 평가되고 적용됩니다.

개발자는 다음과 같은 코드를 작성하여 Dinner 개체가 유효한지 사전에 확인하고 예외를 제기하지 않고 해당 개체의 모든 위반 목록을 검색할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

잘못된 상태로 Dinner를 저장하려고 하면 DinnerRepository에서 Save() 메서드를 호출할 때 예외가 발생합니다. 이는 LINQ to SQL이 Dinner.OnValidate() 부분 메서드를 Dinner.OnValidate() 부분 메서드를 저장하기 전에 자동으로 호출하고 Dinner.OnValidate() 에 코드를 추가하여 Dinner.OnValidate() 에 규칙 위반이 있는 경우 예외를 발생시키기 때문에 발생합니다. 이 예외를 catch 하 고 수정 할 위반 목록을 적극적으로 검색할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

유효성 검사 및 비즈니스 규칙은 UI 계층 이 아닌 모델 계층 내에서 구현되므로 응용 프로그램 내의 모든 시나리오에 적용되고 사용됩니다. 나중에 비즈니스 규칙을 변경하거나 추가할 수 있으며 Dinner 개체와 함께 작동하는 모든 코드가 이를 존중할 수 있습니다.

응용 프로그램 및 UI 논리 전반에 걸쳐 이러한 변경 내용이 파급되지 않고 한 곳에서 비즈니스 규칙을 유연하게 변경할 수 있는 유연성은 잘 작성된 응용 프로그램의 표시이며 MVC 프레임워크가 권장하는 이점입니다.

### <a name="next-step"></a>다음 단계

이제 데이터베이스를 쿼리하고 업데이트하는 데 사용할 수 있는 모델이 있습니다.

이제 프로젝트에 HTML UI 환경을 구축하는 데 사용할 수 있는 몇 가지 컨트롤러와 뷰를 추가해 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-database.md)
> [다음](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
