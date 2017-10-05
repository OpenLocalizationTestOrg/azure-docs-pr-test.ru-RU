---
title: "Требование безопасной передачи в службе хранилища Azure | Документация Майкрософт"
description: "Узнайте о функции требования безопасной передачи для службы хранилища Azure и о том, как ее включить."
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
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="require-secure-transfer"></a>Требование безопасной передачи

Параметр "Требуется безопасное перемещение" повышает безопасность учетной записи хранения, разрешая выполнять к ней запросы, отправленные только посредством безопасных подключений. Например, при вызове интерфейсов REST API для доступа к своей учетной записи хранения необходимо подключиться с помощью протокола HTTPS. Если включен параметр "Требуется безопасное перемещение", то любые запросы с помощью протокола HTTP отклоняются.

Кроме того, если этот параметр включен, то при использовании службы файлов Azure любое подключение без шифрования завершается сбоем. Это относится к сценариям, включающим в себя SMB 2.1, SMB 3.0 без шифрования и некоторые конфигурации SMB-клиента Linux. 

По умолчанию параметр "Требуется безопасное перемещение" отключен.

> [!NOTE]
> Так как служба хранилища Azure не поддерживает протокол HTTPS для имен личных доменов, при использовании данных имен этот параметр не применяется.

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a>Включение параметра "Требуется безопасное перемещение" на портале Azure

Параметр "Требуется безопасное перемещение" можно включить как при создании учетной записи хранения на [портале Azure](https://portal.azure.com), так и для существующих учетных записей хранения.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Включение требования безопасной передачи при создании учетной записи хранения

1. Откройте колонку **Создание учетной записи хранения** на портале Azure.
1. В разделе **Требуется безопасное перемещение** щелкните **Включено**.

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Включение требования безопасной передачи для существующей учетной записи хранения

1. Выберите учетную запись хранения на портале Azure.
1. Щелкните **Конфигурация** в разделе **Параметры** в колонке меню учетной записи хранения.
1. В разделе **Требуется безопасное перемещение** щелкните **Включено**.

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Включение параметра "Требуется безопасное перемещение" программным способом

Имя параметра в свойствах учетной записи хранения — _supportsHttpsTrafficOnly_. Вы можете включить параметр "Требуется безопасное перемещение" с помощью REST API, инструментов или библиотек:

* **REST API** (версия 2016-12-01): [пакет выпуска](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts);
* **PowerShell** (версия 4.1.0): [пакет выпуска](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0);
* **интерфейс командной строки** (версия 2.0.11): [пакет выпуска](https://pypi.python.org/pypi/azure-cli-storage/2.0.11);
* **NodeJS** (версия 1.1.0): [пакет выпуска](https://www.npmjs.com/package/azure-arm-storage/);
* **пакет SDK для .NET** (версия 6.3.0): [пакет выпуска](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview);
* **пакет SDK для Python** (версия 1.1.0): [пакет выпуска](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0);
* **пакет SDK для Ruby** (версия 0.11.0): [пакет выпуска](https://rubygems.org/gems/azure_mgmt_storage).

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Включение параметра "Требуется безопасное перемещение" с помощью REST API

Чтобы упростить тестирование с помощью REST API, можно использовать [ArmClient](https://github.com/projectkudu/ARMClient) для вызова из командной строки.

 Для проверки параметра с помощью REST API можно использовать командную строку ниже:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

В ответе можно найти параметр _supportsHttpsTrafficOnly_. Пример:

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

Для включения параметра с помощью REST API можно использовать командную строку ниже:

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
Служба хранилища Azure предоставляет полный набор возможностей обеспечения безопасности, которые в совокупности позволяют разработчикам создавать защищенные приложения. Дополнительные сведения см. в [руководстве по безопасности службы хранилища](storage-security-guide.md).
