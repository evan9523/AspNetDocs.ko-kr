---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062720"
---
# <a name="aspnet-core-response-caching-sample"></a>ASP.NET Core 응답 캐싱 예제

이 샘플에서는 ASP.NET Core의 사용을 보여 줍니다 [응답 캐싱 미들웨어](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)합니다.

해당 인덱스 페이지를 사용 하 여 앱이 응답 등을 `Cache-Control` 캐싱 동작을 구성 하는 헤더입니다. 앱 설정 합니다 `Vary` 경우에만 응답에 맞도록 캐시를 구성 하는 헤더는 `Accept-Encoding` 후속 요청의 헤더는 원래 요청에서 일치 합니다.

이 샘플을 실행 하는 경우 인덱스 페이지가 저장 하 고 최대 10 초 동안 캐시 되 면 캐시에서 제공 됩니다.
