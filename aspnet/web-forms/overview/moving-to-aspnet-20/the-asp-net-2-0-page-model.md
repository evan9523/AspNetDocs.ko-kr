---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다. 코드 숨결은 Src attr을 사용하여 구현 할 수 있습니다 ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542861"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 페이지 모델

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다. 코드 숨는 Src 특성 또는 지시의 CodeBehind 특성을 사용 하 여 구현될 수 있습니다. @Page ASP.NET 2.0에서 개발자는 여전히 인라인 코드와 코드 숨미기 중에서 선택할 수 있지만 코드 숨미는 모델에 대한 상당한 개선 사항이 있었습니다.

ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다. 코드 숨는 Src 특성 또는 지시의 CodeBehind 특성을 사용 하 여 구현될 수 있습니다. @Page ASP.NET 2.0에서 개발자는 여전히 인라인 코드와 코드 숨미기 중에서 선택할 수 있지만 코드 숨미는 모델에 대한 상당한 개선 사항이 있었습니다.

## <a name="improvements-in-the-code-behind-model"></a>코드 뒤 모델의 개선 사항

ASP.NET 2.0의 코드 뒤에 있는 모델의 변경 사항을 완전히 이해하려면 ASP.NET 1.x에 존재했던 모델을 신속하게 검토하는 것이 가장 좋습니다.

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x의 코드 뒤 모델

ASP.NET 1.x에서 코드 뒤 모델은 ASPX 파일(웹폼)과 프로그래밍 코드가 포함된 코드 숨결 파일로 구성되었습니다. 두 파일은 ASPX 파일의 @Page 지시문을 사용하여 연결되었습니다. ASPX 페이지의 각 컨트롤에는 코드 숨김 파일에 인스턴스 변수로 해당 선언이 있었습니다. 코드 숨김 파일에는 이벤트 바인딩을 위한 코드와 Visual Studio 디자이너에 필요한 생성된 코드도 포함되어 있습니다. 이 모델은 상당히 잘 작동했지만 ASPX 페이지의 모든 ASP.NET 요소는 코드 숨은 파일에서 해당 코드가 필요하기 때문에 코드와 콘텐츠의 진정한 분리가 없었습니다. 예를 들어 디자이너가 Visual Studio IDE 외부의 ASPX 파일에 새 서버 컨트롤을 추가한 경우 코드 숨김 파일에서 해당 컨트롤에 대한 선언이 없기 때문에 응용 프로그램이 중단됩니다.

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 코드 뒤 모델 2.0

ASP.NET 2.0은 이 모델에서 크게 향상됩니다. ASP.NET 2.0에서는 ASP.NET 2.0에 제공된 새 *부분 클래스를* 사용하여 코드 숨미는 것이 구현됩니다. ASP.NET 2.0의 코드 숨김 클래스는 클래스 정의의 일부만 포함한다는 것을 의미하는 부분 클래스로 정의됩니다. 클래스 정의의 나머지 부분은 런타임 시 또는 웹 사이트가 미리 컴파일될 때 ASPX 페이지를 사용하여 ASP.NET 2.0에 의해 동적으로 생성됩니다. @Page 지시문을 사용하여 코드 숨김 파일과 ASPX 페이지 간의 링크는 여전히 설정됩니다. 그러나 CodeBehind 또는 Src 특성 대신 ASP.NET 2.0은 이제 CodeFile 특성을 사용합니다. Inherits 특성은 페이지의 클래스 이름을 지정하는 데도 사용됩니다.

일반적인 @ 페이지 지시문은 다음과 같습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 코드 숨김 파일의 일반적인 클래스 정의는 다음과 같습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# 및 Visual Basic은 현재 부분 클래스를 지원하는 유일한 관리언어입니다. 따라서 J#을 사용하는 개발자는 ASP.NET 2.0에서 코드 뒤 모델을 사용할 수 없습니다.

개발자는 이제 자신이 만든 코드만 포함하는 코드 파일을 갖게 되므로 새 모델은 코드 숨미기 모델을 향상시킵니다. 또한 코드 숨김 파일에 인스턴스 변수 선언이 없기 때문에 코드와 콘텐츠를 진정한 분리를 제공합니다.

> [!NOTE]
> ASPX 페이지의 부분 클래스는 이벤트 바인딩이 이루어지는 위치이므로 Visual Basic 개발자는 코드 뒤에서 Handles 키워드를 사용하여 이벤트를 바인딩하여 약간의 성능 향상을 실현할 수 있습니다. C#에는 동등한 키워드가 없습니다.

## <a name="new--page-directive-attributes"></a>새 @ 페이지 지시문 특성

ASP.NET 2.0 @ 페이지 지시문에 많은 새 특성이 추가됩니다. ASP.NET 2.0의 새로운 특성은 다음과 같습니다.

## <a name="async"></a>Async

비동기 특성을 사용하면 비동기적으로 실행되도록 페이지를 구성할 수 있습니다. 이 모듈의 후반부에서 비동기 페이지를 다룹니다.

## <a name="asynctimeout"></a>비동기 시간 시간

비동기 페이지에 대한 시간 지정을 지정했습니다. 기본값은 45초입니다.

## <a name="codefile"></a>Codefile

CodeFile 특성은 Visual Studio 2002/2003의 CodeBehind 특성을 대체합니다.

### <a name="codefilebaseclass"></a>코드 파일베이스 클래스

CodeFileBaseClass 특성은 여러 페이지가 단일 기본 클래스에서 파생되는 경우에 사용됩니다. 이 특성이 없는 ASP.NET 부분 클래스를 구현하기 때문에 ASP.NETs 컴파일 엔진이 페이지의 컨트롤을 기반으로 새 멤버를 자동으로 생성하기 때문에 ASPX 페이지에 선언된 참조 컨트롤에 공유 공통 필드를 사용하는 기본 클래스가 제대로 작동하지 않습니다. 따라서 ASP.NET 두 개 이상의 페이지에 대한 공통 기본 클래스를 원하는 경우 CodeFileBaseClass 특성에서 기본 클래스를 지정한 다음 해당 기본 클래스에서 각 페이지 클래스를 파생시켜야 합니다. 이 특성을 사용할 때도 CodeFile 특성이 필요합니다.

## <a name="compilationmode"></a>편집 모드

이 특성을 사용하면 ASPX 페이지의 컴파일레이션모드 속성을 설정할 수 있습니다. 컴파일모드 속성은 **항상**, **자동**및 **안**함 값을 포함하는 열거형입니다. 기본값은 **항상**입니다. **자동** 설정을 사용하면 ASP.NET 가능하면 페이지를 동적으로 컴파일할 수 없습니다. 동적 컴파일에서 페이지를 제외하면 성능이 향상됩니다. 그러나 제외된 페이지에 컴파일해야 하는 코드가 포함된 경우 페이지를 탐색할 때 오류가 발생합니다.

## <a name="enableeventvalidation"></a>활성화이벤트유효성 검사

이 특성은 포스트백 및 콜백 이벤트의 유효성을 검사할지 여부를 지정합니다. 이 옵션을 사용하면 포스트백 또는 콜백 이벤트에 대한 인수가 확인되어 원래 렌더링한 서버 컨트롤에서 시작되었는지 확인합니다.

## <a name="enabletheming"></a>Enabletheming

이 특성은 ASP.NET 테마가 페이지에서 사용되는지 여부를 지정합니다. 기본값은 **false입니다.** ASP.NET 테마는 [모듈 10에서](profiles-themes-and-web-parts.md)다룹니다.

## <a name="linepragmas"></a>라인프라그마스

이 특성은 컴파일 중에 라인 실용모를 추가해야 하는지 여부를 지정합니다. 라인 pragmas 코드의 특정 섹션을 표시 하는 디버거에 의해 사용 되는 옵션입니다.

## <a name="maintainscrollpositiononpostback"></a>유지 보수스크롤포지션포스트백

이 특성은 포스트백 간의 스크롤 위치를 유지하기 위해 JavaScript가 페이지에 삽입되는지 여부를 지정합니다. 이 특성은 기본적으로 **false입니다.**

이 특성이 **true이면**ASP.NET &lt;&gt; 다음과 같이 보이는 스크립트 블록을 포스트백에 추가합니다.

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

이 스크립트 블록의 src는 WebResource.axd입니다. 이 리소스는 물리적 경로가 아닙니다. 이 스크립트가 요청되면 ASP.NET 동적으로 스크립트를 빌드합니다.

### <a name="masterpagefile"></a>마스터페이지파일

이 특성은 현재 페이지의 마스터 페이지 파일을 지정합니다. 경로는 상대적이거나 절대적일 수 있습니다. 마스터 페이지는 [모듈 4에서](master-pages.md)다룹니다.

## <a name="stylesheettheme"></a>Stylesheettheme

이 특성을 사용하면 ASP.NET 2.0 테마로 정의된 사용자 인터페이스 모양 속성을 재정의할 수 있습니다. 테마는 [모듈 10에서](profiles-themes-and-web-parts.md)다룹니다.

## <a name="theme"></a>테마

페이지의 테마를 지정합니다. StyleSheetTheme 특성에 대한 값을 지정하지 않은 경우 테마 특성은 페이지의 컨트롤에 적용되는 모든 스타일을 재정의합니다.

## <a name="title"></a>제목

페이지의 제목을 설정합니다. 여기에 지정된 값은 렌더링된 페이지의 &lt;제목&gt; 요소에 표시됩니다.

### <a name="viewstateencryptionmode"></a>뷰상태 암호화 모드

ViewState암호화모드 열거형의 값을 설정합니다. 사용 가능한 값은 **항상**, **자동**및 **없음**입니다. 기본값은 **자동**입니다. 이 특성이 **자동**값으로 설정되면 viewstate가 암호화되어 **등록요구뷰스테이트암호화** 메서드를 호출하여 제어 요청을 합니다.

## <a name="setting-public-property-values-via-the--page-directive"></a>@ 페이지 지시문을 통해 공용 속성 값 설정

ASP.NET 2.0에서 @Page 지시문의 또 다른 새로운 기능은 기본 클래스의 공용 속성의 초기 값을 설정하는 기능입니다. 예를 들어 기본 클래스에 **SomeText라는** 공용 속성이 있고 페이지가 로드될 때 **Hello로** 초기화하려고 한다고 가정합니다. @Page 지시문에 다음과 같이 값을 설정하기만 하면 이 작업을 수행할 수 있습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ 페이지 지시문의 **SomeText** 특성은 기본 클래스의 SomeText 속성의 초기 값을 *Hello로 설정합니다.*. 아래 비디오는 @ Page 지시문을 사용하여 기본 클래스에서 공용 속성의 초기 값을 설정하는 연습입니다.

![](the-asp-net-2-0-page-model/_static/image1.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>페이지 클래스의 새 공용 속성

다음 공용 속성은 ASP.NET 2.0의 새 속성입니다.

## <a name="apprelativetemplatesourcedirectory"></a>앱상대템플릿소스디렉터리

응용 프로그램 상대 경로를 페이지 또는 컨트롤에 반환합니다. 예를 들어 http://app/folder/page.aspx에 있는 페이지의 경우 속성은 ~/폴더/를 반환합니다.

## <a name="apprelativevirtualpath"></a>앱상대가상패스

상대 가상 디렉터리 경로를 페이지 또는 컨트롤에 반환합니다. 예를 들어 에 http://app/folder/page.aspx있는 페이지의 경우 속성은 ~/폴더/page.aspx를 반환합니다.

## <a name="asynctimeout"></a>비동기 시간 시간

비동기 페이지 처리에 사용되는 시간 시간을 가져옵니다. 비동기 페이지는 이 모듈의 후반부에서 다룹니다.

## <a name="clientquerystring"></a>클라이언트 쿼리 스트링

요청된 URL의 쿼리 문자열 부분을 반환하는 읽기 전용 속성입니다. 이 값은 URL 인코딩됩니다. HttpServerUtility 클래스의 UrlDecode 메서드를 사용하여 디코딩할 수 있습니다.

## <a name="clientscript"></a>클라이언트 스크립트

이 속성은 클라이언트 쪽 스크립트의 ASP.NETs 방출을 관리하는 데 사용할 수 있는 ClientScriptManager 개체를 반환합니다. (ClientScriptManager 클래스는 이 모듈의 후반부에서 다룹니다.)

## <a name="enableeventvalidation"></a>활성화이벤트유효성 검사

이 속성은 포스트백 및 콜백 이벤트에 대해 이벤트 유효성 검사를 사용하도록 설정할지 여부를 제어합니다. 이 옵션을 사용하면 포스트백 또는 콜백 이벤트에 대한 인수가 확인되어 원래 렌더링된 서버 컨트롤에서 시작되었는지 확인합니다.

## <a name="enabletheming"></a>Enabletheming

이 속성은 ASP.NET 2.0 테마가 페이지에 적용되는지 여부를 지정하는 부울을 얻거나 설정합니다.

## <a name="form"></a>Form

이 속성은 ASPX 페이지에서 HTML 양식을 HtmlForm 개체로 반환합니다.

## <a name="header"></a>헤더

이 속성은 페이지 헤더를 포함하는 HtmlHead 개체에 대한 참조를 반환합니다. 반환된 HtmlHead 오브젝트를 사용하여 스타일 시트, 메타 태그 등을 얻음/설정할 수 있습니다.

## <a name="idseparator"></a>IdSparator

이 읽기 전용 속성은 ASP.NET 페이지에서 컨트롤에 대 한 고유 ID를 빌드할 때 컨트롤 식별자를 분리 하는 데 사용 되는 문자를 가져옵니다. 코드에서 직접 사용하기에 적합하지 않습니다.

## <a name="isasync"></a>IsAsync

이 속성은 비동기 페이지를 허용합니다. 비동기 페이지는 이 모듈의 후반부에서 설명합니다.

## <a name="iscallback"></a>IsCallback

이 읽기 전용 속성은 페이지가 호출 백의 결과인 경우 **true를** 반환합니다. 콜백은 이 모듈의 뒷부분에서 설명합니다.

## <a name="iscrosspagepostback"></a>이스크로스페이지포스트백

이 읽기 전용 속성은 페이지가 교차 페이지 포스트백의 일부인 경우 **true를** 반환합니다. 교차 페이지 포스트백은 이 모듈의 뒷부분에서 다룹니다.

## <a name="items"></a>Items

페이지 컨텍스트에 저장된 모든 개체를 포함하는 IDictionary 인스턴스에 대한 참조를 반환합니다. 이 IDictionary 개체에 항목을 추가할 수 있으며 컨텍스트의 수명 동안 사용할 수 있습니다.

## <a name="maintainscrollpositiononpostback"></a>유지 보수스크롤포지션포스트백

이 속성은 ASP.NET 포스트백이 발생한 후 브라우저에서 페이지 스크롤 위치를 유지하는 JavaScript를 내는지 여부를 제어합니다. 이 속성에 대한 자세한 내용은 이 모듈의 앞에서 설명했습니다.

## <a name="master"></a>마스터

이 읽기 전용 속성은 마스터 페이지가 적용된 페이지에 대한 MasterPage 인스턴스에 대한 참조를 반환합니다.

## <a name="masterpagefile"></a>마스터페이지파일

페이지의 마스터 페이지 파일 이름을 가져옵니다. 이 속성은 PreInit 메서드에서만 설정할 수 있습니다.

## <a name="maxpagestatefieldlength"></a>맥스페이지스테이트필드길이

이 속성은 페이지 상태의 최대 길이를 바이트로 가져옵니다. 속성이 양수로 설정된 경우 페이지 보기 상태는 지정된 바이트 수를 초과하지 않도록 여러 숨겨진 필드로 나뉩니다. 속성이 음수인 경우 뷰 상태는 청크로 나눌 수 없습니다.

## <a name="pageadapter"></a>페이지 어댑터

요청 브라우저에 대한 페이지를 수정하는 PageAdapter 개체에 대한 참조를 반환합니다.

## <a name="previouspage"></a>Previouspage

Server.Transfer 또는 교차 페이지 포스트백의 경우 이전 페이지에 대한 참조를 반환합니다.

## <a name="skinid"></a>Skinid

페이지에 적용할 ASP.NET 2.0 스킨을 지정합니다.

## <a name="stylesheettheme"></a>Stylesheettheme

이 속성은 페이지에 적용되는 스타일 시트를 얻거나 설정합니다.

## <a name="templatecontrol"></a>템플릿 제어

페이지에 대한 포함 컨트롤에 대한 참조를 반환합니다.

## <a name="theme"></a>테마

페이지에 적용된 ASP.NET 2.0 테마의 이름을 가져옵니다. 이 값은 PreInit 메서드 앞에 설정해야 합니다.

## <a name="title"></a>제목

이 속성은 페이지 헤더에서 가져온 대로 페이지의 제목을 가져오거나 설정합니다.

## <a name="viewstateencryptionmode"></a>뷰상태 암호화 모드

페이지의 ViewState암호화 모드를 가져옵니다. 이 단원의 앞에서 이 속성에 대한 자세한 설명은 참조하세요.

## <a name="new-protected-properties-of-the-page-class"></a>페이지 클래스의 새 보호속성

다음은 ASP.NET 2.0에서 Page 클래스의 새 보호된 속성입니다.

## <a name="adapter"></a>어댑터

요청한 장치에서 페이지를 렌더링하는 ControlAdapter에 대한 참조를 반환합니다.

## <a name="asyncmode"></a>비동기 모드

이 속성은 페이지가 비동기적으로 처리되는지 여부를 나타냅니다. 코드에서 직접 사용하지 않고 런타임에서 사용하기 위한 것입니다.

## <a name="clientidseparator"></a>클라이언트ID세파레이터

이 속성은 컨트롤에 대 한 고유한 클라이언트 아이디를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다. 코드에서 직접 사용하지 않고 런타임에서 사용하기 위한 것입니다.

## <a name="pagestatepersister"></a>페이지스테이트퍼시스터

이 속성은 페이지에 대 한 PageStatePersister 개체를 반환 합니다. 이 속성은 주로 ASP.NET 컨트롤 개발자가 사용합니다.

## <a name="uniquefilepathsuffix"></a>유니크파일패스서픽스

이 속성은 브라우저를 캐싱하기 위한 파일 경로에 추가된 고유한 접미사를 반환합니다. 기본값은 \_ \_ufps= 및 6자리 숫자입니다.

## <a name="new-public-methods-for-the-page-class"></a>페이지 클래스에 대한 새 공용 메서드

다음 공개 메서드는 ASP.NET 2.0의 Page 클래스에 새로 가되었습니다.

## <a name="addonprerendercompleteasync"></a>애드온프리렌더컴량

이 메서드는 비동기 페이지 실행을 위한 이벤트 처리기 대리자를 등록합니다. 비동기 페이지는 이 모듈의 후반부에서 설명합니다.

## <a name="applystylesheetskin"></a>적용스타일시트스킨

페이지 스타일 시트의 속성을 페이지에 적용합니다.

## <a name="executeregisteredasynctasks"></a>실행등록된 동기 작업

이 메서드는 비동기 작업입니다.

### <a name="getvalidators"></a>겟검증자

지정되지 않은 유효성 검사 그룹이 없는 경우 지정된 유효성 검사 그룹 또는 기본 유효성 검사 그룹에 대한 유효성 검사기 컬렉션을 반환합니다.

## <a name="registerasynctask"></a>레지스터AsyncTask

이 메서드는 새 비동기 작업을 등록합니다. 비동기 페이지는 이 모듈의 후반부에서 다룹니다.

## <a name="registerrequirescontrolstate"></a>레지스터필요컨트롤상태

이 메서드는 ASP.NET 페이지 제어 상태를 유지 해야 합니다.

## <a name="registerrequiresviewstateencryption"></a>Register필요뷰상태암호화

이 메서드는 ASP.NET 페이지 viewstate 암호화가 필요 합니다.

## <a name="resolveclienturl"></a>해결 클라이언트Url

이미지 등에 대한 클라이언트 요청에 사용할 수 있는 상대 URL을 반환합니다.

## <a name="setfocus"></a>SetFocus

이 메서드는 페이지를 처음 로드할 때 지정 된 컨트롤에 포커스를 설정 합니다.

## <a name="unregisterrequirescontrolstate"></a>레지스터 해제컨트롤상태

이 메서드는 더 이상 제어 상태 지속성을 필요로 하지 않는 컨트롤으로 전달 되는 컨트롤을 등록 취소 합니다.

## <a name="changes-to-the-page-lifecycle"></a>페이지 수명 주기 변경

ASP.NET 2.0의 페이지 수명 주기는 크게 변경되지 않았지만 알아야 할 몇 가지 새로운 방법이 있습니다. ASP.NET 2.0 페이지 수명 주기는 아래에 설명되어 있습니다.

## <a name="preinit-new-in-aspnet-20"></a>프리이니트 (ASP.NET 2.0의 새로운 것)

PreInit 이벤트는 개발자가 액세스할 수 있는 수명 주기의 초기 단계입니다. 이 이벤트가 추가되면 2.0 테마, 마스터 페이지, ASP.NET 2.0 프로필에 대한 액세스 속성 등을 프로그래밍 방식으로 변경할 수 ASP.NET. 포스트백 상태에 있는 경우 Viewstate가 수명 주기의 이 시점에서 컨트롤에 아직 적용되지 않았다는 것을 깨닫는 것이 중요합니다. 따라서 이 단계에서 개발자가 컨트롤의 속성을 변경하는 경우 페이지 수명 주기의 나중에 덮어쓸 수 있습니다.

## <a name="init"></a>Init

Init 이벤트는 ASP.NET 1.x에서 변경되지 않았습니다. 페이지에서 컨트롤의 속성을 읽거나 초기화하려는 위치입니다. 이 단계에서는 마스터 페이지, 테마 등이 이미 페이지에 적용됩니다.

## <a name="initcomplete-new-in-20"></a>InitComplete(2.0의 새로운 것)

InitComplete 이벤트는 페이지 초기화 단계의 끝에서 호출됩니다. 수명 주기의 이 시점에서 페이지의 컨트롤에 액세스할 수 있지만 해당 상태는 아직 채워지지 않았습니다.

## <a name="preload-new-in-20"></a>사전 로드(2.0의 새로운 것)

이 이벤트는 모든 포스트백 데이터가 적용된 후 페이지\_로드 직전에 호출됩니다.

## <a name="load"></a>로드

로드 이벤트는 ASP.NET 1.x에서 변경되지 않았습니다.

## <a name="loadcomplete-new-in-20"></a>로드완료(2.0의 새로운 것)

LoadComplete 이벤트는 페이지 로드 단계의 마지막 이벤트입니다. 이 단계에서는 모든 포스트백 및 뷰상태 데이터가 페이지에 적용되었습니다.

## <a name="prerender"></a>Prerender

페이지에 동적으로 추가된 컨트롤에 대해 viewstate를 적절하게 유지 관리하려면 PreRender 이벤트가 마지막으로 추가될 수 있습니다.

## <a name="prerendercomplete-new-in-20"></a>프리렌더완료(2.0의 새로운 것)

PreRenderComplete 단계에서 모든 컨트롤이 페이지에 추가되고 페이지를 렌더링할 준비가 되었습니다. PreRenderComplete 이벤트는 페이지 뷰상태가 저장되기 전에 발생한 마지막 이벤트입니다.

## <a name="savestatecomplete-new-in-20"></a>저장 상태완료(2.0의 새로운 것)

SaveStateComplete 이벤트는 모든 페이지 뷰상태 및 제어 상태가 저장된 직후에 호출됩니다. 이 이벤트는 페이지가 실제로 브라우저에 렌더링되기 전의 마지막 이벤트입니다.

## <a name="render"></a>렌더링

렌더링 메서드는 1.x ASP.NET 이후로 변경되지 않았습니다. HtmlTextWriter가 초기화되고 페이지가 브라우저에 렌더링되는 위치입니다.

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0의 크로스 페이지 포스트백

ASP.NET 1.x에서는 포스트백이 같은 페이지에 게시해야 했습니다. 교차 페이지 포스트백은 허용되지 않았습니다. ASP.NET 2.0은 IButtonControl 인터페이스를 통해 다른 페이지에 다시 게시할 수 있는 기능을 추가합니다. 타사 사용자 지정 컨트롤 외에 새로운 IButtonControl 인터페이스(단추, LinkButton 및 ImageButton)를 구현하는 모든 컨트롤은 PostBackUrl 특성을 사용하여 이 새로운 기능을 활용할 수 있습니다. 다음 코드는 두 번째 페이지로 다시 게시하는 Button 컨트롤을 보여 주며, 이 컨트롤은 두 번째 페이지로 다시 게시됩니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

페이지가 다시 게시되면 포스트백을 시작하는 페이지는 두 번째 페이지의 PreviousPage 속성을 통해 액세스할 수 있습니다. 이 기능은 컨트롤이 다른\_페이지로 다시 게시할 때 ASP.NET 2.0이 페이지에 렌더링되는 새로운 WebForm DoPostBackWithOptions 클라이언트 쪽 기능을 통해 구현됩니다. 이 자바 스크립트 함수는 클라이언트에 스크립트를 내보하는 새로운 WebResource.axd 처리기에서 제공됩니다.

아래 동영상은 교차 페이지 포스트백의 연습입니다.

![](the-asp-net-2-0-page-model/_static/image2.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>교차 페이지 포스트백에 대한 자세한 내용

### <a name="viewstate"></a>Viewstate

교차 페이지 포스트백 시나리오의 첫 번째 페이지에서 뷰 상태에 어떤 일이 발생하는지 이미 자문해 보았을 수 있습니다. 결국 IPostBackDataHandler를 구현하지 않는 모든 컨트롤은 viewstate를 통해 해당 상태를 유지하므로 교차 페이지 포스트백의 두 번째 페이지에서 해당 컨트롤의 속성에 액세스하려면 페이지의 뷰상태에 대한 액세스 권한이 있어야 합니다. ASP.NET 2.0은 이전 PAGE라는 \_ \_두 번째 페이지에서 새 숨겨진 필드를 사용하여 이 시나리오를 처리합니다. 이전 \_ \_페이지 양식 필드에는 첫 번째 페이지의 뷰상태가 포함되어 있으므로 두 번째 페이지의 모든 컨트롤의 속성에 액세스할 수 있습니다.

### <a name="circumventing-findcontrol"></a>찾기 제어 우회

교차 페이지 포스트백의 비디오 연습에서 FindControl 메서드를 사용하여 첫 페이지의 TextBox 컨트롤에 대한 참조를 얻었습니다. 이 메서드는 이러한 용도로 는 잘 작동하지만 FindControl은 비용이 많이 들며 추가 코드를 작성해야 합니다. 다행히 ASP.NET 2.0은 많은 시나리오에서 작동하는 이 목적을 위해 FindControl에 대한 대안을 제공합니다. 이전 PageType 지시문을 사용하면 TypeName 또는 VirtualPath 특성을 사용하여 이전 페이지에 대한 강력한 형식의 참조를 가질 수 있습니다. TypeName 특성을 사용하면 이전 페이지의 형식을 지정할 수 있으며 VirtualPath 특성을 사용하면 가상 경로를 사용하여 이전 페이지를 참조할 수 있습니다. 이전 PageType 지시문을 설정한 후 공용 속성을 사용하여 액세스를 허용하려는 컨트롤 등을 노출해야 합니다.

## <a name="lab-1-cross-page-postback"></a>랩 1 크로스 페이지 포스트백

이 실습에서는 ASP.NET 2.0의 새 교차 페이지 포스트백 기능을 사용하는 응용 프로그램을 만듭니다.

1. Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.
2. page2.aspx라는 새 웹 양식을 추가합니다.
3. 디자인 뷰에서 Default.aspx를 열고 단추 컨트롤과 텍스트 상자 컨트롤을 추가합니다. 

    1. 단추 컨트롤에 **SubmitButton의** ID를 지정하고 TextBox에서 **사용자 이름의**ID를 제어합니다.
    2. 단추의 PostBackUrl 속성을 page2.aspx로 설정합니다.
4. 소스 보기에서 페이지2.aspx를 엽니다.
5. 아래와 같이 @ 이전 페이지 유형 지시문을 추가하십시오.
6. page2.aspx의\_코드 숨결의 페이지 로드에 다음 코드를 추가합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 빌드 메뉴에서 빌드를 클릭하여 프로젝트를 빌드합니다.
8. Default.aspx에 대한 코드 숨결에 다음 코드를 추가합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. page2.aspx의 페이지\_로드를 다음과 같이 변경합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 프로젝트를 빌드합니다.
11. 프로젝트를 실행합니다.
12. TextBox에 이름을 입력하고 버튼을 클릭합니다.
13. 결과는 무엇입니까?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0의 비동기 페이지

ASP.NET 많은 경합 문제는 외부 호출(예: 웹 서비스 또는 데이터베이스 호출), 파일 IO 대기 시간 등의 대기 시간으로 인해 발생합니다. ASP.NET 응용 프로그램에 대해 요청이 이루어지면 ASP.NET 해당 작업자 스레드 중 하나를 사용하여 해당 요청을 서비스합니다. 해당 요청은 요청이 완료되고 응답이 전송될 때까지 해당 스레드를 소유합니다. ASP.NET 2.0은 페이지를 비동기적으로 실행하는 기능을 추가하여 이러한 유형의 문제와 함께 대기 시간 문제를 해결하려고 합니다. 즉, 작업자 스레드는 요청을 시작한 다음 다른 스레드에 추가 실행을 전달하여 사용 가능한 스레드 풀로 빠르게 돌아갈 수 있습니다. 파일 IO, 데이터베이스 호출 등이 완료되면 스레드 풀에서 새 스레드를 가져와 요청을 완료합니다.

페이지를 비동기적으로 실행하게 만드는 첫 번째 단계는 다음과 같이 페이지 지시문의 **Async** 특성을 설정하는 것입니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

이 특성은 ASP.NET 페이지에 대한 IHttpAsyncHandler를 구현하도록 지시합니다.

다음 단계는 PreRender 이전 페이지의 수명 주기의 한 지점에서 AddOnPreRenderCompleteAsync 메서드를 호출하는 것입니다. 이 메서드는 일반적으로 페이지\_로드에서 호출 됩니다. AddOnPreRenderCompleteAsync 메서드는 두 개의 매개 변수를 사용합니다. 시작 이벤트 처리기 및 끝 이벤트 처리기. BeginEventHandler는 IAsyncResult를 반환한 다음 EndEventHandler에 매개 변수로 전달됩니다.

아래 비디오는 비동기 페이지 요청의 연습입니다.

![](the-asp-net-2-0-page-model/_static/image3.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> EndEventHandler가 완료될 때까지 비동기 페이지가 브라우저에 렌더링되지 않습니다. 의심의 여지가 있지만 일부 개발자는 비동기 호출과 유사하다고 생각할 것입니다. 그렇지 않다는 것을 깨닫는 것이 중요합니다. 비동기 요청의 이점은 첫 번째 작업자 스레드를 스레드 풀로 반환하여 새 요청을 서비스할 수 있어 IO 바인딩 등으로 인한 경합이 줄어든다는 점입니다.

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0의 스크립트 콜백

웹 개발자는 항상 콜백과 관련된 깜박임을 방지하는 방법을 모색해 왔으며, ASP.NET 1.x에서 SmartNavigation은 깜박임을 방지하는 가장 일반적인 방법이었지만 SmartNavigation은 클라이언트에서 구현이 복잡하기 때문에 일부 개발자에게 문제를 일으켰습니다. ASP.NET 2.0은 스크립트 콜백으로 이 문제를 해결합니다. 스크립트 콜백은 XMLHttp를 사용하여 JavaScript를 통해 웹 서버에 대한 요청을 합니다. XMLHttp 요청은 브라우저의 DOM을 통해 조작할 수 있는 XML 데이터를 반환합니다. XMLHttp 코드는 새 WebResource.axd 처리기에 의해 사용자에게 숨김이 있습니다.

ASP.NET 2.0에서 스크립트 콜백을 구성하는 데 필요한 몇 가지 단계가 있습니다.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>1단계 : ICallbackEventHandler 인터페이스 구현

ASP.NET 페이지를 스크립트 콜백에 참여하는 것으로 인식하려면 ICallbackEventHandler 인터페이스를 구현해야 합니다. 다음과 같이 코드 숨결 파일에서 이 작업을 수행할 수 있습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

@Implements 지시문을 다음과 같이 사용하여 이 작업을 수행할 수도 있습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

일반적으로 인라인 ASP.NET 코드를 사용할 때 @Implements 지시문을 사용합니다.

## <a name="step-2--call-getcallbackeventreference"></a>2단계 : GetCallbackEvent참조 호출

앞에서 설명한 것처럼 XMLHttp 호출은 WebResource.axd 처리기에 캡슐화됩니다. 페이지가 렌더링되면 ASP.NET WebResource.axd에서\_제공하는 클라이언트 스크립트인 WebForm DoCallback에 대한 호출을 추가합니다. WebForm\_DoCallback 함수는 \_ \_콜백에 대한 doPostBack 함수를 대체합니다. doPostBack은 프로그래밍 방식으로 페이지에 양식을 제출한다는 것을 \_ \_기억하십시오. 콜백 시나리오에서는 포스트백을 방지하려고 하므로 \_ \_doPostBack으로는 충분하지 않습니다.

> [!NOTE]
> \_\_doPostBack은 여전히 클라이언트 스크립트 콜백 시나리오의 페이지에 렌더링됩니다. 그러나 콜백에는 사용되지 않습니다.

WebForm\_DoCallback 클라이언트 측 함수에 대한 인수는 일반적으로 페이지\_로드에서 호출되는 서버 측 함수 GetCallbackEventReference를 통해 제공됩니다. GetCallbackEventReference에 대한 일반적인 호출은 다음과 같습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 이 경우 cm는 ClientScriptManager의 인스턴스입니다. ClientScriptManager 클래스는 이 모듈의 후반부에서 다룹니다.

GetCallbackEventReference에는 여러 오버로드된 버전이 있습니다. 이 경우 인수는 다음과 같습니다.

`this`

GetCallbackEventReference가 호출되는 컨트롤에 대한 참조입니다. 이 경우 페이지 자체입니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

클라이언트 측 코드에서 서버 쪽 이벤트로 전달되는 문자열 인수입니다. 이 경우, 임 ddlCompany라는 드롭다운의 값을 전달한다.

`ShowCompanyName`

서버 쪽 콜백 이벤트에서 반환 값(문자열)을 수락하는 클라이언트 측 함수의 이름입니다. 이 함수는 서버 측 콜백이 성공한 경우에만 호출됩니다. 따라서 견고성을 위해 일반적으로 오류 발생 시 실행할 클라이언트 측 함수의 이름을 지정하는 추가 문자열 인수를 사용하는 GetCallbackEventReference의 오버로드된 버전을 사용하는 것이 좋습니다.

`null`

서버에 대한 콜백 전에 시작한 클라이언트 측 함수를 나타내는 문자열입니다. 이 경우 이러한 스크립트가 없으므로 인수는 null입니다.

`true`

콜백을 비동기적으로 수행할지 여부를 지정하는 부울입니다.

클라이언트에서 WebForm\_DoCallback을 호출하면 이러한 인수가 전달됩니다. 따라서 이 페이지가 클라이언트에서 렌더링되면 해당 코드는 다음과 같습니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

클라이언트에서 함수의 시그니처가 약간 다릅니다. 클라이언트 측 함수는 5개의 문자열과 부울을 전달합니다. 위의 예제에서 null인 추가 문자열에는 서버 측 콜백의 오류를 처리하는 클라이언트 측 함수가 포함되어 있습니다.

## <a name="step-3--hook-the-client-side-control-event"></a>3단계 : 클라이언트 측 제어 이벤트 연결

위의 GetCallbackEventReference의 반환 값이 문자열 변수에 할당되었습니다. 이 문자열은 콜백을 시작하는 컨트롤에 대한 클라이언트 쪽 이벤트를 연결하는 데 사용됩니다. 이 예제에서는 콜백이 페이지의 드롭다운에 의해 시작되므로 *OnChange* 이벤트를 연결하려고 합니다.

클라이언트 쪽 이벤트를 연결하려면 다음과 같이 클라이언트 쪽 태그에 처리기를 추가하기만 하면 됩니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

*cbRef는* GetCallbackEventReference에 대한 호출의 반환 값입니다. 여기에는 위에 표시된\_WebForm DoCallback에 대한 호출이 포함되어 있습니다.

## <a name="step-4--register-the-client-side-script"></a>4단계 : 클라이언트 측 스크립트 등록

GetCallbackEventReference 호출은 서버 측 콜백이 성공할 때 **ShowCompanyName이라는** 클라이언트 측 스크립트가 실행되도록 지정했습니다. 해당 스크립트는 ClientScriptManager 인스턴스를 사용 하 여 페이지에 추가 해야 합니다. 클라이언트스크립트관리자 클래스는 이 모듈의 후반부에서 설명합니다. 다음과 같이 합니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>5 단계 : ICallbackEventHandler 인터페이스의 메서드를 호출합니다.

ICallbackEventHandler코드에서 구현해야 하는 두 가지 방법이 포함되어 있습니다. 그들은 **레이즈콜백 이벤트** 및 **겟콜백 이벤트입니다.**

**RaiseCallbackEvent** 인수로 문자열을 소요 하 고 아무것도 반환 하지 않습니다. 문자열 인수는 클라이언트 측 호출에서 WebForm\_DoCallback으로 전달됩니다. 이 경우 해당 값은 ddlCompany라는 드롭다운의 *값* 특성입니다. 서버 쪽 코드는 RaiseCallbackEvent 메서드에 배치해야 합니다. 예를 들어 콜백이 외부 리소스에 대해 WebRequest를 만드는 경우 해당 코드는 RaiseCallbackEvent에 배치되어야 합니다.

**GetCallbackEvent** 클라이언트에 콜백의 반환을 처리 하는 담당 합니다. 인수를 수행하지 않고 문자열을 반환합니다. 반환하는 문자열은 클라이언트 측 함수에 인수로 전달됩니다(이 경우 *ShowCompanyName*.

위의 단계를 완료하면 ASP.NET 2.0에서 스크립트 콜백을 수행할 준비가 된 것입니다.

![](the-asp-net-2-0-page-model/_static/image4.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET 스크립트 콜백은 XMLHttp 호출을 지원하는 모든 브라우저에서 지원됩니다. 여기에는 현재 사용 되는 모든 최신 브라우저가 포함 됩니다. Internet Explorer는 XMLHttp ActiveX 개체를 사용하지만 다른 최신 브라우저(예정된 IE 7 포함)는 본질적인 XMLHttp 개체를 사용합니다. 브라우저가 콜백을 지원하는지 프로그래밍 방식으로 확인하려면 **Request.Browser.SupportCallback** 속성을 사용할 수 있습니다. 요청 클라이언트가 스크립트 콜백을 지원하는 경우 이 속성은 **true를** 반환합니다.

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2.0에서 클라이언트 스크립트로 작업

ASP.NET 2.0의 클라이언트 스크립트는 ClientScriptManager 클래스를 사용하여 관리됩니다. ClientScriptManager 클래스는 형식과 이름을 사용하여 클라이언트 스크립트를 추적합니다. 이렇게 하면 동일한 스크립트가 프로그래밍 방식으로 페이지에 두 번 이상 삽입되지 않습니다.

> [!NOTE]
> 스크립트가 페이지에 성공적으로 등록된 후 동일한 스크립트를 등록하려고 하면 스크립트가 두 번째로 등록되지 않습니다. 중복 스크립트가 추가되지 않으며 예외가 발생하지 않습니다. 불필요한 계산을 방지하기 위해 스크립트가 이미 등록되어 있는지 확인하는 데 사용할 수 있으므로 두 번 이상 등록하지 않도록 할 수 있습니다.

ClientScriptManager의 메서드는 모든 현재 ASP.NET 개발자에게 익숙해야 합니다.

## <a name="registerclientscriptblock"></a>레지스터클라이언트스크립트블록

이 메서드는 렌더링된 페이지의 맨 위에 스크립트를 추가합니다. 이 기능은 클라이언트에서 명시적으로 호출되는 함수를 추가하는 데 유용합니다.

이 메서드에는 두 가지 오버로드된 버전이 있습니다. 네 개의 인수 중 세 가지가 일반적입니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

`type (string)`

***형식*** 인수는 스크립트에 대한 형식을 식별합니다. 일반적으로 페이지의 유형(이 형식)을 사용하는 것이 좋습니다. 형식에 대한 GetType())입니다.

`key (string)`

***키*** 인수는 스크립트에 대한 사용자 정의 키입니다. 각 스크립트에 대해 고유해야 합니다. 동일한 키와 이미 추가된 스크립트 유형이 있는 스크립트를 추가하려고 하면 추가되지 않습니다.

`script (string)`

***스크립트*** 인수는 추가할 실제 스크립트를 포함하는 문자열입니다. StringBuilder를 사용하여 스크립트를 만든 다음 StringBuilder의 ToString() 메서드를 사용하여 ***스크립트*** 인수를 할당하는 것이 좋습니다.

세 개의 인수만 사용하는 오버로드된 RegisterClientScriptBlock을 사용하는 경우&lt;스크립트&gt; &lt;요소에&gt;스크립트 요소(스크립트 및 /script)를 포함해야 합니다.

네 번째 인수를 사용하는 RegisterClientScriptBlock의 오버로드를 사용하도록 선택할 수 있습니다. 네 번째 인수는 ASP.NET 스크립트 요소를 추가해야 하는지 여부를 지정하는 부울입니다. 이 인수가 **true이면**스크립트에 스크립트 요소를 명시적으로 포함해서는 안 됩니다.

IsClientScriptBlock등록 메서드를 사용하여 스크립트가 이미 등록되었는지 확인합니다. 이렇게 하면 이미 등록된 스크립트를 다시 등록하려는 시도를 피할 수 있습니다.

### <a name="registerclientscriptinclude-new-in-20"></a>레지스터클라이언트스크립트포함(2.0의 새로운 것)

RegisterClientScriptInclude 태그는 외부 스크립트 파일에 연결되는 스크립트 블록을 만듭니다. 두 개의 오버로드가 있습니다. 하나는 키와 URL을 사용합니다. 두 번째 인수는 형식을 지정하는 세 번째 인수를 추가합니다.

예를 들어 다음 코드는 응용 프로그램의 스크립트 폴더 루트에서 jsfunctions.js에 연결하는 스크립트 블록을 생성합니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

이 코드는 렌더링된 페이지에서 다음과 같은 코드를 생성합니다.

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 스크립트 블록은 페이지 하단에 렌더링됩니다.

IsClientScriptInclude등록 된 방법을 사용하여 스크립트가 이미 등록되었는지 확인합니다. 이렇게 하면 스크립트를 다시 등록하려는 시도를 피할 수 있습니다.

## <a name="registerstartupscript"></a>레지스터스타트업 스크립트

RegisterStartupScript 메서드는 RegisterClientScriptBlock 메서드와 동일한 인수를 사용합니다. RegisterStartupScript에 등록된 스크립트는 페이지로드 후하지만 OnLoad 클라이언트 측 이벤트 전에 실행됩니다. 1.X에서 &lt;RegisterStartupScript에 등록된 스크립트는 닫기/양식&gt; 태그 바로 앞에 배치되었으며 RegisterClientScriptBlock에 등록된 &lt;&gt; 스크립트는 개구 양식 태그 바로 다음에 배치되었습니다. ASP.NET 2.0에서는 둘 다 닫기 &lt;/form&gt; 태그 바로 앞에 배치됩니다.

> [!NOTE]
> RegisterStartupScript에 함수를 등록하면 클라이언트 쪽 코드에서 명시적으로 호출할 때까지 해당 함수가 실행되지 않습니다.

IsStartupScript등록 메서드를 사용하여 스크립트가 이미 등록되었는지 확인하고 스크립트를 다시 등록하려는 시도를 방지합니다.

## <a name="other-clientscriptmanager-methods"></a>기타 클라이언트스크립트관리자 방법

다음은 ClientScriptManager 클래스의 다른 유용한 방법 중 일부입니다.

|  <strong>겟콜백이벤트</strong>   |                                                 이 모듈의 이전 스크립트 콜백을 참조하십시오.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>겟포스트백클라이언트하이퍼링크</strong>  |                클라이언트 측 이벤트에서 다시 게시하는 데 사용할 수 있는 JavaScript 참조(자바스크립트:&lt;호출)를&gt;가져옵니다.                 |
|  <strong>겟포스트백이벤트참조</strong>   |                                   클라이언트에서 다시 게시물을 시작하는 데 사용할 수 있는 문자열을 가져옵니다.                                    |
|      <strong>GetWebResourceUrl</strong>       | 어셈블리에 포함된 리소스에 URL을 반환합니다. <strong>RegisterClientScript리소스</strong>와 함께 사용해야 합니다. |
| <strong>레지스터클라이언트스크립트리소스</strong> |     페이지에 웹 리소스를 등록합니다. 이러한 리소스는 어셈블리에 포함되고 새 WebResource.axd 처리기에서 처리합니다.      |
|     <strong>레지스터히든필드</strong>      |                                                 페이지에 숨겨진 양식 필드를 등록합니다.                                                 |
|  <strong>레지스터온제출서</strong>   |                                  HTML 양식이 제출될 때 실행되는 클라이언트 쪽 코드를 등록합니다.                                   |
