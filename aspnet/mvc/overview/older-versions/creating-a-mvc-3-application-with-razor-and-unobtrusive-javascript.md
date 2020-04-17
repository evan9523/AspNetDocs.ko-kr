---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 면도기와 눈에 거슬리지 자바 스크립트와 MVC 3 응용 프로그램 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 사용자 목록 샘플 웹 응용 프로그램은 Razor 보기 엔진을 사용하여 ASP.NET MVC 3 응용 프로그램을 만드는 것이 얼마나 간단한지 보여 줍니다. 샘플 응용 프로그램 ...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542458"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor 및 Unobtrusive JavaScript를 사용하여 MVC 3 애플리케이션 만들기

[로 마이크로 소프트](https://github.com/microsoft)

> 사용자 목록 샘플 웹 응용 프로그램은 Razor 보기 엔진을 사용하여 ASP.NET MVC 3 응용 프로그램을 만드는 것이 얼마나 간단한지 보여 줍니다. 샘플 응용 프로그램은 ASP.NET MVC 버전 3 및 Visual Studio 2010과 함께 새로운 Razor 뷰 엔진을 사용하여 사용자 만들기, 표시, 편집 및 삭제와 같은 기능을 포함하는 가상의 사용자 목록 웹 사이트를 만드는 방법을 보여 줍니다.
> 
> 이 자습서에서는 MVC 3 응용 프로그램에서 사용자 목록 샘플을 빌드하기 위해 수행된 단계를 ASP.NET 설명합니다. C# 및 VB 소스 코드가 있는 Visual Studio 프로젝트를 이 [항목과](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)함께 사용할 수 있습니다. 이 튜토리얼에 대한 질문이있는 경우, [MVC 포럼에](https://forums.asp.net/1146.aspx)게시하시기 바랍니다 .

## <a name="overview"></a>개요

빌드할 응용 프로그램은 간단한 사용자 목록 웹 사이트입니다. 사용자는 사용자 정보를 입력, 보기 및 업데이트할 수 있습니다.

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

여기에서 VB 및 C# 완료된 프로젝트를 다운로드할 수 [있습니다.](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

자습서를 시작 하려면 Visual Studio 2010을 열고 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿을 사용 하 여 새 프로젝트를 만듭니다. 응용 프로그램 &quot;Mvc3Razor의&quot;이름을 지정합니다.

[![새로운 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

새로운 **ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램을**선택하고 Razor 보기 엔진을 선택한 다음 **확인을**클릭합니다.

![새로운 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

이 자습서에서는 ASP.NET 멤버 자격 공급자를 사용 하지 않습니다., 그래서 로그온 및 멤버 자격과 관련 된 모든 파일을 삭제할 수 있습니다. **솔루션 탐색기에서**다음 파일 및 디렉터리를 제거합니다.

- *컨트롤러\계정 컨트롤러*
- *모델\계정 모델*
- *뷰\공유\\_LogOnPartial*
- *뷰\계정(이* 디렉터리에 있는 모든 파일)

![졸 익스피타](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em>&quot;</em>&quot; <em> \_Layout.cshtml</em> 파일을 편집하고 로그인 사용 안 `<div>` 함이라는 요소 `logindisplay` 내부의 태그를 대체합니다. 다음 예제에서는 새 태그를 보여 주며 있습니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>모델 추가

**솔루션 탐색기에서** *모델* 폴더를 마우스 오른쪽 단추로 클릭하고 **에 추가를**선택한 다음 **클래스**를 클릭합니다.

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

클래스 `UserModel` 이름을 지정합니다. *UserModel* 파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

클래스는 `UserModel` 사용자를 나타냅니다. 클래스의 각 멤버는 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임스페이스의 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 주석이 추가됩니다. [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임스페이스의 특성은 웹 응용 프로그램에 대한 자동 클라이언트 및 서버 측 유효성 검사를 제공합니다.

클래스를 `HomeController` 열고 `using` `UserModel` 및 `Users` 클래스에 액세스할 수 있도록 지시문을 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

`HomeController` 선언 직후 다음 주석과 참조를 클래스에 `Users` 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

클래스는 `Users` 이 자습서에서 사용할 단순화된 메모리 내 데이터 저장소입니다. 실제 응용 프로그램에서는 데이터베이스를 사용하여 사용자 정보를 저장합니다. `HomeController` 파일의 처음 몇 줄은 다음 예제에 나와 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

다음 단계에서 스캐폴딩 마법사에서 사용자 모델을 사용할 수 있도록 응용 프로그램을 빌드합니다.

## <a name="creating-the-default-view"></a>기본 뷰 만들기

다음 단계는 사용자를 표시할 작업 메서드 및 보기를 추가하는 것입니다.

기존 *뷰\Home\Index 파일을 삭제합니다.* 사용자를 표시하는 새 *Index* 파일을 만듭니다.

`HomeController` 클래스에서 `Index` 메서드의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

메서드 내부를 `Index` 마우스 오른쪽 단추로 클릭한 다음 **보기 추가를**클릭합니다.

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

강력한 **형식의 뷰 만들기 옵션을 선택합니다.** **데이터 클래스 보기의**경우 **Mvc3Razor.Models.UserModel**을 선택합니다. (보기 **데이터 클래스** 상자에 **Mvc3Razor.Models.UserModel이** 표시되지 않으면 프로젝트를 빌드해야 합니다.) 뷰 엔진이 **Razor로**설정되어 있는지 확인합니다. **콘텐츠 보기를** **목록으로** 설정한 다음 **추가를**클릭합니다.

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

새 보기는 뷰에 전달된 사용자 데이터를 자동으로 스캐폴드합니다. `Index` 새로 생성된 *뷰\Home\Index 파일을 검사합니다.* **새 만들기,** **편집,** **세부 정보**및 **삭제** 링크는 작동하지 않지만 페이지의 나머지 는 작동합니다. 페이지를 실행합니다. 사용자 목록이 표시됩니다.

![색인 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

*Index.cshtml* 파일을 열고 **편집**, **세부 정보**및 **삭제에** `ActionLink` 대한 태그를 다음 코드로 바꿉니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

사용자 이름은 ID로 사용되어 **편집,** **세부 정보**및 **삭제** 링크에서 선택한 레코드를 찾습니다.

## <a name="creating-the-details-view"></a>세부 정보 보기 만들기

다음 단계는 사용자 `Details` 세부 정보를 표시하기 위해 작업 메서드및 보기를 추가하는 것입니다.

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

홈 컨트롤러에 다음 `Details` 메서드를 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

메서드 내부를 `Details` 마우스 오른쪽 단추로 클릭한 다음 <strong>보기 추가를</strong>선택합니다. <strong>보기 데이터 클래스</strong> 상자에 <strong>Mvc3Razor.Models.UserModel</strong>이 포함되어 있는지 확인합니다.<em>.</em> <strong>콘텐츠 보기를</strong> <strong>세부 정보로</strong> 설정한 다음 <strong>을 클릭합니다.</strong>

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

응용 프로그램을 실행하고 세부 정보 링크를 선택합니다. 자동 스캐폴딩은 모델의 각 속성을 표시합니다.

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>편집 뷰 만들기

홈 컨트롤러에 다음 `Edit` 방법을 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

이전 단계에서와 같이 뷰를 추가하지만 **View 콘텐츠를** **편집하도록**설정합니다.

![편집 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

응용 프로그램을 실행하고 사용자 중 하나의 이름과 성을 편집합니다. `UserModel` 클래스에 적용된 `DataAnnotation` 제약 조건을 위반하는 경우 양식을 제출할 때 서버 코드에서 생성되는 유효성 검사 오류가 표시됩니다. &quot;예를 들어 양식을 제출할 때&quot; 이름 &quot;&quot;Ann을 A로 변경하면 양식에 다음 오류가 표시됩니다.

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

이 자습서에서는 사용자 이름을 기본 키로 처리합니다. 따라서 사용자 이름 속성을 변경할 수 없습니다. *Edit.cshtml* 파일에서 `Html.BeginForm` 명령문 바로 다음에서 사용자 이름을 숨겨진 필드로 설정합니다. 이렇게 하면 모델에서 속성이 전달됩니다. 다음 코드 조각은 명령문의 `Hidden` 배치를 보여 주며,

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

사용자 `TextBoxFor` 이름에 `ValidationMessageFor` 대한 및 마크업을 `DisplayFor` 호출로 바꿉니다. 메서드는 `DisplayFor` 속성을 읽기 전용 요소로 표시합니다. 다음 예제에서는 전체 태그를 보여 줍니다. 원본 `TextBoxFor` 및 `ValidationMessageFor` 호출은 Razor 시작 주석 및 최종 주석`@* *@`문자 () 로 주석처리됩니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>클라이언트 측 유효성 검사 사용

ASP.NET MVC 3에서 클라이언트 측 유효성 검사를 사용하려면 두 개의 플래그를 설정해야 하며 세 개의 JavaScript 파일을 포함해야 합니다.

응용 프로그램의 *Web.config* 파일을 엽니다. 응용 `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` 프로그램 설정에서 확인 및 true로 설정됩니다. 루트 *Web.config* 파일의 다음 조각에는 올바른 설정이 표시됩니다.

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

true로 설정하면 `UnobtrusiveJavaScriptEnabled` 눈에 거슬리지 않는 Ajax 및 눈에 거슬리지 않는 클라이언트 유효성 검사를 수행할 수 있습니다. 눈에 거슬리지 않는 유효성 검사를 사용하면 유효성 검사 규칙이 HTML5 특성으로 바뀌게 됩니다. HTML5 특성 이름은 소문자, 숫자 및 대시로만 구성될 수 있습니다.

true로 설정하면 `ClientValidationEnabled` 클라이언트 측 유효성 검사가 가능합니다. 응용 프로그램 *Web.config* 파일에 이러한 키를 설정 하 여 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 눈에 거슬리지 자바 스크립트를 사용 하도록 설정 합니다. 다음 코드를 사용하여 개별 보기 또는 컨트롤러 메서드에서 이러한 설정을 활성화하거나 사용하지 않도록 설정할 수도 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

또한 렌더링된 보기에 여러 JavaScript 파일을 포함해야 합니다. 모든 보기에 자바스크립트를 포함하는 쉬운 방법은 *뷰\공유\\_Layout.cshtml* 파일에 추가하는 것입니다. Layout.cshtml 파일의 `<head>` 요소를 다음 코드로 바꿉니다. * \_*

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

처음 두 개의 jQuery 스크립트는 Microsoft Ajax 콘텐츠 전송 네트워크(CDN)에서 호스팅됩니다. Microsoft Ajax CDN을 활용하면 응용 프로그램의 첫 번째 성능이 크게 향상될 수 있습니다.

응용 프로그램을 실행하고 편집 링크를 클릭합니다. 브라우저에서 페이지의 소스를 봅니다. 브라우저 원본에는 양식의 `data-val` 많은 특성이 표시됩니다(데이터 유효성 검사용). 클라이언트 유효성 검사와 눈에 거슬리지 않는 JavaScript를 사용하도록 설정하면 `data-val="true"` 클라이언트 유효성 검사 규칙이 있는 입력 필드에는 눈에 거슬리지 않는 클라이언트 유효성 검사를 트리거하는 특성이 포함됩니다. 예를 들어 `City` 모델의 필드가 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 장식되어 다음 예제에 표시된 HTML이 생성됩니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

각 클라이언트 유효성 검사 규칙에 대해 폼이 `data-val-rulename="message"`있는 특성이 추가됩니다. 앞서 `City` 보여 드신 필드 예제를 사용 하 `data-val-required` 여 필요한 &quot;클라이언트 유효성 검사&quot;규칙 특성을 생성 하 고 메시지 도시 필드가 필요 합니다. 응용 프로그램을 실행하고 사용자 중 하나를 편집하고 `City` 필드를 지웁습니다. 필드를 탭하면 클라이언트 측 유효성 검사 오류 메시지가 표시됩니다.

![도시 필수](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

마찬가지로 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 `data-val-rulename-paramname=paramvalue`폼이 있는 특성이 추가됩니다. 예를 들어 `FirstName` 속성은 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성에 추가되고 최소 길이 3과 최대 길이 8을 지정합니다. 명명된 `length` 데이터 유효성 검사 `max` 규칙에는 매개 변수 이름과 매개 변수 값 8이 있습니다. 다음은 사용자 중 하나를 편집할 `FirstName` 때 필드에 대해 생성되는 HTML을 보여 주는 것입니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

눈에 거슬리지 않는 클라이언트 유효성 검사에 대한 자세한 내용은 브래드 윌슨의 [블로그에서 ASP.NET MVC 3의 눈에 거슬리지 않는 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) 항목을 참조하십시오.

> [!NOTE]
> ASP.NET MVC 3 베타에서는 클라이언트 측 유효성 검사를 시작하려면 양식을 제출해야 하는 경우가 있습니다. 최종 릴리스에 대해 변경될 수 있습니다.

## <a name="creating-the-create-view"></a>뷰 만들기

다음 단계는 사용자가 `Create` 새 사용자를 만들 수 있도록 작업 메서드 및 보기를 추가하는 것입니다. 홈 컨트롤러에 다음 `Create` 메서드를 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

이전 단계에서와 같이 뷰를 추가하지만 **뷰 콘텐츠를** **만들기로 설정합니다.**

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

응용 프로그램을 실행하고 링크 **만들기를** 선택하고 새 사용자를 추가합니다. 메서드는 `Create` 자동으로 클라이언트 쪽 및 서버 쪽 유효성 검사를 활용 합니다. Ben X와 &quot;&quot;같은 공백이 포함된 사용자 이름을 입력해 보십시오. 사용자 이름 필드를 탭하면 클라이언트 측 유효성 검사`White space is not allowed`오류()가 표시됩니다.

## <a name="add-the-delete-method"></a>삭제 메서드 추가

자습서를 완료하려면 홈 `Delete` 컨트롤러에 다음 방법을 추가합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

이전 `Delete` 단계에서와 같이 보기를 추가하여 **콘텐츠** **보기를 삭제로**설정합니다.

![보기 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

이제 유효성 검사를 통해 간단하지만 완벽하게 작동하는 ASP.NET MVC 3 응용 프로그램이 있습니다.
