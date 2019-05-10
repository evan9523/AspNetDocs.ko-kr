---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: 405 오류 게시 후 웹 HTTP 문제 해결 API 응용 프로그램 | Microsoft Docs
author: rmcmurray
description: 이 자습서에는 프로덕션 웹 서버에 Web API 응용 프로그램을 게시 한 후 HTTP 405 오류를 해결 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 336df47dd4bda813839913676f12a51b899c0cf9
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65121977"
---
# <a name="troubleshooting-http-405-errors-after-publishing-web-api-applications"></a>Web API 응용 프로그램을 게시 한 후 HTTP 405 오류 문제 해결

> 이 자습서에는 프로덕션 웹 서버에 Web API 응용 프로그램을 게시 한 후 HTTP 405 오류를 해결 하는 방법을 설명 합니다.
> 
> ## <a name="software-used-in-this-tutorial"></a>이 자습서에서 사용 되는 소프트웨어
> 
> 
> - [인터넷 정보 서비스 (IIS)](https://www.iis.net/) (버전 7 이상)
> - [Web API](../../index.md) 

웹 API 응용 프로그램은 일반적으로 몇 가지 일반적인 HTTP 동사를 사용합니다. GET, POST, PUT, DELETE 및 경우에 따라 패치 합니다. 즉, 개발자가 발생할 경우 이러한 동사 또는 Visual Studio 개발 서버에서 제대로 작동 하는 Web API 컨트롤러를 반환 하는 경우에는 해당 프로덕션 서버의 다른 IIS 모듈에 의해 구현 되는 위치는 HTTP 405 프로덕션 서버에 배포 하는 동안 오류가 발생 했습니다. 다행히이 문제는 쉽게 해결 하지만 문제가 발생 하는 이유와 설명은 보장 하는 확인 합니다.

## <a name="what-causes-http-405-errors"></a>HTTP 405 오류 원인

HTTP 405 오류 문제 하는 방법을 배우는 첫 번째 단계에서 HTTP 405 오류 실제로 의미를 이해 하는 것입니다. HTTP에 대 한 문서 주 제어 [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)와 HTTP 405 상태 코드를 정의 하는 ***메서드를 사용할 수 없습니다***, 상황으로이 상태 코드를 자세히 설명 하 고 있는 &quot;메서드 에 지정 된 요청 줄 요청 URI로 식별 되는 리소스에 허용 되지 않습니다.&quot; 즉, HTTP 동사는 HTTP 클라이언트 요청에 특정 URL에 허용 되지 않습니다.

간략 한 검토 결과 대부분 사용 되는 HTTP 메서드의 여러 RFC 2616, RFC 4918 및 RFC 5789에 정의 된 대로 다음과 같습니다.

| HTTP 메서드 | 설명 |
| --- | --- |
| **GET** | 이 메서드는 데이터를 검색할 URI에서 아마도 가장 사용 되는 HTTP 메서드가 사용 됩니다. |
| **HEAD** | 이 메서드는 요청 URI에서에서 데이터를 실제로 검색 하지 해당-HTTP 상태를 간단히 검색 한다는 점을 제외 하면 GET 메서드의 경우와 비슷하게 합니다. |
| **POST** | 이 메서드는 일반적으로 데 URI;에 새 데이터를 전송 합니다. POST는 양식 데이터를 전송할 자주 사용 됩니다. |
| **PUT** | 이 메서드는 일반적으로 데; URI에서 원시 데이터 보내기 PUT는 Web API 응용 프로그램에 JSON 또는 XML 데이터를 전송할 자주 사용 됩니다. |
| **DELETE** | 이 메서드는 URI에서 데이터를 제거 하려면 사용 됩니다. |
| **옵션** | 이 메서드는 URI에 대해 지원 되는 HTTP 메서드 목록을 검색 하려면 일반적으로 사용 됩니다. |
| **복사 이동** | 그 목적은 쉽게 이해할 수 및 WebDAV를 사용 하 여 이러한 두 가지 방법을 사용 됩니다. |
| **MKCOL** | WebDAV를 사용 하 여이 메서드를 사용 하 고 지정된 된 URI의 컬렉션 (예: 디렉터리)를 만드는 데 사용 됩니다. |
| **PROPFIND PROPPATCH** | WebDAV를 사용 하 여 이러한 두 메서드는 사용 및 사용 되는 쿼리 또는 URI에 대 한 속성을 설정 합니다. |
| **잠금을 해제** | WebDAV를 사용 하 여 이러한 두 메서드가 사용 됩니다 하 고 작성 하는 경우 요청 URI에 의해 식별 되는 리소스 잠금/잠금 해제 하는 데 사용 됩니다. |
| **PATCH** | 이 메서드는 기존 HTTP 리소스를 수정 하려면 사용 됩니다. |

HTTP 메서드 중 하나는 서버에서 사용 하기 위해 구성 되 면 서버가 HTTP 상태 및 요청에 대 한 적절 한 기타 데이터를 사용 하 여 응답 합니다. (예를 들어 GET 메서드는 HTTP 200 나타날 ***확인*** 응답 및 PUT 메서드를 HTTP 201 나타날 ***Created*** 응답 합니다.)

서버는 HTTP 501를 사용 하 여 응답할 HTTP 메서드는 서버에서 사용 하기 위해 구성 되지 않은 경우 ***구현 되지*** 오류입니다.

그러나 HTTP 메서드를 서버에서 사용 하도록 구성 된 지정한 URI에 대 한 비활성화 된 경우 서버는 응답을 보냅니다는 HTTP 405 ***메서드를 사용할 수 없습니다*** 오류입니다.

## <a name="example-http-405-error"></a>예제에서는 HTTP 405 오류

다음 예제에서는 HTTP 요청 및 응답 있는 웹 서버에서 Web API 응용 프로그램에 값을 배치 하기 위해 시도 하는 HTTP 클라이언트 및 서버 상태 PUT 메서드를 사용할 수 있는 HTTP 오류를 반환 합니다. 상황을 보여 줍니다.

HTTP 요청:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP 응답:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

이 예제에서는 HTTP 클라이언트는 유효한 JSON 요청 웹 서버에 있는 Web API 응용 프로그램에 대 한 URL을 보냈지만 서버 URL에 대 한 PUT 메서드를 허용 되지 않음을 나타내는 HTTP 405 오류 메시지를 반환 합니다. 반면, 요청 URI는 Web API 응용 프로그램에 대 한 경로 일치 하지 않은 서버 반환을 HTTP 404 ***찾지*** 오류입니다.

## <a name="resolve-http-405-errors"></a>HTTP 405 오류 해결

이유는 특정 HTTP 동사를 사용할 수 없는, 하지만 IIS에서이 오류의 주요 원인입니다. 한 가지 주요 시나리오는 여러 가지가 있습니다: 동일한 동사/메서드에 대 한 처리기를 여러 개 정의 되어 있고에서 예상 되는 처리기를 차단 하는 처리기 중 하나 요청을 처리 합니다. 통해 IIS에서 마지막으로 항목을 기준으로 순서 처리기 경로, 동사, 리소스 등의 첫 번째 일치 하는 조합을 사용 하는 요청을 처리 하는 위치 applicationHost.config 및 web.config 파일에서 첫 번째 처리기를 처리 합니다.

다음 예제에서는 PUT 메서드를 사용 하 여 Web API 응용 프로그램에 데이터를 전송할 때에서 HTTP 405 오류를 반환 된 IIS 서버에 대 한 applicationHost.config 파일에서 발췌 한 경우 이 발췌에서 여러 HTTP 처리기 정의 및 각 처리기에는 다른 HTTP 메서드 집합을 구성 하는-목록의 마지막 항목은 다른 처리기는 chanc 전에 사용 되는 기본 처리기는 정적 콘텐츠 처리기 요청을 검사 하려면 e:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

위의 예에서 WebDAV 처리기와 ASP.NET (웹 API에 대 한 사용 됨)에 대 한 확장명이 없는 URL 처리기 명확 하 게 별도 목록은 HTTP 메서드 정의 됩니다. 이 구성은 오류가 반드시 인해 하지 않지만 모든 HTTP 메서드에 대 한 ISAPI DLL 처리기 구성 되어 있는지를 참고 합니다. 그러나 HTTP 405 오류 문제 해결 시 고려해 야 할이 이와 같은 구성 설정입니다.

위의 예제에서는 ISAPI DLL 처리기 문제가 아닙니다. 사실, 문제는 IIS 서버에 대 한 applicationHost.config 파일에서 정의 되지 않았습니다-Visual Studio에서 웹 API 응용 프로그램을 만들 때 web.config 파일에서 만든 항목으로 문제가 발생 했습니다. 응용 프로그램의 web.config 파일에서 발췌 한 다음 문제의 위치를 보여 줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

이 발췌에서 ASP.NET에 대 한 확장명이 없는 URL 처리기는 Web API 응용 프로그램을 사용 하 여 사용할 추가 HTTP 메서드를 포함 하도록 재정의 됩니다. 그러나 HTTP 메서드 집합을 유사한 WebDAV 처리기에 대 한 정의 되므로 충돌이 발생 합니다. 이 특정 예제의 WebDAV 처리기가 정의 되 고 웹 API 응용 프로그램을 포함 하는 웹 사이트에 대 한 WebDAV가 사용 하지 않도록 설정 하는 경우에 IIS에서 로드 합니다. HTTP PUT 요청을 처리 하는 동안에 PUT 동사가 정의 되므로 IIS WebDAV 모듈을 호출 합니다. WebDAV 모듈 호출 되 면 해당 구성을 확인 하 고는 HTTP 405 반환 하므로 비활성 상태임을 확인 ***메서드를 사용할 수 없습니다*** WebDAV 요청을 유사 하는 모든 요청에 대 한 오류입니다. 이 문제를 해결 하려면 WebDAV 웹 API 응용 프로그램 정의 되어 있는 웹 사이트에 대 한 HTTP 모듈 목록에서 제거 해야 합니다. 다음 예제는 수 형태 보여 줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

이 시나리오는 응용 프로그램은 개발 환경에서 프로덕션 환경에 게시 된 후 처리기/모듈 목록을 개발 환경과 프로덕션 환경이 다르기 때문에 이런에 종종 발생 합니다. 예를 들어, Visual Studio 2012를 사용 하는 경우 또는 Web API 응용 프로그램을 개발 하려면 나중에 IIS Express는 테스트에 대 한 기본 웹 서버. 이 개발 웹 서버는 서버 제품에서 제공 되는 모든 IIS 기능을 축소 된 버전 및이 개발 웹 서버에는 개발 시나리오에 대 한 추가 된 몇 가지 변경 내용이 포함 되어 있습니다. 예를 들어, WebDAV 모듈 실제 사용에서 되지 않을 수 있습니다 하지만 자주 IIS의 전체 버전을 실행 하는 프로덕션 웹 서버에 설치 됩니다. 개발 버전의 IIS (IIS Express), WebDAV 모듈을 설치 하지만 WebDAV 모듈에 대 한 항목은 의도적으로 주석으로 WebDAV 모듈은 특히 IIS Express 구성을 변경 하지 않는 경우 IIS Express에서 로드 되지 않습니다 있도록 IIS Express 설치를 사용 하 여 WebDAV 기능을 추가 하려면 설정입니다. 결과적으로, 웹 응용 프로그램 개발 컴퓨터에 제대로 작동 않을 수 있지만 프로덕션 웹 서버에 Web API 응용 프로그램을 게시할 때 HTTP 405 오류를 발생할 수 있습니다.

## <a name="summary"></a>요약

HTTP 405 오류는 요청된 된 URL의 HTTP 메서드를 웹 서버에서 허용 하지 않는 경우에 발생 합니다. 이 문제는 주로 특정 동사에 대 한 특정 처리기를 정의 되 고 해당 처리기는 요청을 처리 해야 하는 처리기를 재정의 하는 경우에 표시 됩니다.

특정 기능을 서버에서 구현 되지 않았음을 의미 하는 HTTP 501 오류 메시지를 받게 되는 상황이 발생 하면이 경우 대체로 처리기가 없는 IIS 설정에서 정의 된 HTTP 요청에 일치 하는 아마도 항목이 올바르게 시스템에 설치 되지 않은 또는 해당 지원 특정 HTTP 메서드를 정의 하는 처리기가 없는 IIS 설정을 변경 했습니다 것을 나타냅니다. 해당 문제를 해결 하려면 해당 모듈 또는 처리기 정의 없습니다 있기 HTTP 메서드를 사용 하려고 시도 하는 응용 프로그램을 다시 설치 해야 합니다.
