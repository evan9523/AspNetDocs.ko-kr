---
title: MVC 앱에 뷰 추가
author: Rick-Anderson
description: MVC 앱에 뷰 추가
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045015"
---
# <a name="adding-a-view"></a>보기 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 섹션에서는 `HelloWorldController` 뷰 템플릿 파일을 사용 하 여 클라이언트에 HTML 응답을 생성 하는 프로세스를 명확 하 게 캡슐화 하도록 클래스를 수정 하겠습니다. 

[Razor 뷰 엔진](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)을 사용 하 여 뷰 템플릿 파일을 만듭니다. Razor 기반 뷰 템플릿은 파일 확장명이. c #을 사용 하 여 HTML 출력을 만드는 세련 된 방법을 제공 *합니다* . Razor는 보기 템플릿을 작성할 때 필요한 문자 및 키 입력 수를 최소화 하 고 신속 하 고 유체 코딩 워크플로를 사용 하도록 설정 합니다.

현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다. `Index`다음 코드와 같이 메서드를 변경 하 여 Controller [뷰](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) 메서드를 호출 합니다.

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

`Index`위의 메서드는 뷰 템플릿을 사용 하 여 브라우저에 HTML 응답을 생성 합니다. 위의 메서드와 같은 컨트롤러 메서드 ( [동작 메서드](http://rachelappel.com/asp.net-mvc-actionresults-explained)라고도 함)는 `Index` 일반적으로 문자열과 같은 기본 형식이 아닌 [Actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (또는 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)에서 파생 된 클래스)를 반환 합니다.

*Views\HelloWorld* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **MVC 5 뷰 페이지 (Razor)** 를 클릭 합니다.
  
![](adding-a-view/_static/image1.png)   
  
**항목 이름 지정** 대화 상자에서 *Index*를 입력 한 다음 **확인**을 클릭 합니다.  
  
![](adding-a-view/_static/image2.png)  
  
**레이아웃 페이지 선택** 대화 상자에서 기본 ** \_ 레이아웃** 을 그대로 적용 하 고 **확인**을 클릭 합니다.  
  
![](adding-a-view/_static/image3.png)  
  
위의 대화 상자에서 *Views\Shared* 폴더는 왼쪽 창에서 선택 됩니다. 다른 폴더에 사용자 지정 레이아웃 파일이 있는 경우이를 선택할 수 있습니다. 이 자습서의 뒷부분에서 레이아웃 파일에 대해 설명 합니다.

*MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 만들어집니다.

![](adding-a-view/_static/image4.png)

다음 강조 표시 된 태그를 추가 합니다.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

*Index cshtml* 파일을 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택 합니다.

![PI](adding-a-view/_static/image5.png)

*인덱스* 를 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기** 를 선택할 수도 있습니다. 자세한 내용은 [페이지 검사기 자습서](../../views/using-page-inspector-in-aspnet-mvc.md) 를 참조 하십시오.

또는 응용 프로그램을 실행 하 고 `HelloWorld` 컨트롤러 ()로 이동 `http://localhost:xxxx/HelloWorld` 합니다. `Index`컨트롤러의 메서드는 많은 작업을 수행 하지 않았습니다. 문을 실행 하기만 했습니다 `return View()` . 메서드는 뷰 템플릿 파일을 사용 하 여 브라우저에 응답을 렌더링 하도록 지정 합니다. 사용할 뷰 템플릿 파일의 이름을 명시적으로 지정 하지 않았기 때문에 ASP.NET *MVC는* \Views\HelloWorld 폴더에 있는 폴더에서 기본적으로 *\Views\HelloWorld* 폴더를 사용 합니다. 아래 이미지는 뷰에 &quot; 하드 코딩 된 보기 템플릿의 Hello 문자열을 보여 줍니다 &quot; .

![](adding-a-view/_static/image6.png)

매우 유용 합니다. 그러나 브라우저의 제목 표시줄에는 "Index-My ASP.NET Application"이 표시 되 고 페이지 맨 위에 있는 빅 링크에는 "응용 프로그램 이름"이 표시 됩니다. 브라우저 창의 크기에 따라 오른쪽 위에 있는 세 개의 막대를 클릭 하 여 **홈**, **정보**, **연락처**, **등록** 및 **로그인** 링크를 확인 해야 할 수 있습니다.

## <a name="changing-views-and-layout-pages"></a>보기 및 레이아웃 페이지 변경

먼저 &quot; 페이지 위쪽의 응용 프로그램 이름 링크를 변경 합니다 &quot; . 해당 텍스트는 모든 페이지에 공통적입니다. 응용 프로그램의 모든 페이지에 표시 되더라도 실제로는 프로젝트의 한 곳 에서만 구현 됩니다. **솔루션 탐색기** 의 */Views/Shared* 폴더로 이동 하 여 * \_ Layout. cshtml* 파일을 엽니다. 이 파일을 *레이아웃 페이지* 라고 하며 다른 모든 페이지에서 사용 하는 공유 폴더에 있습니다.

![_LayoutCshtml](adding-a-view/_static/image7.png)

레이아웃 템플릿을 사용하면 한 곳에서 사이트의 HTML 컨테이너 레이아웃을 지정한 다음 사이트의 여러 페이지에 걸쳐 적용할 수 있습니다. `@RenderBody()` 줄을 찾습니다. `RenderBody`는 사용자가 만드는 모든 보기 전용 페이지가 표시되는 자리 표시자이며 레이아웃 페이지에서 &quot;래핑됩니다&quot;. 예를 들어 **About** 링크를 선택 하면 *Views\Home\About.cshtml* 뷰가 메서드 내에서 렌더링 됩니다 `RenderBody` .

제목 요소의 콘텐츠를 변경합니다. 레이아웃 템플릿의 [m을](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) &quot; 응용 프로그램 이름에서 &quot; &quot; MVC Movie로 &quot; , 컨트롤러를에서 `Home` 로 `Movies` 변경 합니다. 전체 레이아웃 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

응용 프로그램을 실행 하 고 이제 MVC 동영상이 표시 되는지 확인 합니다 &quot; &quot; . **About** 링크를 클릭 하면 해당 페이지에 MVC 동영상이 표시 되는 방식이 표시 &quot; &quot; 됩니다. 레이아웃 템플릿을 한 번 변경 하 고 사이트의 모든 페이지에 새 제목을 반영할 수 있습니다.

![](adding-a-view/_static/image8.png)

*Views\HelloWorld\Index.cshtml* 파일을 처음 만들었을 때이 파일에는 다음 코드가 포함 됩니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

위의 Razor 코드는 레이아웃 페이지를 명시적으로 설정 합니다. *뷰 \\ _ViewStart cshtml* 파일에는 정확히 동일한 Razor 태그가 포함 되어 있습니다. *[뷰 \\ _ViewStart cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 파일은 모든 보기에서 사용 되는 공통 레이아웃을 정의 하므로 *Views\HelloWorld\Index.cshtml* 파일에서 코드를 주석으로 처리 하거나 제거할 수 있습니다.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

`Layout` 속성을 사용하여 다른 레이아웃 보기를 설정하거나 레이아웃 파일을 사용하지 않도록 `null`로 설정할 수 있습니다.

이제 인덱스 뷰의 제목을 변경 하겠습니다.

*MvcMovie\Views\HelloWorld\Index.cshtml*를 엽니다. 변경 하는 데는 두 가지 위치가 있습니다. 첫 번째는 브라우저의 제목에 표시 되는 텍스트이 고, 그 다음에는 보조 헤더 (요소)에 표시 됩니다. `<h2>` 어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

표시할 HTML 제목을 나타내려면 위의 코드는 개체의 속성을 설정 합니다 `Title` `ViewBag` (여기서는 *인덱스. cshtml* 뷰 템플릿). 레이아웃 템플릿 ( *Views\Shared \\ _Layout. cshtml* )은 요소에서이 값을 `<title>` `<head>` 이전에 수정한 HTML 섹션의 일부로 사용 합니다.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

이 방법을 사용 하 여 `ViewBag` 보기 템플릿과 레이아웃 파일 사이에 다른 매개 변수를 쉽게 전달할 수 있습니다.

애플리케이션을 실행합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl + F5 키를 눌러 서버의 응답을 강제로 로드 합니다. 브라우저 제목은 `ViewBag.Title` *인덱스* 에서 설정 하 고, &quot; 레이아웃 파일에 추가 된 동영상 앱을 &quot; 추가 하 여 생성 됩니다.

또한 *색인과* 뷰 템플릿의 콘텐츠가 레이아웃에 병합 되었는지 확인 * \_ 합니다. CSHTML* 뷰 템플릿과 단일 HTML 응답이 브라우저에 전송 되었습니다. 레이아웃 템플릿을 사용하면 애플리케이션의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.

![](adding-a-view/_static/image9.png)

그러나 약간의 &quot; 데이터 &quot; (이 경우에는 &quot; 보기 템플릿! 메시지의 Hello &quot; )는 하드 코드 되어 있습니다. MVC 응용 프로그램에는 &quot; V ( &quot; 뷰)가 있으며 &quot; C ( &quot; 컨트롤러)가 있지만 &quot; M &quot; (모델)은 없습니다. 잠시 후 데이터베이스를 만들고 해당 데이터베이스에서 모델 데이터를 검색 하는 방법을 살펴보겠습니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

데이터베이스로 이동 하 여 모델에 대해 이야기 하기 전에 먼저 컨트롤러에서 뷰로 정보를 전달 하는 방법에 대해 알아보겠습니다. 컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다. 컨트롤러 클래스는 들어오는 브라우저 요청을 처리 하는 코드를 작성 하 고, 데이터베이스에서 데이터를 검색 하 고, 궁극적으로 브라우저에 다시 보낼 응답 유형을 결정 합니다. 그러면 컨트롤러에서 뷰 템플릿을 사용 하 여 브라우저에 HTML 응답을 생성 하 고 서식을 지정할 수 있습니다.

컨트롤러는 뷰 템플릿이 브라우저에 응답을 렌더링 하는 데 필요한 모든 데이터 또는 개체를 제공 합니다. 모범 사례: **뷰 템플릿은 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 하지 않아야**합니다. 대신, 뷰 템플릿은 컨트롤러에서 제공 하는 데이터에 대해서만 작동 해야 합니다. 이러한 문제의 &quot; 분리를 유지 &quot; 하면 코드를 정리 하 고, 테스트 가능 하 고, 유지 관리 하기 쉽게 유지할 수 있습니다.

현재 `Welcome` 클래스의 작업 메서드는 `HelloWorldController` 및 매개 변수를 사용 하 여 `name` 값을 `numTimes` 브라우저에 직접 출력 합니다. 컨트롤러에서이 응답을 문자열로 렌더링 하 게 하는 대신 뷰 템플릿을 사용 하도록 컨트롤러를 변경 하겠습니다. 보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다. 이렇게 하려면 뷰가 뷰 템플릿이 `ViewBag` 액세스할 수 있는 개체에 필요한 동적 데이터 (매개 변수)를 컨트롤러에서 배치 하도록 하 여이 작업을 수행할 수 있습니다.

*HelloWorldController.cs* 파일로 돌아가서 메서드를 변경 하 여 `Welcome` `Message` 및 `NumTimes` 값을 개체에 추가 `ViewBag` 합니다. `ViewBag` 는 동적 개체입니다. 즉,에 원하는 모든 항목을 넣을 수 있습니다. `ViewBag` 개체 안에 항목을 넣을 때까지 개체에 정의 된 속성이 없습니다. [ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 은 `name` `numTimes` 주소 표시줄의 쿼리 문자열에서 메서드의 매개 변수로 명명 된 매개 변수 (및)를 자동으로 매핑합니다. 전체 *HelloWorldController.cs* 파일은 다음과 같습니다.

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

이제 `ViewBag` 개체는 뷰에 자동으로 전달 되는 데이터를 포함 합니다. 다음으로 시작 보기 템플릿이 필요 합니다. **빌드** 메뉴에서 **솔루션 빌드** (또는 Ctrl + Shift + B)를 선택 하 여 프로젝트가 컴파일되는지 확인 합니다. *Views\HelloWorld* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **MVC 5 뷰 페이지 (Razor)** 를 클릭 합니다.
  
![](adding-a-view/_static/image10.png)   
  
**항목 이름 지정** 대화 상자에서 *시작*을 입력 한 다음 **확인**을 클릭 합니다.   
  
**레이아웃 페이지 선택** 대화 상자에서 기본 ** \_ 레이아웃** 을 그대로 적용 하 고 **확인**을 클릭 합니다.  
  
![](adding-a-view/_static/image11.png)   

*MvcMovie\Views\HelloWorld\Welcome.cshtml* 파일이 만들어집니다.

*시작. cshtml* 파일의 태그를 바꿉니다. 사용자에 게 표시 되는 횟수 만큼 Hello 라는 루프를 만듭니다 &quot; &quot; . 전체 *시작. cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

이제 데이터가 URL에서 가져온 후 [모델 바인더](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)를 사용 하 여 컨트롤러에 전달 됩니다. 컨트롤러는 데이터를 개체로 패키지 하 `ViewBag` 고 해당 개체를 뷰에 전달 합니다. 그런 다음 보기는 사용자에 게 데이터를 HTML로 표시 합니다.

![](adding-a-view/_static/image12.png)

위의 샘플에서는 개체를 사용 하 여 `ViewBag` 컨트롤러에서 뷰로 데이터를 전달 했습니다. 자습서의 뒷부분에서 보기 모델을 사용하여 컨트롤러에서 보기로 데이터를 전달합니다. 데이터 전달에 대 한 뷰 모델 접근 방식은 일반적으로 보기 모음 접근 방법 보다 훨씬 선호 됩니다. 자세한 내용은 블로그 항목 [동적 V 강력한 형식의 뷰](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 를 참조 하세요. 

이것은 &quot; &quot; 모델의 경우에는 데이터베이스 종류가 아니라 M의 일종입니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
