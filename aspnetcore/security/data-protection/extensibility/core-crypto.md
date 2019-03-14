---
title: Rozšiřitelnost základní kryptografie v ASP.NET Core
author: rick-anderson
description: Další informace o IAuthenticatedEncryptor, IAuthenticatedEncryptorDescriptor, IAuthenticatedEncryptorDescriptorDeserializer a objekt pro vytváření nejvyšší úrovně.
ms.author: riande
ms.date: 8/11/2017
uid: security/data-protection/extensibility/core-crypto
ms.openlocfilehash: 47432cfefe0a52c9f815d717f7269ec68fdb6af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069472"
---
# <a name="core-cryptography-extensibility-in-aspnet-core"></a><span data-ttu-id="5ca45-103">Rozšiřitelnost základní kryptografie v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5ca45-103">Core cryptography extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-core-crypto"></a>

>[!WARNING]
> <span data-ttu-id="5ca45-104">Typy, které implementují některý z následujících rozhraní by měly být bezpečné pro vlákna pro více volání.</span><span class="sxs-lookup"><span data-stu-id="5ca45-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptor"></a>

## <a name="iauthenticatedencryptor"></a><span data-ttu-id="5ca45-105">IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-105">IAuthenticatedEncryptor</span></span>

<span data-ttu-id="5ca45-106">**IAuthenticatedEncryptor** rozhraní je základním stavebním blokem šifrovací subsystém.</span><span class="sxs-lookup"><span data-stu-id="5ca45-106">The **IAuthenticatedEncryptor** interface is the basic building block of the cryptographic subsystem.</span></span> <span data-ttu-id="5ca45-107">Obecně je jeden IAuthenticatedEncryptor za klíč a IAuthenticatedEncryptor instance zabalí všechny kryptografické klíče a vylepšením informace potřebné k provedení kryptografických operací.</span><span class="sxs-lookup"><span data-stu-id="5ca45-107">There's generally one IAuthenticatedEncryptor per key, and the IAuthenticatedEncryptor instance wraps all cryptographic key material and algorithmic information necessary to perform cryptographic operations.</span></span>

<span data-ttu-id="5ca45-108">Jak název napovídá, typ je odpovědný za poskytnutí ověřeného šifrovacích a dešifrovacích služeb.</span><span class="sxs-lookup"><span data-stu-id="5ca45-108">As its name suggests, the type is responsible for providing authenticated encryption and decryption services.</span></span> <span data-ttu-id="5ca45-109">Poskytuje následující dvě rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5ca45-109">It exposes the following two APIs.</span></span>

* <span data-ttu-id="5ca45-110">Dešifrování (ArraySegment<byte> šifrovaného textu, ArraySegment<byte> additionalAuthenticatedData): byte]</span><span class="sxs-lookup"><span data-stu-id="5ca45-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

* <span data-ttu-id="5ca45-111">Šifrování (ArraySegment<byte> ve formátu prostého textu, ArraySegment<byte> additionalAuthenticatedData): byte]</span><span class="sxs-lookup"><span data-stu-id="5ca45-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

<span data-ttu-id="5ca45-112">Vrátí metoda šifrování objektů blob, který zahrnuje enciphered ve formátu prostého textu a ověřovací značka.</span><span class="sxs-lookup"><span data-stu-id="5ca45-112">The Encrypt method returns a blob that includes the enciphered plaintext and an authentication tag.</span></span> <span data-ttu-id="5ca45-113">Ověřovací značka musí zahrnovat další ověřených dat (AAD), i když AAD, samotný nemusí být obnovitelné z poslední datové části.</span><span class="sxs-lookup"><span data-stu-id="5ca45-113">The authentication tag must encompass the additional authenticated data (AAD), though the AAD itself need not be recoverable from the final payload.</span></span> <span data-ttu-id="5ca45-114">Metoda dešifrovat ověří ověřovací značka a vrátí deciphered datové části.</span><span class="sxs-lookup"><span data-stu-id="5ca45-114">The Decrypt method validates the authentication tag and returns the deciphered payload.</span></span> <span data-ttu-id="5ca45-115">K cryptographicexception – musí být homogenizovány všechny chyby (s výjimkou ArgumentNullException a podobně).</span><span class="sxs-lookup"><span data-stu-id="5ca45-115">All failures (except ArgumentNullException and similar) should be homogenized to CryptographicException.</span></span>

> [!NOTE]
> <span data-ttu-id="5ca45-116">Samotné instanci IAuthenticatedEncryptor ve skutečnosti nemusí obsahovat materiál klíče.</span><span class="sxs-lookup"><span data-stu-id="5ca45-116">The IAuthenticatedEncryptor instance itself doesn't actually need to contain the key material.</span></span> <span data-ttu-id="5ca45-117">Například může delegovat implementace modulu hardwarového zabezpečení pro všechny operace.</span><span class="sxs-lookup"><span data-stu-id="5ca45-117">For example, the implementation could delegate to an HSM for all operations.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptorfactory"></a>
<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="how-to-create-an-iauthenticatedencryptor"></a><span data-ttu-id="5ca45-118">Vytvoření IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-118">How to create an IAuthenticatedEncryptor</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ca45-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ca45-120">**IAuthenticatedEncryptorFactory** rozhraní představuje typ, který se ví, jak vytvořit [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span><span class="sxs-lookup"><span data-stu-id="5ca45-120">The **IAuthenticatedEncryptorFactory** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="5ca45-121">Své rozhraní API je následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="5ca45-121">Its API is as follows.</span></span>

* <span data-ttu-id="5ca45-122">CreateEncryptorInstance (klíč Instrumentační klíč): IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-122">CreateEncryptorInstance(IKey key) : IAuthenticatedEncryptor</span></span>

<span data-ttu-id="5ca45-123">Pro jakoukoli danou instanci Instrumentační klíč, všechny ověřené encryptors vytvářené metodou jeho CreateEncryptorInstance by měl být ekvivalentní, stejně jako následující vzorový kód.</span><span class="sxs-lookup"><span data-stu-id="5ca45-123">For any given IKey instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ca45-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5ca45-125">**IAuthenticatedEncryptorDescriptor** rozhraní představuje typ, který se ví, jak vytvořit [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span><span class="sxs-lookup"><span data-stu-id="5ca45-125">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="5ca45-126">Své rozhraní API je následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="5ca45-126">Its API is as follows.</span></span>

* <span data-ttu-id="5ca45-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span></span>

* <span data-ttu-id="5ca45-128">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="5ca45-128">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

<span data-ttu-id="5ca45-129">Stejně jako IAuthenticatedEncryptor instance IAuthenticatedEncryptorDescriptor je považován za zabalení jeden konkrétní klíč.</span><span class="sxs-lookup"><span data-stu-id="5ca45-129">Like IAuthenticatedEncryptor, an instance of IAuthenticatedEncryptorDescriptor is assumed to wrap one specific key.</span></span> <span data-ttu-id="5ca45-130">To znamená, že pro všechny instance daného IAuthenticatedEncryptorDescriptor všechny ověřené encryptors vytvářené metodou jeho CreateEncryptorInstance by měl být považovány za ekvivalentní, stejně jako v následující vzorový kód.</span><span class="sxs-lookup"><span data-stu-id="5ca45-130">This means that for any given IAuthenticatedEncryptorDescriptor instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

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

## <a name="iauthenticatedencryptordescriptor-aspnet-core-2x-only"></a><span data-ttu-id="5ca45-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x jenom)</span><span class="sxs-lookup"><span data-stu-id="5ca45-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x only)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ca45-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ca45-133">**IAuthenticatedEncryptorDescriptor** rozhraní představuje typ, který umí samotné exportovat do formátu XML.</span><span class="sxs-lookup"><span data-stu-id="5ca45-133">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to export itself to XML.</span></span> <span data-ttu-id="5ca45-134">Své rozhraní API je následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="5ca45-134">Its API is as follows.</span></span>

* <span data-ttu-id="5ca45-135">ExportToXml() : XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="5ca45-135">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ca45-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

---

## <a name="xml-serialization"></a><span data-ttu-id="5ca45-137">Serializace XML</span><span class="sxs-lookup"><span data-stu-id="5ca45-137">XML Serialization</span></span>

<span data-ttu-id="5ca45-138">Hlavní rozdíl mezi IAuthenticatedEncryptor a IAuthenticatedEncryptorDescriptor je, že popisovač ví, jak vytvořit šifrování a poskytne mu platné argumenty.</span><span class="sxs-lookup"><span data-stu-id="5ca45-138">The primary difference between IAuthenticatedEncryptor and IAuthenticatedEncryptorDescriptor is that the descriptor knows how to create the encryptor and supply it with valid arguments.</span></span> <span data-ttu-id="5ca45-139">Vezměte v úvahu IAuthenticatedEncryptor, jehož implementace využívá SymmetricAlgorithm a KeyedHashAlgorithm.</span><span class="sxs-lookup"><span data-stu-id="5ca45-139">Consider an IAuthenticatedEncryptor whose implementation relies on SymmetricAlgorithm and KeyedHashAlgorithm.</span></span> <span data-ttu-id="5ca45-140">Úloha šifrování je používat tyto typy, ale nemá specifické znalosti nutně těchto typů, odkud, takže ho nejde vypsat skutečně správné popis toho, jak vytvořit samotné znovu, pokud se aplikace restartuje.</span><span class="sxs-lookup"><span data-stu-id="5ca45-140">The encryptor's job is to consume these types, but it doesn't necessarily know where these types came from, so it can't really write out a proper description of how to recreate itself if the application restarts.</span></span> <span data-ttu-id="5ca45-141">Popisovač funguje jako vyšší úroveň nad to.</span><span class="sxs-lookup"><span data-stu-id="5ca45-141">The descriptor acts as a higher level on top of this.</span></span> <span data-ttu-id="5ca45-142">Vzhledem k tomu, že popisovač ví, jak vytvořit instanci šifrování (například ví, jak vytvořit požadované algoritmy), tak, aby modul instance může být znovu vytvořena po obnovení aplikace ji může serializovat dané znalosti v podobě XML.</span><span class="sxs-lookup"><span data-stu-id="5ca45-142">Since the descriptor knows how to create the encryptor instance (e.g., it knows how to create the required algorithms), it can serialize that knowledge in XML form so that the encryptor instance can be recreated after an application reset.</span></span>

<a name="data-protection-extensibility-core-crypto-exporttoxml"></a>

<span data-ttu-id="5ca45-143">Popisovač lze serializovat pomocí jeho ExportToXml rutiny.</span><span class="sxs-lookup"><span data-stu-id="5ca45-143">The descriptor can be serialized via its ExportToXml routine.</span></span> <span data-ttu-id="5ca45-144">Tato rutina vrátí XmlSerializedDescriptorInfo, která obsahuje dvě vlastnosti: XElement reprezentace popisovač a typ, který představuje [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) může být použít resurrect tento popisovač zadaný odpovídající XElement.</span><span class="sxs-lookup"><span data-stu-id="5ca45-144">This routine returns an XmlSerializedDescriptorInfo which contains two properties: the XElement representation of the descriptor and the Type which represents an [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) which can be used to resurrect this descriptor given the corresponding XElement.</span></span>

<span data-ttu-id="5ca45-145">Serializovaná popisovače mohou obsahovat citlivé informace, jako je například kryptografické klíče.</span><span class="sxs-lookup"><span data-stu-id="5ca45-145">The serialized descriptor may contain sensitive information such as cryptographic key material.</span></span> <span data-ttu-id="5ca45-146">Systém ochrany dat obsahuje integrovanou podporu pro šifrování informací, než se trvale uložena do úložiště.</span><span class="sxs-lookup"><span data-stu-id="5ca45-146">The data protection system has built-in support for encrypting information before it's persisted to storage.</span></span> <span data-ttu-id="5ca45-147">Umožní využít této popisovač by měl označit element, který obsahuje citlivé informace pomocí atributu name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), hodnota "true".</span><span class="sxs-lookup"><span data-stu-id="5ca45-147">To take advantage of this, the descriptor should mark the element which contains sensitive information with the attribute name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), value "true".</span></span>

>[!TIP]
> <span data-ttu-id="5ca45-148">Nastavení tohoto atributu je pomocná rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5ca45-148">There's a helper API for setting this attribute.</span></span> <span data-ttu-id="5ca45-149">Volání metody rozšíření, které XElement.MarkAsRequiresEncryption() nachází v oboru názvů Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span><span class="sxs-lookup"><span data-stu-id="5ca45-149">Call the extension method XElement.MarkAsRequiresEncryption() located in namespace Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span></span>

<span data-ttu-id="5ca45-150">Může existovat také případy, kdy serializovaná popisovač neobsahuje citlivé informace.</span><span class="sxs-lookup"><span data-stu-id="5ca45-150">There can also be cases where the serialized descriptor doesn't contain sensitive information.</span></span> <span data-ttu-id="5ca45-151">Podívejte se znovu na kryptografického klíče uložené v modulu hardwarového zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="5ca45-151">Consider again the case of a cryptographic key stored in an HSM.</span></span> <span data-ttu-id="5ca45-152">Popisovač nelze vypsat materiál klíče při serializaci samotné, protože modul hardwarového zabezpečení nebude vystavit materiál v podobě prostého textu.</span><span class="sxs-lookup"><span data-stu-id="5ca45-152">The descriptor cannot write out the key material when serializing itself since the HSM won't expose the material in plaintext form.</span></span> <span data-ttu-id="5ca45-153">Místo toho může být popisovač vypsat klíč zabalené verze klíče (Pokud modul hardwarového zabezpečení umožňuje export tímto způsobem) nebo hardwarového zabezpečení pro vlastní jedinečný identifikátor pro klíč.</span><span class="sxs-lookup"><span data-stu-id="5ca45-153">Instead, the descriptor might write out the key-wrapped version of the key (if the HSM allows export in this fashion) or the HSM's own unique identifier for the key.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer"></a>

## <a name="iauthenticatedencryptordescriptordeserializer"></a><span data-ttu-id="5ca45-154">IAuthenticatedEncryptorDescriptorDeserializer</span><span class="sxs-lookup"><span data-stu-id="5ca45-154">IAuthenticatedEncryptorDescriptorDeserializer</span></span>

<span data-ttu-id="5ca45-155">**IAuthenticatedEncryptorDescriptorDeserializer** rozhraní představuje typ, který se ví, jak provést deserializaci instance IAuthenticatedEncryptorDescriptor z XElement.</span><span class="sxs-lookup"><span data-stu-id="5ca45-155">The **IAuthenticatedEncryptorDescriptorDeserializer** interface represents a type that knows how to deserialize an IAuthenticatedEncryptorDescriptor instance from an XElement.</span></span> <span data-ttu-id="5ca45-156">Poskytuje jedinou metodu:</span><span class="sxs-lookup"><span data-stu-id="5ca45-156">It exposes a single method:</span></span>

* <span data-ttu-id="5ca45-157">ImportFromXml (XElement element): IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-157">ImportFromXml(XElement element) : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="5ca45-158">Metoda ImportFromXml přebírá XElement, který byl vrácen [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) a vytvoří ekvivalent původní IAuthenticatedEncryptorDescriptor.</span><span class="sxs-lookup"><span data-stu-id="5ca45-158">The ImportFromXml method takes the XElement that was returned by [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) and creates an equivalent of the original IAuthenticatedEncryptorDescriptor.</span></span>

<span data-ttu-id="5ca45-159">Typy, které implementují IAuthenticatedEncryptorDescriptorDeserializer musí mít jednu z následujících dvou veřejných konstruktorů:</span><span class="sxs-lookup"><span data-stu-id="5ca45-159">Types which implement IAuthenticatedEncryptorDescriptorDeserializer should have one of the following two public constructors:</span></span>

* <span data-ttu-id="5ca45-160">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="5ca45-160">.ctor(IServiceProvider)</span></span>

* <span data-ttu-id="5ca45-161">.ctor()</span><span class="sxs-lookup"><span data-stu-id="5ca45-161">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="5ca45-162">IServiceProvider předaný konstruktoru může mít hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="5ca45-162">The IServiceProvider passed to the constructor may be null.</span></span>

## <a name="the-top-level-factory"></a><span data-ttu-id="5ca45-163">Objekt pro vytváření nejvyšší úrovně</span><span class="sxs-lookup"><span data-stu-id="5ca45-163">The top-level factory</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ca45-164">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-164">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ca45-165">**AlgorithmConfiguration** třída představuje typ, který umí vytvořit [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instancí.</span><span class="sxs-lookup"><span data-stu-id="5ca45-165">The **AlgorithmConfiguration** class represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="5ca45-166">Poskytuje jediné rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5ca45-166">It exposes a single API.</span></span>

* <span data-ttu-id="5ca45-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="5ca45-168">AlgorithmConfiguration můžete představit jako objekt pro vytváření nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="5ca45-168">Think of AlgorithmConfiguration as the top-level factory.</span></span> <span data-ttu-id="5ca45-169">Konfigurace slouží jako šablona.</span><span class="sxs-lookup"><span data-stu-id="5ca45-169">The configuration serves as a template.</span></span> <span data-ttu-id="5ca45-170">Zabalí vylepšením informace (například tato konfigurace vytvoří popisovače pomocí hlavního klíče AES-128-GCM), ale je ještě není přidružená určitého klíče.</span><span class="sxs-lookup"><span data-stu-id="5ca45-170">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="5ca45-171">Když je zavolána CreateNewDescriptor, výhradně pro toto volání se vytvoří nový materiál klíče a je vytvořen nový IAuthenticatedEncryptorDescriptor který zabalí tento materiál klíče a vylepšením informace požadované pro využívání materiálu.</span><span class="sxs-lookup"><span data-stu-id="5ca45-171">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="5ca45-172">Materiál klíče může vytvořit v softwaru (a uložené v paměti), může být vytvořen a uložených v HSM a tak dále.</span><span class="sxs-lookup"><span data-stu-id="5ca45-172">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="5ca45-173">Velmi důležitý bod je, že dvě volání CreateNewDescriptor nikdy vytvořit ekvivalentní IAuthenticatedEncryptorDescriptor instancí.</span><span class="sxs-lookup"><span data-stu-id="5ca45-173">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="5ca45-174">Typ AlgorithmConfiguration slouží jako vstupní bod pro vytvoření klíče rutin, jako [automatické klíč se zajištěním provozu](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span><span class="sxs-lookup"><span data-stu-id="5ca45-174">The AlgorithmConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="5ca45-175">Chcete-li změnit implementace pro všechny budoucí klíče, nastavte vlastnost AuthenticatedEncryptorConfiguration v KeyManagementOptions.</span><span class="sxs-lookup"><span data-stu-id="5ca45-175">To change the implementation for all future keys, set the AuthenticatedEncryptorConfiguration property in KeyManagementOptions.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ca45-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ca45-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5ca45-177">**IAuthenticatedEncryptorConfiguration** rozhraní představuje typ, který umí vytvořit [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instancí.</span><span class="sxs-lookup"><span data-stu-id="5ca45-177">The **IAuthenticatedEncryptorConfiguration** interface represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="5ca45-178">Poskytuje jediné rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5ca45-178">It exposes a single API.</span></span>

* <span data-ttu-id="5ca45-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="5ca45-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="5ca45-180">IAuthenticatedEncryptorConfiguration můžete představit jako objekt pro vytváření nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="5ca45-180">Think of IAuthenticatedEncryptorConfiguration as the top-level factory.</span></span> <span data-ttu-id="5ca45-181">Konfigurace slouží jako šablona.</span><span class="sxs-lookup"><span data-stu-id="5ca45-181">The configuration serves as a template.</span></span> <span data-ttu-id="5ca45-182">Zabalí vylepšením informace (například tato konfigurace vytvoří popisovače pomocí hlavního klíče AES-128-GCM), ale je ještě není přidružená určitého klíče.</span><span class="sxs-lookup"><span data-stu-id="5ca45-182">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="5ca45-183">Když je zavolána CreateNewDescriptor, výhradně pro toto volání se vytvoří nový materiál klíče a je vytvořen nový IAuthenticatedEncryptorDescriptor který zabalí tento materiál klíče a vylepšením informace požadované pro využívání materiálu.</span><span class="sxs-lookup"><span data-stu-id="5ca45-183">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="5ca45-184">Materiál klíče může vytvořit v softwaru (a uložené v paměti), může být vytvořen a uložených v HSM a tak dále.</span><span class="sxs-lookup"><span data-stu-id="5ca45-184">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="5ca45-185">Velmi důležitý bod je, že dvě volání CreateNewDescriptor nikdy vytvořit ekvivalentní IAuthenticatedEncryptorDescriptor instancí.</span><span class="sxs-lookup"><span data-stu-id="5ca45-185">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="5ca45-186">Typ IAuthenticatedEncryptorConfiguration slouží jako vstupní bod pro vytvoření klíče rutin, jako [automatické klíč se zajištěním provozu](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span><span class="sxs-lookup"><span data-stu-id="5ca45-186">The IAuthenticatedEncryptorConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="5ca45-187">Chcete-li změnit implementace pro všechny budoucí klíče, zaregistrujte IAuthenticatedEncryptorConfiguration jednotlivý prvek v kontejneru služby.</span><span class="sxs-lookup"><span data-stu-id="5ca45-187">To change the implementation for all future keys, register a singleton IAuthenticatedEncryptorConfiguration in the service container.</span></span>

---
