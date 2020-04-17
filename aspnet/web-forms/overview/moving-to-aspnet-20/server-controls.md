---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 서버 제어 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 2.0은 여러 가지 방법으로 서버 제어를 향상시킵니다. 이 단원에서는 ASP.NET 2.0 및 Visual Studio 200...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543745"
---
# <a name="server-controls"></a>서버 컨트롤

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 2.0은 여러 가지 방법으로 서버 제어를 향상시킵니다. 이 단원에서는 ASP.NET 2.0 및 Visual Studio 2005가 서버 컨트롤을 다루는 방식에 대한 아키텍처 변경 사항 중 일부를 다룹니다.

ASP.NET 2.0은 여러 가지 방법으로 서버 제어를 향상시킵니다. 이 단원에서는 ASP.NET 2.0 및 Visual Studio 2005가 서버 컨트롤을 다루는 방식에 대한 아키텍처 변경 사항 중 일부를 다룹니다.

## <a name="view-state"></a>상태 보기

ASP.NET 2.0의 뷰 상태의 주요 변화는 크기의 극적인 감소입니다. 캘린더 컨트롤만 있는 페이지를 고려합니다. 다음은 ASP.NET 1.1의 뷰 상태입니다.

[!code-css[Main](server-controls/samples/sample1.css)]

이제 ASP.NET 2.0의 동일한 페이지에 있는 보기 상태입니다.

[!code-css[Main](server-controls/samples/sample2.css)]

이는 상당히 중요한 변화이며 뷰 상태가 전선을 통해 앞뒤로 전달된다는 점을 고려할 때 이러한 변경으로 개발자는 상당한 성능 향상을 가져올 수 있습니다. 뷰 상태의 크기 감소는 주로 내부적으로 처리하는 방식에 기인합니다. 뷰 상태는 Base64 인코딩된 문자열입니다. ASP.NET 2.0의 뷰 상태 변화를 더 잘 이해하려면 위의 예제에서 디코딩된 값을 살펴보겠습니다.

디코딩된 1.1 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample3.css)]

이것은 횡설수설처럼 보일 수 있지만 여기에 패턴이 있습니다. ASP.NET 1.x에서는 단일 문자를 사용하여 문자 형식을 식별하고 &lt; &gt; 문자를 사용하여 제한된 값을 식별했습니다. 위의 뷰 상태 샘플의 "t"는 삼중항을 나타냅니다. 삼중항에는 한 쌍의 ArrayLists가 포함되어 있습니다("l"은 ArrayList를 나타냅니다.) 이러한 ArrayLists 중 하나는 값이 1인 Int32("i")를 포함하고 다른 하나는 다른 삼중항을 포함합니다. 삼중항에는 배열 목록 등이 포함되어 있습니다. 기억해야 할 중요한 점은 쌍을 포함하는 트리플렛을 사용하고, 문자를 통해 데이터 형식을 식별하고, &lt; &gt; 문자와 문자를 구분 기호로 사용한다는 것입니다.

ASP.NET 2.0에서는 디코딩된 뷰 상태가 약간 다르게 보입니다.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

디코딩된 뷰 상태의 모양에 큰 변화가 있습니다. 이 변경에는 몇 가지 아키텍처 기반이 있습니다. ASP.NET 1.x의 보기 상태는 LosFormatter를 사용하여 데이터를 직렬화했습니다. 2.0에서는 새 ObjectStateFormatter 클래스를 사용합니다. 이 클래스는 뷰 상태 및 제어 상태의 직렬화 및 역직렬화를 돕기 위해 특별히 설계되었습니다. (제어 상태는 다음 섹션에서 다룹니다.) 직렬화 및 직렬화가 수행되는 방법을 변경하면 많은 이점이 있습니다. 가장 극적인 것 중 하나는 텍스트 라이터를 사용하는 LosFormatter와 달리 ObjectStateFormatter가 바이너리 라이터를 사용한다는 사실입니다. 이렇게 하면 ASP.NET 2.0을 사용하여 문자열 대신 일련의 바이트를 뷰 상태를 저장할 수 있습니다. 예를 들어 정수입니다. ASP.NET 1.1에서 정수에는 4바이트의 뷰 상태가 필요했습니다. ASP.NET 2.0에서 동일한 정수만 1바이트만 필요합니다. 다른 향상된 기능은 저장되는 뷰 상태의 양을 줄이기 위해 만들어졌습니다. 예를 들어 DateTime 값은 이제 문자열 대신 TickCount를 사용하여 저장됩니다.

이 모든 것이 충분하지 않은 것처럼, 1.x에서 뷰 상태의 가장 큰 소비자 중 하나가 DataGrid 및 유사한 컨트롤이라는 사실에 특별한주의를 기울였습니다. 뷰 상태가 우려되는 DataGrid와 같은 컨트롤의 주요 단점은 종종 많은 양의 반복된 정보가 포함되어 있다는 것입니다. ASP.NET 1.x에서 반복되는 정보가 단순히 반복해서 저장되어 뷰 상태가 비대해졌습니다. ASP.NET 2.0에서는 새 IndexedString 클래스를 사용하여 이러한 데이터를 저장합니다. 문자열이 반복되면 IndexedString에 대한 토큰과 인덱스스트링 개체의 실행 중인 테이블 내에 인덱스를 저장합니다.

## <a name="control-state"></a>제어 상태

개발자가 보기 상태와 함께 가지고 있던 주요 한 가지 는 HTTP 페이로드에 추가 된 크기였습니다. 앞에서 설명한 것처럼 뷰 상태의 가장 큰 소비자 중 하나는 DataGrid 컨트롤입니다. DataGrid에서 생성된 엄청난 양의 뷰 상태를 피하기 위해 많은 개발자는 해당 컨트롤에 대해 보기 상태를 사용하지 않도록 설정합니다. 불행히도, 그 해결책이 항상 좋은 해결책은 아니었습니다. ASP.NET 1.x의 뷰 상태는 컨트롤의 올바른 기능에 필요한 데이터뿐만 아니라 포함되어 있습니다. 또한 컨트롤의 UI 상태에 관한 정보도 포함되어 있습니다. 즉, DataGrid에서 페이지 마스꽝스기를 허용하려면 뷰 상태에 포함된 UI 정보가 모두 필요하지 않더라도 보기 상태를 사용하도록 설정해야 합니다. 그것은 전부 또는 아무것도 시나리오입니다.

ASP.NET 2.0에서 제어 상태는 제어 상태의 도입을 통해 해당 문제를 잘 해결합니다. 컨트롤 상태에는 컨트롤의 적절한 기능에 절대적으로 필요한 데이터가 포함되어 있습니다. 뷰 상태와 달리 제어 상태를 비활성화할 수 없습니다. 따라서 제어 상태에 저장 되는 데이터를 신중 하 게 제어 하는 것이 중요 합니다.

> [!NOTE]
> 제어 상태는 \_ \_VIEWSTATE 숨겨진 양식 필드의 뷰 상태와 함께 유지됩니다.

이 비디오는 보기 상태 및 제어 상태의 연습입니다.

![](server-controls/_static/image1.png)

[전체 화면 비디오 열기](server-controls/_static/state1.wmv)

서버 컨트롤이 읽고 쓰기하여 상태를 제어하려면 세 단계를 수행해야 합니다.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>1단계: RegisterRequiresControlState 메서드를 호출합니다.

RegisterNeedsControlState 메서드는 컨트롤이 컨트롤 상태를 유지해야 ASP.NET 알려줍니다. 등록된 컨트롤인 형식 컨트롤의 인수 가 하나 필요합니다.

등록은 요청부터 요청까지 지속되지 않습니다. 따라서 컨트롤이 제어 상태를 유지하려면 모든 요청에서 이 메서드를 호출해야 합니다. OnInit에서 메서드를 호출하는 것이 좋습니다.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>2단계: SaveControlState 재정의

SaveControlState 메서드는 마지막 포스트 백 이후 컨트롤에 대 한 컨트롤 상태 변경 내용을 저장 합니다. 컨트롤의 상태를 나타내는 개체를 반환합니다.

## <a name="step-3-override-loadcontrolstate"></a>3단계: 로드컨트롤스테이트 재정의

LoadControlState 메서드는 저장된 상태를 컨트롤에 로드합니다. 메서드는 컨트롤에 대 한 저장 된 상태를 보유 하는 형식 Object의 한 인수를 사용 합니다.

## <a name="full-xhtml-compliance"></a>전체 XHTML 규정 준수

모든 웹 개발자는 웹 응용 프로그램에서 표준의 중요성을 알고 있습니다. 표준 기반 개발 환경을 유지하기 위해 ASP.NET 2.0은 완전히 XHTML을 준수합니다. 따라서 모든 태그는 HTML 4.0 이상의 브라우저를 지원하는 브라우저의 XHTML 표준에 따라 렌더링됩니다.

ASP.NET 1.1의 DOCTYPE 정의는 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0에서 기본 DOCTYPE 정의는 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample7.html)]

원하는 경우 구성 파일의 xhtmlConformance 노드를 통해 기본 XHTML 준수를 변경할 수 있습니다. 예를 들어 web.config 파일의 다음 노드는 XHTML 준수를 XHTML 1.0 Strict으로 변경합니다.

[!code-xml[Main](server-controls/samples/sample8.xml)]

원하는 경우 다음과 같이 ASP.NET 1.x에 사용된 레거시 구성을 사용하도록 ASP.NET 구성할 수도 있습니다.

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>어댑터를 사용한 어댑티브 렌더링

ASP.NET 1.x에서 구성 파일에는 &lt;HttpBrowserCapabilities 개체를 채우는 브라우저Caps&gt; 섹션이 포함되어 있습니다. 이 개체를 통해 개발자는 특정 요청을 하는 장치를 결정하고 코드를 적절하게 렌더링할 수 있었습니다. ASP.NET 2.0에서 모델이 개선되었으며 이제 새로운 ControlAdapter 클래스를 사용합니다. ControlAdapter 클래스는 컨트롤의 수명 주기에서 이벤트를 재정의하고 사용자 에이전트의 기능에 따라 컨트롤 렌더링을 제어합니다. 특정 사용자 에이전트의 기능은 c:\windows\microsoft.net framework\v2.0에 저장된 브라우저 정의 파일(.브라우저 파일 확장자를 가진 파일)에 의해 정의됩니다. \* \* \*\CONFIG\브라우저 폴더입니다. \*

> [!NOTE]
> ControlAdapter 클래스는 추상 클래스입니다.

1.x의 &lt;&gt; browserCaps 섹션과 마찬가지로 브라우저 정의 파일은 정규식을 사용하여 요청 브라우저를 식별하기 위해 사용자 에이전트 문자열을 구문 분석합니다. 해당 사용자 에이전트에 대한 특정 기능을 정의합니다. 컨트롤 어댑터는 렌더 메서드를 통해 컨트롤을 렌더링합니다. 따라서 Render 메서드를 재정의하는 경우 기본 클래스에서 Render를 호출해서는 안 됩니다. 이렇게 하면 어댑터에 대해 한 번, 컨트롤 자체에 대해 한 번 두 번 렌더링이 발생할 수 있습니다.

## <a name="developing-a-custom-adapter"></a>사용자 지정 어댑터 개발

ControlAdapter에서 상속하여 사용자 지정 어댑터를 개발할 수 있습니다. 또한 페이지에 어댑터가 필요한 경우 추상 클래스 PageAdapter에서 상속할 수 있습니다. 컨트롤을 사용자 지정 어댑터에 매핑하는 작업은 브라우저 정의 파일의 &lt;controlAdapters&gt; 요소를 통해 수행됩니다. 예를 들어 브라우저 정의 파일에서 다음 XML은 메뉴 컨트롤을 MenuAdapter 클래스에 매핑합니다.

[!code-html[Main](server-controls/samples/sample10.html)]

이 모델을 사용하면 컨트롤 개발자가 특정 장치 나 브라우저를 대상으로 하는 것이 매우 쉬워집니다. 또한 개발자가 모든 장치에서 페이지가 렌더링되는 방식을 완벽하게 제어하는 것도 매우 간단합니다.

## <a name="per-device-rendering"></a>장치별 렌더링

ASP.NET 2.0의 서버 제어 속성은 브라우저별 접두사를 사용하여 장치당 지정할 수 있습니다. 예를 들어 아래 코드는 페이지를 탐색하는 데 사용되는 장치에 따라 레이블의 텍스트를 변경합니다.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

이 레이블이 포함된 페이지를 Internet Explorer에서 탐색하면 레이블에 "Internet Explorer에서 검색중"이라는 텍스트가 표시됩니다. 페이지가 Firefox에서 검색되면 레이블에 "Firefox에서 탐색 중"이라는 텍스트가 표시됩니다. 다른 장치에서 페이지를 탐색하면 "알 수 없는 장치에서 탐색 중"이 표시됩니다. 이 특수 구문을 사용하여 모든 속성을 지정할 수 있습니다.

## <a name="setting-focus"></a>초점 설정

ASP.NET 1.x 개발자는 특정 컨트롤에 초기 포커스를 설정하는 방법에 대해 자주 물었습니다. 예를 들어 로그인 페이지에서 페이지가 처음 로드될 때 사용자 ID 텍스트 상자에서 포커스를 얻도록 하는 것이 유용합니다. ASP.NET 1.x에서는 클라이언트 쪽 스크립트를 작성해야 했습니다. 이러한 스크립트는 사소한 작업이지만 SetFocus 메서드 덕분에 ASP.NET 2.0에서는 더 이상 필요하지 않습니다. SetFocus 메서드는 포커스를 받아야 하는 컨트롤을 나타내는 하나의 인수를 사용 합니다. 이 인수는 컨트롤의 클라이언트 ID가 문자열로 지정되거나 Server 컨트롤을 컨트롤 개체로 이름 지정할 수 있습니다. 예를 들어 페이지가 처음 로드될 때 txtUserID라는 TextBox 컨트롤로 초기 포커스를\_설정하려면 다음 코드를 페이지 로드에 추가합니다.

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-- 또는

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0은 Webresource.axd 처리기(이전에 설명한)를 사용하여 포커스를 설정하는 클라이언트 측 함수를 렌더링합니다. 클라이언트 측 함수의 이름은 다음과\_같이 WebForm 자동 초점입니다.

[!code-html[Main](server-controls/samples/sample14.html)]

또는 컨트롤에 포커스 메서드를 사용하여 초기 포커스를 해당 컨트롤에 설정할 수 있습니다. Focus 메서드는 컨트롤 클래스에서 파생되며 모든 ASP.NET 2.0 컨트롤에서 사용할 수 있습니다. 유효성 검사 오류가 발생할 때 특정 컨트롤에 포커스를 설정할 수도 있습니다. 이는 이후 모듈에서 다룹니다.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0의 새로운 서버 제어

다음은 ASP.NET 2.0의 새로운 서버 컨트롤입니다. 우리는 이후 모듈에서 그들 중 일부에 대한 자세한 내용으로 이동합니다.

## <a name="imagemap-control"></a>이미지맵 제어

ImageMap 컨트롤을 사용하면 게시물을 다시 시작하거나 URL로 이동할 수 있는 이미지에 핫스팟을 추가할 수 있습니다. 사용 가능한 핫스팟에는 세 가지 유형이 있습니다. 서클핫스팟, 직사각형핫스팟 및 다각형 핫스팟. 핫스팟은 Visual Studio의 컬렉션 편집기 또는 프로그래밍 방식으로 코드에 추가됩니다. 이미지에 핫스팟을 그리는 데 사용할 수 있는 사용자 인터페이스가 없습니다. 핫스팟의 좌표와 크기 또는 반지름은 선언적으로 지정해야 합니다. 디자이너의 핫스팟을 시각적으로 표현하지도 않습니다. 핫스팟이 URL로 이동하도록 구성된 경우 URL은 핫스팟의 NavigateUrl 속성을 통해 지정됩니다. 포스트 백 핫스팟의 경우 PostBackValue 속성을 사용하면 서버 쪽 코드에서 검색할 수 있는 포스트 백에 문자열을 전달할 수 있습니다.

![비주얼 스튜디오의 핫스팟 컬렉션 편집기](server-controls/_static/image1.jpg)

**그림 1**: 비주얼 스튜디오의 핫스팟 컬렉션 편집기

## <a name="bulletedlist-control"></a>글머리 기호 목록 컨트롤

글머리 기호 List 컨트롤은 데이터 바인딩이 용이할 수 있는 글머리 기호 목록입니다. 이 목록은 BulletStyle 속성을 통해 주문(번호 매기기) 또는 순서없이 정렬할 수 있습니다. 목록의 각 항목은 ListItem 개체로 표시됩니다.

![비주얼 스튜디오에서 글머리 기호 목록 컨트롤](server-controls/_static/image1.gif)

**그림 2**: 비주얼 스튜디오에서 글머리 기호 목록 제어

## <a name="hiddenfield-control"></a>숨겨진 필드 제어

HiddenField 컨트롤은 서버에 숨겨진 양식 필드를 페이지에 추가하며, 이 필드는 서버 쪽 코드에서 사용할 수 있습니다. 숨겨진 폼 필드의 값은 일반적으로 포스트 백 간에 변경되지 않은 상태로 유지될 것으로 예상됩니다. 그러나 악의적인 사용자가 다시 게시하기 전에 값을 변경할 수 있습니다. 이 경우 HiddenField 컨트롤은 ValueChanged 이벤트를 발생시게 됩니다. HiddenField 컨트롤에 중요한 정보가 있고 변경되지 않은 상태로 유지하려면 코드에서 ValueChanged 이벤트를 처리해야 합니다.

## <a name="fileupload-control"></a>파일 업로드 컨트롤

ASP.NET 2.0의 FileUpload 컨트롤을 사용하면 ASP.NET 페이지를 통해 웹 서버에 파일을 업로드할 수 있습니다. 이 컨트롤은 몇 가지 예외가 있는 ASP.NET 1.x HtmlInputFile 클래스와 매우 유사합니다. ASP.NET 1.x에서는 올바른 파일이 있는지 확인하려면 PostedFile 속성을 null로 확인하는 것이 좋습니다. ASP.NET 2.0의 FileUpload 컨트롤은 동일한 용도로 사용할 수 있는 새로운 HasFile 속성을 추가하며 좀 더 효율적입니다.

PostedFile 파일 속성은 HttpPostedFile 개체에 액세스할 수 있지만 HttpPostedFile의 일부 기능은 이제 FileUpload 컨트롤에서 본질적으로 사용할 수 있습니다. 예를 들어 업로드된 파일을 1.x ASP.NET 저장하려면 HttpPostedFile 개체에서 SaveAs 메서드를 호출합니다. ASP.NET 2.0에서 FileUpload 컨트롤을 사용 하 여 FileUpload 컨트롤 자체에 SaveAs 메서드를 호출 합니다.

2.0 동작의 또 다른 중요한 변경 사항은 업로드된 전체 파일을 저장하기 전에 더 이상 메모리에 로드할 필요가 없다는 것입니다. 1.x에서는 업로드된 모든 파일이 디스크에 기록되기 전에 완전히 메모리에 저장됩니다. 이 아키텍처는 대용량 파일의 업로드를 방지합니다.

ASP.NET 2.0에서 httpRuntime 요소의 requestLengthDiskThreshold 특성을 사용하면 디스크에 기록되기 전에 메모리의 버퍼에 보유되는 킬로바이트 수를 구성할 수 있습니다.

**중요**: MSDN 문서(및 다른 문서)는 이 값이 KB가 아닌 바이트이고 기본값은 256임을 지정합니다. 값은 실제로 Kilobytes에 지정되며 기본값은 80입니다. 기본값을 80K로 설정하면 버퍼가 큰 개체 힙에서 끝나지 않도록 합니다.

## <a name="wizard-control"></a>마법사 제어

패널을 사용하거나 페이지로 전송하여 일련의 "페이지"에서 정보를 수집하려고 시도하는 데 어려움을 겪고있는 ASP.NET 개발자를 만나는 것은 매우 일반적입니다. 종종, 노력은 좌절 하나이며 시간이 많이 걸립니다. 새로운 마법사 컨트롤은 사용자가 잘 알고 있는 마법사 인터페이스에서 선형 및 비선형 단계를 허용하여 문제를 해결합니다. 마법사 컨트롤은 일련의 단계로 입력 양식을 제공합니다. 각 단계는 컨트롤의 StepType 속성에 의해 지정된 특정 형식입니다. 사용 가능한 단계 유형은 다음과 같습니다.

| **스텝 유형** | **설명** |
| --- | --- |
| 자동 | 마법사는 단계 계층 구조 내의 위치에 따라 단계 유형을 자동으로 결정합니다. |
| 시작 | 첫 번째 단계는 종종 소개 문을 제시하는 데 사용됩니다. |
| 단계 | 정상적인 단계입니다. |
| Finish | 마지막 단계는 일반적으로 마법사를 완료하는 단추를 표시하는 데 사용됩니다. |
| 완료 | 성공 또는 실패를 알리는 메시지를 제공합니다. |

> [!NOTE]
> 마법사 컨트롤은 ASP.NET 제어 상태를 사용하여 상태를 추적합니다. 따라서 EnableViewState 속성은 손상 없이 false로 설정할 수 있습니다.

이 비디오는 마법사 컨트롤의 연습입니다.

![](server-controls/_static/image2.png)

[전체 화면 비디오 열기](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>지역화 제어

지역화 컨트롤은 리터럴 컨트롤과 유사합니다. 그러나 지역화 컨트롤에는 추가되는 태그가 렌더링되는 방법을 제어하는 **Mode** 속성이 있습니다. Mode 속성은 다음 값을 지원합니다.

| **모드** | **설명** |
| --- | --- |
| 변환 | 마크업은 요청을 하는 브라우저의 프로토콜에 따라 변환됩니다. |
| 통과 | 태그가 있는 것처럼 렌더링됩니다. |
| 인코딩 | 컨트롤에 추가된 태그는 HtmlEncode를 사용하여 인코딩됩니다. |

## <a name="multiview-and-view-controls"></a>멀티뷰 및 뷰 컨트롤

MultiView 컨트롤은 View 컨트롤에 대한 컨테이너 역할을 하며 View 컨트롤은 다른 컨트롤에 대한 컨테이너(예: 패널 컨트롤)의 역할을 합니다. MultiView 컨트롤의 각 보기는 단일 보기 컨트롤로 표시됩니다. 다중 보기의 첫 번째 뷰 컨트롤은 뷰 0, 두 번째 보기 1 등입니다. 다중 보기 컨트롤의 ActiveViewIndex를 지정하여 뷰를 전환할 수 있습니다.

## <a name="substitution-control"></a>대체 제어

대체 제어는 ASP.NET 캐싱과 함께 사용됩니다. 캐싱을 활용하길 하지만 각 요청에서 업데이트해야 하는 페이지 부분(즉, 캐싱에서 제외되는 페이지의 일부)이 있는 경우 대체 구성 요소는 훌륭한 솔루션을 제공합니다. 컨트롤은 실제로 자체적으로 출력을 렌더링하지 않습니다. 대신 서버 쪽 코드의 메서드에 바인딩됩니다. 페이지가 요청되면 메서드가 호출되고 반환된 태그가 대체 컨트롤 대신 렌더링됩니다.

대체 컨트롤이 바인딩되는 메서드는 **MethodName** 속성을 통해 지정됩니다. 이 메서드는 다음 기준을 충족해야 합니다.

- 정적(VB에서 공유) 메서드여야 합니다.
- HttpContext 형식의 하나의 매개 변수를 허용 합니다.
- 페이지의 컨트롤을 대체해야 하는 태그를 나타내는 문자열을 반환합니다.

대체 컨트롤은 페이지의 다른 컨트롤을 수정할 수 없지만 매개 변수를 통해 현재 HttpContext에 액세스할 수 있습니다.

## <a name="gridview-control"></a>그리드뷰 제어

GridView 컨트롤은 DataGrid 컨트롤을 대체합니다. 이 컨트롤은 이후 모듈에서 자세히 다룹니다.

## <a name="detailsview-control"></a>세부 정보보기 제어

DetailsView 컨트롤을 사용하면 데이터 원본에서 단일 레코드를 표시하고 편집하거나 삭제할 수 있습니다. 이후 모듈에서 자세히 다룹니다.

## <a name="formview-control"></a>양식뷰 제어

FormView 컨트롤은 구성 가능한 인터페이스에서 데이터 원본의 단일 레코드를 표시하는 데 사용됩니다. 이후 모듈에서 자세히 다룹니다.

## <a name="accessdatasource-control"></a>액세스 데이터 소스 제어

AccessDataSource 컨트롤은 Access 데이터베이스를 바인딩하는 데 사용됩니다. 이후 모듈에서 자세히 다룹니다.

## <a name="objectdatasource-control"></a>개체 데이터 소스 제어

ObjectDataSource 컨트롤은 컨트롤이 데이터 원본에 직접 바인딩되는 2계층 모델이 아닌 중간 계층 비즈니스 개체에 데이터 바인딩할 수 있도록 3계층 아키텍처를 지원하는 데 사용됩니다. 이후 단원에서 자세히 설명합니다.

## <a name="xmldatasource-control"></a>XmlData소스 제어

XmlDataSource 컨트롤은 XML 데이터 원본에 데이터 바인딩하는 데 사용됩니다. 이후 모듈에서 자세히 다룹니다.

## <a name="sitemapdatasource-control"></a>사이트맵데이터소스 제어

SiteMapDataSource 컨트롤은 사이트 맵을 기반으로 사이트 탐색 컨트롤에 대한 데이터 바인딩을 제공합니다. 이후 단원에서 자세히 설명합니다.

## <a name="sitemappath-control"></a>사이트맵 경로 제어

SiteMapPath 컨트롤은 일반적으로 이동 경로라고 하는 일련의 탐색 링크를 표시합니다. 이후 모듈에서 자세히 다룹니다.

## <a name="menu-control"></a>Menu 컨트롤

메뉴 컨트롤은 DHTML을 사용하여 동적 메뉴를 표시합니다. 이후 모듈에서 자세히 다룹니다.

## <a name="treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤은 데이터의 계층적 트리 보기를 표시하는 데 사용됩니다. 이후 모듈에서 자세히 다룹니다.

## <a name="login-control"></a>로그인 제어

로그인 컨트롤은 웹 사이트에 로그인하는 메커니즘을 제공합니다. 이후 모듈에서 자세히 다룹니다.

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤을 사용하면 사용자의 로그인 상태에 따라 다른 템플릿을 표시할 수 있습니다. 이후 모듈에서 자세히 다룹니다.

## <a name="passwordrecovery-control"></a>암호 복구 제어

PasswordRecovery 컨트롤은 ASP.NET 응용 프로그램의 사용자가 잊어버린 암호를 검색하는 데 사용됩니다. 이후 모듈에서 자세히 다룹니다.

## <a name="loginstatus"></a>LoginStatus

로그인 상태 컨트롤은 사용자의 로그인 상태를 표시합니다. 이후 모듈에서 자세히 다룹니다.

## <a name="loginname"></a>LoginName

로그인 이름 컨트롤은 ASP.NET 응용 프로그램에 로그인한 후 사용자의 사용자 이름을 표시합니다. 이후 모듈에서 자세히 다룹니다.

## <a name="createuserwizard"></a>사용자 마법사 만들기

CreateUserWizard는 사용자가 ASP.NET 응용 프로그램에서 사용할 수 있도록 ASP.NET 멤버 자격 계정을 만들 수 있는 구성 가능한 마법사입니다. 이후 모듈에서 자세히 다룹니다.

## <a name="changepassword"></a>ChangePassword

ChangePassword 컨트롤을 사용하면 사용자가 ASP.NET 응용 프로그램에 대한 암호를 변경할 수 있습니다. 이후 모듈에서 자세히 다룹니다.

## <a name="various-webparts"></a>다양한 웹 파트

ASP.NET 2.0 은 다양한 웹 부품과 함께 제공됩니다. 이 내용은 이후 모듈에서 자세히 다룹니다.
