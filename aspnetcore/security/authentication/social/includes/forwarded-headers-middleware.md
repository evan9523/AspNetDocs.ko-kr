---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130452"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a>앞으로 프록시를 사용 하 여 정보를 요청 하거나 부하 분산 장치

앱 프록시 서버 또는 부하 분산 장치 뒤에 배포 하는 경우 원래 요청 정보 중 일부를 앱 요청 헤더에 전달 될 수 있습니다. 이 정보에는 일반적으로 보안 요청 체계가 포함 됩니다 (`https`), 호스트 및 클라이언트 IP 주소입니다. 앱 검색 하 고 원래 요청 정보를 사용 하 여 이러한 요청 헤더를 자동으로 읽습니다 하지 않습니다.

스키마 외부 공급자를 사용 하 여 인증 흐름에 영향을 주는 링크 생성에 사용 됩니다. 보안 체계 손실 (`https`) 안전 하지 않은 잘못 된 리디렉션 Url을 생성 하는 앱에서 발생 합니다.

전달 된 헤더 미들웨어를 사용 하 여 원래 요청 정보를 요청 처리에 대 한 앱을 사용할 수 있도록 합니다.

자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.
