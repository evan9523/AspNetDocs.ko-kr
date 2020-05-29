---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF 마이그레이션 사용 및 Azure에 배포'
author: tdykstra
description: 이 자습서에서는 Code First 마이그레이션을 사용 하도록 설정 하 고 응용 프로그램을 Azure의 클라우드에 배포 합니다.
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 21a3efa865e5b5498dfb0f2adec199800fc70c58
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172975"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>자습서: ASP.NET MVC 앱에서 EF 마이그레이션 사용 및 Azure에 배포

지금까지 Contoso 대학 샘플 웹 응용 프로그램은 개발 컴퓨터의 IIS Express에서 로컬로 실행 되었습니다. 다른 사용자가 인터넷을 통해 사용할 수 있는 실제 응용 프로그램을 만들려면 웹 호스팅 공급자에 배포 해야 합니다. 이 자습서에서는 Code First 마이그레이션을 사용 하도록 설정 하 고 응용 프로그램을 Azure의 클라우드에 배포 합니다.

- Code First 마이그레이션를 사용 하도록 설정 합니다. 마이그레이션 기능을 사용 하면 데이터베이스를 삭제 하 고 다시 만들지 않고도 데이터베이스 스키마를 업데이트 하 여 데이터 모델을 변경 하 고 변경 내용을 프로덕션에 배포할 수 있습니다.
- Azure에 배포 합니다. 이 단계는 선택 사항입니다. 프로젝트를 배포 하지 않고 나머지 자습서를 계속 진행할 수 있습니다.

배포를 위해 원본 제어와 함께 연속 통합 프로세스를 사용 하는 것이 좋지만,이 자습서에서는 이러한 항목에 대해 다루지 않습니다. 자세한 내용은 [Azure를 사용 하 여 실제 클라우드 앱 빌드](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)에 대 한 [소스 제어](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) 및 [연속 통합](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) 챕터를 참조 하세요.

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * Code First 마이그레이션 사용
> * Azure에서 앱 배포 (선택 사항)

## <a name="prerequisites"></a>필수 구성 요소

- [연결 복원력 및 명령 인터셉션](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>Code First 마이그레이션 사용

새 애플리케이션을 개발하는 경우 데이터 모델은 자주 변경되며 모델이 변경될 때마다 데이터베이스와 동기화를 가져옵니다. 데이터 모델을 변경할 때마다 데이터베이스를 자동으로 삭제 하 고 다시 만들기 위해 Entity Framework를 구성 했습니다. 엔터티 클래스를 추가, 제거 또는 변경 하거나 클래스를 변경 하 `DbContext` 는 경우 다음에 응용 프로그램을 실행할 때 기존 데이터베이스가 자동으로 삭제 되 고, 모델과 일치 하는 새 데이터베이스가 만들어지고, 테스트 데이터로 시드 됩니다.

데이터베이스를 데이터 모델과 동기화된 상태로 유지하는 이 메서드는 애플리케이션을 프로덕션 환경에 배포할 때까지 잘 작동합니다. 응용 프로그램이 프로덕션 환경에서 실행 되는 경우 일반적으로 보관할 데이터를 저장 하 고, 새 열을 추가 하는 등의 변경 작업을 수행할 때마다 모든 항목을 손실 하지 않으려고 합니다. [Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 기능은 Code First를 사용 하 여 데이터베이스를 삭제 하 고 다시 만드는 대신 데이터베이스 스키마를 업데이트할 수 있도록 하 여이 문제를 해결 합니다. 이 자습서에서는 응용 프로그램을 배포 하 고 마이그레이션을 사용 하도록 준비 합니다.

1. 이전에 설정한 이니셜라이저를 사용 하지 않도록 설정 하 여 `contexts` 응용 프로그램 web.config 파일에 추가한 요소를 주석으로 처리 하거나 삭제 합니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 또한 응용 프로그램 *web.config* 파일에서 연결 문자열에 있는 데이터베이스의 이름을 ContosoUniversity2로 변경 합니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    이 변경 내용은 첫 번째 마이그레이션이 새 데이터베이스를 만들 때 프로젝트를 설정 합니다. 이는 필수는 아니지만 나중에 좋은 생각이 표시 될 것입니다.
3. **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

1. 프롬프트에 `PM>` 다음 명령을 입력 합니다.

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    `enable-migrations`이 명령은 ContosoUniversity 프로젝트에 *마이그레이션* 폴더를 만들고 해당 폴더에 *Configuration.cs* 파일을 저장 합니다 .이 파일을 편집 하 여 마이그레이션을 구성할 수 있습니다.

    데이터베이스 이름을 변경 하도록 지시 하는 위의 단계를 놓친 경우 마이그레이션은 기존 데이터베이스를 찾고 자동으로 `add-migration` 명령을 실행 합니다. 이는 데이터베이스를 배포 하기 전에 마이그레이션 코드 테스트를 실행 하지 않는다는 것을 의미 합니다. 나중에 명령을 실행할 때 `update-database` 데이터베이스가 이미 있기 때문에 아무 작업도 수행 되지 않습니다.

    *ContosoUniversity\Migrations\Configuration.cs* 파일을 엽니다. 앞서 살펴본 이니셜라이저 클래스와 마찬가지로 `Configuration` 클래스에는 메서드가 포함 되어 있습니다 `Seed` .

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    [초기값](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 방법의 목적은 Code First 데이터베이스를 만들거나 업데이트 한 후 테스트 데이터를 삽입 하거나 업데이트할 수 있도록 하는 것입니다. 메서드는 데이터베이스를 만들 때와 데이터 모델이 변경 된 후 데이터베이스 스키마가 업데이트 될 때마다 호출 됩니다.

### <a name="set-up-the-seed-method"></a>초기값 설정

모든 데이터 모델이 변경 될 때마다 데이터베이스를 삭제 하 고 다시 만들 때 이니셜라이저 클래스의 메서드를 사용 하 여 `Seed` 테스트 데이터를 삽입 합니다 .이 경우 모든 모델 변경 후 데이터베이스를 삭제 하 고 모든 테스트 데이터가 손실 되기 때문입니다. Code First 마이그레이션를 사용 하면 데이터베이스 변경 후에 테스트 데이터가 유지 되므로 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드에 테스트 데이터를 포함 하는 것은 일반적으로 필요 하지 않습니다. 실제로 `Seed` 는 `Seed` 메서드가 프로덕션 환경에서 실행 되기 때문에 마이그레이션을 사용 하 여 데이터베이스를 프로덕션 환경에 배포 하는 경우 테스트 데이터를 삽입 하는 것을 원하지 않습니다. 이 경우 `Seed` 프로덕션 환경에 필요한 데이터만 데이터베이스에 삽입 하려고 합니다. 예를 들어 `Department` 응용 프로그램을 프로덕션 환경에서 사용할 수 있게 되 면 데이터베이스에 테이블의 실제 부서 이름이 포함 되도록 할 수 있습니다.

이 자습서에서는 배포에 대해 마이그레이션을 사용 하지만 `Seed` 많은 데이터를 수동으로 삽입 하지 않고도 응용 프로그램 기능이 작동 하는 방식을 쉽게 확인할 수 있도록 메서드가 테스트 데이터를 삽입 합니다.

1. *Configuration.cs* 파일의 내용을 새 데이터베이스에 테스트 데이터를 로드 하는 다음 코드로 바꿉니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [초기값](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 데이터베이스 컨텍스트 개체를 입력 매개 변수로 사용 하 고 메서드의 코드는 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대해 코드는 새 엔터티 컬렉션을 만들고 적절 한 [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성에 추가한 다음 변경 내용을 데이터베이스에 저장 합니다. 여기에서 수행 하는 것 처럼 각 엔터티 그룹 다음에 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 호출할 필요는 없지만, 이렇게 하면 코드에서 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 원인을 찾을 수 있습니다.

    데이터를 삽입 하는 문 중 일부는 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드를 사용 하 여 "upsert" 작업을 수행 합니다. `Seed`명령을 실행할 때마다 메서드가 실행 되기 때문에 `update-database` 일반적으로 각 마이그레이션 후에는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 추가 하려는 행이 이미 있기 때문에 데이터를 삽입 하기만 하면 됩니다. "Upsert" 작업은 이미 있는 행을 삽입 하려고 할 때 발생 하는 오류를 방지 하지만 응용 프로그램을 테스트 하는 동안 수행 된 데이터의 변경 내용을 ***재정의*** 합니다. 일부 테이블에서 테스트 데이터를 사용 하는 경우 이러한 상황이 발생 하지 않을 수 있습니다. 테스트 하는 동안 데이터를 변경 하는 경우 데이터베이스 업데이트 후에 변경 내용을 유지 하려는 경우도 있습니다. 조건부 삽입 작업을 수행 하려는 경우: 행이 아직 없는 경우에만 행을 삽입 합니다. 초기값 메서드는 두 가지 방법을 모두 사용 합니다.

    [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드에 전달 된 첫 번째 매개 변수는 행이 이미 있는지 여부를 확인 하는 데 사용할 속성을 지정 합니다. 제공 하는 테스트 학생 데이터의 경우 `LastName` 목록의 각 성이 고유 하므로 속성을이 용도로 사용할 수 있습니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    이 코드에서는 성이 고유한 것으로 가정 합니다. 중복 성이 있는 학생을 수동으로 추가 하는 경우 다음에 마이그레이션을 수행할 때 다음과 같은 예외가 발생 합니다.

    **시퀀스에 둘 이상의 요소가 포함 되어 있습니다.**

    "Alexander Carson" 이라는 두 학생 같은 중복 데이터를 처리 하는 방법에 대 한 자세한 내용은 Rick Anderson의 블로그에서 [EF (시드 및 디버깅 Entity Framework) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 를 참조 하세요. 메서드에 대 한 자세한 내용은 `AddOrUpdate` Julie Lerman의 블로그에서 [EF 4.3 AddOrUpdate 메서드를 사용](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) 하는 방법을 참조 하세요.

    엔터티를 만드는 코드는 컬렉션을 `Enrollment` `ID` `students` 만드는 코드에서 해당 속성을 설정 하지 않았지만 컬렉션의 엔터티에 값이 있다고 가정 합니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    `ID` `ID` 컬렉션에 대해를 호출할 때 값이 설정 되므로 여기에서 속성을 사용할 수 있습니다 `SaveChanges` `students` . EF는 데이터베이스에 엔터티를 삽입할 때 기본 키 값을 자동으로 가져오고, `ID` 메모리에서 엔터티의 속성을 업데이트 합니다.

    엔터티 집합에 각 엔터티를 추가 하는 코드는 `Enrollment` `Enrollments` 메서드를 사용 하지 않습니다 `AddOrUpdate` . 엔터티가 이미 있는지 확인 하 고 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 방법은 응용 프로그램 UI를 사용 하 여 등록 등급에 대 한 변경 내용을 유지 합니다. 이 코드는 목록의 각 멤버를 반복 `Enrollment` [List](https://msdn.microsoft.com/library/6sh2ey19.aspx) 하 고, 등록을 데이터베이스에서 찾을 수 없는 경우 데이터베이스에 등록을 추가 합니다. 처음으로 데이터베이스를 업데이트할 때 데이터베이스는 비어 있으므로 각 등록을 추가 합니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. 프로젝트를 빌드합니다.

### <a name="execute-the-first-migration"></a>첫 번째 마이그레이션 실행

명령을 실행 하면 `add-migration` 마이그레이션을 통해 데이터베이스를 처음부터 만드는 코드가 생성 됩니다. 이 코드는 또한 * &lt; 타임 스탬프 &gt; \_ InitialCreate.cs*이라는 파일의 *마이그레이션* 폴더에 있습니다. `Up`클래스의 메서드는 `InitialCreate` 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만들고 메서드는 해당 테이블을 `Down` 삭제 합니다.

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.

이는 명령을 입력할 때 생성 된 초기 마이그레이션입니다 `add-migration InitialCreate` . 파일 이름에는 매개 변수 ( `InitialCreate` 예:)가 사용 되며 원하는 모든 항목을 사용할 수 있습니다. 일반적으로 마이그레이션에서 수행 되는 항목을 요약 하는 단어나 구를 선택 합니다. 예를 들어 이후 마이그레이션 AddDepartmentTable의 이름을로 할 수 있습니다 &quot; &quot; .

데이터베이스가 이미 존재할 때 초기 마이그레이션을 만든 경우 데이터베이스 만들기 코드가 생성되지만 데이터베이스는 이미 데이터 모델과 일치하기 때문에 실행할 필요는 없습니다. 데이터베이스가 아직 없는 다른 환경에 앱을 배포하는 경우 이 코드를 실행하여 데이터베이스를 만들기 때문에 먼저 테스트하는 것이 좋습니다. 앞 &mdash; 에서 새로 만들 수 있도록 연결 문자열에서 데이터베이스 이름을 변경한 이유 때문입니다.

1. **패키지 관리자 콘솔** 창에서 다음 명령을 입력합니다.

    `update-database`

    `update-database`이 명령은 메서드를 `Up` 실행 하 여 데이터베이스를 만든 다음 메서드를 실행 하 여 `Seed` 데이터베이스를 채웁니다. 다음 섹션에서 볼 수 있듯이 응용 프로그램을 배포한 후 프로덕션 환경에서 동일한 프로세스가 자동으로 실행 됩니다.
2. **서버 탐색기** 를 사용 하 여 첫 번째 자습서에서 했던 것 처럼 데이터베이스를 검사 하 고 응용 프로그램을 실행 하 여 모든 항목이 이전과 동일 하 게 작동 하는지 확인 합니다.

## <a name="deploy-to-azure"></a>Azure에 배포

지금까지 응용 프로그램은 개발 컴퓨터의 IIS Express에서 로컬로 실행 되었습니다. 다른 사용자가 인터넷을 통해 사용할 수 있도록 하려면 웹 호스팅 공급자에 배포 해야 합니다. 자습서의이 섹션에서는 Azure에 배포 합니다. 이 섹션은 선택 사항입니다. 이 작업을 건너뛰고 다음 자습서를 계속 진행 하거나, 선택한 다른 호스팅 공급자에 대해이 섹션의 지침을 적용할 수 있습니다.

### <a name="use-code-first-migrations-to-deploy-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스 배포

데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 합니다. Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용 하는 게시 프로필을 만들 때 **데이터베이스 업데이트**라는 확인란을 선택 합니다. 이 설정을 사용 하면 Code First가 이니셜라이저 클래스를 사용 하도록 배포 프로세스에서 대상 서버에 응용 프로그램 *web.config* 파일을 자동으로 구성 합니다 `MigrateDatabaseToLatestVersion` .

Visual Studio는 프로젝트를 대상 서버에 복사 하는 동안 배포 프로세스 중에 데이터베이스에서 어떤 작업도 수행 하지 않습니다. 배포 된 응용 프로그램을 실행 하 고 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First는 데이터베이스가 데이터 모델과 일치 하는지 확인 합니다. 일치 하지 않는 경우 Code First는 데이터베이스를 자동으로 만들거나 (아직 존재 하지 않는 경우) 데이터베이스 스키마를 최신 버전으로 업데이트 합니다 (데이터베이스가 있지만 모델과 일치 하지 않는 경우). 응용 프로그램이 마이그레이션 방법을 구현 하는 경우이 `Seed` 메서드는 데이터베이스가 만들어지거나 스키마가 업데이트 된 후에 실행 됩니다.

마이그레이션 `Seed` 방법은 테스트 데이터를 삽입 합니다. 프로덕션 환경에 배포 하는 경우 `Seed` 프로덕션 데이터베이스에 삽입 하려는 데이터만 삽입 하도록 메서드를 변경 해야 합니다. 예를 들어 현재 데이터 모델에서는 개발 데이터베이스에 실제 강의를 포함 하 고 가상 학생이 있을 수 있습니다. 개발 중에를 `Seed` 로드 하는 메서드를 작성 한 다음 프로덕션에 배포 하기 전에 가상 학생을 주석으로 처리할 수 있습니다. 또는 `Seed` 단지 강좌를 로드 하는 메서드를 작성 하 고 응용 프로그램의 UI를 사용 하 여 테스트 데이터베이스에 가상 학생을 수동으로 입력할 수 있습니다.

### <a name="get-an-azure-account"></a>Azure 계정 가져오기

Azure 계정이 필요 합니다. 아직 없는 경우 Visual Studio 구독이 있는 경우 [구독 혜택을 활성화할](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)수 있습니다. 그렇지 않으면 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/free/)을 참조 하세요.

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Azure에서 웹 사이트 및 SQL 데이터베이스 만들기

Azure의 웹 앱은 공유 호스팅 환경에서 실행 됩니다. 즉, 다른 Azure 클라이언트와 공유 되는 Vm (가상 머신)에서 실행 됩니다. 공유 호스팅 환경은 클라우드를 시작하는 저비용 방법입니다. 나중에 웹 트래픽이 증가하면 애플리케이션이 전용 VM에서 실행되어 요구에 맞게 확장될 수 있습니다. Azure App Service에 대 한 가격 책정 옵션에 대 한 자세한 내용은 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조 하세요.

Azure SQL database에 데이터베이스를 배포 합니다. SQL database는 SQL Server 기술을 기반으로 구축 된 클라우드 기반의 관계형 데이터베이스 서비스입니다. SQL Server와 함께 작동 하는 도구 및 응용 프로그램은 SQL database 에서도 작동 합니다.

1. [Azure 관리 포털](https://portal.azure.com)의 왼쪽 탭에서 **리소스 만들기** 를 선택한 다음 **새** 창 또는 *블레이드에서* **모두 보기** 를 선택 하 여 사용 가능한 모든 리소스를 확인 합니다. **모든** 블레이드의 **웹** 섹션에서 **웹 앱 + SQL** 을 선택 합니다. 마지막으로 **만들기**를 선택 합니다.

    ![Azure Portal에서 리소스 만들기](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   새 **웹 앱 + SQL** 리소스를 만드는 양식이 열립니다.

2. 응용 프로그램의 고유한 URL로 사용할 **앱 이름** 상자에 문자열을 입력 합니다. 전체 URL은 여기에 입력 한 내용 및 Azure 앱 서비스의 기본 도메인 (. azurewebsites.net)으로 구성 됩니다. **앱 이름이** 이미 사용 되 고 있으면 마법사에서 빨간색으로 표시 되 *고 앱 이름을 사용할 수 없음* 메시지가 표시 됩니다. **앱 이름을** 사용할 수 있는 경우 녹색 확인 표시가 나타납니다.

3. **구독** 상자에서 **App Service** 상주할 Azure 구독을 선택 합니다.

4. **리소스 그룹** 텍스트 상자에서 리소스 그룹을 선택 하거나 새 리소스 그룹을 만듭니다. 이 설정은 웹 사이트를 실행 하는 데이터 센터를 지정 합니다. 리소스 그룹에 대 한 자세한 내용은 [리소스 그룹](/azure/azure-resource-manager/resource-group-overview#resource-groups)을 참조 하세요.

5. *App Service 섹션*을 클릭 하 고, **새로 만들기**를 클릭 하 고 **App Service 계획** 을 입력 하 고 (App Service와 동일한 이름), **위치**및 **가격 책정 계층** (무료 옵션)을 클릭 하 여 새 **App Service 계획** 을 만듭니다.

6. **SQL Database**를 클릭 한 다음 **새 데이터베이스 만들기** 를 선택 하거나 기존 데이터베이스를 선택 합니다.

7. **이름** 상자에 데이터베이스의 이름을 입력 합니다.
8. **대상 서버** 상자를 클릭 한 다음 **새 서버 만들기**를 선택 합니다. 또는 이전에 서버를 만든 경우 사용 가능한 서버 목록에서 해당 서버를 선택할 수 있습니다.
9. **가격 책정 계층** 섹션을 선택 하 고 *무료*를 선택 합니다. 추가 리소스가 필요한 경우 언제 든 지 데이터베이스를 확장할 수 있습니다. Azure SQL 가격에 대 한 자세한 내용은 [Azure SQL Database 가격 책정](https://azure.microsoft.com/pricing/details/sql-database/managed/)을 참조 하세요.
10. 필요에 따라 [데이터 정렬을](/sql/relational-databases/collations/collation-and-unicode-support) 수정 합니다.
11. 관리자 Sql 관리자 **사용자 이름** 및 **sql 관리자 암호**를 입력 합니다.

    - **새 SQL Database 서버**를 선택한 경우 나중에 데이터베이스에 액세스할 때 사용할 새 이름과 암호를 정의 합니다.
    - 이전에 만든 서버를 선택한 경우 해당 서버에 대 한 자격 증명을 입력 합니다.

12. Application Insights를 사용 하 여 App Service에 대 한 원격 분석 수집을 사용 하도록 설정할 수 있습니다. 약간의 구성으로 Application Insights는 중요 한 이벤트, 예외, 종속성, 요청 및 추적 정보를 수집 합니다. Application Insights에 대해 자세히 알아보려면 [Azure Monitor](https://azure.microsoft.com/services/monitor/)를 참조 하세요.
13. 맨 아래에서 **만들기** 를 클릭 하 여 완료 되었음을 표시 합니다.

    관리 포털 대시보드 페이지로 반환 되 고 페이지 맨 위에 있는 **알림** 영역에 사이트가 생성 되 고 있는 것으로 표시 됩니다. 잠시 후 (일반적으로 1 분 미만) 배포에 성공 했다는 알림이 발생 합니다. 왼쪽의 탐색 모음에 새 App Service **App Services** 섹션에 표시 되 고 **sql** 데이터베이스 섹션에 새 sql 데이터베이스가 표시 됩니다.

### <a name="deploy-the-app-to-azure"></a>Azure에 앱 배포

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.

2. **게시 대상 선택** 페이지에서 **App Service** 를 선택한 다음 **기존을 선택**하 고 **게시**를 선택 합니다.

    ![게시 대상 선택 페이지](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/select-existing-app-service.png)

3. 이전에 Visual Studio에서 Azure 구독을 추가 하지 않은 경우 화면에서 단계를 수행 합니다. 이러한 단계를 통해 Visual Studio가 **App Services** 목록에 웹 사이트를 포함 하도록 Azure 구독에 연결할 수 있습니다.

4. **App Service** 페이지에서 App Service 추가 된 **구독** 을 선택 합니다. **보기**아래에서 **리소스 그룹**을 선택 합니다. App Service 추가한 리소스 그룹을 확장 한 다음 App Service를 선택 합니다. **확인** 을 선택 하 여 앱을 게시 합니다.

5. **출력** 창에 수행된 배포 작업이 표시되고 성공적인 배포 완료가 보고됩니다.

6. 성공적으로 배포 되 면 배포 된 웹 사이트의 URL에 대 한 기본 브라우저가 자동으로 열립니다.

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    앱이 이제 클라우드에서 실행 되 고 있습니다.

이 시점에서 **Code First 마이그레이션 실행 (앱 시작 시 실행)** 을 선택 하 여 Azure SQL Database에서 *schoolcontext.cs* 데이터베이스를 만들었습니다. 배포 된 웹 *사이트의 web.config 파일이 변경* 되어 코드가 처음으로 데이터베이스에서 데이터를 읽거나 쓸 때 ( **학생** 탭을 선택 했을 때 발생) [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저가 실행 됩니다.

![Web.config 파일 발췌](https://asp.net/media/4367421/mig.png)

또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하 고 데이터베이스를 시드 하는 데 사용할 Code First 마이그레이션에 대 한 새 연결 문자열 *(Schoolcontext.cs \_ databasepublish*)을 만들었습니다.

![Web.config 파일의 연결 문자열](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*의 사용자 컴퓨터에서 배포 된 버전의 web.config 파일을 찾을 수 있습니다. FTP를 사용 하 여 배포 된 *web.config* 파일 자체에 액세스할 수 있습니다. 지침은 [Visual Studio를 사용 하 여 웹 배포 ASP.NET: 코드 업데이트 배포](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)를 참조 하세요. "FTP 도구를 사용 하려면 FTP URL, 사용자 이름 및 암호를 사용 해야 합니다."로 시작 하는 지침을 따르세요.

> [!NOTE]
> 웹 앱은 보안을 구현 하지 않으므로 URL을 검색 하는 모든 사용자가 데이터를 변경할 수 있습니다. 웹 사이트를 보호 하는 방법에 대 한 지침은 [멤버 자격, OAuth 및 SQL database가 포함 된 secure ASP.NET MVC 앱을 Azure에 배포](/aspnet/core/security/authorization/secure-data)를 참조 하세요. Visual Studio에서 Azure 관리 포털 또는 **서버 탐색기** 를 사용 하 여 서비스를 중지 하 여 다른 사용자가 사이트를 사용 하지 못하도록 할 수 있습니다.

![앱 서비스 중지 메뉴 항목](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>고급 마이그레이션 시나리오

이 자습서에 표시 된 것 처럼 마이그레이션을 자동으로 실행 하 여 데이터베이스를 배포 하 고 여러 서버에서 실행 되는 웹 사이트에 배포 하는 경우 여러 서버에서 동시에 마이그레이션을 실행 하려고 할 수 있습니다. 마이그레이션은 원자성 이므로 두 서버가 동일한 마이그레이션을 실행 하려고 하면 하나는 성공 하 고 나머지는 실패 하 게 됩니다 (작업을 두 번 수행할 수 없다고 가정). 이 시나리오에서는 이러한 문제를 방지 하려는 경우 마이그레이션을 수동으로 호출 하 고 한 번만 수행 하도록 사용자 고유의 코드를 설정할 수 있습니다. 자세한 내용은 주문형의 블로그 및 [debug.exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) (명령줄에서 마이그레이션을 실행 하는 경우)에서 [코드에서 마이그레이션을 실행 하 고 스크립팅](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/) 하는 방법을 참조 하세요.

다른 마이그레이션 시나리오에 대 한 자세한 내용은 migration [동영상 가이드 Series](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)항목을 참조 하세요.

## <a name="update-specific-migration"></a>특정 마이그레이션 업데이트

`update-database -target MigrationName`

`update-database -target MigrationName`명령은 대상 마이그레이션을 실행 합니다.

## <a name="ignore-migration-changes-to-database"></a>데이터베이스 마이그레이션 변경 내용 무시

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges`현재 모델을 스냅숏으로 사용 하 여 빈 마이그레이션을 만듭니다.

## <a name="code-first-initializers"></a>Code First 이니셜라이저

배포 섹션에서 사용 되는 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 살펴보았습니다. [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값), [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (이전에 사용한) 및 [dropcreatedatabasealways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)를 비롯 한 다른 이니셜라이저가 제공 됩니다. Code First `DropCreateAlways`이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다. 사용자 고유의 이니셜라이저를 작성 하 고 응용 프로그램이 데이터베이스에서 읽거나 데이터베이스에 쓸 때까지 기다리지 않으려는 경우 이니셜라이저를 명시적으로 호출할 수도 있습니다.

이니셜라이저에 대 한 자세한 내용은 [Entity Framework Code First의 데이터베이스 이니셜라이저 이해](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm) 및 설명서의 6 장 [프로그래밍 Entity Framework:](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 및 rowan를 통해 Code First

## <a name="get-the-code"></a>코드 다운로드

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 데이터 액세스-권장 리소스](xref:whitepapers/aspnet-data-access-content-map)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * Code First 마이그레이션 사용
> * Azure에 앱을 배포 합니다 (선택 사항).

ASP.NET MVC 응용 프로그램에 더 복잡 한 데이터 모델을 만드는 방법에 대해 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [더 복잡 한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
