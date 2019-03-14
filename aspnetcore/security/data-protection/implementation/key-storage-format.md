---
title: ASP.NET Core에서 키 저장소 형식
author: rick-anderson
description: ASP.NET Core 데이터 보호 키 저장소 형식 구현 세부 정보에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-format
ms.openlocfilehash: bca19ad001dd20b5d02ae5470f7d928082496037
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044820"
---
# <a name="key-storage-format-in-aspnet-core"></a><span data-ttu-id="fc766-103">ASP.NET Core에서 키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="fc766-103">Key storage format in ASP.NET Core</span></span>

<a name="data-protection-implementation-key-storage-format"></a>

<span data-ttu-id="fc766-104">개체는 XML 표현에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-104">Objects are stored at rest in XML representation.</span></span> <span data-ttu-id="fc766-105">키 저장소에 대 한 기본 디렉터리는 %LOCALAPPDATA%\ASP.NET\DataProtection-Keys\ 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-105">The default directory for key storage is %LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span></span>

## <a name="the-key-element"></a><span data-ttu-id="fc766-106">\<키 > 요소</span><span class="sxs-lookup"><span data-stu-id="fc766-106">The \<key> element</span></span>

<span data-ttu-id="fc766-107">키를 키 저장소의 최상위 개체로 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-107">Keys exist as top-level objects in the key repository.</span></span> <span data-ttu-id="fc766-108">규칙에 따라 키 파일을 갖습니다 **키-{guid}.xml**여기서 {guid}는 키의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-108">By convention keys have the filename **key-{guid}.xml**, where {guid} is the id of the key.</span></span> <span data-ttu-id="fc766-109">이러한 각 파일에는 단일 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-109">Each such file contains a single key.</span></span> <span data-ttu-id="fc766-110">파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-110">The format of the file is as follows.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<key id="80732141-ec8f-4b80-af9c-c4d2d1ff8901" version="1">
  <creationDate>2015-03-19T23:32:02.3949887Z</creationDate>
  <activationDate>2015-03-19T23:32:02.3839429Z</activationDate>
  <expirationDate>2015-06-17T23:32:02.3839429Z</expirationDate>
  <descriptor deserializerType="{deserializerType}">
    <descriptor>
      <encryption algorithm="AES_256_CBC" />
      <validation algorithm="HMACSHA256" />
      <enc:encryptedSecret decryptorType="{decryptorType}" xmlns:enc="...">
        <encryptedKey>
          <!-- This key is encrypted with Windows DPAPI. -->
          <value>AQAAANCM...8/zeP8lcwAg==</value>
        </encryptedKey>
      </enc:encryptedSecret>
    </descriptor>
  </descriptor>
</key>
```

<span data-ttu-id="fc766-111">\<키 > 요소는 다음 특성과 자식 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-111">The \<key> element contains the following attributes and child elements:</span></span>

* <span data-ttu-id="fc766-112">키 id입니다. 이 값은 정식으로; 처리 파일 이름이 휴먼 가독성을 높이기 위해 능률이 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-112">The key id. This value is treated as authoritative; the filename is simply a nicety for human readability.</span></span>

* <span data-ttu-id="fc766-113">버전을 \<키 > 요소를 1로 현재 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-113">The version of the \<key> element, currently fixed at 1.</span></span>

* <span data-ttu-id="fc766-114">키의 생성, 활성화 및 만료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-114">The key's creation, activation, and expiration dates.</span></span>

* <span data-ttu-id="fc766-115">\<설명자 >이 키에 포함 된 인증 된 암호화 구현에 대 한 정보를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-115">A \<descriptor> element, which contains information on the authenticated encryption implementation contained within this key.</span></span>

<span data-ttu-id="fc766-116">위의 예제에서는 키의 id가 {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, 만들어지고 2015 년 3 월 19 일에서 활성화 된 있고 90 일 동안 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-116">In the above example, the key's id is {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, it was created and activated on March 19, 2015, and it has a lifetime of 90 days.</span></span> <span data-ttu-id="fc766-117">(경우에 따라 활성화 날짜 약간 있을 수 있으며이 예제와 같이 만든 날짜 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-117">(Occasionally the activation date might be slightly before the creation date as in this example.</span></span> <span data-ttu-id="fc766-118">이것이 Api 작동 하 고는 실제로 치명적이 지는 방법에 nit 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="fc766-118">This is due to a nit in how the APIs work and is harmless in practice.)</span></span>

## <a name="the-descriptor-element"></a><span data-ttu-id="fc766-119">\<설명자 > 요소</span><span class="sxs-lookup"><span data-stu-id="fc766-119">The \<descriptor> element</span></span>

<span data-ttu-id="fc766-120">외부 \<설명자 > IAuthenticatedEncryptorDescriptorDeserializer를 구현 하는 형식의 정규화 된 어셈블리 이름를 특성 deserializerType 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-120">The outer \<descriptor> element contains an attribute deserializerType, which is the assembly-qualified name of a type which implements IAuthenticatedEncryptorDescriptorDeserializer.</span></span> <span data-ttu-id="fc766-121">이 형식은 내부를 읽는 역할을 하 \<설명자 > 요소 내에 포함 된 정보를 구문 분석 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-121">This type is responsible for reading the inner \<descriptor> element and for parsing the information contained within.</span></span>

<span data-ttu-id="fc766-122">특정 형식의 \<설명자 > 요소 키를 캡슐화 하는 인증 된 암호기 구현에 달려 및이 대해 약간 다른 형식을 필요로 하는 각 역직렬 변환기가 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-122">The particular format of the \<descriptor> element depends on the authenticated encryptor implementation encapsulated by the key, and each deserializer type expects a slightly different format for this.</span></span> <span data-ttu-id="fc766-123">일반적으로 하지만,이 요소를 포함 합니다 알고리즘 정보 (이름, 형식, Oid, 또는 이와 유사한) 및 비밀 키 자료입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-123">In general, though, this element will contain algorithmic information (names, types, OIDs, or similar) and secret key material.</span></span> <span data-ttu-id="fc766-124">위의 예에서 설명자는이 키는 AES-256-CBC 암호화 + HMACSHA256 유효성 검사를 래핑하는 것을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-124">In the above example, the descriptor specifies that this key wraps AES-256-CBC encryption + HMACSHA256 validation.</span></span>

## <a name="the-encryptedsecret-element"></a><span data-ttu-id="fc766-125">\<encryptedSecret > 요소</span><span class="sxs-lookup"><span data-stu-id="fc766-125">The \<encryptedSecret> element</span></span>

<span data-ttu-id="fc766-126">**&lt;encryptedSecret&gt;** 비밀 키 자료의 암호화 된 폼을 포함 하는 요소 수 있을 경우 [미사용 비밀 암호화를 사용 하](xref:security/data-protection/implementation/key-encryption-at-rest)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-126">An **&lt;encryptedSecret&gt;** element which contains the encrypted form of the secret key material may be present if [encryption of secrets at rest is enabled](xref:security/data-protection/implementation/key-encryption-at-rest).</span></span> <span data-ttu-id="fc766-127">특성 `decryptorType` 구현 하는 형식의 어셈블리 정규화 된 이름 [IXmlDecryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmldecryptor)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-127">The attribute `decryptorType` is the assembly-qualified name of a type which implements [IXmlDecryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmldecryptor).</span></span> <span data-ttu-id="fc766-128">이 형식은 내부 읽기 담당 **&lt;encryptedKey&gt;** 요소 및 복구를 원래의 일반 텍스트로 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-128">This type is responsible for reading the inner **&lt;encryptedKey&gt;** element and decrypting it to recover the original plaintext.</span></span>

<span data-ttu-id="fc766-129">와 마찬가지로 \<설명자 >, 특정 형식의 <encryptedSecret> 요소에서 사용 하 여 미사용 암호화 메커니즘에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-129">As with \<descriptor>, the particular format of the <encryptedSecret> element depends on the at-rest encryption mechanism in use.</span></span> <span data-ttu-id="fc766-130">위의 예제에서 주석을 마다 Windows DPAPI를 사용 하 여 마스터 키를 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-130">In the above example, the master key is encrypted using Windows DPAPI per the comment.</span></span>

## <a name="the-revocation-element"></a><span data-ttu-id="fc766-131">\<해지 > 요소</span><span class="sxs-lookup"><span data-stu-id="fc766-131">The \<revocation> element</span></span>

<span data-ttu-id="fc766-132">해지 키 저장소의 최상위 개체로 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-132">Revocations exist as top-level objects in the key repository.</span></span> <span data-ttu-id="fc766-133">규칙에 따라 해지는 파일 이름을 가진 **해지-{timestamp}.xml** (에 대 한 특정 날짜 이전의 모든 키를 취소) 또는 **해지-{guid}.xml** (에 대 한 특정 키를 해지).</span><span class="sxs-lookup"><span data-stu-id="fc766-133">By convention revocations have the filename **revocation-{timestamp}.xml** (for revoking all keys before a specific date) or **revocation-{guid}.xml** (for revoking a specific key).</span></span> <span data-ttu-id="fc766-134">각 파일에 단일 \<해지 > 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-134">Each file contains a single \<revocation> element.</span></span>

<span data-ttu-id="fc766-135">개별 키 해지, 파일 내용이 됩니다 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-135">For revocations of individual keys, the file contents will be as below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T22:45:30.2616742Z</revocationDate>
  <key id="eb4fc299-8808-409d-8a34-23fc83d026c9" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="fc766-136">이 경우 지정된 된 키가 해지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-136">In this case, only the specified key is revoked.</span></span> <span data-ttu-id="fc766-137">그러나 키 id가 "\*", 에서처럼는 아래 예제에서는 생성 날짜가 지정 된 해지 날짜 전에 해당 하는 모든 키가 해지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-137">If the key id is "\*", however, as in the below example, all keys whose creation date is prior to the specified revocation date are revoked.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T15:45:45.7366491-07:00</revocationDate>
  <!-- All keys created before the revocation date are revoked. -->
  <key id="*" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="fc766-138">\<이유 > 요소는 시스템에서 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-138">The \<reason> element is never read by the system.</span></span> <span data-ttu-id="fc766-139">단순히 해지 하는 사람이 읽을 수 있는 이유를 저장 하는 편리한 장소는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc766-139">It's simply a convenient place to store a human-readable reason for revocation.</span></span>
