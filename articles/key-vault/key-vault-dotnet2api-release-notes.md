---
title: "заметки о выпуске API 2.x .NET хранилища aaaKey | Документы Microsoft"
description: "Разработчики .NET будет использовать этот API toocode для хранилища ключей Azure"
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
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="3b26f-103">Хранилище ключей Azure .NET 2.0. Руководство по миграции и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="3b26f-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="3b26f-104">Hello следующие примечания и инструкции предназначены для разработчиков, работающих с хранилищем ключей Azure .NET или библиотеки C#.</span><span class="sxs-lookup"><span data-stu-id="3b26f-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="3b26f-105">В hello переход с версии toohello 2.0 версии hello 1.0, количество операций обновления были внесены позволит потребуется выполнить определенные действия по миграции в коде, чтобы toobenefit из функциональных улучшений hello и функции дополнения, такие как **хранилища ключей Сертификаты** поддержки.</span><span class="sxs-lookup"><span data-stu-id="3b26f-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="3b26f-106">Сертификаты Key Vault</span><span class="sxs-lookup"><span data-stu-id="3b26f-106">Key Vault certificates</span></span>

<span data-ttu-id="3b26f-107">Предоставляет поддержку сертификатов хранилища ключей для управления вашей x509 сертификаты и hello следующие варианты поведения:</span><span class="sxs-lookup"><span data-stu-id="3b26f-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="3b26f-108">Позволяет владельцу сертификата toocreate сертификату через процесс создания хранилища ключей или hello Импорт существующего сертификата.</span><span class="sxs-lookup"><span data-stu-id="3b26f-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="3b26f-109">Это применимо как для самозаверяющих сертификатов, так и для сертификатов, созданных центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="3b26f-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="3b26f-110">Позволяет владельцу сертификата хранилища ключей, tooimplement безопасное хранение и управление ими X509 сертификатов без взаимодействия с материал закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="3b26f-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="3b26f-111">Позволяет владельцу сертификата toocreate политику, которая направляет хранилище ключей toomanage hello жизненного цикла сертификата.</span><span class="sxs-lookup"><span data-stu-id="3b26f-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="3b26f-112">Позволяет владельцам сертификат tooprovide контактные данные для уведомления о событиях жизненного цикла истечение срока действия и обновления сертификата.</span><span class="sxs-lookup"><span data-stu-id="3b26f-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="3b26f-113">Автоматическое обновление с возможностью выбора издателей сертификатов хранилища ключей — партнерских поставщиков сертификатов X509 и центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="3b26f-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="3b26f-114">Обратите внимание — поставщики партнером и центры также разрешены, но не будет поддерживать hello автоматического обновления компонентов.</span><span class="sxs-lookup"><span data-stu-id="3b26f-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="3b26f-115">Поддержка .NET</span><span class="sxs-lookup"><span data-stu-id="3b26f-115">.NET support</span></span>

* <span data-ttu-id="3b26f-116">**.NET 4.0** не поддерживается в версии hello 2.0 hello хранилище ключей Azure .NET или библиотеки C#</span><span class="sxs-lookup"><span data-stu-id="3b26f-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="3b26f-117">**.NET core** поддерживается в версии hello 2.0 hello хранилище ключей Azure .NET или библиотеки C#</span><span class="sxs-lookup"><span data-stu-id="3b26f-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="3b26f-118">Пространства имен</span><span class="sxs-lookup"><span data-stu-id="3b26f-118">Namespaces</span></span>

* <span data-ttu-id="3b26f-119">Здравствуйте, пространство имен для **моделей** меняется с **Microsoft.Azure.KeyVault** слишком**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="3b26f-120">Hello **Microsoft.Azure.KeyVault.Internal** удалении пространства имен.</span><span class="sxs-lookup"><span data-stu-id="3b26f-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="3b26f-121">пространство имен зависимости пакета Azure SDK Hello изменяются с **Hyak.Common** и **Hyak.Common.Internals** слишком**Microsoft.Rest** и  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="3b26f-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="3b26f-122">Изменения в типах</span><span class="sxs-lookup"><span data-stu-id="3b26f-122">Type changes</span></span>

* <span data-ttu-id="3b26f-123">*Секрет* изменено слишком*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="3b26f-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="3b26f-124">*Словарь* изменено слишком*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="3b26f-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="3b26f-125">*Список<T>, string []* изменено слишком*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="3b26f-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="3b26f-126">*NextList* изменено слишком *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="3b26f-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="3b26f-127">Возвращаемые типы</span><span class="sxs-lookup"><span data-stu-id="3b26f-127">Return types</span></span>

* <span data-ttu-id="3b26f-128">**KeyList** и **SecretList** возвращают *IPage<T>* вместо *ListKeysResponseMessage*.</span><span class="sxs-lookup"><span data-stu-id="3b26f-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="3b26f-129">созданный Hello **BackupKeyAsync** вернет *BackupKeyResult* , содержащее *значение* (резервное копирование больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="3b26f-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="3b26f-130">Перед hello метод выполнен перенос и возвращение только значение hello.</span><span class="sxs-lookup"><span data-stu-id="3b26f-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="3b26f-131">Исключения</span><span class="sxs-lookup"><span data-stu-id="3b26f-131">Exceptions</span></span>

* <span data-ttu-id="3b26f-132">*KeyVaultClientException* изменяется слишком*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="3b26f-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="3b26f-133">Ошибка службы Hello изменяется с *исключение. Ошибка* слишком*исключение. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="3b26f-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="3b26f-134">Удалить Дополнительные сведения из сообщения об ошибке hello для **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="3b26f-135">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="3b26f-135">Constructors</span></span>

* <span data-ttu-id="3b26f-136">Чтобы не принимать *HttpClient* как аргумент конструктора hello конструктор принимает только *HttpClientHandler* или *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="3b26f-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="3b26f-137">Скачанные пакеты</span><span class="sxs-lookup"><span data-stu-id="3b26f-137">Downloaded packages</span></span>

<span data-ttu-id="3b26f-138">Когда клиент обрабатывает зависимость на были загружены следующие hello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="3b26f-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="3b26f-139">Предыдущий список пакетов</span><span class="sxs-lookup"><span data-stu-id="3b26f-139">Previous package list</span></span>

* <span data-ttu-id="3b26f-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="3b26f-148">Текущий список пакетов</span><span class="sxs-lookup"><span data-stu-id="3b26f-148">Current package list</span></span>

* <span data-ttu-id="3b26f-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="3b26f-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="3b26f-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="3b26f-152">Изменения в классах</span><span class="sxs-lookup"><span data-stu-id="3b26f-152">Class changes</span></span>

* <span data-ttu-id="3b26f-153">Класс **UnixEpoch** удален.</span><span class="sxs-lookup"><span data-stu-id="3b26f-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="3b26f-154">**Base64UrlConverter** класс переименовывается слишком**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="3b26f-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="3b26f-155">Другие изменения</span><span class="sxs-lookup"><span data-stu-id="3b26f-155">Other changes</span></span>

* <span data-ttu-id="3b26f-156">Для настройки политики повтора операции КВ при временных сбоях hello была добавлена поддержка версии toothis hello API.</span><span class="sxs-lookup"><span data-stu-id="3b26f-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="3b26f-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="3b26f-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="3b26f-158">Для операций hello, которые возвращены *хранилище*, тип возврата hello был класса, который содержит свойства хранилища.</span><span class="sxs-lookup"><span data-stu-id="3b26f-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="3b26f-159">Hello тип возвращаемого значения — теперь *хранилище*.</span><span class="sxs-lookup"><span data-stu-id="3b26f-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="3b26f-160">*PermissionsToKeys* и *PermissionsToSecrets* — изменено на *Permissions.Keys* и *Permissions.Secrets*.</span><span class="sxs-lookup"><span data-stu-id="3b26f-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="3b26f-161">Некоторые hello возвращаемые типы изменения применяются toohello плоскости управления также.</span><span class="sxs-lookup"><span data-stu-id="3b26f-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="3b26f-162">Пакет NuGet Microsoft.Azure.KeyVault.Extensions</span><span class="sxs-lookup"><span data-stu-id="3b26f-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="3b26f-163">пакет Hello разбита слишком**Microsoft.Azure.KeyVault.Extensions** и **Microsoft.Azure.KeyVault.Cryptography** для hello криптографических операций.</span><span class="sxs-lookup"><span data-stu-id="3b26f-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

