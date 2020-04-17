---
uid: ajax/cdn/overview
title: 마이크로소프트 아약스 콘텐츠 전송 네트워크 | 마이크로 소프트 문서
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540209"
---
# <a name="microsoft-ajax-content-delivery-network"></a>Microsoft Ajax Content Delivery Network

> [!WARNING]
> 프로덕션 응용 프로그램은 CDN 자산에 대한 하드 의존성을 가져서는 안 됩니다. 응용 프로그램은 참조된 CDN 자산을 테스트하고 CDN을 사용할 수 없는 경우 대체 자산을 사용해야 합니다.
>
> Microsoft Ajax CDN에는 Azure CDN을 사용하는 것 이상의 SLA가 없습니다.
>
> [이 GitHub 문제를](https://github.com/dotnet/AspNetDocs/issues/116) 사용하여 Microsoft Ajax CDN의 문제를 보고합니다.

## <a name="table-of-contents"></a>목차

**[ajax.microsoft.com 이름이 ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**  
**[비주얼 스튜디오 .vsdoc 지원](#Visual_Studio_vsdoc_Support_19)**  
**[CDN에서 ASP.NET 아약스 사용](#Using_ASPNET_Ajax_from_the_CDN_20)**  
**[CDN에서 jQuery 사용](#Using_jQuery_from_the_CDN_21)**  
**[CDN에서 jQuery UI 사용](#Using_jQuery_UI_from_the_CDN_22)**  
**[CDN의 타사 파일](#Third-Party_Files_on_the_CDN_23)**  
  
 [cdN에서 jQuery 릴리스](#jQuery_Releases_on_the_CDN_0)  
 [cdN에서 릴리스를 마이그레이션하는 jQuery](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [cdN에서 ui 를 릴리스하는 jQuery](#jQuery_UI_Releases_on_the_CDN_2)  
 [cdN에서 j쿼리 유효성 검사 릴리스](#jQuery_Validation_Releases_on_the_CDN_3)  
 [cdN에서 모바일 릴리스를 쿼리합니다.](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [cdN에서 j쿼리 템플릿 릴리스](#jQuery_Templates_Releases_on_the_CDN_5)  
 [CDN에서 jQuery 주기 릴리스](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [cdN에서 데이터 테이블 릴리스를 쿼리합니다.](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [모더니저, CDN에서 출시](#Modernizr_Releases_on_the_CDN_8)  
 [JSHint, CDN에서 출시](#JSHint_Releases_on_the_CDN_10)  
 [CDN에서 녹아웃 릴리스](#Knockout_Releases_on_the_CDN_11)  
 [CDN에서 릴리스 세계화](#Globalize_Releases_on_the_CDN_12)  
 [CDN에서 릴리스 응답](#Respond_Releases_on_the_CDN_13)  
 [CDN에서 부트스트랩 릴리스](#Bootstrap_Releases_on_the_CDN_14)  
 [부트스트랩 터치카로젤이 CDN에서 출시됩니다.](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [CDN에서 해머.js 릴리스](#Hammerjs_Releases_on_the_CDN_19)  
 [CDN에서 웹 양식 및 아약스 릴리스에 ASP.NET](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [ASP.NET MVC 는 CDN에서 출시됩니다.](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [CDN에서 ASP.NET 시그널R 릴리스](#ASPNET_SignalR_Releases_on_the_CDN_17)

Microsoft Ajax 콘텐츠 전송 네트워크(CDN)는 jQuery와 같은 인기 있는 타사 자바스크립트 라이브러리를 호스팅하며 웹 응용 프로그램에 쉽게 추가할 수 있습니다. 예를 들어 이 CDN에서 호스팅되는 jQuery를 사용하여 페이지에 &lt;&gt; ajax.aspnetcdn.com 가리키는 스크립트 태그를 추가하기만 하면 됩니다.

CDN을 활용하면 Ajax 응용 프로그램의 성능을 크게 향상시킬 수 있습니다. CDN의 내용은 전 세계에 있는 서버에 캐시됩니다. 또한 CDN을 사용하면 브라우저가 다른 도메인에 있는 웹 사이트에 캐시된 타사 JavaScript 파일을 재사용할 수 있습니다.

CDN은 보안 소켓 계층을 사용하여 웹 페이지를 제공해야 하는 경우 SSL(HTTPS)을 지원합니다.

CDN은 해당 라이브러리의 소유자가 업로드하고 라이선스가 부여된 다음과 같은 타사 스크립트 라이브러리를 호스팅합니다.

- j쿼리 (www.jquery.com)
- j쿼리 UI (www.jqueryui.com)
- jQuery 모바일 (www.jquerymobile.com)
- j쿼리 유효성 검사 (https://jqueryvalidation.org/)
- j쿼리 주기(www.malsup.com/jquery/cycle/)
- j쿼리 데이터 테이블 (http://datatables.net/)

마이크로 소프트 아약스 CDN은 또한 마이크로 소프트에 의해 업로드 된 다음과 같은 라이브러리를 포함한다 :

- ASP.NET Ajax
- ASP.NET MVC 자바 스크립트 파일
- ASP.NET 시그널러 자바 스크립트 파일

Microsoft는 이 CDN에서 호스팅되는 타사 라이브러리의 소유권을 주장하지 않습니다. 라이브러리의 저작권 소유자는 이러한 라이브러리에 라이선스를 부여합니다. 이러한 라이브러리를 다운로드하고 사용해야 할 모든 권리는 각 저작권 소유자에 의해서만 부여됩니다. Microsoft는 Microsoft 라이브러리가 아니기 때문에 이 CDN에서 호스팅되는 타사 라이브러리에 대한 보증 또는 지적 재산권 라이선스(내재된 특허 권 없음 포함)를 제공하지 않습니다.

자바 스크립트 라이브러리를 제출하고자하고 라이브러리는 상위 자바 스크립트 라이브러리 중 http://trends.builtwith.com) 하나입니다 (에 나열된 또는 (a) 인기있는 이러한 라이브러리에 확장 / 플러그인; 또는 AjaxCDNSubmission@Microsoft.com(b) ASP.NET 사용하기에 도움이 다음 문의하시기 바랍니다 .

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a>ajax.microsoft.com 이름이 ajax.aspnetcdn.com

cdN은 microsoft.com 도메인 이름을 사용하는 데 사용되었으며 aspnetcdn.com 도메인 이름을 사용하도록 변경되었습니다. 브라우저가 microsoft.com 도메인을 참조할 때 각 요청과 함께 해당 도메인의 쿠키를 전송하기 때문에 이러한 변경은 성능을 높이기 위해 이루어졌습니다. microsoft.com 이외의 도메인 이름으로 이름을 변경하면 성능을 최대 25%까지 높일 수 있습니다. ajax.microsoft.com 계속 작동하지만 ajax.aspnetcdn.com 것이 좋습니다.

- 이전 형식:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js
- 새로운 형식:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a>비주얼 스튜디오 .vsdoc 지원

Visual Studio 2008에서 .vsdoc 파일을 올바르게 사용하려면 VS 2008 SP1이 설치되어 있는지 확인하고 vsdoc 파일에 대한 핫픽스가 설치되어 있는지 확인해야 합니다. 여기에서 다음을 얻을 수 있습니다.

- [비주얼 스튜디오 2008 SP1 다운로드](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "비주얼 스튜디오 2008 SP1 다운로드")
- [비주얼 스튜디오 2008 SP1에 대한 .vsdoc 핫픽스 다운로드](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "비주얼 스튜디오 2008 SP1에 대한 .vsdoc 핫픽스 다운로드")

Visual Studio 2010은 추가 패치 없이 .vsdoc 파일을 지원합니다.

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a>CDN에서 ASP.NET 아약스 사용

ASP.NET 4를 사용하는 경우 ASP.NET 프레임워크 스크립트에 대한 모든 요청을 CDN으로 리디렉션할 수 있습니다. 로컬 웹 서버 대신 CDN에서 스크립트를 검색하면 공용 ASP.NET 웹 사이트의 성능이 크게 향상될 수 있습니다.

스크립트 관리자 EnableCDN 속성을 사용하여 모든 ASP.NET 프레임워크 스크립트 요청을 Microsoft Ajax CDN으로 리디렉션합니다.

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a>CDN에서 jQuery 사용

다음 스크립트 요소를 페이지에 추가하여 웹 응용 프로그램에서 CDN에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.

[!code-html[Main](overview/samples/sample2.html)]

CDN에는 다음 요소를 사용할 수 있는 jQuery 스크립트의 축소된 버전도 포함되어 있습니다.

[!code-html[Main](overview/samples/sample3.html)]

CDN을 사용할 수 없는 경우 페이지가 자신의 웹 사이트의 로컬 경로에서 jQuery로 대체되도록 하려면 CDN을 참조하는 요소 바로 다음에 다음 요소를 추가합니다.

[!code-html[Main](overview/samples/sample4.html)]

다음 샘플 페이지에서는 jQuery 라이브러리의 CDN 버전을 사용하여 단추를 클릭할 때 div 요소의 내용을 표시합니다.

[!code-html[Main](overview/samples/sample5.html)]

jQuery에 대해 자세히 알아보고 [jQuery](http://jquery.com/) 웹 사이트를 방문하여 jQuery의 로컬 복사본을 다운로드할 수 있습니다.

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a>CDN에서 jQuery UI 사용

또한 CDN은 jQuery UI 라이브러리를 호스팅합니다. jQuery UI 라이브러리에는 ASP.NET 응용 프로그램에서 사용할 수 있는 다양한 위젯 및 효과 집합이 포함되어 있습니다. 예를 들어 다음 페이지에서는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker를 사용하여 팝업 일정을 표시하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample6.aspx)]

키보드를 사용하여 TextBox로 포커스를 이동하면 캘린더가 표시됩니다.

![날짜 선택기로 만든 팝업 달력](overview/_static/image1.png)

위의 코드에 CDN의 파일 세 파일을 포함해야 합니다.

- jQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 다릅니다. jQuery UI 라이브러리를 추가하기 전에 페이지에 jQuery 라이브러리를 추가해야 합니다.
- jQuery UI &mdash; 라이브러리 jQuery UI 라이브러리에는 위의 페이지에 사용된 Datepicker 위젯과 같은 모든 jQuery UI 효과 및 위젯이 포함되어 있습니다.
- jQuery UI 테마 &mdash; jQuery UI는 서로 다른 테마를 지원합니다. 위의 페이지에는 Redmond 테마를 가져오는 CSS 파일에 대한 링크가 포함되어 있습니다.

모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다. [각](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10") 테마에 대한 미리보기 이미지를 보려면 이 페이지를 방문하십시오.

jQuery UI 라이브러리에 대한 자세한 내용은 공식 [jQuery UI 웹 사이트를](http://jQueryUI.com "jQuery UI 웹 사이트")방문하십시오.

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a>CDN의 타사 파일

CDN은 가장 인기 있는 타사 자바스크립트 라이브러리를 호스팅합니다. Microsoft는 이 CDN에서 호스팅되는 타사 라이브러리의 소유권을 주장하지 않습니다. 라이브러리의 저작권 소유자는 이러한 라이브러리에 라이선스를 부여합니다. 이러한 라이브러리를 다운로드하고 사용해야 할 모든 권리는 각 저작권 소유자에 의해서만 부여됩니다. Microsoft는 Microsoft 라이브러리가 아니기 때문에 이 CDN에서 호스팅되는 타사 라이브러리에 대한 보증 또는 지적 재산권 라이선스(내재된 특허 권 없음 포함)를 제공하지 않습니다.

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a>cdN에서 jQuery 릴리스

jQuery의 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="jquery-version-350"></a>j쿼리 버전 3.5.0
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a>j쿼리 버전 3.4.1
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a>j쿼리 버전 3.4.0
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a>j쿼리 버전 3.3.1
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a>j쿼리 버전 3.2.1
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a>j쿼리 버전 3.2.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a>j쿼리 버전 3.1.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a>j쿼리 버전 3.1.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a>j쿼리 버전 3.0.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a>j쿼리 버전 2.2.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a>j쿼리 버전 2.2.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a>j쿼리 버전 2.2.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a>j쿼리 버전 2.2.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a>j쿼리 버전 2.2.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a>j쿼리 버전 2.1.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a>j쿼리 버전 2.1.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a>j쿼리 버전 2.1.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a>j쿼리 버전 2.1.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a>j쿼리 버전 2.1.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a>j쿼리 버전 2.0.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a>j쿼리 버전 2.0.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a>j쿼리 버전 2.0.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a>jQuery 버전 2.0.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a>j쿼리 버전 1.12.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a>j쿼리 버전 1.12.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a>j쿼리 버전 1.12.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a>j쿼리 버전 1.12.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a>j쿼리 버전 1.12.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a>j쿼리 버전 1.11.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a>j쿼리 버전 1.11.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a>j쿼리 버전 1.11.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a>j쿼리 버전 1.11.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a>j쿼리 버전 1.10.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a>j쿼리 버전 1.10.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a>j쿼리 버전 1.10.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a>j쿼리 버전 1.9.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a>j쿼리 버전 1.9.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a>j쿼리 버전 1.8.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a>j쿼리 버전 1.8.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a>j쿼리 버전 1.8.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a>j쿼리 버전 1.8.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a>j쿼리 버전 1.7.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a>j쿼리 버전 1.7.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a>j쿼리 버전 1.7

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a>j쿼리 버전 1.6.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a>j쿼리 버전 1.6.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a>j쿼리 버전 1.6.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a>j쿼리 버전 1.6.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a>j쿼리 버전 1.6

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a>j쿼리 버전 1.5.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a>j쿼리 버전 1.5.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a>j쿼리 버전 1.5

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a>j쿼리 버전 1.4.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a>j쿼리 버전 1.4.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a>j쿼리 버전 1.4.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a>j쿼리 버전 1.4.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a>j쿼리 버전 1.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a>j쿼리 버전 1.3.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a>cdN에서 릴리스를 마이그레이션하는 jQuery

jQuery 마이그레이션의 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="jquery-migrate-version-300"></a>jQuery 버전 마이그레이션 3.0.0

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a>jQuery 마이그레이션 버전 1.2.1

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

jQuery 마이그레이션 버전 1.2.0

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a>jQuery 마이그레이션 버전 1.1.1

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a>jQuery 마이그레이션 버전 1.1.0

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a>jQuery 마이그레이션 버전 1.0.0

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a>cdN에서 ui 를 릴리스하는 jQuery

jQuery UI 라이브러리의 다음 릴리스는 이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [j쿼리 UI 1.12.1](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN의 jQuery UI 1.12.1")
- [j쿼리 UI 1.12.0](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN의 jQuery UI 1.12.0")
- [j쿼리 UI 1.11.4](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN의 jQuery UI 1.11.4")
- [j쿼리 UI 1.11.3](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN의 jQuery UI 1.11.3")
- [j쿼리 UI 1.11.2](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN의 jQuery UI 1.11.2")
- [j쿼리 UI 1.11.1](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN의 jQuery UI 1.11.1")
- [j쿼리 UI 1.11.0](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN의 jQuery UI 1.11.0")
- [j쿼리 UI 1.10.4](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN의 jQuery UI 1.10.4")
- [j쿼리 UI 1.10.3](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN의 jQuery UI 1.10.3")
- [j쿼리 UI 1.10.2](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN의 jQuery UI 1.10.2")
- [j쿼리 UI 1.10.1](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN의 jQuery UI 1.10.1")
- [j쿼리 UI 1.10.0](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN의 jQuery UI 1.10.0")
- [j쿼리 UI 1.9.2](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN의 jQuery UI 1.9.2")
- [j쿼리 UI 1.9.1](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN의 jQuery UI 1.9.1")
- [j쿼리 UI 1.9.0](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN의 jQuery UI 1.9.0")
- [j쿼리 UI 1.8.24](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN의 jQuery UI 1.8.24")
- [j쿼리 UI 1.8.23](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN의 jQuery UI 1.8.23")
- [j쿼리 UI 1.8.22](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN의 jQuery UI 1.8.22")
- [j쿼리 UI 1.8.21](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN의 jQuery UI 1.8.21")
- [j쿼리 UI 1.8.20](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN의 jQuery UI 1.8.20")
- [j쿼리 UI 1.8.19](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN의 jQuery UI 1.8.19")
- [j쿼리 UI 1.8.18](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN의 jQuery UI 1.8.18")
- [j쿼리 UI 1.8.17](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN의 jQuery UI 1.8.17")
- [j쿼리 UI 1.8.16](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN의 jQuery UI 1.8.16")
- [j쿼리 UI 1.8.15](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN의 jQuery UI 1.8.15")
- [j쿼리 UI 1.8.14](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN의 jQuery UI 1.8.14")
- [j쿼리 UI 1.8.13](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN의 jQuery UI 1.8.13")
- [j쿼리 UI 1.8.12](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN의 jQuery UI 1.8.12")
- [jQuery UI 1.8.11](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN의 jQuery UI 1.8.11")
- [j쿼리 UI 1.8.10](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10")
- [j쿼리 UI 1.8.9](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN의 jQuery UI 1.8.9")
- [j쿼리 UI 1.8.8](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN의 jQuery UI 1.8.8")
- [j쿼리 UI 1.8.7](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN의 jQuery UI 1.8.7")
- [j쿼리 UI 1.8.6](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN의 jQuery UI 1.8.6")
- [jQuery UI 1.8.5](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a>cdN에서 j쿼리 유효성 검사 릴리스

[jQuery 유효성 검사](https://jqueryvalidation.org/ "j쿼리 유효성 검사 플러그인") 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [j쿼리 유효성 검사 1.19.1](jquery-validate/cdnjqueryvalidate1191.md "j쿼리 유효성 검사 1.19.1")
- [j쿼리 유효성 검사 1.19.0](jquery-validate/cdnjqueryvalidate1190.md "j쿼리 유효성 검사 1.19.0")
- [j쿼리 유효성 검사 1.17.0](jquery-validate/cdnjqueryvalidate1170.md "j쿼리 유효성 검사 1.17.0")
- [j쿼리 유효성 검사 1.16.0](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [j쿼리 유효성 검사 1.15.1](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [j쿼리 유효성 검사 1.15.0](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [j쿼리 유효성 검사 1.14.0](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [j쿼리 유효성 검사 1.13.1](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [j쿼리 유효성 검사 1.13.0](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [j쿼리 유효성 검사 1.12.0](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [j쿼리 유효성 검사 1.11.1](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [j쿼리 유효성 검사 1.11.0](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [j쿼리 유효성 검사 1.10.0](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [j쿼리 유효성 검사 1.9](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [j쿼리 유효성 검사 1.8.1](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 버전 1.8.1")
- [j쿼리 유효성 검사 1.8](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [j쿼리 유효성 검사 1.7](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [jQuery Validate 1.6](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [jQuery Validate 1.5.5](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a>cdN에서 모바일 릴리스를 쿼리합니다.

jQuery Mobile 라이브러리의 다음 릴리스는 이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [jQuery 모바일 1.4.5](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.5")
- [jQuery 모바일 1.4.2](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.2")
- [jQuery 모바일 1.4.1](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.1")
- [jQuery 모바일 1.4.0](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.0")
- [jQuery 모바일 1.3.2](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.2")
- [jQuery 모바일 1.3.1](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.1")
- [jQuery 모바일 1.3.0](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.0")
- [jQuery 모바일 1.2.0](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN의 jQuery Mobile 1.2.0")
- [jQuery 모바일 1.1.2](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.2")
- [jQuery 모바일 1.1.1](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.1")
- [jQuery 모바일 1.1.0](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0")
- [jQuery 모바일 1.1.0 RC 2](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0 RC2")
- [jQuery 모바일 1.0.1](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN의 jQuery Mobile 1.0.1")
- [jQuery 모바일 1.0](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN의 jQuery Mobile 1.0")
- [jQuery 모바일 1.0 RC 2](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC2")
- [jQuery 모바일 1.0 RC 1](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC1")
- [jQuery 모바일 1.0 베타 3](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a>cdN에서 j쿼리 템플릿 릴리스

jQuery 템플릿 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [jQuery 템플릿 베타 1](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a>CDN에서 jQuery 주기 릴리스

jQuery 주기 플러그인의 다음 릴리스는이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [j쿼리 주기 2.99](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [jQuery Cycle 2.94](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [jQuery Cycle 2.88](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a>cdN에서 데이터 테이블 릴리스를 쿼리합니다.

jQuery DataTables 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [jQuery DataTables 1.10.5](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [jQuery DataTables 1.10.4](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [jQuery DataTables 1.9.4](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [jQuery DataTables 1.9.3](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [jQuery DataTables 1.9.2](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [jQuery DataTables 1.9.1](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [j쿼리 데이터 테이블 1.9.0](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [jQuery DataTables 1.8.2](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a>모더니저, CDN에서 출시

[모더니즈르의](http://www.modernizr.com "모더니즈르") 다음 릴리스는 CDN에서 호스팅됩니다.

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a>JSHint, CDN에서 출시

[JSHint의](http://www.jshint.com "JSHint") 다음 릴리스는 CDN에서 호스팅됩니다.

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a>CDN에서 녹아웃 릴리스

[녹아웃의](http://www.knockoutjs.com "녹아웃") 다음 릴리스는 CDN에서 호스팅됩니다.

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a>CDN에서 릴리스 세계화

[글로벌화의](https://github.com/jquery/globalize "세계화") 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="globalize-version-100"></a>버전 1.0.0 세계화

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a>버전 세계화 0.1.1

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - 모든 문화
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - "{문화권 코드}"를 원하는 문화권 코드로 바꿉니다(예: globalize.culture.en-GB.js== CDN의 Microsoft 파일 ==이러한 라이브러리는 Microsoft에서 업로드했습니다.

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a>CDN에서 릴리스 응답

[응답의](https://github.com/scottjehl/Respond "대응") 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="respond-version-142"></a>응답 버전 1.4.2

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a>응답 버전 1.4.1

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a>응답 버전 1.4.0

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a>응답 버전 1.3.0

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a>응답 버전 1.2.0

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a>CDN에서 부트스트랩 릴리스

[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩의 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="bootstrap-version-441"></a>부트 스트랩 버전 4.4.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a>부트스트랩 버전 4.3.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a>부트스트랩 버전 4.2.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a>부트 스트랩 버전 4.1.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a>부트스트랩 버전 4.0.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a>부트스트랩 버전 3.4.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a>부트스트랩 버전 3.4.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a>부트스트랩 버전 3.3.7

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a>부트스트랩 버전 3.3.6

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a>부트스트랩 버전 3.3.5

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a>부트스트랩 버전 3.3.4

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a>부트스트랩 버전 3.3.2

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a>부트스트랩 버전 3.3.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a>부트스트랩 버전 3.3.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a>부트스트랩 버전 3.2.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a>부트스트랩 버전 3.1.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a>부트스트랩 버전 3.1.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a>부트스트랩 버전 3.0.3

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a>부트스트랩 버전 3.0.2

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a>부트스트랩 버전 3.0.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a>부트스트랩 버전 3.0.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a>부트스트랩 버전 2.3.2

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a>부트스트랩 버전 2.3.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a>부트스트랩 터치카로젤이 CDN에서 출시됩니다.

부트 스트랩 [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") 터치 카루스엘 릴리스의 다음 릴리스는 CDN에서 호스팅됩니다 :

#### <a name="bootstrap-touchcarousel-version-080"></a>부트스트랩 터치카로젤 버전 0.8.0

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a>CDN에서 해머.js 릴리스

Hammer.js [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") 릴리스의 다음 릴리스는 CDN에서 호스팅됩니다.

#### <a name="hammerjs-version-204"></a>해머.js 버전 2.0.4

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a>CDN에서 웹 양식 및 아약스 릴리스에 ASP.NET

ASP.NET 아약스 라이브러리의 다음 릴리스는 CDN에서 호스팅됩니다. 각 링크를 클릭하여 파일의 실제 목록을 확인합니다.

- [ASP.NET 웹 양식 및 아약스 버전 4.5.2](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [ASP.NET 웹 양식 및 아약스 버전 4](cdnajax4.md "ASP.NET Web Forms and Ajax 4")
- [ASP.NET 아약스 버전 3.5](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a>ASP.NET MVC 는 CDN에서 출시됩니다.

다음은 이 CDN에서 ASP.NET MVC 자바스크립트 파일이 호스팅됩니다.

#### <a name="aspnet-mvc-523"></a>ASP.NET MVC 5.2.3

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a>ASP.NET MVC 5.1

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a>ASP.NET MVC 5.0

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a>ASP.NET MVC 4.0

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a>ASP.NET MVC 3.0

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a>ASP.NET MVC 2.0

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a>ASP.NET MVC 1.0

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a>CDN에서 ASP.NET 시그널R 릴리스

다음 ASP.NET SignalR 자바 스크립트 파일은이 CDN에서 호스팅됩니다.

#### <a name="aspnet-signalr-222"></a>ASP.NET 시그널R 2.2.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a>ASP.NET 시그널R 2.2.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a>ASP.NET 시그널R 2.2.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a>ASP.NET 시그널R 2.1.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a>ASP.NET 시그널R 2.0.3

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a>ASP.NET 시그널R 2.0.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a>ASP.NET 시그널R 2.0.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a>ASP.NET 시그널R 2.0.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a>ASP.NET 시그널R 1.1.3

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a>ASP.NET 시그널R 1.1.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a>ASP.NET 시그널R 1.1.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a>ASP.NET 시그널R 1.1.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a>ASP.NET 시그널R 1.0.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

CDN의 사용 약관에 대한 자세한 내용은 [Microsoft Ajax CDN 사용 약관을](https://www.asp.net/terms-of-use "마이크로소프트 아약스 CDN 이용 약관")참조하십시오.
