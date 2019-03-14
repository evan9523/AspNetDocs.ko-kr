---
title: 파일 감시자를 사용하여 ASP.NET Core 앱 개발
author: rick-anderson
description: 이 자습서에서는 ASP.NET Core 앱에서 .NET Core CLI 파일 감시자(dotnet 조사식) 도구를 사용하는 방법을 보여줍니다.
ms.author: riande
ms.date: 05/31/2018
uid: tutorials/dotnet-watch
ms.openlocfilehash: f1e0d91b27df4af7cbfb6f2547c94c0370c65d0d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029590"
---
# <a name="develop-aspnet-core-apps-using-a-file-watcher"></a>파일 감시자를 사용하여 ASP.NET Core 앱 개발

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Victor Hurdugaci](https://twitter.com/victorhurdugaci)

`dotnet watch`은 원본 파일을 변경할 때 [.NET Core CLI](/dotnet/core/tools) 명령을 실행하는 도구입니다. 예를 들어 파일 변경은 컴파일, 테스트 실행 또는 배포를 트리거할 수 있습니다.

이 자습서에서는 합계를 반환하는 엔드포인트 및 제품을 반환하는 엔드포인트 등 두 개의 엔드포인트에서 기존 Web API를 사용합니다. 제품 메서드에는 버그가 있습니다. 이 문제가 이 자습서에서 해결되었습니다.

[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample)을 다운로드합니다. 다음 두 프로젝트로 구성되어 있습니다. *WebApp*(ASP.NET Core 웹 API) 및 *WebAppTests*(웹 API의 단위 테스트).

명령 셸에서 *WebApp* 폴더로 이동합니다. 다음 명령을 실행합니다.

```console
dotnet run
```

콘솔 출력은 다음과 유사한 메시지를 표시합니다(앱이 실행되고 요청을 대기하는 것을 나타냄).

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

웹 브라우저에서 `http://localhost:<port number>/api/math/sum?a=4&b=5`로 이동합니다. `9`라는 결과가 표시됩니다.

API 제품으로 이동합니다(`http://localhost:<port number>/api/math/product?a=4&b=5`). 예상한 대로 `20`이 아니라 `9`를 반환합니다. 이러한 문제는이 자습서의 뒷부분에서 해결되었습니다.

::: moniker range="<= aspnetcore-2.0"

## <a name="add-dotnet-watch-to-a-project"></a>프로젝트에 `dotnet watch` 추가

`dotnet watch` 파일 감시자 도구는 .NET Core SDK 버전 2.1.300에 포함되어 있습니다. 다음 단계는 이전 버전의 .NET Core SDK를 사용하는 경우에 필요합니다.

1. `Microsoft.DotNet.Watcher.Tools` 패키지 참조를 *.csproj* 파일에 추가합니다.

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>
    ```

1. 다음 명령을 실행하여 `Microsoft.DotNet.Watcher.Tools` 패키지를 설치합니다.

    ```console
    dotnet restore
    ```

::: moniker-end

## <a name="run-net-core-cli-commands-using-dotnet-watch"></a>`dotnet watch`를 사용하여 .NET Core CLI 명령 실행

모든 [.NET Core CLI 명령](/dotnet/core/tools#cli-commands)을 `dotnet watch`로 실행할 수 있습니다. 예를 들어:

| 명령 | watch를 사용하는 명령 |
| ---- | ----- |
| dotnet run | dotnet watch run |
| dotnet run -f netcoreapp2.0 | dotnet watch run -f netcoreapp2.0 |
| dotnet run -f netcoreapp2.0 -- --arg1 | dotnet watch run -f netcoreapp2.0 -- --arg1 |
| dotnet test | dotnet watch 테스트 |

*WebApp* 폴더에서 `dotnet watch run`을 실행합니다. 콘솔 출력은 `watch`가 시작했음을 나타냅니다.

## <a name="make-changes-with-dotnet-watch"></a>`dotnet watch` 변경

`dotnet watch`가 실행되고 있는지 확인합니다.

합계가 아닌 제품을 반환하도록 *MathController.cs*의 `Product` 메서드에서 버그를 수정합니다.

```csharp
public static int Product(int a, int b)
{
  return a * b;
}
```

파일을 저장합니다. 콘솔 출력은 `dotnet watch`에서 파일 변경을 검색했고 앱을 다시 시작했음을 나타냅니다.

`http://localhost:<port number>/api/math/product?a=4&b=5`에서 올바른 결과를 반환하는지 확인합니다.

## <a name="run-tests-using-dotnet-watch"></a>`dotnet watch`를 사용하여 테스트 실행

1. *MathController.cs*의 `Product` 메서드가 합계를 반환하도록 변경합니다. 파일을 저장합니다.
1. 명령 셸에서 *WebAppTests* 폴더로 이동합니다.
1. [dotnet restore](/dotnet/core/tools/dotnet-restore)를 실행합니다.
1. `dotnet watch test`를 실행합니다. 이 출력은 테스트에 실패했으며 감시자가 파일 변경을 대기 중임을 나타냅니다.

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. 제품을 반환하도록 `Product` 메서드 코드를 수정합니다. 파일을 저장합니다.

`dotnet watch`는 파일 변경을 검색하고 테스트를 다시 실행합니다. 콘솔 출력은 통과된 테스트를 나타냅니다.

## <a name="customize-files-list-to-watch"></a>조사할 파일 목록 사용자 지정

기본적으로 `dotnet-watch`는 다음 GLOB 패턴과 일치하는 모든 파일을 추적합니다.

* `**/*.cs`
* `*.csproj`
* `**/*.resx`

*.csproj* 파일을 편집하여 조사식 목록에 더 많은 항목을 추가할 수 있습니다. 개별적으로 또는 GLOB 패턴을 사용하여 항목을 지정할 수 있습니다.

```xml
<ItemGroup>
    <!-- extends watching group to include *.js files -->
    <Watch Include="**\*.js" Exclude="node_modules\**\*;**\*.js.map;obj\**\*;bin\**\*" />
</ItemGroup>
```

## <a name="opt-out-of-files-to-be-watched"></a>감시할 파일 옵트아웃

기본 설정을 무시하도록 `dotnet-watch`를 구성할 수 있습니다. 특정 파일을 무시하려면 *.csproj* 파일에서 `Watch="false"` 특성을 항목의 정의로 추가합니다.

```xml
<ItemGroup>
    <!-- exclude Generated.cs from dotnet-watch -->
    <Compile Include="Generated.cs" Watch="false" />

    <!-- exclude Strings.resx from dotnet-watch -->
    <EmbeddedResource Include="Strings.resx" Watch="false" />

    <!-- exclude changes in this referenced project -->
    <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj" Watch="false" />
</ItemGroup>
```

## <a name="custom-watch-projects"></a>사용자 정의 조사식 프로젝트

`dotnet-watch`는 C# 프로젝트로 제한되지 않습니다. 다른 시나리오를 처리하도록 사용자 지정 조사식 프로젝트를 만들 수 있습니다. 다음 프로젝트 레이아웃을 사용합니다.

* **test/**
  * *UnitTests/UnitTests.csproj*
  * *IntegrationTests/IntegrationTests.csproj*

두 프로젝트를 조사하는 것이 목적인 경우 두 프로젝트를 감시하도록 구성된 사용자 지정 프로젝트 파일을 만듭니다.

```xml
<Project>
    <ItemGroup>
        <TestProjects Include="**\*.csproj" />
        <Watch Include="**\*.cs" />
    </ItemGroup>

    <Target Name="Test">
        <MSBuild Targets="VSTest" Projects="@(TestProjects)" />
    </Target>

    <Import Project="$(MSBuildExtensionsPath)\Microsoft.Common.targets" />
</Project>
```

파일이 두 프로젝트를 감시하는 시작하려면 *test* 폴더를 변경합니다. 다음 명령을 실행합니다.

```console
dotnet watch msbuild /t:Test
```

테스트 프로젝트 중 하나에서 파일을 변경하면 VSTest가 실행됩니다.

## <a name="dotnet-watch-in-github"></a>GitHub의 `dotnet-watch`

`dotnet-watch`는 GitHub [aspnet/AspNetCore 리포지토리](https://github.com/aspnet/AspNetCore/tree/master/src/Tools/dotnet-watch)의 일부입니다.
