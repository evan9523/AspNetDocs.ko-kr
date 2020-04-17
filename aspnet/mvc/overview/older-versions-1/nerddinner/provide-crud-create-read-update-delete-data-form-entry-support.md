---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD 제공(데이터 양식 입력 지원 생성, 읽기, 업데이트, 삭제 | 마이크로 소프트 문서
author: rick-anderson
description: 5단계는 DinnersController 클래스를 편집, 생성 및 삭제에 대한 지원을 활성화하여 더 나아가는 방법을 보여 주며, Dinners를 사용하여 저녁 식사도 생성하고 삭제할 수 있도록 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542627"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD(만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 제공

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 5단계입니다.
> 
> 5단계는 DinnersController 클래스를 편집, 생성 및 삭제에 대한 지원을 활성화하여 더 나아가는 방법을 보여 주며, Dinners를 사용하여 저녁 식사도 생성하고 삭제할 수 있도록 합니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 단계 5: 양식 시나리오 만들기, 업데이트, 삭제

컨트롤러와 뷰를 도입했으며 이를 사용하여 현장에서 Dinners에 대한 목록/세부 정보 환경을 구현하는 방법을 다루었습니다. 우리의 다음 단계는 우리의 DinnersController 클래스를 더 가지고 편집, 생성 및 그것으로 저녁 식사를 삭제에 대한 지원을 가능하게하는 것입니다.

### <a name="urls-handled-by-dinnerscontroller"></a>저녁 식사 컨트롤러에 의해 처리 되는 URL

이전에는 DinnersController에 두 개의 URL에 대한 지원을 구현한 */Dinners/Details/[id]* 작업 *메서드를 추가했습니다.*

| **URL** | **VERB** | **용도** |
| --- | --- | --- |
| */저녁 식사/* | GET | 다가오는 저녁 식사의 HTML 목록을 표시합니다. |
| */저녁 식사/세부 정보/[ID]* | GET | 특정 저녁 식사에 대한 세부 정보를 표시합니다. |

이제 세 개의 추가 URL을 구현하기 위한 작업 *메서드를 추가합니다: /Dinners/편집/[id]*, */Dinners/Create*및 */Dinners/Delete/id.* 이러한 URL을 사용하면 기존 저녁 식사 편집, 새 저녁 식사 만들기 및 저녁 식사 삭제를 지원할 수 있습니다.

이러한 새 URL과의 HTTP GET 및 HTTP POST 동사 상호 작용을 모두 지원합니다. 이러한 URL에 대한 HTTP GET 요청은 데이터의 초기 HTML 보기를 표시합니다("편집"의 경우 Dinner 데이터로 채워진 양식, "만들기"의 경우 빈 양식, "삭제"의 경우 삭제 확인 화면). 이러한 URL에 대한 HTTP POST 요청은 DinnerRepository(그리고 거기에서 데이터베이스까지)에서 Dinner 데이터를 저장/업데이트/삭제합니다.

| **URL** | **VERB** | **용도** |
| --- | --- | --- |
| */저녁 식사/편집/[id]* | GET | Dinner 데이터로 채워진 편집 가능한 HTML 양식을 표시합니다. |
| POST | 특정 Dinner에 대한 양식 변경 내용을 데이터베이스에 저장합니다. |
| */저녁 식사/만들기* | GET | 사용자가 새 Dinners를 정의할 수 있는 빈 HTML 양식을 표시합니다. |
| POST | 새 Dinner를 만들고 데이터베이스에 저장합니다. |
| */저녁 식사/삭제/[id]* | GET | 삭제 확인 화면을 표시합니다. |
| POST | 데이터베이스에서 지정된 저녁 식사를 삭제합니다. |

### <a name="edit-support"></a>지원 편집

먼저 "편집" 시나리오를 구현해 보겠습니다.

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET 편집 작업 방법

먼저 편집 작업 메서드의 HTTP "GET" 동작을 구현합니다. 이 메서드는 */Dinners/편집/[id]* URL이 요청될 때 호출됩니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

위의 코드는 DinnerRepository를 사용하여 Dinner 개체를 검색합니다. 그런 다음 Dinner 개체를 사용하여 뷰 템플릿을 렌더링합니다. *View()* 도우미 메서드에 템플릿 이름을 명시적으로 전달하지 않았으므로 규칙 기반 기본 경로를 사용하여 보기 템플릿을 확인합니다.

이제 이 보기 템플릿을 만들어 보겠습니다. 편집 방법 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 이 작업을 수행합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 해당 모델로 전달하고 "편집" 템플릿을 자동으로 스캐폴드하도록 선택했음을 나타냅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에 새 "Edit.aspx" 보기 템플릿 파일이 추가됩니다. 또한 코드 편집기 내에서 새로운 "Edit.aspx" 보기 템플릿을 엽니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

생성된 기본 "편집" 스캐폴드를 몇 가지 변경하고 편집 보기 템플릿을 업데이트하여 아래 콘텐츠(노출하지 않으려는 속성 중 일부를 제거)를 갖도록 하겠습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

응용 프로그램을 실행하고 *"저녁 식사 / 편집 / 1"URL을* 요청하면 다음 페이지가 표시됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

뷰에서 생성된 HTML 태그는 다음과 같습니다. "저장" &lt;&gt; 입력 유형="제출"/버튼을 눌려있을 때 */Dinners/편집/1* URL에 HTTP POST를 수행하는 &lt;양식&gt; 요소가 있는 표준 HTML입니다. HTML &lt;입력 유형="텍스트"/요소가&gt; 각 편집 가능한 속성에 대해 출력되었습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() 및 Html.TextBox() HTML 도우미 방법

우리의 "편집.aspx" 보기 템플릿은 몇 가지 "Html 도우미" 메서드를 사용 하 여: Html.ValidationSummary (), Html.BeginForm (), Html.TextBox(), 그리고 Html.ValidationMessage(). 이러한 도우미 메서드는 HTML 태그를 생성하는 것 외에도 기본 제공 오류 처리 및 유효성 검사 지원을 제공합니다.

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() 도우미 방법

Html.BeginForm() 도우미 메서드는 태그에서 &lt;HTML&gt; 양식 요소를 출력하는 방법입니다. Edit.aspx 보기 템플릿에서는 이 메서드를 사용할 때 C# "using" 문을 적용하고 있음을 알 수 있습니다. 열린 곱슬 대괄호는 &lt;양식&gt; 내용의 시작을 나타내고 닫는 곱슬 대괄호는 &lt;/form&gt; 요소의 끝을 나타냅니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

또는 이와 같은 시나리오에서 "using" 문 접근 방식이 부자연스럽다면 Html.BeginForm() 및 Html.EndForm(동일한 작업을 수행하는) 조합을 사용할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

매개 변수없이 Html.BeginForm()을 호출하면 현재 요청의 URL에 HTTP-POST를 수행하는 양식 요소가 출력됩니다. 그래서 편집 보기는 * &lt;양식 동작="/Dinners/편집/1" 메서드="post"&gt; 요소를 생성합니다.* 다른 URL에 게시하려는 경우 명시적 매개 변수를 Html.BeginForm()에 전달할 수도 있습니다.

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() 도우미 방법

Edit.aspx 보기는 Html.TextBox() 도우미 메서드를 &lt;사용하여 입력 입력&gt; ="텍스트"/요소를 출력합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

위의 Html.TextBox() 메서드는 &lt;입력 type="text"/요소의&gt; id/name 속성을 모두 출력할 뿐만 아니라 텍스트 상자 값을 채우는 모델 속성을 지정하는 데 사용되는 단일 매개 변수를 사용합니다. 예를 들어 편집 뷰에 전달한 Dinner 개체에는 ".NET Futures"의 "Title" 속성 값이 있으므로 Html.TextBox("제목") 메서드 호출 출력: * &lt;입력 id="Title" name="Title" type="text" 값="net"net&gt;*

또는 첫 번째 Html.TextBox() 매개 변수를 사용하여 요소의 ID/이름을 지정한 다음 값을 명시적으로 전달하여 두 번째 매개 변수로 사용할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

종종 출력되는 값에 대한 사용자 지정 서식을 수행해야 합니다. .NET에 내장된 String.Format() 정적 메서드는 이러한 시나리오에 유용합니다. Edit.aspx 보기 템플릿은 이 것을 사용하여 EventDate 값(DateTime 형식)을 포맷하여 시간 동안 초를 표시하지 않습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html.TextBox()에 대한 세 번째 매개 변수는 선택적으로 추가 HTML 특성을 출력하는 데 사용할 수 있습니다. 아래 코드 조각은 입력 type="text"/요소에 &lt;&gt; 추가 크기="30" 특성 및 클래스="mycssclass" 특성을 렌더링하는 방법을 보여 줍니다. "클래스"를@" character because "사용하여 클래스 특성의 이름을 이스케이프하는 방법은 C#의 예약된 키워드입니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP-POST 편집 작업 방법 구현

이제 편집 작업 메서드의 HTTP-GET 버전이 구현되었습니다. 사용자가 */Dinners/편집/1 URL을* 요청하면 다음과 같은 HTML 페이지가 표시됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"저장" 버튼을 누르면 */Dinners/편집/1* URL에 양식 게시물이 발생 하 &lt;&gt; 고 HTTP POST 동사를 사용 하 여 HTML 입력 양식 값을 제출 합니다. 이제 Dinner 저장을 처리하는 편집 작업 메서드의 HTTP POST 동작을 구현해 보겠습니다.

HTTP POST 시나리오를 처리한다는 것을 나타내는 "AcceptVerbs" 특성이 있는 DinnersController에 오버로드된 "편집" 작업 메서드를 추가하여 시작합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

[AcceptVerbs] 특성이 오버로드된 작업 메서드에 적용되면 ASP.NET MVC는 들어오는 HTTP 동사에 따라 적절한 작업 메서드로 요청을 디스패치하는 요청을 자동으로 처리합니다. HTTP POST */Dinners/편집/[id]* URL에 대한 HTTP POST 요청은 위의 편집 방법으로 이동하지만 다른 모든 HTTP 동사 요청은 */Dinners/편집/[id]* URL로 이동하며, URL은 `[AcceptVerbs]` 특성이 없는 첫 번째 편집 메서드로 이동합니다.

| **측면 주제: HTTP 동사를 통해 차별화하는 이유는 무엇입니까?** |
| --- |
| 단일 URL을 사용하고 HTTP 동사를 통해 동작을 차별화하는 이유는 무엇입니까? 편집 변경 내용을 로드하고 저장하는 데 두 개의 별도 URL만 있는 것은 어떨까요? 예: /Dinners/편집/[id]를 표시하여 초기 양식을 표시하고/Dinners/Save/[id]를 표시하여 양식 게시물을 처리하여 저장합니까? 두 개의 별도 URL을 게시하는 단점은 입력 오류로 인해 HTML 양식을 다시 표시해야하는 경우 최종 사용자가 브라우저의 주소 표시 줄에 /Dinners / Save /2 URL을 표시해야한다는 것입니다 (해당 양식이 게시 된 URL이었기 때문에). 최종 사용자가 이 페이지를 브라우저 즐겨찾기 목록에 다시 표시하거나 URL을 복사/붙여넣은 후 친구에게 이메일을 지정하면 나중에 작동하지 않는 URL이 저장됩니다(해당 URL은 게시물 값에 따라 달라지기 때문에). 단일 URL(예: /Dinners/Edit/[id])을 노출하고 HTTP 동사로 처리를 차별화하면 최종 사용자가 편집 페이지를 즐겨찾기에 표시하거나 URL을 다른 사용자에게 보내는 것이 안전합니다. |

#### <a name="retrieving-form-post-values"></a>양식 게시물 값 검색

HTTP POST "편집" 방법 내에서 게시된 양식 매개 변수에 액세스할 수 있는 다양한 방법이 있습니다. 한 가지 간단한 방법은 Controller 기본 클래스의 Request 속성을 사용하여 양식 컬렉션에 액세스하고 게시된 값을 직접 검색하는 것입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

위의 방법은 약간 상세하지만, 특히 오류 처리 논리를 추가하면 됩니다.

이 시나리오에 대 한 더 나은 방법은 컨트롤러 기본 클래스에 기본 *제공 UpdateModel()* 도우미 메서드를 활용 하는 것입니다. 들어오는 양식 매개 변수를 사용하여 전달하는 개체의 속성 업데이트를 지원합니다. 리플렉션을 사용하여 개체의 속성 이름을 결정한 다음 클라이언트가 제출한 입력 값에 따라 자동으로 변환하고 값을 할당합니다.

UpdateModel() 메서드를 사용하여 이 코드를 사용하여 HTTP-POST 편집 작업을 단순화할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

이제 */Dinners/편집/1 URL을* 방문하여 저녁 식사 의 제목을 변경할 수 있습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"저장" 단추를 클릭하면 편집 작업에 양식 게시를 수행하고 업데이트된 값이 데이터베이스에 유지됩니다. 그런 다음 Dinner의 세부 정보 URL로 리디렉션됩니다(새로 저장된 값이 표시됩니다).

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>편집 오류 처리

현재 HTTP-POST 구현은 오류가 있는 경우를 제외하고 는 정상적으로 작동합니다.

사용자가 양식을 편집하는 실수를 할 때 양식을 수정하도록 안내하는 유익한 오류 메시지와 함께 양식이 다시 표시되는지 확인해야 합니다. 여기에는 최종 사용자가 잘못된 입력(예: 잘못된 날짜 문자열)을 게시하는 경우와 입력 형식이 유효하지만 비즈니스 규칙 위반이 있는 경우가 포함됩니다. 오류가 발생하면 양식은 사용자가 원래 입력한 입력 데이터를 보존하여 변경 내용을 수동으로 다시 채울 필요가 없도록 해야 합니다. 이 프로세스는 양식이 성공적으로 완료될 때까지 필요한 만큼 반복되어야 합니다.

ASP.NET MVC에는 오류 처리 및 양식 재표시를 쉽게 만드는 몇 가지 멋진 기본 제공 기능이 포함되어 있습니다. 이러한 기능을 확인하려면 다음 코드로 편집 작업 메서드를 업데이트해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

위의 코드는 이전 구현과 유사합니다 . UpdateModel()를 호출할 때 예외가 발생하거나 DinnerRepository를 시도하고 저장할 때(저장하려는 Dinner 개체가 모델 내의 규칙 위반으로 인해 유효하지 않은 경우 예외를 발생시) catch 오류 처리 블록이 실행됩니다. 그 안에서 Dinner 개체에 있는 규칙 위반을 반복하고 ModelState 개체에 추가합니다(곧 설명하겠습니다). 그런 다음 뷰를 다시 표시합니다.

이 작업을 보려면 응용 프로그램을 다시 실행하고 Dinner를 편집하고 빈 제목인 "BOGUS"의 EventDate를 가지고 미국 국가 값이 있는 영국 전화 번호를 사용하도록 변경합니다. "저장" 버튼을 누르면 HTTP POST 편집 방법이 Dinner를 저장할 수 없으며(오류가 있기 때문에) 양식을 다시 표시합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

우리의 응용 프로그램은 괜찮은 오류 경험이 있습니다. 잘못된 입력이 있는 텍스트 요소가 빨간색으로 강조 표시되고 유효성 검사 오류 메시지가 최종 사용자에게 표시됩니다. 또한 양식은 사용자가 원래 입력한 입력 데이터를 보존하므로 아무 것도 다시 채울 필요가 없습니다.

어떻게 이런 일이 발생했습니까? 제목, EventDate 및 ContactPhone 텍스트 상자는 빨간색으로 자신을 강조 표시하고 원래 입력한 사용자 값을 출력하는 방법을 알고 있었습니까? 그리고 오류 메시지가 상단의 목록에 어떻게 표시되었습니까? 좋은 소식은 이것이 마술에 의해 발생하지 않았다는 것입니다 - 오히려 입력 유효성 검사 및 오류 처리 시나리오를 쉽게 만드는 기본 제공 ASP.NET MVC 기능 중 일부를 사용했기 때문입니다.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>모델상태 및 유효성 검사 HTML 도우미 방법 이해

컨트롤러 클래스에는 모델 개체가 뷰에 전달되는 경우 오류가 있음을 나타내는 방법을 제공하는 "ModelState" 속성 컬렉션이 있습니다. ModelState 컬렉션 내의 오류 항목은 문제가 있는 모델 속성의 이름을 식별하고(예: "제목", "EventDate" 또는 "ContactPhone") 인간 친화적인 오류 메시지를 지정할 수 있습니다(예: "제목이 필요합니다.").

*UpdateModel()* 도우미 메서드는 모델 개체의 속성에 양식 값을 할당하는 동안 오류가 발생하면 ModelState 컬렉션을 자동으로 채웁니다. 예를 들어 Dinner 개체의 EventDate 속성은 DateTime 형식입니다. UpdateModel() 메서드가 위의 시나리오에서 문자열 값 "BOGUS"를 할당할 수 없는 경우 UpdateModel() 메서드는 해당 속성에서 할당 오류가 발생했음을 나타내는 ModelState 컬렉션에 항목을 추가했습니다.

개발자는 Dinner 개체의 활성 규칙 위반을 기반으로 하는 항목으로 ModelState 컬렉션을 채우는 "catch" 오류 처리 블록 내에서 아래에서 수행하는 것처럼 ModelState 컬렉션에 오류 항목을 명시적으로 추가하는 코드를 작성할 수도 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>모델스테이트와 Html 도우미 통합

HTML 도우미 메서드(예: Html.TextBox() - 출력을 렌더링할 때 ModelState 컬렉션을 선택합니다. 항목에 대한 오류가 있으면 사용자 입력 값과 CSS 오류 클래스를 렌더링합니다.

예를 들어 "편집" 보기에서 Html.TextBox() 도우미 메서드를 사용하여 Dinner 개체의 EventDate를 렌더링합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

오류 시나리오에서 뷰가 렌더링되었을 때 Html.TextBox() 메서드는 ModelState 컬렉션을 선택하여 Dinner 개체의 "EventDate" 속성과 관련된 오류가 있는지 확인했습니다. 오류가 있다고 판단되면 제출된 사용자 입력("BOGUS")을 값으로 렌더링하고 &lt;생성된 입력 유형="textbox"/&gt; 태그에 css 오류 클래스를 추가했습니다.

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

원하는 모양으로 css 오류 클래스의 모양을 사용자 지정할 수 있습니다. 기본 CSS 오류 클래스인 "입력 유효성 검사 오류"는 *\content\site.css* 스타일시트에 정의되어 있으며 다음과 같습니다.

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

이 CSS 규칙은 잘못된 입력 요소를 다음과 같이 강조 표시하게 하는 것입니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.유효성 검사메시지() 도우미 방법

Html.ValidationMessage() 도우미 메서드를 사용하여 특정 모델 속성과 연결된 ModelState 오류 메시지를 출력할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

위의 코드 출력: * &lt;span class="필드 유효성&gt; 검사-오류" 값 'BOGUS' 값이 잘못되었습니다/범위&lt;&gt;*

Html.ValidationMessage() 도우미 메서드는 개발자가 표시되는 오류 텍스트 메시지를 재정의할 수 있는 두 번째 매개 변수도 지원합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

위의 코드 출력: * &lt;&gt;\*&lt;EventDate&gt; * 속성에 대 한 오류가 있을 때 기본 오류 텍스트 대신 "필드 유효성 검사 오류" /span 클래스=

##### <a name="htmlvalidationsummary-helper-method"></a>Html.유효성 검사요약() 도우미 방법

Html.ValidationSummary() 도우미 메서드는 ModelState 컬렉션의 모든 자세한 오류 &lt;메시지의 ul&gt;&lt;li/ul&gt;&lt;&gt; 목록과 함께 요약 오류 메시지를 렌더링하는 데 사용할 수 있습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.ValidationSummary() 도우미 메서드는 선택적 문자열 매개 변수를 사용 하며, 자세한 오류 목록 위에 표시 하는 요약 오류 메시지를 정의 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

선택적으로 CSS를 사용하여 오류 목록의 모양을 재정의할 수 있습니다.

#### <a name="using-a-addruleviolations-helper-method"></a>추가 규칙 위반 도우미 방법 사용

우리의 초기 HTTP-POST 편집 구현 은 Dinner 개체의 규칙 위반을 반복하고 컨트롤러의 ModelState 컬렉션에 추가하기 위해 catch 블록 내의 foreach 문을 사용했습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

NerdDinner 프로젝트에 "ControllerHelpers" 클래스를 추가하여 이 코드를 좀 더 깨끗하게 만들고 mVC ModelStateDictionary 클래스에 도우미 메서드를 추가하는 "AddRule위반" 확장 메서드를 구현할 수 ASP.NET. 이 확장 메서드는 ModelStateDictionary를 규칙 위반 오류 목록으로 채우는 데 필요한 논리를 캡슐화할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

그런 다음 HTTP-POST 편집 작업 메서드를 업데이트하여 이 확장 메서드를 사용하여 Dinner 규칙 위반으로 ModelState 컬렉션을 채울 수 있습니다.

#### <a name="complete-edit-action-method-implementations"></a>작업 방법 구현 완료

아래 코드는 편집 시나리오에 필요한 모든 컨트롤러 논리를 구현합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

편집 구현의 좋은 점은 컨트롤러 클래스나 View 템플릿이 Dinner 모델에서 적용되는 특정 유효성 검사 또는 비즈니스 규칙에 대해 아무 것도 알 필요가 없다는 것입니다. 나중에 모델에 규칙을 추가할 수 있으며 지원하기 위해 컨트롤러 나 뷰를 코드를 변경할 필요가 없습니다. 이를 통해 최소한의 코드 변경으로 향후 응용 프로그램 요구 사항을 쉽게 발전할 수 있습니다.

### <a name="create-support"></a>지원 만들기

DinnersController 클래스의 "편집" 동작 구현을 완료했습니다. 이제 사용자가 새 Dinners를 추가할 수 있는 "만들기" 지원을 구현해 보겠습니다.

#### <a name="the-http-get-create-action-method"></a>HTTP-GET 만들기 작업 방법

먼저 만들기 작업 메서드의 HTTP "GET" 동작을 구현합니다. 이 메서드는 *사용자가 /Dinners/CREATE URL을* 방문할 때 호출됩니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

위의 코드는 새 Dinner 개체를 만들고 해당 EventDate 속성을 나중에 1주일로 지정합니다. 그런 다음 새 Dinner 개체를 기반으로 하는 뷰를 렌더링합니다. *View()* 도우미 메서드에 이름을 명시적으로 전달하지 않았으므로 규칙 기반 기본 경로를 사용하여 보기 템플릿을 확인합니다.

이제 이 보기 템플릿을 만들어 보겠습니다. 작업 만들기 메서드 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 이 작업을 수행할 수 있습니다. "보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 전달하고 "만들기" 템플릿을 자동으로 스캐폴드하도록 선택합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"추가" 단추를 클릭하면 Visual Studio에서 새 스캐폴드 기반 "Create.aspx" 보기를 "\View\Dinners" 디렉토리에 저장하고 IDE 내에서 엽니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

우리를 위해 생성 된 기본 "만들기"스캐폴드 파일을 몇 가지 변경하고 아래와 같이 수정해 보겠습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

이제 응용 프로그램을 실행하고 브라우저 내에서 *"/Dinners/Create"* URL에 액세스하면 작업 구현 만들기에서 아래와 같은 UI를 렌더링합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP-POST 만들기 작업 메서드 구현

우리는 우리의 만들기 작업 메서드의 HTTP-GET 버전을 구현 했습니다. 사용자가 "저장" 단추를 클릭하면 */Dinners/Create* URL에 양식 게시물을 수행하고 HTTP &lt;POST&gt; 동사를 사용하여 HTML 입력 양식 값을 제출합니다.

이제 만들기 작업 메서드의 HTTP POST 동작을 구현해 보겠습니다. HTTP POST 시나리오를 처리한다는 것을 나타내는 "AcceptVerbs" 특성이 있는 DinnersController에 오버로드된 "만들기" 작업 메서드를 추가하여 시작합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP-POST 지원 "만들기" 메서드 내에서 게시된 양식 매개 변수에 액세스할 수 있는 방법에는 여러 가지가 있습니다.

한 가지 방법은 새 Dinner 개체를 만든 다음 *UpdateModel()* 도우미 메서드(편집 작업에서 와 같이)를 사용하여 게시된 양식 값으로 채우는 것입니다. 그런 다음 DinnerRepository에 추가하고 데이터베이스에 유지한 다음 사용자를 세부 정보 작업으로 리디렉션하여 아래 코드를 사용하여 새로 만든 Dinner를 표시할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

또는 Create() 작업 메서드가 Dinner 개체를 메서드 매개 변수로 사용하는 접근 방식을 사용할 수 있습니다. ASP.NET MVC는 자동으로 우리를 위해 새 Dinner 개체를 인스턴스화하고 양식 입력을 사용하여 속성을 채우고 작업 메서드에 전달합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

위의 작업 메서드는 ModelState.IsValid 속성을 확인 하여 Dinner 개체가 양식 게시물 값으로 성공적으로 채워졌는지 확인합니다. 입력 변환 문제(예: EventDate 속성에 대한 "BOGUS" 문자열)가 있고 문제가 있는 경우 작업 메서드가 양식을 다시 표시하는 경우 false가 반환됩니다.

입력 값이 유효한 경우 작업 메서드는 DinnerRepository에 새 Dinner를 추가하고 저장하려고 시도합니다. 이 작업을 try/catch 블록 내에서 래핑하고 비즈니스 규칙 위반이 있는 경우 양식을 다시 표시합니다(dinnerRepository.Save() 메서드가 예외를 발생시게 됩니다.

이 오류 처리 동작이 작동하는 것을 보려면 */Dinners/Create URL을* 요청하고 새 Dinner에 대한 세부 정보를 입력할 수 있습니다. 잘못된 입력 이나 값 아래와 같이 강조 된 오류와 함께 만들기 양식다시 표시 될 수 있습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

만들기 양식이 편집 양식과 동일한 유효성 검사 및 비즈니스 규칙을 어떻게 준수하는지 확인합니다. 이는 유효성 검사 및 비즈니스 규칙이 모델에 정의되어 있고 응용 프로그램의 UI 또는 컨트롤러 내에 포함되지 않았기 때문입니다. 즉, 나중에 유효성 검사 또는 비즈니스 규칙을 한 곳에서 변경/발전시키고 응용 프로그램 전체에 적용할 수 있습니다. 기존 규칙이나 수정 사항을 자동으로 준수하기 위해 편집 또는 작업 메서드 만들기 내에서 코드를 변경할 필요가 없습니다.

입력 값을 수정하고 "저장" 버튼을 다시 클릭하면 DinnerRepository에 추가가 성공하고 새 Dinner가 데이터베이스에 추가됩니다. 그런 다음 */Dinners/Details/[id]* URL로 리디렉션되며 새로 생성된 저녁 식사에 대한 세부 정보가 표시됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>지원 삭제

이제 DinnersController에 "삭제" 지원을 추가해 보겠습니다.

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET 삭제 작업 방법

먼저 삭제 작업 메서드의 HTTP GET 동작을 구현합니다. 이 메서드는 누군가가 */Dinners/Delete/id] URL을* 방문할 때 호출됩니다. 다음은 구현입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

작업 메서드는 삭제할 Dinner를 검색하려고 시도합니다. Dinner가 있는 경우 Dinner 개체를 기반으로 보기를 렌더링합니다. 개체가 존재하지 않거나 이미 삭제된 경우 "세부 정보" 작업 메서드를 위해 이전에 만든 "NotFound" 뷰 템플릿을 렌더링하는 뷰를 반환합니다.

삭제 작업 메서드 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 "삭제" 보기 템플릿을 만들 수 있습니다. "보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 해당 모델로 전달하고 빈 템플릿을 만들도록 선택했음을 나타냅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에 새 "Delete.aspx" 보기 템플릿 파일이 추가됩니다. 템플릿에 HTML 및 코드를 추가하여 다음과 같은 삭제 확인 화면을 구현합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

위의 코드는 삭제할 Dinner의 제목을 표시하고 &lt;최종&gt; 사용자가 해당 내의 "삭제" 단추를 클릭하면 POST를 수행하는 양식 요소를 /Dinners/Delete/[id] URL로 출력합니다.

응용 프로그램을 실행하고 유효한 Dinner 개체에 대한 *"/Dinners/Delete/id"URL에* 액세스하면 다음과 같이 UI가 렌더링됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **측면 주제: POST를 수행하는 이유는 무엇입니까?** |
| --- |
| 삭제 확인 화면에서 &lt;양식을&gt; 만드는 작업을 거치게 된 이유는 무엇입니까? 실제 삭제 작업을 수행하는 작업 메서드에 연결하기 위해 표준 하이퍼링크를 사용하는 것은 어떨까요? 그 이유는 웹 크롤러와 검색 엔진이 URL을 발견하고 링크를 따를 때 실수로 데이터가 삭제되는 것을 막기 위해 주의를 기울여야 하기 때문입니다. HTTP-GET 기반 URL은 액세스/크롤링에 대해 "안전"으로 간주되며 HTTP-POST URL을 따르지 않아야 합니다. 좋은 규칙은 항상 HTTP-POST 요청 뒤에 파괴적 이거나 데이터 수정 작업을 배치 하는 것입니다. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP-POST 삭제 작업 방법 구현

이제 삭제 확인 화면을 표시하는 삭제 작업 메서드의 HTTP-GET 버전이 구현되었습니다. 최종 사용자가 "삭제" 버튼을 클릭하면 */Dinners/Dinner/[id]* URL에 양식 게시물을 수행합니다.

이제 아래 코드를 사용하여 삭제 작업 메서드의 HTTP "POST" 동작을 구현해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

삭제 작업 메서드의 HTTP-POST 버전은 삭제할 dinner 개체를 검색하려고 시도합니다. 찾을 수 없는 경우(이미 삭제되었기 때문에) "NotFound" 템플릿을 렌더링합니다. 저녁 식사가 발견되면 DinnerRepository에서 삭제됩니다. 그런 다음 "삭제됨" 템플릿을 렌더링합니다.

"삭제됨" 템플릿을 구현하려면 작업 메서드에서 마우스 오른쪽 단추로 클릭하고 "보기 추가" 컨텍스트 메뉴를 선택합니다. 뷰의 이름을 "삭제됨"으로 지정하고 빈 템플릿으로 지정하고 강력한 형식의 모델 개체를 사용하지 않도록 합니다. 그런 다음 HTML 콘텐츠를 추가합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

그리고 지금 우리가 우리의 응용 프로그램을 실행 하 고 액세스 할 때 *"/Dinners/Delete/id]"* URL 유효한 Dinner 개체에 대 한 그것은 렌더링 됩니다 우리의 Dinner 삭제 확인 화면 아래 와 같이:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"삭제" 버튼을 클릭하면 데이터베이스에서 Dinner를 삭제하고 "삭제됨" 보기 템플릿을 표시하는 */Dinners/Delete/[id]* URL에 HTTP-POST를 수행합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>모델 바인딩 보안

ASP.NET MVC의 기본 제공 모델 바인딩 기능을 사용하는 두 가지 방법에 대해 설명했습니다. 첫 번째는 UpdateModel() 메서드를 사용하여 기존 모델 개체의 속성을 업데이트하고 두 번째는 ASP.NET MVC의 지원으로 모델 개체를 작업 메서드 매개 변수로 전달합니다. 이 두 가지 기술은 모두 매우 강력하고 매우 유용합니다.

이 힘은 또한 그 힘으로 책임을 가져옵니다. 사용자 입력을 수락할 때 항상 보안에 대해 편집증적으로 하는 것이 중요하며, 개체를 바인딩하여 입력을 형성할 때도 마찬가지입니다. HTML 및 JavaScript 주입 공격을 피하기 위해 항상 사용자 입력 된 값을 인코딩하고 SQL 주입 공격에주의해야합니다 (참고 : 이러한 유형의 공격을 방지하기 위해 매개 변수를 자동으로 인코딩하는 응용 프로그램에 LINQto to SQL을 사용하고 있습니다). 클라이언트 측 유효성 검사만으로는 절대로 사용하지 말아야 하며 항상 서버 측 유효성 검사를 사용하여 가짜 값을 보내려는 해커를 방지합니다.

ASP.NET MVC의 바인딩 기능을 사용할 때 생각할 수 있는 추가 보안 항목 중 하나는 바인딩할 개체의 범위입니다. 특히 바인딩할 수 있는 속성의 보안 의미를 이해하고 최종 사용자가 실제로 업데이트해야 하는 속성만 업데이트하도록 허용해야 합니다.

기본적으로 UpdateModel() 메서드는 들어오는 양식 매개 변수 값과 일치하는 모델 개체의 모든 속성을 업데이트하려고 시도합니다. 마찬가지로 작업 메서드 매개 변수로 전달된 개체는 기본적으로 양식 매개 변수를 통해 설정된 모든 속성을 가질 수 있습니다.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>사용단위로 바인딩 잠금

업데이트할 수 있는 속성의 명시적 "포함 목록"을 제공하여 사용별로 바인딩 정책을 잠글 수 있습니다. 이 작업은 다음과 같은 UpdateModel() 메서드에 추가 문자열 배열 매개 변수를 전달하여 수행할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

작업 메서드 매개 변수로 전달된 개체는 다음과 같이 허용된 속성의 "포함 목록"을 지정할 수 있는 [Bind] 특성도 지원합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>형식별로 바인딩 잠금

형식별로 바인딩 규칙을 잠글 수도 있습니다. 이렇게 하면 바인딩 규칙을 한 번 지정한 다음 모든 컨트롤러 및 작업 메서드에서 모든 시나리오(UpdateModel 및 action 메서드 매개 변수 시나리오 포함)에 적용하도록 할 수 있습니다.

형식에 [Bind] 특성을 추가하거나 응용 프로그램의 Global.asax 파일 내에 등록하여 형식별 바인딩 규칙을 사용자 지정할 수 있습니다(형식을 소유하지 않은 시나리오에 유용). 그런 다음 Bind 특성의 Include 및 Exclude 속성을 사용하여 특정 클래스 또는 인터페이스에 바인딩할 수 있는 속성을 제어할 수 있습니다.

NerdDinner 응용 프로그램에서 Dinner 클래스에 이 기술을 사용하고 바인딩 가능한 속성 목록을 다음으로 제한하는 [Bind] 특성을 추가합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

바인딩을 통해 RSVS 컬렉션을 조작할 수 없으며 DinnerID 또는 HostedBy 속성을 바인딩을 통해 설정할 수 없습니다. 보안상의 이유로 작업 메서드 내에서 명시적 코드를 사용하여 이러한 특정 속성만 조작합니다.

### <a name="crud-wrap-up"></a>CRUD 랩업

ASP.NET MVC에는 양식 게시 시나리오를 구현하는 데 도움이 되는 여러 기본 제공 기능이 포함되어 있습니다. 우리는 우리의 DinnerRepository 의 상단에 CRUD UI 지원을 제공하기 위해 이러한 기능의 다양한 사용했다.

우리는 우리의 응용 프로그램을 구현하기 위해 모델 중심의 접근 방식을 사용하고 있습니다. 즉, 모든 유효성 검사 및 비즈니스 규칙 논리는 컨트롤러 나 뷰 내에서가 아니라 모델 계층 내에서 정의됩니다. 컨트롤러 클래스나 View 템플릿은 Dinner 모델 클래스에서 적용되는 특정 비즈니스 규칙에 대해 알지 못합니다.

이렇게 하면 응용 프로그램 아키텍처를 깔끔하게 유지하고 테스트하기가 더 쉬워집니다. 나중에 모델 계층에 비즈니스 규칙을 추가할 수 있으며 지원하기 위해 컨트롤러 또는 뷰에 *코드를 변경할 필요가 없습니다.* 이를 통해 향후 응용 프로그램을 발전시키고 변경할 수 있는 민첩성이 크게 제공될 것입니다.

이제 DinnersController를 사용하면 저녁 식사 목록 / 세부 정보뿐만 아니라 지원을 생성, 편집 및 삭제할 수 있습니다. 클래스의 전체 코드는 아래에서 찾을 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>다음 단계

이제 DinnersController 클래스 내에서 기본 CRUD(만들기, 읽기, 업데이트 및 삭제) 지원 구현이 있습니다.

이제 ViewData 및 ViewModel 클래스를 사용하여 양식에서 더욱 풍부한 UI를 활성화하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)
