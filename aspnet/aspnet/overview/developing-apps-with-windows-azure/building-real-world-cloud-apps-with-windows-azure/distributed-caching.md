---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 분산 캐싱(Azure를 사용한 실제 클라우드 앱 빌드) | 마이크로 소프트 문서
author: MikeWasson
description: Azure 전자책을 사용한 실제 클라우드 앱 구축은 Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 그것은 그가 할 수있는 13 패턴과 관행을 설명합니다 ...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675660"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>분산 캐싱(Azure를 사용한 실제 클라우드 앱 빌드)

[마이크 와슨,](https://github.com/MikeWasson) [릭 앤더슨,](https://twitter.com/RickAndMSFT) [톰 다이크스트라](https://github.com/tdykstra)

[프로젝트 수정](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure 전자책을 **사용한 실제 클라우드 앱 구축은** Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 클라우드용 웹 앱을 성공적으로 개발하는 데 도움이 되는 13가지 패턴과 사례에 대해 설명합니다. 전자책에 대한 자세한 내용은 [첫 번째 장을](introduction.md)참조하십시오.

이전 장에서는 일시적인 오류 처리를 살펴보고 회로 차단기 전략으로 캐싱을 언급했습니다. 이 장에서는 캐싱을 사용할 시기, 캐싱을 사용하는 일반적인 패턴 및 Azure에서 캐싱을 구현하는 방법을 포함하여 캐싱에 대한 자세한 배경을 제공합니다.

## <a name="what-is-distributed-caching"></a>분산 캐싱이란 무엇입니까?

캐시는 메모리에 데이터를 저장하여 일반적으로 액세스되는 응용 프로그램 데이터에 대한 높은 처리량, 낮은 대기 시간 액세스를 제공합니다. 클라우드 앱의 경우 가장 유용한 캐시 유형은 분산 캐시로, 이는 데이터가 개별 웹 서버의 메모리에 저장되지 않고 다른 클라우드 리소스에 저장되며 캐시된 데이터는 응용 프로그램의 모든 웹 서버(또는 응용 프로그램에서 사용되는 다른 클라우드 VM)에서 사용할 수 있습니다.

![동일한 캐시 서버에 액세스하는 여러 웹 서버를 보여주는 다이어그램](distributed-caching/_static/image1.png)

응용 프로그램이 서버를 추가하거나 제거하여 확장되거나 업그레이드 또는 오류로 인해 서버를 교체할 때 캐시된 데이터는 응용 프로그램을 실행하는 모든 서버에서 계속 액세스할 수 있습니다.

영구 데이터 저장소의 높은 대기 시간 데이터 액세스를 방지하면 캐싱이 응용 프로그램 응답성을 크게 향상시킬 수 있습니다. 예를 들어 캐시에서 데이터를 검색하는 것이 관계형 데이터베이스에서 데이터를 검색하는 것보다 훨씬 빠릅니다.

캐싱의 측면 이점은 영구 데이터 저장소로 의 트래픽을 줄이며, 영구 데이터 저장소에 대한 데이터 송신 요금이 발생할 경우 비용이 낮아질 수 있습니다.

## <a name="when-to-use-distributed-caching"></a>분산 캐싱을 사용하는 경우

캐싱은 데이터 쓰기보다 더 많은 읽기를 수행하는 응용 프로그램 워크로드와 데이터 모델이 캐시에 데이터를 저장하고 검색하는 데 사용하는 키/값 조직을 지원하는 경우에 가장 적합합니다. 또한 응용 프로그램 사용자가 많은 공통 데이터를 공유할 때 더 유용합니다. 예를 들어 각 사용자가 일반적으로 해당 사용자에 고유한 데이터를 검색하는 경우 캐시는 많은 이점을 제공하지 않습니다. 데이터가 자주 변경되지 않고 모든 고객이 동일한 데이터를 보고 있기 때문에 캐싱이 매우 유리할 수 있는 예는 제품 카탈로그입니다.

영구 데이터 저장소의 처리량 제한 및 대기 시간 지연이 전체 응용 프로그램 성능에 대한 제한이 증가함에 따라 캐싱의 이점은 응용 프로그램 확장이 증가할수록 점점 더 측정 가능해지고 있습니다. 그러나 성능 이외의 다른 이유로 캐싱을 구현할 수도 있습니다. 사용자에게 표시될 때 완벽하게 최신 상태일 필요가 없는 데이터의 경우 영구 데이터 저장소가 응답하지 않거나 사용할 수 없는 경우 캐시 액세스가 회로 차단기로 사용될 수 있습니다.

## <a name="popular-cache-population-strategies"></a>인기 있는 캐시 채우기 전략

캐시에서 데이터를 검색하려면 먼저 데이터를 저장해야 합니다. 캐시에 필요한 데이터를 가져오는 데는 몇 가지 전략이 있습니다.

- 온디맨드 / 캐시 따로

    응용 프로그램은 캐시에서 데이터를 검색하려고 시도하며 캐시에 데이터가 없는 경우("누락") 응용 프로그램은 다음에 사용할 수 있도록 캐시에 데이터를 저장합니다. 다음에 응용 프로그램이 동일한 데이터를 얻으려고 할 때 캐시에서 찾고 있는 데이터를 찾습니다("적중"). 데이터베이스에서 변경된 캐시된 데이터를 가져오지 않도록 하려면 데이터 저장소를 변경할 때 캐시를 무효화합니다.
- 백그라운드 데이터 푸시

    백그라운드 서비스는 정기적으로 데이터를 캐시로 푸시하고 앱은 항상 캐시에서 가져옵니다. 이 방법은 항상 최신 데이터를 반환할 필요가 없는 대기 시간이 많은 데이터 원본에서 적합합니다.
- 회로 차단기

    응용 프로그램은 일반적으로 영구 데이터 저장소와 직접 통신하지만 영구 데이터 저장소에 가용성 문제가 있는 경우 응용 프로그램은 캐시에서 데이터를 검색합니다. 캐시를 따로 사용하거나 백그라운드 데이터 푸시 전략을 사용하여 데이터가 캐시에 저장되었을 수 있습니다. 이는 성능 향상 전략이 아닌 오류 처리 전략입니다.

캐시에 데이터를 최신 상태로 유지하려면 응용 프로그램에서 데이터를 만들거나 업데이트하거나 삭제할 때 관련 캐시 항목을 삭제할 수 있습니다. 응용 프로그램에서 약간 오래된 데이터를 얻는 것이 괜찮다면 구성 가능한 만료 시간을 사용하여 오래된 캐시 데이터 수에 대한 제한을 설정할 수 있습니다.

절대 만료(캐시 항목이 생성된 이후의 시간) 또는 슬라이딩 만료(캐시 항목에 마지막으로 액세스한 이후의 시간)를 구성할 수 있습니다. 데이터가 너무 오래되지 않도록 캐시 만료 메커니즘에 따라 절대 만료가 사용됩니다. Fix It 앱에서는 오래된 캐시 항목을 수동으로 제거하며 슬라이딩 만료를 사용하여 최신 데이터를 캐시에 유지합니다. 선택한 만료 정책에 관계없이 캐시는 캐시의 메모리 제한에 도달하면 가장 오래된(가장 최근에 사용한 항목 또는 LRU) 항목을 자동으로 제거합니다.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>수정 앱에 대한 샘플 캐시 옆 코드

다음 샘플 코드에서는 Fix It 작업을 검색할 때 캐시를 먼저 확인합니다. 캐시에서 작업이 발견되면 반환합니다. 찾을 수 없는 경우 데이터베이스에서 가져옵니다 및 캐시에 저장 합니다. 메서드에 캐싱을 추가하기 위해 `FindTaskByIdAsync` 변경한 내용이 강조 표시됩니다.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Fix It 작업을 업데이트하거나 삭제할 때 캐시된 작업을 무효화(제거)해야 합니다. 그렇지 않으면 나중에 해당 작업을 읽으려고 하면 캐시에서 이전 데이터가 계속 가져옵니다.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

다음은 간단한 캐싱 코드를 설명하는 샘플입니다. 캐싱은 다운로드 가능한 Fix It 프로젝트에서 구현되지 않았습니다.

## <a name="azure-caching-services"></a>Azure 캐싱 서비스

Azure는 다음과 같은 캐싱 서비스를 제공합니다: [Azure Redis 캐시](https://msdn.microsoft.com/library/dn690523.aspx) 및 [Azure 관리되는 캐시.](https://msdn.microsoft.com/library/dn386094.aspx) Azure Redis 캐시는 인기 있는 [오픈 소스 Redis 캐시를](http://redis.io/) 기반으로 하며 대부분의 캐싱 시나리오에 대 한 첫 번째 선택입니다.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>캐시 공급자를 사용하여 세션 상태를 ASP.NET

웹 개발 [모범 사례 장에서](web-development-best-practices.md)언급했듯이 세션 상태를 사용하지 않는 것이 좋습니다. 응용 프로그램에 세션 상태가 필요한 경우 다음 모범 사례는 확장(웹 서버의 여러 인스턴스)을 활성화하지 않으므로 기본 메모리 내 공급자를 피하는 것입니다. ASP.NET SQL Server 세션 상태 공급자를 사용하면 여러 웹 서버에서 실행되는 사이트가 세션 상태를 사용할 수 있지만 메모리 내 공급자에 비해 대기 시간이 많이 소요됩니다. 세션 상태를 사용해야 하는 경우 가장 좋은 방법은 Azure 캐시에 [대한 세션 상태 공급자와](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)같은 캐시 공급자를 사용하는 것입니다.

## <a name="summary"></a>요약

Fix It 앱이 응답 시간과 확장성을 개선하고 데이터베이스를 사용할 수 없을 때 앱이 읽기 작업에 계속 응답할 수 있도록 하기 위해 캐싱을 구현하는 방법을 보았습니다. 다음 [장에서는](queue-centric-work-pattern.md) 확장성을 더욱 개선하고 앱이 쓰기 작업에 계속 반응하도록 하는 방법을 보여 드리겠습니다.

## <a name="resources"></a>리소스

캐싱에 대한 자세한 내용은 다음 리소스를 참조하십시오.

문서화

- [Azure 캐시](https://msdn.microsoft.com/library/gg278356.aspx). Azure에서 캐싱에 대한 공식 MSDN 설명서입니다.
- [마이크로 소프트 패턴 및 관행 - Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx). 캐싱 지침 및 캐시 옆면 패턴을 참조하십시오.
- [페일세이프: 탄력적인 클라우드 아키텍처에 대한 지침.](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx) 마크 머큐리, 울리히 호만, 앤드류 타운힐의 백서. 캐싱의 섹션을 참조하십시오.
- [Azure 클라우드 서비스에서 대규모 서비스 설계를 위한 모범 사례입니다.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) W. 백서: 마크 심스와 마이클 토마시 분산 캐싱 섹션을 참조하십시오.
- [확장성에 대한 경로에 분산 캐싱](https://msdn.microsoft.com/magazine/dd942840.aspx). 이전 (2009) MSDN 잡지 기사,하지만 일반적으로 분산 캐싱에 명확하게 작성 된 소개; FailSafe 및 모범 사례 백서의 캐싱 섹션보다 더 심층적입니다.

동영상

- [페일세이프: 확장 가능하고 탄력적인 클라우드 서비스 구축.](https://channel9.msdn.com/Series/FailSafe) 울리히 호만, 마크 머큐리, 마크 심스의 9부작 시리즈. 클라우드 앱을 설계하는 방법에 대한 400수준 보기를 제공합니다. 이 시리즈는 이론과 이유에 초점을 맞추고; 자세한 방법은 Mark Simms의 빌딩 빅 시리즈를 참조하십시오. 1:24:14부터 시작되는 에피소드 3의 캐싱 토론을 참조하십시오.
- [큰 건물: Azure 고객으로부터 얻은 교훈 - 파트 I](https://channel9.msdn.com/Events/Build/2012/3-029). 사이먼 데이비스는 46:00부터 분산 캐싱에 대해 설명합니다. Failsafe 시리즈와 유사하지만 자세한 방법 세부 정보로 이동합니다. 프레젠테이션은 2012년 10월 31일에 제공되었기 때문에 2013년에 도입된 Azure 앱 서비스에서 웹 앱의 캐싱 서비스는 다루지 않습니다.

코드 샘플

- [Azure의 클라우드 서비스 기본 사항.](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649) 분산 캐싱을 구현하는 샘플 응용 프로그램입니다. 첨부 블로그 게시물 [클라우드 서비스 기본 사항 – 캐싱 기본 .](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)

> [!div class="step-by-step"]
> [이전](transient-fault-handling.md)
> [다음](queue-centric-work-pattern.md)
