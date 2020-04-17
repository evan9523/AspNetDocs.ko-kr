---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '반복 #3 – 양식 유효성 검사(VB) 추가 | 마이크로 소프트 문서'
author: rick-anderson
description: 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 필수 양식 필드를 작성하지 않고 양식을 제출하지 못하도록 합니다. 우리는 또한 emai를 검증 ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ee2f40996873a7af2eaa255edd5f157c3fefb29
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542393"
---
# <a name="iteration-3--add-form-validation-vb"></a>반복 #3 - 양식 유효성 검사 추가(VB)

[로 마이크로 소프트](https://github.com/microsoft)

[코드 다운로드](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 필수 양식 필드를 작성하지 않고 양식을 제출하지 못하도록 합니다. 또한 이메일 주소와 전화 번호의 유효성을 검사합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램(VB) 구축

이 자습서 시리즈에서는 처음부터 끝까지 전체 연락처 관리 응용 프로그램을 빌드합니다. 연락처 관리자 응용 프로그램을 사용하면 사람 목록에 대한 연락처 정보(이름, 전화 번호 및 이메일 주소)를 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 반복할 때마다 응용 프로그램이 점차 개선됩니다. 이 여러 반복 접근 방식의 목표는 각 변경의 이유를 이해할 수 있도록 하는 것입니다.

- 반복 #1 - 응용 프로그램을 만듭니다. 첫 번째 반복에서는 가능한 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업에 대한 지원을 추가합니다: CRUD 만들기, 읽기, 업데이트 및 삭제.

- 반복 #2 - 응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 계단식 스타일 시트를 수정하여 응용 프로그램의 모양을 개선합니다.

- 반복 #3 - 양식 유효성 검사를 추가합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 필수 양식 필드를 작성하지 않고 양식을 제출하지 못하도록 합니다. 또한 이메일 주소와 전화 번호의 유효성을 검사합니다.

- 반복 #4 - 응용 프로그램을 느슨하게 결합합니다. 이 네 번째 반복에서는 여러 소프트웨어 디자인 패턴을 활용하여 Contact Manager 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 합니다.

- 반복 #5 - 단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가하여 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있도록 합니다. 데이터 모델 클래스를 모의하고 컨트롤러 및 유효성 검사 논리에 대한 단위 테스트를 빌드합니다.

- 반복 #6 - 테스트 기반 개발을 사용합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성하고 단위 테스트에 대한 코드를 작성하여 응용 프로그램에 새로운 기능을 추가합니다. 이 반복에서는 연락처 그룹을 추가합니다.

- 반복 #7 - Ajax 기능을 추가합니다. 일곱 번째 반복에서는 Ajax에 대한 지원을 추가하여 응용 프로그램의 응답성과 성능을 향상시킵니다.

## <a name="this-iteration"></a>이 반복

연락처 관리자 응용 프로그램의 이 두 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 필수 양식 필드에 대한 값을 입력하지 않고 연락처를 제출하지 못하도록 합니다. 또한 전화 번호와 이메일 주소의 유효성을 검사합니다(그림 1 참조).

[![새 프로젝트 대화 상자](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**그림 01**: 유효성 검사가 있는[양식(전체 크기 이미지를 보려면 클릭)](iteration-3-add-form-validation-vb/_static/image2.png)

이 반복에서는 유효성 검사 논리를 컨트롤러 작업에 직접 추가합니다. 일반적으로 이 방법은 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가하는 데 권장되지 않습니다. 더 나은 방법은 응용 프로그램 유효성 검사 논리를 별도의 [서비스 계층에](http://martinfowler.com/eaaCatalog/serviceLayer.html)배치하는 것입니다. 다음 반복에서는 응용 프로그램을 보다 유지 관리할 수 있도록 연락처 관리자 응용 프로그램을 리팩터링합니다.

이 반복에서는 작업을 단순하게 유지하기 위해 모든 유효성 검사 코드를 직접 작성합니다. 유효성 검사 코드를 작성하는 대신 유효성 검사 프레임워크를 활용할 수 있습니다. 예를 들어 VAB(Microsoft 엔터프라이즈 라이브러리 유효성 검사 응용 프로그램 블록)를 사용하여 ASP.NET MVC 응용 프로그램에 대한 유효성 검사 논리를 구현할 수 있습니다. 유효성 검사 응용 프로그램 블록에 대한 자세한 내용은 다음을 참조하십시오.

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>만들기 보기에 유효성 검사 추가

먼저 만들기 보기에 유효성 검사 논리를 추가합니다. 다행히 Visual Studio를 사용하여 만들기 뷰를 생성했기 때문에 만들기 보기에는 유효성 검사 메시지를 표시하는 데 필요한 모든 사용자 인터페이스 논리가 이미 포함되어 있습니다. 만들기 뷰는 목록 1에 포함되어 있습니다.

**목록 1 - \뷰\연락처\만들기.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

필드 유효성 검사 오류 클래스는 Html.ValidationMessage() 도우미에서 렌더링한 출력의 스타일을 만드는 데 사용됩니다. 입력 유효성 검사 오류 클래스는 Html.TextBox() 도우미가 렌더링한 텍스트 상자(입력)의 스타일을 만드는 데 사용됩니다. 유효성 검사 요약 오류 클래스는 Html.ValidationSummary() 도우미에서 렌더링한 정렬되지 않은 목록의 스타일을 지정하는 데 사용됩니다.

> [!NOTE] 
> 
> 이 섹션에 설명된 스타일 시트 클래스를 수정하여 유효성 검사 오류 메시지의 모양을 사용자 지정할 수 있습니다.

## <a name="adding-validation-logic-to-the-create-action"></a>만들기 작업에 유효성 검사 논리 추가

현재 Create 보기에는 메시지를 생성하는 논리를 작성하지 않았기 때문에 유효성 검사 오류 메시지가 표시되지 않습니다. 유효성 검사 오류 메시지를 표시하려면 ModelState에 오류 메시지를 추가해야 합니다.

> [!NOTE] 
> 
> UpdateModel() 메서드는 속성에 양식 필드의 값을 할당하는 오류가 있는 경우 ModelState에 오류 메시지를 자동으로 추가합니다. 예를 들어 DateTime 값을 허용하는 BirthDate 속성에 문자열 "apple"을 할당하려고 하면 UpdateModel() 메서드가 ModelState에 오류를 추가합니다.

목록 2의 수정된 Create() 메서드에는 새 연락처가 데이터베이스에 삽입되기 전에 Contact 클래스의 속성을 확인하는 새 섹션이 포함되어 있습니다.

**목록 2 - 컨트롤러\ContactController.vb(유효성 검사로 만들기)**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

유효성 검사 섹션에서는 네 가지 고유한 유효성 검사 규칙을 적용합니다.

- FirstName 속성의 길이가 0보다 커야 하며 공백으로만 구성할 수 없습니다.
- LastName 속성의 길이가 0보다 커야 하며 공백으로만 구성할 수 없습니다.
- Phone 속성의 값이 (길이가 0보다 큰) 경우 Phone 속성은 정규식과 일치해야 합니다.
- Email 속성의 값이 0보다 큰 경우 Email 속성은 정규식과 일치해야 합니다.

유효성 검사 규칙 위반이 있는 경우 AddModelError() 메서드의 도움으로 모델 상태에 오류 메시지가 추가 됩니다. ModelState에 메시지를 추가하면 속성 이름과 유효성 검사 오류 메시지의 텍스트를 제공합니다. 이 오류 메시지는 Html.ValidationSummary() 및 Html.ValidationMessage() 도우미 메서드에 의해 보기에 표시됩니다.

유효성 검사 규칙이 실행된 후 모델상태의 IsValid 속성이 검사됩니다. 유효성 검사 오류 메시지가 ModelState에 추가된 경우 IsValid 속성은 false를 반환합니다. 유효성 검사가 실패하면 만들기 양식이 오류 메시지와 함께 다시 표시됩니다.

> [!NOTE] 
> 
> 정규식 리포지토리에서 전화 번호와 전자 메일 주소를 검증하기 위한 정규식을 얻었습니다.[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>편집 작업에 유효성 검사 논리 추가

편집() 작업은 연락처를 업데이트합니다. 편집() 작업은 Create() 작업과 정확히 동일한 유효성 검사를 수행해야 합니다. 동일한 유효성 검사 코드를 복제하는 대신 Create() 및 Edit() 작업이 동일한 유효성 검사 메서드를 호출할 수 있도록 연락처 컨트롤러를 리팩터링해야 합니다.

수정된 연락처 컨트롤러 클래스는 목록 3에 포함되어 있습니다. 이 클래스에는 Create() 및 Edit() 작업 모두에서 호출되는 새 ValidateContact() 메서드가 있습니다.

**목록 3 - 컨트롤러\연락처Controller.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 기본 양식 유효성 검사를 추가했습니다. 유효성 검사 논리는 사용자가 FirstName 및 LastName 속성에 대한 값을 제공하지 않고 새 연락처를 제출하거나 기존 연락처를 편집할 수 없도록 합니다. 또한 사용자는 유효한 전화 번호와 이메일 주소를 제공해야 합니다.

이 반복에서는 가능한 가장 쉬운 방법으로 연락처 관리자 응용 프로그램에 유효성 검사 논리를 추가했습니다. 그러나 유효성 검사 논리를 컨트롤러 논리에 혼합하면 장기적으로 문제가 발생합니다. 우리의 응용 프로그램은 유지 보수 및 시간이 지남에 따라 수정하기가 더 어려울 것입니다.

다음 반복에서는 컨트롤러에서 유효성 검사 논리 및 데이터베이스 액세스 논리를 리팩터링합니다. 몇 가지 소프트웨어 디자인 원칙을 활용하여 보다 느슨하게 결합되고 유지 관리 가능한 응용 프로그램을 만들 수 있습니다.

> [!div class="step-by-step"]
> [이전](iteration-2-make-the-application-look-nice-vb.md)
> [다음](iteration-4-make-the-application-loosely-coupled-vb.md)
