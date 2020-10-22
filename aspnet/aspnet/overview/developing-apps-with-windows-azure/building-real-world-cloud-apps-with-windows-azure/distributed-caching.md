---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 분산 캐싱 (Azure를 사용 하 여 클라우드 앱 빌드 Real-World) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345521"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>분산 캐싱 (Azure를 사용 하 여 클라우드 앱 빌드 Real-World)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

이전 장에서는 일시적인 오류 처리 및 언급 된 캐싱을 회로 차단기 전략으로 살펴보았습니다. 이 장에서는 캐싱에 대 한 자세한 배경 정보를 사용할 시기, 사용 하는 일반적인 패턴, Azure에서 구현 하는 방법 등을 설명 합니다.

## <a name="what-is-distributed-caching"></a>분산 캐싱 이란?

캐시는 메모리에 데이터를 저장 하 여 자주 액세스 하는 응용 프로그램 데이터에 대 한 높은 처리량, 짧은 대기 시간 액세스를 제공 합니다. 클라우드 앱의 경우 가장 유용한 캐시 유형은 분산 된 캐시입니다. 즉, 데이터가 개별 웹 서버의 메모리에 저장 되는 것이 아니라 다른 클라우드 리소스에 저장 되며, 캐시 된 데이터는 응용 프로그램의 모든 웹 서버 (또는 응용 프로그램에서 사용 하는 다른 클라우드 Vm)에서 사용할 수 있게 됩니다.

![동일한 캐시 서버에 액세스 하는 여러 웹 서버를 보여 주는 다이어그램](distributed-caching/_static/image1.png)

서버를 추가 또는 제거 하 여 응용 프로그램의 크기를 조정 하거나, 업그레이드 또는 오류로 인해 서버가 교체 되 면 응용 프로그램을 실행 하는 모든 서버에서 캐시 된 데이터에 계속 액세스할 수 있습니다.

캐시는 영구 데이터 저장소의 대기 시간이 긴 데이터 액세스를 방지 함으로써 응용 프로그램 응답성을 크게 향상 시킬 수 있습니다. 예를 들어 캐시에서 데이터를 검색 하는 것은 관계형 데이터베이스에서 데이터를 검색 하는 것 보다 훨씬 빠릅니다.

캐싱은 영구적 데이터 저장소에 대 한 트래픽 감소를 초래 하므로 영구적 데이터 저장소에 대 한 데이터 송신 요금이 있는 경우 비용이 저렴 해질 수 있습니다.

## <a name="when-to-use-distributed-caching"></a>분산 캐싱을 사용 하는 경우

캐싱은 데이터 쓰기 보다 읽기가 많은 응용 프로그램 작업에 가장 적합 하며, 데이터 모델이 캐시에 데이터를 저장 하 고 검색 하는 데 사용 하는 키/값 조직을 지 원하는 경우에 가장 적합 합니다. 응용 프로그램 사용자가 많은 공통 데이터를 공유 하는 경우에도 더 유용 합니다. 예를 들어 각 사용자가 일반적으로 해당 사용자에 게 고유한 데이터를 검색 하는 경우 캐시는 많은 이점을 제공 하지 않습니다. 캐싱을 매우 유용 하 게 사용할 수 있는 예는 데이터는 자주 변경 되지 않으며 모든 고객이 동일한 데이터를 보고 하기 때문에 제품 카탈로그입니다.

영구적 데이터 저장소의 처리량 제한 및 대기 시간 지연으로 인해 전체 응용 프로그램 성능에 대 한 제한이 증가 하므로 응용 프로그램의 크기를 조정 하는 것이 더 커질 수 있습니다. 그러나 성능 외에 다른 이유로도 캐싱을 구현할 수 있습니다. 사용자에 게 표시 될 때 완벽 하 게 작동 하지 않아도 되는 데이터의 경우, 캐시 액세스는 영구적 데이터 저장소가 응답 하지 않거나 사용할 수 없는 경우에 대 한 회로 차단기 역할을 할 수 있습니다.

## <a name="popular-cache-population-strategies"></a>인기 있는 캐시 채우기 전략

캐시에서 데이터를 검색할 수 있으려면 먼저 해당 데이터를 저장 해야 합니다. 캐시에 필요한 데이터를 가져오는 방법에는 여러 가지가 있습니다.

- 주문형/캐시 별도로

    응용 프로그램이 캐시에서 데이터를 검색 하려고 하 고 캐시에 데이터가 없는 경우 ("누락") 응용 프로그램은 다음에 사용할 수 있도록 캐시에 데이터를 저장 합니다. 다음 번에 응용 프로그램이 동일한 데이터를 가져오려고 하면 캐시에서 찾고 있는 항목 ("적중")을 찾습니다. 데이터베이스에서 변경 된 캐시 된 데이터를 인출 하지 않으려면 데이터 저장소를 변경할 때 캐시를 무효화 합니다.
- 백그라운드 데이터 푸시

    백그라운드 서비스는 정기적인 일정에 따라 데이터를 캐시에 푸시하고 앱은 항상 캐시에서 가져옵니다. 이 접근 방식은 항상 최신 데이터를 반환 하지 않아도 되는 대기 시간이 긴 데이터 원본에서 잘 작동 합니다.
- 회로 차단기

    응용 프로그램은 일반적으로 영구 데이터 저장소와 직접 통신 하지만 영구 데이터 저장소에 가용성 문제가 있는 경우 응용 프로그램은 캐시에서 데이터를 검색 합니다. 데이터는 캐시에 보관 된 캐시 또는 백그라운드 데이터 푸시 전략을 사용 하 여 캐시에 저장 되었을 수 있습니다. 이는 성능 향상 전략이 아닌 오류 처리 전략입니다.

현재 캐시에 있는 데이터를 유지 하기 위해 응용 프로그램에서 데이터를 만들거나 업데이트 하거나 삭제할 때 관련 캐시 항목을 삭제할 수 있습니다. 응용 프로그램에서 약간 오래 된 데이터를 가져오는 것이 좋은 경우 구성 가능한 만료 시간을 사용 하 여 오래 된 캐시 데이터의 크기 제한을 설정할 수 있습니다.

절대 만료 (캐시 항목이 생성 된 이후 경과 된 시간) 또는 슬라이딩 만료 (캐시 항목을 마지막으로 액세스 한 이후 경과 된 시간)를 구성할 수 있습니다. 절대 만료는 데이터가 너무 오래 되지 않도록 방지 하기 위해 캐시 만료 메커니즘에 따라 달라 지는 경우에 사용 됩니다. Fix It 앱에서 오래 된 캐시 항목을 수동으로 제거 하 고, 현재 데이터를 캐시에 유지 하기 위해 슬라이딩 만료를 사용 합니다. 선택한 만료 정책에 관계 없이 캐시의 메모리 제한에 도달 하면 캐시에서 가장 오래 된 (가장 최근에 사용한 항목이 나 LRU) 항목이 자동으로 제거 됩니다.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>샘플 캐시-수정 It 앱 용 코드 분리

다음 샘플 코드에서는 Fix It 작업을 검색할 때 먼저 캐시를 확인 합니다. 캐시에서 작업을 찾은 경우 반환 됩니다. 찾을 수 없는 경우 데이터베이스에서 가져와 캐시에 저장 합니다. 메서드에 캐싱을 추가 하기 위해 변경한 내용이 `FindTaskByIdAsync` 강조 표시 됩니다.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Fix It 작업을 업데이트 하거나 삭제 하는 경우 캐시 된 작업을 무효화 (제거) 해야 합니다. 그렇지 않으면 나중에 해당 작업을 읽으려고 할 때 계속 해 서 캐시에서 이전 데이터를 가져옵니다.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

다음은 간단한 캐싱 코드를 보여 주는 샘플입니다. 캐싱을 다운로드 가능한 Fix It 프로젝트에서 구현 하지 않았습니다.

## <a name="azure-caching-services"></a>Azure 캐싱 서비스

Azure는 다음과 같은 캐싱 서비스를 제공 합니다. [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) 및 [azure Managed Cache](https://msdn.microsoft.com/library/dn386094.aspx) Azure Redis cache는 인기 있는 [오픈 소스 Redis Cache](http://redis.io/) 을 기반으로 하며 대부분의 캐싱 시나리오에 가장 적합 합니다.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>캐시 공급자를 사용 하 여 세션 상태 ASP.NET

[웹 개발 모범 사례 챕터](web-development-best-practices.md)에서 설명 했 듯이, 세션 상태를 사용 하지 않는 것이 가장 좋습니다. 응용 프로그램에서 세션 상태를 요구 하는 경우 다음 모범 사례는 확장 (웹 서버의 여러 인스턴스)을 사용할 수 없기 때문에 기본 메모리 내 공급자를 피하는 것입니다. ASP.NET SQL Server 세션 상태 공급자를 사용 하면 여러 웹 서버에서 실행 되는 사이트에서 세션 상태를 사용할 수 있지만 메모리 내 공급자에 비해 높은 대기 시간 비용이 발생 합니다. 세션 상태를 사용 해야 하는 경우 [Azure 캐시용 세션 상태 공급자](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)와 같은 캐시 공급자를 사용 하는 것이 가장 좋습니다.

## <a name="summary"></a>요약

응답 시간 및 확장성을 개선 하기 위해 Fix It 앱이 캐싱을 구현 하는 방법을 확인 하 고, 데이터베이스를 사용할 수 없을 때 앱이 읽기 작업에 계속 응답할 수 있도록 합니다. [다음 장에서](queue-centric-work-pattern.md) 는 확장성을 더욱 개선 하 고 앱이 쓰기 작업에 계속 응답 하도록 하는 방법을 보여 줍니다.

## <a name="resources"></a>리소스

캐싱에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

문서화

- [Azure 캐시](https://msdn.microsoft.com/library/gg278356.aspx). Azure의 캐싱에 대 한 공식 MSDN 설명서입니다.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) 캐싱 지침 및 Cache-Aside 패턴을 참조 하세요.
- [비상 복구: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)입니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill의 백서입니다. 캐싱에 대 한 섹션을 참조 하세요.
- [Azure Cloud Services에서 Large-Scale 서비스를 디자인 하는 방법에 대 한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)입니다. W. 이 백서에서는 Simm 및 Michael Thomassy을 표시 합니다. 분산 캐싱에 대 한 섹션을 참조 하세요.
- [확장성을 위한 경로에 분산 캐싱](https://msdn.microsoft.com/magazine/dd942840.aspx) 이전 (2009) MSDN Magazine 문서 이지만, 일반적으로 분산 캐싱 소개를 명확 하 게 작성 합니다. 는 안전 및 모범 사례 백서의 캐싱 섹션 보다 더 깊이 있습니다.

동영상

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) Ulrich HoMarc Mercuri 및 Mark Simm에서 9 부분으로 된 시리즈. 클라우드 앱을 설계 하는 방법에 대 한 400 수준 보기를 제공 합니다. 이 시리즈는 이론적 및 이유를 중점적으로 설명 합니다. 자세한 방법에 대 한 자세한 내용은 표시 Simm을 사용한 빅 시리즈 빌드를 참조 하세요. 1:24:14에서 시작 하는 에피소드 3의 캐싱 논의를 참조 하세요.
- [대규모 빌드: Azure 고객 으로부터 얻은 교훈을](https://channel9.msdn.com/Events/Build/2012/3-029)확인 하세요. Simon Davies 46:00에서 시작 하는 분산 캐싱에 대해 설명 합니다. 안전 계열과 유사 하지만 자세한 방법에 대해 자세히 설명 합니다. 프레젠테이션은 2012 년 10 월 31 일에 제공 되었으므로 2013에 도입 된 Azure App Service의 캐싱 Web Apps 서비스에 대해서는 설명 하지 않습니다.

코드 샘플

- [Azure의 클라우드 서비스 기본 사항](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)입니다. 분산 캐싱을 구현 하는 예제 응용 프로그램입니다. 제공 되는 블로그 게시물 [클라우드 서비스 기본 사항 – 캐싱 기본 사항](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](transient-fault-handling.md)
> [다음](queue-centric-work-pattern.md)
