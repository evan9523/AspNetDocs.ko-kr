---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: '반복 #4 – 응용 프로그램을 느슨하게 결합(C#) | 마이크로 소프트 문서'
author: rick-anderson
description: 이 네 번째 반복에서는 여러 소프트웨어 디자인 패턴을 활용하여 Contact Manager 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있습니다. For...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542367"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>반복 #4 – 애플리케이션을 느슨하게 결합(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[코드 다운로드](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 이 네 번째 반복에서는 여러 소프트웨어 디자인 패턴을 활용하여 Contact Manager 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>연락처 관리 ASP.NET MVC 응용 프로그램(C#) 구축

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

연락처 관리자 응용 프로그램의 네 번째 반복에서는 응용 프로그램을 보다 느슨하게 결합하도록 응용 프로그램을 리팩터링합니다. 응용 프로그램이 느슨하게 결합된 경우 응용 프로그램의 다른 부분에서 코드를 수정할 필요 없이 응용 프로그램의 한 부분에서 코드를 수정할 수 있습니다. 느슨하게 결합된 응용 프로그램은 변경에 더 탄력적입니다.

현재 Contact Manager 응용 프로그램에서 사용하는 모든 데이터 액세스 및 유효성 검사 논리는 컨트롤러 클래스에 포함되어 있습니다. 이것은 나쁜 생각이다. 응용 프로그램의 한 부분을 수정해야 할 때마다 응용 프로그램의 다른 부분에 버그가 발생할 위험이 있습니다. 예를 들어 유효성 검사 논리를 수정하면 데이터 액세스 또는 컨트롤러 논리에 새 버그가 발생할 위험이 있습니다.

> [!NOTE] 
> 
> (SRP) 클래스는 변경할 이유가 두 개 이상 없어야 합니다. 컨트롤러, 유효성 검사 및 데이터베이스 논리를 혼합하는 것은 단일 책임 원칙을 크게 위반하는 것입니다.

응용 프로그램을 수정해야 하는 몇 가지 이유가 있습니다. 응용 프로그램에 새 기능을 추가해야 하거나, 응용 프로그램에서 버그를 수정해야 하거나, 응용 프로그램의 기능이 구현되는 방식을 수정해야 할 수 있습니다. 응용 프로그램은 거의 정적인 경우입니다. 그(것)들은 성장하고 시간이 지남에 따라 돌연변이하는 경향이 있습니다.

예를 들어 데이터 액세스 계층을 구현하는 방법을 변경하기로 결정한다고 가정해 보겠습니다. 현재 연락처 관리자 응용 프로그램은 Microsoft 엔터티 프레임워크를 사용하여 데이터베이스에 액세스합니다. 그러나 ADO.NET 데이터 서비스 또는 NHibernate와 같은 새 데이터 액세스 기술로 마이그레이션할 수도 있습니다. 그러나 데이터 액세스 코드는 유효성 검사 및 컨트롤러 코드에서 격리되지 않으므로 데이터 액세스와 직접 관련이 없는 다른 코드를 수정하지 않고는 응용 프로그램의 데이터 액세스 코드를 수정할 수 없습니다.

반면에 응용 프로그램이 느슨하게 결합되면 응용 프로그램의 다른 부분을 건드리지 않고 응용 프로그램의 한 부분을 변경할 수 있습니다. 예를 들어 유효성 검사 또는 컨트롤러 논리를 수정하지 않고 데이터 액세스 기술을 전환할 수 있습니다.

이 반복에서는 연락처 관리자 응용 프로그램을 보다 느슨하게 결합된 응용 프로그램으로 리팩터링할 수 있는 몇 가지 소프트웨어 디자인 패턴을 활용합니다. 작업이 완료되면 연락처 관리자는 이전에는 수행하지 않았던 작업을 수행하지 않습니다. 그러나 나중에 응용 프로그램을 더 쉽게 변경할 수 있습니다.

> [!NOTE] 
> 
> 리팩터링은 기존 기능을 잃지 않도록 응용 프로그램을 다시 작성하는 프로세스입니다.

## <a name="using-the-repository-software-design-pattern"></a>리포지토리 소프트웨어 설계 패턴 사용

첫 번째 변경 사항은 저장소 패턴이라는 소프트웨어 디자인 패턴을 활용하는 것입니다. 저장소 패턴을 사용하여 응용 프로그램의 나머지 부분에서 데이터 액세스 코드를 격리합니다.

저장소 패턴을 구현하려면 다음 두 단계를 완료해야 합니다.

1. 인터페이스 만들기
2. 인터페이스를 구현하는 구체적인 클래스 만들기

먼저 수행해야 하는 모든 데이터 액세스 방법을 설명하는 인터페이스를 만들어야 합니다. IContactManagerRepository 인터페이스는 목록 1에 포함되어 있습니다. 이 인터페이스는 CreateContact(), DeleteContact(), 편집연락처(), GetContact및 ListContacts()의 다섯 가지 방법을 설명합니다.

**목록 1 - 모델\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

다음으로 IContactManagerRepository 인터페이스를 구현하는 구체적인 클래스를 만들어야 합니다. Microsoft 엔터티 프레임워크를 사용하여 데이터베이스에 액세스하기 때문에 EntityContactManagerRepository라는 새 클래스를 만듭니다. 이 클래스는 목록 2에 포함되어 있습니다.

**목록 2 - 모델\엔터티연락처관리자Repository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

EntityContactManagerRepository 클래스는 IContactManagerRepository 인터페이스를 구현 합니다. 클래스는 해당 인터페이스에서 설명하는 다섯 가지 메서드를 모두 구현합니다.

당신은 우리가 인터페이스를 귀찮게해야하는 이유를 궁금해 할 수 있습니다. 인터페이스와 인터페이스를 구현하는 클래스를 모두 만들어야 하는 이유는 무엇입니까?

한 가지 예외를 제외하고, 응용 프로그램의 나머지 는 구체적인 클래스가 아닌 인터페이스와 상호 작용합니다. EntityContactManagerRepository 클래스에서 노출 된 메서드를 호출 하는 대신 IContactManagerRepository 인터페이스에 의해 노출 된 메서드를 호출 합니다.

이렇게 하면 응용 프로그램의 나머지 부분을 수정할 필요 없이 새 클래스로 인터페이스를 구현할 수 있습니다. 예를 들어, 미래의 날짜에 IContactManagerRepository 인터페이스를 구현 하는 DataServicesContactManagerRepository 클래스를 구현 할 수 있습니다. DataServicesContactManagerRepository 클래스는 ADO.NET 데이터 서비스를 사용하여 Microsoft 엔터티 프레임워크 대신 데이터베이스에 액세스할 수 있습니다.

응용 프로그램 코드가 IContactManagerRepository 인터페이스 대신 구체적인 EntityContactManagerRepository 클래스에 대해 프로그래밍된 경우 나머지 코드를 수정하지 않고 구체적인 클래스를 전환할 수 있습니다. 예를 들어 데이터 액세스 또는 유효성 검사 논리를 수정하지 않고 EntityContactManagerRepository 클래스에서 DataServicesContactManagerRepository 클래스로 전환할 수 있습니다.

구체적인 클래스 대신 인터페이스(추상화)에 대해 프로그래밍하면 응용 프로그램이 변경에 더 탄력적입니다.

> [!NOTE] 
> 
> 메뉴 옵션 리팩터링, 인터페이스 추출을 선택하여 Visual Studio 내의 구체적인 클래스에서 인터페이스를 빠르게 만들 수 있습니다. 예를 들어 EntityContactManagerRepository 클래스를 먼저 만든 다음 추출 인터페이스를 사용하여 IContactManager Repository 인터페이스를 자동으로 생성할 수 있습니다.

## <a name="using-the-dependency-injection-software-design-pattern"></a>종속성 사출 소프트웨어 설계 패턴 사용

데이터 액세스 코드를 별도의 저장소 클래스로 마이그레이션되었으므로 이 클래스를 사용하려면 연락처 컨트롤러를 수정해야 합니다. 컨트롤러에서 리포지토리 클래스를 사용 하 여 종속성 주입 이라는 소프트웨어 디자인 패턴을 활용 합니다.

수정된 연락처 컨트롤러는 목록 3에 포함되어 있습니다.

**목록 3 - 컨트롤러\연락처Controller.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

목록 3의 연락처 컨트롤러에는 두 개의 생성자가 있습니다. 첫 번째 생성자는 IContactManagerRepository 인터페이스의 구체적인 인스턴스를 두 번째 생성자에게 전달합니다. 연락처 컨트롤러 클래스는 *생성자 종속성 주입을*사용합니다.

EntityContactManagerRepository 클래스가 사용되는 유일한 장소는 첫 번째 생성자입니다. 나머지 클래스는 구체적인 EntityContactManagerRepository 클래스 대신 IContactManagerRepository 인터페이스를 사용합니다.

이렇게 하면 나중에 IContactManagerRepository 클래스의 구현을 쉽게 전환할 수 있습니다. EntityContactManagerRepository 클래스 대신 DataServicesContactRepository 클래스를 사용 하려는 경우 첫 번째 생성기를 수정 합니다.

생성자 종속성 주입또한 Contact controller 클래스를 매우 테스트 가능하게 만듭니다. 단위 테스트에서 IContactManagerRepository 클래스의 모의 구현을 통과 하 여 연락처 컨트롤러를 인스턴스화할 수 있습니다. 종속성 주입의 이 기능은 연락처 관리자 응용 프로그램에 대한 단위 테스트를 빌드할 때 다음 반복에서 매우 중요합니다.

> [!NOTE] 
> 
> IContactManagerRepository 인터페이스의 특정 구현에서 Contact 컨트롤러 클래스를 완전히 분리하려는 경우 StructureMap 또는 MEF(Microsoft 엔터티 프레임워크)와 같은 종속성 주입을 지원하는 프레임워크를 활용할 수 있습니다. 종속성 주입 프레임 워크를 활용 하 여 코드에서 구체적인 클래스를 참조 할 필요가 없습니다.

## <a name="creating-a-service-layer"></a>서비스 계층 만들기

리스팅 3의 수정된 컨트롤러 클래스에서 유효성 검사 논리가 여전히 컨트롤러 논리와 혼합되어 있음을 알았을 것입니다. 데이터 액세스 논리를 격리하는 것이 좋습니다.

이 문제를 해결 하려면 별도 [*서비스 계층을*](http://martinfowler.com/eaaCatalog/serviceLayer.html)만들 수 있습니다. 서비스 계층은 컨트롤러와 리포지토리 클래스 사이에 삽입할 수 있는 별도의 계층입니다. 서비스 계층에는 모든 유효성 검사 논리를 포함하는 비즈니스 논리가 포함되어 있습니다.

연락처 관리자 서비스는 목록 4에 포함되어 있습니다. 연락처 컨트롤러 클래스의 유효성 검사 논리가 포함되어 있습니다.

**목록 4 - 모델\컨택 관리자서비스.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

ContactManagerService의 생성자는 유효성 검사사전이 필요합니다. 서비스 계층은 이 유효성 검사사전을 통해 컨트롤러 계층과 통신합니다. 데코레이터 패턴에 대해 설명할 때 다음 섹션에서 유효성 검사사전에 대해 자세히 설명합니다.

또한 ContactManagerServiceIContactManagerService 인터페이스를 구현 합니다. 항상 구체적인 클래스 대신 인터페이스에 대해 프로그래밍하려고 노력해야 합니다. 연락처 관리자 응용 프로그램의 다른 클래스는 ContactManagerService 클래스와 직접 상호 작용하지 않습니다. 대신 한 가지 예외를 제외하고 나머지 연락처 관리자 응용 프로그램은 IContactManagerService 인터페이스에 대해 프로그래밍됩니다.

IContactManagerService 인터페이스는 목록 5에 포함되어 있습니다.

**목록 5 - 모델\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

수정된 연락처 컨트롤러 클래스는 목록 6에 포함되어 있습니다. 연락처 컨트롤러가 더 이상 ContactManager 리포지토리와 상호 작용하지 않습니다. 대신 연락처 컨트롤러는 연락처 관리자 서비스와 상호 작용합니다. 각 레이어는 다른 레이어에서 가능한 한 격리됩니다.

**목록 6 - 컨트롤러\연락처Controller.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

우리의 응용 프로그램은 더 이상 단일 책임 원칙 (SRP)의 파울을 실행하지 않습니다. 목록 6의 연락처 컨트롤러는 응용 프로그램 실행 흐름을 제어하는 것 이외의 모든 책임이 제거되었습니다. 모든 유효성 검사 논리가 Contact 컨트롤러에서 제거되고 서비스 계층으로 푸시되었습니다. 모든 데이터베이스 논리가 리포지토리 계층으로 푸시되었습니다.

## <a name="using-the-decorator-pattern"></a>데코레이터 패턴 사용

컨트롤러 계층에서 서비스 계층을 완전히 분리할 수 있기를 원합니다. 원칙적으로 MVC 응용 프로그램에 대한 참조를 추가할 필요 없이 컨트롤러 계층과 별도의 어셈블리로 서비스 계층을 컴파일할 수 있어야 합니다.

그러나 서비스 계층은 유효성 검사 오류 메시지를 컨트롤러 계층으로 다시 전달할 수 있어야 합니다. 서비스 계층이 컨트롤러와 서비스 계층을 결합하지 않고 유효성 검사 오류 메시지를 전달하도록 하려면 어떻게 해야 합니까? 우리는 [데코레이터](http://en.wikipedia.org/wiki/Decorator_pattern)패턴이라는 소프트웨어 디자인 패턴을 활용할 수 있습니다.

컨트롤러는 ModelStateDictionary라는 이름의 ModelState를 사용하여 유효성 검사 오류를 나타냅니다. 따라서 컨트롤러 계층에서 서비스 계층으로 ModelState를 전달하려는 유혹이 있을 수 있습니다. 그러나 서비스 계층에서 ModelState를 사용하면 서비스 계층이 ASP.NET MVC 프레임워크의 기능에 종속됩니다. 언젠가 는 ASP.NET MVC 응용 프로그램 대신 WPF 응용 프로그램과 함께 서비스 계층을 사용할 수 있기 때문에 이 문제는 좋지 않습니다. 이 경우 ModelStateDictionary 클래스를 사용 하 여 ASP.NET MVC 프레임 워크를 참조 하 고 싶지 않을 것입니다.

데코레이터 패턴을 사용하면 인터페이스를 구현하기 위해 기존 클래스를 새 클래스로 래핑할 수 있습니다. 연락처 관리자 프로젝트에는 목록 7에 포함된 ModelStateWrapper 클래스가 포함됩니다. ModelStateWrapper 클래스는 목록 8의 인터페이스를 구현합니다.

**목록 7 - 모델\유효성 검사\모델스테이트래퍼.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**목록 8 \ 모델\유효성 검사\IvalidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

목록 5를 자세히 살펴보면 ContactManager 서비스 계층에서 IValidationDictionary 인터페이스를 독점적으로 사용하는 것을 볼 수 있습니다. ContactManager 서비스는 ModelStateDictionary 클래스에 종속되지 않습니다. 연락처 컨트롤러가 ContactManager 서비스를 만들면 컨트롤러는 다음과 같이 ModelState를 래핑합니다.

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 새 기능을 추가 하지 않았습니다. 이 반복의 목표는 유지 관리 및 수정이 더 쉬워지도록 연락처 관리자 응용 프로그램을 리팩터링하는 것이었습니다.

먼저 저장소 소프트웨어 디자인 패턴을 구현했습니다. 모든 데이터 액세스 코드를 별도의 ContactManager 리포지토리 클래스로 마이그레이션했습니다.

또한 컨트롤러 논리에서 유효성 검사 논리를 격리했습니다. 유효성 검사 코드를 모두 포함하는 별도의 서비스 계층을 만들었습니다. 컨트롤러 계층은 서비스 계층과 상호 작용하고 서비스 계층은 리포지토리 계층과 상호 작용합니다.

서비스 계층을 만들 때 데코레이터 패턴을 활용하여 ModelState를 서비스 계층에서 격리했습니다. 서비스 계층에서는 ModelState 대신 IValidationDictionary 인터페이스에 대해 프로그래밍했습니다.

마지막으로 종속성 주입 패턴이라는 소프트웨어 디자인 패턴을 활용했습니다. 이 패턴을 사용하면 구체적인 클래스 대신 인터페이스(추상화)에 대해 프로그래밍할 수 있습니다. 종속성 주입 디자인 패턴을 구현하면 코드를 더 쉽게 테스트할 수 있습니다. 다음 반복에서는 프로젝트에 단위 테스트를 추가합니다.

> [!div class="step-by-step"]
> [이전](iteration-3-add-form-validation-cs.md)
> [다음](iteration-5-create-unit-tests-cs.md)
