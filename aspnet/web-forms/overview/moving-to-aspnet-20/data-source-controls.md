---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 데이터 소스 제어 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 1.x의 DataGrid 제어는 웹 응용 프로그램의 데이터 액세스가 크게 개선되었습니다. 그러나, 그것은 사용자 친화적인 되지 않았습니다....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540222"
---
# <a name="data-source-controls"></a>데이터 소스 제어

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 1.x의 DataGrid 제어는 웹 응용 프로그램의 데이터 액세스가 크게 개선되었습니다. 그러나, 그것은 사용자 친화적인 되지 않았습니다. 여전히 많은 유용한 기능을 얻기 위해 상당한 양의 코드가 필요했습니다. 이러한 1.x의 모든 데이터 액세스 노력의 모델입니다.

ASP.NET 1.x의 DataGrid 제어는 웹 응용 프로그램의 데이터 액세스가 크게 개선되었습니다. 그러나, 그것은 사용자 친화적인 되지 않았습니다. 여전히 많은 유용한 기능을 얻기 위해 상당한 양의 코드가 필요했습니다. 이러한 1.x의 모든 데이터 액세스 노력의 모델입니다.

ASP.NET 2.0은 데이터 원본 컨트롤을 사용하여 부분적으로 이 주소를 처리합니다. ASP.NET 2.0의 데이터 원본 컨트롤은 개발자에게 데이터 검색, 데이터 표시 및 데이터 편집을 위한 선언적 모델을 제공합니다. 데이터 원본 컨트롤의 목적은 해당 데이터의 원본에 관계없이 데이터 바인딩된 컨트롤에 데이터를 일관되게 표현하는 것입니다. ASP.NET 2.0의 데이터 원본 컨트롤의 핵심은 DataSourceControl 추상 클래스입니다. DataSourceControl 클래스는 IDataSource 인터페이스와 IListSource 인터페이스의 기본 구현을 제공하며, 후자는 데이터 원본 컨트롤을 데이터 바인딩 된 컨트롤의 DataSource로 할당하고 (나중에 설명한 새 DataSourceId 속성을 통해) 목록으로 데이터를 노출할 수 있습니다. 데이터 원본 컨트롤의 각 데이터 목록은 DataSourceView 개체로 노출됩니다. DataSourceView 인스턴스에 대한 액세스는 IDataSource 인터페이스에서 제공됩니다. 예를 들어 GetViewNames 메서드는 특정 데이터 원본 컨트롤과 연결된 DataSourceView를 등록할 수 있는 ICollection을 반환하고 GetView 메서드를 사용하면 이름으로 특정 DataSourceView 인스턴스에 액세스할 수 있습니다.

데이터 원본 컨트롤에는 사용자 인터페이스가 없습니다. 선언적 구문을 지원하고 원하는 경우 페이지 상태에 액세스할 수 있도록 서버 컨트롤로 구현됩니다. 데이터 원본 컨트롤은 클라이언트에 HTML 태그를 렌더링하지 않습니다.

> [!NOTE]
> 나중에 살펴보겠습니다.

## <a name="storing-connection-strings"></a>연결 문자열 저장

데이터 원본 컨트롤을 구성하는 방법을 살펴보기 전에 연결 문자열과 관련하여 ASP.NET 2.0의 새로운 기능을 다루어야 합니다. ASP.NET 2.0은 런타임에 동적으로 읽을 수 있는 연결 문자열을 쉽게 저장할 수 있는 구성 파일에 새 섹션을 소개합니다. &lt;연결Strings&gt; 섹션을 사용하면 연결 문자열을 쉽게 저장할 수 있습니다.

아래 코드 조각은 새 연결 문자열을 추가합니다.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;appSettings&gt; &lt;섹션과 마찬가지로 연결문자열&gt; 섹션은 구성 파일의 &lt;system.web&gt; 섹션 외부에 나타납니다.

이 연결 문자열을 사용 하려면 서버 컨트롤의 ConnectionString 특성을 설정할 때 다음 구문을 사용할 수 있습니다.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;연결Strings&gt; 섹션은 중요한 정보가 노출되지 않도록 암호화할 수도 있습니다. 이 기능은 이후 단원에서 다룹니다.

## <a name="caching-data-sources"></a>데이터 원본 캐싱

각 DataSourceControl은 캐싱을 구성하기 위한 네 가지 속성을 제공합니다. 인에이블캐칭, 캐시지속, 캐시익스피어레이션정책 및 캐시키독립성.

## <a name="enablecaching"></a>인에이블캐칭

EnableCaching은 데이터 원본 컨트롤에 대해 캐싱이 활성화되었는지 여부를 결정하는 부울 속성입니다.

## <a name="cacheduration-property"></a>캐시지속 속성

CacheDuration 속성은 캐시가 유효한 상태로 유지되는 시간(초)을 설정합니다. 이 속성을 **0으로** 설정하면 캐시가 명시적으로 무효화될 때까지 유효하게 유지됩니다.

## <a name="cacheexpirationpolicy-property"></a>캐시익기정책 속성

CacheExpirationPolicy 속성은 **절대** 또는 **슬라이딩**으로 설정할 수 있습니다. 절대로 설정하면 데이터가 캐시될 최대 시간이 CacheDuration 속성에서 지정한 초(초)임을 의미합니다. 슬라이딩으로 설정하면 각 작업이 수행될 때 만료 시간이 재설정됩니다.

## <a name="cachekeydependency-property"></a>캐시키리퍼렌디속성

CacheKeyDependncy 속성에 대해 문자열 값을 지정하면 ASP.NET 해당 문자열을 기반으로 새 캐시 종속성을 설정합니다. 이렇게 하면 CacheKeyDependency를 변경하거나 제거하기만 하면 캐시를 명시적으로 무효화할 수 있습니다.

**중요**: 가장이 활성화되어 있고 데이터 원본 및/또는 데이터 콘텐츠에 대한 액세스가 클라이언트 ID를 기반으로 하는 경우 EnableCaching을 False로 설정하여 캐싱을 사용하지 않도록 설정하는 것이 좋습니다. 이 시나리오에서 캐싱을 사용하도록 설정하고 원래 데이터를 요청한 사용자 이외의 사용자가 요청을 발행하는 경우 데이터 원본에 대한 권한 부여가 적용되지 않습니다. 데이터는 단순히 캐시에서 제공됩니다.

## <a name="the-sqldatasource-control"></a>SqlDataSource 컨트롤

SqlDataSource 컨트롤을 사용하면 개발자가 ADO.NET 지원하는 모든 관계형 데이터베이스에 저장된 데이터에 액세스할 수 있습니다. System.Data.SqlClient 공급자를 사용하여 SQL Server 데이터베이스, System.Data.OleDb 공급자, System.Data.Odbc 공급자 또는 System.Data.OracleClient 공급자에 액세스하여 오라클에 액세스할 수 있습니다. 따라서 SqlDataSource는 SQL Server 데이터베이스의 데이터에 액세스하는 데만 사용되는 것이 아닙니다.

SqlDataSource를 사용 하려면 연결 String 속성에 대 한 값을 제공 하 고 SQL 명령 또는 저장 프로시저를 지정 합니다. SqlDataSource 컨트롤은 기본 ADO.NET 아키텍처 작업을 처리합니다. 연결을 열고, 데이터 원본을 쿼리하거나, 저장된 프로시저를 실행하고, 데이터를 반환한 다음, 연결을 닫습니다.

> [!NOTE]
> DataSourceControl 클래스는 자동으로 연결을 닫기 때문에 데이터베이스 연결 누수로 인해 생성된 고객 호출 수를 줄여야 합니다.

아래 코드 코드 조각은 위와 같이 구성 파일에 저장된 연결 문자열을 사용하여 DropDownList 컨트롤을 SqlDataSource 컨트롤에 바인딩합니다.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

위에서 설명한 대로 SqlDataSource의 DataSourceMode 속성은 데이터 원본에 대한 모드를 지정합니다. 위의 예에서 DataSourceMode는 DataReader로 설정됩니다. 이 경우 SqlDataSource는 정방향 전용 및 읽기 전용 커서를 사용하여 IDataReader 개체를 반환합니다. 반환되는 지정된 유형의 개체는 사용되는 공급자에 의해 제어됩니다. 이 경우 web.config 파일의 &lt;연결Strings 섹션에 지정된 대로&gt; System.Data.SqlClient 공급자를 사용하고 있습니다. 따라서 반환되는 개체는 SqlDataReader 형식입니다. DataSet의 DataSourceMode 값을 지정하면 서버의 DataSet에 데이터를 저장할 수 있습니다. 이 모드를 사용하면 정렬, 페이징 등과 같은 기능을 추가할 수 있습니다. SqlDataSource를 GridView 컨트롤에 데이터 바인딩했다면 데이터 집합 모드를 선택했을 것입니다. 그러나 드롭다운리스트의 경우 데이터 리더 모드가 올바른 선택입니다.

> [!NOTE]
> SqlDataSource 또는 AccessDataSource를 캐싱할 때 DataSourceMode 속성을 데이터 집합으로 설정해야 합니다. DataSourceMode의 DataSourceMode를 사용하여 캐싱을 사용하도록 설정하면 예외가 발생합니다.

## <a name="sqldatasource-properties"></a>SqlDataSource 속성

다음은 SqlDataSource 컨트롤의 속성 중 일부입니다.

### <a name="cancelselectonnullparameter"></a>취소선택온Null매개변수

매개 변수 중 하나가 null인 경우 선택 명령이 취소되는지 여부를 지정하는 부울 값입니다. 기본적으로 true입니다.

### <a name="conflictdetection"></a>충돌 감지

여러 사용자가 동시에 데이터 원본을 업데이트할 수 있는 경우 ConflictDetection 속성은 SqlDataSource 컨트롤의 동작을 결정합니다. 이 속성은 충돌옵션 열거형의 값 중 하나를 평가합니다. 이러한 값은 **비교AllValues** 및 **덮어쓰기변경**. Overwrite변경으로 설정된 경우 데이터 원본에 데이터를 작성하는 마지막 사람이 이전 변경 내용을 덮어씁니다. 그러나 충돌 감지 속성이 CompareAllValues로 설정된 경우 SelectCommand에서 반환하는 열에 대해 매개 변수가 만들어지고, SelectCommand가 실행된 이후 값이 변경되었는지 여부를 확인할 수 있도록 해당 각 열의 원래 값을 보유하도록 매개 변수도 만들어집니다.

### <a name="deletecommand"></a>명령 삭제

데이터베이스에서 행을 삭제할 때 사용되는 SQL 문자열을 설정하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="deletecommandtype"></a>삭제명령 유형

SQL 쿼리(Text) 또는 저장 프로시저(저장 프로시저)를 삭제 명령 의 형식을 설정하거나 가져옵니다.

### <a name="deleteparameters"></a>삭제매개 변수

SqlDataSource 컨트롤과 연결된 SqlDataSourceView 개체의 DeleteCommand에서 사용되는 매개 변수를 반환합니다.

### <a name="oldvaluesparameterformatstring"></a>이전 값매개 변수 형식 문자열

이 속성은 ConflictDetection 속성이 CompareAllValues로 설정된 경우 원래 값 매개 변수의 형식을 지정하는 데 사용됩니다. 기본값은 {0} 원래 값 매개 변수가 원래 매개 변수와 동일한 이름을 사용한다는 것을 의미합니다. 즉, 필드 이름이 EmployeeID인 경우 원래 값 매개 @EmployeeID변수는 입니다.

### <a name="selectcommand"></a>SelectCommand

데이터베이스에서 데이터를 검색하는 데 사용되는 SQL 문자열을 설정하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="selectcommandtype"></a>명령 유형 선택

SQL 쿼리(Text) 또는 저장 프로시저(저장 프로시저)를 선택 명령의 형식을 설정하거나 가져옵니다.

### <a name="selectparameters"></a>선택매개 변수

SqlDataSource 컨트롤과 연결된 SqlDataSourceView 개체의 SelectCommand에서 사용하는 매개 변수를 반환합니다.

### <a name="sortparametername"></a>정렬 매개 변수 이름

데이터 원본 컨트롤에서 검색한 데이터를 정렬할 때 사용되는 저장 프로시저 매개 변수의 이름을 가져옵니다. SelectCommandType이 저장프로시프로로 설정된 경우에만 유효합니다.

### <a name="sqlcachedependency"></a>SqlCache 종속성

SQL Server 캐시 종속성에 사용되는 데이터베이스와 테이블을 지정하는 세미 콜론 구분 문자열입니다. (SQL 캐시 종속성은 이후 모듈에서 설명합니다.)

### <a name="updatecommand"></a>업데이트 명령

데이터베이스의 데이터를 업데이트할 때 사용되는 SQL 문자열을 설정하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="updatecommandtype"></a>업데이트 명령 유형

SQL 쿼리(Text) 또는 저장 프로시저(저장 프로시저)를 설정하거나 업데이트 명령 의 형식을 가져옵니다.

### <a name="updateparameters"></a>업데이트매개 변수

SqlDataSource 컨트롤과 연결된 SqlDataSourceView 개체의 UpdateCommand에서 사용하는 매개 변수를 반환합니다.

## <a name="the-accessdatasource-control"></a>액세스 데이터 소스 제어

AccessDataSource 컨트롤은 SqlDataSource 클래스에서 파생되며 Microsoft Access 데이터베이스에 데이터 바인딩에 사용됩니다. AccessDataSource 컨트롤에 대한 연결 String 속성은 읽기 전용 속성입니다. AccessString 속성을 사용하는 대신 DataFile 속성은 아래와 같이 액세스 데이터베이스를 가리키는 데 사용됩니다.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource는 항상 기본 SqlDataSource의 공급자 이름을 System.Data.OleDb로 설정하고 Microsoft.Jet.OLEDB.4.0 OLE DB 공급자를 사용하여 데이터베이스에 연결합니다. AccessDataSource 컨트롤을 사용하여 암호로 보호된 액세스 데이터베이스에 연결할 수 없습니다. 암호로 보호된 데이터베이스에 연결해야 하는 경우 SqlDataSource 컨트롤을 사용해야 합니다.

> [!NOTE]
> 웹 사이트에 저장된 액세스 데이터베이스는 앱\_데이터 디렉터리에 배치해야 합니다. ASP.NET 이 디렉터리에서 파일을 찾아볼 수 없습니다. Access 데이터베이스를 사용할 때 프로세스 계정 읽기 및\_쓰기 권한을 앱 데이터 디렉터리에 부여해야 합니다.

## <a name="the-xmldatasource-control"></a>XmlData소스 제어

XmlDataSource는 XML 데이터를 데이터 바인딩 컨트롤에 데이터 바인딩하는 데 사용됩니다. DataFile 속성을 사용하여 XML 파일에 바인딩하거나 Data 속성을 사용하여 XML 문자열에 바인딩할 수 있습니다. XmlDataSource는 XML 특성을 바인딩 가능한 필드로 노출합니다. 특성으로 표시되지 않는 값에 바인딩해야 하는 경우 XSL 변환을 사용해야 합니다. XPath 식을 사용하여 XML 데이터를 필터링할 수도 있습니다.

다음 XML 파일을 고려하십시오.

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource는 &lt;&gt; *사람/사람의* XPath 속성을 사용하여 사람 노드만 필터링합니다. 그런 다음 드롭다운리스트는 DataTextField 속성을 사용하여 LastName 특성에 데이터 바인딩합니다.

XmlDataSource 컨트롤은 주로 읽기 전용 XML 데이터에 데이터 바인딩에 사용되지만 XML 데이터 파일을 편집할 수 있습니다. 이러한 경우 XML 파일의 정보 자동 삽입, 업데이트 및 삭제는 다른 데이터 원본 컨트롤과 마찬가지로 자동으로 수행되지 않습니다. 대신 XmlDataSource 컨트롤의 다음 방법을 사용하여 데이터를 수동으로 편집하는 코드를 작성해야 합니다.

### <a name="getxmldocument"></a>겟Xml문서

XmlDataSource에서 검색한 XML 코드가 포함된 XmlDocument 개체를 검색합니다.

### <a name="save"></a>저장

인메모리 XmlDocument를 데이터 원본에 다시 저장합니다.

Save 메서드는 다음 두 조건이 충족될 때만 작동한다는 것을 깨닫는 것이 중요합니다.

1. XmlDataSource는 DataFile 속성을 사용하여 데이터 속성 대신 XML 파일에 바인딩하여 메모리 내 XML 데이터에 바인딩합니다.
2. 변환 또는 TransformFile 속성을 통해 변환이 지정되지 않습니다.

또한 Save 메서드는 여러 사용자가 동시에 호출할 때 예기치 않은 결과를 얻을 수 있습니다.

## <a name="the-objectdatasource-control"></a>개체 데이터 소스 컨트롤

지금까지 적용한 데이터 원본 컨트롤은 데이터 원본 컨트롤이 데이터 저장소에 직접 통신하는 2계층 응용 프로그램에 적합합니다. 그러나 많은 실제 응용 프로그램은 데이터 원본 컨트롤이 비즈니스 개체와 통신해야 하는 다중 계층 응용 프로그램으로, 이 응용 프로그램은 데이터 계층과 통신합니다. 이러한 상황에서는 ObjectDataSource가 청구서를 멋지게 채웁니다. ObjectDataSource는 원본 개체와 함께 작동합니다. ObjectDataSource 컨트롤은 원본 개체의 인스턴스를 만들고, 지정된 메서드를 호출하고, 개체에 정적 메서드 대신 인스턴스 메서드가 있는 경우 단일 요청의 범위 내에서 개체 인스턴스를 모두 삭제합니다(Visual Basic에서 공유). 따라서 개체는 상태 비저장이어야 합니다. 즉, 개체는 단일 요청의 범위 내에서 필요한 모든 리소스를 획득하고 해제해야 합니다. ObjectDataSource 컨트롤의 ObjectCreating 이벤트를 처리 하여 소스 개체를 만드는 방법을 제어할 수 있습니다. 소스 개체의 인스턴스를 만든 다음 ObjectDataSourceEventArgs 클래스의 ObjectInstance 속성을 해당 인스턴스로 설정할 수 있습니다. ObjectDataSource 컨트롤은 자체적으로 인스턴스를 만드는 대신 ObjectCreated 이벤트에서 생성된 인스턴스를 사용합니다.

ObjectDataSource 컨트롤의 원본 개체가 데이터를 검색하고 수정하기 위해 호출할 수 있는 공용 정적 메서드(Visual Basic에서 공유)를 노출하는 경우 ObjectDataSource 컨트롤은 해당 메서드를 직접 호출합니다. ObjectDataSource 컨트롤 메서드를 호출 하기 위해 소스 개체의 인스턴스를 만들어야 하는 경우 개체에는 매개 변수를 사용 하지 않는 공용 생성자가 포함 해야 합니다. ObjectDataSource 컨트롤은 소스 개체의 새 인스턴스를 만들 때 이 생성자 호출합니다.

원본 개체에 매개 변수가 없는 공용 생성자가 없는 경우 ObjectCreate 이벤트에서 ObjectDataSource 컨트롤에서 사용할 소스 개체의 인스턴스를 만들 수 있습니다.

## <a name="specifying-object-methods"></a>개체 메서드 지정

ObjectDataSource 컨트롤의 원본 개체에는 데이터를 선택, 삽입, 업데이트 또는 삭제하는 데 사용되는 여러 가지 메서드가 포함될 수 있습니다. 이러한 메서드는 ObjectDataSource 컨트롤의 SelectMethod, InsertMethod, UpdateMethod 또는 DeleteMethod 속성을 사용하여 식별되는 메서드 이름을 기반으로 ObjectDataSource 컨트롤에서 호출됩니다. 소스 개체에는 데이터 원본의 총 개체 수 수를 반환하는 SelectCountMethod 속성을 사용하여 ObjectDataSource 컨트롤에 의해 식별되는 선택적 SelectCount 메서드도 포함될 수 있습니다. ObjectDataSource 컨트롤은 Select 메서드가 호출된 후 페이징 할 때 사용할 데이터 원본의 총 레코드 수를 검색하기 위해 SelectCount 메서드를 호출합니다.

## <a name="lab-using-data-source-controls"></a>데이터 원본 컨트롤을 사용하는 랩

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>연습 1 - SqlDataSource 컨트롤을 사용하여 데이터 표시

다음 연습에서는 SqlDataSource 컨트롤을 사용하여 Northwind 데이터베이스에 연결합니다. SQL Server 2000 인스턴스에서 Northwind 데이터베이스에 액세스할 수 있다고 가정합니다.

1. 새 ASP.NET 웹 사이트 만들기
2. 새 web.config 파일을 추가합니다.

    1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 새 항목 추가를 클릭합니다.
    2. 템플릿 목록에서 웹 구성 파일을 선택하고 추가를 클릭합니다.
3. &lt;다음과 같이 연결&gt; 문자열 섹션을 편집합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 코드 보기로 전환하고 다음과 같이 asp:SqlDataSource &lt;&gt; 컨트롤에 ConnectionString 특성 과 SelectCommand 특성을 추가합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 설계 보기에서 새 GridView 컨트롤을 추가합니다.
6. GridView 작업 메뉴에서 데이터 원본 선택 드롭다운에서 SqlDataSource1을 선택합니다.
7. Default.aspx를 마우스 오른쪽 버튼으로 클릭하고 메뉴에서 브라우저에서 보기를 선택합니다. 저장하라는 메시지가 표시되면 예를 클릭합니다.
8. GridView는 제품 테이블의 데이터를 표시합니다.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>연습 2 - SqlDataSource 컨트롤로 데이터 편집

다음 연습에서는 선언적 구문을 사용하여 DropDownList 컨트롤을 데이터 바인딩하는 방법을 보여 주며 DropDownList 컨트롤에 표시되는 데이터를 편집할 수 있습니다.

1. 설계 보기에서 Default.aspx에서 GridView 컨트롤을 삭제합니다. 

    **중요**: 페이지에 SqlDataSource 컨트롤을 둡니다.
2. 디폴드.aspx에 드롭다운리스트 컨트롤을 추가합니다.
3. 소스 보기로 전환합니다.
4. 다음과 같이 asp:DropDownList &lt;&gt; 컨트롤에 DataSourceId, DataTextField 및 DataValueField 특성을 추가합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default.aspx를 저장하고 브라우저에서 볼 수 있습니다. 드롭다운목록에는 노스윈드 데이터베이스의 모든 제품이 포함되어 있습니다.
6. 브라우저를 닫습니다.
7. Default.aspx의 소스 보기에서 드롭다운리스트 컨트롤 아래에 새 텍스트 상자 컨트롤을 추가합니다. 텍스트 상자의 ID 속성을 txtProductName으로 변경합니다.
8. TextBox 컨트롤에서 새 단추 컨트롤을 추가합니다. 단추의 ID 속성을 btnUpdate로 변경하고 텍스트 속성을 **제품 이름을 업데이트합니다.**
9. Default.aspx의 소스 보기에서 다음과 같이 UpdateCommand 속성과 두 개의 새 UpdateParameters를 SqlDataSource 태그에 추가합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 이 코드에는 두 가지 업데이트 매개 변수(ProductName 및 ProductID)가 추가되어 있습니다. 이러한 매개 변수는 txtProductName 텍스트 상자의 텍스트 속성과 ddlProducts 드롭다운 목록의 SelectedValue 속성에 매핑됩니다.
10. 디자인 보기로 전환하고 Button 컨트롤을 두 번 클릭하여 이벤트 처리기를 추가합니다.
11. btnUpdate\_클릭 코드에 다음 코드를 추가합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx를 마우스 오른쪽 버튼으로 클릭하고 브라우저에서 볼 수 있도록 선택합니다. 모든 변경 내용을 저장하라는 메시지가 표시되면 예를 클릭합니다.
13. ASP.NET 2.0 부분 클래스는 런타임에 컴파일을 허용합니다. 코드 변경 내용이 적용되는지 확인하기 위해 응용 프로그램을 빌드할 필요는 없습니다.
14. 드롭다운 목록에서 제품을 선택합니다.
15. TextBox에서 선택한 제품의 새 이름을 입력한 다음 업데이트 단추를 클릭합니다.
16. 제품 이름이 데이터베이스에서 업데이트됩니다.

## <a name="exercise-3-using-the-objectdatasource-control"></a>연습 3 개체 데이터 소스 컨트롤 사용

이 연습에서는 ObjectDataSource 컨트롤 및 소스 개체를 사용하여 Northwind 데이터베이스와 상호 작용하는 방법을 보여 줍니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 새 항목 추가를 클릭합니다.
2. 템플릿 목록에서 웹 양식을 선택합니다. 이름을 object.aspx로 변경하고 추가를 클릭합니다.
3. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 새 항목 추가를 클릭합니다.
4. 템플릿 목록에서 클래스를 선택합니다. 클래스 이름을 변경하여 NorthwindData.cs 추가를 클릭합니다.
5. 앱\_코드 폴더에 클래스를 추가하라는 메시지가 표시되면 예를 클릭합니다.
6. NorthwindData.cs 파일에 다음 코드를 추가합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. object.aspx의 소스 보기에 다음 코드를 추가합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 모든 파일을 저장하고 object.aspx를 찾아봅금.
9. 세부 정보를 보고, 직원을 편집하고, 직원을 추가하고, 직원을 삭제하여 인터페이스와 상호 작용합니다.
