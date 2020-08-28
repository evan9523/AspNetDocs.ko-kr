---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045145"
---
# <a name="adding-a-new-field"></a>새 필드 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 섹션에서는 변경 내용이 데이터베이스에 적용 되도록 Entity Framework Code First 마이그레이션를 사용 하 여 일부 변경 사항을 모델 클래스로 마이그레이션합니다.

기본적으로이 Code First 자습서의 앞부분에서와 같이 Entity Framework Code First를 사용 하 여 데이터베이스를 자동으로 만드는 경우 데이터베이스에 테이블을 추가 하 여 데이터베이스의 스키마가 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적할 수 있습니다. 동기화 되지 않은 경우 Entity Framework에서 오류를 throw 합니다. 이렇게 하면 런타임에 발생 하는 문제를 쉽게 추적할 수 있습니다. 단, 런타임에는 명확 하지 않은 오류를 통해서만 찾을 수 있습니다.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>모델 변경에 대 한 Code First 마이그레이션 설정

솔루션 탐색기로 이동 합니다. *동영상 .mdf* 파일을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 하 여 동영상 데이터베이스를 제거 합니다. *영화 .mdf* 파일이 표시 되지 않으면 아래에 표시 된 **모든 파일 표시** 아이콘을 빨간색 윤곽선에 클릭 합니다.

![](adding-a-new-field/_static/image1.png)

애플리케이션을 빌드하여 오류가 없는지 확인합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** , **패키지 관리자 콘솔**을 차례로 클릭 합니다.

![Pack Man 추가](adding-a-new-field/_static/image2.png)

**패키지 관리자 콘솔** 창의 프롬프트에 다음을 `PM>` 입력 합니다.

사용-마이그레이션-MovieDBContext

![](adding-a-new-field/_static/image3.png)

위의 **마이그레이션 사용** 명령 (위에 표시 됨)은 새 *마이그레이션* 폴더에 *Configuration.cs* 파일을 만듭니다.

![](adding-a-new-field/_static/image4.png)

Visual Studio에서 *Configuration.cs* 파일을 엽니다. `Seed` *Configuration.cs* 파일의 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

아래의 빨간색 물결선을 마우스로 가리킨 `Movie` `Show Potential Fixes` 다음 클릭 하 고 **mvcmovie를 사용 합니다. 모델을 클릭 합니다.** **using**

![](adding-a-new-field/_static/image5.png)

이렇게 하면 다음 using 문을 추가 합니다.

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First 마이그레이션 `Seed` 은 모든 마이그레이션 후 메서드를 호출 하 고 (즉, 패키지 관리자 콘솔에서 **업데이트-데이터베이스** 를 호출),이 메서드는 이미 삽입 된 행을 업데이트 하거나 아직 존재 하지 않는 경우 삽입 합니다.
> 
> 다음 코드의 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 "upsert" 작업을 수행 합니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> [초기값](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 은 마이그레이션할 때마다 실행 되기 때문에 추가 하려는 행은 데이터베이스를 만드는 첫 번째 마이그레이션 후에 이미 있기 때문에 데이터를 삽입 하기만 하면 됩니다. "[Upsert](http://en.wikipedia.org/wiki/Upsert)" 작업은 이미 있는 행을 삽입 하려고 할 때 발생 하는 오류를 방지 하지만 응용 프로그램을 테스트 하는 동안 수행 된 데이터의 변경 내용을 재정의 합니다. 일부 테이블에서 테스트 데이터를 사용 하는 경우 이러한 상황이 발생 하지 않을 수 있습니다. 테스트 하는 동안 데이터를 변경 하는 경우 데이터베이스 업데이트 후에 변경 내용을 유지 하려는 경우도 있습니다. 조건부 삽입 작업을 수행 하려는 경우: 행이 아직 없는 경우에만 행을 삽입 합니다.   
> 
> [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드에 전달 된 첫 번째 매개 변수는 행이 이미 있는지 여부를 확인 하는 데 사용할 속성을 지정 합니다. 제공 하는 테스트 동영상 데이터의 경우 `Title` 목록에서 각 제목이 고유 하므로 속성을이 용도로 사용할 수 있습니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 이 코드에서는 제목이 고유한 것으로 가정 합니다. 중복 제목을 수동으로 추가 하는 경우 다음에 마이그레이션을 수행할 때 다음과 같은 예외가 발생 합니다.   
> 
> *시퀀스에 둘 이상의 요소가 포함 되어 있습니다.*  
> 
> [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 방법에 대 한 자세한 내용은 [EF 4.3 Addorupdate 메서드를 사용 하 여 처리](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)를 참조 하세요.

**CTRL + SHIFT + B를 눌러 프로젝트를 빌드합니다.** 이 시점에서 빌드하지 않은 경우 다음 단계가 실패 합니다.

다음 단계는 초기 마이그레이션의 클래스를 만드는 것입니다 `DbMigration` . 이 마이그레이션은 새 데이터베이스를 만들기 때문에 이전 단계에서 *영화 .mdf* 파일을 삭제 했습니다.

**패키지 관리자 콘솔** 창에서 명령을 입력 `add-migration Initial` 하 여 초기 마이그레이션을 만듭니다. "초기" 이름은 임의로 생성 되며 만들어진 마이그레이션 파일의 이름을 사용 하는 데 사용 됩니다.

![](adding-a-new-field/_static/image6.png)

Code First 마이그레이션는 *마이그레이션* 폴더 ( *{datestamp} \_ Initial.cs* )에 다른 클래스 파일을 만들고,이 클래스에는 데이터베이스 스키마를 만드는 코드가 포함 되어 있습니다. 마이그레이션 파일 이름은 순서를 지정 하는 데 도움이 되는 타임 스탬프로 미리 고정 되어 있습니다. *{Datestamp} \_ Initial.cs* 파일을 검토 합니다. 여기에는 `Movies` Movie DB에 대 한 테이블을 만드는 지침이 포함 되어 있습니다. 아래 지침에서 데이터베이스를 업데이트 하는 경우이 *{Datestamp} \_ Initial.cs* 파일이 실행 되어 DB 스키마를 만듭니다. 그런 다음 **시드** 메서드를 실행 하 여 DB를 테스트 데이터로 채웁니다.

**패키지 관리자 콘솔**에서 명령을 입력 `update-database` 하 여 데이터베이스를 만들고 메서드를 실행 `Seed` 합니다.

![](adding-a-new-field/_static/image7.png)

테이블이 이미 존재 하 고 만들 수 없음을 나타내는 오류가 발생 하는 경우 데이터베이스를 삭제 하 고 실행 하기 전에 응용 프로그램을 실행 했기 때문일 수 있습니다 `update-database` . 이 경우에는 *동영상 .mdf* 파일을 다시 삭제 하 고 명령을 다시 시도 하십시오 `update-database` . 그래도 오류가 발생 하면 마이그레이션 폴더와 내용을 삭제 한 후이 페이지 맨 위에 있는 지침부터 시작 합니다. 즉, 영화를 삭제 *합니다.* 그래도 오류가 발생 하면 SQL Server 개체 탐색기를 열고 목록에서 데이터베이스를 제거 합니다.

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. 초기값 데이터가 표시 됩니다.

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

기존 클래스에 새 속성을 추가 하 여 시작 `Rating` `Movie` 합니다. *Models\Movie.cs* 파일을 열고 `Rating` 다음과 같은 속성을 추가 합니다.

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

이제 전체 `Movie` 클래스는 다음 코드와 같습니다.

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

응용 프로그램을 빌드합니다 (Ctrl + Shift + B).

클래스에 새 필드를 추가 했으므로 `Movie` 이 새 속성이 포함 되도록 바인딩 *목록* 도 업데이트 해야 합니다. 속성을 `bind` `Create` `Edit` 포함 하도록 및 작업 메서드에 대 한 특성을 업데이트 합니다 `Rating` .

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿도 업데이트해야 합니다.

*\Views\Movies\Index.cshtml* 파일을 열고 `<th>Rating</th>` **Price** 열 바로 뒤에 열 머리글을 추가 합니다. 그런 다음 `<td>` 템플릿 끝 근처에 열을 추가 하 여 값을 렌더링 `@item.Rating` 합니다. 다음은 업데이트 된 *인덱스입니다. cshtml* 뷰 템플릿은 다음과 같습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

그런 다음 *\Views\Movies\Create.cshtml* 파일을 열고 `Rating` 다음 강조 표시 된 태그를 사용 하 여 필드를 추가 합니다. 그러면 새 동영상이 생성 될 때 등급을 지정할 수 있도록 텍스트 상자가 렌더링 됩니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

이제 새 속성을 지원 하도록 응용 프로그램 코드를 업데이트 했습니다 `Rating` .

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. 그러나이 작업을 수행 하면 다음 오류 중 하나가 표시 됩니다.

![](adding-a-new-field/_static/image9.png)  
  
' MovieDBContext ' 컨텍스트를 지 원하는 모델이 데이터베이스를 만든 이후 변경 되었습니다. Code First 마이그레이션를 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 https://go.microsoft.com/fwlink/?LinkId=238269) .

![](adding-a-new-field/_static/image10.png)

`Movie`응용 프로그램의 업데이트 된 모델 클래스가 이제 기존 데이터베이스 테이블의 스키마와 다르기 때문에이 오류가 표시 됩니다 `Movie` . (데이터베이스 테이블에 `Rating` 열이 없습니다.)

이 오류를 해결할 수 있는 몇 가지 방법이 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다. 그러나 단점은 데이터베이스의 기존 데이터를 잃지 않으므로 프로덕션 데이터베이스에서이 방법을 사용 *하지* 않는 것입니다. 테스트 데이터로 데이터베이스를 자동으로 시드하는 데 이니셜라이저를 사용하는 것은 종종 애플리케이션을 개발하는 효율적인 방법입니다. Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터가 유지된다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 수정합니다.

이 자습서의 경우 Code First 마이그레이션을 사용합니다.

초기값 메서드를 업데이트 하 여 새 열에 대 한 값을 제공 합니다. Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 열고 다음 명령을 입력 합니다.

`add-migration Rating`

이 `add-migration` 명령은 마이그레이션 프레임 워크에 현재 MOVIE db 스키마를 사용 하 여 현재 동영상 모델을 검사 하 고 DB를 새 모델로 마이그레이션하는 데 필요한 코드를 만듭니다. 이름 등급은 임의 이며 마이그레이션 파일의 이름을 *지정한* 데 사용 됩니다. 마이그레이션 단계에서 의미 있는 이름을 사용 하는 것이 좋습니다.

이 명령이 완료 되 면 Visual Studio가 새 파생 클래스를 정의 하는 클래스 파일을 열고 `DbMigration` `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

솔루션을 빌드한 다음 `update-database` **패키지 관리자 콘솔** 창에 명령을 입력 합니다.

다음 이미지는 **패키지 관리자 콘솔** 창에 출력을 보여 줍니다 (날짜 스탬프 앞에 나오는 *등급* 은 다름).

![](adding-a-new-field/_static/image11.png)

응용 프로그램을 다시 실행 하 고/또는 비디오 URL로 이동 합니다. 새 등급 필드를 볼 수 있습니다.

![](adding-a-new-field/_static/image12.png)

새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다. 등급을 추가할 수 있습니다.

![7_CreateRioII](adding-a-new-field/_static/image13.png)

**만들기**를 클릭합니다. 이제 등급을 포함 하 여 새 동영상이 영화 목록에 표시 됩니다.

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

이제 프로젝트에서 마이그레이션을 사용 하 고 있으므로 새 필드를 추가 하거나 스키마를 업데이트할 때 데이터베이스를 삭제할 필요가 없습니다. 다음 섹션에서는 더 많은 스키마 변경을 수행 하 고 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.

또한 `Rating` 필드를 편집, 세부 정보 및 삭제 보기 템플릿에 추가 해야 합니다.

스키마가 모델과 일치 하므로 **패키지 관리자 콘솔** 창에서 "업데이트-데이터베이스" 명령을 다시 입력 하면 마이그레이션 코드가 실행 되지 않습니다. 그러나 "upsert"를 실행 하면 메서드가 다시 실행 되며 `Seed` 초기값 데이터를 변경한 경우 메서드에서 데이터를 변경 하면 변경 내용이 손실 됩니다 `Seed` . 이 메서드에 대 한 자세한 내용은 `Seed` Tom Dykstra의 인기 있는 [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에서 확인할 수 있습니다.

이 섹션에서는 모델 개체를 수정 하 고 데이터베이스를 변경 내용과 동기화 된 상태로 유지 하는 방법을 살펴보았습니다. 시나리오를 시험해 볼 수 있도록 새로 만든 데이터베이스를 샘플 데이터로 채우는 방법도 배웠습니다. 이는 Code First에 대 한 간략 한 소개입니다. 주제에 대 한 전체 자습서는 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 참조 하세요. 다음으로 모델 클래스에 더 다양 한 유효성 검사 논리를 추가 하 고 일부 비즈니스 규칙을 적용할 수 있도록 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-search.md)
> [다음](adding-validation.md)
