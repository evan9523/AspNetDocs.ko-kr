---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Id-ASP.NET에 대 한 사용자 지정 저장소 공급자 개요 4.x
author: Rick-Anderson
description: ASP.NET Id는 사용자 고유의 저장소 공급자를 만들고 응용은 작업이 다시 실행 하지 않고 응용 프로그램에 연결할 수 있는 확장 가능한 시스템...
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 71201e9d91080855350349b966fe7916ce21a909
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411269"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity에 대한 사용자 지정 스토리지 공급자 개요

[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Id는 확장 가능한 시스템 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 사용 하지 않고 응용 프로그램에 연결할 수 있습니다. 이 항목에서는 ASP.NET Id에 대 한 사용자 지정된 저장소 공급자를 만드는 방법을 설명 합니다. 사용자 고유의 저장소 공급자를 만들기 위한 중요 한 개념을 설명 하는 사용자 지정 저장소 공급자를 구현 하는 단계별 연습 것만 합니다.
> 
> 사용자 지정 저장소 공급자를 구현 하는 예제를 보려면 [사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)합니다.
> 
> 이 항목에서는 ASP.NET Identity 2.0에 대 한 업데이트 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2013 업데이트 2
> - ASP.NET Id 2


## <a name="introduction"></a>소개

기본적으로 ASP.NET Id 시스템을 SQL Server 데이터베이스에 사용자 정보를 저장 하 고 데이터베이스를 만들려고 Entity Framework Code First를 사용 합니다. 대부분의 응용 프로그램에 대 한이 방법은 잘 작동합니다. 그러나 다른 유형의 Azure Table Storage 등의 지 속성 메커니즘을 사용 하는 것이 좋습니다 또는 기본 구현 보다 매우 다른 구조를 사용 하 여 데이터베이스 테이블을 이미 있을 수도 있습니다. 두 경우 모두 저장소 메커니즘에 대 한 사용자 지정된 공급자를 작성할 수 있으며 응용 프로그램에 해당 공급자를 연결할 수 있습니다.

ASP.NET Id는 다양 한 Visual Studio 2013 서식 파일에는 기본적으로 포함 됩니다. 통해 ASP.NET Id로 업데이트를 가져올 수 있습니다 [Microsoft AspNet Identity EntityFramework NuGet 패키지](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)합니다.

이 항목에는 다음 단원이 포함되어 있습니다.

- [아키텍처 이해](#architecture)
- [저장 된 데이터 이해](#data)
- [데이터 액세스 레이어 만들기](#dal)
- [사용자 클래스를 사용자 지정](#user)
- [사용자 저장소를 사용자 지정](#userstore)
- [역할 클래스를 사용자 지정](#role)
- [역할 저장소를 사용자 지정](#rolestore)
- [새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성](#reconfigure)
- [다른 사용자 지정 저장소 공급자 구현](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>아키텍처 이해

ASP.NET Id 관리자 및 저장소를 호출 하는 클래스로 구성 됩니다. 관리자는 응용 프로그램 개발자는 ASP.NET Id 시스템에 사용자를 만드는 등의 작업을 수행 하는 상위 클래스입니다. 저장소는 사용자와 역할 같은 엔터티를 유지 되는 방법을 지정 하는 하위 클래스입니다. 저장소는 지 속성 메커니즘을 사용 하 여 밀접 하 게 결합 되어 있지만 관리자는에서 분리 된 저장소는 전체 응용 프로그램을 방해 없이 지 속성 메커니즘을 바꿀 수 있습니다.

다음 다이어그램에서는 웹 응용 프로그램 관리자와 상호 작용 하는 방법 및 저장소 데이터 액세스 계층 상호 작용 합니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

ASP.NET Id에 대 한 사용자 지정된 저장소 공급자를 만들려면이 데이터 액세스 계층을 사용 하 여 데이터 원본, 데이터 액세스 계층 및 상호 작용 하는 저장소 클래스를 만들 필요가 있습니다. 사용자에 했지만 이제 데이터가 다른 저장소 시스템에 저장 되는 데이터 작업을 수행 하려면 동일한 관리자 Api를 사용 하 여 계속할 수 있습니다.

사용자 클래스 형식의 UserManager RoleManager의 새 인스턴스를 만들 때 제공한 관리자 클래스를 사용자 지정 및 저장소 클래스의 인스턴스를 인수로 전달할 필요가 없습니다. 이 방법을 사용 하면 기존 구조에 사용자 지정된 클래스를 연결할 수 있습니다. UserManager 및 RoleManager 섹션에서 사용자 지정 된 저장소 클래스를 사용 하 여 인스턴스화하는 방법을 보면 [새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성](#reconfigure)합니다.

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>저장 된 데이터 이해

사용자 지정 저장소 공급자를 구현 하려면 ASP.NET Id를 사용 하는 데이터 형식을 이해 하 고 응용 프로그램과 관련 되는 기능을 결정 해야 합니다.

| 데이터 | 설명 |
| --- | --- |
| Users | 웹 사이트의 사용자를 등록된 합니다. 사용자 Id 및 사용자 이름을 포함합니다. 사용자가 사이트에 관련 된 자격 증명으로 로그인 하는 경우에 해시 된 암호를 포함할 수 있습니다 (을 하지 않고 자격 증명을 사용 하 여 Facebook과 같은 외부 사이트에서) 및 아무 것도 사용자 자격 증명이 변경 되었는지 여부를 나타내는 보안 스탬프입니다. 또한 전자 메일 주소를 포함할 수 있습니다, 전화 번호, 실패 한 로그인을 현재 수를 2 단계 인증이 사용 되는지 여부를 계정을 잠 궜 습니다 여부 및 합니다. |
| 사용자 클레임 | 사용자의 id를 나타내는 사용자에 대 한 문 (또는 클레임)의 집합. 사용자의 id 역할을 통해 수행할 수 있습니다 보다 큰 식을 설정할 수 있습니다. |
| 사용자 로그인 | 외부 인증 공급자 (예: Facebook)에 대 한 정보는 사용자를 로그인 할 때 사용 하도록 합니다. |
| 역할 | 사이트에 대 한 권한 부여 그룹입니다. 역할 Id 및 역할 이름 (예: "Admin" 또는 "Employee")를 포함합니다. |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>데이터 액세스 레이어 만들기

이 항목에서는 사용 하고자 하는 지 속성 메커니즘 및 해당 메커니즘에 대 한 엔터티를 만드는 방법에 익숙하다고 가정 합니다. 이 항목에서는 저장소 또는 데이터 액세스 클래스를 만드는 방법에 대 한 정보를 제공 하지 않습니다. 대신, 디자인 결정에 대 한 ASP.NET Id를 사용 하 여 작업할 때 해야 할 몇 가지 제안을 제공 합니다.

저장소 공급자 자유롭게 사용자 지정에 대 한 리포지토리를 디자인할 때 많이 있습니다. 응용 프로그램에서 사용 하려는 기능에 대 한 리포지토리를 만들 해야 합니다. 예를 들어, 응용 프로그램에서 역할을 사용 하지 않는 경우 역할 또는 사용자 역할에 대 한 저장소를 만들 필요가 없습니다. 기술 및 기존 인프라에는 ASP.NET Identity의 기본 구현에서 매우 다른 구조가 필요할 수 있습니다. 데이터 액세스 계층, 리포지토리의 구조와 작동 하는 논리를 제공 합니다.

MySQL 구현 하는 ASP.NET Identity 2.0에 대 한 데이터 리포지토리를 참조 하세요 [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)합니다.

데이터 액세스 계층을 데이터 원본에 ASP.NET Id에서 데이터를 저장 하는 논리를 제공 합니다. 사용자 지정된 저장소 공급자에 대 한 데이터 액세스 계층 사용자 및 역할 정보를 저장 하는 다음 클래스를 포함할 수 있습니다.

| 클래스 | 설명 | 예제 |
| --- | --- | --- |
| 컨텍스트 | 지 속성 메커니즘에 연결 하 여 쿼리를 실행 하는 정보를 캡슐화 합니다. 이 클래스는 핵심 데이터 액세스 계층입니다. 다른 데이터 클래스를 해당 작업을 수행 하려면이 클래스의 인스턴스를 필요 합니다. 또한이 클래스의 인스턴스를 사용 하 여 저장소 클래스를 초기화 합니다. | [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 사용자 저장소 | 저장 하 고 사용자 정보 (예: 사용자 이름 및 암호 해시)을 검색 합니다. | [UserTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 역할 저장소 | 저장 하 고 (예: 역할 이름) 역할 정보를 검색 합니다. | [RoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 저장소 | 저장 하 고 사용자 클레임 정보 (예: 클레임 유형과 값)을 검색 합니다. | [UserClaimsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 저장소 | 저장 하 고 사용자 로그인 정보 (예: 외부 인증 공급자)를 검색 합니다. | [UserLoginsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole 저장소 | 저장 하 고 사용자에 할당 된 역할을 검색 합니다. | [UserRoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

마찬가지로 응용 프로그램에서 사용 하려는 클래스를 구현 하기만 하면 됩니다.

데이터 액세스 클래스에 특정 지 속성 메커니즘에 대 한 데이터 작업을 수행 하는 코드를 제공 합니다. 예를 들어 MySQL 구현 내에서 UserTable 클래스는 사용자가 데이터베이스 테이블을 사용 하 여 새 레코드를 삽입 하는 메서드를 포함 합니다. 명명 된 변수의 `_database` MySQLDatabase 클래스의 인스턴스입니다.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

데이터 액세스 클래스를 만든 후 데이터 액세스 계층의 특정 메서드를 호출 하는 저장소 클래스를 만들어야 합니다.

<a id="user"></a>
## <a name="customize-the-user-class"></a>사용자 클래스를 사용자 지정

해당 하는 사용자 정의 클래스 사용자 고유의 저장소 공급자를 구현할 때 만들어야 합니다 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx) 클래스는 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스:

다음 다이어그램에는 만들어야 하는 IdentityUser 클래스 및이 클래스에서 구현 하는 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

합니다 [IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스 usermanager가 요청 된 작업을 수행 하는 경우 호출 하려고 시도 하는 속성을 정의 합니다. 인터페이스 Id 및 사용자 이름 두 속성을 포함합니다. 합니다 [IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스를 사용 하면 제네릭을 통해 사용자에 대 한 키의 형식을 지정할 수 있습니다 **TKey** 매개 변수입니다. Id 속성의 형식을 TKey 매개 변수의 값을 찾습니다.

Id 프레임 워크를 제공 합니다 [IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx) 인터페이스 (하지 않고 제네릭 매개 변수) 키에 대 한 문자열 값을 사용 하려는 경우.

IdentityUser 클래스 IUser 구현 및 추가 속성 또는 웹 사이트에서 사용자에 대 한 생성자를 포함 합니다. 다음 예제에서는 키에 대 한 정수를 사용 하 여 IdentityUser 클래스를 보여 줍니다. Id 필드 설정 되어 **int** 제네릭 매개 변수의 값과 일치 하도록 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 완전 한 구현에 대 한 참조 [IdentityUser (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs)합니다. 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>사용자 저장소를 사용자 지정

또한 사용자에 모든 데이터 작업에 대 한 메서드를 제공 하는 UserStore 클래스를 만듭니다. 이 클래스는 해당 하는 [UserStore&lt;TUser&gt; ](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx) 클래스를 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스입니다. UserStore 클래스에서 구현 된 [IUserStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 및 선택적 인터페이스입니다. 응용 프로그램에서 제공 하려는 기능에 따라 구현 해야 하는 선택적 인터페이스를 선택 합니다.

다음 이미지에는 만들어야 UserStore 클래스 및 관련 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

기본 프로젝트 템플릿을 Visual Studio에서 사용자 저장소에 구현 된 여러 가지 선택적 인터페이스를 가정 하는 코드를 포함 합니다. 기본 템플릿을 사용자 지정된 사용자 저장소를 사용 하는 경우 사용자 저장소의 선택적 인터페이스를 구현 하거나 더 이상 사용자가 구현한 인터페이스의 메서드를 호출 하는 템플릿 코드를 변경 합니다.

 다음 예제에서는 간단한 사용자 저장소 클래스를 보여 줍니다. 합니다 **TUser** 제네릭 매개 변수는 일반적으로 정의한 IdentityUser 클래스는 사용자 클래스의 형식입니다. 합니다 **TKey** 제네릭 매개 변수는 사용자 키의 형식입니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 이 예제에서는 생성자 매개 변수를 사용 하는 이름이 *데이터베이스* ExampleDatabase 형식의 데이터 액세스 클래스에 전달 하는 방법의 그림을입니다. 예를 들어 MySQL 구현에서는이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다. 

UserStore 클래스 내에서 작업을 수행 하기 위해 만든 데이터 액세스 클래스를 사용할 수 있습니다. 예를 들어 MySQL 구현에서 UserStore 클래스에 UserTable의 인스턴스를 사용 하 여 새 레코드를 삽입 하는 CreateAsync 메서드 합니다 **삽입** 메서드는 **userTable** 개체는 이전 섹션에 표시 된 것과 동일한 메서드. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>사용자 저장소를 사용자 지정할 때 구현 하는 인터페이스

다음 이미지는 각 인터페이스에 정의 된 기능에 대 한 자세한 세부 정보를 보여 줍니다. 모든 선택적 인터페이스 IUserStore에서 상속합니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  합니다 [IUserStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) 인터페이스는 인터페이스에서 사용자 저장소를 구현 해야 합니다. 만들기, 업데이트, 삭제 및 사용자를 검색 하기 위한 메서드를 정의 합니다.
- **IUserClaimStore**  
  합니다 [IUserClaimStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx) 인터페이스 메서드를 정의 합니다. 사용자 클레임을 사용 하도록 설정 하기 위해 사용자 저장소에서 구현 해야 합니다. 메서드 또는 추가, 제거 및 사용자 클레임을 검색을 포함 합니다.
- **IUserLoginStore**  
  합니다 [IUserLoginStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx) 메서드를 정의 외부 인증 공급자를 사용 하도록 설정 하기 위해 사용자 저장소에서 구현 해야 합니다. 추가, 제거 및 사용자 로그인 및 로그인 정보를 기반으로 사용자를 검색 하는 메서드를 검색 하는 메서드를 포함 합니다.
- **IUserRoleStore**  
  합니다 [IUserRoleStore&lt;TKey, TUser&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 인터페이스 메서드를 정의 합니다. 사용자 역할에 매핑할 사용자 저장소에서 구현 해야 합니다. 추가, 제거 및 사용자의 역할 및 역할에 사용자가 할당 되었는지 확인 하는 메서드를 검색 하는 메서드를 포함 합니다.
- **IUserPasswordStore**  
  [IUserPasswordStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx) 인터페이스 유지 하기 위해 사용자 저장소에서 구현 해야 하는 메서드를 정의 합니다. 암호를 해시 합니다. 가져와 사용자가 암호를 설정 하는지 여부를 나타내는 메서드와 해시 된 암호를 설정 하는 메서드를 포함 합니다.
- **IUserSecurityStampStore**  
  합니다 [IUserSecurityStampStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx) 인터페이스 사용자의 계정 정보 변경 되었는지 여부를 나타내는 보안 스탬프를 사용 하 여 사용자 저장소에서 구현 해야 하는 메서드를 정의 합니다. . 사용자 암호를 변경 또는 추가 하거나 로그인을 제거 하는 경우이 스탬프 업데이트 됩니다. 가져오기 및 설정의 보안 스탬프에 대 한 메서드를 포함 합니다.
- **IUserTwoFactorStore**  
  합니다 [IUserTwoFactorStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx) 인터페이스 구현에 구현 2 단계 인증을 해야 하는 메서드를 정의 합니다. 가져와 사용자에 대 한 2 단계 인증이 사용 되는지 여부를 설정 하는 메서드를 포함 합니다.
- **IUserPhoneNumberStore**  
  합니다 [IUserPhoneNumberStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx) 인터페이스 사용자 전화 번호를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 가져오기 및 전화 번호 및 전화 번호가 확인 되었는지 여부를 설정에 대 한 메서드를 포함 합니다.
- **IUserEmailStore**  
  합니다 [IUserEmailStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx) 인터페이스 사용자 전자 메일 주소를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 가져오기 및 전자 메일 주소 및 전자 메일 확인 되었는지 여부를 설정에 대 한 메서드를 포함 합니다.
- **IUserLockoutStore**  
  합니다 [IUserLockoutStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx) 인터페이스 계정 잠금에 대 한 정보를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 현재 실패 한 액세스 시도 횟수를 시작, 가져오기, 계정을 잠글 수, 가져오기 및 잠금 종료 날짜를 설정, 시도 실패 수가 증가 하는지 여부를 설정 및 실패 한 시도 횟수를 다시 설정에 대 한 메서드를 포함 합니다.
- **IQueryableUserStore**  
  합니다 [IQueryableUserStore&lt;TUser, TKey&gt; ](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx) 인터페이스 멤버를 정의 합니다 쿼리 가능한 사용자 저장소를 제공 하도록 구현 해야 합니다. 쿼리 가능 사용자를 포함 하는 속성을 포함 합니다.

  응용 프로그램에서 필요한 인터페이스를 구현 같은 IUserClaimStore, IUserLoginStore, IUserRoleStore, IUserPasswordStore, 및 IUserSecurityStampStore 아래와 같이 인터페이스입니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

완전 한 구현 (인터페이스를 모두 포함)를 참조 하세요. [UserStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs)합니다.

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim, IdentityUserLogin, 및 IdentityUserRole

Microsoft.AspNet.Identity.EntityFramework 네임 스페이스에 구현 된 [IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx)를 [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx), 및 [IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx) 클래스입니다. 이러한 기능을 사용 하는 경우에 이러한 클래스의 고유한 버전을 만들고 응용 프로그램에 대 한 속성을 정의 하는 것이 좋습니다. 그러나 경우가 없습니다 (예: 추가 또는 제거 하는 사용자의 클레임) 기본 작업을 수행할 때 이러한 엔터티를 메모리로 로드 하는 것이 효율적입니다. 대신 백 엔드 저장소 클래스는 데이터 원본에서 직접 이러한 작업을 실행할 수 있습니다. 예를 들어 UserStore.GetClaimsAsync() 메서드는 userClaimTable.FindByUserId(user.를 호출할 수 있습니다. Id)에서 쿼리를 실행 하려면 반환 메서드를 직접 테이블 클레임 목록입니다.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>역할 클래스를 사용자 지정

해당 하는 역할 클래스를 사용자 고유의 저장소 공급자를 구현할 때 만들어야 합니다 [IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx) 클래스는 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스:

다음 다이어그램에는 만들어야 하는 IdentityRole 클래스 및이 클래스에서 구현 하는 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

합니다 [IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스는 RoleManager 요청 된 작업을 수행 하는 경우 호출 하려고 시도 하는 속성을 정의 합니다. 인터페이스는 두 속성-Id 및 이름을 포함합니다. 합니다 [IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스를 사용 하면 제네릭을 통해 역할에 대 한 키의 형식을 지정할 수 있습니다 **TKey** 매개 변수입니다. Id 속성의 형식을 TKey 매개 변수의 값을 찾습니다.

Id 프레임 워크를 제공 합니다 [IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx) 인터페이스 (하지 않고 제네릭 매개 변수) 키에 대 한 문자열 값을 사용 하려는 경우.

다음 예제에서는 키에 대 한 정수를 사용 하 여 IdentityRole 클래스를 보여 줍니다. Id 필드는 제네릭 매개 변수의 값과 일치 하도록 int로 설정 됩니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 완전 한 구현에 대 한 참조 [IdentityRole (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs)합니다. 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>역할 저장소를 사용자 지정

또한 모든 데이터 작업 역할에 대 한 메서드를 제공 하는 RoleStore 클래스를 만듭니다. 이 클래스는 해당 하는 [RoleStore&lt;TRole&gt; ](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) Microsoft.ASP.NET.Identity.EntityFramework 네임 스페이스의 클래스입니다. RoleStore 클래스에서 구현 된 [IRoleStore&lt;TRole, TKey&gt; ](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) 및 필요에 따라 합니다 [IQueryableRoleStore&lt;TRole, TKey&gt; ](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx) 인터페이스입니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

다음 예제에서는 역할 저장소 클래스를 보여 줍니다. TRole 제네릭 매개 변수는 일반적으로 정의한 IdentityRole 클래스는 역할 클래스의 형식입니다. TKey 제네릭 매개 변수는 역할 키의 형식입니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  합니다 [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx) 인터페이스 역할 저장소 클래스에서 구현 하는 메서드를 정의 합니다. 만들기, 업데이트, 삭제 및 역할을 검색 하는 메서드를 포함 합니다.
- **RoleStore&lt;TRole&gt;**  
  RoleStore에 맞게 IRoleStore 인터페이스를 구현 하는 클래스를 만듭니다. 경우에이 클래스를 구현 하기만 하면 시스템에서 역할을 사용 하려면. 명명 된 매개 변수를 사용 하는 생성자 *데이터베이스* ExampleDatabase 형식의 데이터 액세스 클래스에 전달 하는 방법의 그림을입니다. 예를 들어 MySQL 구현에서는이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다.  
  
  완전 한 구현에 대 한 참조 [RoleStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) 합니다.

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성

새 저장소 공급자를 구현 했습니다. 이제이 저장소 공급자를 사용 하도록 응용 프로그램을 구성 해야 합니다. 기본 저장소 공급자 프로젝트에 포함 된 경우 기본 공급자를 제거 하 고 공급자를 사용 하 여 대체 합니다.

### <a name="replace-default-storage-provider-in-mvc-project"></a>MVC 프로젝트에서 기본 저장소 공급자를 대체 합니다.

1. 에 **NuGet 패키지 관리** 창에서 제거 합니다 **Microsoft ASP.NET Identity EntityFramework** 패키지 합니다. Identity.EntityFramework에 대 한 설치 된 패키지를 검색 하 여이 패키지를 찾을 수 있습니다.  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) Entity Framework를 제거 하려는 경우 라는 메시지가 표시 됩니다. 응용 프로그램의 다른 부분에서 필요 하지 않는 경우에이 제거할 수 있습니다.
2. Models 폴더에서 IdentityModels.cs 파일을 삭제 하거나 주석으로 처리 합니다 **ApplicationUser** 하 고 **ApplicationDbContext** 클래스입니다. MVC 응용 프로그램에서 전체 IdentityModels.cs 파일을 삭제할 수 있습니다. Web Forms 응용 프로그램에서는 두 개의 클래스를 삭제 하지만 IdentityModels.cs 파일에도 있는 도우미 클래스를 유지 해야 합니다.
3. 저장소 공급자에는 별도 프로젝트에 있는 경우 웹 응용 프로그램에서에 대 한 참조를 추가 합니다.
4. 에 대 한 모든 참조를 대체 `using Microsoft.AspNet.Identity.EntityFramework;` 을 사용 하 여 저장소 공급자의 네임 스페이스에 대 한 문입니다.
5. 에 **Startup.Auth.cs** 클래스를 변경 합니다 **ConfigureAuth** 적절 한 컨텍스트의 단일 인스턴스를 사용 하는 방법입니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 앱에서\_시작 폴더를 열고 **IdentityConfig.cs**합니다. ApplicationUserManager 클래스에서 변경 된 **만들기** 사용자 지정된 사용자 저장소를 사용 하는 사용자 관리자를 반환 하는 방법입니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. 에 대 한 모든 참조를 바꿀 **ApplicationUser** 사용 하 여 **IdentityUser**합니다.
8. 기본 프로젝트 IUser 인터페이스에서 정의 되지 않은 사용자 클래스에서 일부 멤버가 포함 됩니다. 전자 메일, PasswordHash, 등 GenerateUserIdentityAsync 합니다. User 클래스에 이러한 멤버에 없는 경우 구현 하거나 이러한 멤버를 사용 하는 코드를 변경 합니다.
9. RoleManager의 모든 인스턴스를 만든 경우 새 RoleStore 클래스를 사용 하도록 코드를 변경 합니다.  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 기본 프로젝트는 키에 대 한 문자열 값이 있는 사용자 정의 클래스에 대 한 설계 되었습니다. 사용자 클래스 (예: 정수) 키에 대 한 다른 형식이 있으면 형식을 사용 하려면 프로젝트를 변경 해야 합니다. 참조 [ASP.NET Id에서 사용자에 대 한 기본 키 변경](change-primary-key-for-users-in-aspnet-identity.md)합니다.
11. 필요한 경우 연결 문자열을 Web.config 파일에 추가 합니다.

<a id="other"></a>
## <a name="other-resources"></a>기타 리소스

- 블로그: [ASP.NET Id를 구현합니다.](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 자습서 및 GIT 코드: [Simple.Data Asp.Net Id 공급자](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 자습서:[는 기본 Id 계정은 설정 하 고 외부 DB를 가리키면 해당](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)합니다. 하 여 [ @xivSolutions ](https://twitter.com/xivSolutions)합니다.
- 자습서[: 사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [CodeFluent 엔터티](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/) 여 [SoftFluent](http://www.softfluent.com/)
- [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) James randall 합니다.
- Azure Table Storage: [AspNet.Identity.TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) 하 여 [ @stuartleeks ](https://twitter.com/stuartleeks)합니다.
- [CouchDB / Daniel Wertheim 여 Cloudant입니다.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 탄력적 검색[h: 탄력적 Identity](https://github.com/bmbsqd/elastic-identity) Bombsquad AB. 여
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) Jonathan Sheely Jonathan Sheely 여 합니다.
- [NHibernate.AspNet.Identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) Antônio Milesi Bastos 여 합니다.
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) by [@tourismgeek](https://twitter.com/tourismgeek).
- [RavenDB.AspNet.Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) by [ILMServices](http://www.ilmservice.com/).
- Redis: [Redis.AspNet.Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "데이터베이스 먼저" 사용자 저장소에 대 한 EF 코드를 생성할 T4 템플릿: [AspNet.Identity.EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
