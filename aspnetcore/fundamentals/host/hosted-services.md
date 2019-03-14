---
title: ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업
author: guardrex
description: ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업을 구현하는 방법을 배웁니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/25/2019
uid: fundamentals/host/hosted-services
ms.openlocfilehash: d10a335429752c1a52c1b3619adecc41725a819a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030190"
---
# <a name="background-tasks-with-hosted-services-in-aspnet-core"></a>ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core에서 백그라운드 작업은 *호스팅되는 서비스*로 구현될 수 있습니다. 호스티드 서비스는 <xref:Microsoft.Extensions.Hosting.IHostedService> 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다. 이 토픽에서는 세 가지 호스팅되는 서비스 예제를 제공합니다.

* 타이머에서 실행되는 백그라운드 작업.
* [범위가 지정된 서비스](xref:fundamentals/dependency-injection#service-lifetimes)를 활성화하는 호스팅되는 서비스. 범위가 지정된 서비스는 종속성 주입을 사용할 수 있습니다.
* 순차적으로 실행되는 대기 중인 백그라운드 작업.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/hosted-services/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample))

샘플 앱은 두 가지 버전으로 제공됩니다.

* 웹 호스트 &ndash; 웹 호스트는 웹앱을 호스팅하는 데 유용합니다. 이 항목에 표시된 예제 코드는 웹 호스트 버전의 샘플에서 가져옵니다. 자세한 내용은 [웹 호스트](xref:fundamentals/host/web-host) 항목을 참조하세요.
* 일반 호스트 &ndash; 일반 호스트는 ASP.NET Core 2.1의 새로운 기능입니다. 자세한 내용은 [일반 호스트](xref:fundamentals/host/generic-host) 항목을 참조하세요.

## <a name="package"></a>Package

[Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)를 참조하거나 [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) 패키지에 대한 패키지 참조를 추가합니다.

## <a name="ihostedservice-interface"></a>IHostedService 인터페이스

호스팅되는 서비스는 <xref:Microsoft.Extensions.Hosting.IHostedService> 인터페이스를 구현합니다. 인터페이스는 호스트에 의해 관리되는 개체에 대한 두 가지 메서드를 정의합니다.

* [StartAsync(CancellationToken)](xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*)&ndash;`StartAsync`에는 백그라운드 작업을 시작하는 논리가 포함됩니다. [웹 호스트](xref:fundamentals/host/web-host)를 사용하는 경우 `StartAsync`는 서버가 시작되고 [IApplicationLifetime.ApplicationStarted](xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime.ApplicationStarted*)가 트리거된 후에 호출됩니다. [제네릭 호스트](xref:fundamentals/host/generic-host)를 사용하는 경우 `ApplicationStarted`가 트리거되기 전에 `StartAsync`가 호출됩니다.

* [StopAsync(CancellationToken)](xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*) &ndash; 호스트가 정상적으로 종료될 때 트리거됩니다. `StopAsync`에는 백그라운드 작업을 종료하는 논리가 포함됩니다. 관리되지 않는 리소스를 삭제하려면 <xref:System.IDisposable> 및 [종료자(소멸자)](/dotnet/csharp/programming-guide/classes-and-structs/destructors)를 구현합니다.

  취소 토큰에는 종료 프로세스가 더 이상 정상화되지 않아야 함을 나타내는 기본 5초 시간 제한이 있습니다. 토큰에 취소가 요청된 경우:

  * 앱이 수행하는 나머지 백그라운드 작업은 중단해야 합니다.
  * `StopAsync`에 호출된 모든 메서드는 즉시 반환해야 합니다.

  그러나 취소가 요청된 후 &mdash; 호출자가 모든 작업을 완료될 때까지 작업을 취소하지 않습니다.

  앱이 예기치 않게 종료된 경우(예: 앱의 프로세스가 실패한 경우), `StopAsync`가 호출되지 않을 수 있습니다. 따라서 메서드 호출이나 `StopAsync`에서 수행된 작업이 발생하지 않을 수 있습니다.

  기본 5초 시스템 종료 시간 제한을 연장하려면 다음을 설정합니다.

  * <xref:Microsoft.Extensions.Hosting.HostOptions.ShutdownTimeout*> 일반 호스트를 사용하는 경우 자세한 내용은 <xref:fundamentals/host/generic-host#shutdown-timeout>을 참조하세요.
  * 웹 호스트를 사용하는 경우 시스템 종료 시간 제한 호스트 구성 설정. 자세한 내용은 <xref:fundamentals/host/web-host#shutdown-timeout>을 참조하세요.

호스팅되는 서비스는 앱 시작 시 한 번 활성화되고 앱 종료 시 정상적으로 종료됩니다. 백그라운드 작업을 실행하는 동안 오류가 발생하면 `StopAsync`가 호출되지 않아도 `Dispose`를 호출해야 합니다.

## <a name="timed-background-tasks"></a>시간이 지정된 백그라운드 작업

시간이 지정된 백그라운드 작업은 [System.Threading.Timer](xref:System.Threading.Timer) 클래스를 사용합니다. 타이머가 작업의 `DoWork` 메서드를 트리거합니다. 서비스 컨테이너가 `Dispose`에서 삭제될 때 `StopAsync`에서 타이머가 비활성화되고 삭제됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/TimedHostedService.cs?name=snippet1&highlight=15-16,30,37)]

서비스는 `AddHostedService` 확장 메서드를 사용하여 `Startup.ConfigureServices`에 등록됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]

## <a name="consuming-a-scoped-service-in-a-background-task"></a>백그라운드 작업에서 범위가 지정된 서비스 사용

`IHostedService` 내에서 [범위가 지정된 서비스](xref:fundamentals/dependency-injection#service-lifetimes)를 사용하려면 범위를 만듭니다. 기본적으로 호스팅되는 서비스에 대한 범위는 생성되지 않습니다.

범위가 지정된 백그라운드 작업 서비스에는 백그라운드 작업의 논리가 포함됩니다. 다음 예제에서는 <xref:Microsoft.Extensions.Logging.ILogger>가 서비스에 삽입됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ScopedProcessingService.cs?name=snippet1)]

호스팅되는 서비스는 범위가 지정된 백그라운드 작업 서비스를 해결하여 `DoWork` 메서드를 호출하는 범위를 만듭니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ConsumeScopedServiceHostedService.cs?name=snippet1&highlight=29-36)]

서비스는 `Startup.ConfigureServices`에 등록됩니다. `IHostedService` 구현은 `AddHostedService` 확장 메서드를 사용하여 등록됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]

## <a name="queued-background-tasks"></a>대기 중인 백그라운드 작업

백그라운드 작업 큐는 .NET 4.x <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem*>([ASP.NET Core 3.0용으로 기본 제공될 예정](https://github.com/aspnet/Hosting/issues/1280))을 기반으로 합니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/BackgroundTaskQueue.cs?name=snippet1)]

`QueueHostedService`에서 큐의 백그라운드 작업은 큐에서 제거되고 장기 실행 `IHostedService`를 구현하기 위한 기본 클래스인 <xref:Microsoft.Extensions.Hosting.BackgroundService>로 실행됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/QueuedHostedService.cs?name=snippet1&highlight=21,25)]

서비스는 `Startup.ConfigureServices`에 등록됩니다. `IHostedService` 구현은 `AddHostedService` 확장 메서드를 사용하여 등록됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]

인덱스 페이지 모델 클래스에서:

* `IBackgroundTaskQueue`는 생성자에 삽입되고 `Queue`에 할당됩니다.
* <xref:Microsoft.Extensions.DependencyInjection.IServiceScopeFactory>가 삽입되어 `_serviceScopeFactory`에 할당됩니다. 팩터리는 범위 내에서 서비스를 만드는 데 사용되는 <xref:Microsoft.Extensions.DependencyInjection.IServiceScope>의 인스턴스를 만드는 데 사용됩니다. 앱의 `AppDbContext`([범위가 지정된 서비스](xref:fundamentals/dependency-injection#service-lifetimes))를 사용하여 `IBackgroundTaskQueue`(싱글톤 서비스)에 데이터베이스 레코드를 작성하는 범위가 생성됩니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet1)]

인덱스 페이지에서 **작업 추가** 단추를 선택하면 `OnPostAddTask` 메서드가 실행됩니다. `QueueBackgroundWorkItem`이 호출되어 작업 항목을 큐에 넣습니다.

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet2)]

## <a name="additional-resources"></a>추가 자료

* [IHostedService 및 BackgroundService 클래스를 사용하여 마이크로 서비스에서 백그라운드 작업 구현](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)
* <xref:System.Threading.Timer>
