---
title: "aaaRequire безопасной передачи в хранилище Azure | Документы Microsoft"
description: "Дополнительные сведения о функции «Требовать безопасной передачи» hello для хранилища Azure и как tooenable его."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Требование безопасной передачи

параметр Hello» безопасной передачи требуется» повышает безопасность hello учетной записи только разрешение запросов toohello учетную запись хранения из безопасных соединений. Например при вызове API-интерфейс REST tooaccess вашей учетной записи хранилища, необходимо подключиться с помощью протокола HTTPS. Если включен параметр "Требуется безопасное перемещение", то любые запросы с помощью протокола HTTP отклоняются.

При использовании службы файлов Azure hello любое соединение без шифрования происходит сбой при включении «Защита передачи, требуемая». К ним относятся сценарии с использованием SMB 2.1, SMB 3.0 без шифрования и некоторые виды hello Linux SMB-клиент. 

По умолчанию hello» безопасной передачи требуется» параметр будет отключен.

> [!NOTE]
> Так как служба хранилища Azure не поддерживает протокол HTTPS для имен личных доменов, при использовании данных имен этот параметр не применяется.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Включить «Необходимые безопасной передачи» в hello портал Azure

Можно включить hello» безопасной передачи требуется» присвоение значения, и при создании учетной записи хранилища в hello [портал Azure](https://portal.azure.com)и для существующих учетных записей хранилища.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Включение требования безопасной передачи при создании учетной записи хранения

1. Откройте hello **создать учетную запись хранения** колонки в hello портал Azure.
1. В разделе **Требуется безопасное перемещение** щелкните **Включено**.

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Включение требования безопасной передачи для существующей учетной записи хранения

1. Выберите существующую учетную запись хранения в hello портал Azure.
1. Выберите **конфигурации** под **параметры** в колонке меню учетной записи хранилища hello.
1. В разделе **Требуется безопасное перемещение** щелкните **Включено**.

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Включение параметра "Требуется безопасное перемещение" программным способом

Имя параметра Hello _supportsHttpsTrafficOnly_ в свойства учетной записи хранения. Вы можете включить параметр "Требуется безопасное перемещение" с помощью REST API, инструментов или библиотек:

* **REST API** (версия 2016-12-01): [пакет выпуска](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts);
* **PowerShell** (версия 4.1.0): [пакет выпуска](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0);
* **интерфейс командной строки** (версия 2.0.11): [пакет выпуска](https://pypi.python.org/pypi/azure-cli-storage/2.0.11);
* **NodeJS** (версия 1.1.0): [пакет выпуска](https://www.npmjs.com/package/azure-arm-storage/);
* **пакет SDK для .NET** (версия 6.3.0): [пакет выпуска](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview);
* **пакет SDK для Python** (версия 1.1.0): [пакет выпуска](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0);
* **пакет SDK для Ruby** (версия 0.11.0): [пакет выпуска](https://rubygems.org/gems/azure_mgmt_storage).

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Включение параметра "Требуется безопасное перемещение" с помощью REST API

toosimplify тестирование с помощью API-интерфейса REST, можно использовать [ArmClient](https://github.com/projectkudu/ARMClient) toocall из командной строки.

 Можно использовать меньше значения hello toocheck командной строки с hello REST API.

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

В ответ hello можно найти _supportsHttpsTrafficOnly_ параметр. Пример:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

Можно использовать меньше значения hello tooenable командной строки с hello REST API.

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Пример Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Дальнейшие действия
Хранилище Azure предоставляет полный набор возможностей безопасности, которые вместе позволяют разработчикам toobuild безопасных приложений. Для получения дополнительных сведений посетите hello [руководство по безопасности хранилища](storage-security-guide.md).
