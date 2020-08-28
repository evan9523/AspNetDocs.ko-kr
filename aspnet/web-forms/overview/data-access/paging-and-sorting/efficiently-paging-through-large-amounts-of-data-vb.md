---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: 많은 양의 데이터를 효율적으로 페이징 (VB) | Microsoft Docs
author: rick-anderson
description: 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션은 기본 데이터 소스 제어 retriev으로 많은 양의 데이터를 사용할 경우 적합 하지 않습니다.
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d1c49e076e1c78e584f91fe2357a98da321f4260
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045106"
---
# <a name="efficiently-paging-through-large-amounts-of-data-vb"></a>대량의 데이터를 효율적으로 페이징(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe) 또는 [PDF 다운로드](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> 데이터의 하위 집합만 표시 되더라도 기본 데이터 원본 컨트롤이 모든 레코드를 검색 하므로 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션은 많은 양의 데이터로 작업할 때 적합 하지 않습니다. 이러한 경우에는 사용자 지정 페이징로 전환 해야 합니다.

## <a name="introduction"></a>소개

위의 자습서에서 설명한 대로 다음 두 가지 방법 중 하나로 페이징을 구현할 수 있습니다.

- **기본 페이징은** 데이터 웹 컨트롤의 스마트 태그에서 페이징 사용 옵션을 선택 하 여 구현할 수 있습니다. 그러나 데이터 페이지를 볼 때마다 ObjectDataSource의 하위 집합만 페이지에 표시 되는 경우에도 ObjectDataSource는 *모든* 레코드를 검색 합니다.
- 사용자 **지정 페이징은** 사용자가 요청한 특정 데이터 페이지에 대해 표시 해야 하는 데이터베이스의 레코드만 검색 하 여 기본 페이징의 성능을 향상 시킵니다. 그러나 사용자 지정 페이징은 기본 페이징 보다 구현 하는 데 약간의 노력이 필요 합니다.

구현 용이성으로 인해 확인란을 선택 하 고 다시 완료 합니다. 기본 페이징은 매력적인 옵션입니다. 그러나 모든 레코드를 검색 하는 naive 접근 방식을 사용 하면 충분히 많은 양의 데이터를 페이징할 때 또는 동시 사용자가 많은 사이트에 대해 집합를 선택할 수 있습니다. 이러한 경우에는 응답성이 뛰어난 시스템을 제공 하기 위해 사용자 지정 페이징 기능을 사용 해야 합니다.

사용자 지정 페이징의 챌린지는 특정 데이터 페이지에 필요한 정확한 레코드 집합을 반환 하는 쿼리를 작성할 수 있는 것입니다. 다행히 Microsoft SQL Server 2005는 결과의 순위를 지정 하는 새 키워드를 제공 하 여 레코드의 적절 한 하위 집합을 효율적으로 검색할 수 있는 쿼리를 작성할 수 있도록 합니다. 이 자습서에서는이 새로운 SQL Server 2005 키워드를 사용 하 여 GridView 컨트롤에서 사용자 지정 페이징을 구현 하는 방법을 알아봅니다. 사용자 지정 페이징에 대 한 사용자 인터페이스는 기본 페이징의 사용자 인터페이스와 동일 하지만, 사용자 지정 페이징을 사용 하 여 한 페이지에서 다음 페이지로의 단계별 실행은 기본 페이징 보다 더 빠른 몇 가지 주문이 될 수 있습니다.

> [!NOTE]
> 사용자 지정 페이징에 의해 표시 되는 정확한 성능 향상은 페이지를 통해 페이징 되는 레코드의 총 수와 데이터베이스 서버에 로드를 배치 하는 위치에 따라 달라 집니다. 이 자습서의 끝 부분에서는 사용자 지정 페이징을 통해 얻은 성능 혜택을 보여 주는 몇 가지 대략적인 메트릭을 살펴보겠습니다.

## <a name="step-1-understanding-the-custom-paging-process"></a>1 단계: 사용자 지정 페이징 프로세스 이해

데이터를 페이징할 때 페이지에 표시 되는 정확한 레코드는 요청 되는 데이터 페이지 및 페이지당 표시 되는 레코드 수에 따라 달라 집니다. 예를 들어, 페이지 당 10 개 제품을 표시 하는 81 제품을 페이지로 이동 하고자 한다고 가정 합니다. 첫 번째 페이지를 볼 때 제품 1 ~ 10 개를 사용할 예정입니다. 두 번째 페이지를 볼 때 제품 11 ~ 20에 관심이 있습니다.

검색 해야 하는 레코드와 페이징 인터페이스를 렌더링 하는 방법을 지정 하는 세 가지 변수가 있습니다.

- **시작 행 인덱스** 표시할 데이터 페이지에 있는 첫 번째 행의 인덱스입니다. 이 인덱스는 페이지 당 표시 되는 레코드와 페이지 인덱스를 곱하여 하나씩 계산할 수 있습니다. 예를 들어, 한 번에 10 개의 레코드를 페이징할 때 첫 번째 페이지 (페이지 인덱스가 0 인 경우)에 대해 시작 행 인덱스는 0 \* 10 + 1 또는 1이 고 두 번째 페이지의 경우 (페이지 인덱스가 1 인 경우) 시작 행 인덱스는 1 \* 10 + 1 또는 11입니다.
- **최대 행** 페이지당 표시할 최대 레코드 수입니다. 이 변수는 마지막 페이지에서 페이지 크기 보다 반환 되는 레코드 수를 줄일 수 있으므로 최대 행 수 라고 합니다. 예를 들어, 페이지당 81 제품 10 레코드를 페이징할 때 아홉 번째 및 마지막 페이지에는 하나의 레코드만 포함 됩니다. 그러나 페이지 없음은 최대 행 수 값 보다 많은 레코드를 표시 합니다.
- **총 레코드 수** -페이징 되는 전체 레코드 수입니다. 이 변수는 지정 된 페이지에 대해 검색할 레코드를 결정 하는 데 필요 하지 않지만 페이징 인터페이스를 지시 합니다. 예를 들어, 페이지를 통해 81 개의 제품이 있는 경우 페이징 인터페이스는 페이징 UI에서 9 개의 페이지 번호를 표시 한다는 것을 알고 있습니다.

기본 페이징을 사용 하면 시작 행 인덱스는 페이지 인덱스의 곱으로 계산 되 고 페이지 크기는 1로 계산 되 고, 최대 행은 단지 페이지 크기입니다. 기본 페이징이 데이터 페이지를 렌더링할 때 데이터베이스에서 모든 레코드를 검색 하기 때문에 각 행에 대 한 인덱스를 알 수 있으므로 시작 행 인덱스 행을 간단한 작업으로 이동할 수 있습니다. 또한 전체 레코드 수는 DataTable의 레코드 수 (또는 데이터베이스 결과를 저장 하는 데 사용 되는 개체)에 불과합니다.

시작 행 인덱스 및 최대 행 수 변수가 지정 된 경우 사용자 지정 페이징 구현은 시작 행 인덱스에서 시작 하 여 레코드의 정확한 하위 집합만 반환 하 고 그 후에는 최대 행 수를 반환 해야 합니다. 사용자 지정 페이징은 다음과 같은 두 가지 문제를 제공 합니다.

- 지정 된 시작 행 인덱스에서 레코드를 반환 하기 시작할 수 있도록 페이지를 통해 전체 데이터의 각 행에 행 인덱스를 효율적으로 연결할 수 있어야 합니다.
- 페이징할 전체 레코드 수를 제공 해야 합니다.

다음 두 단계에서는 이러한 두 가지 문제에 대응 하는 데 필요한 SQL 스크립트를 살펴보겠습니다. SQL 스크립트 외에도 DAL 및 BLL에서 메서드를 구현 해야 합니다.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>2 단계: 페이징할 수 있는 레코드의 총 수 반환

표시 되는 페이지에 대 한 레코드의 정확한 하위 집합을 검색 하는 방법을 살펴보기 전에에서 먼저 페이지를 통해 전체 레코드 수를 반환 하는 방법을 살펴보겠습니다. 이 정보는 페이징 사용자 인터페이스를 올바르게 구성 하기 위해 필요 합니다. 특정 SQL 쿼리에서 반환 되는 총 레코드 수는 [ `COUNT` 집계 함수](https://msdn.microsoft.com/library/ms175997.aspx)를 사용 하 여 가져올 수 있습니다. 예를 들어 테이블의 총 레코드 수를 확인 하기 위해 `Products` 다음 쿼리를 사용할 수 있습니다.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

에서이 정보를 반환 하는 메서드를 DAL에 추가 해 보겠습니다. 특히, `TotalNumberOfProducts()` 위에 표시 된 문을 실행 하는 라는 DAL 메서드를 만듭니다 `SELECT` .

먼저 `Northwind.xsd` 폴더에서 형식화 된 데이터 집합 파일을 엽니다 `App_Code/DAL` . 그런 다음 디자이너에서을 마우스 오른쪽 단추로 클릭 `ProductsTableAdapter` 하 고 쿼리 추가를 선택 합니다. 이전 자습서에서 살펴본 것 처럼이 작업을 수행 하면 DAL에 새 메서드를 추가할 수 있습니다 .이 메서드를 호출 하면 특정 SQL 문 또는 저장 프로시저를 실행 하 게 됩니다. 이전 자습서의 TableAdapter 메서드와 마찬가지로이 경우 임시 SQL 문을 사용 하는 것이 적합 합니다.

![임시 SQL 문 사용](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**그림 1**: 임시 SQL 문 사용

다음 화면에서 만들 쿼리 유형을 지정할 수 있습니다. 이 쿼리는 단일 스칼라 값을 반환 하므로 테이블의 총 레코드 수는 `Products` `SELECT` 단일 값 옵션을 반환 하는를 선택 합니다.

![단일 값을 반환 하는 SELECT 문을 사용 하도록 쿼리를 구성 합니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**그림 2**: 단일 값을 반환 하는 SELECT 문을 사용 하 여 쿼리 구성

사용할 쿼리 유형을 표시 한 후에는 다음 쿼리를 지정 해야 합니다.

![Products의 SELECT COUNT (*) 쿼리 사용](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**그림 3**: PRODUCTS의 SELECT COUNT ( \* ) 쿼리 사용

마지막으로 메서드의 이름을 지정 합니다. 앞서 언급 했 듯이를 사용 하겠습니다 `TotalNumberOfProducts` .

![DAL 방법의 이름을 TotalNumberOfProducts로 합니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**그림 4**: DAL 방법의 이름 TotalNumberOfProducts

마침을 클릭 하면 마법사가 `TotalNumberOfProducts` DAL에 메서드를 추가 합니다. SQL 쿼리의 결과가 인 경우 DAL의 스칼라 반환 메서드는 nullable 형식을 반환 합니다 `NULL` . `COUNT`그러나이 쿼리는 항상 값이 아닌 값을 반환 합니다 `NULL` .이에 관계 없이 DAL 메서드는 nullable 정수를 반환 합니다.

DAL 메서드 외에도 BLL에 메서드가 필요 합니다. `ProductsBLL`클래스 파일을 열고 `TotalNumberOfProducts` 간단히 DAL s 메서드를 호출 하는 메서드를 추가 합니다 `TotalNumberOfProducts` .

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

DAL의 `TotalNumberOfProducts` 메서드는 nullable 정수를 반환 하지만 `ProductsBLL` `TotalNumberOfProducts` 표준 정수를 반환 하도록 클래스의 메서드를 만들었습니다. 따라서 `ProductsBLL` 클래스의 `TotalNumberOfProducts` 메서드는 DAL s 메서드에서 반환한 nullable 정수의 값 부분을 반환 해야 합니다 `TotalNumberOfProducts` . 에 대 한 호출은 `GetValueOrDefault()` null 허용 정수 (있는 경우)의 값을 반환 하 고 null을 허용 하는 경우에는 `null` 기본 정수 값인 0을 반환 합니다.

## <a name="step-3-returning-the-precise-subset-of-records"></a>3 단계: 정확한 레코드 하위 집합 반환

다음 태스크는 앞서 설명한 시작 행 인덱스 및 최대 행 변수를 허용 하 고 적절 한 레코드를 반환 하는 DAL 및 BLL에서 메서드를 만드는 것입니다. 이 작업을 수행 하기 전에 먼저 필요한 SQL 스크립트를 살펴보겠습니다. 이에 대 한 문제는 시작 행 인덱스에서 시작 하는 레코드 (및 최대 레코드 수까지)를 반환할 수 있도록 페이징에서 전체 결과의 각 행에 인덱스를 효율적으로 할당할 수 있어야 한다는 것입니다.

데이터베이스 테이블에 행 인덱스 역할을 하는 열이 이미 있는 경우에는이 작업이 쉽지 않습니다. 처음에는 `Products` `ProductID` 첫 번째 제품이 `ProductID` 1, 두 번째 a 2 등으로 충분 하다 고 생각 하는 것으로 생각할 수 있습니다. 그러나 제품을 삭제 하면 순서 대로 간격이 되돌리고이 접근 방식이 유지 됩니다.

행 인덱스를 페이지의 데이터와 효율적으로 연결 하 여 레코드의 정확한 하위 집합을 검색할 수 있도록 하는 두 가지 일반적인 기술이 있습니다.

- **SQL Server 2005 s `ROW_NUMBER()` 사용 ** SQL Server 2005에 대 한 키워드 new 키워드는 `ROW_NUMBER()` 순서에 따라 반환 된 각 레코드에 순위를 연결 합니다. 이 순위는 각 행에 대 한 행 인덱스로 사용할 수 있습니다.
- **테이블 변수 및 `SET ROWCOUNT` ** SQL Server s [ `SET ROWCOUNT` 문을](https://msdn.microsoft.com/library/ms188774.aspx) 사용 하 여 쿼리를 종료 하기 전에 처리할 총 레코드 수를 지정할 수 있습니다. [테이블 변수](http://www.sqlteam.com/item.asp?ItemID=9454) 는 테이블 형식 데이터를 보유할 수 있는 로컬 t-sql 변수 이며 [임시 테이블과](http://www.sqlteam.com/item.asp?ItemID=2029)유사 합니다. 이 방법은 Microsoft SQL Server 2005 및 SQL Server 2000에서 동일 하 게 작동 `ROW_NUMBER()` 합니다. 단, 방법은 SQL Server 2005 에서만 작동 합니다.  
  
  여기서의 개념은 `IDENTITY` 데이터를 페이징할 테이블의 기본 키에 대 한 열과 열이 있는 테이블 변수를 만드는 것입니다. 그런 다음 데이터가 페이징 되는 테이블의 내용이 테이블 변수에 덤프 되어 `IDENTITY` 테이블의 각 레코드에 대 한 순차적 행 인덱스 (열을 통해)를 연결 합니다. 테이블 변수가 채워지면 `SELECT` 기본 테이블과 조인 된 테이블 변수에 대 한 문을 실행 하 여 특정 레코드를 끌어올 수 있습니다. `SET ROWCOUNT`문을 사용 하 여 테이블 변수로 덤프 해야 하는 레코드 수를 지능적으로 제한할 수 있습니다.  
  
  이 방법의 효율성은 요청 되는 페이지 번호를 기반으로 합니다 .이 값에는 `SET ROWCOUNT` 시작 행 인덱스와 최대 행의 값이 할당 됩니다. 데이터의 처음 몇 페이지와 같이 번호가 낮은 페이지를 페이징할 때이 접근 방식은 매우 효율적입니다. 그러나 끝에 가까운 페이지를 검색 하는 경우 기본 페이징 모양의 성능을 보여 주는 것입니다.

이 자습서에서는 키워드를 사용 하 여 사용자 지정 페이징을 구현 `ROW_NUMBER()` 합니다. 테이블 변수와 기술을 사용 하는 방법에 대 한 자세한 내용은 `SET ROWCOUNT` [많은 결과 집합을 페이징 하는 보다 효율적인 방법](http://www.4guysfromrolla.com/webtech/042606-1.shtml)을 참조 하세요.

`ROW_NUMBER()`다음 구문을 사용 하 여 특정 순서에 대해 반환 된 각 레코드의 순위와 연결 된 키워드입니다.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` 표시 된 순서와 관련 하 여 각 레코드의 순위를 지정 하는 숫자 값을 반환 합니다. 예를 들어 각 제품에 대 한 순위를 가장 비싼 것부터 최소 순으로 표시 하려면 다음 쿼리를 사용할 수 있습니다.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

그림 5에서는 Visual Studio에서 쿼리 창을 통해 실행 하는 경우의 쿼리 결과를 보여 줍니다. 제품은 각 행에 대 한 가격 순위와 함께 가격을 기준으로 정렬 됩니다.

![반환 된 각 레코드에 대해 가격 순위가 포함 됩니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**그림 5**: 반환 되는 각 레코드에 대 한 가격 순위 포함

> [!NOTE]
> `ROW_NUMBER()` 는 SQL Server 2005에서 사용할 수 있는 여러 가지 새로운 순위 함수 중 하나일 뿐입니다. 에 대 한 보다 자세한 설명은 `ROW_NUMBER()` 기타 순위 함수와 함께 [Microsoft SQL Server 2005를 사용 하 여 순위 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml)을 참조 하세요.

절에서 지정 된 열을 기준으로 결과를 순위를 지정 하는 경우 `ORDER BY` `OVER` ( `UnitPrice` 위 예제에서는) SQL Server 결과를 정렬 해야 합니다. 이는 결과가 정렬 되는 열에 대해 클러스터형 인덱스가 있는 경우 또는 포함 하는 인덱스가 있는 경우에는 빠른 작업이 며 그렇지 않은 경우 비용이 더 많이 들 수 있습니다. 충분 한 크기의 쿼리에 대 한 성능 향상을 위해에서 결과의 순서를 지정 하는 열에 대해 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 성능 고려 사항을 자세히 확인 하려면 [SQL Server 2005의 순위 함수 및 성능](http://www.sql-server-performance.com/ak_ranking_functions.asp) 을 참조 하세요.

에서 반환 하는 순위 정보는 `ROW_NUMBER()` 절에서 직접 사용할 수 없습니다 `WHERE` . 그러나 파생 테이블을 사용 하 여 결과를 반환할 수 있으며이는 `ROW_NUMBER()` 절에 나타날 수 있습니다 `WHERE` . 예를 들어 다음 쿼리는 파생 테이블을 사용 하 여 ProductName 및 UnitPrice 열을 결과와 함께 반환한 `ROW_NUMBER()` 다음, 절을 사용 하 여 `WHERE` 가격 등급이 11에서 20 사이인 제품만 반환 합니다.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

이 개념을 조금 더 확장 하면이 방법을 사용 하 여 원하는 시작 행 인덱스 및 최대 행 값이 지정 된 특정 데이터 페이지를 검색할 수 있습니다.

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> 이 자습서의 뒷부분에서 볼 수 있듯이 ObjectDataSource에서 제공 하는는 0부터 시작 하는 *`StartRowIndex`* 반면 `ROW_NUMBER()` SQL Server 2005에서 반환 된 값은 1부터 시작 하 여 인덱싱됩니다. 따라서 절은 `WHERE` `PriceRank` 이 정확히 크고 보다 작거나 같은 레코드를 반환 *`StartRowIndex`* *`StartRowIndex`*  +  *`MaximumRows`* 합니다.

이제 `ROW_NUMBER()` 시작 행 인덱스 및 최대 행 수 값에 따라 특정 데이터 페이지를 검색 하는 데를 사용 하는 방법을 설명 했으므로 이제 DAL 및 BLL의 메서드로이 논리를 구현 해야 합니다.

이 쿼리를 만들 때 결과가 순위를 지정 하는 순서를 결정 해야 합니다. 이름을 기준으로 제품을 사전순으로 정렬 하겠습니다. 즉,이 자습서의 사용자 지정 페이징 구현을 사용 하면 정렬할 수 있는 것 보다 사용자 지정 페이지가 지정 된 보고서를 만들 수 없습니다. 그러나 다음 자습서에서는 이러한 기능을 제공 하는 방법을 살펴보겠습니다.

이전 섹션에서는 DAL 메서드를 임시 SQL 문으로 만들었습니다. 불행 하 게도 TableAdapter 마법사에서 사용 하는 Visual Studio의 T-sql 파서는 `OVER` 함수에서 사용 하는 구문과 동일 하지 `ROW_NUMBER()` 않습니다. 따라서이 DAL 메서드를 저장 프로시저로 만들어야 합니다. 보기 메뉴에서 서버 탐색기를 선택 하거나 Ctrl + Alt + S를 눌러 노드를 확장 `NORTHWND.MDF` 합니다. 새 저장 프로시저를 추가 하려면 저장 프로시저 노드를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가를 선택 합니다 (그림 6 참조).

![제품을 페이징 하기 위한 새 저장 프로시저 추가](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**그림 6**: 제품을 페이징 하기 위한 새 저장 프로시저 추가

이 저장 프로시저는 두 개의 정수 입력 매개 변수를 허용 하 고, `@startRowIndex` `@maximumRows` 필드를 기준으로 정렬 된 함수를 사용 하 여 `ROW_NUMBER()` `ProductName` 지정 된 보다 크고가 보다 작거나 같은 행만 반환 합니다 `@startRowIndex` `@startRowIndex`  +  `@maximumRow` . 새 저장 프로시저에 다음 스크립트를 입력 한 다음 저장 아이콘을 클릭 하 여 데이터베이스에 저장 프로시저를 추가 합니다.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

저장 프로시저를 만든 후 잠시 후에 테스트를 수행 합니다. `GetProductsPaged` 서버 탐색기에서 저장 프로시저 이름을 마우스 오른쪽 단추로 클릭 하 고 실행 옵션을 선택 합니다. 그러면 Visual Studio에서 입력 매개 변수 및 s를 묻는 메시지를 표시 `@startRowIndex` `@maximumRow` 합니다 (그림 7 참조). 다른 값을 시도 하 고 결과를 검사 합니다.

![@startRowIndex및 매개 변수의 값을 입력 합니다. @maximumRows](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>그림 7</strong>: @startRowIndex 및 @maximumRows 매개 변수의 값을 입력 합니다.

이러한 입력 매개 변수 값을 선택 하면 출력 창에 결과가 표시 됩니다. 그림 8에서는 `@startRowIndex` 및 매개 변수에 대해 10을 전달할 때의 결과를 보여 줍니다 `@maximumRows` .

[![데이터의 두 번째 페이지에 표시 되는 레코드가 반환 됩니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**그림 8**: 데이터의 두 번째 페이지에 표시 되는 레코드 반환 ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png))

이 저장 프로시저를 만든 후 메서드를 만들 준비가 되었습니다 `ProductsTableAdapter` . 형식화 된 `Northwind.xsd` 데이터 집합을 열고를 마우스 오른쪽 단추로 클릭 `ProductsTableAdapter` 한 다음 쿼리 추가 옵션을 선택 합니다. 임시 SQL 문을 사용 하 여 쿼리를 만드는 대신 기존 저장 프로시저를 사용 하 여 쿼리를 만듭니다.

![기존 저장 프로시저를 사용 하 여 DAL 메서드 만들기](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**그림 9**: 기존 저장 프로시저를 사용 하 여 DAL 메서드 만들기

그런 다음 호출할 저장 프로시저를 선택 하 라는 메시지가 표시 됩니다. `GetProductsPaged`드롭다운 목록에서 저장 프로시저를 선택 합니다.

![드롭다운 목록에서 Get제품 Sp오래 된 저장 프로시저를 선택 합니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**그림 10**: 드롭다운 목록에서 Get제품 Sp오래 된 저장 프로시저 선택

그런 다음, 다음 화면에서는 저장 프로시저에서 반환 되는 데이터 종류 (표 형식 데이터, 단일 값 또는 값 없음)를 묻는 메시지를 표시 합니다. `GetProductsPaged`저장 프로시저는 여러 레코드를 반환할 수 있으므로 테이블 형식 데이터를 반환 하도록 지정 합니다.

![저장 프로시저에서 테이블 형식 데이터를 반환 함을 나타냄](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**그림 11**: 저장 프로시저에서 테이블 형식 데이터를 반환 함을 나타냄

마지막으로 만들려는 메서드의 이름을 지정 합니다. 이전 자습서와 마찬가지로 계속 해 서 DataTable 채우기 및 DataTable 반환을 모두 사용 하 여 메서드를 만듭니다. 첫 번째 메서드의 이름을로, 두 번째를로 이름을로 `FillPaged` `GetProductsPaged` 합니다.

![메서드 이름 채우기 및 Get제품 Sp에이징됩니다](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**그림 12**: 메서드 이름 채우기-페이징 및 Get제품 sp오래 된 이름

특정 제품 페이지를 반환 하기 위해 DAL 메서드를 만들 뿐 아니라 BLL 에서도 이러한 기능을 제공 해야 합니다. DAL 메서드와 마찬가지로, BLL의 Get제품 Sp오래 된 메서드는 시작 행 인덱스 및 최대 행을 지정 하는 데 두 개의 정수 입력을 허용 해야 하며 지정 된 범위에 속하는 레코드만 반환 해야 합니다. 다음과 같이 ProductsBLL 클래스에 이러한 BLL 메서드를 만들어 DAL s Get제품 Sp오래 된 메서드만 호출 합니다.

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

BLL 메서드의 입력 매개 변수에는 임의의 이름을 사용할 수 있습니다 `startRowIndex` `maximumRows` . 그러나이 메서드를 사용 하도록 ObjectDataSource를 구성 하는 경우 추가 작업을 수행 하 고이를 사용 하도록 선택 하는 것이 곧 표시 될 것입니다.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>4 단계: 사용자 지정 페이징을 사용 하도록 ObjectDataSource 구성

레코드의 특정 하위 집합에 액세스 하기 위한 BLL 및 DAL 메서드를 사용 하 여 사용자 지정 페이징을 사용 하는 기본 레코드를 통해 페이지를 지정 하는 GridView 컨트롤을 만들 준비가 완료 되었습니다. 먼저 `EfficientPaging.aspx` 폴더에서 페이지를 열고 `PagingAndSorting` GridView를 페이지에 추가한 다음 새 ObjectDataSource 컨트롤을 사용 하도록 구성 합니다. 이전 자습서에서는 클래스의 메서드를 사용 하도록 ObjectDataSource를 구성 하는 경우가 많습니다 `ProductsBLL` `GetProducts` . 그러나이 메서드는 `GetProductsPaged` `GetProducts` 데이터베이스의 *모든* 제품을 반환 하는 반면는 `GetProductsPaged` 레코드의 특정 하위 집합만 반환 하기 때문에 메서드를 대신 사용 하려고 합니다.

![ProductsBLL 클래스 s Get제품 Sp오래 된 메서드를 사용 하도록 ObjectDataSource 구성](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**그림 13**: ProductsBLL 클래스 s를 사용 하도록 ObjectDataSource 구성 Get제품 sp오래 된 메서드

읽기 전용 GridView를 다시 만들기 때문에 삽입, 업데이트 및 삭제 탭에서 메서드 드롭다운 목록을 (없음)으로 설정 합니다.

다음으로, ObjectDataSource 마법사는 `GetProductsPaged` 메서드 `startRowIndex` 및 `maximumRows` 입력 매개 변수 값의 소스를 묻는 메시지를 표시 합니다. 이러한 입력 매개 변수는 실제로 GridView에서 자동으로 설정 되므로 소스를 None으로 설정 하 고 마침을 클릭 하기만 하면 됩니다.

![입력 매개 변수 원본을 None으로 유지](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**그림 14**: 입력 매개 변수 원본을 None으로 유지

ObjectDataSource 마법사를 완료 한 후 GridView에는 각 제품 데이터 필드에 대 한 BoundField 또는 CheckBoxField가 포함 됩니다. 적합 하다 고 생각 하는 대로 GridView의 모양을 자유롭게 조정 하세요. `ProductName`,, `CategoryName` `SupplierName` , `QuantityPerUnit` 및 `UnitPrice` BoundFields 표시 하도록 옵트인 했습니다. 또한 해당 스마트 태그에서 페이징 사용 확인란을 선택 하 여 페이징을 지원 하도록 GridView를 구성 합니다. 이러한 변경 후에는 GridView 및 ObjectDataSource 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

그러나 브라우저를 통해 페이지를 방문 하는 경우에는 GridView를 찾을 수 없습니다.

![GridView가 표시 되지 않습니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**그림 15**: GridView가 표시 되지 않습니다.

ObjectDataSource가 현재 `GetProductsPaged` `startRowIndex` 및 입력 매개 변수의 값으로 0을 사용 하 고 있으므로 GridView가 누락 되었습니다 `maximumRows` . 따라서 결과 SQL 쿼리는 레코드를 반환 하지 않으므로 GridView가 표시 되지 않습니다.

이를 해결 하려면 사용자 지정 페이징을 사용 하도록 ObjectDataSource를 구성 해야 합니다. 이 작업은 다음 단계에서 수행할 수 있습니다.

1. **Objectdatasource s 속성을이 `EnablePaging` 속성 `true` 을 설정** 하면 `SelectMethod` 두 개의 추가 매개 변수 (시작 행 인덱스 ()를 지정 하는 매개 변수 [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) 및 최대 행 수를 지정 하는 하나 [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) )에 전달 해야 한다는 것을 나타냅니다.
2. 이에 **따라 ObjectDataSource `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 속성을 설정** 합니다 `StartRowIndexParameterName` `MaximumRowsParameterName` . 및 속성은 `SelectMethod` 사용자 지정 페이징 목적으로에 전달 되는 입력 매개 변수의 이름을 표시 합니다. 기본적으로 이러한 매개 변수 이름은 `startIndexRow` 및입니다 `maximumRows` . 따라서 BLL에서 메서드를 만들 때 `GetProductsPaged` 입력 매개 변수에 대해 이러한 값을 사용 했습니다. 예를 들어 및와 같은 BLL 메서드에 다른 매개 변수 이름을 사용 하도록 선택한 경우에 `GetProductsPaged` `startIndex` `maxRows` 는 ObjectDataSource와 속성을 적절 하 게 설정 해야 `StartRowIndexParameterName` `MaximumRowsParameterName` 합니다 (예:에 대 한 startIndex for `StartRowIndexParameterName` 및 maxRows `MaximumRowsParameterName` ).
3. **ObjectDataSource의 [ `SelectCountMethod` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) 을 페이징 통과 하는 레코드의 총 수를 반환 하는 메서드의 이름으로 설정 `TotalNumberOfProducts` ** 합니다. 즉, 클래스의 `ProductsBLL` 메서드는 `TotalNumberOfProducts` 쿼리를 실행 하는 DAL 메서드를 사용 하 여 페이징 되는 레코드의 총 수를 반환 합니다 `SELECT COUNT(*) FROM Products` . 이 정보는 페이징 인터페이스를 올바르게 렌더링 하기 위해 ObjectDataSource에 필요 합니다.
4. 마법사를 통해 ObjectDataSource를 구성할 때 ** `startRowIndex` `maximumRows` `<asp:Parameter>` objectdatasource s 선언 태그에서 및 요소를 제거** 합니다. 그러면 Visual Studio에서 `<asp:Parameter>` 해당 `GetProductsPaged` 메서드의 입력 매개 변수에 대해 두 개의 요소를 자동으로 추가 합니다. 로 설정 `EnablePaging` 하면 `true` 이러한 매개 변수가 자동으로 전달 됩니다. 선언 구문에도 표시 되는 경우 ObjectDataSource는 메서드에 *4* 개의 매개 변수를 전달 하 고 두 개의 매개 변수를 메서드에 전달 하려고 `GetProductsPaged` `TotalNumberOfProducts` 합니다. 이러한 요소를 제거 하지 않은 경우 `<asp:Parameter>` 브라우저를 통해 페이지를 방문 하면 다음과 같은 오류 메시지가 표시 됩니다. *ObjectDataSource ' ObjectDataSource1 ' 매개 변수를 포함 하는 제네릭이 아닌 ' TotalNumberOfProducts ' 메서드를 찾을 수 없습니다 (Startrowindex, maximumrows*).

이러한 변경을 수행한 후 ObjectDataSource의 선언적 구문은 다음과 같습니다.

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

`EnablePaging`및 `SelectCountMethod` 속성이 설정 되었으며 `<asp:Parameter>` 요소가 제거 되었습니다. 그림 16에는 이러한 변경 내용이 적용 된 후 속성 창의 스크린샷이 나와 있습니다.

![사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤을 구성 합니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**그림 16**: 사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤 구성

이러한 변경을 수행한 후 브라우저를 통해이 페이지를 방문 하세요. 사전순으로 정렬 된 10 개의 제품이 표시 되어야 합니다. 잠시 후에 한 페이지씩 데이터를 단계별로 실행 합니다. 기본 페이징 및 사용자 지정 페이징 간에 최종 사용자의 관점과 시각적 차이가 없지만, 지정 된 페이지에 대해 표시 되어야 하는 레코드를 검색 하기만 하므로 많은 양의 데이터를 사용 하 여 페이지를 더 효율적으로 페이징할 수 있습니다.

[![제품 이름을 기준으로 정렬 된 데이터는 사용자 지정 페이징을 사용 하 여 페이징 됩니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**그림 17**: 제품 이름을 기준으로 정렬 된 데이터는 사용자 지정 페이징 ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png))을 사용 하 여 페이징 됩니다.

> [!NOTE]
> 사용자 지정 페이징을 사용 하 여 ObjectDataSource에서 반환 된 페이지 수 값은 `SelectCountMethod` GridView의 뷰 상태에 저장 됩니다. `PageIndex`,,, 컬렉션 등의 기타 gridview 변수는 `EditIndex` `SelectedIndex` `DataKeys` gridview의 속성 값에 관계 없이 유지 되는 *컨트롤 상태*에 저장 됩니다 `EnableViewState` . `PageCount`뷰 상태를 사용 하 여 다시 게시 간에 값이 유지 되므로 마지막 페이지로 이동 하는 링크를 포함 하는 페이징 인터페이스를 사용 하는 경우 GridView의 뷰 상태를 사용 하도록 설정 해야 합니다. (페이징 인터페이스가 마지막 페이지에 대 한 직접 링크를 포함 하지 않는 경우 보기 상태를 사용 하지 않도록 설정할 수 있습니다.)

마지막 페이지 링크를 클릭 하면 포스트백이 발생 하 고 해당 속성을 업데이트 하도록 GridView에 지시 합니다 `PageIndex` . 마지막 페이지 링크를 클릭 한 경우 GridView는 속성 `PageIndex` 값 보다 작은 값으로 속성을 할당 합니다 `PageCount` . 뷰 상태를 사용 하지 않도록 설정 하면 `PageCount` 다시 게시 간에 값이 손실 되 고에 `PageIndex` 대신 최대 정수 값이 할당 됩니다. 그런 다음 GridView는 및 속성을 곱하여 시작 행 인덱스를 확인 하려고 `PageSize` 합니다 `PageCount` . 그러면 `OverflowException` 제품이 허용 된 최대 정수 크기를 초과 하므로이 발생 합니다.

## <a name="implement-custom-paging-and-sorting"></a>사용자 지정 페이징 및 정렬 구현

현재 사용자 지정 페이징 구현을 위해 저장 프로시저를 만들 때 데이터를 페이징 하는 순서를 정적으로 지정 해야 합니다 `GetProductsPaged` . 그러나 GridView s 스마트 태그에는 페이징 사용 옵션 외에도 정렬 사용 확인란이 포함 되어 있습니다. 아쉽게도 현재 사용자 지정 페이징 구현을 사용 하 여 GridView에 정렬 지원을 추가 하면 현재 표시 된 데이터 페이지의 레코드만 정렬 됩니다. 예를 들어, GridView가 페이징을 지원 하도록 구성 하는 경우 데이터의 첫 페이지를 볼 때 product name을 기준으로 내림차순으로 정렬 하 여 1 페이지에서 제품의 순서를 반대로 바꿉니다. 그림 18에 나와 있는 것 처럼 Carnarvon Tigers는 역순으로 정렬할 때 첫 번째 제품으로 표시 되며,이는 Carnarvon Tigers가 사전순으로 표시 되는 71 다른 제품을 무시 합니다. 첫 번째 페이지의 레코드만 정렬에서 고려 됩니다.

[![현재 페이지에 표시 된 데이터만 정렬 됩니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**그림 18**: 현재 페이지에 표시 된 데이터만 정렬 ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))

정렬은 BLL 메서드에서 데이터를 검색 한 후에 발생 `GetProductsPaged` 하며,이 메서드는 특정 페이지에 대 한 레코드만 반환 하기 때문에 데이터의 현재 페이지에만 적용 됩니다. 정렬을 올바르게 구현 하려면 `GetProductsPaged` 특정 데이터 페이지를 반환 하기 전에 데이터를 적절 하 게 순위를 지정할 수 있도록 정렬 식을 메서드에 전달 해야 합니다. 다음 자습서에서이를 수행 하는 방법을 살펴보겠습니다.

## <a name="implementing-custom-paging-and-deleting"></a>사용자 지정 페이징 및 삭제 구현

사용자 지정 페이징 기술을 사용 하 여 데이터를 페이징 하는 GridView에서 기능을 삭제 하도록 설정 하면 마지막 페이지에서 마지막 레코드를 삭제할 때 gridview가 적절 하 게 감소 하는 것이 아니라 GridView가 사라집니다 `PageIndex` . 이 버그를 재현 하려면 방금 만든 자습서에 대 한 삭제를 사용 하도록 설정 합니다. 마지막 페이지 (9 페이지)로 이동 합니다 .이 페이지에는 81 제품을 페이징 하 고 한 번에 10 개의 제품을 페이징 하므로 단일 제품이 표시 되어야 합니다. 이 제품을 삭제 합니다.

마지막 제품을 삭제 하는 경우 GridView는 여덟 번째 페이지로 *자동으로 이동* 하 고 이러한 기능에는 기본 페이징이 포함 됩니다. 그러나 사용자 지정 페이징을 사용 하면 마지막 페이지에서 마지막 제품을 삭제 한 후 GridView가 화면에서 완전히 사라집니다. 이 문제가 발생 *하는 정확한 이유는* 이 자습서의 범위를 벗어나는 것입니다. 이 문제의 소스에 대 한 하위 수준 세부 정보에 대 한 [사용자 지정 페이징이 있는 GridView에서 마지막 페이지의 마지막 레코드 삭제](http://scottonwriting.net/sowblog/posts/7326.aspx) 를 참조 하세요. 요약 하자면, 삭제 단추를 클릭할 때 GridView에서 수행 하는 일련의 단계는 다음과 같습니다.

1. 레코드 삭제
2. 지정 된 및에 대해 표시할 적절 한 레코드를 가져옵니다. `PageIndex``PageSize`
3. `PageIndex`가 데이터 원본에 있는 데이터 페이지 수를 초과 하지 않는지 확인 합니다 .이 값이 있으면 GridView의 속성을 자동으로 감소 시킵니다. `PageIndex`
4. 2 단계에서 얻은 레코드를 사용 하 여 적절 한 데이터 페이지를 GridView에 바인딩합니다.

이 문제는 2 단계에서 `PageIndex` 표시할 레코드를 검색할 때 사용 된의 경우에 `PageIndex` 만 단지 유일한 레코드가 삭제 된 마지막 페이지의입니다. 따라서 2 단계에서는 데이터의 마지막 페이지에 더 이상 레코드가 포함 되지 않기 때문 *에 레코드가 반환 되지 않습니다.* 그런 다음 3 단계에서 GridView는 `PageIndex` 마지막 페이지의 마지막 레코드를 삭제 하 여 해당 속성이 데이터 소스에 있는 페이지의 총 수보다 큰지 인식 하므로 속성을 감소 시킵니다 `PageIndex` . 4 단계에서 GridView는 2 단계에서 검색 된 데이터에 바인딩을 시도 합니다. 그러나 2 단계에서 레코드가 반환 되지 않았기 때문에 빈 GridView가 생성 됩니다. 2 단계에서는 *모든* 레코드가 데이터 원본에서 검색 되므로 기본 페이징을 사용 하면이 문제는 발생 하지 않습니다.

이 문제를 해결 하기 위해 두 가지 옵션이 있습니다. 첫 번째는 `RowDeleted` 방금 삭제 된 페이지에 표시 된 레코드 수를 결정 하는 GridView s 이벤트 처리기에 대 한 이벤트 처리기를 만드는 것입니다. 레코드가 하나만 있는 경우 방금 삭제 한 레코드는 마지막 레코드이 고 GridView를 감소 시켜야 합니다 `PageIndex` . 물론 `PageIndex` 삭제 작업이 실제로 성공한 경우를 업데이트 하려고 합니다 .이는 속성이 인지 확인 하 여 확인할 수 있습니다 `e.Exception` `null` .

이 방법은 `PageIndex` 1 단계와 2 단계 전에를 업데이트 하기 때문에 작동 합니다. 따라서 2 단계에서는 적절 한 레코드 집합이 반환 됩니다. 이를 수행 하려면 다음과 같은 코드를 사용 합니다.

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

또 다른 해결 방법은 ObjectDataSource s 이벤트에 대 한 이벤트 처리기를 만들고 `RowDeleted` 속성 값을 1로 설정 하는 것입니다 `AffectedRows` . 1 단계에서 레코드를 삭제 한 후 (2 단계에서 데이터를 다시 검색 하기 전) GridView는 `PageIndex` 하나 이상의 행이 작업의 영향을 받은 경우 해당 속성을 업데이트 합니다. 그러나 속성은 `AffectedRows` ObjectDataSource에 의해 설정 되지 않으므로이 단계는 생략 됩니다. 이 단계를 실행 하는 한 가지 방법은 `AffectedRows` 삭제 작업이 성공적으로 완료 된 경우 속성을 수동으로 설정 하는 것입니다. 다음과 같은 코드를 사용 하 여이 작업을 수행할 수 있습니다.

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

이러한 이벤트 처리기에 대 한 코드는 예제의 코드 기반 클래스에서 찾을 수 있습니다 `EfficientPaging.aspx` .

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>기본 페이징 및 사용자 지정 페이징의 성능 비교

사용자 지정 페이징은 필요한 레코드만 검색 하는 반면 기본 페이징은 표시 되는 각 페이지에 대 한 *모든* 레코드를 반환 하는 반면, 사용자 지정 페이징은 기본 페이징 보다 더 효율적 이라는 것을 알 수 있습니다. 그러나 사용자 지정 페이징의 효율성은 얼마 인가요? 기본 페이징을 사용자 지정 페이징으로 이동 하 여 어떤 종류의 성능 향상을 볼 수 있나요?

아쉽게도 모든 답에 맞는 한 가지 크기는 없습니다. 성능 향상은 많은 요인에 따라 달라 지 며, 가장 두드러진 두 가지는 페이징할 수 있는 레코드 수와 데이터베이스 서버에 배치 되는 부하 및 웹 서버와 데이터베이스 서버 간의 통신 채널입니다. 수십 개의 레코드가 포함 된 작은 테이블의 경우 성능 차이는 무시할 수 있습니다. 수천 개에서 수백 개의 행을 포함 하는 큰 테이블의 경우 성능 차이는 음입니다.

[SQL Server 2005를 사용 하는 ASP.NET 2.0의 사용자 지정 페이징이](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)포함 된 문서에는 5만 레코드를 사용 하 여 데이터베이스 테이블을 페이징할 때 이러한 두 페이징 기술 간의 성능 차이를 보이는 몇 가지 성능 테스트가 포함 되어 있습니다. 이러한 테스트에서는 [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)를 사용 하 여 SQL Server 수준에서 쿼리를 실행 하 고 [ASP.NET s 추적 기능](https://msdn.microsoft.com/library/y13fw6we.aspx)을 사용 하는 ASP.NET 페이지에서 쿼리를 실행 하는 시간을 모두 검사 했습니다. 이러한 테스트는 단일 활성 사용자로 개발 상자에서 실행 되었으며 일반적인 웹 사이트 로드 패턴을 모방 하지 unscientific. 상관 없이 결과는 충분 한 양의 데이터로 작업할 때의 기본 및 사용자 지정 페이징에 대 한 실행 시간의 상대적 차이를 보여 줍니다.

|  | **평균 기간 (초)** | **Reads** |
| --- | --- | --- |
| **기본 페이징 SQL 프로파일러** | 1.411 | 383 |
| **사용자 지정 페이징 SQL 프로파일러** | 0.002 | 29 |
| **기본 페이징 ASP.NET 추적** | 2.379 | *해당 사항 없음* |
| **사용자 지정 페이징 ASP.NET 추적** | 0.029 | *해당 사항 없음* |

여기에서 볼 수 있듯이 데이터의 특정 페이지를 검색 하는 데는 평균적으로 평균을 354 하 고 시간을 단축 하 여 완료 해야 합니다. ASP.NET 페이지에서 사용자 지정 페이지는 기본 페이징을 사용 하는 경우 발생 하는 시간<sup>을 1/100 이상으로 렌더링할</sup> 수 있었습니다. 사용자 환경에서 이러한 테스트를 재현 하기 위해 다운로드할 수 있는 코드 및 데이터베이스와 함께 이러한 결과에 대 한 자세한 내용은 [my 문서](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) 를 참조 하세요.

## <a name="summary"></a>요약

기본 페이징은 데이터 웹 컨트롤의 스마트 태그에서 페이징 사용 확인란을 선택 하는 것만을 구현 하는 cinch, 이러한 단순성은 성능 비용으로 제공 됩니다. 기본 페이징을 사용 하는 경우 사용자가 데이터 페이지를 요청 하면 그 중 일부만 표시 될 수 있지만 *모든* 레코드가 반환 됩니다. 이 성능 오버 헤드를 줄이기 위해 ObjectDataSource는 대체 페이징 옵션인 사용자 지정 페이징을 제공 합니다.

사용자 지정 페이징이 표시 되어야 하는 레코드만 검색 하 여 기본 페이징의 성능 문제를 개선 하는 반면, 사용자 지정 페이징을 구현 하는 데 더 많은 관련이 있습니다. 먼저 요청 된 레코드의 특정 하위 집합에 올바르게 액세스 하는 쿼리를 작성 해야 합니다. 여러 가지 방법으로이를 수행할 수 있습니다. 이 자습서에서 검토 한 내용은 SQL Server 2005 s 새 함수를 사용 하 여 `ROW_NUMBER()` 결과의 순위를 지정한 다음 순위가 지정 된 범위 내에 속하는 결과만 반환 하는 것입니다. 또한 페이지를 통해 전체 레코드 수를 확인 하는 수단을 추가 해야 합니다. 이러한 DAL 및 BLL 메서드를 만든 후에는 ObjectDataSource를 구성 하 여 총 레코드 수를 페이징 하는 방법을 결정 하 고 시작 행 인덱스 및 최대 행 값을 BLL에 올바르게 전달할 수 있도록 해야 합니다.

사용자 지정 페이징을 구현 하는 경우에는 몇 가지 단계가 필요 하며 기본 페이징 만큼 간단 하지는 않지만, 사용자 지정 페이징은 충분히 많은 양의 데이터를 페이징할 때 필요 합니다. 결과를 검사 한 결과, 사용자 지정 페이징은 ASP.NET 페이지 렌더링 시간에서 초를 10 배까지 사용할 수 있으며 데이터베이스 서버에 대 한 부하를 한 번 더 더 크게 만들 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. 에 연결할 수 있습니다 [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) 또는의 블로그를 통해 찾을 수 있습니다 [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

> [!div class="step-by-step"]
> [이전](paging-and-sorting-report-data-vb.md)
> [다음](sorting-custom-paged-data-vb.md)
