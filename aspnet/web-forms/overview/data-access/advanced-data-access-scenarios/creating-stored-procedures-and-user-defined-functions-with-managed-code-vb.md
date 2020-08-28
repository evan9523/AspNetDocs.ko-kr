---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: 관리 코드를 사용 하 여 저장 프로시저 및 사용자 정의 함수 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005는 개발자가 관리 코드를 통해 데이터베이스 개체를 만들 수 있도록 .NET 공용 언어 런타임과 통합 됩니다. 이 자습서 ...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 30c37750d89ff3503ead32c0b2a9708b99d785ff
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045288"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>관리 코드를 사용하여 저장 프로시저 및 사용자 정의 함수 만들기(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) 또는 [PDF 다운로드](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005는 개발자가 관리 코드를 통해 데이터베이스 개체를 만들 수 있도록 .NET 공용 언어 런타임과 통합 됩니다. 이 자습서에서는 Visual Basic 또는 c # 코드를 사용 하 여 관리 되는 저장 프로시저 및 관리 되는 사용자 정의 함수를 만드는 방법을 보여 줍니다. 또한 이러한 버전의 Visual Studio를 사용 하 여 이러한 관리 되는 데이터베이스 개체를 디버깅 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

Microsoft s SQL Server 2005 같은 데이터베이스는 데이터 삽입, 수정 및 검색을 위해 [t-sql (구조적 쿼리 언어 transact-sql)](http://en.wikipedia.org/wiki/Transact-SQL) 을 사용 합니다. 대부분의 데이터베이스 시스템은 재사용 가능한 단일 단위로 실행할 수 있는 일련의 SQL 문을 그룹화 하는 구문을 포함 합니다. 저장 프로시저는 한 가지 예입니다. 또 다른 구문은 udf ( *사용자 정의 함수*)로, 9 단계에서 더 자세히 살펴보겠습니다.

기본적으로 SQL은 데이터 집합을 사용할 수 있도록 설계 되었습니다. `SELECT`, `UPDATE` 및 `DELETE` 문은 본질적으로 해당 테이블의 모든 레코드에 적용 되며 해당 절에 의해서만 제한 됩니다 `WHERE` . 그러나 한 번에 하나의 레코드를 사용 하 고 스칼라 데이터를 조작 하기 위해 설계 된 많은 언어 기능이 있습니다. [ `CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) 를 사용 하 여 레코드 집합을 한 번에 하나씩 반복할 수 있습니다. 문자열 조작 함수 `LEFT` 는, `CHARINDEX` 및와 마찬가지로 `PATINDEX` 스칼라 데이터로 작업 합니다. 또한 SQL에는 및와 같은 제어 흐름 문이 포함 되어 있습니다 `IF` `WHILE` .

Microsoft SQL Server 2005 이전에는 저장 프로시저 및 Udf를 T-sql 문의 컬렉션 으로만 정의할 수 있었습니다. 그러나 SQL Server 2005는 모든 .NET 어셈블리에서 사용 되는 런타임 [CLR (공용 언어 런타임)](https://msdn.microsoft.com/netframework/aa497266.aspx)과의 통합을 제공 하도록 설계 되었습니다. 따라서 SQL Server 2005 데이터베이스의 저장 프로시저 및 Udf는 관리 코드를 사용 하 여 만들 수 있습니다. 즉, Visual Basic 클래스에서 메서드로 저장 프로시저나 UDF를 만들 수 있습니다. 이렇게 하면 이러한 저장 프로시저 및 Udf를 사용 하 여 .NET Framework 및 사용자 고유의 사용자 지정 클래스의 기능을 활용할 수 있습니다.

이 자습서에서는 관리 되는 저장 프로시저 및 사용자 정의 함수를 만드는 방법과이를 Northwind 데이터베이스에 통합 하는 방법을 살펴봅니다. S를 시작 하겠습니다.

> [!NOTE]
> 관리 되는 데이터베이스 개체는 해당 SQL 대응에 대 한 몇 가지 이점을 제공 합니다. 언어 풍부 하 고 친숙 하며 기존 코드 및 논리를 다시 사용 하는 기능이 주요 장점입니다. 하지만 관리 되는 데이터베이스 개체는 많은 절차적 논리를 포함 하지 않는 데이터 집합으로 작업할 때 효율성이 떨어질 수 있습니다. 관리 코드를 사용 하는 경우의 이점에 대 한 자세한 논의는 [관리 코드를 사용 하 여 데이터베이스 개체를 만드는 경우의 이점](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)을 참조 하세요.

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>1 단계: Northwind 데이터베이스를 다음으로 이동`App_Data`

지금까지 모든 자습서에서 웹 응용 프로그램 폴더에 Microsoft SQL Server 2005 Express Edition 데이터베이스 파일을 사용 했습니다 `App_Data` . `App_Data`모든 파일은 하나의 디렉터리 내에 있으며 자습서를 테스트 하는 추가 구성 단계가 필요 하지 않으므로 이러한 자습서를 간소화 된 방식으로 배포 하 고 실행할 수 있습니다.

그러나이 자습서에서는를 사용 하 여 Northwind 데이터베이스를 외부로 이동 `App_Data` 하 고 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 명시적으로 등록 합니다. 폴더의 데이터베이스를 사용 하 여이 자습서에 대 한 단계를 수행할 수 있지만 데이터베이스를 `App_Data` SQL Server 2005 Express Edition 데이터베이스 인스턴스에 명시적으로 등록 하면 많은 단계가 훨씬 더 간단 하 게 수행 됩니다.

이 자습서에 대 한 다운로드에는 두 개의 데이터베이스 파일이 `NORTHWND.MDF` 있으며 `NORTHWND_log.LDF` 라는 폴더에 배치 `DataFiles` 됩니다. 자습서의 고유한 구현과 함께 사용 하는 경우 Visual Studio를 닫고 `NORTHWND.MDF` `NORTHWND_log.LDF` 웹 사이트의 `App_Data` 폴더에서 웹 사이트 외부 폴더로 및 파일을 이동 합니다. 데이터베이스 파일을 다른 폴더로 이동한 후에는 Northwind 데이터베이스를 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 등록 해야 합니다. SQL Server Management Studio에서이 작업을 수행할 수 있습니다. 2005 SQL Server Express 버전이 아닌 버전이 컴퓨터에 설치 되어 있는 경우 이미 Management Studio 설치 되어 있을 것입니다. 컴퓨터에 SQL Server 2005 Express Edition만 있는 경우 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)를 다운로드 하 여 설치 합니다.

SQL Server Management Studio를 시작합니다. 그림 1에 나와 있는 것 처럼 Management Studio는 연결할 서버를 요청 하는 것으로 시작 합니다. 서버 이름에 localhost\SQLExpress를 입력 하 고 인증 드롭다운 목록에서 Windows 인증을 선택한 다음 연결을 클릭 합니다.

![적절 한 데이터베이스 인스턴스에 연결 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**그림 1**: 해당 데이터베이스 인스턴스에 연결

연결 되 면 개체 탐색기 창에 해당 데이터베이스, 보안 정보, 관리 옵션 등을 비롯 한 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 대 한 정보가 나열 됩니다.

Northwind 데이터베이스를 `DataFiles` SQL Server 2005 Express Edition 데이터베이스 인스턴스로 폴더 (또는 이동 해야 할 경우)에 연결 해야 합니다. 데이터베이스 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결 옵션을 선택 합니다. 그러면 데이터베이스 연결 대화 상자가 표시 됩니다. 추가 단추를 클릭 하 고 해당 파일을 드릴 다운 `NORTHWND.MDF` 한 다음 확인을 클릭 합니다. 이 시점에서 화면은 그림 2와 유사 하 게 표시 됩니다.

[![적절 한 데이터베이스 인스턴스에 연결 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**그림 2**: 해당 데이터베이스 인스턴스에 연결 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png))

> [!NOTE]
> 데이터베이스 연결 대화 상자를 Management Studio를 통해 SQL Server 2005 Express Edition 인스턴스에 연결할 때 내 문서와 같은 사용자 프로필 디렉터리로 드릴 다운할 수 없습니다. 따라서 `NORTHWND.MDF` 및 `NORTHWND_log.LDF` 파일을 사용자가 작성 하지 않은 프로필 디렉터리에 저장 해야 합니다.

확인 단추를 클릭 하 여 데이터베이스를 연결 합니다. 데이터베이스 연결 대화 상자가 닫히고 개체 탐색기에서 이제 연결 된 데이터베이스를 나열 합니다. Northwind 데이터베이스는와 같은 이름을 가질 가능성이 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` 있습니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 이름 바꾸기를 선택 하 여 데이터베이스 이름을 Northwind로 바꿉니다.

![데이터베이스 이름을 Northwind로 바꿉니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**그림 3**: 데이터베이스를 Northwind로 이름 바꾸기

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>2 단계: Visual Studio에서 새 솔루션 및 SQL Server 프로젝트 만들기

SQL Server 2005에서 관리 되는 저장 프로시저 또는 udf를 만들려면 저장 프로시저 및 UDF 논리를 클래스의 Visual Basic 코드로 작성 합니다. 코드를 작성 한 후에는이 클래스를 어셈블리 (파일)로 컴파일하고 어셈블리를 `.dll` SQL Server 데이터베이스에 등록 한 다음 어셈블리의 해당 메서드를 가리키는 데이터베이스에 저장 프로시저나 UDF 개체를 만들어야 합니다. 이러한 단계는 모두 수동으로 수행할 수 있습니다. 모든 텍스트 편집기에서 코드를 만들고, Visual Basic 컴파일러 ()를 사용 하 여 명령줄에서 컴파일하고, `vbc.exe` 명령을 사용 하 여 데이터베이스에 등록 하거나, Management Studio를 사용 하 여 데이터베이스에 등록 [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) 하 고, 비슷한 방법으로 저장 프로시저 또는 UDF 개체를 추가할 수 있습니다. 다행히 Visual Studio Professional 및 Team Systems 버전에는 이러한 작업을 자동화 하는 SQL Server 프로젝트 형식이 포함 되어 있습니다. 이 자습서에서는 SQL Server 프로젝트 형식을 사용 하 여 관리 되는 저장 프로시저 및 UDF를 만드는 과정을 안내 합니다.

> [!NOTE]
> Visual Studio의 visual Web Developer 또는 Standard edition을 사용 하는 경우에는 수동 방법을 대신 사용 해야 합니다. 13 단계에서는 이러한 단계를 수동으로 수행 하는 방법에 대 한 자세한 지침을 제공 합니다. 이 단계에서는 사용 중인 Visual Studio 버전에 관계 없이 적용 해야 하는 중요 한 SQL Server 구성 지침을 포함 하므로 13 단계를 읽기 전에 2 ~ 12 단계를 읽어야 합니다.

Visual Studio를 열어 시작 합니다. 파일 메뉴에서 새 프로젝트를 선택 하 여 새 프로젝트 대화 상자를 표시 합니다 (그림 4 참조). 데이터베이스 프로젝트 형식으로 드릴 다운 한 다음 오른쪽에 나열 된 템플릿에서 새 SQL Server 프로젝트를 만들도록 선택 합니다. 이 프로젝트의 이름을로 지정 하 `ManagedDatabaseConstructs` 고 라는 솔루션에 배치 하도록 선택 했습니다 `Tutorial75` .

[![새 SQL Server 프로젝트 만들기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**그림 4**: 새 SQL Server 프로젝트 만들기 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))

새 프로젝트 대화 상자에서 확인 단추를 클릭 하 여 솔루션 및 SQL Server 프로젝트를 만듭니다.

SQL Server 프로젝트는 특정 데이터베이스에 연결 됩니다. 따라서 새 SQL Server 프로젝트를 만든 후에는이 정보를 지정 하 라는 메시지가 즉시 표시 됩니다. 그림 5에서는 1 단계에서 다시 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 등록 한 Northwind 데이터베이스를 가리키도록 작성 된 새 데이터베이스 참조 대화 상자를 보여 줍니다.

![SQL Server 프로젝트를 Northwind 데이터베이스에 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**그림 5**: SQL Server 프로젝트를 Northwind 데이터베이스에 연결

이 프로젝트 내에서 만들 관리 되는 저장 프로시저 및 Udf를 디버깅 하려면 연결에 대해 SQL/CLR 디버깅 지원을 사용 하도록 설정 해야 합니다. 그림 5와 같이 SQL Server 프로젝트를 새 데이터베이스와 연결할 때마다 Visual Studio에서 연결에 대해 SQL/CLR 디버깅을 사용 하도록 설정할지 여부를 묻는 메시지를 표시 합니다 (그림 6 참조). 예를 클릭합니다.

![SQL/CLR 디버깅 사용](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**그림 6**: SQL/CLR 디버깅 사용

이제 새 SQL Server 프로젝트가 솔루션에 추가 되었습니다. 이 파일에는 `Test Scripts` `Test.sql` 프로젝트에서 만든 관리 되는 데이터베이스 개체를 디버깅 하는 데 사용 되는 라는 파일이 있는 라는 폴더가 포함 됩니다. 12 단계에서 디버깅을 살펴보겠습니다.

이제 새로운 관리 되는 저장 프로시저 및 Udf를이 프로젝트에 추가할 수 있지만, 먼저 솔루션에 기존 웹 응용 프로그램이 포함 됩니다. 파일 메뉴에서 추가 옵션을 선택 하 고 기존 웹 사이트를 선택 합니다. 해당 웹 사이트 폴더로 이동한 다음 확인을 클릭 합니다. 그림 7에 표시 된 것 처럼이 경우 웹 사이트와 SQL Server 프로젝트의 두 프로젝트를 포함 하도록 솔루션이 업데이트 됩니다 `ManagedDatabaseConstructs` .

![현재 솔루션 탐색기에는 두 개의 프로젝트가 포함 되어 있습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**그림 7**: 이제 솔루션 탐색기에 두 개의 프로젝트가 포함 되어 있습니다.

`NORTHWNDConnectionString`의 값은 `Web.config` 현재 `NORTHWND.MDF` 폴더에 있는 파일을 참조 합니다 `App_Data` . 에서이 데이터베이스를 제거 `App_Data` 하 고 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 명시적으로 등록 했으므로 값을 업데이트 해야 `NORTHWNDConnectionString` 합니다. `Web.config`웹 사이트에서 파일을 열고 `NORTHWNDConnectionString` 연결 문자열이를 읽도록 값을 변경 `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` 합니다. 이 변경 후 `<connectionStrings>` 의 섹션은 다음과 같이 표시 `Web.config` 됩니다.

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> [이전 자습서](debugging-stored-procedures-vb.md)에서 설명한 대로 ASP.NET 웹 사이트와 같은 클라이언트 응용 프로그램에서 SQL Server 개체를 디버깅할 때 연결 풀링을 사용 하지 않도록 설정 해야 합니다. 위에 표시 된 연결 문자열은 연결 풀링을 사용 하지 않도록 설정 `Pooling=false` 합니다 (). ASP.NET 웹 사이트에서 관리 되는 저장 프로시저 및 Udf를 디버깅 하지 않으려는 경우 연결 풀링을 사용 하도록 설정 합니다.

## <a name="step-3-creating-a-managed-stored-procedure"></a>3 단계: 관리 되는 저장 프로시저 만들기

Northwind 데이터베이스에 관리 되는 저장 프로시저를 추가 하려면 먼저 SQL Server 프로젝트에서 메서드로 저장 프로시저를 만들어야 합니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 `ManagedDatabaseConstructs` 하 고 새 항목을 추가 하도록 선택 합니다. 그러면 프로젝트에 추가할 수 있는 관리 되는 데이터베이스 개체의 형식을 나열 하는 새 항목 추가 대화 상자가 표시 됩니다. 그림 8에 나와 있는 것 처럼 여기에는 저장 프로시저 및 사용자 정의 함수가 포함 됩니다.

더 이상 사용 되지 않는 모든 제품을 반환 하는 저장 프로시저를 추가 하 여를 시작 합니다. 새 저장 프로시저 파일의 이름을로 `GetDiscontinuedProducts.vb` 합니다.

[![GetDiscontinuedProducts 라는 새 저장 프로시저를 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**그림 8**: 이름이 인 새 저장 프로시저 추가 `GetDiscontinuedProducts.vb` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png))

그러면 다음 내용이 포함 된 새 Visual Basic 클래스 파일이 생성 됩니다.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

저장 프로시저는 `Shared` 이라는 클래스 파일 내의 메서드로 구현 됩니다 `Partial` `StoredProcedures` . 또한 메서드를 `GetDiscontinuedProducts` 저장 프로시저로 표시 하는 [ `SqlProcedure` 특성](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx)으로 데코 레이트 됩니다.

다음 코드는 개체를 만들고 `SqlCommand` `CommandText` `SELECT` 이 `Products` 필드가 1 인 제품에 대 한 테이블의 모든 열을 반환 하는 쿼리로 설정 합니다 `Discontinued` . 그런 다음 명령을 실행 하 고 결과를 다시 클라이언트 응용 프로그램으로 보냅니다. 메서드에이 코드를 추가 `GetDiscontinuedProducts` 합니다.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

모든 관리 되는 데이터베이스 개체에는 호출자의 컨텍스트를 나타내는 [ `SqlContext` 개체](https://msdn.microsoft.com/library/ms131108.aspx) 에 대 한 액세스 권한이 있습니다. 는 `SqlContext` [ `Pipe` 속성](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)을 통해 [ `SqlPipe` 개체](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) 에 대 한 액세스를 제공 합니다. 이 `SqlPipe` 개체는 SQL Server 데이터베이스와 호출 하는 응용 프로그램 간에 정보를 한쪽 하는 데 사용 됩니다. 이름에서 알 수 있듯이 [ `ExecuteAndSend` 메서드](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) 는 전달 된 개체를 실행 `SqlCommand` 하 고 결과를 클라이언트 응용 프로그램에 다시 보냅니다.

> [!NOTE]
> 관리 되는 데이터베이스 개체는 설정 기반 논리가 아닌 절차적 논리를 사용 하는 저장 프로시저 및 Udf에 가장 적합 합니다. 절차적 논리에는 행 단위로 데이터 집합을 사용 하거나 스칼라 데이터로 작업 하는 작업이 포함 됩니다. `GetDiscontinuedProducts`그러나 방금 만든 메서드는 프로시저 논리를 포함 하지 않습니다. 따라서이는 T-sql 저장 프로시저로 구현 하는 것이 가장 좋습니다. 관리 되는 저장 프로시저를 만들고 배포 하는 데 필요한 단계를 보여 주기 위해 관리 되는 저장 프로시저로 구현 됩니다.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>4 단계: 관리 되는 저장 프로시저 배포

이 코드가 완료 되 면 Northwind 데이터베이스에 배포할 준비가 된 것입니다. SQL Server 프로젝트를 배포 하면 코드를 어셈블리로 컴파일하고, 어셈블리를 데이터베이스에 등록 하 고, 어셈블리의 적절 한 메서드에 연결 하 여 데이터베이스에 해당 개체를 만듭니다. 배포 옵션에 의해 수행 되는 정확한 작업 집합은 13 단계에서 보다 정확 하 게 알 수 있습니다. `ManagedDatabaseConstructs`솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 배포 옵션을 선택 합니다. 그러나 다음 오류로 인해 배포가 실패 합니다. ' EXTERNAL ' 근처의 구문이 잘못 되었습니다. 이 기능을 사용하려면 현재 데이터베이스의 호환성 수준 값을 더 높게 설정해야 합니다. 저장 프로시저에 대 한 도움말을 참조 하세요 `sp_dbcmptlevel` .

이 오류 메시지는 어셈블리를 Northwind 데이터베이스에 등록 하려고 할 때 발생 합니다. SQL Server 2005 데이터베이스에 어셈블리를 등록 하려면 데이터베이스 호환성 수준을 90으로 설정 해야 합니다. 기본적으로 새 SQL Server 2005 데이터베이스의 호환성 수준은 90입니다. 그러나 Microsoft SQL Server 2000를 사용 하 여 만든 데이터베이스의 기본 호환성 수준은 80입니다. Northwind 데이터베이스는 처음에 Microsoft SQL Server 2000 데이터베이스 이므로 호환성 수준이 현재 80로 설정 되어 있으므로 관리 되는 데이터베이스 개체를 등록 하려면 90로 늘려야 합니다.

데이터베이스 호환성 수준을 업데이트 하려면 Management Studio에서 새 쿼리 창을 열고 다음을 입력 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

위의 쿼리를 실행 하려면 도구 모음에서 실행 아이콘을 클릭 합니다.

[![Northwind 데이터베이스 호환성 수준 업데이트](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**그림 9**: Northwind 데이터베이스의 호환성 수준 업데이트 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png))

호환성 수준을 업데이트 한 후 SQL Server 프로젝트를 다시 배포 합니다. 이번에는 배포를 오류 없이 완료 해야 합니다.

SQL Server Management Studio로 돌아가서 개체 탐색기에서 Northwind 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다. 그런 다음 프로그래밍 기능 폴더로 드릴 다운 하 고 어셈블리 폴더를 확장 합니다. 그림 10과 같이 Northwind 데이터베이스에는 이제 프로젝트에 의해 생성 된 어셈블리가 포함 됩니다 `ManagedDatabaseConstructs` .

![이제 ManagedDatabaseConstructs 어셈블리가 Northwind 데이터베이스에 등록 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**그림 10**: `ManagedDatabaseConstructs` 어셈블리가 Northwind 데이터베이스에 등록 되어 있습니다.

또한 저장 프로시저 폴더를 확장 합니다. 라는 이름의 저장 프로시저가 표시 됩니다 `GetDiscontinuedProducts` . 이 저장 프로시저는 배포 프로세스에 의해 생성 되 고 `GetDiscontinuedProducts` 어셈블리의 메서드를 가리킵니다 `ManagedDatabaseConstructs` . `GetDiscontinuedProducts`저장 프로시저를 실행 한 후에는 메서드를 실행 합니다 `GetDiscontinuedProducts` . 이는 관리 되는 저장 프로시저 이므로 Management Studio (따라서 저장 프로시저 이름 옆의 잠금 아이콘)을 통해 편집할 수 없습니다.

![GetDiscontinuedProducts 저장 프로시저는 저장 프로시저 폴더에 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**그림 11**: 저장 `GetDiscontinuedProducts` 프로시저는 저장 프로시저 폴더에 나열 됩니다.

관리 되는 저장 프로시저를 호출 하기 전에 해결 해야 하는 하나 이상의 장애물 있습니다. 데이터베이스는 관리 코드의 실행을 차단 하도록 구성 되어 있습니다. 새 쿼리 창을 열고 저장 프로시저를 실행 하 여이를 확인 `GetDiscontinuedProducts` 합니다. .NET Framework에서 사용자 코드 실행이 사용 하지 않도록 설정 된 다음 오류 메시지가 표시 됩니다. ' Clr 사용 구성 옵션을 사용 하도록 설정 합니다.

Northwind 데이터베이스 구성 정보를 검사 하려면 쿼리 창에 명령을 입력 하 고 실행 합니다 `exec sp_configure` . 이는 현재 clr 사용 설정이 0으로 설정 되어 있음을 보여 줍니다.

[![Clr 사용 설정은 현재 0으로 설정 되어 있습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**그림 12**: Clr 사용 설정이 현재 0으로 설정 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png)).

그림 12의 각 구성 설정에는 최소 및 최대 값과 구성 및 실행 값의 네 가지 값이 나열 됩니다. Clr 사용 설정의 구성 값을 업데이트 하려면 다음 명령을 실행 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

을 다시 실행 하면 `exec sp_configure` 위의 문이 clr enabled 설정의 구성 값을 1로 업데이트 했지만 실행 값은 여전히 0으로 설정 된 것을 알 수 있습니다. 이 구성 변경 내용을 적용 하려면 실행 값을 현재 구성 값으로 설정 하는 [ `RECONFIGURE` 명령을](https://msdn.microsoft.com/library/ms176069.aspx)실행 해야 합니다. 단순히 `RECONFIGURE` 쿼리 창에를 입력 하 고 도구 모음에서 실행 아이콘을 클릭 합니다. 이제를 실행 하 `exec sp_configure` 는 경우 clr 사용 설정의 구성 및 실행 값에 1 값이 표시 됩니다.

Clr 사용 구성이 완료 되 면 관리 되는 저장 프로시저를 실행할 준비가 된 것 `GetDiscontinuedProducts` 입니다. 쿼리 창에서 명령을 입력 하 고 실행 `exec` `GetDiscontinuedProducts` 합니다. 저장 프로시저를 호출 하면 메서드의 해당 관리 코드를 `GetDiscontinuedProducts` 실행할 수 있습니다. 이 코드는 더 이상 지원 `SELECT` 되지 않는 모든 제품을 반환 하는 쿼리를 실행 하 고이 데이터를 호출 하는 응용 프로그램에 반환 합니다 .이는이 인스턴스에 SQL Server Management Studio. 이러한 결과를 수신 하 Management Studio 결과 창에 표시 합니다.

[![GetDiscontinuedProducts 저장 프로시저는 중단 된 모든 제품을 반환 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**그림 13**: 저장 프로시저에서 지원 되지 않는 `GetDiscontinuedProducts` 모든 제품 반환 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>5 단계: 입력 매개 변수를 허용 하는 관리 되는 저장 프로시저 만들기

이러한 자습서에서 만든 많은 쿼리 및 저장 프로시저에는 *매개 변수가*사용 되었습니다. 예를 들어 형식화 된 [데이터 집합에 대 한 새 저장 프로시저 만들기의 tableadapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서에서 `GetProductsByCategoryID` 라는 입력 매개 변수를 수락한 라는 저장 프로시저를 만들었습니다 `@CategoryID` . 그런 다음 저장 프로시저는 `CategoryID` 필드가 제공 된 매개 변수의 값과 일치 하는 모든 제품을 반환 합니다 `@CategoryID` .

입력 매개 변수를 허용 하는 관리 되는 저장 프로시저를 만들려면 메서드 정의에서 해당 매개 변수를 지정 하면 됩니다. 이를 설명 하기 위해 라는 프로젝트에 다른 관리 되는 저장 프로시저를 추가 해 보겠습니다 `ManagedDatabaseConstructs` `GetProductsWithPriceLessThan` . 이 관리 되는 저장 프로시저는 가격을 지정 하는 입력 매개 변수를 수락 하 고 해당 `UnitPrice` 필드가 매개 변수 값 보다 작은 모든 제품을 반환 합니다.

프로젝트에 새 저장 프로시저를 추가 하려면 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 `ManagedDatabaseConstructs` 고 새 저장 프로시저를 추가 하도록 선택 합니다. 파일 이름을 `GetProductsWithPriceLessThan.vb`로 지정합니다. 3 단계에서 살펴본 것 처럼, 클래스 내에 배치 된 이라는 메서드를 사용 하 여 새 Visual Basic 클래스 파일을 만듭니다 `GetProductsWithPriceLessThan` `Partial` `StoredProcedures` .

메서드 정의를 업데이트 하 여 `GetProductsWithPriceLessThan` [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) 라는 입력 매개 변수를 허용 하 `price` 고 코드를 작성 하 여 쿼리 결과를 실행 하 고 반환 합니다.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan`메서드의 정의와 코드는 `GetDiscontinuedProducts` 3 단계에서 만든 메서드의 정의와 코드와 매우 유사 합니다. 유일한 차이점은 `GetProductsWithPriceLessThan` 메서드가 입력 매개 변수 ()로 수락 하 고 `price` , `SqlCommand` 쿼리는 매개 변수 ()를 포함 하며, s `@MaxPrice` 컬렉션에 매개 변수를 추가 하 `SqlCommand` `Parameters` 고 변수 값을 할당 `price` 한다는 것입니다.

이 코드를 추가한 후 SQL Server 프로젝트를 다시 배포 합니다. 그런 다음 SQL Server Management Studio로 돌아가서 저장 프로시저 폴더를 새로 고칩니다. 새 항목인가 표시 되어야 합니다 `GetProductsWithPriceLessThan` . 그림 14에 나와 있는 것 처럼 쿼리 창에서 명령을 입력 하 고 실행 합니다 `exec GetProductsWithPriceLessThan 25` . 그러면 $25 보다 작은 모든 제품이 나열 됩니다.

[![$25 미만의 제품이 표시 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**그림 14**: $25 아래의 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png)).

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>6 단계: 데이터 액세스 계층에서 관리 되는 저장 프로시저 호출

이 시점에서 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 관리 되는 저장 프로시저를 프로젝트에 추가 하 `ManagedDatabaseConstructs` 고 Northwind SQL Server 데이터베이스에 등록 했습니다. 또한 SQL Server Management Studio에서 이러한 관리 되는 저장 프로시저를 호출 했습니다 (그림 13 및 14 참조). 그러나 ASP.NET 응용 프로그램은 이러한 관리 되는 저장 프로시저를 사용 하기 위해 아키텍처의 데이터 액세스 및 비즈니스 논리 계층에 추가 해야 합니다. 이 단계에서는 형식화 된 데이터 `ProductsTableAdapter` `NorthwindWithSprocs` 집합의 [tableadapter 자습서에 대 한 새 저장 프로시저 만들기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 에서 처음에 만든 형식화 된 데이터 집합의에 두 개의 새 메서드를 추가 합니다. 7 단계에서는 해당 하는 메서드를 BLL에 추가 합니다.

`NorthwindWithSprocs`Visual Studio에서 형식화 된 데이터 집합을 열고 라는에 새 메서드를 추가 하 여 시작 `ProductsTableAdapter` `GetDiscontinuedProducts` 합니다. TableAdapter에 새 메서드를 추가 하려면 디자이너에서 TableAdapter s 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 쿼리 추가 옵션을 선택 합니다.

> [!NOTE]
> Northwind 데이터베이스를 `App_Data` 폴더에서 SQL Server 2005 Express Edition 데이터베이스 인스턴스로 이동 했으므로이 변경 내용을 반영 하도록 Web.config의 해당 연결 문자열을 업데이트 해야 합니다. 2 단계에서는의 값을 업데이트 하는 방법에 대해 설명 했습니다 `NORTHWNDConnectionString` `Web.config` . 이 업데이트를 수행 하지 않은 경우 쿼리를 추가 하지 못했습니다 라는 오류 메시지가 표시 됩니다. `NORTHWNDConnectionString` `Web.config` TableAdapter에 새 메서드를 추가 하려고 할 때 대화 상자에서 개체에 대 한 연결을 찾을 수 없습니다. 이 오류를 해결 하려면 확인을 클릭 한 다음로 이동 하 `Web.config` 여 `NORTHWNDConnectionString` 2 단계에서 설명한 대로 값을 업데이트 합니다. 그런 다음 메서드를 TableAdapter에 다시 추가 해 봅니다. 이번에는 오류 없이 작동 해야 합니다.

새 메서드를 추가 하면 이전 자습서에서 여러 번 사용한 TableAdapter 쿼리 구성 마법사가 시작 됩니다. 첫 번째 단계에서는 TableAdapter가 데이터베이스에 액세스 하는 방법을 지정 하 라는 메시지를 표시 합니다. 즉, 임시 SQL 문이나 기존 또는 기존 저장 프로시저를 통해 데이터베이스에 액세스 하는 방법을 지정 합니다. 이미 데이터베이스를 사용 하 여 관리 되는 저장 프로시저를 만들고 등록 했으므로 `GetDiscontinuedProducts` 기존 저장 프로시저 사용 옵션을 선택 하 고 다음을 누릅니다.

[![기존 저장 프로시저 사용 옵션을 선택 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**그림 15**: 기존 저장 프로시저 사용 옵션 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png))

다음 화면에는 메서드가 호출 하는 저장 프로시저에 대 한 메시지가 표시 됩니다. `GetDiscontinuedProducts`드롭다운 목록에서 관리 되는 저장 프로시저를 선택 하 고 다음을 누릅니다.

[![GetDiscontinuedProducts 관리 되는 저장 프로시저를 선택 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**그림 16**: `GetDiscontinuedProducts` 관리 되는 저장 프로시저 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png))

그런 다음 저장 프로시저에서 행, 단일 값 또는 nothing을 반환 하는지 여부를 지정 하 라는 메시지가 표시 됩니다. 는 지원 되지 않는 `GetDiscontinuedProducts` 제품 행 집합을 반환 하므로 첫 번째 옵션 (테이블 형식 데이터)을 선택 하 고 다음을 클릭 합니다.

[![테이블 형식 데이터 옵션 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**그림 17**: 테이블 형식 데이터 옵션 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png))

최종 마법사 화면에서는 사용 된 데이터 액세스 패턴 및 결과 메서드의 이름을 지정할 수 있습니다. 두 확인란을 모두 선택 된 상태로 두고 메서드 및의 이름을로 지정 `FillByDiscontinued` `GetDiscontinuedProducts` 합니다. 마침을 클릭하여 마법사를 완료합니다.

[![메서드의 이름을 FillByDiscontinued 및 GetDiscontinuedProducts로](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**그림 18**: 메서드 이름 `FillByDiscontinued` 및 `GetDiscontinuedProducts` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))

이러한 단계를 반복 하 여 `FillByPriceLessThan` `GetProductsWithPriceLessThan` `ProductsTableAdapter` 관리 되는 저장 프로시저에 대 한 및에 라는 메서드를 만듭니다 `GetProductsWithPriceLessThan` .

그림 19에서는 `ProductsTableAdapter` `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 관리 되는 저장 프로시저에 대 한에 메서드를 추가한 후 데이터 집합 디자이너의 스크린샷을 보여 줍니다.

[![이 단계에서 추가 된 새 메서드가 제품 Stableadapter에 포함 되어 있습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**그림 19**:에는 `ProductsTableAdapter` 이 단계에서 추가 된 새 메서드가 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)).

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>7 단계: 비즈니스 논리 계층에 해당 메서드 추가

4 단계와 5 단계에서 추가 된 관리 되는 저장 프로시저를 호출 하는 메서드를 포함 하도록 데이터 액세스 계층을 업데이트 했으므로 비즈니스 논리 계층에 해당 메서드를 추가 해야 합니다. 클래스에 다음 두 메서드를 추가 합니다 `ProductsBLLWithSprocs` .

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

두 메서드는 모두 해당 DAL 메서드를 호출 하 고 인스턴스를 반환 합니다 `ProductsDataTable` . `DataObjectMethodAttribute`각 메서드 위의 태그를 통해 이러한 메서드는 ObjectDataSource의 데이터 소스 구성 마법사의 선택 탭에 있는 드롭다운 목록에 포함 됩니다.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>8 단계: 프레젠테이션 계층에서 관리 되는 저장 프로시저 호출

및 관리 되는 저장 프로시저를 호출 하는 기능을 포함 하도록 비즈니스 논리 및 데이터 액세스 계층이 확대 된 상태 `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` 에서 이제 ASP.NET 페이지를 통해 이러한 저장 프로시저 결과를 표시할 수 있습니다.

`ManagedFunctionsAndSprocs.aspx`폴더에서 페이지를 열고 `AdvancedDAL` 도구 상자에서 GridView를 디자이너로 끌어 옵니다. GridView의 속성을 `ID` 로 설정 하 `DiscontinuedProducts` 고 스마트 태그에서 라는 새 ObjectDataSource에 바인딩합니다 `DiscontinuedProductsDataSource` . 클래스의 메서드에서 데이터를 가져오도록 ObjectDataSource를 구성 `ProductsBLLWithSprocs` `GetDiscontinuedProducts` 합니다.

[![ProductsBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**그림 20**: 클래스를 사용 하도록 ObjectDataSource 구성 `ProductsBLLWithSprocs` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))

[![선택 탭의 드롭다운 목록에서 GetDiscontinuedProducts 메서드를 선택 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**그림 21**: `GetDiscontinuedProducts` 선택 탭의 드롭다운 목록에서 메서드 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png))

이 표는 제품 정보만 표시 하는 데 사용 되므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 하 고 마침을 클릭 합니다.

마법사가 완료 되 면 Visual Studio는의 각 데이터 필드에 대해 BoundField 또는 CheckBoxField을 자동으로 추가 `ProductsDataTable` 합니다. 및를 제외 하 고 다음 필드를 모두 제거 합니다 `ProductName` `Discontinued` . 이때 GridView와 ObjectDataSource의 선언적 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

잠시 시간을 사용 하 여 브라우저를 통해이 페이지를 봅니다. 페이지를 방문할 때 ObjectDataSource는 클래스의 메서드를 호출 합니다 `ProductsBLLWithSprocs` `GetDiscontinuedProducts` . 7 단계에서 살펴본 것 처럼이 메서드는 저장 프로시저를 호출 하는 DAL s 클래스의 메서드를 호출 합니다 `ProductsDataTable` `GetDiscontinuedProducts` `GetDiscontinuedProducts` . 이 저장 프로시저는 관리 되는 저장 프로시저이 고 3 단계에서 만든 코드를 실행 하 여 단종 된 제품을 반환 합니다.

관리 되는 저장 프로시저에서 반환 되는 결과는 DAL에서로 패키지 된 `ProductsDataTable` 다음 BLL로 반환 됩니다. 그러면 해당 값이 GridView에 바인딩되고 표시 되는 프레젠테이션 계층으로 반환 됩니다. 예상 대로 그리드는 단종 된 제품을 나열 합니다.

[![단종 된 제품이 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**그림 22**: 단종 된 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png)).

추가 연습을 위해 텍스트 상자와 다른 GridView를 페이지에 추가 합니다. 이 GridView에는 클래스의 메서드를 호출 하 여 텍스트 상자에 입력 한 양보다 작은 제품이 표시 되도록 `ProductsBLLWithSprocs` `GetProductsWithPriceLessThan` 합니다.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>9 단계: T-sql Udf 만들기 및 호출

Udf (사용자 정의 함수)는 프로그래밍 언어의 함수 의미 체계를 긴밀 하 게 모방 하는 데이터베이스 개체입니다. Visual Basic 함수와 마찬가지로 Udf는 다양 한 입력 매개 변수를 포함 하 고 특정 형식의 값을 반환할 수 있습니다. UDF는 문자열, 정수 등의 스칼라 데이터 또는 테이블 형식 데이터를 반환할 수 있습니다. 에서는 스칼라 데이터 형식을 반환 하는 UDF에서 시작 하 여 두 가지 유형의 Udf를 간략히 살펴보겠습니다.

다음 UDF는 특정 제품에 대 한 재고의 예상 값을 계산 합니다. 이렇게 하려면 세 개의 입력 매개 변수 ( `UnitPrice` `UnitsInStock` 특정 제품의, 및 값)를 가져와 `Discontinued` 형식의 값을 반환 합니다 `money` . 에를 곱하여 재고의 예상 값을 계산 합니다 `UnitPrice` `UnitsInStock` . 지원 되지 않는 항목의 경우이 값은 반입니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

이 UDF가 데이터베이스에 추가 되 면 프로그래밍 기능 폴더를 확장 하 고 함수를 확장 한 다음 스칼라 값 함수를 확장 하 여 Management Studio를 통해 찾을 수 있습니다. 다음과 같은 쿼리에서 사용할 수 있습니다 `SELECT` .

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

`udf_ComputeInventoryValue`Northwind 데이터베이스에 UDF를 추가 했습니다. 그림 23은 `SELECT` Management Studio를 통해 볼 때 위 쿼리의 출력을 보여 줍니다. 또한 UDF는 개체 탐색기의 스칼라 값 함수 폴더 아래에 나열 됩니다.

[![각 제품의 인벤토리 값이 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**그림 23**: 각 제품의 인벤토리 값이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png)).

Udf는 표 형식 데이터를 반환할 수도 있습니다. 예를 들어 특정 범주에 속하는 제품을 반환 하는 UDF를 만들 수 있습니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID`UDF는 `@CategoryID` 입력 매개 변수를 허용 하 고 지정 된 쿼리 결과를 반환 합니다 `SELECT` . 이 UDF를 만든 후에는 `FROM` 쿼리의 (또는) 절에서이 UDF를 참조할 수 있습니다 `JOIN` `SELECT` . 다음 예에서는 `ProductID` `ProductName` `CategoryID` 각 음료에 대해, 및 값을 반환 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

`udf_GetProductsByCategoryID`Northwind 데이터베이스에 UDF를 추가 했습니다. 그림 24에서는 `SELECT` Management Studio를 통해 볼 때 위의 쿼리 결과를 보여 줍니다. 테이블 형식 데이터를 반환 하는 Udf는 개체 탐색기 s 테이블 값 함수 폴더에서 찾을 수 있습니다.

[![ProductID, ProductName 및 CategoryID는 각 음료에 대해 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**그림 24**: `ProductID` `ProductName` `CategoryID` 각 음료에 대해, 및가 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)).

> [!NOTE]
> Udf를 만들고 사용 하는 방법에 대 한 자세한 내용은 [사용자 정의 함수 소개](http://www.sqlteam.com/item.asp?ItemID=1955)를 참조 하세요. 또한 [사용자 정의 함수의 장점과 단점](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)을 확인 하세요.

## <a name="step-10-creating-a-managed-udf"></a>10 단계: 관리 되는 UDF 만들기

`udf_ComputeInventoryValue` `udf_GetProductsByCategoryID` 위의 예제에서 만든 및 Udf는 t-sql 데이터베이스 개체입니다. SQL Server 2005은 `ManagedDatabaseConstructs` 3 단계와 5 단계에서 관리 되는 저장 프로시저와 마찬가지로 프로젝트에 추가할 수 있는 관리 되는 udf도 지원 합니다. 이 단계에서는 `udf_ComputeInventoryValue` 관리 코드에서 UDF를 구현 해 보겠습니다.

프로젝트에 관리 되는 UDF를 추가 하려면 `ManagedDatabaseConstructs` 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 하도록 선택 합니다. 새 항목 추가 대화 상자에서 사용자 정의 템플릿을 선택 하 고 새 UDF 파일의 이름을 지정 `udf_ComputeInventoryValue_Managed.vb` 합니다.

[![새 관리 되는 UDF를 ManagedDatabaseConstructs 프로젝트에 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**그림 25**: 프로젝트에 새로운 관리 되는 UDF 추가 `ManagedDatabaseConstructs` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))

사용자 정의 함수 템플릿은 `Partial` `UserDefinedFunctions` 이름이 클래스 파일의 이름 (이 인스턴스에서)과 동일한 메서드를 사용 하 여 라는 클래스를 만듭니다 `udf_ComputeInventoryValue_Managed` . 이 메서드는 특성을 사용 하 여 데코 레이트 됩니다 .이 [ `SqlFunction` 특성](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)은 메서드를 관리 되는 UDF로 플래그 합니다.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

`udf_ComputeInventoryValue`메서드는 현재 [ `SqlString` 개체](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) 를 반환 하 고 입력 매개 변수를 허용 하지 않습니다. 3 개의 입력 매개 변수, 및를 허용 하 `UnitPrice` `UnitsInStock` `Discontinued` 고 개체를 반환 하도록 메서드 정의를 업데이트 해야 합니다 `SqlMoney` . 재고 값을 계산 하는 논리는 T-sql UDF의 값과 동일 합니다 `udf_ComputeInventoryValue` .

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

UDF 메서드의 입력 매개 변수는 해당 하는 SQL 형식입니다. `SqlMoney` 필드에 대 한 `UnitPrice` 필드, [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) 의 `UnitsInStock` 및 [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) `Discontinued` 의 경우입니다. 이러한 데이터 형식은 테이블에 정의 된 유형을 반영 합니다 `Products` . `UnitPrice` 열은 형식 `money` , `UnitsInStock` 형식의 열 `smallint` 및 `Discontinued` 형식의 열 `bit` 입니다.

이 코드는 `SqlMoney` 값이 0 인 이라는 인스턴스를 만들어 시작 합니다 `inventoryValue` . `Products`테이블은 `NULL` 및 열의 데이터베이스 값을 허용 `UnitsInPrice` `UnitsInStock` 합니다. 따라서 먼저 `NULL` 개체의 속성을 통해 이러한 값에가 포함 되어 있는지 확인 해야 `SqlMoney` 합니다. [ `IsNull` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx) `UnitPrice`과가 모두 `UnitsInStock` 값을 포함 하지 않는 경우를 `NULL` 두 값 `inventoryValue` 의 곱으로 계산 합니다. 그런 다음 `Discontinued` 이 true 이면 값을 halve 합니다.

> [!NOTE]
> `SqlMoney`개체를 사용 하면 두 개의 `SqlMoney` 인스턴스만 함께 사용할 수 있습니다. `SqlMoney`인스턴스를 리터럴 부동 소수점 숫자로 곱할 수 없습니다. 따라서 halve에는 `inventoryValue` 값이 0.5 인 새 `SqlMoney` 인스턴스와 곱합니다.

## <a name="step-11-deploying-the-managed-udf"></a>11 단계: 관리 되는 UDF 배포

이제 관리 되는 UDF를 만들었으므로 Northwind 데이터베이스에 배포할 준비가 되었습니다. 4 단계에서 살펴본 것 처럼 SQL Server 프로젝트의 관리 되는 개체는 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 배포 옵션을 선택 하 여 배포 됩니다.

프로젝트를 배포한 후 SQL Server Management Studio로 돌아가서 스칼라 반환 함수 폴더를 새로 고칩니다. 이제 두 개의 항목이 표시 됩니다.

- `dbo.udf_ComputeInventoryValue` -9 단계에서 만든 T-sql UDF
- `dbo.udf ComputeInventoryValue_Managed` -방금 배포 된 10 단계에서 만든 관리 되는 UDF.

이 관리 되는 UDF를 테스트 하려면 Management Studio 내에서 다음 쿼리를 실행 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

이 명령은 `udf ComputeInventoryValue_Managed` T-sql UDF 대신 관리 되는 udf `udf_ComputeInventoryValue` 를 사용 하지만 출력은 동일 합니다. 그림 23을 참조 하 여 UDF의 출력에 대 한 스크린샷을 확인 하세요.

## <a name="step-12-debugging-the-managed-database-objects"></a>12 단계: 관리 되는 데이터베이스 개체 디버깅

[저장 프로시저 디버깅](debugging-stored-procedures-vb.md) 자습서에서는 Visual Studio를 통한 SQL Server 디버깅을 위한 세 가지 옵션, 즉 직접 데이터베이스 디버깅, 응용 프로그램 디버깅 및 SQL Server 프로젝트의 디버깅에 대해 설명 했습니다. 관리 되는 데이터베이스 개체는 직접 데이터베이스 디버깅을 통해 디버그할 수 없지만 클라이언트 응용 프로그램에서 디버그 하 고 SQL Server 프로젝트에서 직접 디버그할 수 있습니다. 그러나 디버깅이 작동 하려면 SQL Server 2005 데이터베이스에서 SQL/CLR 디버깅을 허용 해야 합니다. Visual Studio 프로젝트를 처음 만들었을 때 `ManagedDatabaseConstructs` SQL/CLR 디버깅을 사용 하도록 설정할지 묻는 메시지가 표시 됩니다 (2 단계에서 그림 6 참조). 이 설정은 서버 탐색기 창에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여 수정할 수 있습니다.

![데이터베이스에서 SQL/CLR 디버깅을 허용 하는지 확인 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**그림 26**: 데이터베이스에서 SQL/CLR 디버깅을 허용 하는지 확인

관리 되는 저장 프로시저를 디버깅 하려고 한다고 가정 합니다 `GetProductsWithPriceLessThan` . 먼저 메서드의 코드 내에서 중단점을 설정 `GetProductsWithPriceLessThan` 합니다.

[![GetProductsWithPriceLessThan 메서드에 중단점 설정](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**그림 27**: 메서드에서 중단점 설정 `GetProductsWithPriceLessThan` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))

먼저 SQL Server 프로젝트에서 관리 되는 데이터베이스 개체를 디버깅 하는 방법을 살펴보겠습니다. 이 솔루션에는 두 개의 SQL Server 프로젝트가 포함 되어 있습니다 .이 프로젝트는 `ManagedDatabaseConstructs` SQL Server 프로젝트에서 디버그 하기 위해 Visual Studio에서 `ManagedDatabaseConstructs` 디버깅을 시작할 때 SQL Server 프로젝트를 시작 하도록 지시 해야 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 `ManagedDatabaseConstructs` 하 고 상황에 맞는 메뉴에서 시작 프로젝트로 설정 옵션을 선택 합니다.

`ManagedDatabaseConstructs`디버거에서 프로젝트가 시작 되 면 `Test.sql` 폴더에 있는 파일의 SQL 문을 실행 합니다 `Test Scripts` . 예를 들어 `GetProductsWithPriceLessThan` 관리 되는 저장 프로시저를 테스트 하려면 기존 `Test.sql` 파일 내용을 다음 문으로 바꿉니다 .이 문은 `GetProductsWithPriceLessThan` 14.95 값을 전달 하는 관리 되는 저장 프로시저를 호출 합니다 `@CategoryID` .

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

위의 스크립트를에 입력 한 후 `Test.sql` 디버그 메뉴로 이동 하 고 디버깅 시작을 선택 하거나 도구 모음에서 F5 또는 녹색 재생 아이콘을 선택 하 여 디버깅을 시작 합니다. 이렇게 하면 솔루션 내에서 프로젝트가 작성 되 고, 관리 되는 데이터베이스 개체를 Northwind 데이터베이스에 배포한 다음, 스크립트를 실행 `Test.sql` 합니다. 이 시점에서 중단점이 적중 되며 메서드를 단계별로 실행 `GetProductsWithPriceLessThan` 하 고 입력 매개 변수 값을 검사할 수 있습니다.

[![GetProductsWithPriceLessThan 메서드의 중단점이 적중 되었습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**그림 28**: `GetProductsWithPriceLessThan` 메서드의 중단점이 적중 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png)).

클라이언트 응용 프로그램을 통해 SQL database 개체를 디버깅 하려면 응용 프로그램 디버깅을 지원 하도록 데이터베이스를 구성 해야 합니다. 서버 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 응용 프로그램 디버깅 옵션이 선택 되어 있는지 확인 합니다. 또한 SQL 디버거와 통합 하 고 연결 풀링을 사용 하지 않도록 설정 하려면 ASP.NET 응용 프로그램을 구성 해야 합니다. 이러한 단계는 [저장 프로시저 디버깅](debugging-stored-procedures-vb.md) 자습서의 2 단계에 자세히 설명 되어 있습니다.

ASP.NET 응용 프로그램 및 데이터베이스를 구성한 후에는 ASP.NET 웹 사이트를 시작 프로젝트로 설정 하 고 디버깅을 시작 합니다. 중단점을 포함 하는 관리 되는 개체 중 하나를 호출 하는 페이지를 방문 하면 응용 프로그램이 중단 되 고 디버거로 제어가 중단 됩니다. 여기서 그림 28과 같이 코드를 단계별로 실행 하면 됩니다.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>13 단계: 관리 되는 데이터베이스 개체 수동 컴파일 및 배포

SQL Server 프로젝트를 사용 하면 관리 되는 데이터베이스 개체를 쉽게 만들고 컴파일하고 배포할 수 있습니다. 그러나 SQL Server 프로젝트는 Visual Studio Professional 및 Team Systems edition 에서만 사용할 수 있습니다. Visual Studio의 visual Web Developer 또는 Standard Edition을 사용 하 고 관리 되는 데이터베이스 개체를 사용 하려는 경우 수동으로 만들고 배포 해야 합니다. 여기에는 4 단계가 포함 됩니다.

1. 관리 되는 데이터베이스 개체에 대 한 소스 코드를 포함 하는 파일을 만듭니다.
2. 개체를 어셈블리로 컴파일합니다.
3. 어셈블리를 SQL Server 2005 데이터베이스에 등록 합니다.
4. 어셈블리에서 적절 한 메서드를 가리키는 SQL Server 데이터베이스 개체를 만듭니다.

이러한 작업을 설명 하기 위해 `UnitPrice` 가 지정 된 값 보다 큰 제품을 반환 하는 새 관리 되는 저장 프로시저를 만들어 보겠습니다. 컴퓨터에서 라는 새 파일을 만들고 `GetProductsWithPriceGreaterThan.vb` 다음 코드를 파일에 입력 합니다. Visual Studio, 메모장 또는 텍스트 편집기를 사용 하 여이 작업을 수행할 수 있습니다.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

이 코드는 `GetProductsWithPriceLessThan` 5 단계에서 만든 메서드의 코드와 거의 동일 합니다. 유일한 차이점은 메서드 이름, `WHERE` 절 및 쿼리에 사용 되는 매개 변수 이름입니다. `GetProductsWithPriceLessThan`메서드로 돌아가서 `WHERE` 절을 읽습니다 `WHERE UnitPrice < @MaxPrice` . 여기서는를 `GetProductsWithPriceGreaterThan` 사용 `WHERE UnitPrice > @MinPrice` 합니다.

이제이 클래스를 어셈블리로 컴파일해야 합니다. 명령줄에서 파일을 저장 한 디렉터리로 이동 하 `GetProductsWithPriceGreaterThan.vb` 고 c # 컴파일러 ()를 사용 `csc.exe` 하 여 클래스 파일을 어셈블리로 컴파일합니다.

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

시스템에 v가 없는 v가 포함 된 폴더의 경우 `bc.exe` `PATH` 다음과 같이 경로를 완전히 참조 해야 합니다 `%WINDOWS%\Microsoft.NET\Framework\version\` .

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[![GetProductsWithPriceGreaterThan을 어셈블리로 컴파일합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**그림 29**: `GetProductsWithPriceGreaterThan.vb` 어셈블리로 컴파일 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png))

`/t`플래그는 Visual Basic 클래스 파일을 실행 파일이 아닌 DLL로 컴파일하도록 지정 합니다. `/out`플래그는 결과 어셈블리의 이름을 지정 합니다.

> [!NOTE]
> `GetProductsWithPriceGreaterThan.vb`명령줄에서 클래스 파일을 컴파일하는 대신 [Visual Basic Express edition](https://msdn.microsoft.com/vstudio/express/vb/) 을 사용 하거나 Visual Studio Standard edition에서 별도의 클래스 라이브러리 프로젝트를 만들 수도 있습니다. S ren Jacob Lauritsen는 저장 프로시저에 대 한 코드와 `GetProductsWithPriceGreaterThan` 3, 5, 10 단계에서 만든 두 개의 관리 되는 저장 프로시저 및 UDF에 대 한 코드를 포함 하는 Visual Basic Express Edition 프로젝트를 제공 했습니다. S ren s 프로젝트에는 해당 데이터베이스 개체를 추가 하는 데 필요한 T-sql 명령도 포함 되어 있습니다.

코드를 어셈블리로 컴파일하면 어셈블리를 SQL Server 2005 데이터베이스에 등록할 준비가 되었습니다. 이는 T-sql을 통해 명령을 사용 하거나 SQL Server Management Studio을 통해 수행할 수 있습니다 `CREATE ASSEMBLY` . Management Studio 사용에 중점을 둡니다.

Management Studio에서 Northwind 데이터베이스의 프로그래밍 기능 폴더를 확장 합니다. 하위 폴더 중 하나는 어셈블리입니다. 데이터베이스에 새 어셈블리를 수동으로 추가 하려면 어셈블리 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 어셈블리를 선택 합니다. 그러면 새 어셈블리 대화 상자가 표시 됩니다 (그림 30 참조). 찾아보기 단추를 클릭 하 고 `ManuallyCreatedDBObjects.dll` 방금 컴파일한 어셈블리를 선택한 다음 확인을 클릭 하 여 어셈블리를 데이터베이스에 추가 합니다. 개체 탐색기에 어셈블리가 표시 되어서는 안 됩니다 `ManuallyCreatedDBObjects.dll` .

[![ManuallyCreatedDBObjects.dll 어셈블리를 데이터베이스에 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**그림 30**: `ManuallyCreatedDBObjects.dll` 데이터베이스에 어셈블리 추가 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png))

![ManuallyCreatedDBObjects.dll는에 나열 되어 있습니다 개체 탐색기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**그림 31**: `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열 됩니다.

Northwind 데이터베이스에 어셈블리를 추가 하는 동안 저장 프로시저를 `GetProductsWithPriceGreaterThan` 어셈블리의 메서드와 연결 해야 합니다. 이 작업을 수행 하려면 새 쿼리 창을 열고 다음 스크립트를 실행 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

이렇게 하면 라는 Northwind 데이터베이스에 새 저장 프로시저가 생성 되 고이를 관리 되는 `GetProductsWithPriceGreaterThan` 메서드 `GetProductsWithPriceGreaterThan` (어셈블리에 있는 클래스의 `StoredProcedures` )와 연결 `ManuallyCreatedDBObjects` 합니다.

위의 스크립트를 실행 한 후 개체 탐색기에서 저장 프로시저 폴더를 새로 고칩니다. 옆에 잠금 아이콘이 있는 새 저장 프로시저 항목이 표시 됩니다 `GetProductsWithPriceGreaterThan` . 이 저장 프로시저를 테스트 하려면 쿼리 창에서 다음 스크립트를 입력 하 고 실행 합니다.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

그림 32에 나와 있는 것 처럼 위의 명령은 $24.95 보다 큰 제품에 대 한 정보를 표시 합니다 `UnitPrice` .

[![ManuallyCreatedDBObjects.dll는에 나열 되어 있습니다 개체 탐색기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**그림 32**: `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png)).

## <a name="summary"></a>요약

Microsoft SQL Server 2005는 관리 코드를 사용 하 여 데이터베이스 개체를 만들 수 있도록 하는 CLR (공용 언어 런타임)과의 통합을 제공 합니다. 이전에는 T-sql을 사용 해야만 이러한 데이터베이스 개체를 만들 수 있었지만 이제는 Visual Basic 같은 .NET 프로그래밍 언어를 사용 하 여 이러한 개체를 만들 수 있습니다. 이 자습서에서는 두 개의 관리 되는 저장 프로시저와 관리 되는 사용자 정의 함수를 만들었습니다.

Visual Studio s SQL Server 프로젝트 형식은 관리 되는 데이터베이스 개체의 생성, 컴파일 및 배포를 용이 하 게 합니다. 또한 풍부한 디버깅 지원 기능을 제공 합니다. 그러나 SQL Server 프로젝트 형식은 Visual Studio Professional 및 Team Systems edition 에서만 사용할 수 있습니다. Visual Web Developer 또는 Standard Edition For Visual Studio를 사용 하는 경우 13 단계에서 살펴본 것 처럼 생성, 컴파일 및 배포 단계를 수동으로 수행 해야 합니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [사용자 정의 함수의 장점 및 단점](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [관리 코드에서 SQL Server 2005 개체 만들기](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005에서 관리 코드를 사용 하 여 트리거 만들기](http://www.15seconds.com/issue/041006.htm)
- [방법: CLR SQL Server 저장 프로시저 만들기 및 실행](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [방법: CLR SQL Server 사용자 정의 함수 만들기 및 실행](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [방법: `Test.sql` SQL 개체를 실행 하는 스크립트 편집](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [사용자 정의 함수 소개](http://www.sqlteam.com/item.asp?ItemID=1955)
- [관리 코드 및 SQL Server 2005 (비디오)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-sql 참조](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [연습: 관리 코드에서 저장 프로시저 만들기](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. 에 연결할 수 있습니다 [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) 또는의 블로그를 통해 찾을 수 있습니다 [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 S ren Jacob Lauritsen입니다. 이 문서를 검토 하는 것 외에도, S ren는 관리 되는 데이터베이스 개체를 수동으로 컴파일하기 위해이 문서에 포함 된 Visual c # Express Edition 프로젝트를 만들었습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 줄을에 놓습니다 [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](debugging-stored-procedures-vb.md)
