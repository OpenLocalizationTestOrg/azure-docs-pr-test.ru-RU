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
# <a name="require-secure-transfer"></a><span data-ttu-id="17f0d-103">Требование безопасной передачи</span><span class="sxs-lookup"><span data-stu-id="17f0d-103">Require secure transfer</span></span>

<span data-ttu-id="17f0d-104">параметр Hello» безопасной передачи требуется» повышает безопасность hello учетной записи только разрешение запросов toohello учетную запись хранения из безопасных соединений.</span><span class="sxs-lookup"><span data-stu-id="17f0d-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="17f0d-105">Например при вызове API-интерфейс REST tooaccess вашей учетной записи хранилища, необходимо подключиться с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="17f0d-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="17f0d-106">Если включен параметр "Требуется безопасное перемещение", то любые запросы с помощью протокола HTTP отклоняются.</span><span class="sxs-lookup"><span data-stu-id="17f0d-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="17f0d-107">При использовании службы файлов Azure hello любое соединение без шифрования происходит сбой при включении «Защита передачи, требуемая».</span><span class="sxs-lookup"><span data-stu-id="17f0d-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="17f0d-108">К ним относятся сценарии с использованием SMB 2.1, SMB 3.0 без шифрования и некоторые виды hello Linux SMB-клиент.</span><span class="sxs-lookup"><span data-stu-id="17f0d-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="17f0d-109">По умолчанию hello» безопасной передачи требуется» параметр будет отключен.</span><span class="sxs-lookup"><span data-stu-id="17f0d-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="17f0d-110">Так как служба хранилища Azure не поддерживает протокол HTTPS для имен личных доменов, при использовании данных имен этот параметр не применяется.</span><span class="sxs-lookup"><span data-stu-id="17f0d-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="17f0d-111">Включить «Необходимые безопасной передачи» в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="17f0d-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="17f0d-112">Можно включить hello» безопасной передачи требуется» присвоение значения, и при создании учетной записи хранилища в hello [портал Azure](https://portal.azure.com)и для существующих учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="17f0d-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="17f0d-113">Включение требования безопасной передачи при создании учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="17f0d-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="17f0d-114">Откройте hello **создать учетную запись хранения** колонки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="17f0d-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="17f0d-115">В разделе **Требуется безопасное перемещение** щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="17f0d-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="17f0d-117">Включение требования безопасной передачи для существующей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="17f0d-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="17f0d-118">Выберите существующую учетную запись хранения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="17f0d-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="17f0d-119">Выберите **конфигурации** под **параметры** в колонке меню учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="17f0d-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="17f0d-120">В разделе **Требуется безопасное перемещение** щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="17f0d-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Снимок экрана](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="17f0d-122">Включение параметра "Требуется безопасное перемещение" программным способом</span><span class="sxs-lookup"><span data-stu-id="17f0d-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="17f0d-123">Имя параметра Hello _supportsHttpsTrafficOnly_ в свойства учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="17f0d-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="17f0d-124">Вы можете включить параметр "Требуется безопасное перемещение" с помощью REST API, инструментов или библиотек:</span><span class="sxs-lookup"><span data-stu-id="17f0d-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="17f0d-125">**REST API** (версия 2016-12-01): [пакет выпуска](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts);</span><span class="sxs-lookup"><span data-stu-id="17f0d-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="17f0d-126">**PowerShell** (версия 4.1.0): [пакет выпуска](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0);</span><span class="sxs-lookup"><span data-stu-id="17f0d-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="17f0d-127">**интерфейс командной строки** (версия 2.0.11): [пакет выпуска](https://pypi.python.org/pypi/azure-cli-storage/2.0.11);</span><span class="sxs-lookup"><span data-stu-id="17f0d-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="17f0d-128">**NodeJS** (версия 1.1.0): [пакет выпуска](https://www.npmjs.com/package/azure-arm-storage/);</span><span class="sxs-lookup"><span data-stu-id="17f0d-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="17f0d-129">**пакет SDK для .NET** (версия 6.3.0): [пакет выпуска](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview);</span><span class="sxs-lookup"><span data-stu-id="17f0d-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="17f0d-130">**пакет SDK для Python** (версия 1.1.0): [пакет выпуска](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0);</span><span class="sxs-lookup"><span data-stu-id="17f0d-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="17f0d-131">**пакет SDK для Ruby** (версия 0.11.0): [пакет выпуска](https://rubygems.org/gems/azure_mgmt_storage).</span><span class="sxs-lookup"><span data-stu-id="17f0d-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="17f0d-132">Включение параметра "Требуется безопасное перемещение" с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="17f0d-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="17f0d-133">toosimplify тестирование с помощью API-интерфейса REST, можно использовать [ArmClient](https://github.com/projectkudu/ARMClient) toocall из командной строки.</span><span class="sxs-lookup"><span data-stu-id="17f0d-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="17f0d-134">Можно использовать меньше значения hello toocheck командной строки с hello REST API.</span><span class="sxs-lookup"><span data-stu-id="17f0d-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="17f0d-135">В ответ hello можно найти _supportsHttpsTrafficOnly_ параметр.</span><span class="sxs-lookup"><span data-stu-id="17f0d-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="17f0d-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="17f0d-136">Sample:</span></span>

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

<span data-ttu-id="17f0d-137">Можно использовать меньше значения hello tooenable командной строки с hello REST API.</span><span class="sxs-lookup"><span data-stu-id="17f0d-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="17f0d-138">Пример Input.json:</span><span class="sxs-lookup"><span data-stu-id="17f0d-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="17f0d-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17f0d-139">Next steps</span></span>
<span data-ttu-id="17f0d-140">Хранилище Azure предоставляет полный набор возможностей безопасности, которые вместе позволяют разработчикам toobuild безопасных приложений.</span><span class="sxs-lookup"><span data-stu-id="17f0d-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="17f0d-141">Для получения дополнительных сведений посетите hello [руководство по безопасности хранилища](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="17f0d-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
