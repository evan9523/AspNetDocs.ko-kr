---
title: ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플
author: blowdart
description: ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440849"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a>ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플

.NET Framework 4.7는 [SameSite](https://www.owasp.org/index.php/SameSite) 특성에 대 한 기본 제공 지원을 제공 하지만 원래 표준을 준수 합니다.
패치 된 동작이 `SameSite.None`의 의미를 변경 하 여 값을 전혀 내보내지 않고 `None`값으로 특성을 내보냅니다. 값을 내보내지 않으려면 쿠키의 `SameSite` 속성을-1로 설정 하면 됩니다.

## <a name="sampleCode"></a>SameSite 특성 작성

다음은 쿠키에 SameSite 특성을 작성 하는 방법의 예입니다.

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

세션 상태에 대 한 기본 sameSite 특성은 세션 설정의 ' cookieSameSite ' 매개 변수에 설정 됩니다 `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>MVC 인증

OWIN MVC 쿠키 기반 인증에서는 쿠키 관리자를 사용 하 여 쿠키 특성을 변경할 수 있습니다. [SameSiteCookieManager](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) 는 고유한 프로젝트로 복사할 수 있는 이러한 클래스의 구현입니다. 

Owin 구성 요소가 모두 버전 4.1.0 이상으로 업그레이드 되었는지 확인 해야 합니다. `packages.config` 파일에서 모든 버전 번호가 일치 하는지 확인 합니다 (예:).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

시작 클래스에서 CookieManager를 사용 하도록 인증 구성 요소를 구성 해야 합니다.

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

쿠키 관리자는이를 지 원하는 *각* 구성 요소에서 설정 해야 합니다. 여기에는 CookieAuthentication 및 OpenIdConnectAuthentication이 포함 됩니다.

SystemWebCookieManager는 응답 쿠키 통합과 관련 하 여 [알려진 문제](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) 를 방지 하는 데 사용 됩니다.

### <a name="running-the-sample"></a>샘플 실행

샘플 프로젝트를 실행 하는 경우 초기 페이지에서 브라우저 디버거를 로드 하 고이를 사용 하 여 사이트에 대 한 쿠키 컬렉션을 확인 하세요.
Edge 및 Chrome에서이 작업을 수행 하려면 `F12`를 클릭 한 다음 `Application` 탭을 선택 하 고 `Storage` 섹션의 `Cookies` 옵션 아래에서 사이트 URL을 클릭 합니다.

![브라우저 디버거 쿠키 목록](sample/img/BrowserDebugger.png)

"SameSite 쿠키 만들기" 단추를 클릭 하면 샘플 [코드](#sampleCode)에 설정 된 값과 일치 하는 `Lax`SameSite 특성 값이 있는 위의 이미지에서 볼 수 있습니다.

## <a name="interception"></a>제어 하지 않는 쿠키 가로채기

.NET 4.5.2는 `Response.AddOnSendingHeaders`헤더 쓰기를 가로채기 위한 새 이벤트를 도입 했습니다. 이는 쿠키를 클라이언트 컴퓨터에 반환 하기 전에 가로채는 데 사용할 수 있습니다. 이 샘플에서는 브라우저가 새로운 sameSite 변경 내용을 지원 하는지 여부를 확인 하는 정적 메서드에 이벤트를 연결 하 고, 그렇지 않은 경우 새 `None` 값이 설정 된 경우에서 특성을 내보내지 않도록 쿠키를 변경 합니다.

이벤트를 처리 하 고 사용자의 코드에 복사할 수 있는 쿠키 `sameSite` 특성을 조정 하는 [예제를 보려면](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) 를 참조 하십시오.

```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

동일한 방식으로 명명 된 쿠키의 특정 동작을 변경할 수 있습니다. 아래 샘플은 `Lax`에서 `None` 값을 지 원하는 브라우저에 `None` 기본 인증 쿠키를 조정 하거나 `None`를 지원 하지 않는 브라우저에서 sameSite 특성을 제거 합니다.

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a>추가 정보
 
[Chrome 업데이트](https://www.chromium.org/updates/same-site)

[OWIN SameSite 설명서](/aspnet/samesite/owin-samesite)

[ASP.NET 설명서](/aspnet/samesite/system-web-samesite)

[.NET SameSite 패치](/aspnet/samesite/kbs-samesite)