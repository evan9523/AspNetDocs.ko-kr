---
title: ASP.NET Core에서 용도 문자열
author: rick-anderson
description: 용도 문자열에서 ASP.NET Core 데이터 보호 Api를 사용 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/purpose-strings
ms.openlocfilehash: 4c85423f8de7e4b784ae1bb304a884541df251b6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051290"
---
# <a name="purpose-strings-in-aspnet-core"></a><span data-ttu-id="1ad19-103">ASP.NET Core에서 용도 문자열</span><span class="sxs-lookup"><span data-stu-id="1ad19-103">Purpose strings in ASP.NET Core</span></span>

<a name="data-protection-consumer-apis-purposes"></a>

<span data-ttu-id="1ad19-104">`IDataProtectionProvider` 를 사용하는 구성 요소는 `CreateProtector` 메서드를 호출할 때 반드시 고유한 *purposes* 매개 변수를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-104">Components which consume `IDataProtectionProvider` must pass a unique *purposes* parameter to the `CreateProtector` method.</span></span> <span data-ttu-id="1ad19-105">이 *purposes* 매개 변수는 내부적으로 데이터 보호 시스템의 보안에 포함되어 루트 암호화 키가 동일한 경우에도 암호화 소비자들을 서로 격리할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-105">The purposes *parameter* is inherent to the security of the data protection system, as it provides isolation between cryptographic consumers, even if the root cryptographic keys are the same.</span></span>

<span data-ttu-id="1ad19-106">소비자가 용도를 지정하면 루트 암호화 키와 용도 문자열이 함께 적용되어 해당 소비자에 고유한 하위 암호화 키가 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-106">When a consumer specifies a purpose, the purpose string is used along with the root cryptographic keys to derive cryptographic subkeys unique to that consumer.</span></span> <span data-ttu-id="1ad19-107">이로 인해서 해당 소비자와 응용 프로그램 내의 모든 다른 암호화 소비자가 서로 격리되며, 해당 소비자의 페이로드를 다른 구성 요소가 읽을 수도, 다른 구성 요소의 페이로드를 해당 소비자가 읽을 수도 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-107">This isolates the consumer from all other cryptographic consumers in the application: no other component can read its payloads, and it cannot read any other component's payloads.</span></span> <span data-ttu-id="1ad19-108">또한 이러한 격리는 구성 요소에 대한 전 범주의 공격을 불가능하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-108">This isolation also renders infeasible entire categories of attack against the component.</span></span>

![목적은 다이어그램 예제](purpose-strings/_static/purposes.png)

<span data-ttu-id="1ad19-110">이 다이어그램에서 `IDataProtector` 의 인스턴스 A 및 B는 서로 상대방의 페이로드를 **읽을 수 없으며**, 자신의 페이로드만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-110">In the diagram above, `IDataProtector` instances A and B **cannot** read each other's payloads, only their own.</span></span>

<span data-ttu-id="1ad19-111">용도 문자열 자체를 암호화할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-111">The purpose string doesn't have to be secret.</span></span> <span data-ttu-id="1ad19-112">정상적으로 동작하는 다른 구성 요소가 사용하는 용도 문자열과 중복되지 않는 유일한 문자열을 지정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-112">It should simply be unique in the sense that no other well-behaved component will ever provide the same purpose string.</span></span>

>[!TIP]
> <span data-ttu-id="1ad19-113">경험적으로 데이터 보호 API를 소비하는 구성 요소의 네임스페이스와 형식 이름을 조합해서 사용하는 것도 좋은 방법입니다. 사실상 이 정보는 중복되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-113">Using the namespace and type name of the component consuming the data protection APIs is a good rule of thumb, as in practice this information will never conflict.</span></span>
>
><span data-ttu-id="1ad19-114">예를 들어, 전달자 토큰의 발급을 담당하는 Contoso 프로젝트의 구성 요소는 용도 문자열로 Contoso.Security.BearerToken을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-114">A Contoso-authored component which is responsible for minting bearer tokens might use Contoso.Security.BearerToken as its purpose string.</span></span> <span data-ttu-id="1ad19-115">혹은 더 개선된 방법으로 Contoso.Security.BearerToken.v1을 용도 문자열로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-115">Or - even better - it might use Contoso.Security.BearerToken.v1 as its purpose string.</span></span> <span data-ttu-id="1ad19-116">이렇게 버전 번호를 추가해 놓으면 이후 버전에서는 용도 문자열로 Contoso.Security.BearerToken.v2 등과 같이 사용할 수 있으므로, 페이로드에 관한한 버전 간에 서로 완벽한 격리를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-116">Appending the version number allows a future version to use Contoso.Security.BearerToken.v2 as its purpose, and the different versions would be completely isolated from one another as far as payloads go.</span></span>

<span data-ttu-id="1ad19-117">`CreateProtector` 메서드의 용도 매개 변수는 문자열 배열 형식이기 때문에, 위의 매개 변수는 대신 `[ "Contoso.Security.BearerToken", "v1" ]` 처럼 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-117">Since the purposes parameter to `CreateProtector` is a string array, the above could've been instead specified as `[ "Contoso.Security.BearerToken", "v1" ]`.</span></span> <span data-ttu-id="1ad19-118">따라서, 이를 활용하면 용도의 계층적 구조를 구성할 수 있으며 데이터 보호 시스템을 사용하는 다중 테넌트(Multi-Tenancy) 시나리오를 고려해 볼 수 있는 여지를 남겨줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-118">This allows establishing a hierarchy of purposes and opens up the possibility of multi-tenancy scenarios with the data protection system.</span></span>

<a name="data-protection-contoso-purpose"></a>

>[!WARNING]
> <span data-ttu-id="1ad19-119">신뢰할 수 없는 사용자의 입력이 구성 요소 용도 체인의 유일한 입력 원본이 될 수 있도록 허용해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-119">Components shouldn't allow untrusted user input to be the sole source of input for the purposes chain.</span></span>
>
><span data-ttu-id="1ad19-120">가령, 보안 메시지의 저장을 담당하는 Contoso.Messaging.SecureMessage라는 구성 요소가 존재한다고 가정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-120">For example, consider a component Contoso.Messaging.SecureMessage which is responsible for storing secure messages.</span></span> <span data-ttu-id="1ad19-121">만약, 이 보안 메시징 구성 요소가 `CreateProtector([ username ])` 와 같이 메서드를 호출하도록 작성되어 있다면, 악의적인 사용자가 "Contoso.Security.BearerToken"이라는 사용자 이름의 계정을 생성해서 `CreateProtector([ "Contoso.Security.BearerToken" ])` 와 같이 메서드를 호출하는 구성 요소를 얻으려고 시도할 수 있으며, 이는 의도하지 않게 인증 토큰으로 인식할 수도 있는 페이로드를 보안 메시징 시스템이 발급할 수도 있는 결과를 초래하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-121">If the secure messaging component were to call `CreateProtector([ username ])`, then a malicious user might create an account with username "Contoso.Security.BearerToken" in an attempt to get the component to call `CreateProtector([ "Contoso.Security.BearerToken" ])`, thus inadvertently causing the secure messaging system to mint payloads that could be perceived as authentication tokens.</span></span>
>
><span data-ttu-id="1ad19-122">따라서 이 메시징 구성 요소에 적합한 용도 체인은, 적절한 격리를 제공할 수 있는 `CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])` 입니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-122">A better purposes chain for the messaging component would be `CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])`, which provides proper isolation.</span></span>

<span data-ttu-id="1ad19-123">\`\`IDataProtectionProvider`, `IDataProtector\` 및 용도에 의해서 제공되는 격리 및 동작은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-123">The isolation provided by and behaviors of `IDataProtectionProvider`, `IDataProtector`, and purposes are as follows:</span></span>

* <span data-ttu-id="1ad19-124">특정 `IDataProtectionProvider` 개체의 `CreateProtector` 메서드는 `IDataProtector` 개체를 생성하는 `IDataProtectionProvider` 개체와 메서드에 전달된 용도 매개 변수 양쪽 모두와 고유하게 연결된 `IDataProtector` 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-124">For a given `IDataProtectionProvider` object, the `CreateProtector` method will create an `IDataProtector` object uniquely tied to both the `IDataProtectionProvider` object which created it and the purposes parameter which was passed into the method.</span></span>

* <span data-ttu-id="1ad19-125">용도 매개 변수에 null을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-125">The purpose parameter must not be null.</span></span> <span data-ttu-id="1ad19-126">(용도를 배열로 지정할 경우에는 배열의 길이가 0이 될 수 없으며 배열의 모든 요소가 null이 아니어야 합니다.) 기술적으로 용도에 빈 문자열을 지정할 수는 있지만 권장하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-126">(If purposes is specified as an array, this means that the array must not be of zero length and all elements of the array must be non-null.) An empty string purpose is technically allowed but is discouraged.</span></span>

* <span data-ttu-id="1ad19-127">두 개 요소로 구성된 용도 인자는 동일한 문자열(서수 비교자가 사용됨)이 동일한 순서로 담겨진 경우에만 같은 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-127">Two purposes arguments are equivalent if and only if they contain the same strings (using an ordinal comparer) in the same order.</span></span> <span data-ttu-id="1ad19-128">단일 용도 문자열 인자의 경우, 해당 인자를 담고 있는 단일 요소 용도 배열과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-128">A single purpose argument is equivalent to the corresponding single-element purposes array.</span></span>

* <span data-ttu-id="1ad19-129">두 개의 `IDataProtector` 개체는 동일한 용도 매개 변수를 이용해서 동일한 `IDataProtectionProvider` 개체로부터 생성된 경우에만 동일한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-129">Two `IDataProtector` objects are equivalent if and only if they're created from equivalent `IDataProtectionProvider` objects with equivalent purposes parameters.</span></span>

* <span data-ttu-id="1ad19-130">특정 `IDataProtector` 개체에서 `Unprotect(protectedData)` 를 호출할 경우, 동일한 `IDataProtector` 개체에서 `protectedData := Protect(unprotectedData)` 인 경우에만 원본 `unprotectedData` 가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-130">For a given `IDataProtector` object, a call to `Unprotect(protectedData)` will return the original `unprotectedData` if and only if `protectedData := Protect(unprotectedData)` for an equivalent `IDataProtector` object.</span></span>

> [!NOTE]
> <span data-ttu-id="1ad19-131">본문에서는 일부 구성 요소가 다른 구성 요소와 동일한 용도 문자열을 의도적으로 선택하는 경우는 감안하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-131">We're not considering the case where some component intentionally chooses a purpose string which is known to conflict with another component.</span></span> <span data-ttu-id="1ad19-132">기본적으로 이런 구성 요소는 악의적인 구성 요소로 간주되며, 데이터 보호 시스템은 이미 악의적인 코드가 작업자 프로세스 내부에서 실행 중인 경우까지 보안을 보장하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ad19-132">Such a component would essentially be considered malicious, and this system isn't intended to provide security guarantees in the event that malicious code is already running inside of the worker process.</span></span>
