---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지 | Microsoft Docs
author: Rick-Anderson
description: 사이트 간 요청 위조 (XSRF 또는 CSRF 라고도 함)는 악의적인 웹 사이트가 interacti에 영향을 줄 수 있는 웹 호스팅 응용 프로그램에 대 한 공격입니다.
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 7c45e342bc55ece3a6b41dcc42a0f33cd3eceffd
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151863"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 사이트 간 요청 위조 (XSRF 또는 CSRF 라고도 함)는 악의적인 웹 사이트가 클라이언트 브라우저와 해당 브라우저가 신뢰 하는 웹 사이트 간의 상호 작용에 영향을 줄 수 있는 웹 호스팅 응용 프로그램에 대 한 공격입니다. 웹 브라우저에서 웹 사이트에 대 한 모든 요청과 함께 인증 토큰을 자동으로 보내기 때문에 이러한 공격을 수행할 수 있습니다. 정식 예로는 ASP.NET의 폼 인증 티켓과 같은 인증 쿠키가 있습니다. 그러나 모든 영구 인증 메커니즘 (예: Windows 인증, 기본 등)을 사용 하는 웹 사이트는 이러한 공격의 대상이 될 수 있습니다.
> 
> XSRF 공격은 피싱 공격과는 구분됩니다. 피싱 공격에는 피해자의 상호 작용이 필요합니다. 피싱 공격에서 악의적인 웹 사이트는 대상 웹 사이트를 모방 하 고, 공격자에 게 중요 한 정보를 제공 하는 것이 속기 됩니다. XSRF 공격에서는 종종 피해자의 상호 작용이 필요하지 않습니다. 대신 공격자가 모든 관련 쿠키를 대상 웹 사이트로 자동으로 보내는 브라우저에 의존 합니다.
> 
> 자세한 내용은 [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))를 참조 하세요.

## <a name="anatomy-of-an-attack"></a>공격 분석

XSRF 공격을 안내 하려면 온라인 뱅킹 거래를 수행 하려는 사용자를 고려 합니다. 이 사용자는 먼저 WoodgroveBank.com를 방문 하 고 로그인 합니다 .이 시점에서 응답 헤더에는 해당 인증 쿠키가 포함 됩니다.

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

인증 쿠키는 세션 쿠키 이므로 브라우저 프로세스가 종료 되 면 브라우저에서 자동으로 삭제 됩니다. 그러나 해당 시간 까지는 브라우저가 WoodgroveBank.com에 대 한 각 요청과 함께 쿠키를 자동으로 포함 합니다. 이제 사용자가 $1000을 다른 계정으로 전송 하 여 은행 사이트에서 양식을 작성 하 고 브라우저에서 서버에이 요청을 만듭니다.

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

이 작업에는 부작용이 있으므로 (통화 트랜잭션이 시작 됨) 뱅킹 사이트에서이 작업을 시작 하기 위해 HTTP POST를 요구 하도록 선택 했습니다. 서버는 요청에서 인증 토큰을 읽고, 현재 사용자의 계정 번호를 조회 하 고, 충분 한 자금이 있는지 확인 한 후 대상 계정으로 트랜잭션을 시작 합니다.

자신의 온라인 뱅킹이 완료 되 면 사용자가 뱅킹 사이트에서 다른 곳으로 이동 하 여 웹의 다른 위치를 방문 합니다. 이러한 사이트 중 하나 – fabrikam.com – iframe 내에 포함 된 페이지에 대해 다음 태그를 포함 합니다 &lt; &gt; .

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

그러면 브라우저에서이 요청을 수행 합니다.

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

공격자는 사용자에 게 대상 웹 사이트에 대 한 유효한 인증 토큰이 남아 있을 수 있음을 알고 있으며 Javascript의 작은 조각을 사용 하 여 브라우저에서 대상 사이트에 대 한 HTTP POST를 자동으로 수행 하도록 합니다. 인증 토큰이 여전히 유효한 경우 은행 사이트에서 공격자가 선택한 계정으로 $250를 전송 하기 시작 합니다.

### <a name="ineffective-mitigations"></a>비효율적인 완화

위의 시나리오에서 WoodgroveBank.com는 SSL을 통해 액세스 되 고 있으며 SSL 전용 인증 쿠키가 있으므로 공격을 차단할 수 없다는 사실을 기억해 두어야 합니다. 공격자는 자신의 form 요소에 [URI 체계](http://en.wikipedia.org/wiki/URI_scheme) (https)를 지정할 수 &lt; &gt; 있으며, 해당 쿠키가 의도 한 대상의 uri 체계와 일치 하는 경우 브라우저는 계속 해 서 만료 되지 않은 쿠키를 대상 사이트로 보냅니다.

신뢰할 수 있는 사이트를 방문 하면 안전 하 게 온라인 상태를 유지 하는 것이 좋습니다. 이에 대 한 몇 가지 사항이 있지만 아쉽게도이는 실용적이 지 않습니다. 사용자가 로컬 뉴스 사이트를 "신뢰" 하 고 ConsolidatedMessenger.com 해당 사이트를 대신 방문 하 게 될 것입니다. 그러나이 사이트에는 공격자가 fabrikam.com에서 실행 되는 것과 동일한 코드 조각을 삽입할 수 있는 XSS 취약성이 있습니다.

들어오는 요청에 도메인을 참조 하는 [Referer 헤더가](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 있는지 확인할 수 있습니다. 그러면 타사 도메인에서 알지 못하는 요청이 중지 됩니다. 그러나 일부 사람들은 개인 정보 보호를 위해 브라우저의 Referer 헤더를 사용 하지 않도록 설정 하 고, 공격자가 안전 하지 않은 특정 소프트웨어를 설치한 경우 해당 헤더를 스푸핑할 수도 있습니다. [Referer 헤더](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 를 확인 하는 것은 XSRF 공격을 방지 하는 안전한 방법으로 간주 되지 않습니다.

## <a name="web-stack-runtime-xsrf-mitigations"></a>웹 스택 런타임 XSRF 완화

ASP.NET 웹 스택 런타임은 [동기화 토큰 패턴](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern) 의 변형을 사용 하 여 XSRF 공격 으로부터 보호 합니다. 동기화 토큰 패턴의 일반적인 형태는 인증 토큰 외에도 각 HTTP POST를 사용 하 여 서버에 두 개의 XSRF 토큰을 제출 하는 것입니다. 하나는 쿠키로, 다른 하나는 폼 값입니다. 공격자가 ASP.NET 런타임에 의해 생성 된 토큰 값을 결정적 이거나 예측 가능 하지 않습니다. 토큰을 제출할 때 서버는 두 토큰이 비교 검사를 통과 하는 경우에만 요청을 계속할 수 있도록 허용 합니다.

XSRF 요청 확인 *세션 토큰* 은 HTTP 쿠키로 저장 되며 현재 페이로드에 다음 정보가 포함 되어 있습니다.

- 임의의 128 비트 식별자로 구성 된 보안 토큰입니다.   
 다음 이미지는 Internet Explorer F12 개발자 도구를 사용 하 여 표시 되는 XSRF 요청 확인 세션 토큰을 보여 줍니다 .이는 현재 구현 이며 변경 될 수도 있습니다.

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*필드 토큰* 은로 저장 `<input type="hidden" />` 되며 해당 페이로드에 다음 정보가 포함 됩니다.

- 로그인 한 사용자의 사용자 이름입니다 (인증 된 경우).
- [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)에서 제공 하는 추가 데이터입니다.

XSRF 토큰의 페이로드는 암호화 되 고 서명 되므로 도구를 사용 하 여 토큰을 검사할 때 사용자 이름을 볼 수 없습니다. 웹 응용 프로그램에서 ASP.NET 4.0를 대상으로 하는 경우에는 [MachineKey](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) 루틴이 암호화 서비스를 제공 합니다. 웹 응용 프로그램이 ASP.NET 4.5 이상을 대상으로 하는 경우 암호화 서비스는 더 나은 성능, 확장성 및 보안을 제공 하는 [MachineKey 보호](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) 루틴에서 제공 됩니다. 자세한 내용은 다음 블로그 게시물을 참조 하세요.

- [ASP.NET 4.5, pt. 1의 암호화 기능 향상](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5, pt. 2의 암호화 기능 향상](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5, pt. 3의 암호화 기능 향상](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>토큰 생성

XSRF 토큰을 생성 하려면 [@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx) Razor 페이지에서 MVC 뷰 또는 ()의 메서드를 호출 합니다 @AntiForgery.GetHtml . 런타임은 다음 단계를 수행 합니다.

1. 현재 HTTP 요청에 XSRF 세션 토큰 (XSRF 쿠키 RequestVerificationToken)이 이미 포함 되어 있는 경우 \_ \_ 보안 토큰이 해당 토큰에서 추출 됩니다. HTTP 요청에 XSRF 세션 토큰이 포함 되어 있지 않거나 보안 토큰의 추출이 실패 하면 새로운 임의 XSRF 토큰이 생성 됩니다.
2. XSRF 필드 토큰은 위의 보안 토큰 (1) 및 현재 로그인 한 사용자의 id를 사용 하 여 생성 됩니다. 사용자 id를 확인 하는 방법에 대 한 자세한 내용은 아래의 **[특수 지원이 있는 시나리오](#_Scenarios_with_special)** 섹션을 참조 하세요. 또한 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) 가 구성 된 경우 런타임은 [getadditionaldata](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) 메서드를 호출 하 고 반환 된 문자열을 필드 토큰에 포함 합니다. 자세한 내용은 **[구성 및 확장성](#_Configuration_and_extensibility)** 섹션을 참조 하십시오.
3. 새 XSRF 토큰이 단계 (1)에서 생성 된 경우이를 포함 하는 새 세션 토큰이 만들어지고 아웃 바운드 HTTP 쿠키 컬렉션에 추가 됩니다. 단계 (2)의 필드 토큰은 요소에 래핑됩니다 `<input type="hidden" />` .이 HTML 태그는 또는의 반환 값이 됩니다 `Html.AntiForgeryToken()` `AntiForgery.GetHtml()` .

## <a name="validating-the-tokens"></a>토큰 유효성 검사

들어오는 앤티 XSRF 토큰의 유효성을 검사 하기 위해 개발자는 MVC 작업 또는 컨트롤러에 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) 특성을 포함 하거나 `@AntiForgery.Validate()` 해당 Razor 페이지에서 호출 합니다. 런타임은 다음 단계를 수행 합니다.

1. 들어오는 세션 토큰 및 필드 토큰을 읽고 각 토큰에서 추출 된 XSRF 토큰을 읽습니다. XSRF 토큰은 생성 루틴에서 단계 마다 동일 해야 합니다 (2).
2. 현재 사용자가 인증 된 경우 사용자의 사용자 이름은 필드 토큰에 저장 된 사용자 이름과 비교 됩니다. 사용자 이름은와 일치 해야 합니다.
3. [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 가 구성 된 경우 런타임은 *validateadditionaldata* 메서드를 호출 합니다. 메서드는 부울 값 *true* 를 반환 해야 합니다.

유효성 검사가 성공 하면 요청을 계속할 수 있습니다. 유효성 검사가 실패 하면 프레임 워크에서 *HttpAntiForgeryException* 를 throw 합니다.

## <a name="failure-conditions"></a>오류 조건

ASP.NET 웹 Stack Runtime v2부터 유효성 검사 중에 발생 하는 모든 *HttpAntiForgeryException* 에는 무엇이 잘못 되었는지에 대 한 자세한 정보가 포함 됩니다. 현재 정의 된 오류 조건은 다음과 같습니다.

- 세션 토큰 또는 폼 토큰이 요청에 없습니다.
- 세션 토큰 또는 폼 토큰을 읽을 수 없습니다. 가장 가능성이 높은 원인은 ASP.NET 웹 스택 런타임의 일치 하지 않는 버전을 실행 하는 팜 또는 &lt; &gt; Web.config의 machineKey 요소가 컴퓨터 간에 서로 다른 팜을 실행 하는 것입니다. Fiddler와 같은 도구를 사용 하 여 XSRF 토큰으로 변조 하 여이 예외를 강제로 적용할 수 있습니다.
- 세션 토큰 및 필드 토큰이 교환 되었습니다.
- 세션 토큰과 필드 토큰에 일치 하지 않는 보안 토큰이 포함 되어 있습니다.
- 필드 토큰에 포함 된 사용자 이름이 현재 로그인 한 사용자의 사용자 이름과 일치 하지 않습니다.
- *[IAntiForgeryAdditionalDataProvider Additionaldata](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* 메서드에서 *false* 를 반환 했습니다.

XSRF 기능을 통해 토큰을 생성 하거나 유효성을 검사 하는 동안 추가 검사를 수행할 수도 있으며, 이러한 검사 중에 오류가 발생 하면 예외가 throw 될 수 있습니다. 자세한 내용은 [WIF/ACS/클레임 기반 인증](#_WIF_ACS) 및 **[구성 및 확장성](#_Configuration_and_extensibility)** 섹션을 참조 하세요.

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>특별 한 지원이 있는 시나리오

### <a name="anonymous-authentication"></a>익명 인증

XSRF 시스템은 익명 사용자에 대 한 특별 한 지원을 포함 합니다. 여기서 "anonymous"는 *IIdentity* 속성이 *false* 를 반환 하는 사용자로 정의 됩니다. 시나리오에는 사용자를 식별 하기 위해 응용 프로그램이 *IIdentity* 이외의 메커니즘을 사용 하는 사용자 지정 인증 스키마 및 로그인 페이지에 XSRF 보호를 제공 하는 작업이 포함 됩니다.

이러한 시나리오를 지원 하기 위해 세션 및 필드 토큰이 임의로 생성 된 128 비트 불투명 식별자 인 보안 토큰으로 조인 됨을 기억 하십시오. 이 보안 토큰은 사용자가 사이트를 탐색할 때 개별 사용자의 세션을 추적 하는 데 사용 되므로 익명 식별자의 용도를 효과적으로 제공 합니다. 위에서 설명한 생성 및 유효성 검사 루틴의 사용자 이름 대신 빈 문자열이 사용 됩니다.

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/클레임 기반 인증

일반적으로 .NET Framework에 기본 제공 된 *IIdentity* 클래스에는 특정 응용 프로그램 내에서 특정 사용자를 고유 하 게 식별 하기에 충분 한 *IIdentity.Name* 속성이 있습니다. 예를 들어 *FormsIdentity.Name* 는 해당 데이터베이스에 따라 모든 응용 프로그램에 대해 고유한 멤버 자격 데이터베이스에 저장 된 사용자 이름을 반환 하 고 *WindowsIdentity.Name* 는 사용자의 도메인 정규화 된 id를 반환 합니다. 이러한 시스템은 인증을 제공 하지 않습니다. 또한 응용 프로그램에 대 한 사용자를 *식별* 합니다.

반면 클레임 기반 인증은 반드시 특정 사용자를 식별 해야 하는 것은 아닙니다. 대신, *ClaimsPrincipal* 및 *ClaimsIdentity* 형식은 *클레임* 인스턴스 집합에 연결 됩니다. 여기서 개별 클레임은 "is 18 + years of age" 또는 "관리자입니다." 일 수 있습니다. 사용자가 반드시 식별 되지 않았기 때문에 런타임은 *ClaimsIdentity.Name* 속성을이 특정 사용자의 고유 식별자로 사용할 수 없습니다. 팀에서는 *ClaimsIdentity.Name* 가 *null* 을 반환 하거나, 친숙 한 (표시) 이름을 반환 하거나, 사용자의 고유 식별자로 사용 하기에 적합 하지 않은 문자열을 반환 하는 실제 예를 살펴보았습니다.

클레임 기반 인증을 사용 하는 대부분의 배포는 특히 ACS ( [Azure Access Control Service](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) )를 사용 합니다. 개발자는 ACS를 사용 하 여 개별 *id 공급자* (예: ADFS, Microsoft 계정 공급자, yahoo!와 같은 openid connect 공급자 등)를 구성 하 고 id 공급자는 *이름 식별자* 를 반환할 수 있습니다. 이러한 이름 식별자에는 전자 메일 주소와 같은 PII (개인적으로 식별이 가능한 정보)가 포함 될 수도 있고, 익명화 수 있습니다. 에 관계 없이 튜플 (id 공급자, 이름 식별자)은 사이트를 검색 하는 동안 특정 사용자에 대 한 적절 한 추적 토큰 역할을 하기 때문에 ASP.NET 웹 스택 런타임은 XSRF 필드 토큰을 생성 하 고 유효성을 검사할 때 사용자 이름 대신 튜플을 사용할 수 있습니다. Id 공급자와 이름 식별자에 대 한 특정 Uri는 다음과 같습니다.

- `https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

자세한 내용은이 [ACS 문서 페이지](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) 를 참조 하세요.

토큰을 생성 하거나 유효성을 검사할 때 ASP.NET 웹 스택 런타임은 런타임에 형식에 대 한 바인딩을 시도 합니다.

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` (WIF SDK의 경우)
- `System.Security.Claims.ClaimsIdentity` (.NET 4.5의 경우).

이러한 형식이 존재 하 고 현재 사용자의 *IIIIdentity* 이 이러한 형식 중 하나를 구현 하거나 서브 클래스 하는 경우 XSRF 기능은 토큰을 생성 하 고 유효성을 검사할 때 사용자 이름 대신 (id 공급자, 이름 식별자) 튜플을 사용 합니다. 이러한 튜플이 없는 경우 요청이 실패 하 고, 사용 중인 특정 클레임 기반 인증 메커니즘을 이해 하도록 XSRF 시스템을 구성 하는 방법을 개발자에 게 설명 하는 오류가 표시 됩니다. 자세한 내용은 **[구성 및 확장성](#_Configuration_and_extensibility)** 섹션을 참조 하세요.

### <a name="oauth--openid-authentication"></a>OAuth/Openid connect 인증

마지막으로, XSRF 기능은 OAuth 또는 Openid connect 인증을 사용 하는 응용 프로그램에 대 한 특별 한 지원을 제공 합니다. 이 지원은 추론을 기반으로 합니다. 현재 *IIdentity.Name* 가 http://또는 https://로 시작 하는 경우에는 기본 stringcomparison.ordinalignorecase 비교자 대신 서 수 비교자를 사용 하 여 사용자 이름 비교가 수행 됩니다.

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>구성 및 확장성

때로는 개발자가 XSRF 생성 및 유효성 검사 동작을 보다 강력 하 게 제어할 수 있습니다. 예를 들어 HTTP 쿠키를 응답에 자동으로 추가 하는 MVC 및 웹 페이지 도우미의 기본 동작은 바람직하지 않으며 개발자는 다른 곳에서 토큰을 유지 하려고 할 수 있습니다. 이를 지원 하기 위한 두 가지 Api가 있습니다.

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*Gettokens* 메서드는 기존 XSRF request 확인 세션 토큰 (null 일 수 있음)을 입력으로 사용 하 고 새 XSRF 요청 확인 세션 토큰 및 필드 토큰을 출력으로 생성 합니다. 토큰은 단순히 장식이 없는 불투명 문자열입니다. *Formtoken* 값은 입력 태그에 래핑되지 않습니다 &lt; &gt; . *NewCookieToken* 값은 null 일 수 있습니다. 이 문제가 발생 하는 경우 *oldCookieToken* 값은 여전히 유효 하며 새 응답 쿠키를 설정 하지 않아도 됩니다. *Gettokens* 호출자는 필요한 모든 응답 쿠키를 유지 하거나 필요한 태그를 생성 하는 일을 담당 합니다. *Gettokens* 메서드 자체는 응답을 부작용으로 변경 하지 않습니다. *Validate* 메서드는 들어오는 세션과 필드 토큰을 사용 하 여 위의 유효성 검사 논리를 실행 합니다.

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

개발자는 응용 프로그램 시작에서 XSRF 시스템을 구성할 수 있습니다 \_ . 구성이 프로그래밍 방식입니다. 정적 *AntiForgeryConfig* 형식의 속성은 아래에 설명 되어 있습니다. 클레임을 사용 하는 대부분의 사용자는 UniqueClaimTypeIdentifier 속성을 설정 하려고 합니다.

| **속성** | **설명** |
| --- | --- |
| **AdditionalDataProvider** | 토큰을 생성 하는 동안 추가 데이터를 제공 하 고 토큰 유효성 검사 중에 추가 데이터를 사용 하는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 입니다. 기본값은 *null* 입니다. 자세한 내용은 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 섹션을 참조 하세요. |
| **CookieName** | XSRF 세션 토큰을 저장 하는 데 사용 되는 HTTP 쿠키의 이름을 제공 하는 문자열입니다. 이 값을 설정 하지 않으면 응용 프로그램의 배포 된 가상 경로에 따라 이름이 자동으로 생성 됩니다. 기본값은 *null* 입니다. |
| **RequireSsl** | SSL 보안 채널을 통해 XSRF 토큰을 제출 해야 하는지 여부를 지정 하는 부울입니다. 이 값이 *true* 이면 자동으로 생성 되는 모든 쿠키에 "secure" 플래그가 설정 되 고, SSL을 통해 제출 되지 않은 요청 내에서 호출 된 경우 XSRF api가 throw 됩니다. 기본 값은 *false* 입니다. |
| **SuppressIdentityHeuristicChecks** | XSRF 시스템에서 클레임 기반 id에 대 한 지원을 비활성화 해야 하는지 여부를 지정 하는 부울입니다. 이 값이 *true* 이면 시스템은 *IIdentity.Name* 이 고유한 사용자별 식별자로 사용 하기에 적합 한 것으로 가정 하 고 [WIF/ACS/클레임 기반 인증](#_WIF_ACS) 섹션에 설명 된 대로 특수 한 *IClaimsIdentity* 또는 *ClClaimsIdentity* 를 시도 하지 않습니다. 기본값은 `false`입니다. |
| **UniqueClaimTypeIdentifier** | 고유한 사용자별 식별자로 사용 하기에 적합 한 클레임 형식을 나타내는 문자열입니다. 이 값을 설정 하 고 현재 *IIdentity* 가 클레임 기반 인 경우 시스템은 *UniqueClaimTypeIdentifier* 에 지정 된 유형의 클레임을 추출 하려고 시도 하며, 필드 토큰을 생성할 때 사용자의 사용자 이름 대신 해당 값이 사용 됩니다. 클레임 유형을 찾을 수 없는 경우 시스템에서 요청이 실패 합니다. 기본값은 *null* 입니다 .이 값은 시스템에서 사용자의 사용자 이름 대신 앞에서 설명한 대로 (id 공급자, 이름 식별자) 튜플을 사용 해야 함을 나타냅니다. |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 형식을 사용 하면 개발자가 각 토큰에서 추가 데이터를 라운드트립 하 여 XSRF 시스템의 동작을 확장할 수 있습니다. *Getadditionaldata* 메서드는 필드 토큰이 생성 될 때마다 호출 되며 반환 값은 생성 된 토큰에 포함 됩니다. 구현자는 타임 스탬프, nonce 또는이 메서드에서 원하는 다른 값을 반환할 수 있습니다.

마찬가지로, *Validateadditionaldata* 메서드는 필드 토큰의 유효성을 검사할 때마다 호출 되며, 토큰에 포함 된 "추가 데이터" 문자열은 메서드에 전달 됩니다. 유효성 검사 루틴은 제한 시간 (토큰을 만들 때 저장 된 시간에 대해 현재 시간을 확인 하 여), nonce 검사 루틴 또는 다른 원하는 논리를 구현할 수 있습니다.

## <a name="design-decisions-and-security-considerations"></a>디자인 결정 및 보안 고려 사항

세션 및 필드 토큰을 연결 하는 보안 토큰은 XSRF 공격에 대해 익명/인증 되지 않은 사용자를 보호 하려는 경우에만 기술적으로 필요 합니다. 사용자가 인증 되 면 인증 토큰 자체 (쿠키 형식으로 전송 됨)가 동기화 장치 토큰 쌍의 절반으로 사용 될 수 있습니다. 그러나 인증 되지 않은 사용자가 적중 한 로그인 페이지를 보호 하는 유효한 시나리오가 있으며, 인증 된 사용자의 경우에도 항상 보안 토큰을 생성 하 고 유효성을 검사 하 여 XSRF 논리가 더 간단해 집니다. 또한 공격자가 세션 토큰을 설정 하거나 추측 하는 것이 다른 장애물 수 있으므로 공격자가 필드 토큰을 손상 시키는 경우 추가 보호 기능을 제공 합니다.

단일 도메인에서 여러 응용 프로그램을 호스트 하는 경우에는 주의 해야 합니다. 예를 들어 *example1.cloudapp.net* 및 *example2.cloudapp.net* 가 서로 다른 호스트인 경우에도 *\* cloudapp.net* 도메인의 모든 호스트 간에 암시적 트러스트 관계가 있습니다. 이 암시적 트러스트 관계 [를 사용 하면 신뢰할 수 없는 호스트가 서로 다른 쿠키에 영향을 줄 수 있습니다](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) . AJAX 요청을 제어 하는 동일한 원본 정책이 반드시 HTTP 쿠키에 적용 되는 것은 아닙니다. ASP.NET 웹 스택 런타임은 사용자 이름이 필드 토큰에 포함 된다는 것을 완화 하는 기능을 제공 합니다. 따라서 악의적인 하위 도메인에서 세션 토큰을 덮어쓸 수 있는 경우에도 사용자에 대해 유효한 필드 토큰을 생성할 수 없습니다. 그러나 이러한 환경에서 호스트 되는 경우에는 기본 제공 되는 XSRF 루틴이 여전히 세션 하이재킹 또는 로그인 XSRF에 대해 방어할 수 없습니다.

XSRF 루틴은 현재 [클릭 재 킹](https://www.owasp.org/index.php/Clickjacking)으로부터 방어 하지 않습니다. 클릭 재 킹에 대해 스스로 방어 하려는 응용 프로그램은 각 응답과 함께 X 프레임 옵션: SAMEORIGIN 헤더를 전송 하 여 쉽게 수행할 수 있습니다. 이 헤더는 모든 최신 브라우저에서 지원 됩니다. 자세한 내용은 [IE 블로그](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx), [SDL 블로그](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)및 [OWASP](https://www.owasp.org/index.php/Clickjacking)를 참조 하세요. ASP.NET 웹 스택 런타임은 일부 향후 릴리스에서는 응용 프로그램이이 공격 으로부터 자동으로 보호 되도록 MVC 및 웹 페이지 XSRF 도우미가이 헤더를 자동으로 설정 하도록 합니다.

웹 개발자는 사이트가 XSS 공격에 취약 하지 않은지 지속적으로 확인 해야 합니다. XSS 공격은 매우 강력 하며, 성공적인 익스플로잇은 XSRF 공격에 대해 ASP.NET 웹 스택 런타임 방어를 중단 시킬 수도 있습니다.

## <a name="acknowledgment"></a>승인

[@LeviBroderick](https://twitter.com/LeviBroderick)에서 많은 ASP.NET 보안 코드를 작성 한 사람이이 정보를 대량으로 작성 했습니다.
