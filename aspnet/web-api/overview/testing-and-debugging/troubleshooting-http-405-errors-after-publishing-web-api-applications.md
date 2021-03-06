---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: Visual Studio에서 작동 하 고 프로덕션 IIS 서버에서 실패 하는 웹 API2 앱 문제 해결
author: rmcmurray
description: Visual Studio에서 작동 하 고 프로덕션 IIS 서버에서 실패 하는 웹 API2 앱 문제 해결
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447029"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>Visual Studio에서 작동 하 고 프로덕션 IIS 서버에서 실패 하는 웹 API2 앱 문제 해결

> 이 문서에서는 프로덕션 IIS 서버에 배포 된 웹 API2 앱의 문제를 해결 하는 방법을 설명 합니다. 일반적인 HTTP 405 및 501 오류를 해결 합니다.
> 
> ## <a name="software-used-in-this-tutorial"></a>이 자습서에서 사용 되는 소프트웨어
> 
> 
> - [인터넷 정보 서비스 (IIS)](https://www.iis.net/) (버전 7 이상)
> - [앱 API](../../index.md) 

웹 API 앱은 일반적으로 GET, POST, PUT, DELETE, 간혹 PATCH 등의 몇 가지 HTTP 동사를 사용 합니다. 즉, 개발자는 해당 동사가 프로덕션 IIS 서버의 다른 IIS 모듈에 의해 구현 되는 상황이 발생할 수 있으며,이로 인해 Visual Studio 또는 개발 서버에서 올바르게 작동 하는 Web API 컨트롤러가 있는 상황이 발생할 수 있습니다. 프로덕션 IIS 서버에 배포 되는 경우 HTTP 405 오류를 반환 합니다.

## <a name="what-causes-http-405-errors"></a>HTTP 405 오류를 발생 시키는 원인

HTTP 405 오류 문제를 해결 하는 방법에 대 한 첫 번째 단계는 HTTP 405 오류가 실제로 무엇을 의미 하는지 이해 하는 것입니다. HTTP에 대 한 기본 관리 문서는 [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)로, http 405 상태 코드를 ***허용 되지 않는 메서드로***정의 하 고, 요청 줄에 지정 된 메서드가 요청 URI로 식별 되는 리소스에 허용 되지 않는 &quot;상황으로이 상태 코드를 추가로 설명 합니다. 즉, http 동사는 HTTP 클라이언트가 요청한 특정 URL에 대해 허용 되지 않습니다.&quot;

간단한 검토로, RFC 2616, RFC 4918 및 RFC 5789에 정의 된 가장 많이 사용 되는 HTTP 메서드는 다음과 같습니다.

| HTTP 메서드 | Description |
| --- | --- |
| **GET** | 이 메서드는 URI에서 데이터를 검색 하는 데 사용 되며, 가장 많이 사용 되는 HTTP 메서드입니다. |
| **HEAD** | 이 메서드는 단순히 HTTP 상태를 검색 하는 요청 URI에서 데이터를 검색 하지 않는다는 점을 제외 하 고 GET 메서드와 매우 유사 합니다. |
| **POST** | 이 메서드는 일반적으로 새 데이터를 URI로 보내는 데 사용 됩니다. POST는 종종 양식 데이터를 전송 하는 데 사용 됩니다. |
| **PUT** | 이 메서드는 일반적으로 원시 데이터를 URI로 보내는 데 사용 됩니다. PUT은 Web API 응용 프로그램에 JSON 또는 XML 데이터를 전송 하는 데 종종 사용 됩니다. |
| **DELETE** | 이 메서드는 URI에서 데이터를 제거 하는 데 사용 됩니다. |
| **OPTIONS** | 이 메서드는 일반적으로 URI에 대해 지원 되는 HTTP 메서드 목록을 검색 하는 데 사용 됩니다. |
| **이동 복사** | 이러한 두 가지 메서드는 WebDAV와 함께 사용 되며 자체의 용도에 대 한 설명이 필요 합니다. |
| **MKCOL** | 이 메서드는 WebDAV와 함께 사용 되며 지정 된 URI에 컬렉션 (예: 디렉터리)을 만드는 데 사용 됩니다. |
| **PROPFIND PROPPATCH** | 이러한 두 메서드는 WebDAV에서 사용 되며, URI에 대 한 속성을 쿼리하거나 설정 하는 데 사용 됩니다. |
| **잠금 잠금 해제** | 이러한 두 메서드는 WebDAV에서 사용 되며, 작성할 때 요청 URI에 의해 식별 되는 리소스를 잠그거나 잠금 해제 하는 데 사용 됩니다. |
| **PATCH** | 이 메서드는 기존 HTTP 리소스를 수정 하는 데 사용 됩니다. |

이러한 HTTP 메서드 중 하나가 서버에서 사용 하도록 구성 된 경우 서버는 HTTP 상태 및 요청에 적절 한 기타 데이터를 사용 하 여 응답 합니다. 예를 들어 GET 메서드는 HTTP 200 ***OK*** 응답을 받을 수 있으며 PUT 메서드는 Http 201 ***생성*** 응답을 받을 수 있습니다.

서버에서 사용할 수 있도록 HTTP 메서드가 구성 되지 않은 경우 서버는 HTTP 501 ***구현 되지 않음*** 오류와 함께 응답 합니다.

그러나 HTTP 메서드가 서버에서 사용 하도록 구성 되었지만 지정 된 URI에 대해 사용 하지 않도록 설정 된 경우 서버는 HTTP 405 ***메서드를 사용할 수 없음*** 오류를 사용 하 여 응답 합니다.

## <a name="example-http-405-error"></a>예제 HTTP 405 오류

다음 예제 HTTP 요청 및 응답은 HTTP 클라이언트가 웹 서버에서 Web API 앱에 값을 삽입 하려고 시도 하는 상황을 보여 줍니다. 서버는 PUT 메서드가 허용 되지 않는다는 내용의 HTTP 오류를 반환 합니다.

HTTP 요청:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP 응답:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

이 예제에서 HTTP 클라이언트는 웹 서버에서 Web API 응용 프로그램에 대 한 URL에 유효한 JSON 요청을 보냈지만 서버에서 HTTP 405 오류 메시지를 반환 했습니다 .이 메시지는 PUT 메서드가 URL에 허용 되지 않았음을 나타냅니다. 반대로 요청 URI가 웹 API 응용 프로그램에 대 한 경로와 일치 하지 않는 경우 서버는 HTTP 404 ***찾을 수 없음*** 오류를 반환 합니다.

## <a name="resolve-http-405-errors"></a>HTTP 405 오류 해결

특정 HTTP 동사가 허용 되지 않는 이유는 여러 가지가 있지만 IIS에서이 오류가 발생 하는 가장 큰 원인은 다음과 같습니다. 동일한 동사/메서드에 대해 여러 처리기가 정의 되 고 처리기 중 하나가 요청 처리에서 예상한 처리기를 차단 하 고 있습니다. 설명 방식으로 IIS는 *applicationhost.config* 및 *web.config* 파일의 주문 처리기 항목을 기반으로 처음부터 마지막으로 처리기를 처리 합니다. 여기서 경로, 동사, 리소스 등의 첫 번째 일치 하는 조합이 요청을 처리 하는 데 사용 됩니다.

다음 예제는 PUT 메서드를 사용 하 여 Web API 응용 프로그램에 데이터를 전송할 때 HTTP 405 오류를 반환 하는 IIS 서버의 *applicationhost.config* 파일에서 발췌 한 것입니다. 이 발췌문에서는 몇 가지 HTTP 처리기가 정의 되 고 각 처리기는 구성 된 다른 HTTP 메서드 집합을 가집니다. 목록의 마지막 항목은 다른 처리기에 chanc 된 후 사용 되는 기본 처리기 인 정적 콘텐츠 처리기입니다. e: 요청을 검토 합니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

앞의 예제에서 WebDAV 처리기와 ASP.NET (Web API에 사용 됨)에 대 한 확장 URL 처리기는 별도의 HTTP 메서드 목록에 대해 명확 하 게 정의 됩니다. 이 구성으로 인해 오류가 발생 하지는 않지만 ISAPI DLL 처리기가 모든 HTTP 메서드에 대해 구성 되어 있습니다. 그러나 HTTP 405 오류 문제를 해결할 때 이와 같은 구성 설정을 고려해 야 합니다.

위의 예제에서 ISAPI DLL 처리기는 문제가 되지 않았습니다. 실제로 IIS 서버의 *applicationhost.config* 파일에 문제가 정의 되지 않았습니다. Visual Studio에서 web API 응용 프로그램을 만들 때 *web.config 파일에서* 발생 한 항목으로 인해 문제가 발생 했습니다. 응용 프로그램의 *web.config* 파일에서 발췌 한 다음은 문제의 위치를 보여 줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

이 발췌문에서는 ASP.NET에 대 한 확장 URL 처리기가 웹 API 응용 프로그램과 함께 사용 될 추가 HTTP 메서드를 포함 하도록 다시 정의 됩니다. 그러나 WebDAV 처리기에 대해 유사한 HTTP 메서드 집합이 정의 되어 있기 때문에 충돌이 발생 합니다. 웹 API 응용 프로그램을 포함 하는 웹 사이트에서 WebDAV를 사용 하지 않도록 설정한 경우에도이 특정 경우에 WebDAV 처리기는 IIS에서 정의 되 고 로드 됩니다. HTTP PUT 요청을 처리 하는 동안 IIS는 PUT 동사에 대해 정의 되어 있으므로 WebDAV 모듈을 호출 합니다. WebDAV 모듈이 호출 되 면 해당 구성을 확인 하 고 사용 하지 않도록 설정 된 것을 확인 하 여 WebDAV 요청과 유사한 모든 요청에 대해 HTTP 405 ***메서드를 사용할 수 없음*** 오류가 반환 됩니다. 이 문제를 해결 하려면 웹 API 응용 프로그램이 정의 된 웹 사이트에 대 한 HTTP 모듈 목록에서 WebDAV를 제거 해야 합니다. 다음 예제에서는 다음과 같은 결과를 보여 줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

이 시나리오는 응용 프로그램이 개발 환경에서 IIS 프로덕션 환경으로 게시 된 후에 발생 하며,이는 처리기/모듈의 목록이 개발 환경과 프로덕션 환경 간에 다르기 때문에 발생 합니다. 예를 들어 Visual Studio 2012 이상 버전을 사용 하 여 Web API 응용 프로그램을 개발 하는 경우 IIS Express는 테스트를 위한 기본 웹 서버입니다. 이 개발 웹 서버는 서버 제품에서 제공 되는 전체 IIS 기능을 축소 한 버전으로,이 개발 웹 서버에는 개발 시나리오에 추가 된 몇 가지 변경 내용이 포함 되어 있습니다. 예를 들어 WebDAV 모듈은 사용 되지 않을 수도 있지만 전체 버전의 IIS를 실행 하는 프로덕션 웹 서버에 설치 되는 경우가 많습니다. IIS의 개발 버전 (IIS Express)은 WebDAV 모듈을 설치 하지만 WebDAV 모듈의 항목은 의도적으로 주석 처리 되어 있으므로 IIS Express 구성을 특별히 변경 하지 않는 한 WebDAV 모듈이 IIS Express에 로드 되지 않습니다. IIS Express 설치에 WebDAV 기능을 추가 하는 설정입니다. 따라서 웹 응용 프로그램은 개발 컴퓨터에서 제대로 작동할 수 있지만 웹 API 응용 프로그램을 프로덕션 IIS 웹 서버에 게시할 때 HTTP 405 오류가 발생할 수 있습니다.

## <a name="http-501-errors"></a>HTTP 501 오류

* 서버에서 특정 기능을 구현 하지 않았음을 나타냅니다.
* 일반적으로 HTTP 요청과 일치 하는 IIS 설정에 정의 된 처리기가 없음을 의미 합니다.
  * 는 IIS에 항목이 제대로 설치 되지 않았음을 나타낼 수 있습니다.
  * 특정 HTTP 메서드를 지 원하는 처리기가 정의 되지 않도록 IIS 설정을 수정 했습니다.

이 문제를 해결 하려면 해당 모듈 또는 처리기 정의가 없는 HTTP 메서드를 사용 하려는 모든 응용 프로그램을 다시 설치 해야 합니다.

## <a name="summary"></a>요약

Http 405 오류는 HTTP 메서드가 요청 된 URL에 대해 웹 서버에서 허용 되지 않는 경우에 발생 합니다. 이 조건은 특정 동사에 대해 특정 처리기가 정의 되 고 해당 처리기가 요청을 처리할 것으로 간주 되는 처리기를 재정의 하는 경우에 주로 표시 됩니다.
