---
title: 첫 번째 Razor 구성 요소 앱 빌드
author: guardrex
description: Blazor 구성 요소 앱을 단계별로 빌드하고 기본 Razor 구성 요소 개념을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040780"
---
# <a name="build-your-first-razor-components-app"></a>첫 번째 Razor 구성 요소 앱 빌드

작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

이 자습서에서는 Razor 구성 요소를 사용하여 앱을 빌드하는 방법을 보여 주고 기본 Razor 구성 요소 개념을 설명합니다. Razor 구성 요소 기반 프로젝트(.NET Core 3.0 이상에서 지원됨)를 사용하거나 Blazor 기반 프로젝트(.NET Core의 이후 릴리스에서 지원됨)를 사용하여 이 자습서를 진행할 수 있습니다.

ASP.NET Core Razor 구성 요소(‘권장’)를 사용하는 환경의 경우:

* <xref:razor-components/get-started>의 지침에 따라 Razor 구성 요소 기반 프로젝트를 만듭니다.
* 프로젝트 이름을 `RazorComponents`로 지정합니다.
* 다중 프로젝트 솔루션은 Razor 구성 요소 템플릿에서 만들어집니다. Razor 구성 요소 프로젝트는 *RazorComponents.App*으로 생성됩니다.

Blazor를 사용하는 환경의 경우:

* <xref:spa/blazor/get-started>의 지침에 따라 Blazor 기반 프로젝트를 만듭니다.
* 프로젝트 이름을 `Blazor`로 지정합니다.
* 단일 프로젝트 솔루션은 Blazor 템플릿에서 만들어집니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample)) 필수 구성 요소에 대해서는 다음 항목을 참조하세요.

## <a name="build-components"></a>구성 요소 빌드

1. 각 앱의 세 페이지로 이동합니다. 홈, 카운터 및 Fetch 데이터. 이 페이지는 *Pages* 폴더에 있는 Razor 파일로 구현됩니다. *Index.cshtml*, *Counter.cshtml* 및 *FetchData.cshtml*.

1. 카운터 페이지에서 **Click me** 단추를 선택하여 페이지 새로 고침 없이 카운터를 증분합니다. 웹 페이지의 카운터를 증분하려면 일반적으로 JavaScript를 작성해야 하지만, Razor 구성 요소는 C#를 사용하여 더 나은 접근 방식을 제공합니다.

1. *Counter.cshtml* 파일에서 Counter 구성 요소의 구현을 살펴봅니다.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   Counter 구성 요소의 UI는 HTML을 사용하여 정의됩니다. 동적 렌더링 논리(예: 루프, 조건, 식)는 [Razor](xref:mvc/views/razor)라는 포함된 C# 구문을 사용하여 추가됩니다. HTML 태그 및 C# 렌더링 논리는 빌드 시 구성 요소 클래스로 변환됩니다. 생성된 .NET 클래스의 이름은 파일 이름과 일치합니다.

   구성 요소 클래스의 멤버는 `@functions` 블록에 정의되어 있습니다. `@functions` 블록에서 구성 요소 상태(속성, 필드) 및 메서드는 이벤트 처리 또는 기타 구성 요소를 정의하기 위해 지정합니다. 그런 다음, 이러한 멤버를 구성 요소 렌더링 논리의 일부 및 이벤트 처리에 사용합니다.

   **Click me** 단추를 선택한 경우:

   * Counter 구성 요소의 등록된 `onclick` 처리기가 호출됩니다(`IncrementCount` 메서드).
   * Counter 구성 요소가 렌더링 트리를 다시 생성합니다.
   * 새 렌더링 트리가 이전 렌더링 트리에 비교됩니다.
   * DOM(문서 개체 모델)에 대한 수정 내용만 적용됩니다. 표시된 개수가 업데이트됩니다.

1. 또한 Counter 구성 요소의 C# 논리를 수정하여 카운트를 1이 아닌 2씩 증분하도록 합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. 앱을 다시 빌드하고 실행하여 변경 내용을 확인합니다. **Click me** 단추를 선택하면 카운터가 2씩 증분됩니다.

## <a name="use-components"></a>구성 요소 사용

HTML 유사 구문을 사용하여 구성 요소를 다른 구성 요소에 포함합니다.

1. Index 구성 요소에 `<Counter />` 요소를 추가하여 앱의 Index(홈페이지) 구성 요소에 Counter 구성 요소를 추가합니다.

   이 환경에 Blazor를 사용하는 경우에는 Survey Prompt 구성 요소(`<SurveyPrompt>` 요소)가 Index 구성 요소에 있습니다. `<SurveyPrompt>` 요소를 `<Counter>` 요소로 바꿉니다.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. 앱을 다시 빌드하고 실행합니다. 홈페이지에는 자체 카운터가 있습니다.

## <a name="component-parameters"></a>구성 요소 매개 변수

구성 요소에는 매개 변수도 포함될 수 있습니다. 구성 요소 매개 변수는 `[Parameter]`로 데코레이트된 component 클래스에서 public이 아닌 속성을 사용하여 정의됩니다. 특성을 사용하여 태그에서 구성 요소의 인수를 지정합니다.

1. 구성 요소의 `@functions` C# 코드를 업데이트합니다.

   * `[Parameter]` 특성으로 데코레이트된 `IncrementAmount` 속성을 추가합니다.
   * `currentCount` 값을 늘릴 때 `IncrementAmount`를 사용하도록 `IncrementCount` 메서드를 변경합니다.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. 특성을 사용하여 Home 구성 요소의 `<Counter>` 요소에 `IncrementAmount` 매개 변수를 지정합니다. 카운터를 10씩 증분하도록 값을 설정합니다.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. 페이지를 다시 로드합니다. **Click me** 단추가 선택될 때마다 홈페이지 카운터가 10씩 증분됩니다. ‘카운터’ 페이지의 카운터는 1씩 증분됩니다.

## <a name="route-to-components"></a>구성 요소 경로

*Counter.cshtml* 파일 맨 위의 `@page` 지시문은 이 구성 요소가 라우팅 엔드포인트임을 지정합니다. Counter 구성 요소는 `/Counter`에 전송된 요청을 처리합니다. `@page` 지시문이 없으면 구성 요소는 라우트된 요청을 처리하지 않지만 구성 요소는 다른 구성 요소에서 계속 사용할 수 있습니다.

## <a name="dependency-injection"></a>종속성 주입

앱의 서비스 컨테이너에 등록된 서비스는 [DI(종속성 주입)](xref:fundamentals/dependency-injection)를 통해 구성 요소에서 사용할 수 있습니다. `@inject` 지시문을 사용하여 서비스를 구성 요소에 삽입합니다.

FetchData 구성 요소(*Pages/FetchData.cshtml*)의 지시문을 검사합니다. `@inject` 지시문은 `WeatherForecastService` 서비스의 인스턴스를 구성 요소에 삽입하는 데 사용됩니다.

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

`WeatherForecastService` 서비스는 [싱글톤](xref:fundamentals/dependency-injection#service-lifetimes)으로 등록되므로, 서비스의 한 인스턴스를 앱 전체에서 사용할 수 있습니다.

FetchData 구성 요소는 삽입된 서비스를 `ForecastService`로 사용하여 `WeatherForecast` 개체의 배열을 검색합니다.

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

[@foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 루프는 각 예측 인스턴스를 날씨 데이터 테이블의 행으로 렌더링하는 데 사용됩니다.

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a>할 일 목록 빌드

간단한 할 일 목록을 구현하는 앱에 새 페이지를 추가합니다.

1. 빈 텍스트 파일의 이름을 *Todo.cshtml*로 지정하여 *Pages* 폴더에 추가합니다.

1. 페이지의 초기 태그를 제공합니다.

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. Todo 페이지를 탐색 모음에 추가합니다.

   NavMenu 구성 요소(*Shared/NavMenu.csthml*)는 앱의 레이아웃에서 사용됩니다. 레이아웃은 앱의 콘텐츠 중복을 방지할 수 있는 구성 요소입니다. 자세한 내용은 <xref:razor-components/layouts>을 참조하세요.

   *Shared/NavMenu.csthml* 파일의 기존 목록 항목 아래에 다음 목록 항목 태그를 추가하여 Todo 페이지의 `<NavLink>`를 추가합니다.

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. 앱을 다시 빌드하고 실행합니다. 새 Todo 페이지를 방문하여 Todo 페이지 링크가 작동하는지 확인합니다.

1. 프로젝트 루트에 *TodoItem.cs* 파일을 추가하여 Todo 항목을 나타내는 클래스를 저장합니다. `TodoItem` 클래스에 대해 다음 C# 코드를 사용합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. Todo 구성 요소(*Todo.cshtml*)로 돌아갑니다.

   * `@functions` 블록에 있는 할 일에 대한 필드를 추가합니다. Todo 구성 요소는 이 필드를 사용하여 할 일 목록의 상태를 유지 관리합니다.
   * 순서가 지정되지 않은 목록 태그 및 `foreach` 루프를 추가하여 각 할 일 항목을 목록 항목으로 렌더링합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. 할 일을 목록에 추가하려면 앱에 UI 요소가 필요합니다. 목록 아래에 텍스트 입력과 단추를 추가합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. 앱을 다시 빌드하고 실행합니다. 단추에 이벤트 처리기가 연결되어 있지 않으므로 **할 일 추가** 단추를 선택하면 아무것도 발생하지 않습니다.

1. `AddTodo` 메서드를 Todo 구성 요소에 추가하고 `onclick` 특성을 사용하여 단추 클릭에 등록합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   단추가 선택되면 `AddTodo` C# 메서드가 호출됩니다.

1. 새 할 일 항목의 제목을 가져오려면 `newTodo` 문자열 필드를 추가하고 `bind` 특성을 사용하여 텍스트 입력 값에 바인딩합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. `AddTodo` 메서드를 업데이트하여 지정된 제목이 있는 `TodoItem`을 목록에 추가합니다. `newTodo`를 빈 문자열로 설정하여 텍스트 입력 값을 지웁니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. 앱을 다시 빌드하고 실행합니다. 할 일 목록에 일부 할 일을 추가하여 새 코드를 테스트합니다.

1. 각 할 일 항목의 제목 텍스트를 편집 가능하게 설정하고 확인란을 통해 사용자가 완료된 항목을 추적하도록 도울 수 있습니다. 각 할 일 항목의 확인란 입력을 추가하고 해당 값을 `IsDone` 속성에 바인딩합니다. `@todo.Title`을 `@todo.Title`에 바인딩된 `<input>` 요소로 변경합니다.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. 해당 값이 바인딩되었는지 확인하려면 `<h1>` 헤더를 업데이트하여 완료되지 않은(`IsDone`이 `false`임) 할 일 항목 수를 표시합니다.

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. 완료된 Todo 구성 요소(*Todo.cshtml*):

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. 앱을 다시 빌드하고 실행합니다. 할 일 항목을 추가하여 새 코드를 테스트합니다.

## <a name="publish-and-deploy-the-app"></a>앱 게시 및 배포

앱을 게시하려면 <xref:host-and-deploy/razor-components/index#publish-the-app>을 참조하세요.
