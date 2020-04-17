---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: 데이터 항수 유효성 검사기(C#)로 유효성 검사 | 마이크로 소프트 문서
author: rick-anderson
description: 데이터 부수 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행합니다. 다양한 유형의 유효성 검사기를 사용하는 방법에 대해 알아봅니다...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542679"
---
# <a name="validation-with-the-data-annotation-validators-c"></a>데이터 주석 유효성 검사기를 사용한 유효성 검사(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> 데이터 부수 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행합니다. 다양한 유형의 유효성 검사기 특성을 사용하고 Microsoft 엔터티 프레임워크에서 유효성 검사기 특성과 함께 작업하는 방법을 알아봅니다.

이 자습서에서는 데이터 별표 유효성 검사기를 사용하여 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행하는 방법을 알아봅니다. 데이터 별표 유효성 검사기를 사용하면 필수 또는 StringLength 특성과 같은 하나 이상의 특성을 클래스 속성에 추가하여 유효성 검사를 수행할 수 있다는 장점이 있습니다.

데이터 주석 유효성 검사기를 사용하려면 먼저 데이터 주석 모델 바인더를 다운로드해야 합니다. 여기를 클릭하여 CodePlex 웹 사이트에서 데이터 주석 모델 바인더 샘플을 다운로드할 수 [있습니다.](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)

데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 프레임워크의 공식 적인 부분이 아니라는 점을 이해하는 것이 중요합니다. 데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 팀에 의해 만들어졌지만 Microsoft는 이 자습서에서 설명하고 사용하는 데이터 주석 모델 바인더에 대한 공식 제품 지원을 제공하지 않습니다.

## <a name="using-the-data-annotation-model-binder"></a>데이터 추가 모델 바인더 사용

ASP.NET MVC 응용 프로그램에서 데이터 주석 모델 바인더를 사용하려면 먼저 Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리 및 System.ComponentModel.DataAnnotations.dll 어셈블리에 대한 참조를 추가해야 합니다. 메뉴 옵션 **프로젝트를 선택, 참조 추가.** 다음으로 **찾아보기** 탭을 클릭하고 데이터 주석 모델 바인더 샘플을 다운로드하고 압축을 풀었던 위치로 이동합니다(그림 **1**참조).

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**그림 1**: 데이터 주석 모델 바인더에 대한 참조 추가[(전체 크기 이미지를 보려면 클릭)](validation-with-the-data-annotation-validators-cs/_static/image3.png)

Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리를 모두 선택하고 **확인** 단추를 클릭합니다.

데이터 주석 모델 바인더가 있는 .NET 프레임워크 서비스 팩 1에 포함된 System.ComponentModel.DataAnnotations.dll 어셈블리는 사용할 수 없습니다. 데이터 주석 모델 바인더 샘플 다운로드에 포함된 System.ComponentModel.DataAnnotations.dll 어셈블리 버전을 사용해야 합니다.

마지막으로 Global.asax 파일에 데이터Annotations 모델 바인더를 등록해야 합니다. 응용\_\_프로그램 Start() 메서드가 다음과 같이 보이도록 다음 코드 줄을 응용 프로그램 Start() 이벤트 처리기에 추가합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

이 코드 줄은 ataAnnotationsModelBinder를 전체 ASP.NET MVC 응용 프로그램의 기본 모델 바인더로 등록합니다.

## <a name="using-the-data-annotation-validator-attributes"></a>데이터 추가 유효성 검사기 특성 사용

데이터 주석 모델 바인더를 사용하는 경우 유효성 검사기 특성을 사용하여 유효성 검사를 수행합니다. System.ComponentModel.DataAnotations 네임스페이스에는 다음 유효성 검사기 특성이 포함됩니다.

- 범위 - 속성 값이 지정된 값 범위 사이에 속하는지 여부를 확인할 수 있습니다.
- 정규 표현식 - 속성 값이 지정된 정규식 패턴과 일치하는지 여부를 확인할 수 있습니다.
- 필수 – 필요에 따라 속성을 표시할 수 있습니다.
- StringLength - 문자열 속성의 최대 길이를 지정할 수 있습니다.
- 유효성 검사 - 모든 유효성 검사기 특성에 대한 기본 클래스입니다.

> [!NOTE] 
> 
> 유효성 검사 요구 사항이 표준 유효성 검사기에 의해 충족되지 않으면 항상 기본 유효성 검사기 특성에서 새 유효성 검사기 특성을 상속하여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.

**목록 1의** 제품 클래스는 이러한 유효성 검사기 특성을 사용하는 방법을 보여 줍니다. 이름, 설명 및 UnitPrice 속성은 필수로 표시됩니다. Name 속성의 문자열 길이는 10자 미만이어야 합니다. 마지막으로 UnitPrice 속성은 통화 금액을 나타내는 정규식 패턴과 일치해야 합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**목록 1**: 모델\Product.cs

Product 클래스는 하나의 추가 특성인 DisplayName 특성을 사용하는 방법을 보여 줍니다. DisplayName 특성을 사용하면 속성이 오류 메시지에 표시될 때 속성 이름을 수정할 수 있습니다. "UnitPrice 필드가 필요합니다"라는 오류 메시지를 표시하는 대신 "가격 필드가 필요합니다"라는 오류 메시지를 표시할 수 있습니다.

> [!NOTE] 
> 
> 유효성 검사기에서 표시되는 오류 메시지를 완전히 사용자 지정하려면 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당할 수 있습니다.`<Required(ErrorMessage:="This field needs a value!")>`

**목록 1의** 제품 클래스를 **목록 2의**Create() 컨트롤러 작업과 함께 사용할 수 있습니다. 이 컨트롤러 작업은 모델 상태에 오류가 있는 경우 뷰 만들기를 다시 표시합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**목록 2**: 컨트롤러\제품컨트롤러.vb

마지막으로 만들기() 작업을 마우스 오른쪽 단추로 클릭하고 **보기 추가**옵션을 선택하여 **목록 3에서** 보기를 만들 수 있습니다. 제품 클래스를 모델 클래스로 사용하여 강력한 형식의 뷰를 만듭니다. 보기 콘텐츠 드롭다운 목록에서 **만들기를** 선택합니다(그림 **2**참조).

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**그림 2**: 뷰 만들기 추가

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**목록 3**: 보기\제품\만들기.aspx

> [!NOTE] 
> 
> **보기 추가** 메뉴 옵션에서 생성된 만들기 양식에서 ID 필드를 제거합니다. Id 필드는 ID 열에 해당하므로 사용자가 이 필드에 대한 값을 입력하도록 허용하지 않습니다.

제품을 만들기 위한 양식을 제출하고 필요한 필드에 대한 값을 입력하지 않으면 그림 **3의** 유효성 검사 오류 메시지가 표시됩니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**그림 3**: 필수 필드 누락

잘못된 통화 금액을 입력하면 **그림 4의** 오류 메시지가 표시됩니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**그림 4**: 유효하지 않은 통화 금액

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>엔터티 프레임워크를 사용하여 데이터 어노미션 유효성 검사기 사용

Microsoft 엔터티 프레임워크를 사용하여 데이터 모델 클래스를 생성하는 경우 클래스에 유효성 검사기 특성을 직접 적용할 수 없습니다. Entity Framework 디자이너는 모델 클래스를 생성하므로 다음에 디자이너를 변경할 때 모델 클래스에 대한 모든 변경 내용이 덮어씁니다.

Entity Framework에서 생성된 클래스와 함께 유효성 검사기를 사용하려면 메타 데이터 클래스를 만들어야 합니다. 유효성 검사기를 실제 클래스에 적용하는 대신 메타 데이터 클래스에 유효성 검사기를 적용합니다.

예를 들어 엔터티 프레임워크를 사용하여 Movie 클래스를 만들었다고 가정합니다(그림 **5**참조). 또한 영화 제목 및 디렉터 속성을 필수 속성으로 만들려는 경우를 가정해 보세요. 이 경우 **목록 4에서**부분 클래스 및 메타 데이터 클래스를 만들 수 있습니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**그림 5**: 엔터티 프레임워크에서 생성된 동영상 클래스

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**목록 4**: 모델\Movie.cs

**리스팅 4의** 파일에는 Movie 및 MovieMetaData라는 두 개의 클래스가 포함되어 있습니다. 동영상 클래스는 부분 클래스입니다. DataModel.Designer.vb 파일에 포함된 엔터티 프레임워크에서 생성된 부분 클래스에 해당합니다.

현재 .NET 프레임워크는 부분 속성을 지원하지 않습니다. 따라서 DataModel.Designer.vb 파일에 정의된 Movie 클래스의 속성에 유효성 검사기 특성을 적용하는 방법은 없습니다. **Listing 4**

동영상 부분 클래스는 MovieMetaData 클래스를 가리키는 MetadataType 특성으로 장식되어 있습니다. MovieMetaData 클래스에는 Movie 클래스의 속성에 대한 프록시 속성이 포함되어 있습니다.

유효성 검사기 특성은 MovieMetaData 클래스의 속성에 적용됩니다. 제목, 디렉터 및 날짜 릴리스 속성은 모두 필수 속성으로 표시됩니다. Director 속성은 5자 미만을 포함하는 문자열을 할당해야 합니다. 마지막으로 DisplayName 특성은 DateReleased 속성에 적용되어 "해제된 날짜 필드가 필요합니다." 등의 오류 메시지가 표시됩니다. 오류 대신 "날짜 릴리스 필드가 필요합니다."

> [!NOTE] 
> 
> MovieMetaData 클래스의 프록시 속성은 Movie 클래스의 해당 속성과 동일한 형식을 나타낼 필요가 없습니다. 예를 들어 Director 속성은 Movie 클래스의 문자열 속성이며 MovieMetaData 클래스의 개체 속성입니다.

**그림 6의** 페이지는 Movie 속성에 대해 잘못된 값을 입력할 때 반환되는 오류 메시지를 보여 줍니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**그림 6**: 엔터티 프레임워크가 있는 유효성 검사기 사용[(전체 크기 이미지를 보려면 클릭)](validation-with-the-data-annotation-validators-cs/_static/image14.png)

## <a name="summary"></a>요약

이 자습서에서는 데이터 별표 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행하는 방법을 배웠습니다. 필수 및 StringLength 특성과 같은 다양한 유형의 유효성 검사기 특성을 사용하는 방법을 배웠습니다. 또한 Microsoft 엔터티 프레임워크로 작업할 때 이러한 특성을 사용하는 방법에 대해서도 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-a-service-layer-cs.md)
> [다음](creating-model-classes-with-the-entity-framework-vb.md)
