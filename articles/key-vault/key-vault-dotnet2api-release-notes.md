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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Хранилище ключей Azure .NET 2.0. Руководство по миграции и заметки о выпуске
Hello следующие примечания и инструкции предназначены для разработчиков, работающих с хранилищем ключей Azure .NET или библиотеки C#. В hello переход с версии toohello 2.0 версии hello 1.0, количество операций обновления были внесены позволит потребуется выполнить определенные действия по миграции в коде, чтобы toobenefit из функциональных улучшений hello и функции дополнения, такие как **хранилища ключей Сертификаты** поддержки.

## <a name="key-vault-certificates"></a>Сертификаты Key Vault

Предоставляет поддержку сертификатов хранилища ключей для управления вашей x509 сертификаты и hello следующие варианты поведения:  

* Позволяет владельцу сертификата toocreate сертификату через процесс создания хранилища ключей или hello Импорт существующего сертификата. Это применимо как для самозаверяющих сертификатов, так и для сертификатов, созданных центром сертификации.
* Позволяет владельцу сертификата хранилища ключей, tooimplement безопасное хранение и управление ими X509 сертификатов без взаимодействия с материал закрытого ключа.  
* Позволяет владельцу сертификата toocreate политику, которая направляет хранилище ключей toomanage hello жизненного цикла сертификата.  
* Позволяет владельцам сертификат tooprovide контактные данные для уведомления о событиях жизненного цикла истечение срока действия и обновления сертификата.  
* Автоматическое обновление с возможностью выбора издателей сертификатов хранилища ключей — партнерских поставщиков сертификатов X509 и центров сертификации.
  
  * Обратите внимание — поставщики партнером и центры также разрешены, но не будет поддерживать hello автоматического обновления компонентов.

## <a name="net-support"></a>Поддержка .NET

* **.NET 4.0** не поддерживается в версии hello 2.0 hello хранилище ключей Azure .NET или библиотеки C#
* **.NET core** поддерживается в версии hello 2.0 hello хранилище ключей Azure .NET или библиотеки C#

## <a name="namespaces"></a>Пространства имен

* Здравствуйте, пространство имен для **моделей** меняется с **Microsoft.Azure.KeyVault** слишком**Microsoft.Azure.KeyVault.Models**.
* Hello **Microsoft.Azure.KeyVault.Internal** удалении пространства имен.
* пространство имен зависимости пакета Azure SDK Hello изменяются с **Hyak.Common** и **Hyak.Common.Internals** слишком**Microsoft.Rest** и  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Изменения в типах

* *Секрет* изменено слишком*SecretBundle*
* *Словарь* изменено слишком*IDictionary*
* *Список<T>, string []* изменено слишком*IList<T>*
* *NextList* изменено слишком *NextPageLink*

## <a name="return-types"></a>Возвращаемые типы

* **KeyList** и **SecretList** возвращают *IPage<T>* вместо *ListKeysResponseMessage*.
* созданный Hello **BackupKeyAsync** вернет *BackupKeyResult* , содержащее *значение* (резервное копирование больших двоичных объектов). Перед hello метод выполнен перенос и возвращение только значение hello.

## <a name="exceptions"></a>Исключения

* *KeyVaultClientException* изменяется слишком*KeyVaultErrorException*
* Ошибка службы Hello изменяется с *исключение. Ошибка* слишком*исключение. Body.Error.Message*.
* Удалить Дополнительные сведения из сообщения об ошибке hello для **[JsonExtensionData]**.

## <a name="constructors"></a>Конструкторы

* Чтобы не принимать *HttpClient* как аргумент конструктора hello конструктор принимает только *HttpClientHandler* или *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Скачанные пакеты

Когда клиент обрабатывает зависимость на были загружены следующие hello хранилища ключей

### <a name="previous-package-list"></a>Предыдущий список пакетов

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>Текущий список пакетов

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>Изменения в классах

* Класс **UnixEpoch** удален.
* **Base64UrlConverter** класс переименовывается слишком**Base64UrlJsonConverter**

## <a name="other-changes"></a>Другие изменения

* Для настройки политики повтора операции КВ при временных сбоях hello была добавлена поддержка версии toothis hello API.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Для операций hello, которые возвращены *хранилище*, тип возврата hello был класса, который содержит свойства хранилища. Hello тип возвращаемого значения — теперь *хранилище*.
* *PermissionsToKeys* и *PermissionsToSecrets* — изменено на *Permissions.Keys* и *Permissions.Secrets*.
* Некоторые hello возвращаемые типы изменения применяются toohello плоскости управления также.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Пакет NuGet Microsoft.Azure.KeyVault.Extensions

* пакет Hello разбита слишком**Microsoft.Azure.KeyVault.Extensions** и **Microsoft.Azure.KeyVault.Cryptography** для hello криптографических операций.

