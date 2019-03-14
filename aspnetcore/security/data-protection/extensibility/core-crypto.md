---
title: ASP.NET Core에서 core 암호화 확장성
author: rick-anderson
description: IAuthenticatedEncryptor, IAuthenticatedEncryptorDescriptor, IAuthenticatedEncryptorDescriptorDeserializer, 및 최상위 factory에 알아봅니다.
ms.author: riande
ms.date: 8/11/2017
uid: security/data-protection/extensibility/core-crypto
ms.openlocfilehash: 47432cfefe0a52c9f815d717f7269ec68fdb6af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036180"
---
# <a name="core-cryptography-extensibility-in-aspnet-core"></a><span data-ttu-id="774ba-103">ASP.NET Core에서 core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="774ba-103">Core cryptography extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-core-crypto"></a>

>[!WARNING]
> <span data-ttu-id="774ba-104">다음 인터페이스 중 하나를 구현 하는 형식은 스레드로부터 안전 해야 합니다. 여러 호출자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptor"></a>

## <a name="iauthenticatedencryptor"></a><span data-ttu-id="774ba-105">IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="774ba-105">IAuthenticatedEncryptor</span></span>

<span data-ttu-id="774ba-106">합니다 **IAuthenticatedEncryptor** 인터페이스는 암호화 하위 시스템의 기본 빌딩 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-106">The **IAuthenticatedEncryptor** interface is the basic building block of the cryptographic subsystem.</span></span> <span data-ttu-id="774ba-107">일반적으로 키 당 하나의 IAuthenticatedEncryptor 되며 모든 암호화 키 자료 및 암호화 작업을 수행 하는 데 필요한 정보를 알고리즘 IAuthenticatedEncryptor 인스턴스를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-107">There's generally one IAuthenticatedEncryptor per key, and the IAuthenticatedEncryptor instance wraps all cryptographic key material and algorithmic information necessary to perform cryptographic operations.</span></span>

<span data-ttu-id="774ba-108">해당 이름에서 알 수 있듯이, 형식이 암호화 및 암호 해독에 대 한 인증 된 서비스를 제공 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-108">As its name suggests, the type is responsible for providing authenticated encryption and decryption services.</span></span> <span data-ttu-id="774ba-109">다음 두 가지 Api를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-109">It exposes the following two APIs.</span></span>

* <span data-ttu-id="774ba-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="774ba-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

* <span data-ttu-id="774ba-111">암호화 (ArraySegment<byte> 일반 텍스트, ArraySegment<byte> additionalAuthenticatedData): byte</span><span class="sxs-lookup"><span data-stu-id="774ba-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

<span data-ttu-id="774ba-112">Encrypt 메서드는 일반 텍스트 암호화 및 인증 태그를 포함 하는 blob를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-112">The Encrypt method returns a blob that includes the enciphered plaintext and an authentication tag.</span></span> <span data-ttu-id="774ba-113">인증 태그 자체는 AAD 최종 페이로드에서 복구할 수 없는 필요 하지만 추가 인증된 데이터 (AAD) 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-113">The authentication tag must encompass the additional authenticated data (AAD), though the AAD itself need not be recoverable from the final payload.</span></span> <span data-ttu-id="774ba-114">암호 해독 메서드 인증 태그의 유효성을 검사 하 고 해독된 페이로드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-114">The Decrypt method validates the authentication tag and returns the deciphered payload.</span></span> <span data-ttu-id="774ba-115">ArgumentNullException 제외한과 유사한 모든 오류는 CryptographicException를 homogenized 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-115">All failures (except ArgumentNullException and similar) should be homogenized to CryptographicException.</span></span>

> [!NOTE]
> <span data-ttu-id="774ba-116">IAuthenticatedEncryptor 인스턴스 자체가 키 자료를 포함 하도록 실제로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-116">The IAuthenticatedEncryptor instance itself doesn't actually need to contain the key material.</span></span> <span data-ttu-id="774ba-117">예를 들어, 구현 모든 작업에 대 한 HSM을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-117">For example, the implementation could delegate to an HSM for all operations.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptorfactory"></a>
<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="how-to-create-an-iauthenticatedencryptor"></a><span data-ttu-id="774ba-118">IAuthenticatedEncryptor를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="774ba-118">How to create an IAuthenticatedEncryptor</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="774ba-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="774ba-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="774ba-120">합니다 **IAuthenticatedEncryptorFactory** 인터페이스를 만드는 방법을 알고 있는 유형을 나타냅니다는 [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="774ba-120">The **IAuthenticatedEncryptorFactory** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="774ba-121">해당 API는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-121">Its API is as follows.</span></span>

* <span data-ttu-id="774ba-122">CreateEncryptorInstance (IKey 키): IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="774ba-122">CreateEncryptorInstance(IKey key) : IAuthenticatedEncryptor</span></span>

<span data-ttu-id="774ba-123">지정된 된 IKey 인스턴스에서 대 한 해당 CreateEncryptorInstance 메서드에 의해 만들어진 모든 인증 된 암호기 고려해 야 에서처럼 해당는 아래 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-123">For any given IKey instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorFactory instance and an IKey instance
IAuthenticatedEncryptorFactory factory = ...;
IKey key = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = factory.CreateEncryptorInstance(key);
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = factory.CreateEncryptorInstance(key);
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="774ba-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="774ba-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="774ba-125">합니다 **IAuthenticatedEncryptorDescriptor** 인터페이스를 만드는 방법을 알고 있는 유형을 나타냅니다는 [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="774ba-125">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="774ba-126">해당 API는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-126">Its API is as follows.</span></span>

* <span data-ttu-id="774ba-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="774ba-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span></span>

* <span data-ttu-id="774ba-128">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="774ba-128">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

<span data-ttu-id="774ba-129">IAuthenticatedEncryptor, 같은 IAuthenticatedEncryptorDescriptor 인스턴스에 하나의 특정 키 래핑로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-129">Like IAuthenticatedEncryptor, an instance of IAuthenticatedEncryptorDescriptor is assumed to wrap one specific key.</span></span> <span data-ttu-id="774ba-130">이 지정된 된 IAuthenticatedEncryptorDescriptor 인스턴스에서 대 한 해당 CreateEncryptorInstance 메서드에 의해 만들어진 모든 인증 된 암호기 고려해 야 에서처럼 해당 의미는 아래 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-130">This means that for any given IAuthenticatedEncryptorDescriptor instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorDescriptor instance
IAuthenticatedEncryptorDescriptor descriptor = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = descriptor.CreateEncryptorInstance();
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = descriptor.CreateEncryptorInstance();
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

---

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="iauthenticatedencryptordescriptor-aspnet-core-2x-only"></a><span data-ttu-id="774ba-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x만)</span><span class="sxs-lookup"><span data-stu-id="774ba-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x only)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="774ba-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="774ba-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="774ba-133">합니다 **IAuthenticatedEncryptorDescriptor** 인터페이스 자신을 XML로 내보낼 수 있는 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-133">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to export itself to XML.</span></span> <span data-ttu-id="774ba-134">해당 API는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-134">Its API is as follows.</span></span>

* <span data-ttu-id="774ba-135">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="774ba-135">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="774ba-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="774ba-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

---

## <a name="xml-serialization"></a><span data-ttu-id="774ba-137">XML Serialization</span><span class="sxs-lookup"><span data-stu-id="774ba-137">XML Serialization</span></span>

<span data-ttu-id="774ba-138">IAuthenticatedEncryptor IAuthenticatedEncryptorDescriptor 사이의 주요 차이점 설명자 암호기를 만들고 올바른 인수를 제공 하는 방법을 알고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="774ba-138">The primary difference between IAuthenticatedEncryptor and IAuthenticatedEncryptorDescriptor is that the descriptor knows how to create the encryptor and supply it with valid arguments.</span></span> <span data-ttu-id="774ba-139">구현이 SymmetricAlgorithm 및 KeyedHashAlgorithm 의존 하는 IAuthenticatedEncryptor를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-139">Consider an IAuthenticatedEncryptor whose implementation relies on SymmetricAlgorithm and KeyedHashAlgorithm.</span></span> <span data-ttu-id="774ba-140">암호기의 작업이 형식을 사용 하는 것 하지만 반드시 있는지 알 수 없으므로 이러한 형식에서 발생 한 위치 응용 프로그램 다시 시작 하는 경우 자체를 다시 만드는 방법에 대 한 적절 한 설명을 작성 실제로 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-140">The encryptor's job is to consume these types, but it doesn't necessarily know where these types came from, so it can't really write out a proper description of how to recreate itself if the application restarts.</span></span> <span data-ttu-id="774ba-141">설명자를 기반으로 더 높은 수준으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-141">The descriptor acts as a higher level on top of this.</span></span> <span data-ttu-id="774ba-142">설명자 암호기 인스턴스를 만드는 방법을 알고 있으므로 (예를 들어 알고 필수 알고리즘을 만드는 방법), 응용 프로그램을 다시 설정한 후 암호기 인스턴스를 다시 만들 수 있도록 해당 지식을 XML 형식의 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-142">Since the descriptor knows how to create the encryptor instance (e.g., it knows how to create the required algorithms), it can serialize that knowledge in XML form so that the encryptor instance can be recreated after an application reset.</span></span>

<a name="data-protection-extensibility-core-crypto-exporttoxml"></a>

<span data-ttu-id="774ba-143">설명자 해당 ExportToXml 루틴을 통해 직렬화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-143">The descriptor can be serialized via its ExportToXml routine.</span></span> <span data-ttu-id="774ba-144">이 루틴을 XmlSerializedDescriptorInfo 두 속성을 포함 하는 반환: XElement 표현을 나타내는 형식과 설명자를 [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) 일 수 있음 해당 XElement 지정이 설명자 부활 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-144">This routine returns an XmlSerializedDescriptorInfo which contains two properties: the XElement representation of the descriptor and the Type which represents an [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) which can be used to resurrect this descriptor given the corresponding XElement.</span></span>

<span data-ttu-id="774ba-145">Serialize 된 설명자는 암호화 키 자료와 같은 중요 한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-145">The serialized descriptor may contain sensitive information such as cryptographic key material.</span></span> <span data-ttu-id="774ba-146">데이터 보호 시스템은 기본적으로 지원 저장소에 유지에 전에 정보를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-146">The data protection system has built-in support for encrypting information before it's persisted to storage.</span></span> <span data-ttu-id="774ba-147">설명자를 이용 하려면이 특성 이름 "requiresEncryption"를 사용 하 여 중요 한 정보를 포함 하는 요소를 표시 합니다 (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), "true" 값입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-147">To take advantage of this, the descriptor should mark the element which contains sensitive information with the attribute name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), value "true".</span></span>

>[!TIP]
> <span data-ttu-id="774ba-148">이 특성을 설정 하기 위한 도우미 API 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-148">There's a helper API for setting this attribute.</span></span> <span data-ttu-id="774ba-149">XElement.MarkAsRequiresEncryption() Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel 네임 스페이스에 있는 확장 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-149">Call the extension method XElement.MarkAsRequiresEncryption() located in namespace Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span></span>

<span data-ttu-id="774ba-150">Serialize 된 설명자를 중요 한 정보가 포함 되지 않습니다 하는 경우 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-150">There can also be cases where the serialized descriptor doesn't contain sensitive information.</span></span> <span data-ttu-id="774ba-151">HSM에 저장 된 암호화 키의 경우 다시 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="774ba-151">Consider again the case of a cryptographic key stored in an HSM.</span></span> <span data-ttu-id="774ba-152">HSM의 일반 텍스트 형태로 자료를 노출 하지 않습니다 하므로 자체를 직렬화 할 때 키 자료 아웃 설명자를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-152">The descriptor cannot write out the key material when serializing itself since the HSM won't expose the material in plaintext form.</span></span> <span data-ttu-id="774ba-153">대신 설명자 (HSM이 방식으로 내보내기 허용) 하는 경우 키 또는 키의 HSM의 고유 식별자 키 래핑 버전 작성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-153">Instead, the descriptor might write out the key-wrapped version of the key (if the HSM allows export in this fashion) or the HSM's own unique identifier for the key.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer"></a>

## <a name="iauthenticatedencryptordescriptordeserializer"></a><span data-ttu-id="774ba-154">IAuthenticatedEncryptorDescriptorDeserializer</span><span class="sxs-lookup"><span data-stu-id="774ba-154">IAuthenticatedEncryptorDescriptorDeserializer</span></span>

<span data-ttu-id="774ba-155">합니다 **IAuthenticatedEncryptorDescriptorDeserializer** 인터페이스 XElement에서 IAuthenticatedEncryptorDescriptor 인스턴스를 deserialize 하는 방법을 아는 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-155">The **IAuthenticatedEncryptorDescriptorDeserializer** interface represents a type that knows how to deserialize an IAuthenticatedEncryptorDescriptor instance from an XElement.</span></span> <span data-ttu-id="774ba-156">이 단일 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-156">It exposes a single method:</span></span>

* <span data-ttu-id="774ba-157">ImportFromXml (XElement 요소). IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="774ba-157">ImportFromXml(XElement element) : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="774ba-158">ImportFromXml 메서드에서 사용 하 여 반환 된 XElement [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) 원래 IAuthenticatedEncryptorDescriptor 해당을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-158">The ImportFromXml method takes the XElement that was returned by [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) and creates an equivalent of the original IAuthenticatedEncryptorDescriptor.</span></span>

<span data-ttu-id="774ba-159">IAuthenticatedEncryptorDescriptorDeserializer를 구현 하는 형식에는 다음 두 명의 public 생성자 중 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-159">Types which implement IAuthenticatedEncryptorDescriptorDeserializer should have one of the following two public constructors:</span></span>

* <span data-ttu-id="774ba-160">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="774ba-160">.ctor(IServiceProvider)</span></span>

* <span data-ttu-id="774ba-161">.ctor()</span><span class="sxs-lookup"><span data-stu-id="774ba-161">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="774ba-162">생성자에 전달 하는 IServiceProvider는 null 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-162">The IServiceProvider passed to the constructor may be null.</span></span>

## <a name="the-top-level-factory"></a><span data-ttu-id="774ba-163">최상위 팩터리</span><span class="sxs-lookup"><span data-stu-id="774ba-163">The top-level factory</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="774ba-164">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="774ba-164">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="774ba-165">합니다 **AlgorithmConfiguration** 클래스를 만드는 방법을 알고 형식을 나타냅니다 [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="774ba-165">The **AlgorithmConfiguration** class represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="774ba-166">단일 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-166">It exposes a single API.</span></span>

* <span data-ttu-id="774ba-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="774ba-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="774ba-168">최상위 팩터리에서 AlgorithmConfiguration 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-168">Think of AlgorithmConfiguration as the top-level factory.</span></span> <span data-ttu-id="774ba-169">구성 템플릿으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-169">The configuration serves as a template.</span></span> <span data-ttu-id="774ba-170">알고리즘 정보를 래핑합니다 (예를 들어,이 구성은 설명자는 AES-128-GCM 마스터 키를 사용 하 여 생성) 되었지만 특정 키와 연관 된 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-170">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="774ba-171">CreateNewDescriptor 라고, 새 키 자료만이 호출에 대해 생성 되 고 새 IAuthenticatedEncryptorDescriptor 생성 되는 경우이 키 자료 및 자료를 사용 하는 데 필요한 알고리즘 정보를 래핑하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-171">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="774ba-172">키 자료 없습니다 수 소프트웨어에서 만든 (메모리에 보관)를 만들고는 HSM 및 기타 등등 내에 보관 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-172">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="774ba-173">중요 한 점은 두 CreateNewDescriptor 호출 해당 IAuthenticatedEncryptorDescriptor 인스턴스를 만들지 마십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-173">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="774ba-174">AlgorithmConfiguration 형식와 같은 키를 만드는 루틴에 대 한 진입점으로 사용 됩니다 [자동 키 롤링](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-174">The AlgorithmConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="774ba-175">이후 모든 키에 대 한 구현을 변경 하려면 KeyManagementOptions에서 AuthenticatedEncryptorConfiguration 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-175">To change the implementation for all future keys, set the AuthenticatedEncryptorConfiguration property in KeyManagementOptions.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="774ba-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="774ba-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="774ba-177">합니다 **IAuthenticatedEncryptorConfiguration** 인터페이스를 만드는 방법을 알고 형식을 나타냅니다 [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="774ba-177">The **IAuthenticatedEncryptorConfiguration** interface represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="774ba-178">단일 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-178">It exposes a single API.</span></span>

* <span data-ttu-id="774ba-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="774ba-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="774ba-180">최상위 팩터리에서 IAuthenticatedEncryptorConfiguration 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-180">Think of IAuthenticatedEncryptorConfiguration as the top-level factory.</span></span> <span data-ttu-id="774ba-181">구성 템플릿으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-181">The configuration serves as a template.</span></span> <span data-ttu-id="774ba-182">알고리즘 정보를 래핑합니다 (예를 들어,이 구성은 설명자는 AES-128-GCM 마스터 키를 사용 하 여 생성) 되었지만 특정 키와 연관 된 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-182">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="774ba-183">CreateNewDescriptor 라고, 새 키 자료만이 호출에 대해 생성 되 고 새 IAuthenticatedEncryptorDescriptor 생성 되는 경우이 키 자료 및 자료를 사용 하는 데 필요한 알고리즘 정보를 래핑하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-183">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="774ba-184">키 자료 없습니다 수 소프트웨어에서 만든 (메모리에 보관)를 만들고는 HSM 및 기타 등등 내에 보관 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-184">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="774ba-185">중요 한 점은 두 CreateNewDescriptor 호출 해당 IAuthenticatedEncryptorDescriptor 인스턴스를 만들지 마십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-185">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="774ba-186">IAuthenticatedEncryptorConfiguration 형식와 같은 키를 만드는 루틴에 대 한 진입점으로 사용 됩니다 [자동 키 롤링](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-186">The IAuthenticatedEncryptorConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="774ba-187">이후 모든 키에 대 한 구현을 변경 하려면 단일 IAuthenticatedEncryptorConfiguration 서비스 컨테이너에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="774ba-187">To change the implementation for all future keys, register a singleton IAuthenticatedEncryptorConfiguration in the service container.</span></span>

---
