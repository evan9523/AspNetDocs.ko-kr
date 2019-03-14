---
title: ASP.NET Core에서 임시 데이터 보호 공급자
author: rick-anderson
description: ASP.NET Core 삭제 되는 데이터 보호 공급자의 구현 세부 사항에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: e4b0014ab3bdbf90b91383e8a33102f94faa8153
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040570"
---
# <a name="ephemeral-data-protection-providers-in-aspnet-core"></a>ASP.NET Core에서 임시 데이터 보호 공급자

<a name="data-protection-implementation-key-storage-ephemeral"></a>

응용 프로그램을 throwaway 해야 하는 시나리오가 있습니다 `IDataProtectionProvider`합니다. 예를 들어, 개발자 일회용 콘솔 응용 프로그램에서 실험만 될 수 있습니다 또는 응용 프로그램 자체는 일시적 (스크립팅된은 또는 단위 테스트 프로젝트). 이러한 시나리오를 지원 합니다 [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) 패키지 형식을 포함 `EphemeralDataProtectionProvider`합니다. 이 형식은의 기본 구현을 제공 `IDataProtectionProvider` 인 키 저장소만 메모리를 보유 하 고 백업 저장소에 기록 되지 않습니다.

각 인스턴스의 `EphemeralDataProtectionProvider` 자체 고유 마스터 키를 사용 합니다. 따라서 경우는 `IDataProtector` 에서 시작 하는 `EphemeralDataProtectionProvider` 보호 된 페이로드를 생성 해당에 의해 해당 페이로드를 보호만 있습니다 `IDataProtector` (동일한 [용도](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes) 체인) 동시 루 팅 `EphemeralDataProtectionProvider` 인스턴스입니다.

다음 샘플을 인스턴스화하는 `EphemeralDataProtectionProvider` 보호 및 데이터를 보호 해제 하는 데 사용 하 합니다.

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
