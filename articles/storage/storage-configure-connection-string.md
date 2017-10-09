---
title: "aaaConfigure строку подключения для хранилища Azure | Документы Microsoft"
description: "Настройка строки подключения для учетной записи хранения Azure. Строка подключения содержит сведения о hello необходимый tooauthenticate доступа учетной записи хранилища tooa из приложения во время выполнения."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Настройка строк подключения службы хранилища Azure

Строка подключения содержит hello сведения проверки подлинности, необходимые для tooaccess данных приложения в учетной записи хранилища Azure во время выполнения. Настройка строки подключения позволяет выполнить следующие действия:

* Подключите toohello эмулятор хранилища Azure.
* получить доступ к учетной записи хранения в Azure;
* получить доступ к указанным ресурсам Azure через подписанный URL-адрес (SAS).

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Хранение строки подключения
Вашему приложению требуется строка подключения tooaccess hello в среды выполнения tooauthenticate запросов, сделанных tooAzure хранилища. Есть несколько вариантов для хранения строки подключения.

* Приложения, запущенного на рабочем столе hello, или на устройстве можно хранить строки подключения hello в **app.config** или **web.config** файла. Добавить toohello строка подключения hello **AppSettings** раздел в этих файлах.
* Приложение, работающее в облачную службу Azure можно хранить строки подключения hello в hello [файл схемы (.cscfg) конфигурации службы Azure](https://msdn.microsoft.com/library/ee758710.aspx). Добавить toohello строка подключения hello **ConfigurationSettings** раздел файла конфигурации службы hello.
* Можно использовать строку подключения непосредственно в коде. Однако в большинстве случаев рекомендуется хранить строку подключения в файле конфигурации.

Хранение строки подключения в файле конфигурации упрощает tooswitch строка подключения легко tooupdate hello между эмулятором хранилища hello и учетная запись хранилища Azure в облаке hello. Требуется только tooedit hello строка подключения toopoint tooyour целевой среды.

Можно использовать hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess в строке подключения во время выполнения независимо от того, где выполняется приложение.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Создать строку подключения для эмулятора хранилища hello
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Дополнительные сведения о эмулятор хранилища hello. в разделе [использовать эмулятор хранилища Azure hello для разработки и тестирования](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Создание строки подключения для учетной записи хранения Azure
toocreate строку подключения для вашей учетной записи хранилища Azure, используйте hello следующий формат. Указать, нужно ли учетная запись хранения toohello tooconnect по протоколу HTTPS (рекомендуется) или HTTP, замените `myAccountName` с именем hello своей учетной записи хранилища, а `myAccountKey` с помощью ключа доступа учетной записи:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Например, строка подключения может выглядеть так:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Служба хранилища Azure поддерживает в строке подключения как HTTP, так и HTTPS, однако *настоятельно рекомендуется использовать HTTPS*.

> [!TIP]
> Строки подключения учетной записи хранилища можно найти в hello [портал Azure](https://portal.azure.com). Перейдите в слишком**параметры** > **ключи доступа** в строках соединения toosee колонке меню вашей учетной записи хранилища для обоих первичный и вторичный ключи доступа.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Создание строки подключения с помощью подписанного URL-адреса
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Создание строки подключения для явной конечной точки хранилища
Конечные точки службы для явного можно указать в строке подключения вместо использования конечных точек по умолчанию hello. toocreate строка подключения, указывающая явная конечная точка hello полную конечную точку для каждой службы, включая спецификации протокола hello (HTTPS (рекомендуется) или HTTP), укажите в hello следующий формат:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Один сценарий, где вы можете toospecify явная конечная точка — когда сопоставленной вашей tooa конечной точке хранилища больших двоичных объектов [пользовательского домена](storage-custom-domain-name.md). В этом случае в строке подключения можно указать пользовательскую конечную точку хранилища BLOB-объектов. При необходимости можно hello конечные точки по умолчанию для hello другие службы, если приложение использует их.

Ниже приведен пример строки подключения, указывающее явная конечная точка для hello службы BLOB-объектов:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

Этот пример определяет явные конечные точки для всех служб, включая пользовательский домен для hello службы BLOB-объектов:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

Hello конечной точки значения в строке подключения используется tooconstruct hello запроса служб хранилища toohello идентификаторы URI и определяют форму всех URI-адресов, которые возвращаются tooyour кода hello.

Если сопоставлена пользовательского домена хранилища tooa конечной точки и опустить этой конечной точки из строки подключения, то нельзя будет toouse соединения строковые данные tooaccess службы из кода.

> [!IMPORTANT]
> Значения конечных точек служб в строках подключения должны быть в формате правильно сформированного универсального кода ресурса (URI), включая `https://` (рекомендуется) или `http://`. Так как хранилище Azure еще не поддерживает протокол HTTPS для пользовательских доменов вы *должен* укажите `http://` для любой конечной точки URI, указывающий tooa пользовательского домена.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Создание строки подключения с суффиксом конечной точки
toocreate строка соединения для службы хранилища в регионах или экземпляров с другой конечной точке суффиксов, например для Китая Azure или Azure для государственных, hello используйте следующий формат строки соединения. Указать, нужно ли учетная запись хранения toohello tooconnect по протоколу HTTPS (рекомендуется) или HTTP, замените `myAccountName` hello имя вашей учетной записи хранилища, замените `myAccountKey` с помощью ключа доступа учетной записи и замените `mySuffix` с hello URI суффикс:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Ниже приведен пример строки подключения для служб хранилища в Azure для Китая.

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Анализ строки подключения
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
* [Используйте hello эмулятор хранилища Azure для разработки и тестирования](storage-use-emulator.md)
* [Клиентские инструменты службы хранилища Azure](storage-explorers.md)
* [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md)

