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
# <a name="require-secure-transfer"></a><span data-ttu-id="fdde1-103">Требование безопасной передачи</span><span class="sxs-lookup"><span data-stu-id="fdde1-103">Require secure transfer</span></span>

<span data-ttu-id="fdde1-104">Параметр "Требуется безопасное перемещение" повышает безопасность учетной записи хранения, разрешая выполнять к ней запросы, отправленные только посредством безопасных подключений.</span><span class="sxs-lookup"><span data-stu-id="fdde1-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="fdde1-105">Например, при вызове интерфейсов REST API для доступа к своей учетной записи хранения необходимо подключиться с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fdde1-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="fdde1-106">Если включен параметр "Требуется безопасное перемещение", то любые запросы с помощью протокола HTTP отклоняются.</span><span class="sxs-lookup"><span data-stu-id="fdde1-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="fdde1-107">Кроме того, если этот параметр включен, то при использовании службы файлов Azure любое подключение без шифрования завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="fdde1-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="fdde1-108">Это относится к сценариям, включающим в себя SMB 2.1, SMB 3.0 без шифрования и некоторые конфигурации SMB-клиента Linux.</span><span class="sxs-lookup"><span data-stu-id="fdde1-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="fdde1-109">По умолчанию параметр "Требуется безопасное перемещение" отключен.</span><span class="sxs-lookup"><span data-stu-id="fdde1-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="fdde1-110">Так как служба хранилища Azure не поддерживает протокол HTTPS для имен личных доменов, при использовании данных имен этот параметр не применяется.</span><span class="sxs-lookup"><span data-stu-id="fdde1-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="fdde1-111">Включение параметра "Требуется безопасное перемещение" на портале Azure</span><span class="sxs-lookup"><span data-stu-id="fdde1-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="fdde1-112">Параметр "Требуется безопасное перемещение" можно включить как при создании учетной записи хранения на [портале Azure](https://portal.azure.com), так и для существующих учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="fdde1-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="fdde1-113">Включение требования безопасной передачи при создании учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="fdde1-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="fdde1-114">Откройте колонку **Создание учетной записи хранения** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde1-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="fdde1-115">В разделе **Требуется безопасное перемещение** щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="fdde1-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="fdde1-117">Включение требования безопасной передачи для существующей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="fdde1-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="fdde1-118">Выберите учетную запись хранения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde1-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="fdde1-119">Щелкните **Конфигурация** в разделе **Параметры** в колонке меню учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fdde1-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="fdde1-120">В разделе **Требуется безопасное перемещение** щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="fdde1-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="fdde1-122">Включение параметра "Требуется безопасное перемещение" программным способом</span><span class="sxs-lookup"><span data-stu-id="fdde1-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="fdde1-123">Имя параметра в свойствах учетной записи хранения — _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="fdde1-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="fdde1-124">Вы можете включить параметр "Требуется безопасное перемещение" с помощью REST API, инструментов или библиотек:</span><span class="sxs-lookup"><span data-stu-id="fdde1-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="fdde1-125">**REST API** (версия 2016-12-01): [пакет выпуска](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts);</span><span class="sxs-lookup"><span data-stu-id="fdde1-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="fdde1-126">**PowerShell** (версия 4.1.0): [пакет выпуска](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0);</span><span class="sxs-lookup"><span data-stu-id="fdde1-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="fdde1-127">**интерфейс командной строки** (версия 2.0.11): [пакет выпуска](https://pypi.python.org/pypi/azure-cli-storage/2.0.11);</span><span class="sxs-lookup"><span data-stu-id="fdde1-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="fdde1-128">**NodeJS** (версия 1.1.0): [пакет выпуска](https://www.npmjs.com/package/azure-arm-storage/);</span><span class="sxs-lookup"><span data-stu-id="fdde1-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="fdde1-129">**пакет SDK для .NET** (версия 6.3.0): [пакет выпуска](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview);</span><span class="sxs-lookup"><span data-stu-id="fdde1-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="fdde1-130">**пакет SDK для Python** (версия 1.1.0): [пакет выпуска](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0);</span><span class="sxs-lookup"><span data-stu-id="fdde1-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="fdde1-131">**пакет SDK для Ruby** (версия 0.11.0): [пакет выпуска](https://rubygems.org/gems/azure_mgmt_storage).</span><span class="sxs-lookup"><span data-stu-id="fdde1-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="fdde1-132">Включение параметра "Требуется безопасное перемещение" с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="fdde1-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="fdde1-133">Чтобы упростить тестирование с помощью REST API, можно использовать [ArmClient](https://github.com/projectkudu/ARMClient) для вызова из командной строки.</span><span class="sxs-lookup"><span data-stu-id="fdde1-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="fdde1-134">Для проверки параметра с помощью REST API можно использовать командную строку ниже:</span><span class="sxs-lookup"><span data-stu-id="fdde1-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="fdde1-135">В ответе можно найти параметр _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="fdde1-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="fdde1-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="fdde1-136">Sample:</span></span>

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

<span data-ttu-id="fdde1-137">Для включения параметра с помощью REST API можно использовать командную строку ниже:</span><span class="sxs-lookup"><span data-stu-id="fdde1-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="fdde1-138">Пример Input.json:</span><span class="sxs-lookup"><span data-stu-id="fdde1-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="fdde1-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fdde1-139">Next steps</span></span>
<span data-ttu-id="fdde1-140">Служба хранилища Azure предоставляет полный набор возможностей обеспечения безопасности, которые в совокупности позволяют разработчикам создавать защищенные приложения.</span><span class="sxs-lookup"><span data-stu-id="fdde1-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="fdde1-141">Дополнительные сведения см. в [руководстве по безопасности службы хранилища](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="fdde1-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
