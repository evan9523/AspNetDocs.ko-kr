---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 자동화된 단위 테스트 사용 | 마이크로 소프트 문서
author: rick-anderson
description: 12단계는 NerdDinner 기능을 검증하는 자동화된 단위 테스트 제품군을 개발하는 방법을 보여 주며, 이를 통해 변경에 대한 자신감을 심어줄 수 있습니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541470"
---
# <a name="enable-automated-unit-testing"></a>자동화된 유닛 테스트 사용

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 12단계입니다.
> 
> 12단계는 NerdDinner 기능을 검증하는 자동화된 단위 테스트 제품군을 개발하는 방법을 보여 주며, 향후 응용 프로그램을 변경하고 개선할 수 있는 자신감을 줄 것입니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-12-unit-testing"></a>얼간이 디너 단계 12: 단위 테스트

NerdDinner 기능을 확인하고 향후 응용 프로그램을 변경하고 개선할 수 있는 확신을 주는 자동화된 단위 테스트 제품군을 개발해 보겠습니다.

### <a name="why-unit-test"></a>왜 단위 테스트?

어느 아침 출근길에 작업 중인 응용 프로그램에 대한 갑작스런 영감이 깜박입니다. 응용 프로그램을 크게 개선할 수 있는 변경 프로그램이 있다는 것을 알게 됩니다. 코드를 정리하거나, 새 기능을 추가하거나, 버그를 수정하는 리팩터링일 수 있습니다.

당신이 당신의 컴퓨터에 도착 했을 때 직면 하는 질문은 – "얼마나 안전이 개선 을 만들기 위해?" 변경하면 부작용이 발생하거나 문제가 발생하면 어떻게 해야 합니까? 변경은 간단하고 구현하는 데 몇 분밖에 걸리지 않을 수 있지만 모든 응용 프로그램 시나리오를 수동으로 테스트하는 데 몇 시간이 걸리는 경우 어떻게 해야 합니까? 시나리오를 다루는 것을 잊어 버리고 깨진 응용 프로그램이 프로덕션에 들어간다면 어떻게 해야 합니까? 이 개선을 하는 것은 정말 모든 노력을 가치가 있다?

자동화된 단위 테스트는 응용 프로그램을 지속적으로 향상시키고 작업 중인 코드를 두려워하지 않도록 하는 안전망을 제공할 수 있습니다. 기능을 신속하게 검증하는 자동화된 테스트를 통해 자신 있게 코딩할 수 있으며, 그렇지 않으면 불편함을 느끼지 않았을 수 있는 개선 작업을 수행할 수 있습니다. 또한 유지 보수가 더 가능하고 수명이 긴 솔루션을 만드는 데 도움을 주어 투자 수익률이 훨씬 높아지도록 합니다.

ASP.NET MVC 프레임워크를 사용하면 응용 프로그램 기능을 쉽고 자연스럽게 단위 테스트할 수 있습니다. 또한 테스트 우선 기반 개발을 가능하게 하는 TDD(테스트 기반 개발) 워크플로를 지원합니다.

### <a name="nerddinnertests-project"></a>얼드디너.테스트 프로젝트

이 자습서의 시작 부분에서 NerdDinner 응용 프로그램을 만들 때 응용 프로그램 프로젝트와 함께 수행 할 단위 테스트 프로젝트를 만들지 여부를 묻는 대화 상자가 표시되었습니다.

![](enable-automated-unit-testing/_static/image1.png)

"예, 단위 테스트 프로젝트 만들기" 라디오 단추를 선택하여 "NerdDinner.Test" 프로젝트가 솔루션에 추가되었습니다.

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Test 프로젝트는 NerdDinner 응용 프로그램 프로젝트 어셈블리를 참조하며 응용 프로그램 기능을 확인하는 자동화된 테스트를 쉽게 추가할 수 있습니다.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>저녁 식사 모델 클래스에 대한 단위 테스트 만들기

NerdDinner.Test 프로젝트에 몇 가지 테스트를 추가하여 모델 레이어를 빌드할 때 만든 Dinner 클래스를 확인합니다.

먼저 "모델"이라는 테스트 프로젝트 내에 새 폴더를 만들어 모델 관련 테스트를 배치합니다. 그런 다음 폴더를 마우스 오른쪽 단추로 클릭하고 **&gt;새 테스트 추가** 메뉴 명령을 선택합니다. 그러면 "새 테스트 추가" 대화 상자가 나타납니다.

"단위 테스트"를 만들고 "DinnerTest.cs"라는 이름을 지정합니다.

![](enable-automated-unit-testing/_static/image3.png)

"확인" 버튼을 클릭하면 Visual Studio가 프로젝트에 DinnerTest.cs 파일을 추가(및 열림)합니다.

![](enable-automated-unit-testing/_static/image4.png)

기본 Visual Studio 단위 테스트 템플릿에는 약간 지저분한 것을 발견하는 보일러 플레이트 코드가 많이 있습니다. 아래 코드를 포함하도록 정리해 보겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

위의 DinnerTest 클래스의 [TestClass] 특성은 테스트뿐만 아니라 선택적 테스트 초기화 및 분해 코드를 포함하는 클래스로 식별합니다. [TestMethod] 특성이 있는 공용 메서드를 추가하여 테스트를 정의할 수 있습니다.

다음은 Dinner 클래스를 연습하는 두 가지 테스트 중 첫 번째 테스트입니다. 첫 번째 테스트는 모든 속성이 올바르게 설정되지 않고 새 Dinner가 만들어지면 Dinner가 유효하지 않은지 확인합니다. 두 번째 테스트는 Dinner에 유효한 값으로 설정된 모든 속성이 있는 경우 Dinner가 유효한지 확인합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

위에서 테스트 이름은 매우 명시적이고 다소 상세하다는 것을 알 수 있습니다. 수백 또는 수천 개의 작은 테스트를 만들 수 있기 때문에 이 작업을 수행하고 있으며, 특히 테스트 러너의 실패 목록을 살펴볼 때 각 테스트의 의도와 동작을 쉽게 확인할 수 있기를 원합니다. 테스트 이름은 테스트 중인 기능의 이름을 따서 명명해야 합니다. 위에서는\_\_"동사 명사" 이름 패턴을 사용하고 있습니다.

"정렬, 행위, 어설션"을 의미하는 "AAA" 테스트 패턴을 사용하여 테스트를 구조화하고 있습니다.

- 정렬: 테스트 중인 장치 설정
- 행동: 시험 중인 유닛을 연습하고 결과를 캡처합니다.
- 어설션: 동작 확인

테스트를 작성할 때 개별 테스트가 너무 많은 작업을 수행하는 것을 피하려고 합니다. 대신 각 테스트는 단일 개념만 확인해야 합니다(오류의 원인을 훨씬 쉽게 찾아낼 수 있음). 좋은 지침은 각 테스트에 대해 하나의 어설션 문만 시도하는 것입니다. 테스트 메서드에 둘 이상의 어설션 문이 있는 경우 모두 동일한 개념을 테스트하는 데 사용되는지 확인합니다. 의심스러울 때는 또 다른 시험을 하십시오.

### <a name="running-tests"></a>테스트 실행 중

Visual Studio 2008 Professional(및 상위 버전)에는 IDE 내에서 Visual Studio 단위 테스트 프로젝트를 실행하는 데 사용할 수 있는 기본 제공 테스트 러너가 포함되어 있습니다. 솔루션 메뉴 의 **&gt;&gt;모든 테스트** 실행(또는 Ctrl R, A 형)을 선택하여 모든 단위 테스트를 실행할 수 있습니다. 또는 특정 테스트 클래스 또는 테스트 메서드 내에 커서를 배치하고 현재 컨텍스트 메뉴 **명령에서 테스트&gt;실행 테스트를&gt;** 사용하거나 Ctrl R, T 를 입력하여 단위 테스트의 하위 집합을 실행할 수 있습니다.

DinnerTest 클래스 내에 커서를 배치하고 "Ctrl R, T"를 입력하여 방금 정의한 두 테스트를 실행해 보겠습니다. 이렇게 하면 Visual Studio 내에 "테스트 결과" 창이 표시되고 테스트 실행 결과가 표시됩니다.

![](enable-automated-unit-testing/_static/image5.png)

*참고: VS 테스트 결과 창에는 기본적으로 클래스 이름 열이 표시되지 않습니다. 테스트 결과 창 에서 마우스 오른쪽 단추를 클릭 하고 열 추가/제거 메뉴 명령을 사용 하 여이 추가할 수 있습니다.*

두 테스트는 실행하는 데 1초밖에 걸리지 않았으며 두 테스트가 모두 통과한 것을 볼 수 있습니다. 이제 특정 규칙 유효성 검사를 확인하는 추가 테스트를 만들어 추가 테스트를 만들고 Dinner 클래스에 추가한 IsUserHost() 및 IsUserRegistered()라는 두 가지 도우미 메서드를 포함할 수 있습니다. Dinner 클래스에 대해 이러한 모든 테스트를 준비하면 나중에 새 비즈니스 규칙 및 유효성 검사를 추가하는 것이 훨씬 쉽고 안전해집니다. Dinner에 새 규칙 논리를 추가한 다음 몇 초 내에 이전 논리 기능이 손상되지 않았는지 확인할 수 있습니다.

설명이 있는 테스트 이름을 사용하면 각 테스트가 확인하는 내용을 쉽게 쉽게 이해할 수 있습니다. **도구-&gt;옵션** 메뉴 명령을 사용하고, 테스트 도구-&gt;테스트 실행 구성 화면을 열고, "실패하거나 결정적이지 않은 단위 테스트 결과를 두 번 클릭하면 테스트실패 지점이 표시됩니다" 확인란을 확인하는 것이 좋습니다. 이렇게 하면 테스트 결과 창에서 오류를 두 번 클릭하고 즉시 어설션 실패로 이동할 수 있습니다.

### <a name="creating-dinnerscontroller-unit-tests"></a>Dinners컨트롤러 단위 테스트 만들기

이제 DinnersController 기능을 확인하는 몇 가지 단위 테스트를 만들어 보겠습니다. 먼저 테스트 프로젝트 내의 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭한 다음 **&gt;새 테스트 추가** 메뉴 명령을 선택합니다. "단위 테스트"를 만들고 "DinnersControllerTest.cs"라는 이름을 지정합니다.

DinnersController에서 Details() 작업 메서드를 확인하는 두 가지 테스트 메서드를 만듭니다. 첫 번째 는 기존 Dinner가 요청될 때 보기가 반환되는지 확인합니다. 두 번째 는 존재하지 않는 Dinner가 요청될 때 "NotFound" 보기가 반환되는지 확인합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

위의 코드는 정리를 컴파일합니다. 그러나 테스트를 실행하면 둘 다 실패합니다.

![](enable-automated-unit-testing/_static/image6.png)

오류 메시지를 보면 TestsRepository 클래스가 데이터베이스에 연결할 수 없었기 때문에 테스트가 실패한 이유를 알 수 있습니다. NerdDinner 응용 프로그램은 NerdDinner 응용 프로그램 프로젝트의 \App\_데이터 디렉토리아래에 있는 로컬 SQL Server Express 파일에 연결 문자열을 사용하고 있습니다. NerdDinner.Test 프로젝트는 응용 프로그램 프로젝트다음 다른 디렉토리에서 컴파일및 실행되므로 연결 문자열의 상대 경로 위치가 올바르지 않습니다.

SQL Express 데이터베이스 파일을 테스트 프로젝트에 복사하여 이 문제를 해결한 다음 테스트 프로젝트의 App.config에서 적절한 테스트 연결 문자열을 추가할 *수* 있습니다. 이렇게 하면 위의 테스트가 차단 해제되고 실행됩니다.

그러나 실제 데이터베이스를 사용하는 단위 테스트 코드에는 여러 가지 문제가 있습니다. 특히 다음에 대한 내용을 설명합니다.

- 단위 테스트의 실행 시간이 크게 느려집니다. 테스트를 실행하는 데 시간이 오래 걸릴수록 테스트를 자주 실행할 가능성이 줄어듭니다. 단위 테스트를 몇 초 만에 실행하고 프로젝트를 컴파일하는 것처럼 자연스럽게 수행할 수 있도록 하는 것이 가장 좋습니다.
- 테스트 내에서 설정 및 정리 논리가 복잡해짐을 유발합니다. 각 단위 테스트를 격리하고 다른 테스트와 독립적으로 지정하려고 합니다(부작용이나 종속성 없음). 실제 데이터베이스에 대해 작업할 때는 상태를 염두에 두고 테스트 간에 다시 설정해야 합니다.

이러한 문제를 해결하고 테스트에서 실제 데이터베이스를 사용할 필요가 없도록 하는 "종속성 주입"이라는 디자인 패턴을 살펴보겠습니다.

### <a name="dependency-injection"></a>종속성 주입

지금 저녁 식사 컨트롤러는 단단히 "결합"저녁 식사Repository 클래스입니다. "커플링"은 클래스가 작업하기 위해 다른 클래스에 명시적으로 의존하는 상황을 나타냅니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository 클래스는 데이터베이스에 대 한 액세스를 필요로 하기 때문에 DinnersController 클래스DinnerRepository에 단단히 결합 된 종속성 DinnersController 작업 메서드를 테스트 하기 위해 데이터베이스를 필요 결국.

"종속성 주입"이라는 디자인 패턴을 사용하여 이 방법을 해결할 수 있습니다. 대신 종속성을 생성자 인수를 사용하여 사용하는 클래스에 명시적으로 전달할 수 있습니다. 인터페이스를 사용하여 종속성을 정의하는 경우 단위 테스트 시나리오에 대해 "가짜" 종속성 구현을 유연하게 전달할 수 있습니다. 이를 통해 실제로 데이터베이스에 액세스할 필요가 없는 테스트 별 종속성 구현을 만들 수 있습니다.

이 작업을 확인 하려면 DinnersController를 사용하여 종속성 주입을 구현해 보겠습니다.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository 인터페이스 추출

첫 번째 단계는 컨트롤러가 Dinners를 검색하고 업데이트하는 데 필요한 리포지토리 계약을 캡슐화하는 새로운 IDinnerRepository 인터페이스를 만드는 것입니다.

\Models 폴더를 마우스 오른쪽 단추로 클릭한 다음 **&gt;새 항목 추가** 메뉴 명령을 선택하고 IDinnerRepository.cs라는 새 인터페이스를 만들어 수동으로 인터페이스 계약을 정의할 수 있습니다.

또는 Visual Studio Professional(및 상위 버전)에 내장된 리팩터링 도구를 사용하여 기존 DinnerRepository 클래스에서 자동으로 인터페이스를 추출하고 만들 수 있습니다. VS를 사용하여 이 인터페이스를 추출하려면 DinnerRepository 클래스의 텍스트 편집기에서 커서를 배치한 다음 마우스 오른쪽 단추를 클릭하고 **리팩터링-&gt;인터페이스 추출** 메뉴 명령을 선택합니다.

![](enable-automated-unit-testing/_static/image7.png)

이렇게 하면 "인터페이스 추출" 대화 상자가 시작되고 만들 인터페이스 이름을 묻는 메시지가 표시됩니다. 기본적으로 IDinnerRepository로 설정되며 인터페이스에 추가할 기존 DinnerRepository 클래스의 모든 공용 메서드를 자동으로 선택합니다.

![](enable-automated-unit-testing/_static/image8.png)

"확인" 버튼을 클릭하면 Visual Studio에서 응용 프로그램에 새로운 IDinnerRepository 인터페이스를 추가합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

그리고 우리의 기존 DinnerRepository 클래스는 인터페이스를 구현 할 수 있도록 업데이트됩니다 :

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>생성자 주입을 지원하기 위한 DinnersController 업데이트

이제 DinnersController 클래스를 업데이트하여 새 인터페이스를 사용합니다.

현재 DinnersController는 "dinnerRepository"필드가 항상 DinnerRepository 클래스가 되도록 하드 코딩되어 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

"dinnerrepository" 필드가 DinnerRepository 대신 IDinnerRepository 유형이 되도록 변경하겠습니다. 그런 다음 두 개의 공용 DinnersController 생성자 추가합니다. 생성자 중 하나를 사용하면 IDinnerRepository를 인수로 전달할 수 있습니다. 다른 하나는 기존 DinnerRepository 구현을 사용하는 기본 생성자입니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

기본적으로 ASP.NET MVC는 기본 생성기를 사용하여 컨트롤러 클래스를 생성하므로 런타임시 DinnersController는 DinnerRepository 클래스를 계속 사용하여 데이터 액세스를 수행합니다.

하지만 이제 단위 테스트를 업데이트하여 매개 변수 생성기를 사용하여 "가짜" dinner 리포지토리 구현을 전달할 수 있습니다. 이 "가짜" dinner 리포지토리는 실제 데이터베이스에 액세스할 필요가 없으며 대신 메모리 내 샘플 데이터를 사용합니다.

#### <a name="creating-the-fakedinnerrepository-class"></a>가짜 Dinner리 리포지토리 클래스 만들기

가짜 DinnerRepository 클래스를 만들어 봅시다.

먼저 NerdDinner.Test 프로젝트 내에서 "가짜" 디렉토리를 만든 다음 새 FakeDinnerRepository 클래스를 추가합니다(폴더를 마우스 오른쪽 버튼으로 클릭하고 **&gt;새 클래스 추가**선택).

![](enable-automated-unit-testing/_static/image9.png)

FakeDinnerRepository 클래스가 IDinnerRepository 인터페이스를 구현할 수 있도록 코드를 업데이트합니다. 그런 다음 마우스 오른쪽 단추로 클릭하고 "인터페이스 IDinnerRepository 구현" 컨텍스트 메뉴 명령을 선택할 수 있습니다.

![](enable-automated-unit-testing/_static/image10.png)

이렇게 하면 Visual Studio에서 모든 IDinnerRepository 인터페이스 멤버를 기본 "스텁 아웃" 구현으로 FakeDinnerRepository 클래스에 자동으로 추가합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

그런 다음 FakeDinnerRepository 구현을 업데이트하여 생성자 인수로&gt; 전달된 메모리 목록 Dinner&lt;컬렉션에서 작동합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

이제 데이터베이스가 필요하지 않고 대신 Dinner 개체의 메모리 내 목록을 작업할 수 있는 가짜 IDinnerRepository 구현이 있습니다.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>단위 테스트와 가짜 Dinnerrerepository 사용

데이터베이스를 사용할 수 없기 때문에 이전에 실패한 DinnersController 단위 테스트로 돌아가보겠습니다. 우리는 아래의 코드를 사용하여 DinnersController에 샘플 인 메모리 Dinner 데이터로 채워진 FakeDinnerRepository를 사용하도록 테스트 방법을 업데이트 할 수 있습니다 .

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

이제 이러한 테스트를 실행하면 둘 다 통과합니다.

![](enable-automated-unit-testing/_static/image11.png)

무엇보다도 실행하는 데 1초밖에 걸리지 않으며 복잡한 설정/정리 논리가 필요하지 않습니다. 이제 실제 데이터베이스에 연결할 필요 없이 모든 DinnersController 작업 메서드 코드(목록, 페이징, 세부 정보, 만들기, 업데이트 및 삭제 포함)를 단위 테스트할 수 있습니다.

| **측면 주제: 종속성 주입 프레임워크** |
| --- |
| 위의 경우와 같이 수동 종속성 주입을 수행하는 것은 잘 작동하지만 응용 프로그램의 종속성 및 구성 요소 수가 증가함에 따라 유지 관리하기가 더 어려워집니다. .NET에 대한 여러 종속성 주입 프레임워크가 존재하여 더 많은 종속성 관리 유연성을 제공할 수 있습니다. "Control의 반전"(IoC) 컨테이너라고도 하는 이러한 프레임워크는 런타임시 개체에 종속성을 지정하고 전달하기 위한 추가 수준의 구성 지원을 가능하게 하는 메커니즘을 제공합니다(대부분 생성자 주입사용). .NET에서 더 인기 있는 OSS 종속성 주입/IOC 프레임 워크 중 일부는 다음과 같습니다: AutoFac, Ninject, Spring.NET, StructureMap 및 윈저. ASP.NET MVC는 개발자가 컨트롤러의 해상도 및 인스턴스화에 참여할 수 있도록 하는 확장성 API를 노출하고 이 프로세스 내에서 종속성 주입/IoC 프레임워크를 깔끔하게 통합할 수 있습니다. DI/IOC 프레임워크를 사용하면 DinnersController에서 기본 생성기를 제거할 수 있으며, 이 생성자는 DinnersController와 DinnerRepository 간의 커플링을 완전히 제거할 수 있습니다. NerdDinner 응용 프로그램을 사용하여 종속성 주입 / IOC 프레임 워크를 사용하지 않습니다. 그러나 NerdDinner 코드 베이스 와 기능이 성장하면 미래를 고려할 수 있습니다. |

### <a name="creating-edit-action-unit-tests"></a>작업 단위 테스트 편집 만들기

이제 DinnersController의 편집 기능을 확인하는 몇 가지 단위 테스트를 만들어 보겠습니다. 먼저 편집 작업의 HTTP-GET 버전을 테스트합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

유효한 Dinners가 요청될 때 DinnerFormViewModel 개체가 백업되는 뷰가 다시 렌더링되는지 확인하는 테스트를 만듭니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

그러나 테스트를 실행하면 편집 메서드가 User.Identity.Name 속성에 액세스하여 Dinner.IsHostedBy() 검사를 수행할 때 null 참조 예외가 throw되기 때문에 실패합니다.

Controller 기본 클래스의 사용자 개체는 로그인한 사용자에 대한 세부 정보를 캡슐화하며 런타임에 컨트롤러를 만들 때 ASP.NET MVC에 의해 채워집니다. 웹 서버 환경 외부에서 DinnersController를 테스트하기 때문에 사용자 개체가 설정되지 않습니다(따라서 null 참조 예외).

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Name 속성 조롱

모의 프레임워크를 사용하면 테스트를 지원하는 종속 개체의 가짜 버전을 동적으로 만들 수 있으므로 테스트를 더 쉽게 만들 수 있습니다. 예를 들어 편집 작업 테스트에서 모의 프레임워크를 사용하여 DinnersController에서 시뮬레이션된 사용자 이름을 조회하는 데 사용할 수 있는 사용자 개체를 동적으로 만들 수 있습니다. 이렇게하면 테스트를 실행할 때 null 참조가 throw되지 않습니다.

ASP.NET MVC와 함께 사용할 수있는 많은 .NET 모의 프레임 워크가 있습니다 [http://www.mockframeworks.com/](http://www.mockframeworks.com/)(여기에서 목록을 볼 수 있습니다). NerdDinner 응용 프로그램을 테스트하기 위해 [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)에서 무료로 다운로드 할 수있는 "Moq"라는 오픈 소스 모킹 프레임 워크를 사용합니다.

다운로드가 완료되면 NerdDinner.Test 프로젝트에 Moq.dll 어셈블리에 참조를 추가하겠습니다.

![](enable-automated-unit-testing/_static/image12.png)

그런 다음 사용자 이름을 매개 변수로 사용하는 테스트 클래스에 "CreateDinnersControllerAs(사용자 이름)" 도우미 메서드를 추가한 다음 DinnersController 인스턴스에서 User.Identity.Name 속성을 "모의"합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

위에서 Moq를 사용하여 ControllerContext 개체를 위조하는 모의 개체를 만듭니다(mVC가 컨트롤러 클래스에 전달하여 사용자, 요청, 응답 및 세션과 같은 런타임 개체를 노출하는 ASP.NET). 컨트롤러Context의 HttpContext.User.Identity.Name 속성이 도우미 메서드에 전달된 사용자 이름 문자열을 반환해야 함을 나타내기 위해 모의 "SetupGet" 메서드를 호출합니다.

우리는 ControllerContext 속성 및 메서드의 수를 모의 수 있습니다. 이를 설명하기 위해 RequestupGet() 호출을 Request.Is인증 속성(아래 테스트에는 실제로 필요하지 않지만 요청 속성을 모을 수 있는 방법을 설명하는 데 도움이 되는)을 추가했습니다. 작업이 완료되면 DinnersController에 Controller컨텍스트 모의 인스턴스를 할당합니다.

이제 이 도우미 메서드를 사용하여 다른 사용자가 포함된 편집 시나리오를 테스트하는 단위 테스트를 작성할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

그리고 지금 우리가 테스트를 실행할 때 그들은 통과 :

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>업데이트모델() 시나리오 테스트

HTTP-GET 버전의 편집 작업을 다루는 테스트를 만들었습니다. 이제 편집 작업의 HTTP-POST 버전을 확인하는 몇 가지 테스트를 만들어 보겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

이 작업 메서드를 지원 하기 위해 우리가 대 한 흥미로운 새로운 테스트 시나리오는 Controller 기본 클래스에 UpdateModel() 도우미 메서드의 사용. 이 도우미 메서드를 사용 하 여 양식 게시물 값을 Dinner 개체 인스턴스에 바인딩합니다.

다음은 UpdateModel() 도우미 메서드에 대해 게시된 양식을 제공하는 방법을 보여 주는 두 가지 테스트입니다. FormCollection 개체를 만들고 채우면 컨트롤러의 "ValueProvider" 속성에 할당합니다.

첫 번째 테스트는 성공적으로 저장하면 브라우저가 세부 정보 작업으로 리디렉션되는지 확인합니다. 두 번째 테스트는 잘못된 입력이 게시될 때 작업이 오류 메시지와 함께 편집 보기를 다시 표시한다는 것을 확인합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>랩업 테스트

단위 테스트 컨트롤러 클래스와 관련된 핵심 개념을 다루었습니다. 이러한 기술을 사용하여 응용 프로그램의 동작을 확인하는 수백 개의 간단한 테스트를 쉽게 만들 수 있습니다.

컨트롤러 및 모델 테스트에는 실제 데이터베이스가 필요하지 않으므로 매우 빠르고 실행하기 쉽습니다. 수백 개의 자동화된 테스트를 몇 초 만에 실행할 수 있으며 변경한 변경이 어떤 것을 깨뜨렸는지 에 대한 피드백을 즉시 받을 수 있습니다. 이렇게 하면 응용 프로그램을 지속적으로 개선, 리팩터링 및 구체화할 수 있는 자신감을 제공할 수 있습니다.

이 장의 마지막 주제로 테스트를 다루었지만, 테스트는 개발 프로세스가 끝날 때 수행해야 할 일이 기 때문에 다루지 않았습니다! 반대로 개발 프로세스에서 가능한 한 빨리 자동화된 테스트를 작성해야 합니다. 이렇게 하면 개발할 때 즉각적인 피드백을 얻을 수 있고, 응용 프로그램의 사용 사례 시나리오에 대해 신중하게 생각할 수 있으며, 깔끔한 계층화 및 커플링을 염두에 두고 응용 프로그램을 디자인하도록 안내할 수 있습니다.

이 책의 다음 장에서는 테스트 기반 개발(TDD)과 ASP.NET MVC에서 사용하는 방법에 대해 설명합니다. TDD는 결과 코드가 만족할 테스트를 먼저 작성하는 반복적인 코딩 방법입니다. TDD를 사용하면 구현하려는 기능을 확인하는 테스트를 만들어 각 기능을 시작합니다. 단위 테스트를 먼저 작성하면 기능과 작동 방식을 명확하게 이해할 수 있습니다. 테스트가 작성된 후에만(실패한다는 것을 확인한 후에) 테스트가 확인한 실제 기능을 구현합니다. 이미 기능이 작동하는 방식의 사용 사례에 대해 생각하는 데 시간을 보냈기 때문에 요구 사항과 이를 구현하는 가장 좋은 방법을 더 잘 이해할 수 있습니다. 구현이 완료되면 테스트를 다시 실행하고 기능이 올바르게 작동하는지 에 대한 즉각적인 피드백을 받을 수 있습니다. 10장에서TDD를 더 자세히 다룹니다.

### <a name="next-step"></a>다음 단계

일부 최종 마무리 코멘트.

> [!div class="step-by-step"]
> [이전](use-ajax-to-implement-mapping-scenarios.md)
> [다음](nerddinner-wrap-up.md)
