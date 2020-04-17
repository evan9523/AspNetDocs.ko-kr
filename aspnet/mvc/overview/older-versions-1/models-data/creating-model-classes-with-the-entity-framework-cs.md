---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 엔터티 프레임워크(C#)를 통해 모델 클래스 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 Microsoft 엔터티 프레임워크에서 ASP.NET MVC를 사용하는 방법을 배웁니다. 엔터티 마법사를 사용하여 엔터티 다와 ADO.NET 만드는 방법을 배웁니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542666"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Entity Framework를 사용하여 모델 클래스 만들기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> 이 자습서에서는 Microsoft 엔터티 프레임워크에서 ASP.NET MVC를 사용하는 방법을 배웁니다. 엔터티 마법사를 사용하여 엔터티 데이터 모델을 ADO.NET 만드는 방법을 알아봅니다. 이 자습서의 과정에서 Entity Framework를 사용 하 여 데이터베이스 데이터를 선택, 삽입, 업데이트 및 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 빌드 합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft 엔터티 프레임워크를 사용하여 데이터 액세스 클래스를 만드는 방법을 설명합니다. 이 자습서는 Microsoft 엔터티 프레임워크에 대한 이전의 지식이 없다고 가정합니다. 이 자습서가 끝나면 Entity Framework를 사용하여 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제하는 방법을 이해할 수 있습니다.

Microsoft 엔터티 프레임워크는 데이터베이스에서 데이터 액세스 계층을 자동으로 생성할 수 있는 O/RM(개체 관계 매핑) 도구입니다. Entity Framework를 사용하면 직접 데이터 액세스 클래스를 빌드하는 지루한 작업을 방지할 수 있습니다.

ASP.NET MVC와 함께 Microsoft 엔터티 프레임워크를 사용하는 방법을 설명하기 위해 간단한 샘플 응용 프로그램을 빌드합니다. 영화 데이터베이스 레코드를 표시하고 편집할 수 있는 영화 데이터베이스 응용 프로그램을 만듭니다.

이 자습서에서는 서비스 팩 1을 통해 Visual Studio 2008 또는 Visual Web Developer 2008이 있다고 가정합니다. 엔터티 프레임워크를 사용하려면 서비스 팩 1이 필요합니다. 다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 서비스 팩 1을 이와 함께 Visual Web 개발자를 다운로드할 수 있습니다.

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC와 Microsoft 엔터티 프레임워크 사이에는 필수적인 연결이 없습니다. ASP.NET MVC에서 사용할 수 있는 엔터티 프레임워크에는 몇 가지 대안이 있습니다. 예를 들어 Microsoft LINQ와 같은 다른 O/RM 도구를 사용하여 SQL, NHibernate 또는 SubSonic에 MVC 모델 클래스를 빌드할 수 있습니다.

## <a name="creating-the-movie-sample-database"></a>동영상 샘플 데이터베이스 만들기

영화 데이터베이스 응용 프로그램은 다음 열을 포함하는 Movies라는 데이터베이스 테이블을 사용합니다.

| 열 이름 | 데이터 형식 | 널 허용? | 기본 키는? |
| --- | --- | --- | --- |
| Id | int | False | True |
| 제목 | 은바르차르 (100) | False | False |
| 감독 | 은바르차르 (100) | False | False |

다음 단계를 수행하여 이 테이블을 ASP.NET MVC 프로젝트에 추가할 수 있습니다.

1. 솔루션 탐색기\_창에서 앱 데이터 폴더를 마우스 오른쪽 단추로 클릭하고 새 항목 추가 메뉴 옵션을 선택합니다. **Add, New Item.**
2. 새 **항목 추가** 대화 상자에서 **SQL Server 데이터베이스를**선택하고 데이터베이스에 MoviesDB.mdf라는 이름을 지정하고 **추가** 단추를 클릭합니다.
3. MoviesDB.mdf 파일을 두 번 클릭하여 서버 탐색기/데이터베이스 탐색기 창을 엽니다.
4. MoviesDB.mdf 데이터베이스 연결을 확장하고 테이블 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션을 **선택합니다.**
5. 테이블 디자이너에서 ID, 제목 및 디렉터 열을 추가합니다.
6. **저장** 버튼(플로피 아이콘이 있음)을 클릭하여 새 테이블을 영화 이름으로 저장합니다.

Movies 데이터베이스 테이블을 만든 후 테이블에 일부 샘플 데이터를 추가해야 합니다. 동영상 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시**옵션을 선택합니다. 표시되는 그리드에 가짜 동영상 데이터를 입력할 수 있습니다.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 만들기

엔터티 프레임워크를 사용하려면 엔터티 데이터 모델을 만들어야 합니다. Visual Studio 엔터티 데이터 *모델 마법사를* 사용하여 데이터베이스에서 엔터티 데이터 모델을 자동으로 생성할 수 있습니다.

다음 단계를 수행하세요.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**을 선택합니다.
2. 새 **항목 추가** 대화 상자에서 데이터 범주를 선택합니다(그림 1 참조).
3. 엔터티 **데이터 모델** ADO.NET 선택하고 엔터티 데이터 모델에 MoviesDBModel.edmx라는 이름을 지정한 다음 **추가** 단추를 클릭합니다. **추가** 단추를 클릭하면 데이터 모델 마법사가 시작됩니다.
4. 모델 **내용 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택하고 **다음** 단추를 클릭합니다(그림 2 참조).
5. 데이터 **연결 선택** 단계에서 MoviesDB.mdf 데이터베이스 연결을 선택하고 엔터티 연결 설정 이름 MoviesDBEntities를 입력한 다음 **단추를** 클릭합니다(그림 3 참조).
6. 데이터베이스 개체 선택 단계에서 동영상 데이터베이스 테이블을 선택하고 **완료** 단추를 **클릭합니다(그림** 4 참조).

이 단계를 완료하면 ADO.NET 엔터티 데이터 모델 디자이너(엔터티 디자이너)가 열립니다.

**그림 1 – 새 엔터티 데이터 모델 만들기**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**그림 2 - 모델 내용 단계 선택**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**그림 3 - 데이터 연결 선택**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**그림 4 – 데이터베이스 개체 선택**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 수정

엔터티 데이터 모델을 만든 후 엔터티 디자이너를 활용하여 모델을 수정할 수 있습니다(그림 5 참조). 솔루션 탐색기 창 내의 모델 폴더에 포함된 MoviesDBModel.edmx 파일을 두 번 클릭하여 언제든지 엔터티 디자이너를 열 수 있습니다.

**그림 5 – ADO.NET 엔터티 데이터 모델 디자이너**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

예를 들어 엔터티 디자이너를 사용하여 엔터티 모델 데이터 마법사가 생성하는 클래스의 이름을 변경할 수 있습니다. 마법사는 Movies라는 새 데이터 액세스 클래스를 만들었습니다. 즉, 마법사는 클래스에 데이터베이스 테이블과 동일한 이름을 지정했습니다. 이 클래스를 사용하여 특정 동영상 인스턴스를 나타내므로 클래스의 이름을 동영상에서 동영상으로 바꿉니다.

엔터티 클래스의 이름을 바꾸려면 엔터티 디자이너에서 클래스 이름을 두 번 클릭하고 새 이름을 입력할 수 있습니다(그림 6 참조). 또는 엔터티 디자이너에서 엔터티를 선택한 후 속성 창에서 엔터티 이름을 변경할 수 있습니다.

**그림 6 - 엔터티 이름 변경**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

저장 단추(플로피 디스크의 아이콘)를 클릭하여 수정한 후 엔터티 데이터 모델을 저장해야 합니다. 뒤에서 엔터티 디자이너는 C# 클래스 집합을 생성합니다. 솔루션 탐색기 창에서 MoviesDBModel.Designer.cs 파일을 열어 이러한 클래스를 볼 수 있습니다.

다음에 Entity Designer를 사용할 때 변경 내용을 덮어쓰므로 Designer.cs 파일의 코드를 수정하지 마십시오. Designer.cs 파일에 정의된 엔터티 클래스의 기능을 확장하려면 별도의 파일에서 *부분 클래스를* 만들 수 있습니다.

#### <a name="selecting-database-records-with-the-entity-framework"></a>엔터티 프레임워크를 사용하여 데이터베이스 레코드 선택

영화 레코드 목록을 표시하는 페이지를 만들어 동영상 데이터베이스 응용 프로그램 빌드를 시작해 보겠습니다. 목록 1의 홈 컨트롤러는 Index()라는 작업을 노출합니다. Index() 작업은 엔터티 프레임워크를 활용하여 Movie 데이터베이스 테이블의 모든 동영상 레코드를 반환합니다.

**목록 1 – 컨트롤러\HomeController.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

목록 1의 컨트롤러에는 생성자가 포함되어 있습니다. 생성자는 db라는 \_클래스 수준 필드를 초기화합니다. \_db 필드는 Microsoft 엔터티 프레임워크에서 생성된 데이터베이스 엔터티를 나타냅니다. \_db 필드는 엔터티 디자이너에 의해 생성된 MoviesDBEntities 클래스의 인스턴스입니다.

홈 컨트롤러에서 MoviesDBEntity 클래스를 사용하려면 MovieEntityApp.Models*네임스페이스(MVCProjectName*) 를 가져와야 합니다. 모델)을 참조하십시오.

\_db 필드는 Index() 작업 내에서 사용되어 Movies 데이터베이스 테이블에서 레코드를 검색합니다. 식 \_db입니다. MovieSet은 Movies 데이터베이스 테이블의 모든 레코드를 나타냅니다. ToList() 메서드는 동영상 집합을 동영상 개체의 일반 컬렉션(동영상&lt;&gt;목록)으로 변환하는 데 사용됩니다.

영화 레코드는 LINQ에서 엔터티로 검색됩니다. 목록 1의 Index() 작업은 LINQ *메서드 구문을* 사용하여 데이터베이스 레코드 집합을 검색합니다. 원하는 경우 대신 LINQ *쿼리 구문을* 사용할 수 있습니다. 다음 두 문은 매우 동일한 작업을 수행합니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

가장 직관적인 LINQ 구문(메서드 구문 또는 쿼리 구문)을 사용합니다. 두 방법 간의 성능 차이는 없습니다 - 유일한 차이점은 스타일입니다.

목록 2의 보기는 동영상 레코드를 표시하는 데 사용됩니다.

**목록 2 – 보기\홈\인덱스.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

리스팅 2의 보기에는 각 동영상 레코드를 반복하고 영화 레코드의 제목 및 디렉터 속성 값을 표시하는 **foreach** 루프가 포함되어 있습니다. 각 레코드 옆에 편집 및 삭제 링크가 표시됩니다. 또한 뷰 하단에 동영상 추가 링크가 나타납니다(그림 7 참조).

**그림 7 - 색인 보기**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

인덱스 보기는 *형식이 입력된 보기입니다.* 인덱스 보기에는 &lt;모델 속성을&gt; 강력하게 입력한 일반 목록 컬렉션(목록&lt;동영상)에 캐스팅하는 *Inherits* 특성이 있는 %@ Page% 지시문이 포함됩니다.

## <a name="inserting-database-records-with-the-entity-framework"></a>엔터티 프레임워크를 사용하여 데이터베이스 레코드 삽입

엔터티 프레임워크를 사용하여 데이터베이스 테이블에 새 레코드를 쉽게 삽입할 수 있습니다. 목록 3에는 Movie 데이터베이스 테이블에 새 레코드를 삽입하는 데 사용할 수 있는 홈 컨트롤러 클래스에 추가된 두 가지 새 작업이 포함되어 있습니다.

**목록 3 – 컨트롤러\HomeController.cs (방법 추가)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

첫 번째 Add() 작업은 뷰를 반환하기만 하면 됩니다. 뷰에는 새 동영상 데이터베이스 레코드를 추가하기 위한 양식이 포함되어 있습니다(그림 8 참조). 양식을 제출하면 두 번째 Add() 작업이 호출됩니다.

두 번째 Add() 작업은 AcceptVerbs 특성으로 장식되어 있습니다. 이 작업은 HTTP POST 작업을 수행할 때만 호출할 수 있습니다. 즉, 이 작업은 HTML 양식을 게시할 때만 호출할 수 있습니다.

두 번째 Add() 작업은 ASP.NET MVC TryUpdateModel() 메서드의 도움을 받아 엔터티 프레임워크 동영상 클래스의 새 인스턴스를 만듭니다. TryUpdateModel() 메서드는 Add() 메서드에 전달된 FormCollection의 필드를 가져와 이러한 HTML 양식 필드의 값을 Movie 클래스에 할당합니다.

엔터티 프레임 워크를 사용 하는 경우 엔터티 클래스의 속성을 업데이트 하려면 TryUpdateModel 또는 UpdateModel 메서드를 사용 하는 경우 속성의 "화이트 리스트"를 제공 해야 합니다.

다음으로 Add() 작업은 몇 가지 간단한 양식 유효성 검사를 수행합니다. 이 작업은 Title 및 Director 속성에 값이 모두 있는지 확인합니다. 유효성 검사 오류가 있는 경우 유효성 검사 오류 메시지가 ModelState에 추가됩니다.

유효성 검사 오류가 없는 경우 엔터티 프레임워크의 도움을 받아 새 동영상 레코드가 Movies 데이터베이스 테이블에 추가됩니다. 새 레코드는 다음과 같은 두 줄의 코드로 데이터베이스에 추가됩니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

코드의 첫 번째 줄은 엔터티 프레임워크에서 추적되는 동영상 집합에 새 Movie 엔터티를 추가합니다. 두 번째 코드 줄은 기본 데이터베이스로 다시 추적되는 동영상에 대한 변경 내용을 저장합니다.

**그림 8 - 추가 보기**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>엔터티 프레임워크로 데이터베이스 레코드 업데이트

엔터티 Framework를 사용하여 데이터베이스 레코드를 새 데이터베이스 레코드를 삽입하기 위해 방금 수행한 접근 방식과 거의 동일한 접근 방식을 따를 수 있습니다. 목록 4에는 Edit()이라는 두 개의 새 컨트롤러 작업이 포함되어 있습니다. 첫 번째 Edit() 작업은 영화 레코드를 편집하기 위한 HTML 양식을 반환합니다. 두 번째 편집() 작업은 데이터베이스를 업데이트하려고 시도합니다.

**목록 4 – 컨트롤러\HomeController.cs (방법 편집)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

두 번째 Edit() 작업은 편집중인 동영상의 ID와 일치하는 데이터베이스에서 동영상 레코드를 검색하여 시작합니다. 다음 LINQ to Entities 문은 특정 ID와 일치하는 첫 번째 데이터베이스 레코드를 가져옵니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

다음으로 TryUpdateModel() 메서드는 HTML 양식 필드의 값을 동영상 엔터티의 속성에 할당하는 데 사용됩니다. 업데이트할 정확한 속성을 지정하는 화이트리스트가 제공됩니다.

다음으로 영화 제목 및 디렉터 속성에 값이 있는지 확인하기 위해 몇 가지 간단한 유효성 검사가 수행됩니다. 두 속성 중 하나에 값이 없는 경우 유효성 검사 오류 메시지가 ModelState 및 ModelState.IsValid에 추가되어 false 값을 반환합니다.

마지막으로 유효성 검사 오류가 없는 경우 기본 Movies 데이터베이스 테이블은 SaveChanges() 메서드를 호출하여 변경 내용으로 업데이트됩니다.

데이터베이스 레코드를 편집할 때 편집중인 레코드의 ID를 데이터베이스 업데이트를 수행하는 컨트롤러 작업에 전달해야 합니다. 그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드를 알 수 없습니다. 목록 5에 포함된 편집 보기에는 편집중인 데이터베이스 레코드의 ID를 나타내는 숨겨진 양식 필드가 포함됩니다.

**목록 5 – 보기\홈\편집.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>엔터티 프레임워크를 사용하여 데이터베이스 레코드 삭제

이 자습서에서 해결해야 하는 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제하는 것입니다. 목록 6의 컨트롤러 작업을 사용하여 특정 데이터베이스 레코드를 삭제할 수 있습니다.

**목록 6 -- \컨트롤러\HomeController.cs (작업 삭제)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete() 작업은 먼저 작업에 전달된 Id와 일치하는 동영상 엔터티를 검색합니다. 다음으로, 동영상은 DeleteObject() 메서드를 호출한 다음 SaveChanges() 메서드를 호출하여 데이터베이스에서 삭제됩니다. 마지막으로 사용자가 색인 보기로 다시 리디렉션됩니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 및 Microsoft 엔터티 프레임워크를 활용하여 데이터베이스 기반 웹 응용 프로그램을 빌드하는 방법을 보여 주는 것입니다. 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제할 수 있는 응용 프로그램을 빌드하는 방법을 배웠습니다.

먼저 엔터티 데이터 모델 마법사를 사용하여 Visual Studio 내에서 엔터티 데이터 모델을 생성하는 방법에 대해 설명했습니다. 다음으로 LINQto 엔터티를 사용하여 데이터베이스 테이블에서 데이터베이스 레코드 집합을 검색하는 방법을 알아봅니다. 마지막으로 엔터티 프레임워크를 사용하여 데이터베이스 레코드를 삽입, 업데이트 및 삭제했습니다.

> [!div class="step-by-step"]
> [다음](creating-model-classes-with-linq-to-sql-cs.md)
