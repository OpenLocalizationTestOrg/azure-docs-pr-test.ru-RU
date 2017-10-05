---
title: "Заметки о выпуске API для хранилища ключей .NET 2.x | Документация Майкрософт"
description: "Разработчики .NET смогут использовать этот API в коде при работе с хранилищем ключей Azure."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="e8b89-103">Хранилище ключей Azure .NET 2.0. Руководство по миграции и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="e8b89-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="e8b89-104">Следующие примечания и инструкции предназначены для разработчиков, использующих библиотеки .NET и C# при работе с Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e8b89-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="e8b89-105">Переходная версия между 1.0 и 2.0 включает ряд таких обновлений, как реализация поддержки **сертификатов хранилища ключей**. Чтобы воспользоваться новыми возможностями и улучшениями, необходимо программным образом выполнить перенос.</span><span class="sxs-lookup"><span data-stu-id="e8b89-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="e8b89-106">Сертификаты Key Vault</span><span class="sxs-lookup"><span data-stu-id="e8b89-106">Key Vault certificates</span></span>

<span data-ttu-id="e8b89-107">Поддержка сертификатов хранилища ключей не только позволяет управлять сертификатами x509, но и предоставляет следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="e8b89-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="e8b89-108">Владелец сертификата может создать сертификат при создании хранилища ключей или импорте существующего сертификата.</span><span class="sxs-lookup"><span data-stu-id="e8b89-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="e8b89-109">Это применимо как для самозаверяющих сертификатов, так и для сертификатов, созданных центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="e8b89-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="e8b89-110">Владелец сертификата хранилища ключей может безопасно хранить сертификаты X509 и управлять ими без необходимости использовать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="e8b89-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="e8b89-111">Владелец сертификата может создать политику, которая определяет для хранилища ключей параметры управления жизненным циклом сертификата.</span><span class="sxs-lookup"><span data-stu-id="e8b89-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="e8b89-112">Владелец сертификата может предоставить контактные данные для получения уведомлений о таких событиях жизненного цикла, как истечение срока действия и обновление сертификата.</span><span class="sxs-lookup"><span data-stu-id="e8b89-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="e8b89-113">Автоматическое обновление с возможностью выбора издателей сертификатов хранилища ключей — партнерских поставщиков сертификатов X509 и центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="e8b89-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="e8b89-114">ПРИМЕЧАНИЕ. Также разрешено использовать сертификаты, которые предоставляются поставщиками и центрами, не являющимися партнерами. Но в таком случае функция автоматического обновления недоступна.</span><span class="sxs-lookup"><span data-stu-id="e8b89-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="e8b89-115">Поддержка .NET</span><span class="sxs-lookup"><span data-stu-id="e8b89-115">.NET support</span></span>

* <span data-ttu-id="e8b89-116">**.NET 4.0** не поддерживается в версии 2.0 библиотеки .NET и C# для хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b89-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="e8b89-117">**.NET Core** поддерживается в версии 2.0 библиотеки .NET и C# для хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b89-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="e8b89-118">Пространства имен</span><span class="sxs-lookup"><span data-stu-id="e8b89-118">Namespaces</span></span>

* <span data-ttu-id="e8b89-119">Пространство имен **Microsoft.Azure.KeyVault** для **моделей** изменено на **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="e8b89-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="e8b89-120">Пространство имен **Microsoft.Azure.KeyVault.Internal** удалено.</span><span class="sxs-lookup"><span data-stu-id="e8b89-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="e8b89-121">Пространство имен **Hyak.Common** и **Hyak.Common.Internals** зависимостей пакета SDK для Azure изменено на **Microsoft.Rest** и **Microsoft.Rest.Serialization** соответственно.</span><span class="sxs-lookup"><span data-stu-id="e8b89-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="e8b89-122">Изменения в типах</span><span class="sxs-lookup"><span data-stu-id="e8b89-122">Type changes</span></span>

* <span data-ttu-id="e8b89-123">*Secret* — изменено на *SecretBundle*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="e8b89-124">*Dictionary* — изменено на *IDictionary*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="e8b89-125">*List<T>, string []* — изменено на *IList<T>*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="e8b89-126">*NextList* — изменено на *NextPageLink*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="e8b89-127">Возвращаемые типы</span><span class="sxs-lookup"><span data-stu-id="e8b89-127">Return types</span></span>

* <span data-ttu-id="e8b89-128">**KeyList** и **SecretList** возвращают *IPage<T>* вместо *ListKeysResponseMessage*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="e8b89-129">Созданный метод **BackupKeyAsync** возвращает *BackupKeyResult* (содержит *Value* — большой двоичный объект для резервного копирования).</span><span class="sxs-lookup"><span data-stu-id="e8b89-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="e8b89-130">Ранее метод был внутренним и возвращал только значение.</span><span class="sxs-lookup"><span data-stu-id="e8b89-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="e8b89-131">Исключения</span><span class="sxs-lookup"><span data-stu-id="e8b89-131">Exceptions</span></span>

* <span data-ttu-id="e8b89-132">*KeyVaultClientException* — изменено на *KeyVaultErrorException*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="e8b89-133">Ошибка службы *exception.Error* изменена на *exception.Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="e8b89-134">Из сообщения об ошибке для **[JsonExtensionData]** удалены дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="e8b89-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="e8b89-135">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="e8b89-135">Constructors</span></span>

* <span data-ttu-id="e8b89-136">В качестве аргумента конструктор принимает только *HttpClientHandler* или *[DelegatingHandler]* вместо *HttpClient*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="e8b89-137">Скачанные пакеты</span><span class="sxs-lookup"><span data-stu-id="e8b89-137">Downloaded packages</span></span>

<span data-ttu-id="e8b89-138">При обработке клиентом зависимости в хранилище ключей раньше скачивались следующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="e8b89-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="e8b89-139">Предыдущий список пакетов</span><span class="sxs-lookup"><span data-stu-id="e8b89-139">Previous package list</span></span>

* <span data-ttu-id="e8b89-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="e8b89-148">Текущий список пакетов</span><span class="sxs-lookup"><span data-stu-id="e8b89-148">Current package list</span></span>

* <span data-ttu-id="e8b89-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="e8b89-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="e8b89-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="e8b89-152">Изменения в классах</span><span class="sxs-lookup"><span data-stu-id="e8b89-152">Class changes</span></span>

* <span data-ttu-id="e8b89-153">Класс **UnixEpoch** удален.</span><span class="sxs-lookup"><span data-stu-id="e8b89-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="e8b89-154">Класс **Base64UrlConverter** переименован в **Base64UrlJsonConverter**.</span><span class="sxs-lookup"><span data-stu-id="e8b89-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="e8b89-155">Другие изменения</span><span class="sxs-lookup"><span data-stu-id="e8b89-155">Other changes</span></span>

* <span data-ttu-id="e8b89-156">В этой версии API можно настраивать политику повтора операции KV при временных сбоях.</span><span class="sxs-lookup"><span data-stu-id="e8b89-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="e8b89-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="e8b89-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="e8b89-158">Для операций, которые возвращали *vault*, возвращаемый тип был представлен классом, который содержал свойство Vault.</span><span class="sxs-lookup"><span data-stu-id="e8b89-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="e8b89-159">Теперь возвращаемый тип — *Vault*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="e8b89-160">*PermissionsToKeys* и *PermissionsToSecrets* — изменено на *Permissions.Keys* и *Permissions.Secrets*.</span><span class="sxs-lookup"><span data-stu-id="e8b89-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="e8b89-161">Некоторые изменения возвращаемых типов применяются также на уровне управления.</span><span class="sxs-lookup"><span data-stu-id="e8b89-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="e8b89-162">Пакет NuGet Microsoft.Azure.KeyVault.Extensions</span><span class="sxs-lookup"><span data-stu-id="e8b89-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="e8b89-163">Пакет разбит на **Microsoft.Azure.KeyVault.Extensions** и **Microsoft.Azure.KeyVault.Cryptography** для шифрования.</span><span class="sxs-lookup"><span data-stu-id="e8b89-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

