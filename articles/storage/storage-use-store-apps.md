---
title: "Использование службы хранилища Azure в приложениях Магазина Windows | Документация Майкрософт"
description: "Узнайте, как создать приложение магазина Windows, которое использует BLOB-объекты, очереди, таблицы или хранилище файлов Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a>Использование службы хранилища Azure в приложениях Магазина Windows
## <a name="overview"></a>Обзор
В этом руководстве показано, как начать разработку приложения Магазина Windows, использующего хранилище Azure.

## <a name="download-required-tools"></a>Скачивание необходимых средств
* [Visual Studio](https://www.visualstudio.com/downloads/) упрощает процесс сборки, отладки, локализации, упаковки и развертывания приложений Магазина Windows. Требуется Visual Studio 2012 или более поздней версии.
* [Клиентская библиотека хранилища Microsoft Azure](https://www.nuget.org/packages/WindowsAzure.Storage) предоставляет библиотеку классов среды выполнения Windows для работы со службой хранилища Azure.
* [Инструменты служб данных WCF для приложений Магазина Windows](http://www.microsoft.com/download/details.aspx?id=30714) расширяют возможности добавления ссылки на службу за счет поддержки OData на стороне клиента для приложений Магазина Windows в Visual Studio.

## <a name="develop-apps"></a>Разработка приложений
### <a name="getting-ready"></a>Подготовка
Создайте новый проект приложения Магазина Windows в Visual Studio 2012 или более поздней версии:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Затем добавьте ссылку на клиентскую библиотеку службы хранилища Azure. Для этого щелкните правой кнопкой мыши элемент **Ссылки**, выберите пункт **Добавить ссылку** и перейдите к скачанной клиентской библиотеке хранилища для среды выполнения Windows:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a>Использование библиотеки со службами BLOB-объектов и очередей
На этом этапе приложение готово к вызову служб BLOB-объектов и очередей Azure. Добавьте следующие операторы **using** , чтобы можно было напрямую ссылаться на типы хранилища Azure:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Далее, добавьте кнопку на страницу. Добавьте следующий код к ее событию **Click** и измените метод обработчика событий с помощью [ключевого слова async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

В этом коде предполагается, что у вас есть две строковые переменные *accountName* и *accountKey*. Они представляют собой имя вашей учетной записи хранения и связанный ней ключ.

Создайте и запустите приложение. Нажав кнопку, вы сможете проверить свою учетную запись на наличие контейнера с именем *container1* и создать его в случае отсутствия.

### <a name="using-the-library-with-the-table-service"></a>Использование библиотеки со службой таблиц
Типы, используемые для связи со службой таблиц Azure, зависят от служб данных WCF для библиотеки приложений Магазина Windows. Добавьте ссылку на необходимые библиотеки WCF с помощью консоли диспетчера пакетов:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Используйте следующую команду для направление диспетчера пакетов к определенному месту в вашем компьютере:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Эта команда автоматически добавляет все необходимые ссылки на проект. Кроме того, вы можете добавить папку NuGet служб данных WCF на локальном компьютере в список источников пакетов, а затем добавить ссылку через пользовательский интерфейс, как описано в разделе [Управление пакетами NuGet с помощью диалогового окна](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

После создания ссылки на NuGet-пакет службы данных WCF измените код события **Click** вашей кнопки:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Этот код позволяет проверить учетную запись на наличие таблицы с именем *table1* и создать ее в случае отсутствия.

Вы также можете добавить ссылку на библиотеку Microsoft.WindowsAzure.Storage.Table.dll, которая находится в том же скачанном пакете. Она содержит дополнительные возможности, такие как сериализация на основе отражения и общие запросы. Обратите внимание, что эта библиотека не поддерживает JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
