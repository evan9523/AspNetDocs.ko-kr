---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '반복 #6 – 테스트 기반 개발(VB) 사용 | 마이크로 소프트 문서'
author: rick-anderson
description: 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성하고 단위 테스트에 대한 코드를 작성하여 응용 프로그램에 새로운 기능을 추가합니다. 이 반복에서,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 8464f4cdee673ef75d561e4cf89613fdca2c16af
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542809"
---
# <a name="iteration-6--use-test-driven-development-vb"></a>반복 #6 - 테스트 중심 개발 사용(VB)

[로 마이크로 소프트](https://github.com/microsoft)

[코드 다운로드](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성하고 단위 테스트에 대한 코드를 작성하여 응용 프로그램에 새로운 기능을 추가합니다. 이 반복에서는 연락처 그룹을 추가합니다.

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

Contact Manager 응용 프로그램의 이전 반복에서 코드에 대한 안전망을 제공하기 위해 단위 테스트를 만들었습니다. 단위 테스트를 만드는 동기는 코드를 보다 탄력적인 변화에 있도록 하는 것이었습니다. 단위 테스트를 통해 코드를 기꺼이 변경하고 기존 기능을 손상했는지 여부를 즉시 알 수 있습니다.

이 반복에서는 완전히 다른 목적을 위해 단위 테스트를 사용합니다. 이 반복에서는 *테스트 기반 개발이라는*응용 프로그램 디자인 철학의 일부로 단위 테스트를 사용합니다. 테스트 기반 개발을 연습할 때 먼저 테스트를 작성한 다음 테스트에 대한 코드를 작성합니다.

보다 정확하게 말하자면, 테스트 기반 개발을 연습할 때 코드를 만들 때 완료하는 세 가지 단계(빨간색/녹색/리팩터링)가 있습니다.

1. 실패하는 단위 테스트 작성(빨간색)
2. 단위 테스트를 통과하는 코드 작성(녹색)
3. 코드 리팩터링(리팩터링)

먼저 단위 테스트를 작성합니다. 단위 테스트는 코드의 행동 방식에 대한 의도를 표현해야 합니다. 단위 테스트를 처음 만들 때 단위 테스트가 실패해야 합니다. 테스트를 제공하는 응용 프로그램 코드를 아직 작성하지 않았기 때문에 테스트가 실패해야 합니다.

다음으로 단위 테스트를 통과하기 위해 충분한 코드를 작성합니다. 목표는 가장 게으른, 조잡하고 가장 빠른 방법으로 코드를 작성하는 것입니다. 응용 프로그램의 아키텍처에 대해 생각하는 데 시간을 낭비해서는 안 됩니다. 대신 단위 테스트에서 표현된 의도를 충족하는 데 필요한 최소한의 코드를 작성하는 데 중점을 두어야 합니다.

마지막으로 충분한 코드를 작성한 후 한 걸음 물러서서 응용 프로그램의 전체 아키텍처를 고려할 수 있습니다. 이 단계에서는 리포지토리 패턴과 같은 소프트웨어 디자인 패턴을 활용하여 코드를 다시 작성(리팩터링)하여 코드를 보다 유지 관리할 수 있도록 합니다. 코드는 단위 테스트에서 다루기 때문에 이 단계에서 코드를 두려움 없이 다시 작성할 수 있습니다.

테스트 기반 개발을 연습하면 얻을 수 있는 많은 이점이 있습니다. 첫째, 테스트 기반 개발을 통해 실제로 작성해야 하는 코드에 집중해야 합니다. 특정 테스트를 통과하기에 충분한 코드를 작성하는 데 계속 집중하기 때문에 잡초를 방황하고 사용하지 않을 엄청난 양의 코드를 작성하는 것을 방지할 수 있습니다.

둘째, "테스트 우선" 디자인 방법론을 사용하면 코드를 사용하는 방식의 관점에서 코드를 작성해야 합니다. 즉, 테스트 기반 개발을 연습할 때 사용자 관점에서 테스트를 지속적으로 작성합니다. 따라서 테스트 기반 개발은 더 깨끗하고 이해하기 쉬운 API를 생성할 수 있습니다.

마지막으로 테스트 기반 개발은 응용 프로그램을 작성하는 일반적인 프로세스의 일부로 단위 테스트를 작성해야 합니다. 프로젝트 기한이 다가오면 일반적으로 테스트가 가장 먼저 창 밖으로 나가는 것입니다. 반면에 테스트 기반 개발을 연습할 때는 테스트 기반 개발로 인해 단위 테스트가 응용 프로그램을 빌드하는 프로세스의 중심이 되므로 단위 테스트를 작성하는 데 더 유덕할 수 있습니다.

> [!NOTE] 
> 
> 테스트 기반 개발에 대해 자세히 알아보려면 Michael Feathers 책을 **레거시 코드로 효과적으로 작업하는**것을 읽는 것이 좋습니다.

이 반복에서는 연락처 관리자 응용 프로그램에 새 기능을 추가합니다. 연락처 그룹에 대한 지원을 추가합니다. 연락처 그룹을 사용하여 연락처를 비즈니스 및 친구 그룹과 같은 범주로 구성할 수 있습니다.

테스트 기반 개발 프로세스에 따라 이 새로운 기능을 응용 프로그램에 추가하겠습니다. 먼저 단위 테스트를 작성하고 이러한 테스트에 대해 모든 코드를 작성합니다.

## <a name="what-gets-tested"></a>테스트되는 내용

이전 반복에서 설명한 것처럼 일반적으로 데이터 액세스 논리 또는 뷰 논리에 대한 단위 테스트를 작성하지 않습니다. 데이터베이스에 액세스하는 작업은 비교적 느린 작업이므로 데이터 액세스 논리에 대한 단위 테스트를 작성하지 마십시오. 뷰에 액세스하려면 상대적으로 느린 작업인 웹 서버를 회전해야 하므로 뷰 논리에 대한 단위 테스트를 작성하지 마십시오. 테스트를 반복해서 실행할 수 없다면 단위 테스트를 작성해서는 안 됩니다.

테스트 기반 개발은 단위 테스트에 의해 구동되므로 처음에는 컨트롤러 및 비즈니스 논리 작성에 중점을 둡니다. 데이터베이스 나 뷰를 건드리지 마십시오. 이 자습서의 맨 끝까지 데이터베이스를 수정하거나 뷰를 만들지 않습니다. 우리는 테스트 할 수있는 것으로 시작합니다.

## <a name="creating-user-stories"></a>사용자 스토리 만들기

테스트 기반 개발을 연습할 때는 항상 테스트를 작성하는 것으로 시작합니다. 이것은 즉시 질문을 제기 : 당신은 어떻게 먼저 작성할 테스트를 결정합니까? 이 질문에 대답하려면 [*사용자 스토리*](http://en.wikipedia.org/wiki/User_stories)집합을 작성해야 합니다.

사용자 스토리는 소프트웨어 요구 사항에 대한 매우 간략한 설명입니다(일반적으로 한 문장) 사용자 관점에서 작성된 요구 사항에 대한 비기술적 설명이어야 합니다.

다음은 새 연락처 그룹 기능에 필요한 기능을 설명하는 사용자 스토리 집합입니다.

1. 사용자는 연락처 그룹 목록을 볼 수 있습니다.
2. 사용자는 새 연락처 그룹을 만들 수 있습니다.
3. 사용자는 기존 연락처 그룹을 삭제할 수 있습니다.
4. 사용자는 새 연락처를 만들 때 연락처 그룹을 선택할 수 있습니다.
5. 사용자는 기존 연락처를 편집할 때 연락처 그룹을 선택할 수 있습니다.
6. 연락처 그룹 목록이 색인 보기에 표시됩니다.
7. 사용자가 연락처 그룹을 클릭하면 일치하는 연락처 목록이 표시됩니다.

이 사용자 스토리 목록은 고객이 완전히 이해할 수 있습니다. 기술 구현 세부 사항에 대한 언급은 없습니다.

응용 프로그램을 빌드하는 동안 사용자 스토리 집합이 더 구체화될 수 있습니다. 사용자 스토리를 여러 스토리(요구 사항)로 나누면 됩니다. 예를 들어 새 연락처 그룹을 만드는 데 유효성 검사가 포함되도록 결정할 수 있습니다. 이름 없이 연락처 그룹을 제출하면 유효성 검사 오류가 반환됩니다.

사용자 스토리 목록을 만든 후 첫 번째 단위 테스트를 작성할 준비가 된 것입니다. 먼저 연락처 그룹 목록을 보기 위한 단위 테스트를 만듭니다.

## <a name="listing-contact-groups"></a>연락처 그룹 목록

첫 번째 사용자 스토리는 사용자가 연락처 그룹 목록을 볼 수 있어야 한다는 것입니다. 우리는 시험으로이 이야기를 표현할 필요가있다.

ContactManager.Test 프로젝트에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭하고 **추가, 새 테스트**를 선택하고 **단위 테스트** 템플릿을 선택하여 새 단위 테스트를 만듭니다(그림 1 참조). 새 단위 테스트 GroupControllerTest.vb의 이름을 지정하고 **확인** 단추를 클릭합니다.

[![그룹컨트롤러테스트 단위 테스트 추가](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**그림 01**: GroupControllerTest 단위 테스트 추가[(클릭하여 전체 크기 이미지 보기)](iteration-6-use-test-driven-development-vb/_static/image2.png)

우리의 첫 번째 단위 테스트는 목록 1에 포함되어 있습니다. 이 테스트는 그룹 컨트롤러의 Index() 메서드가 그룹 집합을 반환하는지 확인합니다. 이 테스트는 그룹 컬렉션이 뷰 데이터에서 반환되는지 확인합니다.

**목록 1 - 컨트롤러\그룹컨트롤러테스트.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

Visual Studio에서 목록 1에 코드를 처음 입력하면 빨간색 구불구불한 선이 많이 표시됩니다. 그룹 컨트롤러 또는 그룹 클래스를 만들지 않았습니다.

이 시점에서 첫 번째 단위 테스트를 실행할 수 없도록 응용 프로그램을 빌드할 수도 없습니다. 그건 좋은. 이는 실패한 테스트로 계산됩니다. 따라서 이제 응용 프로그램 코드 작성을 시작할 수 있습니다. 테스트를 실행하기에 충분한 코드를 작성해야 합니다.

목록 2의 그룹 컨트롤러 클래스에는 단위 테스트를 통과하는 데 필요한 최소 코드가 포함되어 있습니다. Index() 작업은 정적으로 코딩된 그룹 목록을 반환합니다(그룹 클래스는 목록 3에 정의되어 있음).

**목록 2 - 컨트롤러\그룹Controller.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**목록 3 - 모델\그룹.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

프로젝트에 GroupController 및 그룹 클래스를 추가한 후 첫 번째 단위 테스트가 성공적으로 완료됩니다(그림 2 참조). 우리는 시험을 통과하는 데 필요한 최소한의 작업을 수행했습니다. 축하할 시간입니다.

[![성공!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**그림 02**: 성공! (전체[크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image4.png)

## <a name="creating-contact-groups"></a>연락처 그룹 만들기

이제 두 번째 사용자 스토리로 넘어갈 수 있습니다. 새 연락처 그룹을 만들 수 있어야 합니다. 우리는 테스트와 함께이 의도를 표현할 필요가있다.

목록 4의 테스트는 Create() 메서드를 새 그룹과 호출하면 Index() 메서드에서 반환되는 그룹 목록에 그룹을 추가하는지 확인합니다. 즉, 새 그룹을 만들면 Index() 메서드에서 반환되는 그룹 목록에서 새 그룹을 다시 얻을 수 있습니다.

**목록 4 - 컨트롤러\그룹컨트롤러테스트.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

목록 4의 테스트는 새 연락처 그룹과 그룹 컨트롤러 Create() 메서드를 호출합니다. 그런 다음 테스트는 그룹 컨트롤러 Index() 메서드를 호출하면 뷰 데이터에서 새 그룹이 반환되는지 확인합니다.

목록 5의 수정된 그룹 컨트롤러에는 새 테스트를 통과하는 데 필요한 최소한의 변경 내용이 포함되어 있습니다.

**목록 5 - 컨트롤러\그룹Controller.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>목록 5의 그룹 컨트롤러에는 새 Create() 작업이 있습니다. 이 작업은 그룹의 컬렉션에 그룹을 추가합니다. 그룹 컬렉션의 내용을 반환하도록 Index() 작업이 수정되었습니다.

다시 한번, 우리는 단위 테스트를 통과하는 데 필요한 최소한의 작업을 수행했습니다. 그룹 컨트롤러를 변경하면 모든 단위 테스트가 통과합니다.

## <a name="adding-validation"></a>유효성 검사 추가

이 요구 사항은 사용자 스토리에 명시적으로 명시되지 않았습니다. 그러나 그룹에 이름을 지정하도록 요구하는 것은 합리적입니다. 그렇지 않으면 연락처를 그룹으로 구성하는 것은 매우 유용하지 않습니다.

목록 6에는 이러한 의도를 표현하는 새 테스트가 포함되어 있습니다. 이 테스트는 이름을 제공하지 않고 그룹을 만들려고 하면 모델 상태의 유효성 검사 오류 메시지가 발생한다는 것을 확인합니다.

**목록 6 - 컨트롤러\그룹컨트롤러테스트.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

이 테스트를 충족하려면 그룹 클래스에 Name 속성을 추가해야 합니다(목록 7 참조). 또한 그룹 컨트롤러의 Create() 작업에 약간의 유효성 검사 논리를 추가해야 합니다(목록 8 참조).

**목록 7 - 모델\그룹.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**목록 8 - 컨트롤러\그룹Controller.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

그룹 컨트롤러 Create() 작업에는 유효성 검사 및 데이터베이스 논리가 모두 포함되어 있습니다. 현재 그룹 컨트롤러에서 사용하는 데이터베이스는 인메모리 컬렉션에 불과합니다.

## <a name="time-to-refactor"></a>리팩터링 시간

빨간색/녹색/리팩터링의 세 번째 단계는 리팩터링 부분입니다. 이 시점에서 코드에서 한 발 물러서서 디자인을 개선하기 위해 응용 프로그램을 리팩터링하는 방법을 고려해야 합니다. 리팩터링 단계는 소프트웨어 디자인 원칙과 패턴을 구현하는 가장 좋은 방법에 대해 열심히 생각하는 단계입니다.

코드 디자인을 개선하기 위해 선택한 방식으로 코드를 자유롭게 수정할 수 있습니다. 우리는 기존의 기능을 위반에서 우리를 방지 단위 테스트의 안전 망이있다.

지금, 우리의 그룹 컨트롤러는 좋은 소프트웨어 디자인의 관점에서 엉망입니다. 그룹 컨트롤러에는 유효성 검사 및 데이터 액세스 코드가 엉망입니다. 단일 책임 원칙을 위반하지 않으려면 이러한 문제를 다른 클래스로 구분해야 합니다.

리팩터링된 그룹 컨트롤러 클래스는 리스팅 9에 포함되어 있습니다. 컨트롤러가 ContactManager 서비스 계층을 사용하도록 수정되었습니다. 이 계층은 Contact 컨트롤러와 함께 사용하는 것과 동일한 서비스 계층입니다.

목록 10에는 그룹의 유효성 검사, 목록 및 만들기를 지원하기 위해 ContactManager 서비스 계층에 추가된 새 메서드가 포함되어 있습니다. IContactManagerService 인터페이스는 새 메서드를 포함하도록 업데이트되었습니다.

목록 11에는 IContactManagerRepository 인터페이스를 구현하는 새로운 FakeContactManagerRepository 클래스가 포함되어 있습니다. 또한 IContactManagerRepository 인터페이스를 구현 하는 EntityContactManagerRepository 클래스와 달리, 우리의 새로운 FakeContactManager Repository 클래스 데이터베이스와 통신 하지 않습니다. FakeContactManagerRepository 클래스는 데이터베이스의 프록시로 메모리 내 컬렉션을 사용합니다. 단위 테스트에서 이 클래스를 가짜 리포지토리 계층으로 사용합니다.

**목록 9 - 컨트롤러\그룹Controller.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**목록 10 - 컨트롤러\연락처관리자서비스.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**목록 11 - 컨트롤러\가짜접촉관리자리포시토리.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

IContactManagerRepository 인터페이스를 수정하려면 EntityContactManagerRepository 클래스에서 CreateGroup() 및 ListGroups() 메서드를 구현하는 데 필요합니다. 이 작업을 수행하는 가장 름것처럼 가장 빠르고 가장 빠른 방법은 다음과 같은 스텁 메서드를 추가하는 것입니다.

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

마지막으로 응용 프로그램의 디자인을 변경하려면 단위 테스트를 일부 수정해야 합니다. 이제 단위 테스트를 수행할 때 FakeContactManagerRepository를 사용해야 합니다. 업데이트된 GroupControllerTest 클래스는 목록 12에 포함되어 있습니다.

**목록 12 - 컨트롤러\그룹컨트롤러테스트.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

이러한 모든 변경 사항을 모두 변경한 후 다시 한 번 모든 단위 테스트가 통과합니다. 빨간색/녹색/리팩터링의 전체 주기를 완료했습니다. 처음 두 사용자 스토리를 구현했습니다. 이제 사용자 스토리에 표현된 요구 사항에 대한 지원 단위 테스트가 있습니다. 나머지 사용자 스토리를 구현하려면 빨간색/녹색/리팩터링의 동일한 주기를 반복해야 합니다.

## <a name="modifying-our-database"></a>데이터베이스 수정

안타깝게도 단위 테스트에서 표현한 모든 요구 사항을 충족했음에도 불구하고 작업이 완료되지 않았습니다. 데이터베이스를 수정해야 합니다.

새 그룹 데이터베이스 테이블을 만들어야 합니다. 다음 단계를 수행하세요.

1. 서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션을 **선택합니다.**
2. 표 디자이너에 아래에 설명된 두 열을 입력합니다.
3. Id 열을 기본 키 및 ID 열로 표시합니다.
4. 플로피 아이콘을 클릭하여 그룹 이름으로 새 테이블을 저장합니다.

<a id="0.12_table01"></a>

| **열 이름** | **데이터 유형** | **Null 허용** |
| --- | --- | --- |
| Id | int | False |
| 속성 | nvarchar(50) | False |

다음으로 연락처 테이블에서 모든 데이터를 삭제해야 합니다(그렇지 않으면 연락처 및 그룹 테이블 간의 관계를 만들 수 없습니다). 다음 단계를 수행하세요.

1. 연락처 테이블을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **테이블 데이터 표시를**선택합니다.
2. 모든 행을 삭제합니다.

다음으로 그룹 데이터베이스 테이블과 기존 연락처 데이터베이스 테이블 간의 관계를 정의해야 합니다. 다음 단계를 수행하세요.

1. 서버 탐색기 창에서 연락처 테이블을 두 번 클릭하여 테이블 디자이너를 엽니다.
2. GroupId라는 연락처 테이블에 새 정수 열을 추가합니다.
3. 관계 단추를 클릭하여 외래 키 관계 대화 상자를 엽니다(그림 3 참조).
4. 추가 단추를 클릭합니다.
5. 표 및 열 사양 버튼 옆에 나타나는 타원 단추를 클릭합니다.
6. 테이블 및 열 대화 상자에서 그룹을 기본 키 테이블로 선택하고 Id를 기본 키 열로 선택합니다. 연락처를 외래 키 테이블로 선택하고 GroupId를 외래 키 열로 선택합니다(그림 4 참조). 확인 단추를 클릭합니다.
7. **삽입 및 업데이트 사양에서**규칙 **삭제에**대한 **캐스케이드** 값을 선택합니다.
8. 종료 단추를 클릭하여 외래 키 관계 대화 상자를 닫습니다.
9. 연락처 테이블에 변경 내용을 저장하려면 저장 단추를 클릭합니다.

[![데이터베이스 테이블 관계 만들기](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**그림 03**: 데이터베이스 테이블 관계 만들기[(전체 크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image6.png)

[![테이블 관계 지정](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**그림 04**: 테이블 관계 지정[(전체 크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image8.png)

### <a name="updating-our-data-model"></a>데이터 모델 업데이트

다음으로 새 데이터베이스 테이블을 나타내도록 데이터 모델을 업데이트해야 합니다. 다음 단계를 수행하세요.

1. 모델 폴더에서 ContactManagerModel.edmx 파일을 두 번 클릭하여 엔터티 디자이너를 엽니다.
2. 디자이너 표면을 마우스 오른쪽 단추로 클릭하고 **데이터베이스에서 모델 업데이트**메뉴 옵션을 선택합니다.
3. 업데이트 마법사에서 그룹 테이블을 선택하고 완료 단추를 클릭합니다(그림 5 참조).
4. 그룹 엔터티를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **이름을 선택합니다.** 그룹 엔터티의 이름을 *그룹(단수)으로* 변경합니다. *Group*
5. 연락처 엔터티의 맨 아래에 표시되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭합니다. *그룹* 탐색 속성의 이름을 *Group* 그룹(단수)으로 변경합니다.

[![데이터베이스에서 엔터티 프레임워크 모델 업데이트](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**그림 05**: 데이터베이스에서 엔터티 프레임워크 모델[업데이트(전체 크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image10.png)

이 단계를 완료하면 데이터 모델이 연락처 및 그룹 테이블을 모두 나타냅니다. 엔터티 디자이너는 두 엔터티를 모두 표시해야 합니다(그림 6 참조).

[![그룹 및 연락처를 표시하는 엔터티 디자이너](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**그림 06**: 그룹 및 연락처를 표시하는 엔터티 디자이너[(전체 크기 이미지를 보려면 클릭하십시오)](iteration-6-use-test-driven-development-vb/_static/image12.png)

### <a name="creating-our-repository-classes"></a>리포지토리 클래스 만들기

다음으로 저장소 클래스를 구현해야 합니다. 이 반복 과정에서 단위 테스트를 만족시키기 위해 코드를 작성하는 동안 IContactManagerRepository 인터페이스에 몇 가지 새로운 메서드를 추가했습니다. IContactManagerRepository 인터페이스의 최종 버전은 목록 14에 포함되어 있습니다.

**목록 14 - 모델\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

실제 EntityContactManagerRepository 클래스에서 연락처 그룹과 작업하는 방법과 관련된 메서드를 실제로 구현하지 않았습니다. 현재 EntityContactManagerRepository 클래스에는 IContactManagerRepository 인터페이스에 나열된 각 연락처 그룹 메서드에 대한 스텁 메서드가 있습니다. 예를 들어 ListGroups() 메서드는 현재 다음과 같습니다.

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

스텁 메서드를 통해 응용 프로그램을 컴파일하고 단위 테스트를 통과할 수 있었습니다. 그러나 이제는 이러한 메서드를 실제로 구현해야 할 때입니다. EntityContactManagerRepository 클래스의 최종 버전은 목록 13에 포함되어 있습니다.

**목록 13 - 모델\엔터티연락처관리자Repository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>뷰 만들기

기본 ASP.NET 뷰 엔진을 사용할 때 MVC 응용 프로그램을 ASP.NET. 따라서 특정 단위 테스트에 대한 응답으로 뷰를 만들지 않아도 됩니다. 그러나 뷰없이 응용 프로그램은 쓸모가 없기 때문에 연락처 관리자 응용 프로그램에 포함된 뷰를 만들고 수정하지 않고는 이 반복을 완료할 수 없습니다.

연락처 그룹을 관리하기 위해 다음과 같은 새 보기를 만들어야 합니다(그림 7 참조).

- 뷰\그룹\인덱스.aspx - 연락처 그룹 목록을 표시합니다.
- 뷰\그룹\Delete.aspx - 연락처 그룹을 삭제하기 위한 확인 양식을 표시합니다.

[![그룹 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**그림 07**: 그룹 색인[보기(전체 크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image14.png)

연락처 그룹을 포함하도록 다음 기존 뷰를 수정해야 합니다.

- 뷰\홈\만들기.aspx
- 뷰\홈\편집.aspx
- 뷰\홈\인덱스.aspx

이 자습서와 함께 제공되는 Visual Studio 응용 프로그램을 확인하여 수정된 보기를 볼 수 있습니다. 예를 들어 그림 8은 연락처 인덱스 뷰를 보여 줍니다.

[![연락처 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**그림 08**: 연락처 색인 보기[(전체 크기 이미지를 보려면 클릭)](iteration-6-use-test-driven-development-vb/_static/image16.png)

## <a name="summary"></a>요약

이 반복에서는 테스트 기반 개발 응용 프로그램 디자인 방법론을 따라 연락처 관리자 응용 프로그램에 새로운 기능을 추가했습니다. 우리는 사용자 스토리 세트를 만드는 것으로 시작했습니다. 사용자 스토리에서 표현하는 요구 사항에 해당하는 단위 테스트 집합을 만들었습니다. 마지막으로 단위 테스트에서 표현한 요구 사항을 충족하기에 충분한 코드를 작성했습니다.

단위 테스트에서 표현된 요구 사항을 충족하기에 충분한 코드 작성을 마친 후 데이터베이스와 뷰를 업데이트했습니다. 데이터베이스에 새 그룹 테이블을 추가하고 엔터티 프레임워크 데이터 모델을 업데이트했습니다. 또한 뷰 집합을 만들고 수정했습니다.

다음 반복에서 최종 반복은 Ajax를 활용하기 위해 응용 프로그램을 다시 작성합니다. Ajax를 활용 하 여, 우리는 응답 성과 연락처 관리자 응용 프로그램의 성능을 향상 시킬 거 야.

> [!div class="step-by-step"]
> [이전](iteration-5-create-unit-tests-vb.md)
> [다음](iteration-7-add-ajax-functionality-vb.md)
