---
uid: config-builder
title: ASP.NET용 구성 빌더
author: rick-anderson
description: 외부 원본에서 web.config 값 이외의 원본에서 구성 데이터를 가져오는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424795"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="ba628-103">ASP.NET용 구성 빌더</span><span class="sxs-lookup"><span data-stu-id="ba628-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="ba628-104">[Stephen Molloy](https://github.com/StephenMolloy) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ba628-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ba628-105">구성 빌더는 ASP.NET apps가 외부 원본에서 구성 값을 가져올 수 있는 최신 및 agile 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="ba628-106">구성 빌더:</span><span class="sxs-lookup"><span data-stu-id="ba628-106">Configuration builders:</span></span>

* <span data-ttu-id="ba628-107">.NET Framework 4.7.1 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="ba628-108">구성 값을 읽기 위한 유연한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="ba628-109">컨테이너 및 클라우드 중심 환경으로 이동 하는 앱의 기본 요구 사항 중 일부를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="ba628-110">를 사용 하 여 .NET 구성 시스템에서 이전에 사용할 수 없는 소스 (예: Azure Key Vault 및 환경 변수)를 그려서 구성 데이터의 보호를 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="ba628-111">키/값 구성 빌더</span><span class="sxs-lookup"><span data-stu-id="ba628-111">Key/value configuration builders</span></span>

<span data-ttu-id="ba628-112">구성 작성기에서 처리할 수 있는 일반적인 시나리오는 키/값 패턴을 따르는 구성 섹션에 대 한 기본 키/값 대체 메커니즘을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="ba628-113">ConfigurationBuilders의 .NET Framework 개념은 특정 구성 섹션 또는 패턴으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="ba628-114">그러나 `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders))의 많은 구성 빌더가 키/값 패턴 내에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="ba628-115">키/값 구성 작성기 설정</span><span class="sxs-lookup"><span data-stu-id="ba628-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="ba628-116">다음 설정은의 모든 키/값 구성 작성기에 적용 `Microsoft.Configuration.ConfigurationBuilders` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="ba628-117">Mode</span><span class="sxs-lookup"><span data-stu-id="ba628-117">Mode</span></span>

<span data-ttu-id="ba628-118">구성 작성기는 키/값 정보의 외부 소스를 사용 하 여 구성 시스템의 선택 된 키/값 요소를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="ba628-119">특히 `<appSettings/>` 및 섹션은 `<connectionStrings/>` 구성 빌더에서 특별 한 처리를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="ba628-120">빌더는 다음과 같은 세 가지 모드에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-120">The builders work in three modes:</span></span>

* <span data-ttu-id="ba628-121">`Strict`-기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-121">`Strict` - The default mode.</span></span> <span data-ttu-id="ba628-122">이 모드에서 구성 빌더는 잘 알려진 키/값 중심 구성 섹션 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="ba628-123">`Strict`모드 섹션의 각 키를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="ba628-124">외부 원본에 일치 하는 키가 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="ba628-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="ba628-125">구성 빌더는 결과 구성 섹션의 값을 외부 원본의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="ba628-126">`Greedy`-이 모드는 모드와 밀접 하 게 관련 되어 `Strict` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="ba628-127">원래 구성에 이미 있는 키로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="ba628-128">구성 빌더는 외부 소스의 모든 키/값 쌍을 결과 구성 섹션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="ba628-129">`Expand`-구성 섹션 개체로 구문 분석 하기 전에 원시 XML에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="ba628-130">문자열에서 토큰을 확장 하는 것으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="ba628-131">패턴과 일치 하는 원시 XML 문자열의 모든 부분은 `${token}` 토큰 확장의 후보가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="ba628-132">외부 원본에 해당 하는 값이 없으면 토큰이 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="ba628-133">이 모드의 빌더는 및 섹션으로 제한 되지 않습니다 `<appSettings/>` `<connectionStrings/>` .</span><span class="sxs-lookup"><span data-stu-id="ba628-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="ba628-134">*web.config* 에서 다음 태그를 사용 하면 환경 [configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 를 모드에서 사용할 수 있습니다 `Strict` .</span><span class="sxs-lookup"><span data-stu-id="ba628-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="ba628-135">다음 코드는 앞의 `<appSettings/>` `<connectionStrings/>` *web.config* 파일에 나와 있는을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="ba628-136">위의 코드에서는 속성 값을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="ba628-137">환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="ba628-138">환경 변수의 값입니다 (설정 된 경우).</span><span class="sxs-lookup"><span data-stu-id="ba628-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="ba628-139">예를 `ServiceID` 들어에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="ba628-140">환경 변수가 `ServiceID` 설정 되지 않은 경우 "ServiceID value from web.config"</span><span class="sxs-lookup"><span data-stu-id="ba628-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="ba628-141">환경 변수의 값입니다 `ServiceID` (설정 된 경우).</span><span class="sxs-lookup"><span data-stu-id="ba628-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="ba628-142">다음 이미지는 `<appSettings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 키/값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/env.png)

<span data-ttu-id="ba628-144">참고: 환경 변수의 변경 내용을 확인 하려면 Visual Studio를 종료 하 고 다시 시작 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="ba628-145">접두사 처리</span><span class="sxs-lookup"><span data-stu-id="ba628-145">Prefix handling</span></span>

<span data-ttu-id="ba628-146">키 접두사는 다음과 같은 경우 키 설정을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="ba628-147">.NET Framework 구성은 복잡 하 고 중첩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="ba628-148">외부 키/값 원본은 일반적으로 기본 이며 본질적으로 플랫입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="ba628-149">예를 들어 환경 변수는 중첩 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="ba628-150">다음 방법 중 하나를 사용 하 여 `<appSettings/>` 환경 변수를 통해 및를 구성에 삽입할 수 `<connectionStrings/>` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="ba628-151">`EnvironmentConfigBuilder`기본 모드의와 `Strict` 구성 파일에 적절 한 키 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="ba628-152">위의 코드와 태그는이 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="ba628-153">이 방법을 사용 하면와 모두에 동일한 이름의 키를 사용할 수 **없습니다** `<appSettings/>` `<connectionStrings/>` .</span><span class="sxs-lookup"><span data-stu-id="ba628-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="ba628-154">모드에서는 두 개의를 `EnvironmentConfigBuilder` `Greedy` 고유 접두사와 함께 사용 `stripPrefix` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="ba628-155">이 접근 방식을 사용 하 여 앱은 `<appSettings/>` `<connectionStrings/>` 구성 파일을 업데이트할 필요 없이 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="ba628-156">다음 섹션인 [stripPrefix](#stripprefix)는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="ba628-157">`EnvironmentConfigBuilder` `Greedy` 서로 다른 접두사를 사용 하 여 모드에서 두 s를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="ba628-158">이 방법에서는 키 이름이 접두사와 달라 야 하므로 중복 키 이름을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="ba628-159">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ba628-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="ba628-160">위의 태그를 사용 하 여 동일한 플랫 키/값 소스를 사용 하 여 두 개의 다른 섹션에 대 한 구성을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="ba628-161">다음 이미지는 `<appSettings/>` `<connectionStrings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 및 키/값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/prefix.png)

<span data-ttu-id="ba628-163">다음 코드는 `<appSettings/>` `<connectionStrings/>` 이전 *web.config* 파일에 포함 된 및 키/값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="ba628-164">위의 코드에서는 속성 값을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="ba628-165">환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="ba628-166">환경 변수의 값입니다 (설정 된 경우).</span><span class="sxs-lookup"><span data-stu-id="ba628-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="ba628-167">예를 들어 이전 *web.config* 파일, 이전 환경 편집기 이미지의 키/값, 이전 코드를 사용 하는 경우 다음 값이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="ba628-168">키</span><span class="sxs-lookup"><span data-stu-id="ba628-168">Key</span></span>              | <span data-ttu-id="ba628-169">값</span><span class="sxs-lookup"><span data-stu-id="ba628-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="ba628-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="ba628-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="ba628-171">Env 변수에서 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="ba628-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="ba628-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="ba628-172">AppSetting_default</span></span>            | <span data-ttu-id="ba628-173">Env의 AppSetting_default 값</span><span class="sxs-lookup"><span data-stu-id="ba628-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="ba628-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="ba628-174">ConnStr_default</span></span>         | <span data-ttu-id="ba628-175">Env에서 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="ba628-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="ba628-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="ba628-176">stripPrefix</span></span>

<span data-ttu-id="ba628-177">`stripPrefix`: 부울, 기본값은 `false` 입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="ba628-178">이전 XML 태그는 응용 프로그램 설정을 연결 문자열에서 분리 하지만 *web.config* 파일의 모든 키가 지정 된 접두사를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="ba628-179">예를 들어 접두사는 `AppSetting` `ServiceID` 키 ("AppSetting_ServiceID")에 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="ba628-180">에서 `stripPrefix` 접두사는 *web.config* 파일에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="ba628-181">구성 작성기 원본 (예: 환경)에는 접두사가 필요 합니다. 대부분의 개발자가를 사용 하 게 될 것으로 예상 `stripPrefix` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="ba628-182">응용 프로그램은 일반적으로 접두사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="ba628-183">다음 *web.config* 는 접두사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="ba628-184">위의 *web.config* 파일에서 `default` 키는 및에 모두 `<appSettings/>` `<connectionStrings/>` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="ba628-185">다음 이미지는 `<appSettings/>` `<connectionStrings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 및 키/값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/prefix.png)

<span data-ttu-id="ba628-187">다음 코드는 `<appSettings/>` `<connectionStrings/>` 이전 *web.config* 파일에 포함 된 및 키/값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="ba628-188">위의 코드에서는 속성 값을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="ba628-189">환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="ba628-190">환경 변수의 값입니다 (설정 된 경우).</span><span class="sxs-lookup"><span data-stu-id="ba628-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="ba628-191">예를 들어 이전 *web.config* 파일, 이전 환경 편집기 이미지의 키/값, 이전 코드를 사용 하는 경우 다음 값이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="ba628-192">키</span><span class="sxs-lookup"><span data-stu-id="ba628-192">Key</span></span>              | <span data-ttu-id="ba628-193">값</span><span class="sxs-lookup"><span data-stu-id="ba628-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="ba628-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="ba628-194">ServiceID</span></span>           | <span data-ttu-id="ba628-195">Env 변수에서 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="ba628-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="ba628-196">기본값</span><span class="sxs-lookup"><span data-stu-id="ba628-196">default</span></span>            | <span data-ttu-id="ba628-197">Env의 AppSetting_default 값</span><span class="sxs-lookup"><span data-stu-id="ba628-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="ba628-198">기본값</span><span class="sxs-lookup"><span data-stu-id="ba628-198">default</span></span>         | <span data-ttu-id="ba628-199">Env에서 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="ba628-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="ba628-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="ba628-200">tokenPattern</span></span>

<span data-ttu-id="ba628-201">`tokenPattern`: 문자열, 기본값:`@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="ba628-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="ba628-202">`Expand`작성기의 동작은 원시 XML에서 처럼 보이는 토큰을 검색 합니다 `${token}` .</span><span class="sxs-lookup"><span data-stu-id="ba628-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="ba628-203">검색은 기본 정규식을 사용 하 여 수행 됩니다 `@"\$\{(\w+)\}"` .</span><span class="sxs-lookup"><span data-stu-id="ba628-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="ba628-204">와 일치 하는 문자 집합은 `\w` XML 보다 엄격 하 고 많은 구성 소스에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="ba628-205">`tokenPattern`토큰 이름에 필요한 것 보다 많은 문자를 사용 `@"\$\{(\w+)\}"` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="ba628-206">`tokenPattern`문자열</span><span class="sxs-lookup"><span data-stu-id="ba628-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="ba628-207">개발자가 토큰 일치에 사용 되는 regex를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="ba628-208">잘 구성 된 위험한 regex 인지 확인 하기 위해 유효성 검사가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="ba628-209">캡처 그룹을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-209">It must contain a capture group.</span></span> <span data-ttu-id="ba628-210">전체 regex는 전체 토큰과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="ba628-211">첫 번째 캡처는 구성 소스에서 조회할 토큰 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="ba628-212">Microsoft.Configuration.ConfigurationBuilders의 구성 빌더</span><span class="sxs-lookup"><span data-stu-id="ba628-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="ba628-213">환경 Configbuilder</span><span class="sxs-lookup"><span data-stu-id="ba628-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="ba628-214">환경 [Configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="ba628-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="ba628-215">는 가장 간단한 구성 빌더입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="ba628-216">환경에서 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-216">Reads values from the environment.</span></span>
* <span data-ttu-id="ba628-217">에는 추가 구성 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="ba628-218">`name`특성 값은 임의입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="ba628-219">**참고:** Windows 컨테이너 환경에서 런타임에 설정 된 변수는 EntryPoint 프로세스 환경에만 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="ba628-220">서비스 또는 비 EntryPoint 프로세스로 실행 되는 앱은 컨테이너의 메커니즘을 통해 다른 방식으로 삽입 되지 않는 한 이러한 변수를 선택 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="ba628-221">[IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)기반 컨테이너의 경우 현재 버전의 [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) 는 *DefaultAppPool* 에서만이를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="ba628-222">다른 Windows 기반 컨테이너 변형은 진입점이 아닌 프로세스에 대 한 자체 삽입 메커니즘을 개발 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="ba628-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="ba628-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="ba628-224">소스 코드에는 암호, 중요 한 연결 문자열 또는 기타 중요 한 데이터를 저장 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ba628-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="ba628-225">프로덕션 암호는 개발 또는 테스트에 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="ba628-226">이 구성 작성기는 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)와 유사한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="ba628-227">.NET Framework 프로젝트에서 [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) 를 사용할 수 있지만 비밀 파일을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="ba628-228">또는 `UserSecretsId` 프로젝트 파일에서 속성을 정의 하 고 읽을 수 있도록 올바른 위치에 원시 비밀 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="ba628-229">외부 종속성을 프로젝트 외부로 유지 하기 위해 비밀 파일은 XML 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="ba628-230">XML 서식 지정은 구현 세부 정보 이며,이 형식은에 의존해 서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="ba628-231">.NET Core 프로젝트를 사용 하 여 파일 *에secrets.js* 를 공유 해야 하는 경우 [SimpleJsonConfigBuilder](#simplejsonconfigbuilder)를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="ba628-232">`SimpleJsonConfigBuilder`또한 .Net Core의 형식은 변경 될 수 있는 구현 세부 정보로 간주 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="ba628-233">구성 특성 `UserSecretsConfigBuilder` :</span><span class="sxs-lookup"><span data-stu-id="ba628-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="ba628-234">`userSecretsId`-XML 암호 파일을 식별 하는 데 선호 되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="ba628-235">이는 프로젝트 속성을 사용 하 여이 식별자를 저장 하는 .NET Core와 유사 하 게 작동 `UserSecretsId` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="ba628-236">문자열은 고유 해야 하며 GUID가 아니어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="ba628-237">이 특성을 사용 하 여 `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` 이 식별자에 속하는 비밀 파일에 대해 잘 알려진 로컬 위치 ()를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="ba628-238">`userSecretsFile`-암호를 포함 하는 파일을 지정 하는 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="ba628-239">`~`문자는 응용 프로그램 루트를 참조 하는 시작 부분에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="ba628-240">이 특성 또는 `userSecretsId` 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="ba628-241">둘 다 지정 하면가 `userSecretsFile` 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="ba628-242">`optional`: boolean, default value `true` -암호 파일을 찾을 수 없는 경우 예외를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="ba628-243">`name`특성 값은 임의입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="ba628-244">비밀 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="ba628-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="ba628-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="ba628-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) 는 [Azure Key Vault](/azure/key-vault/key-vault-whatis)에 저장 된 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="ba628-247">`vaultName`필요 합니다 (자격 증명 모음의 이름 또는 자격 증명 모음에 대 한 URI).</span><span class="sxs-lookup"><span data-stu-id="ba628-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="ba628-248">다른 특성은 연결할 자격 증명 모음에 대 한 제어를 허용 하지만 응용 프로그램이에서 작동 하는 환경에서 실행 되 고 있지 않은 경우에만 필요 합니다 `Microsoft.Azure.Services.AppAuthentication` .</span><span class="sxs-lookup"><span data-stu-id="ba628-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="ba628-249">Azure 서비스 인증 라이브러리는 가능 하면 실행 환경에서 연결 정보를 자동으로 선택 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="ba628-250">연결 문자열을 제공 하 여 자동으로 연결 정보를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="ba628-251">`vaultName`-이 `uri` 제공 되지 않은 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="ba628-252">키/값 쌍을 읽을 Azure 구독의 자격 증명 모음 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="ba628-253">`connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) 에서 사용할 수 있는 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="ba628-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="ba628-254">`uri`-지정 된 값을 사용 하 여 다른 Key Vault 공급자에 연결 `uri` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="ba628-255">지정 하지 않으면 Azure ( `vaultName` )는 자격 증명 모음 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="ba628-256">`version`-Azure Key Vault는 암호에 대 한 버전 관리 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="ba628-257">을 `version` 지정 하면 작성기는이 버전과 일치 하는 암호만 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="ba628-258">`preloadSecretNames`-기본적으로이 빌더는 초기화 될 때 key vault의 **모든** 키 이름을 querys 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="ba628-259">모든 키 값을 읽지 않으려면이 특성을로 설정 `false` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="ba628-260">이를로 설정 `false` 하면 한 번에 하나씩 비밀을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="ba628-261">자격 증명 모음에서 "Get" 액세스를 허용 하지만 "목록" 액세스를 허용 하지 않는 경우 암호를 한 번에 하나씩 읽는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="ba628-262">**참고:** `Greedy`모드를 사용 하 `preloadSecretNames` 는 경우은 `true` (기본값) 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="ba628-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="ba628-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="ba628-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 는 디렉터리의 파일을 값의 원본으로 사용 하는 기본 구성 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="ba628-265">파일 이름은 키 이며 콘텐츠는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="ba628-266">이 구성 작성기는 오케스트레이션 컨테이너 환경에서 실행할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="ba628-267">Docker Swarm 및 Kubernetes와 같은 시스템 `secrets` 은이 파일을 기준으로이 키로 해당 오케스트레이션 windows 컨테이너를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="ba628-268">특성 정보:</span><span class="sxs-lookup"><span data-stu-id="ba628-268">Attribute details:</span></span>

* <span data-ttu-id="ba628-269">`directoryPath` - 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-269">`directoryPath` - Required.</span></span> <span data-ttu-id="ba628-270">값을 찾을 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="ba628-271">Windows용 Docker 암호는 기본적으로 *C:\ProgramData\Docker\secrets* 디렉터리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="ba628-272">`ignorePrefix`-이 접두사로 시작 하는 파일은 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="ba628-273">기본값은 “무시”입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="ba628-274">`keyDelimiter`-기본값은 `null` 입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="ba628-275">지정 된 경우 구성 빌더는 디렉터리의 여러 수준을 트래버스하 고이 구분 기호를 사용 하 여 키 이름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="ba628-276">이 값이 이면 `null` 구성 빌더는 디렉터리의 최상위 수준만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="ba628-277">`optional`-기본값은 `false` 입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="ba628-278">원본 디렉터리가 없는 경우 구성 작성기에서 오류를 발생 시켜야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="ba628-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="ba628-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="ba628-280">소스 코드에는 암호, 중요 한 연결 문자열 또는 기타 중요 한 데이터를 저장 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ba628-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="ba628-281">프로덕션 암호는 개발 또는 테스트에 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="ba628-282">.NET Core 프로젝트는 일반적으로 구성에 JSON 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="ba628-283">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder를 사용 하면 .NET Core JSON 파일을 .NET Framework에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="ba628-284">이 구성 작성기는 플랫 키/값 원본에서 .NET Framework 구성의 특정 키/값 영역으로의 기본 매핑을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="ba628-285">이 구성 작성기는 계층적 구성을 제공 **하지** 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="ba628-286">JSON 지원 파일은 복합 계층적 개체가 아닌 사전과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="ba628-287">다중 수준 계층 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="ba628-288">이 공급자 `flatten` 는를 구분 기호로 사용 하 여 각 수준에 속성 이름을 추가 하 여 깊이 `:` 입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="ba628-289">특성 정보:</span><span class="sxs-lookup"><span data-stu-id="ba628-289">Attribute details:</span></span>

* <span data-ttu-id="ba628-290">`jsonFile` - 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-290">`jsonFile` - Required.</span></span> <span data-ttu-id="ba628-291">읽을 JSON 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="ba628-292">`~`문자는 앱 루트를 참조 하는 시작 부분에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="ba628-293">`optional`-부울, 기본값은 `true` 입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="ba628-294">JSON 파일을 찾을 수 없는 경우 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="ba628-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="ba628-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="ba628-296">기본값은 `Flat`입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-296">`Flat` is the default.</span></span> <span data-ttu-id="ba628-297">`jsonMode`가 이면 `Flat` JSON 파일은 단일 플랫 키/값 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="ba628-298">`EnvironmentConfigBuilder`및는 `AzureKeyVaultConfigBuilder` 단일 플랫 키/값 원본 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="ba628-299">`SimpleJsonConfigBuilder`가 모드로 구성 된 경우 `Sectional` :</span><span class="sxs-lookup"><span data-stu-id="ba628-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="ba628-300">JSON 파일은 개념적으로 최상위 수준 에서만 여러 사전으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="ba628-301">각 사전은 연결 된 최상위 속성 이름과 일치 하는 구성 섹션에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="ba628-302">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ba628-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a><span data-ttu-id="ba628-303">구성 작성기 순서</span><span class="sxs-lookup"><span data-stu-id="ba628-303">Configuration builders order</span></span>

<span data-ttu-id="ba628-304">[Aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub 리포지토리에서 [Configurationbuilders 실행 순서](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) 를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-304">See [ConfigurationBuilders Order of Execution](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) in the [aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub repository.</span></span>

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="ba628-305">사용자 지정 키/값 구성 작성기 구현</span><span class="sxs-lookup"><span data-stu-id="ba628-305">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="ba628-306">구성 빌더가 요구를 충족 하지 않는 경우 사용자 지정 항목을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-306">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="ba628-307">`KeyValueConfigBuilder`기본 클래스는 대체 모드와 대부분의 접두사 문제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-307">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="ba628-308">구현 프로젝트에는 다음만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-308">An implementing project need only:</span></span>

* <span data-ttu-id="ba628-309">기본 클래스에서 상속 하 고 및을 통해 키/값 쌍의 기본 소스를 구현 합니다 `GetValue` `GetAllValues` .</span><span class="sxs-lookup"><span data-stu-id="ba628-309">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="ba628-310">프로젝트에 [urationBuildersMicrosoft.Configuration.Config](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-310">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="ba628-311">`KeyValueConfigBuilder`기본 클래스는 키/값 구성 작성기에서 많은 작업과 일관 된 동작을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba628-311">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba628-312">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ba628-312">Additional resources</span></span>

* [<span data-ttu-id="ba628-313">구성 빌더 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="ba628-313">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="ba628-314">.NET을 사용 하 여 Azure Key Vault에 대 한 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="ba628-314">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
