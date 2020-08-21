---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '부록: Fix It 샘플 응용 프로그램 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs'
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 549d1513279190ae5abe87c59a48e1caa1cfa5f7
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702935"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>부록: Fix It 샘플 응용 프로그램 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

Azure를 사용 하 여 실제 클라우드 앱 빌드에 대 한이 부록에는 다운로드할 수 있는 Fix It 샘플 응용 프로그램에 대 한 추가 정보를 제공 하는 다음 섹션이 포함 되어 있습니다.

- [알려진 문제](#knownissues)
- [모범 사례](#bestpractices)
- [로컬 컴퓨터의 Visual Studio에서 앱을 실행 하는 방법](#run-in-vs)
- [Windows PowerShell 스크립트를 사용 하 여 Azure App Service Web Apps에 기본 앱을 배포 하는 방법](#deploybase)
- [Windows PowerShell 스크립트 문제 해결](#troubleshooting)
- [큐 처리를 사용 하 여 앱을 배포 하 여 Web Apps 및 Azure 클라우드 서비스를 Azure App Service 하는 방법](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>알려진 문제

이 설명서에 제공 된 패턴 중 일부를 가능한 한 간단 하 게 보여 주기 위해 Fix It 앱이 원래 개발 되었습니다. 그러나이 문서에서는 실제 앱을 빌드하는 데 대 한 정보를 제공 하기 때문에 릴리스 소프트웨어에 대해 수행 했던 것과 비슷한 검토 및 테스트 프로세스에 대 한 수정 It 코드를 제공 합니다. 모든 실제 응용 프로그램에서와 마찬가지로 몇 가지 문제가 발견 되었으며 일부는 수정 하 고 그 중 일부는 이후 릴리스로 연기 했습니다.

다음 목록은 프로덕션 응용 프로그램에서 해결 해야 하는 문제를 포함 하지만, 한 가지 이유 또는 Fix It 샘플 응용 프로그램의 초기 릴리스에서 해결 하지 않기로 결정 했습니다.

### <a name="security"></a>보안

- 존재 하지 않는 소유자에 게 작업을 할당할 수 없는지 확인 합니다.
- 사용자가 만들었거나 할당 한 작업만 보고 수정할 수 있는지 확인 합니다.
- 로그인 페이지 및 인증 쿠키에 HTTPS를 사용 합니다.
- 인증 쿠키에 대 한 시간 제한을 지정 합니다.

### <a name="input-validation"></a>입력 유효성 검사

일반적으로 프로덕션 앱은 Fix It 앱 보다 더 많은 입력 유효성 검사를 수행 합니다. 예를 들어 업로드에 허용 되는 이미지 크기/이미지 파일 크기를 제한 해야 합니다.

### <a name="administrator-functionality"></a>관리자 기능

관리자는 기존 태스크에 대 한 소유권을 변경할 수 있어야 합니다. 예를 들어 관리 액세스를 사용 하도록 설정 하지 않은 경우 작업을 유지 관리할 수 있는 권한이 없는 작업의 작성자는 회사를 떠날 수 있습니다.

### <a name="queue-message-processing"></a>큐 메시지 처리

Fix It 앱에서 큐 메시지 처리는 최소한의 코드를 사용 하 여 큐 중심 작업 패턴을 보여 주기 위해 간단 하 게 설계 되었습니다. 이 간단한 코드는 실제 프로덕션 응용 프로그램에는 적합 하지 않습니다.

- 이 코드는 각 큐 메시지가 한 번만 처리 되는 것을 보장 하지 않습니다. 큐에서 메시지를 받는 경우 다른 큐 수신기에 메시지가 표시 되지 않는 시간 제한 기간이 있습니다. 메시지를 삭제 하기 전에 제한 시간이 만료 되 면 메시지가 다시 표시 됩니다. 따라서 작업자 역할 인스턴스에서 메시지를 처리 하는 데 시간이 오래 걸리는 경우에는 이론적으로 동일한 메시지를 두 번 처리 하 여 데이터베이스에서 중복 작업을 수행할 수 있습니다. 이 문제에 대 한 자세한 내용은 [Azure Storage 큐 사용](https://msdn.microsoft.com/library/ff803365.aspx#sec7)을 참조 하세요.
- 큐 폴링 논리는 메시지 검색을 일괄 처리 하 여 더 비용 효율적일 수 있습니다. [Cloudqueue. GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)을 호출할 때마다 트랜잭션 비용이 발생 합니다. 대신, 단일 트랜잭션에서 여러 메시지를 가져오는 [GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (복수형의 ')를 호출할 수 있습니다. Azure Storage 큐에 대 한 트랜잭션 비용은 매우 낮으므로 대부분의 시나리오에서 비용에 미치는 영향은 그다지 중요 하지 않습니다.
- 큐 메시지 처리 코드에서 루프를 사용 하면 다중 코어 Vm을 효율적으로 활용 하지 않는 CPU 선호도가 발생 합니다. 더 나은 디자인은 작업 병렬 처리를 사용 하 여 여러 비동기 작업을 병렬로 실행 합니다.
- 큐 메시지 처리에는 기초적인 예외 처리만 있습니다. 예를 들어 코드는 [포이즌 메시지](https://msdn.microsoft.com/library/ms789028.aspx)를 처리 하지 않습니다. 메시지 처리 시 예외가 발생 하는 경우 오류를 기록 하 고 메시지를 삭제 해야 합니다. 그렇지 않으면 작업자 역할은 다시 처리를 시도 하 고 루프가 무기한 계속 됩니다.

### <a name="sql-queries-are-unbounded"></a>SQL 쿼리는 제한 되지 않습니다.

현재 수정 It 코드는 인덱스 페이지에 대 한 쿼리가 반환할 수 있는 행 수에 제한이 없습니다. 많은 양의 작업을 데이터베이스에 입력 하는 경우 수신 된 결과 목록의 크기가 성능 문제를 일으킬 수 있습니다. 이 솔루션은 페이징을 구현 하는 것입니다. 예제를 보려면 [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)을 참조 하세요.

### <a name="view-models-recommended"></a>모델 보기 권장

Fix It 앱은 FixItTask 엔터티 클래스를 사용 하 여 컨트롤러와 뷰 간에 정보를 전달 합니다. 모범 사례는 보기 모델을 사용 하는 것입니다. 도메인 모델 (예: FixItTask 엔터티 클래스)은 데이터를 지 원하는 데 필요한 항목을 중심으로 디자인 되었으며, 데이터를 표시 하기 위해 뷰 모델을 디자인할 수 있습니다. 자세한 내용은 [12 ASP.NET MVC 모범 사례](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)를 참조 하세요.

### <a name="secure-image-blob-recommended"></a>보안 이미지 blob 권장

Fix It 앱은 업로드 된 이미지를 공개로 저장 합니다. 즉, URL을 찾는 사람이 이미지에 액세스할 수 있습니다. 이미지는 공용이 아닌 보안을 설정할 수 있습니다.

### <a name="no-powershell-automation-scripts-for-queues"></a>큐에 대 한 PowerShell automation 스크립트가 없습니다.

샘플 PowerShell 자동화 스크립트는 전체 Azure App Service Web Apps에서 실행 되는 Fix의 기본 버전용으로 작성 되었습니다. 웹 앱을 설정 하 고 배포 하는 데 필요한 스크립트를 제공 하지 않았습니다. 큐 처리에 필요한 클라우드 서비스 환경을 제공 합니다.

### <a name="special-handling-for-html-codes-in-user-input"></a>사용자 입력의 HTML 코드에 대 한 특수 처리

ASP.NET는 악의적인 사용자가 사용자 입력 텍스트 상자에 스크립트를 입력 하 여 사이트 간 스크립팅 공격을 시도할 수 있는 여러 가지 방법을 자동으로 방지 합니다. 그리고 `DisplayFor` 작업 제목과 메모를 표시 하는 데 사용 되는 MVC 도우미는 브라우저에 보내는 값을 자동으로 HTML 인코딩합니다. 그러나 프로덕션 앱에서는 추가 측정을 수행 하는 것이 좋습니다. 자세한 내용은 [ASP.NET의 요청 유효성 검사](https://msdn.microsoft.com/library/hh882339.aspx)를 참조 하세요.

<a id="bestpractices"></a>
## <a name="best-practices"></a>모범 사례

다음은 코드 검토에서 검색 된 후 수정 된 문제 및 Fix It 앱의 원래 버전에 대 한 테스트입니다. 일부는 코드를 신속 하 게 작성 하 고 릴리스 소프트웨어를 사용 하기 위한 것이 아니라 원래 코드 작성자 있는지 특정 모범 사례를 인식 하지 못하기 때문에 발생 했습니다. 웹 앱을 개발 하는 다른 사용자에 게 도움이 될 수 있는이 검토 및 테스트에서 배운 내용이 있는 경우 여기에서 문제를 나열 하 고 있습니다.

### <a name="dispose-the-database-repository"></a>데이터베이스 리포지토리를 삭제 합니다.

`FixItTaskRepository`클래스는 Entity Framework 인스턴스를 삭제 해야 합니다 `DbContext` . 클래스에서를 구현 하 여이 작업을 수행 했습니다 `IDisposable` `FixItTaskRepository` .

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac는 인스턴스를 자동으로 삭제 `FixItTaskRepository` 하므로 명시적으로 삭제할 필요가 없습니다.

또 다른 옵션은 `DbContext` 에서 멤버 변수를 제거 하 `FixItTaskRepository` 고 대신 `DbContext` 문 내에서 각 리포지토리 메서드 내에 지역 변수를 만드는 `using` 것입니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>DI를 사용 하 여 단일 항목를 등록 합니다.

클래스 및 클래스의 인스턴스는 하나만 `PhotoService` `Logger` 필요 하므로 이러한 클래스는 *DependenciesConfig.cs*의 [종속성 주입에 대 한 단일 인스턴스로 등록](https://code.google.com/p/autofac/wiki/InstanceScope) 되어야 합니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>보안: 사용자에 게 오류 정보를 표시 하지 않음

원래 Fix It 앱에는 일반 오류 페이지가 없으며 모든 예외를 UI로 버블링 하므로 데이터베이스 연결 오류와 같은 일부 예외 때문에 브라우저에 전체 스택 추적이 표시 될 수 있습니다. 자세한 오류 정보는 악의적인 사용자의 공격을 쉽게 수행할 수 있습니다. 해결 방법은 예외 정보를 기록 하 고 오류 세부 정보를 포함 하지 않는 오류 페이지를 사용자에 게 표시 하는 것입니다. Fix It 앱은 이미 로깅 되었으며 오류 페이지를 표시 하기 위해 `<customErrors mode=On>` Web.config 파일에 추가 되었습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

이 경우 기본적으로 오류에 대해 *Views\Shared\Error.cshtml* 가 표시 됩니다. 오류를 사용자 지정할 수 있습니다 *. cshtml* 또는 고유한 오류 페이지 보기를 만들고 특성을 추가 `defaultRedirect` 합니다. 특정 오류에 대해 서로 다른 오류 페이지를 지정할 수도 있습니다.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>보안: 작성자만 작업을 편집할 수 있습니다.

대시보드 인덱스 페이지에는 로그온 한 사용자가 만든 작업만 표시 되지만 악의적인 사용자가 다른 사용자의 작업에 대 한 ID를 사용 하 여 URL을 만들 수 있습니다. 이 경우 404을 반환 하는 코드를 *DashboardController.cs* 에 추가 했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>예외를 무시 안 함

원본 Fix It 앱은 SQL 쿼리에서 발생 한 예외를 기록한 후에만 null을 반환 했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

이렇게 하면 쿼리가 성공 했지만 행을 반환 하지 않은 것 처럼 사용자에 게 표시 됩니다. 솔루션은 catch 및 로깅 후 예외를 다시 throw 하는 것입니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>작업자 역할의 모든 예외 Catch

작업자 역할에서 처리 되지 않은 예외가 발생 하면 VM이 재활용 되므로 try-catch 블록에서 수행 하는 모든 작업을 래핑하고 모든 예외를 처리 하려고 합니다.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>엔터티 클래스에서 문자열 속성의 길이 지정

간단한 코드를 표시 하기 위해 원래 버전의 Fix It 앱은 FixItTask 엔터티의 필드에 대해 길이를 지정 하지 않았기 때문에 데이터베이스에서 varchar (max)로 정의 되었습니다. 결과적으로 UI에는 거의 모든 양의 입력이 허용 됩니다. Length를 지정 하면 웹 페이지의 사용자 입력과 데이터베이스의 열 크기에 모두 적용 되는 제한이 설정 됩니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Private 멤버를 변경할 수 없는 경우 readonly로 표시 합니다.

예를 들어 클래스에서 `DashboardController` 인스턴스는 `FixItTaskRepository` 생성 되며 변경 될 것으로 예상 되지 않으므로이를 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)로 정의 했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>List를 사용 합니다. 목록 대신 Any () Count () &gt; 0

목록에 있는 항목 중 하나 이상이 지정 된 조건에 맞는지 확인 하는 것이 가장 중요 한 경우에는 [모든 메서드를](https://msdn.microsoft.com/library/bb534972.aspx) 사용 합니다 .이는 조건에 따라 항목이 발견 되는 즉시 반환 되는 반면, 메서드는 `Count` 항상 모든 항목을 반복 해야 하는 경우에 해당 합니다. 대시보드 *인덱스 cshtml* 파일에는 원래 다음 코드가 있습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

이를 다음과 같이 변경 했습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC 도우미를 사용 하 여 MVC 뷰에서 Url 생성

홈 페이지의 **Fix It 만들기** 단추에 대해 fix it 앱은 앵커 요소를 하드 코딩 했습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

이와 같은 보기/작업 링크의 경우 [Url. action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 도우미를 사용 하는 것이 좋습니다. 예를 들면 다음과 같습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>작업자 역할에서 Sleep 대신 작업을 사용 합니다.

새 프로젝트 템플릿은 `Thread.Sleep` 작업자 역할에 대 한 샘플 코드를 만들지만 스레드를 절전 모드로 전환 하면 스레드 풀에서 불필요 한 추가 스레드를 생성할 수 있습니다. 대신, [Delay](https://msdn.microsoft.com/library/hh139096.aspx) 를 사용 하 여이를 방지할 수 있습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>비동기 void 방지

비동기 메서드가 값을 반환 하지 않아도 되는 경우 대신 형식을 반환 `Task` `void` 합니다.

이 예제는 클래스에서 가져온 것입니다 `FixItQueueManager` .

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

`async void`최상위 이벤트 처리기에만를 사용 해야 합니다. 로 메서드를 정의 하는 경우 호출자는 메서드를 대기 `async void` 하거나 메서드에서 throw 하는 예외를 catch **할** 수 없습니다. 자세한 내용은 [비동기 프로그래밍의 모범 사례](https://msdn.microsoft.com/magazine/jj991977.aspx)를 참조 하세요.

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>취소 토큰을 사용 하 여 작업자 역할 루프에서 중단

일반적으로 작업자 역할의 **Run** 메서드는 무한 루프를 포함 합니다. 작업자 역할을 중지 하면 [Roleentrypoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 메서드가 호출 됩니다. 이 메서드를 사용 하 여 **실행** 메서드 내에서 수행 되는 작업을 취소 하 고 정상적으로 종료 해야 합니다. 그렇지 않으면 작업이 작업 중간에 종료 될 수 있습니다.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>자동 MIME 스니핑 프로시저 옵트아웃 (Opt out)

Internet Explorer에서 웹 서버에 지정 된 형식과 다른 MIME 형식을 보고 하는 경우도 있습니다. 예를 들어, Internet Explorer에서 HTTP 응답 헤더 Content-type과 함께 배달 된 파일의 HTML 콘텐츠를 찾으면 (텍스트/일반) Internet Explorer는 콘텐츠를 HTML로 렌더링 해야 함을 결정 합니다. 아쉽게도이 "MIME 스니핑"은 신뢰할 수 없는 콘텐츠를 호스트 하는 서버에 대 한 보안 문제를 일으킬 수도 있습니다. Internet Explorer 8은이 문제를 해결 하기 위해 MIME 형식 확인 코드를 다양 하 게 변경 하 고 응용 프로그램 개발자에 게 MIME 검사를 [옵트아웃 (opt out)](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)할 수 있도록 합니다. 다음 코드가 *Web.config* 파일에 추가 되었습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>묶음 및 축소 사용

Visual Studio에서 새 웹 프로젝트를 만들 때 JavaScript 파일의 묶음 및 축소는 기본적으로 사용 되지 않습니다. BundleConfig.cs에 코드 줄을 추가 했습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>인증 쿠키에 대 한 만료 시간 제한 설정

기본적으로 인증 쿠키는 2 주 후에 만료 됩니다. 시간이 짧으면 더 안전 합니다. *StartupAuth.cs*에서이 설정을 변경할 수 있습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>로컬 컴퓨터의 Visual Studio에서 앱을 실행 하는 방법

Fix It 앱을 실행 하는 방법에는 두 가지가 있습니다.

- 새 작업을 SQL 데이터베이스에 직접 기록 하는 기본 응용 프로그램을 실행 합니다.
- 큐와 백 엔드 서비스를 사용 하 여 응용 프로그램을 실행 하 여 작업을 만듭니다. 큐 패턴은 [큐 중심 작업 패턴](queue-centric-work-pattern.md)장에 설명 되어 있습니다.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>기본 응용 프로그램 실행

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 설치합니다.
2. [Visual Studio 용 AZURE SDK for .net](https://azure.microsoft.com/downloads/)을 설치 합니다.
3. [MSDN 코드 갤러리](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)에서 .zip 파일을 다운로드 합니다.
4. 파일 탐색기에서 .zip 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 한 다음 속성 창 차단 해제를 클릭 합니다.
5. 파일의 압축을 풉니다.
6. .Sln 파일을 두 번 클릭 하 여 Visual Studio를 시작 합니다.
7. **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭 합니다.
8. 패키지 관리자 콘솔 (PMC)에서 복원을 클릭 합니다.
9. Visual Studio를 끝냅니다.
10. [Azure Storage 에뮬레이터](/azure/storage/common/storage-use-emulator)를 시작 합니다.
11. Visual Studio를 다시 시작 하 고 이전 단계에서 닫은 솔루션 파일을 엽니다.
12. FixIt 프로젝트가 시작 프로젝트로 설정 되어 있는지 확인 한 다음 CTRL + F5 키를 눌러 프로젝트를 실행 합니다.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>큐 처리를 사용 하 여 응용 프로그램 실행

1. [기본 응용 프로그램을 실행](#runbase)하는 지침에 따라 브라우저를 닫고 Visual Studio를 닫습니다.
2. 관리자 권한으로 Visual Studio를 시작 합니다. (Azure 계산 에뮬레이터를 사용 하 고 관리자 권한이 필요 합니다.)
3. *Myfixit* 프로젝트 (웹 프로젝트)의 응용 프로그램 *Web.config* 파일에서의 값을 `appSettings/UseQueues` "true"로 변경 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. [Azure Storage 에뮬레이터가](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 아직 실행 되 고 있지 않은 경우 다시 시작 합니다.
5. FixIt 웹 프로젝트 및 MyFixItCloudService 프로젝트를 동시에 실행 합니다.

    Visual Studio 사용:

   1. F 5 **를 눌러 FixIt 프로젝트를 실행** 합니다.
   2. **솔루션 탐색기**에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **디버그**  >  **새 인스턴스 시작**을 클릭 합니다.

    웹에 Visual Studio 2013 Express 사용:

   3. 솔루션 탐색기에서 FixIt 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.
   4. **여러 개의 시작 프로젝트**를 선택 합니다.
   5. MyFixIt 및 MyFixItCloudService의 **작업** 드롭다운 목록에서 **시작**을 선택 합니다.
   6. **확인**을 클릭합니다.
   7. **F5** 키를 눌러 두 프로젝트를 실행합니다.

      MyFixItCloudService 프로젝트를 실행 하면 Visual Studio에서 Azure 계산 에뮬레이터를 시작 합니다. 방화벽 구성에 따라 에뮬레이터를 방화벽을 통해 허용 해야 할 수도 있습니다.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell 스크립트를 사용 하 여 Azure App Service Web Apps에 기본 앱을 배포 하는 방법

[모두 자동화](automate-everything.md) 패턴을 설명 하기 위해 Azure에서 환경을 설정 하 고 프로젝트를 새 환경에 배포 하는 스크립트를 사용 하 여 Fix It 앱을 제공 합니다. 다음 지침에서는 스크립트를 사용 하는 방법을 설명 합니다.

큐를 사용 하지 않고 Azure에서 실행 하려는 경우 큐를 사용 하 여 로컬로 실행 하도록 변경 하려면 다음 지침을 수행 하기 전에 UseQueues appSetting 값을 다시 false로 설정 해야 합니다.

이 지침에서는 수정 It 솔루션을 로컬로 다운로드 하 여 실행 한 것으로 가정 하 고 Azure 계정이 있거나 관리할 수 있는 Azure 구독이 있다고 가정 합니다.

1. **Azure PowerShell** 콘솔을 설치 합니다. 자세한 내용은 [Azure PowerShell 설치 및 구성법](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)을 참조하세요.

    이 사용자 지정 콘솔은 Azure 구독과 함께 작동 하도록 구성 됩니다. Azure 모듈은 *Program Files* 디렉터리에 설치 되며 Azure PowerShell 콘솔을 사용할 때마다 자동으로 가져옵니다.

    Windows PowerShell ISE와 같은 다른 호스트 프로그램에서 작업 하려면 [import-module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet을 사용 하 여 azure 모듈을 가져오거나 azure 모듈의 명령을 사용 하 여 모듈의 자동 가져오기를 트리거하는 것이 좋습니다.
2. **관리자 권한으로 실행** 옵션을 사용 하 여 Azure PowerShell를 시작 합니다.
3. [Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet을 실행 하 여 Azure PowerShell 실행 정책을로 설정 `RemoteSigned` 합니다. **Y** (예의 경우)를 입력 하 여 정책 변경을 완료 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    이 설정을 사용 하면 디지털 서명 되지 않은 로컬 스크립트를 실행할 수 있습니다. 실행 정책을로 설정할 수도 있습니다. 이렇게 하면 `Unrestricted` 나중에 차단 해제 단계가 필요 하지 않습니다. 하지만 보안상의 이유로이 방법은 권장 되지 않습니다.
4. Cmdlet을 실행 `Add-AzureAccount` 하 여 계정에 대 한 자격 증명으로 PowerShell을 설정 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    이러한 자격 증명은 일정 기간 후에 만료 되므로 cmdlet을 다시 실행 해야 합니다 `Add-AzureAccount` . 이 e-learning을 작성 하는 동안 자격 증명의 만료 시간 제한은 12 시간입니다.
5. 구독이 여러 개인 경우 Get-azuresubscription cmdlet을 사용 하 여 테스트 환경을 만들려는 구독을 지정 합니다.
6. 및 cmdlet을 사용 하 여 동일한 Azure 구독에 대 한 관리 인증서를 가져옵니다 `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` . 이 cmdlet 중 첫 번째 cmdlet은 인증서 파일을 다운로드 하 고, 두 번째 cmdlet은 파일을 가져오기 위해 해당 파일의 위치를 지정 합니다. > [!IMPORTANT]
   > 다운로드 한 파일은 Azure 서비스를 관리 하는 데 사용할 수 있는 인증서를 포함 하므로 안전한 위치에 보관 하거나 작업을 수행 하는 경우 삭제 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    인증서는 SQL Database 서버에서 방화벽 규칙을 설정 하기 위해 개발 컴퓨터의 IP 주소를 검색 하는 REST API 호출에 사용 됩니다.
7. [집합 위치](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (별칭은 `cd` , `chdir` 및)을 실행 하 여 `sl` 스크립트가 포함 된 디렉터리로 이동 합니다. (It 솔루션 수정 폴더의 *Automation* 폴더에 있습니다.) 디렉터리 이름에 공백이 포함 된 경우 경로를 따옴표로 묶습니다. 예를 들어 디렉터리로 이동 하려면 `c:\Sample Apps\FixIt\Automation` 다음 명령을 입력 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell에서 이러한 스크립트를 실행할 수 있도록 하려면 [파일 차단 해제](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet을 사용 합니다. 스크립트는 인터넷에서 다운로드 되었으므로 차단 됩니다.

    > [!WARNING]
    > 보안-스크립트나 실행 파일을 실행 하기 전에 `Unblock-File` 메모장에서 파일을 열고 명령을 검사 하 여 악성 코드가 포함 되지 않았는지 확인 합니다.

    예를 들어 다음 명령은 `Unblock-File` 현재 디렉터리의 모든 스크립트에서 cmdlet을 실행 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 기본 (큐 처리 없음)에 대 한 웹 앱을 만들려면 It 앱을 수정 하 고 환경 생성 스크립트를 실행 합니다.

    필수 `Name` 매개 변수는 데이터베이스의 이름을 지정 하며 스크립트에서 만드는 저장소 계정에도 사용 됩니다. 이름은 azurewebsites.net 도메인 내에서 전역적으로 고유 해야 합니다. Fixit 또는 Test와 같이 고유 하지 않은 이름을 지정 하거나 (예: fixitdemo) `New-AzureWebsite` cmdlet은 충돌을 보고 하는 내부 오류로 인해 실패 합니다. 이 스크립트는 이름을 모두 소문자로 변환 하 여 웹 앱, 저장소 계정 및 데이터베이스의 이름 요구 사항을 준수 합니다.

    필수 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 생성 되는 관리자 계정의 암호를 지정 합니다. 암호에 특수 XML 문자를 포함 하지 않습니다 ( &amp; &lt; &gt; ;). 이는 스크립트가 작성 된 방식에 대 한 제한 사항이 며 Azure의 제한이 아닙니다.

    예를 들어 "fixitdemo" 라는 웹 앱을 만들고 SQL Server 관리자 암호 "Passw0rd1"를 사용 하려는 경우 다음 명령을 입력할 수 있습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    이름은 azurewebsites.net 도메인에서 고유 해야 하며 암호 복잡성에 대 한 SQL Database 요구 사항을 충족 해야 합니다. Passw0rd1 예제는 요구 사항을 충족 합니다.

    명령은 ". .로 시작 합니다. \" 악의적인 스크립트 실행을 방지 하기 위해 Windows PowerShell을 사용 하려면 스크립트를 실행할 때 스크립트 파일의 정규화 된 경로를 제공 해야 합니다. 점을 사용 하 여 현재 디렉터리 (".)를 나타낼 수 있습니다. \" 또는 다음과 같이 정규화 된 경로를 제공 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    스크립트에 대 한 자세한 내용을 보려면 cmdlet을 사용 하십시오 `Get-Help` .

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    `Detailed` `Full` `Parameters` `Examples` Get-help cmdlet의,, 및 매개 변수를 사용 하 여 반환 되는 도움말을 필터링 할 수 있습니다.

    스크립트가 실패 하거나 오류를 생성 하는 경우 (예: "AzureWebsite: Call Get-azuresubscription and Get-azuresubscription first") Azure PowerShell의 구성을 완료 하지 않았을 수 있습니다.

    스크립트가 완료 되 면 Azure 관리 포털를 사용 하 여 생성 된 리소스를 볼 수 있습니다 .이에 대해서는 [모두 자동화](automate-everything.md) 단원을 참조 하세요.
10. 새 Azure 환경에 FixIt 프로젝트를 배포 하려면 *AzureWebsite.ps1* 스크립트를 사용 합니다. 예를 들면 다음과 같습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    배포가 완료 되 면 브라우저가 Azure에서 실행 되는 수정 사항으로 열립니다.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell 스크립트 문제 해결

이러한 스크립트를 실행할 때 발생 하는 가장 일반적인 오류는 사용 권한과 관련이 있습니다. 및가 성공적으로 실행 되었으며 `Add-AzureAccount` `Import-AzurePublishSettingsFile` 동일한 Azure 구독에 사용 했는지 확인 합니다. `Add-AzureAccount`가 성공적으로 수행 된 경우에도 다시 실행 해야 할 수 있습니다. 에 의해 추가 된 사용 권한은 `Add-AzureAccount` 12 시간 후에 만료 됩니다.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>개체 참조가 개체의 인스턴스로 설정되지 않았습니다.

스크립트에서 "개체 참조가 개체의 인스턴스로 설정 되지 않았습니다."와 같은 오류를 반환 하는 경우 Windows PowerShell에서 처리할 개체를 찾을 수 없음을 의미 합니다 .이는 null 참조 예외입니다 .이 경우에는 cmdlet을 실행 `Add-AzureAccount` 하 고 스크립트를 다시 시도 합니다.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: 서버에서 내부 오류가 발생 했습니다.

`New-AzureWebsite`Azurewebsites.net 도메인에서 이름이 고유 하지 않은 경우 cmdlet은 내부 오류를 반환 합니다. 오류를 해결 하려면 *New-AzureWebsiteEnv.ps1*의 name 매개 변수에 있는 이름에 대해 다른 값을 사용 합니다.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>스크립트 다시 시작

*New-AzureWebsiteEnv.ps1* 스크립트가 "스크립트가 완료 되었습니다." 라는 메시지를 인쇄 하기 전에 실패 하 여 다시 시작 해야 하는 경우 스크립트가 중지 되기 전에 만든 리소스를 삭제할 수 있습니다. 예를 들어 스크립트가 ContosoFixItDemo 웹 앱을 이미 만들었고 동일한 이름으로 스크립트를 다시 실행 하는 경우에는 이름이 사용 중 이므로 스크립트가 실패 합니다.

스크립트가 중지 되기 전에 만든 리소스를 확인 하려면 다음 cmdlet을 사용 합니다.

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`:이 cmdlet을 실행 하려면 데이터베이스 서버 이름을 `Get-AzureSqlDatabase` 다음과 같이 파이프 합니다.   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

이러한 리소스를 삭제 하려면 다음 명령을 사용 합니다. 데이터베이스 서버를 삭제 하면 해당 서버와 연결 된 데이터베이스가 자동으로 삭제 됩니다.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>큐 처리를 사용 하 여 앱을 배포 하 여 Web Apps 및 Azure 클라우드 서비스를 Azure App Service 하는 방법

큐를 사용 하도록 설정 하려면 MyFixIt\Web.config 파일에서 다음과 같이 변경 합니다. 에서 `appSettings` 의 값을 `UseQueues` "true"로 변경 합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

그런 다음 [앞](#deploybase)에서 설명한 대로 AZURE APP SERVICE에서 MVC 응용 프로그램을 웹 앱에 배포 합니다.

다음으로 새 Azure 클라우드 서비스를 만듭니다. Fix It 앱에 포함 된 스크립트는 클라우드 서비스를 만들거나 배포 하지 않으므로이를 위해 Azure Portal를 사용 해야 합니다. 포털에서 **새로 만들기**  --  **계산** – **클라우드 서비스**  --  **빠른 생성**을 클릭 하 고 URL 및 데이터 센터 위치를 입력 합니다. 웹 앱을 배포한 동일한 데이터 센터를 사용 합니다.

![](the-fix-it-sample-application/_static/image1.png)

클라우드 서비스를 배포 하려면 먼저 일부 구성 파일을 업데이트 해야 합니다.

MyFixIt.WorkerRole\app.config의에서 `connectionStrings` 연결 문자열의 값을 `appdb` SQL Database에 대 한 실제 연결 문자열로 바꿉니다. 포털에서 연결 문자열을 가져올 수 있습니다. 포털에서 **SQL 데이터베이스**  -  **appdb**  -  **뷰 SQL Database ADO .net, ODBC, PHP 및 JDBC에 대 한 연결 문자열**을 클릭 합니다. ADO.NET 연결 문자열을 복사 하 고 값을 app.config 파일에 붙여넣습니다. "{Your \_ password \_ }"를 데이터베이스 암호로 바꿉니다. (스크립트를 사용 하 여 MVC 앱을 배포 했다고 가정 하 고 스크립트 매개 변수에서 데이터베이스 암호를 지정 `SqlDatabasePassword` 했습니다.)

결과는 다음과 같습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

동일한 MyFixIt.WorkerRole\app.config 파일의에서 `appSettings` Azure storage 계정에 대 한 두 자리 표시자 값을 바꿉니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

포털에서 선택 키를 가져올 수 있습니다. [저장소 계정을 관리 하는 방법을](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)참조 하세요.

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg에서 Azure storage 계정에 대해 동일한 두 자리 표시자 값을 바꿉니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

이제 클라우드 서비스를 배포할 준비가 되었습니다. 솔루션 탐색기에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다. 자세한 내용은 [이 자습서](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)의 2 부에 있는 "[Azure에 응용 프로그램 배포](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"를 참조 하세요.

> [!div class="step-by-step"]
> [이전](more-patterns-and-guidance.md)
