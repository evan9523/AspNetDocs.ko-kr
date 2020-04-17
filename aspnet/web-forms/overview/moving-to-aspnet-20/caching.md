---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 캐싱 | 마이크로 소프트 문서
author: rick-anderson
description: 잘 수행되는 ASP.NET 응용 프로그램에는 캐싱에 대한 이해가 중요합니다. ASP.NET 1.x캐싱에 대한 세 가지 옵션을 제공했습니다. 출력 캐싱,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542939"
---
# <a name="caching"></a>캐싱

[로 마이크로 소프트](https://github.com/microsoft)

> 잘 수행되는 ASP.NET 응용 프로그램에는 캐싱에 대한 이해가 중요합니다. ASP.NET 1.x캐싱에 대한 세 가지 옵션을 제공했습니다. 출력 캐싱, 조각 캐싱 및 캐시 API를 참조하십시오.

잘 수행되는 ASP.NET 응용 프로그램에는 캐싱에 대한 이해가 중요합니다. ASP.NET 1.x캐싱에 대한 세 가지 옵션을 제공했습니다. 출력 캐싱, 조각 캐싱 및 캐시 API를 참조하십시오. ASP.NET 2.0은 이러한 세 가지 방법을 모두 제공하지만 몇 가지 중요한 추가 기능을 추가합니다. 몇 가지 새로운 캐시 종속성이 있으며 개발자는 이제 사용자 지정 캐시 종속성을 만들 수도 있습니다. 캐싱 의 구성도 크게 개선되었습니다 ASP.NET 2.0.

## <a name="new-features"></a>새로운 기능

## <a name="cache-profiles"></a>캐시 프로필

캐시 프로필을 사용하면 개발자가 개별 페이지에 적용할 수 있는 특정 캐시 설정을 정의할 수 있습니다. 예를 들어 12시간 후에 캐시에서 만료되어야 하는 페이지가 있는 경우 해당 페이지에 적용할 수 있는 캐시 프로필을 쉽게 만들 수 있습니다. 새 캐시 프로필을 추가하려면 &lt;구성 파일에서 outputCacheSettings&gt; 섹션을 사용합니다. 예를 들어, 다음은 12시간의 캐시 기간을 구성하는 *2일이라는* 캐시 프로필의 구성입니다.

[!code-xml[Main](caching/samples/sample1.xml)]

이 캐시 프로필을 특정 페이지에 적용하려면 아래와 같이 @OutputCache 지시문의 CacheProfile 특성을 사용합니다.

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>사용자 지정 캐시 종속성

ASP.NET 1.x 개발자는 사용자 지정 캐시 종속성에 대해 외쳤습니다. ASP.NET 1.x에서 CacheDependency 클래스가 봉인되어 개발자가 해당 클래스에서 자신의 클래스를 파생할 수 없게 되었습니다. ASP.NET 2.0에서는 이러한 제한이 제거되고 개발자는 자유롭게 사용자 지정 캐시 종속성을 개발할 수 있습니다. CacheDependency 클래스를 사용하면 파일, 디렉터리 또는 캐시 키를 기반으로 사용자 지정 캐시 종속성을 만들 수 있습니다.

예를 들어 아래 코드는 웹 응용 프로그램의 루트에 있는 stuff.xml이라는 파일을 기반으로 새 사용자 지정 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample3.cs)]

이 시나리오에서는 stuff.xml 파일 변경 하면 캐시 된 항목이 무효화 됩니다.

캐시 키를 사용하여 사용자 지정 캐시 종속성을 만들 수도 있습니다. 이 메서드를 사용 하 여 캐시 키를 제거 하면 캐시된 데이터를 무효화 합니다. 다음 예제에서는 이에 대해 설명합니다.

[!code-csharp[Main](caching/samples/sample4.cs)]

위에 삽입된 항목을 무효화하려면 캐시에 삽입된 항목을 제거하여 캐시 키 역할을 합니다.

[!code-csharp[Main](caching/samples/sample5.cs)]

캐시 키 역할을 하는 항목의 키는 캐시 키 배열에 추가된 값과 같아야 합니다.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>폴링 기반 SQL 캐시 종속성(테이블 기반 종속성이라고도 함)

SQL Server 7 및 2000은 SQL 캐시 종속성에 대한 폴링 기반 모델을 사용합니다. 폴링 기반 모델은 테이블의 데이터가 변경될 때 트리거되는 데이터베이스 테이블의 트리거를 사용합니다. 이 트리거는 ASP.NET 주기적으로 검사하는 알림 테이블의 **changeId** 필드를 업데이트합니다. **변경Id** 필드가 업데이트된 경우 ASP.NET 데이터가 변경되었음을 알고 캐시된 데이터를 무효화합니다.

> [!NOTE]
> SQL Server 2005는 폴링 기반 모델을 사용할 수도 있지만 폴링 기반 모델이 가장 효율적인 모델이 아니므로 SQL Server 2005와 함께 쿼리 기반 모델(나중에 설명)을 사용하는 것이 좋습니다.

폴링 기반 모델을 사용하는 SQL 캐시 종속성이 올바르게 작동하려면 테이블에 알림이 활성화되어 있어야 합니다. 이 작업은 SqlCacheDependencyAdmin 클래스를 사용하거나 aspnet\_regsql.exe 유틸리티를 사용하여 프로그래밍 방식으로 수행할 수 있습니다.

다음 명령줄은 SQL 캐시 종속성에 대한 *dbase라는* SQL Server 인스턴스에 있는 Northwind 데이터베이스의 Products 테이블을 등록합니다.

[!code-console[Main](caching/samples/sample6.cmd)]

다음은 위의 명령에 사용되는 명령줄 스위치에 대한 설명입니다.

| **명령줄 스위치** | **용도** |
| --- | --- |
| -S *server* | 서버 이름을 지정합니다. |
| -에드 | SQL 캐시 종속성에 대해 데이터베이스를 사용하도록 설정해야 함을 지정합니다. |
| -d *\_데이터베이스 이름* | SQL 캐시 종속성에 대해 사용하도록 설정해야 하는 데이터베이스 이름을 지정합니다. |
| -E | 데이터베이스에 연결할 때 aspnet\_regsql을 Windows 인증을 사용해야 한다고 지정합니다. |
| -et | SQL 캐시 종속성에 대 한 데이터베이스 테이블을 사용 하는 지정 합니다. |
| -t *\_테이블 이름* | SQL 캐시 종속성을 사용하도록 사용할 데이터베이스 테이블의 이름을 지정합니다. |

> [!NOTE]
> aspnet\_regsql.exe에 사용할 수 있는 다른 스위치가 있습니다. 전체 목록을 보려면 aspnet\_regsql.exe를 실행하십시오. 명령줄에서.

이 명령을 실행하면 SQL Server 데이터베이스가 다음과 같은 변경 사항을 수행합니다.

- **AspNet\_SqlCacheTablesFor변경 알림** 테이블이 추가됩니다. 이 테이블에는 SQL 캐시 종속성이 활성화된 데이터베이스의 각 테이블에 대해 하나의 행이 포함되어 있습니다.
- 다음 저장 프로시저는 데이터베이스 내부에서 만들어집니다.

| AspNet\_SqlCachePolling저장절차 | AspNet\_SqlCacheTablesForChangeNotification 테이블을 쿼리하고 SQL 캐시 종속성 및 각 테이블에 대한 changeId 값에 대해 활성화된 모든 테이블을 반환합니다. 이 저장된 proc는 데이터가 변경되었는지 여부를 확인하기 위해 폴링에 사용됩니다. |
| --- | --- |
| AspNet\_SqlCache쿼리등록테이블저장절차 | AspNet\_SqlCacheTablesForChangeNotification 테이블을 쿼리하여 SQL 캐시 종속성에 대해 활성화된 모든 테이블을 반환하고 SQL 캐시 종속성에 대해 사용하도록 설정된 모든 테이블을 반환합니다. |
| AspNet\_SqlCache등록테이블저장절차 | 알림 테이블에 필요한 항목을 추가하여 SQL 캐시 종속성에 대한 테이블을 등록하고 트리거를 추가합니다. |
| AspNet\_SqlCacheUn등록 테이블저장절차 | 알림 테이블의 항목을 제거하여 SQL 캐시 종속성에 대한 테이블을 등록 취소하고 트리거를 제거합니다. |
| AspNet\_SqlCacheUpdate변경Id저장절차 | 변경된 테이블에 대한 변경 Id를 증가시켜 알림 테이블을 업데이트합니다. ASP.NET 이 값을 사용하여 데이터가 변경되었는지 확인합니다. 아래에 표시된 대로 이 저장된 proc는 테이블이 활성화될 때 생성된 트리거에 의해 실행됩니다. |

- ** _테이블\_이름_\_AspNet\_SqlCacheNotification\_트리거라는** SQL Server 트리거가 테이블에 대해 만들어집니다. 이 트리거는 테이블에서 삽입, 업데이트 또는 DELETE가 수행될 때 AspNet\_SqlCacheUpdateUpdateId저장 시술을 실행합니다.
- **aspnet\_변경 알림\_수신NotificationOnlyAccess라는** SQL Server 역할이 데이터베이스에 추가됩니다.

**aspnet\_변경\_알림 수신NotificationOnlyAccess** SQL Server 역할에는 AspNet\_SqlCachePolling저장시술에 대한 EXEC 권한이 있습니다. 폴링 모델이 올바르게 작동하려면 프로세스 계정을 aspnet\_변경 알림\_수신NotificationOnlyAccess 역할에 추가해야 합니다. aspnet\_regsql.exe 도구는 당신을 위해이 작업을 수행하지 않습니다.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>폴링 기반 SQL 캐시 종속성 구성

폴링 기반 SQL 캐시 종속성을 구성하는 데 필요한 몇 가지 단계가 있습니다. 첫 번째 단계는 위에서 설명한 대로 데이터베이스와 테이블을 사용하도록 설정하는 것입니다. 해당 단계가 완료되면 구성의 나머지 는 다음과 같습니다.

- ASP.NET 구성 파일 구성.
- SqlCache 종속성 구성

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET 구성 파일 구성

이전 모듈에서 설명한 대로 연결 문자열을 추가하는 것 외에도 &lt;&gt; 아래와 &lt;같이 sqlCacheDependency&gt; 요소를 사용하여 캐시 요소를 구성해야 합니다.

[!code-xml[Main](caching/samples/sample7.xml)]

이 구성을 사용하면 pubs 데이터베이스에 대한 SQL 캐시 종속성을 사용할 수 *있습니다.* &lt;sqlCacheDependency&gt; 요소의 pollTime 특성은 기본적으로 60000밀리초 또는 1분입니다. 이 값은 500밀리초 미만일 수 없습니다. 이 예제에서 &lt;추가&gt; 요소는 새 데이터베이스를 추가하고 pollTime을 재정의하여 9000000밀리초로 설정합니다.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCache 종속성 구성

다음 단계는 SqlCacheDependency를 구성하는 것입니다. 이를 수행하는 가장 쉬운 방법은 @ Outcache 지시문에서 SqlDependency 특성에 대한 값을 다음과 같이 지정하는 것입니다.

[!code-aspx[Main](caching/samples/sample8.aspx)]

위의 @ OutputCache 지시문에서 SQL 캐시 종속성은 *pubs* 데이터베이스의 *작성자* 테이블에 대해 구성됩니다. 다음과 같이 세미콜론으로 구분하여 여러 종속성을 구성할 수 있습니다.

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency를 구성하는 또 다른 방법은 프로그래밍 방식으로 구성하는 것입니다. 다음 코드는 *pubs* 데이터베이스의 *작성자* 테이블에 새 SQL 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL 캐시 종속성을 프로그래밍 방식으로 정의할 때의 이점 중 하나는 발생할 수 있는 모든 예외를 처리할 수 있다는 것입니다. 예를 들어 알림에 대해 활성화되지 않은 데이터베이스에 대한 SQL 캐시 종속성을 정의하려고 하면 **DatabaseNotEnabledForNotificationException** 예외가 throw됩니다. 이 경우 **SqlCacheDependencyAdmin.EnableNotifications** 메서드를 호출하고 데이터베이스 이름을 전달하여 알림에 대한 데이터베이스를 사용하도록 설정할 수 있습니다.

마찬가지로 알림에 대해 활성화되지 않은 테이블에 대한 SQL 캐시 종속성을 정의하려고 하면 **TableNotEnabledForNotificationException이** throw됩니다. 그런 다음 **SqlCacheDependencyAdmin.EnableTableForNotifications** 메서드를 호출하여 데이터베이스 이름과 테이블 이름을 전달할 수 있습니다.

다음 코드 샘플에서는 SQL 캐시 종속성을 구성할 때 예외 처리를 올바르게 구성하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample11.cs)]

추가 정보:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>쿼리 기반 SQL 캐시 종속성(SQL Server 2005에만)

SQL Cache 종속성에 SQL Server 2005를 사용하는 경우 폴링 기반 모델이 필요하지 않습니다. SQL Server 2005와 함께 사용할 경우 SQL 캐시 종속성은 SQL Server 2005 쿼리 알림을 사용하여 SQL Server 인스턴스에 대한 SQL 연결을 통해 직접 통신합니다(추가 구성은 필요하지 않습니다).

쿼리 기반 알림을 활성화하는 가장 간단한 방법은 데이터 원본 개체의 **SqlCacheDependency** 특성을 **CommandNotification로** 설정하고 **EnableCaching** 특성을 **true로**설정하여 선언적으로 설정하는 것입니다. 이 메서드를 사용 하 여 코드가 필요 하지 않습니다. 데이터 원본에 대해 실행된 명령의 결과가 변경되면 캐시 데이터가 무효화됩니다.

다음 예제는 SQL 캐시 종속성에 대 한 데이터 원본 컨트롤을 구성 합니다.

[!code-aspx[Main](caching/samples/sample12.aspx)]

이 경우 **SelectCommand에** 지정된 쿼리가 원래와 다른 결과를 반환하면 캐시된 결과가 무효화됩니다.

**@OutputCache** 지시문의 **SqlDependency** 특성을 **CommandNotification**로 설정하여 모든 데이터 원본을 SQL 캐시 종속성에 사용하도록 지정할 수도 있습니다. 아래 예제에서는 이를 보여 줍니다.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005의 쿼리 알림에 대한 자세한 내용은 SQL Server 온라인 책을 참조하십시오.

쿼리 기반 SQL 캐시 종속성을 구성하는 또 다른 방법은 SqlCacheDependency 클래스를 사용하여 프로그래밍 방식으로 구성하는 것입니다. 다음 코드 샘플에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample14.cs)]

추가 정보:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>사후 캐시 대체

페이지를 캐싱하면 웹 응용 프로그램의 성능이 크게 향상될 수 있습니다. 그러나 경우에 따라 대부분의 페이지를 캐시해야 하고 페이지 내의 일부 조각이 동적이어야 합니다. 예를 들어 설정된 기간 동안 완전히 정적인 뉴스 기사 페이지를 만드는 경우 전체 페이지를 캐시하도록 설정할 수 있습니다. 모든 페이지 요청에 변경된 회전 광고 배너를 포함하려면 광고가 포함된 페이지 부분이 동적이어야 합니다. 페이지를 캐시하지만 일부 콘텐츠를 동적으로 대체할 수 있도록 캐시 후 대체 ASP.NET 사용할 수 있습니다. 캐시 후 대체를 사용하면 전체 페이지가 캐싱에서 제외된 것으로 표시된 특정 부분으로 캐시됩니다. 광고 배너의 예에서 AdRotator 컨트롤을 사용하면 캐시 후 대체를 활용하여 각 사용자와 각 페이지를 새로 고칠 때마다 광고가 동적으로 생성되도록 할 수 있습니다.

캐시 후 대체를 구현하는 방법에는 세 가지가 있습니다.

- 선언적으로 대체 컨트롤을 사용 합니다.
- 프로그래밍 방식으로 대체 제어 API를 사용합니다.
- 암시적으로, AdRotatator 컨트롤을 사용 하 여.

### <a name="substitution-control"></a>대체 제어

ASP.NET 대체 제어는 캐시되지 않고 동적으로 생성된 캐시된 페이지의 섹션을 지정합니다. 동적 콘텐츠를 표시할 페이지의 위치에 대체 컨트롤을 배치합니다. 런타임에 대체 제어는 MethodName 속성을 사용하여 지정하는 메서드를 호출합니다. 메서드는 문자열을 반환해야 하며 대체 컨트롤의 내용을 대체합니다. 메서드는 포함 된 Page 또는 UserControl 컨트롤에 정적 메서드여야 합니다. 대체 제어를 사용하면 클라이언트 측 캐시 가능성이 서버 캐시 가능성으로 변경되어 페이지가 클라이언트에 캐시되지 않습니다. 이렇게 하면 페이지에 대한 이후 요청이 메서드를 호출하여 동적 콘텐츠를 생성할 수 있습니다.

### <a name="substitution-api"></a>대체 API

프로그래밍 방식으로 캐시된 페이지에 대한 동적 콘텐츠를 만들려면 페이지 코드에서 [WriteSubstittion](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) 메서드를 호출하여 메서드 이름을 매개 변수로 전달할 수 있습니다. 동적 콘텐츠 만들기를 처리하는 메서드는 단일 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 매개 변수를 사용하여 문자열을 반환합니다. 반환 문자열은 지정된 위치에서 대체될 내용입니다. 대체 컨트롤을 선언적으로 사용하는 대신 WriteSubstittion 메서드를 호출하는 이점은 페이지 또는 UserControl 개체의 정적 메서드를 호출하는 대신 임의의 개체의 메서드를 호출할 수 있다는 것입니다.

WriteSubtitution 메서드를 호출하면 클라이언트 측 캐시 가능성이 서버 캐시 가능성으로 변경되어 페이지가 클라이언트에 캐시되지 않습니다. 이렇게 하면 페이지에 대한 이후 요청이 메서드를 호출하여 동적 콘텐츠를 생성할 수 있습니다.

### <a name="adrotator-control"></a>애드로테이터 제어

AdRotator 서버 제어는 내부적으로 사후 캐시 대체에 대한 지원을 구현합니다. 페이지에 AdRotatator 컨트롤을 배치하면 상위 페이지가 캐시되었는지 여부에 관계없이 각 요청에 고유한 광고가 렌더링됩니다. 따라서 AdRotator 컨트롤이 포함된 페이지는 서버 측에만 캐시됩니다.

## <a name="controlcachepolicy-class"></a>제어캐시정책 클래스

ControlCachePolicy 클래스를 사용하면 사용자 컨트롤을 사용하여 조각 캐싱을 프로그래밍 방식으로 제어할 수 있습니다. ASP.NET [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) 인스턴스 내에 사용자 컨트롤을 포함합니다. BasePartialCachingControl 클래스는 출력 캐싱을 사용하도록 설정한 사용자 컨트롤을 나타냅니다.

[PartialCachingControl 컨트롤의 BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) 속성에 액세스하면 항상 유효한 ControlCachePolicy 개체를 받게 됩니다. [PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) 그러나 UserControl.CachePolicy 사용자 컨트롤의 [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) 속성에 액세스 하는 경우 사용자 컨트롤이 BasePartialCachingControl 컨트롤에 의해 이미 래핑 된 경우에 유효한 ControlCachePolicy 개체를 받습니다. [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) 래핑되지 않으면 속성에서 반환되는 ControlCachePolicy 개체는 연결된 BasePartialCachingControl이 없기 때문에 조작을 시도할 때 예외를 throw합니다. UserControl 인스턴스가 예외를 생성하지 않고 캐싱을 지원하는지 확인하려면 [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) 속성을 검사합니다.

ControlCachePolicy 클래스를 사용 하 여 출력 캐싱을 사용 하는 여러 가지 방법 중 하나입니다. 다음 목록에서는 출력 캐싱을 사용 하도록 설정 하 여 메서드를 설명 합니다.

- @ [OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문을 사용하여 선언적 시나리오에서 출력 캐싱을 활성화합니다.
- [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) 특성을 사용하여 코드 숨이 뒤의 파일에서 사용자 컨트롤에 대한 캐싱을 사용하도록 설정합니다.
- ControlCachePolicy 클래스를 사용하여 이전 방법 중 하나를 사용하여 캐시를 사용하도록 설정하고 [System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) 메서드를 사용하여 동적으로 로드된 BasePartialCachingControl 인스턴스로 작업하는 프로그래밍 방식 시나리오에서 캐시 설정을 지정합니다.

ControlCachePolicy 인스턴스는 제어 수명 주기의 초기화 및 PreRender 단계 사이에서만 성공적으로 조작할 수 있습니다. PreRender 단계 후에 ControlCachePolicy 개체를 수정하는 경우 컨트롤이 렌더링된 후 변경한 내용이 캐시 설정에 실제로 영향을 줄 수 없기 때문에 예외를 ASP.NET 합니다(컨트롤은 렌더 단계 동안 캐시됩니다). 마지막으로 사용자 컨트롤 인스턴스(및 따라서 ControlCachePolicy 개체)는 실제로 렌더링될 때만 프로그래밍 방식으로 조작할 수 있습니다.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>캐싱 구성 변경 &lt;-&gt; 캐싱 요소

ASP.NET 2.0에서 캐싱 구성에 몇 가지 변경 사항이 있습니다. &lt;캐싱&gt; 요소는 ASP.NET 2.0에서 새로 야하며 구성 파일에서 캐싱 구성을 변경할 수 있습니다. 다음 특성을 사용할 수 있습니다.

| **요소** | **설명** |
| --- | --- |
| **캐시** | 선택적 요소입니다. 전역 응용 프로그램 캐시 설정을 정의합니다. |
| **Outputcache** | 선택적 요소입니다. 응용 프로그램 전체 출력 캐시 설정을 지정합니다. |
| **outputCacheSettings** | 선택적 요소입니다. 응용 프로그램의 페이지에 적용할 수 있는 출력 캐시 설정을 지정합니다. |
| **sqlCacheDependency** | 선택적 요소입니다. ASP.NET 애플리케이션의 SQL 캐시 종속성을 구성합니다. |

### <a name="the-ltcachegt-element"></a>&lt;캐시&gt; 요소

캐시 &lt;&gt; 요소에서 다음 특성을 사용할 수 있습니다.

| **attribute** | **설명** |
| --- | --- |
| **메모리 수집 을 사용하지 않도록 설정** | 부울 **속성(옵션)입니다.** 컴퓨터가 메모리 압력을 받고 있을 때 발생하는 캐시 메모리 컬렉션이 비활성화되었는지 여부를 나타내는 값을 얻거나 설정합니다. |
| **사용 안 함** | 부울 **속성(옵션)입니다.** 캐시 만료가 비활성화되어 있는지 여부를 나타내는 값을 얻거나 설정합니다. 비활성화하면 캐시된 항목이 만료되지 않고 만료된 캐시 항목의 백그라운드 청소가 발생하지 않습니다. |
| **프라이빗 바이트제한** | 선택적 **Int64** 특성입니다. 캐시가 만료된 항목을 플러시하고 메모리를 회수하기 전에 응용 프로그램의 개인 바이트의 최대 크기를 나타내는 값을 얻거나 설정합니다. 이 제한에는 캐시에서 사용하는 메모리와 실행 중인 응용 프로그램의 일반 메모리 오버헤드가 모두 포함됩니다. 0으로 설정하면 ASP.NET 메모리 회수 시기를 결정하기 위해 자체 추론을 사용합니다. |
| **백분율물리적 메모리사용한계** | 선택적 **Int32** 특성입니다. 캐시가 만료된 항목을 플러시하고 메모리를 회수하기 전에 응용 프로그램에서 사용할 수 있는 컴퓨터의 실제 메모리의 최대 백분율을 나타내는 값을 얻거나 설정합니다. 0으로 설정하면 ASP.NET 메모리 회수 시기를 결정하기 위해 자체 추론을 사용합니다. |
| **프라이빗 바이트폴타임** | 선택적 **TimeSpan** 특성입니다. 응용 프로그램의 개인 바이트 메모리 사용량에 대한 폴링 사이의 시간 간격을 나타내는 값을 얻거나 설정합니다. |

### <a name="the-ltoutputcachegt-element"></a>&lt;출력캐시&gt; 요소

&lt;다음 특성은 outputCache&gt; 요소에 사용할 수 있습니다.

|       <strong>attribute</strong>        |                                                                                                                                                                                                                                                       <strong>설명</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>사용 백량출력 캐시</strong>    |                                                                                                                                                          부울 <strong>속성(옵션)입니다.</strong> 페이지 출력 캐시를 활성화/비활성화합니다. 사용하지 않도록 설정하면 프로그래밍 방식 또는 선언적 설정에 관계없이 페이지가 캐시되지 않습니다. 기본값은 <strong>true입니다.</strong>                                                                                                                                                           |
|  <strong>인에이블프래프래그캐시</strong>   |                                                부울 <strong>속성(옵션)입니다.</strong> 응용 프로그램 조각 캐시를 활성화/비활성화합니다. 사용하지 않도록 설정하면 [사용된 @OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문 또는 캐싱 프로필에 관계없이 페이지가 캐시되지 않습니다. 업스트림 프록시 서버와 브라우저 클라이언트가 페이지 출력을 캐시하려고 시도해서는 안 된다는 것을 나타내는 캐시 제어 헤더가 포함되어 있습니다. 기본값은 <strong>false</strong>입니다.                                                 |
| <strong>sendCacheControl헤더</strong> |                                                                                                                                                      부울 <strong>속성(옵션)입니다.</strong> 기본적으로 출력 캐시 모듈에서 <strong>캐시 제어:개인</strong> 헤더가 전송되는지 여부를 나타내는 값을 가져오거나 설정합니다. 기본값은 <strong>false</strong>입니다.                                                                                                                                                      |
|      <strong>옴티바리스타</strong>      | 부울 <strong>속성(옵션)입니다.</strong> 응답에서 http " 변경:<strong> \</강한>" 헤더를 보내는 것을 사용 /비활성화합니다. <em> 기본 설정인 false를 사용하면</em>"*Vary: \* <strong>"헤더가 출력 캐시된 페이지에 대해 전송됩니다. [Vary 헤더]가 전송되면 Vary 헤더에 지정된 내용에 따라 다른 버전을 캐시할 수 있습니다. 예를 <em>들어, 변화:사용자 에이전트는</em> 요청을 발급하는 사용자 에이전트에 따라 페이지의 다른 버전을 저장합니다. 기본값은 **false입니다.</strong> |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;출력캐시설정&gt; 요소

&lt;outputCacheSettings&gt; 요소는 앞에서 설명한 대로 캐시 프로파일을 만들 수 있습니다. &lt;&gt; outputCacheSettings 요소에 대 한 유일한 &lt;자식 요소는&gt; cache profiles 를 구성 하기 위한 outputCacheProfiles 요소입니다.

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCache 종속성&gt; 요소

sqlCacheDependency&gt; 요소에 &lt;대해 다음 특성을 사용할 수 있습니다.

| **attribute** | **설명** |
| --- | --- |
| **사용** | 필요한 **부울** 속성입니다. 변경 내용이 폴링되고 있는지 여부를 나타냅니다. |
| **폴타임** | 선택적 **Int32** 특성입니다. SqlCacheDependency가 변경 내용을 위해 데이터베이스 테이블을 폴싱하는 빈도를 설정합니다. 이 값은 연속된 폴링 사이의 밀리초 수에 해당합니다. 500밀리초 미만으로 설정할 수 없습니다. 기본값은 1분입니다. |

### <a name="more-information"></a>추가 정보

캐시 구성과 관련하여 알아야 할 몇 가지 추가 정보가 있습니다.

- 작업자 프로세스 개인 바이트 제한이 설정되지 않은 경우 캐시는 다음 제한 중 하나를 사용합니다. 

    - x86 2GB: 800MB 또는 실제 RAM의 60% 중 더 적은
    - x86 3GB: 1800MB 또는 실제 RAM의 60% 중 더 적은
    - x64: 1테라바이트 또는 물리적 RAM의 60% 중 더 적은 RAM
- 작업자 프로세스 개인 바이트 제한 &lt;및 캐시 privateBytesLimit/를&gt; 모두 설정 하는 경우 캐시는 둘 중 최소를 사용 합니다.
- 1.x와 마찬가지로 캐시 항목을 삭제하고 GC를 호출합니다. 다음 두 가지 이유로 수집합니다. 

    - 우리는 개인 바이트 제한에 매우 가깝습니다.
    - 사용 가능한 메모리가 10% 가까이 또는 미만입니다.
- 캐시 백분율을 100으로 설정하여 &lt;사용 가능한 메모리가 낮은&gt; 조건에 대한 트림 및 캐시를 효과적으로 비활성화할 수 있습니다.
- 1.x와 달리 2.0은 트림을 일시 중단하고 마지막 GC인 경우 호출을 수집합니다. 수집은 개인 바이트 또는 관리되는 힙의 크기를 캐시(캐시) 메모리 제한의 1% 이상 줄이지 않았습니다.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: 사용자 지정 캐시 종속성

1. 새 웹 사이트를 만듭니다.
2. cache.xml이라는 새 XML 파일을 추가하고 웹 응용 프로그램의 루트에 저장합니다.
3. default.aspx의\_코드 뒤에 페이지 로드 메서드에 다음 코드를 추가합니다. 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 소스 뷰에서 default.aspx 의 맨 위에 다음을 추가합니다. 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 기본값.aspx 찾아봅그. 시간은 무엇을 말하는가?
6. 브라우저를 새로 고칩니다. 시간은 무엇을 말하는가?
7. cache.xml을 열고 다음 코드를 추가합니다. 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. cache.xml을 저장합니다.
9. 브라우저를 새로 고칩니다. 시간은 무엇을 말하는가?
10. 이전에 캐시된 값을 표시하는 대신 시간이 업데이트된 이유를 설명합니다.

## <a name="lab-2-using-polling-based-cache-dependencies"></a>랩 2: 폴링 기반 캐시 종속성 사용

이 랩에서는 이전 모듈에서 만든 프로젝트를 사용하여 GridView 및 DetailsView 컨트롤을 통해 Northwind 데이터베이스의 데이터를 편집할 수 있습니다.

1. 비주얼 스튜디오 2005에서 프로젝트를 엽니다.
2. 노스윈드 데이터베이스에\_대해 aspnet regsql 유틸리티를 실행하여 데이터베이스 및 Products 테이블을 활성화합니다. Visual Studio 명령 프롬프트에서 다음 명령을 사용합니다. 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. web.config 파일에 다음을 추가합니다. 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. showdata.aspx라는 새 웹 양식을 추가합니다.
5. showdata.aspx 페이지에 다음 @ outputcache 지시문을 추가합니다. 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. showdata.aspx의\_페이지 로드에 다음 코드를 추가합니다. 

    [!code-html[Main](caching/samples/sample21.html)]
7. 새 SqlDataSource 컨트롤을 추가하여 showdata.aspx를 추가하고 Northwind 데이터베이스 연결을 사용하도록 구성합니다. 다음을 클릭합니다.
8. 제품 이름 및 제품 ID 확인란을 선택하고 다음을 클릭합니다.
9. 마침을 클릭합니다.
10. showdata.aspx 페이지에 새 GridView를 추가합니다.
11. 드롭다운에서 SqlDataSource1을 선택합니다.
12. 저장 및 showdata.aspx를 찾아보십시오. 표시된 시간을 기록해 둡을 기록합니다.
