---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '부록: 수정 샘플 응용 프로그램 (Azure를 사용 하 고 실제 클라우드 애플 리 케이 션 빌드) | 마이크로 소프트 문서'
author: MikeWasson
description: Azure 전자책을 사용한 실제 클라우드 앱 구축은 Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 그것은 그가 할 수있는 13 패턴과 관행을 설명합니다 ...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675636"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>부록: 수정 샘플 응용 프로그램(Azure를 사용하여 실제 클라우드 앱 빌드)

[마이크 와슨,](https://github.com/MikeWasson) [릭 앤더슨,](https://twitter.com/RickAndMSFT) [톰 다이크스트라](https://github.com/tdykstra)

[수정 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure 전자책을 **사용한 실제 클라우드 앱 구축은** Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 클라우드용 웹 앱을 성공적으로 개발하는 데 도움이 되는 13가지 패턴과 사례에 대해 설명합니다. 전자책에 대한 자세한 내용은 [첫 번째 장을](introduction.md)참조하십시오.

Azure 전자책이 있는 실제 클라우드 앱 빌드에 대한 이 부록에는 다운로드할 수 있는 Fix It 샘플 응용 프로그램에 대한 추가 정보를 제공하는 다음 섹션이 포함되어 있습니다.

- [알려진 문제](#knownissues)
- [모범 사례](#bestpractices)
- [로컬 컴퓨터에서 Visual Studio에서 앱을 실행하는 방법](#run-in-vs)
- [Windows PowerShell 스크립트를 사용하여 기본 앱을 Azure 앱 서비스 웹 앱에 배포하는 방법](#deploybase)
- [Windows PowerShell 스크립트 문제 해결](#troubleshooting)
- [Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스에 큐 처리를 사용하여 앱을 배포하는 방법](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>알려진 문제

Fix It 앱은 원래 이 전자책에 제시된 패턴 중 일부를 가능한 한 간단하게 설명하기 위해 개발되었습니다. 그러나 전자 책은 실제 앱을 빌드하는 것에 관한 것이므로 릴리스된 소프트웨어에 대해 수행하는 것과 유사한 검토 및 테스트 프로세스에 Fix It 코드를 적용했습니다. 우리는 여러 가지 문제를 발견했으며 실제 응용 프로그램과 마찬가지로 일부 응용 프로그램은 수정했으며 일부는 나중에 릴리스로 연기했습니다.

다음 목록에는 프로덕션 응용 프로그램에서 해결해야 하는 문제가 포함되어 있지만 한 가지 이유 또는 다른 이유로 Fix It 샘플 응용 프로그램의 초기 릴리스에서 해결하지 않기로 결정했습니다.

### <a name="security"></a>보안

- 존재하지 않는 소유자에게 작업을 할당할 수 없는지 확인합니다.
- 생성했거나 사용자에게 할당된 작업만 보고 수정할 수 있는지 확인합니다.
- 로그인 페이지 및 인증 쿠키에 HTTPS를 사용합니다.
- 인증 쿠키에 대한 시간 제한을 지정합니다.

### <a name="input-validation"></a>입력 유효성 검사

일반적으로 프로덕션 앱은 Fix It 앱보다 더 많은 입력 유효성 검사를 수행합니다. 예를 들어 업로드가 허용되는 이미지 크기/이미지 파일 크기는 제한되어야 합니다.

### <a name="administrator-functionality"></a>관리자 기능

관리자는 기존 작업의 소유권을 변경할 수 있어야 합니다. 예를 들어 작업 작성자는 관리 액세스가 활성화되지 않는 한 작업을 유지할 권한이 없는 회사를 떠날 수 있습니다.

### <a name="queue-message-processing"></a>큐 메시지 처리

Fix It 앱에서 큐 메시지 처리는 최소한의 코드로 큐 중심 작업 패턴을 설명하기 위해 간단하도록 설계되었습니다. 이 간단한 코드는 실제 프로덕션 응용 프로그램에 적합하지 않습니다.

- 코드는 각 큐 메시지가 한 번에 처리된다는 것을 보장하지 않습니다. 큐에서 메시지를 받으면 다른 큐 수신기에 메시지가 표시되지 않는 시간 시간(시간) 기간이 있습니다. 메시지가 삭제되기 전에 시간 시간이 만료되면 메시지가 다시 표시됩니다. 따라서 작업자 역할 인스턴스가 메시지를 처리하는 데 오랜 시간을 소비하는 경우 이론적으로 동일한 메시지가 두 번 처리되어 데이터베이스에 중복 작업이 발생할 수 있습니다. 이 문제에 대한 자세한 내용은 [Azure 저장소 큐 사용](https://msdn.microsoft.com/library/ff803365.aspx#sec7)을 참조하십시오.
- 메시지 검색을 일괄 처리하여 큐 폴링 논리를 보다 비용 효율적일 수 있습니다. [CloudQueue.GetMessageAsync를](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)호출할 때마다 트랜잭션 비용이 듭니다. 대신 단일 트랜잭션에서 여러 메시지를 받는 [CloudQueue.GetMessagesAsync(복수의](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) 's')를 호출할 수 있습니다. Azure 저장소 큐의 트랜잭션 비용은 매우 낮으므로 대부분의 시나리오에서는 비용에 미치는 영향이 그리 많지 않습니다.
- 큐 메시지 처리 코드의 긴밀한 루프는 다중 코어 VM을 효율적으로 활용하지 않는 CPU 선호도를 유발합니다. 더 나은 디자인은 작업 병렬 처리를 사용하여 여러 비동기 작업을 병렬로 실행합니다.
- 큐 메시지 처리에는 기본적인 예외 처리만 있습니다. 예를 들어 코드는 [포이즌 메시지를](https://msdn.microsoft.com/library/ms789028.aspx)처리하지 않습니다. 메시지 처리로 인해 예외가 발생하면 오류를 기록하고 메시지를 삭제해야 하거나 작업자 역할이 다시 처리하려고 시도하면 루프가 무기한 계속됩니다.

### <a name="sql-queries-are-unbounded"></a>SQL 쿼리는 무한합니다.

현재 Fix It 코드는 인덱스 페이지에 대한 쿼리가 반환할 수 있는 행 수에 제한을 두지 않습니다. 데이터베이스에 많은 양의 작업을 입력하면 수신된 결과 목록의 크기로 인해 성능 문제가 발생할 수 있습니다. 해결책은 페이징을 구현하는 것입니다. 예를 들어 [ASP.NET MVC 응용 프로그램에서 엔터티 프레임워크를 사용 하 여 정렬, 필터링 및 페이징을](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)참조 합니다.

### <a name="view-models-recommended"></a>권장 모델 보기

Fix It 앱은 FixItTask 엔터티 클래스를 사용하여 컨트롤러와 뷰 간에 정보를 전달합니다. 뷰 모델을 사용하는 것이 가장 좋습니다. 도메인 모델(예: FixItTask 엔터티 클래스)은 데이터 지속성에 필요한 것을 중심으로 설계되었으며 뷰 모델은 데이터 프레젠테이션용으로 설계할 수 있습니다. 자세한 내용은 [12ASP.NET MVC 모범 사례를](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)참조하십시오.

### <a name="secure-image-blob-recommended"></a>보안 이미지 Blob 권장

Fix It 앱은 업로드된 이미지를 공개로 저장하므로 URL을 찾는 사람은 누구나 이미지에 액세스할 수 있습니다. 이미지는 공개가 아닌 보호할 수 있습니다.

### <a name="no-powershell-automation-scripts-for-queues"></a>큐에 대한 PowerShell 자동화 스크립트 없음

샘플 PowerShell 자동화 스크립트는 Azure App Service 웹 앱에서 전적으로 실행되는 Fix It의 기본 버전에 대해서만 작성되었습니다. 웹 앱에 설정하고 배포하기 위한 스크립트와 큐 처리에 필요한 클라우드 서비스 환경을 제공하지 않았습니다.

### <a name="special-handling-for-html-codes-in-user-input"></a>사용자 입력에서 HTML 코드에 대한 특수 처리

ASP.NET 악의적인 사용자가 사용자 입력 텍스트 상자에 스크립트를 입력하여 사이트 간 스크립팅 공격을 시도할 수 있는 여러 가지 방법을 자동으로 방지합니다. 그리고 작업 `DisplayFor` 제목및 메모를 표시하는 데 사용되는 MVC 도우미는 브라우저에 전송하는 값을 자동으로 HTML 인코딩합니다. 그러나 프로덕션 앱에서는 추가 조치를 취할 수 있습니다. 자세한 내용은 ASP.NET 유효성 [검사 요청을](https://msdn.microsoft.com/library/hh882339.aspx)참조하십시오.

<a id="bestpractices"></a>
## <a name="best-practices"></a>모범 사례

다음은 Fix It 앱의 원래 버전의 코드 검토 및 테스트에서 발견된 후 수정된 몇 가지 문제입니다. 일부는 원래 코더가 특정 모범 사례를 인식하지 못하고 코드가 신속하게 작성되어 릴리스된 소프트웨어를 위한 것이 아니기 때문에 발생했습니다. 이 리뷰와 테스트에서 배운 것이 웹 앱을 개발하는 다른 사람들에게 도움이 될 수 있는 문제가 있는 경우를 대비하여 여기에 문제를 나열하고 있습니다.

### <a name="dispose-the-database-repository"></a>데이터베이스 리포지토리 삭제

클래스는 `FixItTaskRepository` 엔터티 프레임워크 `DbContext` 인스턴스를 삭제해야 합니다. 클래스에서 구현하여 `IDisposable` 이 `FixItTaskRepository` 작업을 수행했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac은 인스턴스를 `FixItTaskRepository` 자동으로 삭제하므로 명시적으로 삭제할 필요가 없습니다.

또 다른 옵션은 `DbContext` 에서 `FixItTaskRepository`멤버 변수를 제거하고 `DbContext` 대신 문 내에서 각 리포지토리 메서드 내에서 로컬 변수를 만드는 것입니다. `using` 예를 들어:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>DI와 같은 싱글톤 등록

`PhotoService` 클래스와 `Logger` 클래스의 인스턴스가 하나만 필요하므로 이러한 클래스는 *DependenciesConfig.cs* [종속성 주입을 위한 단일 인스턴스로 등록되어야](https://code.google.com/p/autofac/wiki/InstanceScope) 합니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>보안: 사용자에게 오류 세부 정보를 표시하지 마십시오.

원래 Fix It 앱에는 일반 오류 페이지가 없으며 모든 예외가 UI에 버블링되도록 하여 데이터베이스 연결 오류와 같은 일부 예외로 인해 전체 스택 추적이 브라우저에 표시될 수 있습니다. 자세한 오류 정보는 악의적인 사용자의 공격을 용이하게 할 수 있습니다. 해결 방법은 예외 세부 정보를 기록하고 오류 세부 정보가 포함되지 않은 사용자에게 오류 페이지를 표시하는 것입니다. Fix It 앱이 이미 로깅 중이었으며 오류 페이지를 `<customErrors mode=On>` 표시하기 위해 Web.config 파일에 추가했습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

기본적으로 이로 인해 *뷰\공유\Error.cshtml이* 오류에 대해 표시됩니다. *Error.cshtml을* 사용자 지정하거나 고유한 오류 페이지 보기를 `defaultRedirect` 만들고 특성을 추가할 수 있습니다. 특정 오류에 대해 다른 오류 페이지를 지정할 수도 있습니다.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>보안: 작성자가 작업을 편집할 수 있도록 허용

대시보드 색인 페이지에는 로그온한 사용자가 만든 작업만 표시되지만 악의적인 사용자는 다른 사용자의 작업에 ID가 있는 URL을 만들 수 있습니다. 이 경우 404를 반환하기 위해 *DashboardController.cs* 코드를 추가했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>예외를 삼키지 마십시오.

원래 Fix It 앱은 SQL 쿼리로 인해 발생한 예외를 로깅한 후 null을 반환했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

이렇게하면 쿼리가 성공했지만 행을 반환하지 않은 것처럼 사용자에게 표시됩니다. 해결 방법은 catch 및 로깅 후 예외를 다시 throw하는 것입니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>작업자 역할의 모든 예외 catch

작업자 역할에서 처리되지 않은 예외는 VM을 재활용하게 되므로 try-catch 블록에서 수행하는 모든 작업을 래핑하고 모든 예외를 처리하려고 합니다.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>엔터티 클래스의 문자열 속성에 대한 길이 지정

간단한 코드를 표시 하기 위해 Fix It 앱의 원래 버전 FixItTask 엔터티의 필드에 대 한 길이 지정 하지 않은, 그리고 결과적으로 그들은 varchar (최대)로 정의 된 데이터베이스에. 결과적으로 UI는 거의 모든 양의 입력을 허용합니다. 길이를 지정하면 웹 페이지의 사용자 입력과 데이터베이스의 열 크기에 모두 적용되는 제한이 설정됩니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>변경될 것으로 예상되지 않을 때 개인 멤버를 readonly로 표시

예를 들어 `DashboardController` 클래스에서 인스턴스가 `FixItTaskRepository` 만들어지고 변경될 것으로 예상되지 않으므로 [readonly로](https://msdn.microsoft.com/library/acdd6hb7.aspx)정의했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>목록을 사용합니다. 목록 대신 Any()입니다. 카운트() &gt; 0

목록의 하나 이상의 항목이 지정된 기준에 맞는지 여부만 신경 [Any](https://msdn.microsoft.com/library/bb534972.aspx) 쓰는 경우 조건에 맞는 항목이 발견되는 즉시 반환되지만 `Count` 메서드는 항상 모든 항목을 반복해야 하므로 Any 메서드를 사용합니다. 대시보드 *Index.cshtml* 파일에는 원래 이 코드가 있었습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

우리는 이것을 변경했습니다:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC 도우미를 사용하여 MVC 보기에서 URL 생성

홈 페이지의 **수정** 만들기 단추의 경우 Fix It 앱이 앵커 요소를 하드 코딩했습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

이와 같은 보기/작업 링크의 경우 [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 도우미를 사용하는 것이 좋습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>작업자 역할에서 Thread.Sleep 대신 Task.Delay 사용

새 프로젝트 템플릿은 `Thread.Sleep` 작업자 역할에 대한 샘플 코드에 포함하지만 스레드가 절전 모드로 연결되면 스레드 풀이 추가 불필요한 스레드를 생성할 수 있습니다. 대신 [Task.Delay를](https://msdn.microsoft.com/library/hh139096.aspx) 사용하여 이를 방지할 수 있습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>비동기 보이드 방지

비동기 메서드가 값을 `Task` 반환할 필요가 없는 경우 . `void`

이 예제는 `FixItQueueManager` 클래스에서 수행되었습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

최상위 이벤트 `async void` 처리기에만 사용해야 합니다. 메서드를 `async void`로 정의하는 경우 호출자는 메서드를 **기다리거나** 메서드가 throw하는 예외를 catch할 수 없습니다. 자세한 내용은 [비동기 프로그래밍의 모범 사례를](https://msdn.microsoft.com/magazine/jj991977.aspx)참조하십시오.

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>취소 토큰을 사용하여 작업자 역할 루프에서 분리

일반적으로 작업자 역할의 **Run** 메서드에는 무한 루프가 포함됩니다. 작업자 역할이 중지되면 [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 메서드가 호출됩니다. 이 메서드를 사용 하 여 **Run** 메서드 내에서 수행 되는 작업을 취소 하 고 정상적으로 종료 해야 합니다. 그렇지 않으면 작업이 중간에 종료될 수 있습니다.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>자동 MIME 스니핑 절차 거부

경우에 따라 Internet Explorer는 웹 서버에서 지정한 유형과 다른 MIME 유형을 보고합니다. 예를 들어 Internet Explorer가 HTTP 응답 헤더 콘텐츠 유형: 텍스트/일반과 함께 전달된 파일에서 HTML 콘텐츠를 발견하면 Internet Explorer는 콘텐츠를 HTML로 렌더링해야 한다고 결정합니다. 안타깝게도 이 "MIME 스니핑"은 신뢰할 수 없는 콘텐츠를 호스팅하는 서버의 보안 문제로 이어질 수도 있습니다. 이 문제를 방지하기 위해 Internet Explorer 8은 MIME 형식 결정 코드를 여러 번 변경했으며 응용 프로그램 개발자가 [MIME 스니핑을 옵트아웃할](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)수 있도록 합니다. 다음 코드가 *Web.config* 파일에 추가되었습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>번들 및 축소 사용

Visual Studio에서 새 웹 프로젝트를 만들 때 자바스크립트 파일의 번들 및 축소는 기본적으로 활성화되지 않습니다. BundleConfig.cs 코드 줄을 추가했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>인증 쿠키의 만료 시간 시간 설정

기본적으로 인증 쿠키는 2주 후 만료됩니다. 짧은 시간은 더 안전합니다. *StartupAuth.cs*이 설정을 변경할 수 있습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>로컬 컴퓨터에서 Visual Studio에서 앱을 실행하는 방법

Fix It 앱을 실행하는 방법에는 두 가지가 있습니다.

- SQL 데이터베이스에 직접 새 작업을 기록하는 기본 응용 프로그램을 실행합니다.
- 큐와 백 엔드 서비스를 사용하여 응용 프로그램을 실행하여 작업을 만듭니다. 큐 패턴은 [큐 중심 작업 패턴](queue-centric-work-pattern.md)장에서 설명합니다.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>기본 응용 프로그램 실행

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 설치합니다.
2. Visual [Studio에 .NET에 대한 Azure SDK를 설치합니다.](https://azure.microsoft.com/downloads/)
3. [MSDN 코드 갤러리에서](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).zip 파일을 다운로드합니다.
4. 파일 탐색기에서 .zip 파일을 마우스 오른쪽 단추로 클릭하고 속성을 클릭한 다음 속성 창에서 차단 해제를 클릭합니다.
5. 파일 의 압축을 해제합니다.
6. .sln 파일을 두 번 클릭하여 Visual Studio를 시작합니다.
7. **도구** 메뉴에서 **패키지 관리자 NuGet을**클릭한 다음 **패키지 관리자 콘솔을**클릭합니다.
8. PMC(패키지 관리자 콘솔)에서 복원을 클릭합니다.
9. Visual Studio를 끝냅니다.
10. Azure [저장소 에뮬레이터를](/azure/storage/common/storage-use-emulator)시작합니다.
11. 이전 단계에서 닫은 솔루션 파일을 열어 Visual Studio를 다시 시작합니다.
12. FixIt 프로젝트가 시작 프로젝트로 설정되어 있는지 확인한 다음 CTRL+F5를 눌러 프로젝트를 실행합니다.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>큐 처리를 사용 하 고 응용 프로그램 실행

1. 기본 응용 [프로그램 실행의 지시에](#runbase)따라 브라우저를 닫고 Visual Studio를 닫습니다.
2. 관리자 권한으로 Visual Studio를 시작합니다. Azure 계산 에뮬레이터를 사용하며 관리자 권한이 필요합니다.
3. *MyFixIt* 프로젝트(웹 프로젝트)의 `appSettings/UseQueues` 응용 프로그램 *Web.config* 파일에서 값을 "true"로 변경합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Azure [저장소 에뮬레이터가](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 계속 실행되지 않으면 다시 시작합니다.
5. FixIt 웹 프로젝트와 MyFixItCloudService 프로젝트를 동시에 실행합니다.

    비주얼 스튜디오 사용:

   1. **F5를** 눌러 FixIt 프로젝트를 실행합니다.
   2. **솔루션 탐색기에서**MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 새 인스턴스 시작 **디버그를** > **Start New Instance**클릭합니다.

    웹용 비주얼 스튜디오 2013 익스프레스 사용:

   3. 솔루션 탐색기에서 FixIt 솔루션을 마우스 오른쪽 단추로 클릭하고 **속성을**선택합니다.
   4. **여러 시작 프로젝트를**선택합니다.
   5. MyFixIt 및 MyFixItCloudService 아래의 **작업** 드롭다운 목록에서 **시작**을 선택합니다.
   6. **확인**을 클릭합니다.
   7. **F5** 키를 눌러 두 프로젝트를 실행합니다.

      MyFixItCloudService 프로젝트를 실행 하면 Visual Studio Azure 계산 에뮬레이터를 시작 합니다. 방화벽 구성에 따라 방화벽을 통해 에뮬레이터를 허용해야 할 수 있습니다.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell 스크립트를 사용하여 기본 앱을 Azure 앱 서비스 웹 앱에 배포하는 방법

[모든 자동화](automate-everything.md) 패턴을 설명하기 위해 Fix It 앱은 Azure에서 환경을 설정하고 새 환경에 프로젝트를 배포하는 스크립트와 함께 제공됩니다. 다음 지침은 스크립트를 사용하는 방법을 설명합니다.

큐를 사용하지 않고 Azure에서 실행하려는 경우 다음 지침을 진행하기 전에 UseQueues appSet 값을 false로 다시 설정해야 합니다.

이러한 지침은 이미 다운로드하여 로컬에서 Fix It 솔루션을 실행하고 Azure 계정이 있거나 관리할 권한이 있는 Azure 구독이 있다고 가정합니다.

1. Azure **PowerShell** 콘솔을 설치합니다. 자세한 내용은 [Azure PowerShell 설치 및 구성법](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)을 참조하세요.

    이 사용자 지정된 콘솔은 Azure 구독에서 작동하도록 구성됩니다. Azure 모듈은 프로그램 *파일* 디렉터리에 설치되며 Azure PowerShell 콘솔을 사용할 때마다 자동으로 가져옵니다.

    Windows PowerShell ISE와 같은 다른 호스트 프로그램에서 작업하려는 경우 가져오기 [모듈](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet을 사용하여 Azure 모듈을 가져오거나 Azure 모듈의 명령을 사용하여 모듈의 자동 가져오기를 트리거해야 합니다.
2. **관리자로 실행** 옵션을 사용 하 고 Azure PowerShell을 시작 합니다.
3. Azure PowerShell 실행 정책을 로 설정하려면 [실행 정책](https://go.microsoft.com/fwlink/p/?linkid=293941) `RemoteSigned`설정 cmdlet을 실행합니다. 정책 **Y** 변경을 완료하려면 Y(예)를 입력합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    이 설정을 사용하면 디지털 서명되지 않은 로컬 스크립트를 실행할 수 있습니다. (나중에 차단 해제 단계가 `Unrestricted`필요하지 않은 을 으로 실행 정책을 설정할 수도 있지만 보안상의 이유로는 권장되지 않습니다.)
4. cmdlet을 `Add-AzureAccount` 실행하여 계정에 대한 자격 증명을 사용하여 PowerShell을 설정합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    이러한 자격 증명은 시간이 지나면 만료되며 cmdlet을 `Add-AzureAccount` 다시 실행해야 합니다. 이 전자책을 작성할 때 자격 증명이 만료되기 까지의 시간 제한은 12시간입니다.
5. 구독이 여러 개인 경우 Select-AzureSubscription cmdlet을 사용하여 테스트 환경을 만들 구독을 지정합니다.
6. 및 `Import-AzurePublishSettingsFile` cmdlet을 사용하여 동일한 Azure `Get-AzurePublishSettingsFile` 구독에 대한 관리 인증서를 가져옵니다. 이러한 cmdlet 중 첫 번째는 인증서 파일을 다운로드하고 두 번째 cmdlet에서는 인증서 파일을 가져오기 위해 해당 파일의 위치를 지정합니다. > [!IMPORTANT]
   > 다운로드한 파일을 안전한 위치에 보관하거나 Azure 서비스를 관리하는 데 사용할 수 있는 인증서가 포함되어 있으므로 파일을 완료하면 삭제합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    이 인증서는 SQL Database 서버에서 방화벽 규칙을 설정하기 위해 개발 컴퓨터의 IP 주소를 검색하는 REST API 호출에 사용됩니다.
7. 설정 [위치](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet(별칭은 `cd`, `chdir`및)을 `sl`실행하여 스크립트가 포함된 디렉터리로 이동합니다. 수정 솔루션 폴더의 *자동화* 폴더에 있습니다. 디렉터리 이름에 공백이 있는 경우 경로를 따옴표로 넣습니다. 예를 들어 `c:\Sample Apps\FixIt\Automation` 디렉터리로 이동하려면 다음 명령을 입력할 수 있습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell에서 이러한 스크립트를 실행할 수 있도록 하려면 [파일 차단 해제](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet을 사용합니다. 스크립트는 인터넷에서 다운로드했기 때문에 차단됩니다.

    > [!WARNING]
    > 보안 - `Unblock-File` 스크립트 또는 실행 파일에서 실행하기 전에 메모장에서 파일을 열고 명령을 검사하고 악성 코드가 포함되어 있지 않은지 확인합니다.

    예를 들어 다음 명령은 `Unblock-File` 현재 디렉터리에서 모든 스크립트에서 cmdlet을 실행합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 기본에 대한 웹 앱을 만들려면(큐 처리 없음) Fix It 앱은 환경 만들기 스크립트를 실행합니다.

    필수 `Name` 매개 변수는 데이터베이스 이름을 지정하고 스크립트가 만드는 저장소 계정에도 사용됩니다. 이름은 azurewebsites.net 도메인 내에서 전역적으로 고유해야 합니다. Fixit 또는 Test와 같이 고유하지 않은 이름을 지정하는 경우(또는 예제에서와 `New-AzureWebsite` 같이 fixitdemo) cmdlet은 충돌을 보고하는 내부 오류와 함께 실패합니다. 스크립트는 웹 앱, 저장소 계정 및 데이터베이스에 대한 이름 요구 사항을 준수하도록 이름을 모든 소문자로 변환합니다.

    필요한 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 만들어질 관리자 계정의 암호를 지정합니다. 암호(;)특수&amp; &lt; &gt; XML 문자를 포함하지 마십시오. 이는 Azure의 제한이 아니라 스크립트를 작성한 방식의 제한입니다.

    예를 들어 "fixitdemo"라는 웹 앱을 만들고 "Passw0rd1"의 SQL Server 관리자 암호를 사용하려는 경우 다음 명령을 입력할 수 있습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    이름은 azurewebsites.net 도메인에서 고유해야 하며 암호가 암호 복잡성에 대한 SQL Database 요구 사항을 충족해야 합니다. (Passw0rd1 예제는 요구 사항을 충족합니다.)

    명령은 "로 시작합니다. \". 스크립트의 악의적인 실행을 방지하려면 Windows PowerShell에서 스크립트를 실행할 때 스크립트 파일에 대한 정규화된 경로를 제공해야 합니다. 점을 사용하여 현재 디렉터리(")를 나타낼\"수 있습니다. 또는 다음과 같이 정규화된 경로를 제공합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    스크립트에 대한 자세한 내용은 `Get-Help` cmdlet을 사용합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    [의 `Detailed`에서 `Full`, `Parameters` `Examples`

    스크립트가 실패하거나 "새-AzureWebsite : 호출 집합-AzureSubscription 및 Select-AzureSubscription 첫 번째"와 같은 오류를 생성하는 경우 Azure PowerShell의 구성을 완료하지 않았을 수 있습니다.

    스크립트가 완료되면 Azure 관리 포털을 사용하여 [모든](automate-everything.md) 자동화 장과 같이 생성된 리소스를 볼 수 있습니다.
10. 새 Azure 환경에 FixIt 프로젝트를 배포하려면 *AzureWebsite.ps1* 스크립트를 사용합니다. 예를 들어:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    배포가 완료되면 브라우저가 Azure에서 실행되는 Fix It으로 열립니다.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell 스크립트 문제 해결

이러한 스크립트를 실행할 때 발생하는 가장 일반적인 오류는 사용 권한과 관련이 있습니다. `Add-AzureAccount` 동일한 `Import-AzurePublishSettingsFile` Azure 구독에 사용했는지 확인하고 성공했는지 확인합니다. 성공한 `Add-AzureAccount` 경우에도 다시 실행해야 할 수 있습니다. 추가된 `Add-AzureAccount` 권한은 12시간 만에 만료됩니다.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>개체 참조가 개체의 인스턴스로 설정되지 않았습니다.

스크립트가 "개체 참조가 개체의 인스턴스로 설정되지 않음"과 같은 오류를 반환하는 경우 Windows PowerShell은 처리할 개체를 찾을 `Add-AzureAccount` 수 없습니다(null 참조 예외)는 cmdlet을 실행하고 스크립트를 다시 시도합니다.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>내부 오류: 서버에 내부 오류가 발생했습니다.

cmdlet은 `New-AzureWebsite` azurewebsites.net 도메인에서 이름이 고유하지 않은 경우 내부 오류를 반환합니다. 오류를 해결하려면 *New-AzureWebsiteEnv.ps1의*이름 매개 변수에 있는 이름에 대해 다른 값을 사용합니다.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>스크립트 다시 시작

"스크립트가 완료되었습니다" 메시지를 인쇄하기 전에 실패했기 때문에 *New-AzureWebsiteEnv.ps1* 스크립트를 다시 시작해야 하는 경우 스크립트가 중지되기 전에 만든 리소스를 삭제할 수 있습니다. 예를 들어 스크립트가 이미 ContosoFixItDemo 웹 앱을 만든 다음 동일한 이름으로 스크립트를 다시 실행하는 경우 이름이 사용 중이기 때문에 스크립트가 실패합니다.

스크립트가 중지되기 전에 만든 리소스를 확인하려면 다음 cmdlet을 사용합니다.

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: 이 cmdlet을 실행하려면 데이터베이스 `Get-AzureSqlDatabase`서버 이름을 다음으로 파이프합니다.`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

이러한 리소스를 삭제하려면 다음 명령을 사용합니다. 데이터베이스 서버를 삭제하면 서버와 연결된 데이터베이스가 자동으로 삭제됩니다.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스에 큐 처리를 사용하여 앱을 배포하는 방법

큐를 사용하려면 MyFixIt\Web.config 파일에서 다음을 변경합니다. 에서 `appSettings`값 `UseQueues` "true"로 변경합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

그런 다음 [앞에서](#deploybase)설명한 대로 Azure 앱 서비스의 웹 앱에 MVC 응용 프로그램을 배포합니다.

다음으로 새 Azure 클라우드 서비스를 만듭니다. Fix It 앱에 포함된 스크립트는 클라우드 서비스를 만들거나 배포하지 않으므로 이를 위해 Azure 포털을 사용해야 합니다. 포털에서 **새** -- **계산** - **클라우드 서비스** -- **빠른 만들기를**클릭한 다음 URL과 데이터 센터 위치를 입력합니다. 웹 앱을 배포한 것과 동일한 데이터 센터를 사용합니다.

![](the-fix-it-sample-application/_static/image1.png)

클라우드 서비스를 배포하려면 일부 구성 파일을 업데이트해야 합니다.

MyFixIt.WorkerRole\app.config에서 아래에서 `connectionStrings` `appdb` 연결 문자열의 값을 SQL Database의 실제 연결 문자열로 바꿉습니다. 포털에서 연결 문자열을 얻을 수 있습니다. 포털에서 - **ADO .Net, ODBC, PHP 및 JDBC에 대한 SQL** - **Databaseappdb**보기 SQL 데이터베이스 연결 문자열을 클릭합니다. **SQL Databases** ADO.NET 연결 문자열을 복사하고 app.config 파일에 값을 붙여 넣습니다. "여기에서\_암호{}"를\_데이터베이스 암호로 바꿉습니다. 스크립트를 사용하여 MVC 앱을 배포했다고 가정하면 `SqlDatabasePassword` 스크립트 매개 변수에 데이터베이스 암호를 지정했습니다.

결과는 다음과 같아야 합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

동일한 MyFixIt.WorkerRole\app.config 파일에서 `appSettings`Azure 저장소 계정에 대한 두 자리 표시자 값을 대체합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

포털에서 액세스 키를 얻을 수 있습니다. [저장소 계정을 관리하는 방법을](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)참조하십시오.

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg에서 Azure 저장소 계정에 대해 동일한 두 자리 표시자 값을 바꿉습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

이제 클라우드 서비스를 배포할 준비가 되었습니다. 솔루션 탐색에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시를**선택합니다. 자세한 내용은 [이 자습서의](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2부에 있는["Azure에 응용 프로그램 배포"를](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)참조하십시오.

> [!div class="step-by-step"]
> [이전](more-patterns-and-guidance.md)
