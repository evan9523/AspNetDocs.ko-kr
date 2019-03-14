---
title: Blazor용 링커 구성
author: guardrex
description: Blazor 앱을 빌드할 때 IL(Intermediate Language) 링커를 제어하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/20/2019
uid: host-and-deploy/razor-components/configure-linker
ms.openlocfilehash: 7c53e7912ec3b0ae471ea38777f874f55a32487d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064540"
---
# <a name="configure-the-linker-for-blazor"></a>Blazor용 링커 구성

[Luke Latham](https://github.com/guardrex)으로

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor는 각 릴리스 모드 빌드 중에 [IL(Intermediate Language)](/dotnet/standard/managed-code#intermediate-language--execution) 연결을 수행하여 출력 어셈블리에서 불필요한 IL을 제거합니다.

다음 방법 중 하나를 사용하여 어셈블리 연결을 제어할 수 있습니다.

* MSBuild 속성을 사용하여 전역적으로 링크를 사용하지 않도록 설정합니다.
* 구성 파일을 사용하여 어셈블리별로 연결을 제어합니다

## <a name="disable-linking-with-an-msbuild-property"></a>MSBuild 속성을 사용하여 연결을 사용하지 않도록 설정합니다.

게시를 포함하는 앱이 빌드되면 릴리스 모드에서 연결이 기본적으로 활성화됩니다. 모든 어셈블리에 대한 연결을 비활성화하려면 프로젝트 파일에서 `<BlazorLinkOnBuild>` MSBuild 속성을 `false`로 설정합니다.

```xml
<PropertyGroup>
  <BlazorLinkOnBuild>false</BlazorLinkOnBuild>
</PropertyGroup>
```

## <a name="control-linking-with-a-configuration-file"></a>구성 파일과의 연결 제어

연결은 XML 구성 파일을 제공하고 프로젝트 파일에서 해당 파일을 MSBuild 항목으로 지정하여 어셈블리별로 제어할 수 있습니다.

다음은 예제 구성 파일(*Linker.xml*)입니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--
  This file specifies which parts of the BCL or Blazor packages must not be
  stripped by the IL Linker even if they aren't referenced by user code.
-->
<linker>
  <assembly fullname="mscorlib">
    <!--
      Preserve the methods in WasmRuntime because its methods are called by 
      JavaScript client-side code to implement timers.
      Fixes: https://github.com/aspnet/Blazor/issues/239
    -->
    <type fullname="System.Threading.WasmRuntime" />
  </assembly>
  <assembly fullname="System.Core">
    <!--
      System.Linq.Expressions* is required by Json.NET and any 
      expression.Compile caller. The assembly isn't stripped.
    -->
    <type fullname="System.Linq.Expressions*" />
  </assembly>
  <!--
    In this example, the app's entry point assembly is listed. The assembly
    isn't stripped by the IL Linker.
  -->
  <assembly fullname="MyCoolBlazorApp" />
</linker>
```

구성 파일의 파일 형식에 대한 자세한 내용은 [IL 링커: Xml 설명자 구문](https://github.com/mono/linker/blob/master/src/linker/README.md#syntax-of-xml-descriptor)을 참조하세요.

`BlazorLinkerDescriptor` 항목을 사용하여 프로젝트 파일에서 구성 파일을 지정합니다.

```xml
<ItemGroup>
  <BlazorLinkerDescriptor Include="Linker.xml" />
</ItemGroup>
```
