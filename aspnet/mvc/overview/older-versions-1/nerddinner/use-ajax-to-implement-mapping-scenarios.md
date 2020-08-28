---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX를 사용 하 여 매핑 시나리오 구현 | Microsoft Docs
author: rick-anderson
description: 11 단계에서는 AJAX 매핑 지원을 사용자의 동료 Ddinner 응용 프로그램에 통합 하 여 dinners을 만들고 편집 하거나 볼 수 있는 사용자가 l ...을 볼 수 있도록 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 03b3a27d4b761d0417160b95cc6f39a345385065
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044326"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX를 사용하여 매핑 시나리오 구현

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 11 단계입니다.
> 
> 11 단계에서는 AJAX 매핑 지원을 동료의 내부 응용 프로그램에 통합 하 여 dinners를 생성, 편집 또는 볼 수 있는 사용자가 dinner of 그래픽의 위치를 볼 수 있도록 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>Nerddinner Step 11: AJAX 맵 통합

이제 AJAX 매핑 지원 기능을 통합 하 여 응용 프로그램을 좀 더 시각적인 방식으로 만들 수 있습니다. 이렇게 하면 dinners를 만들거나 편집 하거나 볼 수 있는 사용자가 dinner a의 위치를 그래픽으로 볼 수 있습니다.

### <a name="creating-a-map-partial-view"></a>지도 부분 보기 만들기

응용 프로그램 내의 여러 위치에서 매핑 기능을 사용할 예정입니다. 코드를 마른 상태로 유지 하기 위해 여러 컨트롤러 작업 및 보기에서 다시 사용할 수 있는 단일 부분 템플릿 내에서 공통 맵 기능을 캡슐화 합니다. 이 부분 보기의 이름을 "\Views\Dinners"로 하 고이를 디렉터리 내에 만듭니다.

\Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가 &gt; 보기 메뉴 명령을 선택 하 여 map. .ascx 부분을 만들 수 있습니다. 뷰 이름을 "Map. .ascx"로 지정 하 고,이를 부분 보기로 확인 하 고, 강력한 형식의 "Dinner" 모델 클래스를 전달 하도록 지정 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

"추가" 단추를 클릭 하면 부분 템플릿이 생성 됩니다. 그런 다음 다음 콘텐츠를 포함 하도록 Map. .ascx 파일을 업데이트 합니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

첫 번째 &lt; 스크립트 &gt; 참조는 Microsoft Virtual 지구 6.2 매핑 라이브러리를 가리킵니다. 두 번째 &lt; 스크립트 &gt; 참조는 일반적인 Javascript 매핑 논리를 캡슐화 하는 즉시 만들 map.js 파일을 가리킵니다. &lt;Div id = "Diap" &gt; 요소는 가상 지구에서 지도를 호스트 하는 데 사용 하는 HTML 컨테이너입니다.

그런 다음 &lt; &gt; 이 뷰와 관련 된 두 가지 JavaScript 함수를 포함 하는 스크립트 블록을 포함 합니다. 첫 번째 함수는 jQuery를 사용 하 여 페이지가 클라이언트 쪽 스크립트를 실행할 준비가 되었을 때 실행 되는 함수를 연결 합니다. Map.js 스크립트 파일 내에서 정의 하는 LoadMap () 도우미 함수를 호출 하 여 가상 지구 지도 컨트롤을 로드 합니다. 두 번째 함수는 위치를 식별 하는 맵에 핀을 추가 하는 콜백 이벤트 처리기입니다.

&lt;클라이언트 쪽 스크립트 블록 내에서 서버 쪽% =% 블록을 사용 하 여 &gt; JavaScript에 매핑할 Dinner a의 위도 및 경도를 포함 하는 방법을 확인 합니다. 이 방법은 클라이언트 쪽 스크립트에서 사용할 수 있는 동적 값을 출력 하는 데 유용 합니다. 값을 검색 하기 위해 별도의 AJAX 호출을 서버에 다시 요청 하지 않고도 더 빠르게 만들 수 있습니다. &lt;% =% &gt; 블록은 뷰가 서버에서 렌더링 될 때 실행 되므로 HTML의 출력이 포함 된 JavaScript 값 (예: var 위도 = 47.64312;)을 사용 하 여 종료 됩니다.

### <a name="creating-a-mapjs-utility-library"></a>Map.js 유틸리티 라이브러리 만들기

이제 맵의 JavaScript 기능을 캡슐화 하는 데 사용할 수 있는 Map.js 파일을 만들고 위의 LoadMap 및 Loadmap 메서드를 구현 합니다. 프로젝트 내의 \Scripts 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 " &gt; 새 항목 추가" 메뉴 명령을 선택한 다음 JScript 항목을 선택 하 고 이름을 "Map.js"로 지정할 수 있습니다.

다음은 지도를 표시 하 고 dinners에 대 한 위치 핀을 추가 하기 위해 가상 지구와 상호 작용 하는 Map.js 파일에 추가할 JavaScript 코드입니다.

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>맵 만들기 및 편집과 맵 통합

이제 기존 만들기 및 편집 시나리오와 맵 지원을 통합 합니다. 좋은 소식은이 방법이 매우 간단 하 고 컨트롤러 코드를 변경 하지 않아도 된다는 것입니다. 만들기 및 편집 뷰는 일반 "' d ' 형식" 부분 보기를 공유 하 여 dinner form UI를 구현 하기 때문에 맵을 한 곳에 추가 하 고 만들기 및 편집 시나리오에서 모두 사용할 수 있습니다.

\Views\Dinners\DinnerForm.ascx 부분 보기를 열고 새 지도 부분을 포함 하도록 업데이트 하기만 하면 됩니다. 다음은 맵이 추가 된 후 업데이트 된 DinnerForm이 표시 되는 모양입니다 (참고: 간단 하 게 하기 위해 아래 코드 조각에서 HTML 폼 요소가 생략 됨).

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

위의 d Innerform 부분에서는 "Getinnerformviewmodel" 형식의 개체를 모델 형식으로 사용 합니다 .이 개체는 Dinner object와 국가의 dropdownlist을 채우기 위한 SelectList를 모두 필요로 하기 때문입니다. 지도 부분에는 모델 형식으로 "Dinner" 형식의 개체가 필요 합니다. 따라서 지도 부분을 렌더링할 때에는 다음의 경우에는

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

부분에 추가 된 JavaScript 함수는 jQuery를 사용 하 여 "흐림" 이벤트를 "주소" HTML 텍스트 상자에 연결 합니다. 사용자가 textbox를 클릭 하거나 탭 할 때 발생 하는 "포커스" 이벤트를 들었습니다. 반대쪽은 사용자가 텍스트 상자를 종료할 때 발생 하는 "흐리게" 이벤트입니다. 위의 이벤트 처리기는이 경우 위도 및 경도 textbox 값을 지운 다음 지도에 새 주소 위치를 그립니다. 그런 다음 map.js 파일 내에서 정의한 콜백 이벤트 처리기는 제공 된 주소에 따라 가상 지구에서 반환 된 값을 사용 하 여 폼의 경도 및 위도 텍스트 상자를 업데이트 합니다.

이제 응용 프로그램을 다시 실행 하 고 "저녁 식사" 탭을 클릭 하면 표준 Dinner form 요소와 함께 표시 되는 기본 지도가 표시 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

주소를 입력 한 다음 tab 키를 누르면 맵은 동적으로 업데이트 되어 위치를 표시 하 고, 이벤트 처리기는 다음 위치 값으로 위도/경도 텍스트 상자를 채웁니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

새 dinner를 저장 하 고 편집을 위해 다시 열면 페이지가 로드 될 때 맵 위치가 표시 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

주소 필드가 변경 될 때마다 지도와 위도/경도 좌표가 업데이트 됩니다.

이제 맵에 Dinner location이 표시 되므로 표시 되는 텍스트 상자에서 위도 및 경도 양식 필드를 숨겨진 요소 (주소가 입력 될 때마다 자동으로 업데이트 하므로)로 변경할 수도 있습니다. 이렇게 하려면 html. TextBox () HTML 도우미를 사용 하 여 html. Hidden () 도우미 메서드를 사용 하는 것으로 전환 합니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

이제는 사용자에 게 친숙 한 형태 이며 원시 위도/경도를 표시 하지 않습니다 (데이터베이스에 각 저녁을 계속 해 서 저장).

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>자세히 보기와 지도 통합

이제 만들기 및 편집 시나리오와 통합 된 맵이 있으므로 세부 정보 시나리오와 통합 하겠습니다. &lt;자세히 보기 내 에서% Html RenderPartial ("map");%를 호출 하기만 하면 됩니다. &gt;

다음은 전체 세부 정보 보기에 대 한 소스 코드 (예: 맵 통합)는 다음과 같습니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

이제 사용자가/Dinners/Details/[id] URL로 이동 하는 경우에는 dinner a에 대 한 세부 정보, 즉, 지도에 있는 저녁의 위치 (위에 있는를 마우스로 가리킨 경우 dinner and 주소의 제목을 표시 함)를 확인 하 고이에 대 한 AJAX 링크를 제공 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>데이터베이스 및 리포지토리에서 위치 검색 구현

AJAX 구현을 완료 하려면 응용 프로그램의 홈 페이지에 지도를 추가 하 여 사용자가 근처에서 dinners를 그래픽으로 검색할 수 있게 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Dinners에 대 한 위치 기반 radius 검색을 효율적으로 수행 하기 위해 데이터베이스 및 데이터 리포지토리 계층 내에서 지원을 구현 하는 것부터 시작 합니다. [Sql 2008의 새로운 지리 공간 기능](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 을 사용 하 여이를 구현 하거나, 다음 문서에서 설명 LINQ to SQL 하는 Gary Dryden에 설명 된 sql 함수 방법을 사용할 수 있습니다. [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

이 기술을 구현 하기 위해 Visual Studio 내에서 "서버 탐색기"을 열고, 공동 작업 Ddinner 데이터베이스를 선택한 다음, 그 아래에 있는 "함수" 하위 노드를 마우스 오른쪽 단추로 클릭 하 고 새 "스칼라 반환 함수"를 만들도록 선택 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

그런 다음, 다음 분산 함수에 붙여넣습니다.

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

그런 다음 "NearestDinners"를 호출 하는 SQL Server에서 새 테이블 반환 함수를 만듭니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

이 "NearestDinners" 테이블 함수는 도우미 함수를 사용 하 여 제공 하는 위도 및 경도의 100 마일 내에 있는 모든 Dinners을 반환 합니다.

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

이 함수를 호출 하려면 먼저 \Ststvstl 디렉터리 내에서 파일을 두 번 클릭 하 여 LINQ to SQL designer를 엽니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

그런 다음 함수 간에 NearestDinners 및 DistanceBetween 함수를 LINQ to SQL 디자이너로 끌어 옵니다. 그러면 LINQ to SQL의이 두 번째 Ddinnerdatacontext 클래스에 메서드로 추가 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

그런 다음 NearestDinner 함수를 사용 하 여 지정 된 위치의 100 마일을 포함 하는 예정 된 Dinners을 반환 하는 "FindByLocation" 쿼리 메서드를

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON 기반 AJAX 검색 동작 메서드 구현

이제 새 FindByLocation () 리포지토리 메서드를 활용 하 여 지도를 채우는 데 사용할 수 있는 Dinner data 목록을 다시 반환 하는 컨트롤러 작업 메서드를 구현 합니다. 이 작업 메서드는 클라이언트에서 JavaScript를 사용 하 여 쉽게 조작할 수 있도록 Dinner data를 JSON (JavaScript Object Notation) 형식으로 다시 반환 합니다.

이를 구현 하기 위해 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가 컨트롤러 메뉴 명령을 선택 하 여 새 "SearchController" 클래스를 만듭니다 &gt; . 그런 다음 아래와 같이 새 SearchController 클래스 내에서 "SearchByLocation" 작업 메서드를 구현 합니다.

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController의 SearchByLocation 동작 메서드는 내부적으로 FindByLocation 메서드를 호출 하 여 인접 한 dinners 목록을 가져옵니다. 그러나 Dinner objects를 클라이언트에 직접 반환 하는 대신 JsonDinner 개체를 반환 합니다. JsonDinner 클래스는 Dinner 속성의 하위 집합을 노출 합니다 (예: 보안을 위해 저녁에 게 RSVP를 제공 하지 않는 사람의 이름을 공개 하지 않음). 또한 저녁에 존재 하지 않는 RSVPCount 속성을 포함 하며, 특정 저녁에 연결 된 RSVP 개체의 수를 계산 하 여 동적으로 계산 합니다.

그런 다음 JSON 기반 통신 형식을 사용 하 여 dinners 시퀀스를 반환 하기 위해 컨트롤러 기본 클래스에서 Json () 도우미 메서드를 사용 합니다. JSON은 간단한 데이터 구조를 나타내는 표준 텍스트 형식입니다. 다음은 동작 메서드에서 반환 되는 경우 두 JsonDinner 개체의 JSON 형식 목록이 어떻게 표시 되는지의 예입니다.

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.txt)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery를 사용 하 여 JSON 기반 AJAX 메서드 호출

이제 NerdDinner 응용 프로그램의 홈 페이지를 업데이트 하 여 SearchController의 SearchByLocation 동작 메서드를 사용할 준비가 되었습니다. 이 작업을 수행 하려면/Views/Home/Index.aspx view 템플릿을 열고 텍스트 상자, 검색 단추, 지도 및 &lt; 이름으로 이름이 지정 된 div 요소를 포함 하도록 업데이트 합니다 &gt; .

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

그런 다음 두 개의 JavaScript 함수를 페이지에 추가할 수 있습니다.

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

첫 번째 JavaScript 함수는 페이지가 처음 로드 될 때 맵을 로드 합니다. 두 번째 JavaScript 함수는 검색 단추에서 JavaScript 클릭 이벤트 처리기를 구성 합니다. 단추를 누르면 Map.js 파일에 추가할 FindDinnersGivenLocation () JavaScript 함수를 호출 합니다.

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

이 FindDinnersGivenLocation () 함수는 map을 호출 합니다. 가상 지구 컨트롤에서 ()를 찾아 입력 한 위치에 가운데 맞춤 합니다. 가상 지구 지도 서비스가 반환 될 때 map입니다. Find () 메서드는 최종 인수로 전달 된 callbackUpdateMapDinners 콜백 메서드를 호출 합니다.

CallbackUpdateMapDinners () 메서드는 실제 작업을 수행 하는 위치입니다. JQuery의 $ post () 도우미 메서드를 사용 하 여 SearchController의 SearchByLocation () 작업 메서드에 대 한 AJAX 호출을 수행 합니다 .이 메서드는 새로 가운데 맞춤 지도의 위도 및 경도를 전달 합니다. 이 클래스는 $. post () 도우미 메서드가 완료 될 때 호출 되는 인라인 함수를 정의 하 고 SearchByLocation () 동작 메서드에서 반환 된 JSON 형식의 dinner results는 "dinners" 라는 변수를 사용 하 여 전달 됩니다. 그런 다음 foreach에서 반환 된 각 dinner a를 수행 하 고 dinner 's 위도 및 경도 및 기타 속성을 사용 하 여 지도에 새 핀을 추가 합니다. 또한 지도의 오른쪽에 있는 dinners의 HTML 목록에 dinner entry를 추가 합니다. 그런 다음 압정 및 HTML 목록 모두에 대해 가리키기 이벤트를 구성 하 여 사용자가 해당 항목을 마우스로 가리킬 때 dinner details에 대 한 세부 정보가 표시 되도록 합니다.

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

이제 응용 프로그램을 실행 하 고 홈 페이지를 방문할 때 지도가 표시 됩니다. 도시 이름을 입력 하면 지도의 앞으로 예정 된 dinners이 표시 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

저녁을 마우스로 가리키면이에 대 한 세부 정보가 표시 됩니다.

HTML 목록에서 거품형 또는 오른쪽에 있는 Dinner title을 클릭 하면 dinner로 이동 하 여 필요에 따라 RSVP로 이동 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>다음 단계

이제 팀의 모든 응용 프로그램 기능을 구현 했습니다. 이제 자동화 된 단위 테스트를 사용 하도록 설정 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](use-ajax-to-deliver-dynamic-updates.md)
> [다음](enable-automated-unit-testing.md)
