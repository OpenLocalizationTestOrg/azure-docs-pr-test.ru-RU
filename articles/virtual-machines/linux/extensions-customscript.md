---
title: "пользовательские сценарии aaaRun на виртуальных машинах Linux в Azure | Документы Microsoft"
description: "Автоматизировать настройку виртуальных Машин Linux с помощью hello настраиваемое расширение скриптов"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="b2e24-103">С помощью hello Azure настраиваемое расширение скриптов с виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="b2e24-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="b2e24-104">Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e24-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="b2e24-105">Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления.</span><span class="sxs-lookup"><span data-stu-id="b2e24-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="b2e24-106">Скрипты можно загружается из хранилища Azure или другое доступное расположение в Интернете, или предоставить toohello расширения времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="b2e24-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="b2e24-107">Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2e24-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="b2e24-108">Этот документ описывает, каким образом toouse hello настраиваемое расширение скриптов из hello Azure CLI и шаблона Azure Resource Manager, а также сведения об устранения неполадок в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="b2e24-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="b2e24-109">Конфигурация расширения</span><span class="sxs-lookup"><span data-stu-id="b2e24-109">Extension Configuration</span></span>
<span data-ttu-id="b2e24-110">Конфигурация настраиваемого расширения скриптов Hello указывает расположение скрипта и запустите toobe команда hello.</span><span class="sxs-lookup"><span data-stu-id="b2e24-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="b2e24-111">Эта конфигурация могут храниться в файлах конфигурации, указанные в командной строке hello, или в шаблон диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e24-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="b2e24-112">Конфиденциальные данные могут храниться в защищенной конфигурации, которая шифруются и расшифровываются только hello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b2e24-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="b2e24-113">Защищенная конфигурация Hello удобен для команды выполнения hello содержит секретные данные, например пароля.</span><span class="sxs-lookup"><span data-stu-id="b2e24-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="b2e24-114">Открытая конфигурация</span><span class="sxs-lookup"><span data-stu-id="b2e24-114">Public Configuration</span></span>
<span data-ttu-id="b2e24-115">Схема.</span><span class="sxs-lookup"><span data-stu-id="b2e24-115">Schema:</span></span>

<span data-ttu-id="b2e24-116">**Примечание**. В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="b2e24-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="b2e24-117">Используйте имена hello, как показано ниже tooavoid проблем развертывания.</span><span class="sxs-lookup"><span data-stu-id="b2e24-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="b2e24-118">**commandToExecute**: (обязательно, string) hello tooexecute сценария точки входа</span><span class="sxs-lookup"><span data-stu-id="b2e24-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="b2e24-119">**fileUris**: загружаются hello URL-адреса для toobe файлов (необязательный, массив строк).</span><span class="sxs-lookup"><span data-stu-id="b2e24-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="b2e24-120">**Отметка времени** (необязательный, целое число) использовать это поле только tootrigger повторить hello скрипта, изменив значение этого поля.</span><span class="sxs-lookup"><span data-stu-id="b2e24-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="b2e24-121">Защищенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="b2e24-121">Protected Configuration</span></span>
<span data-ttu-id="b2e24-122">Схема.</span><span class="sxs-lookup"><span data-stu-id="b2e24-122">Schema:</span></span>

<span data-ttu-id="b2e24-123">**Примечание**. В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="b2e24-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="b2e24-124">Используйте имена hello, как показано ниже tooavoid проблем развертывания.</span><span class="sxs-lookup"><span data-stu-id="b2e24-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="b2e24-125">**commandToExecute**: (необязательный, string) hello tooexecute сценария точки входа.</span><span class="sxs-lookup"><span data-stu-id="b2e24-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="b2e24-126">Используйте это поле, если команда содержит секретные данные, например пароли.</span><span class="sxs-lookup"><span data-stu-id="b2e24-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="b2e24-127">**storageAccountName**: (необязательный, string) hello имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b2e24-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="b2e24-128">Если указаны учетные данные, все значения fileUris должны иметь формат URL-адресов для BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e24-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="b2e24-129">**storageAccountKey**: (необязательный, string) hello ключа доступа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b2e24-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="b2e24-130">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b2e24-130">Azure CLI</span></span>
<span data-ttu-id="b2e24-131">При использовании hello Azure CLI toorun hello настраиваемое расширение скриптов, создайте файл конфигурации или файлов, содержащих uri файла минимального hello и hello команды выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="b2e24-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b2e24-132">При необходимости hello можно задать параметры в команде hello как строка в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b2e24-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="b2e24-133">Это позволяет toobe hello конфигурации, заданные во время выполнения и без отдельный файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b2e24-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="b2e24-134">Примеры использования интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b2e24-134">Azure CLI Examples</span></span>

<span data-ttu-id="b2e24-135">**Пример 1** — открытая конфигурация с файлом сценария.</span><span class="sxs-lookup"><span data-stu-id="b2e24-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="b2e24-136">Команда интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="b2e24-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b2e24-137">**Пример 2** — открытая конфигурация без файла сценария.</span><span class="sxs-lookup"><span data-stu-id="b2e24-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="b2e24-138">Команда интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="b2e24-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b2e24-139">**Пример 3** — файл открытой конфигурации файла скрипта используется toospecify hello URI, который файл защищенной конфигурации используется toospecify hello команда toobe выполнена.</span><span class="sxs-lookup"><span data-stu-id="b2e24-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="b2e24-140">Файл открытой конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b2e24-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="b2e24-141">Файл защищенной конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b2e24-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="b2e24-142">Команда интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="b2e24-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="b2e24-143">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2e24-143">Resource Manager Template</span></span>
<span data-ttu-id="b2e24-144">Hello Azure настраиваемое расширение скриптов может выполняться во время развертывания виртуальной машины с помощью шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b2e24-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="b2e24-145">Таким образом, toodo добавить шаблон развертывания toohello правильно отформатированную JSON.</span><span class="sxs-lookup"><span data-stu-id="b2e24-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="b2e24-146">Примеры использования Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2e24-146">Resource Manager Examples</span></span>
<span data-ttu-id="b2e24-147">**Пример 1** — открытая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="b2e24-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="b2e24-148">**Пример 2** — команда выполнения в защищенной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b2e24-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="b2e24-149">Разделе hello .net Core Music Store Демонстрация полный пример - [Демонстрация хранилища Музыка](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="b2e24-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b2e24-150">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b2e24-150">Troubleshooting</span></span>
<span data-ttu-id="b2e24-151">При запуске hello настраиваемое расширение скриптов hello скрипт создается или загружать их в аналогичные toohello каталог, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="b2e24-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="b2e24-152">выходные данные команды Hello также сохраняется в этот каталог в `stdout` и `stderr` файла.</span><span class="sxs-lookup"><span data-stu-id="b2e24-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="b2e24-153">Hello расширение сценария Azure создает журнал, который можно найти здесь.</span><span class="sxs-lookup"><span data-stu-id="b2e24-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="b2e24-154">также можно получить состояние выполнения Hello hello настраиваемое расширение скриптов с hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b2e24-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="b2e24-155">Hello вывод выглядит следующим образом после текста hello.</span><span class="sxs-lookup"><span data-stu-id="b2e24-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="b2e24-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2e24-156">Next Steps</span></span>
<span data-ttu-id="b2e24-157">Сведения о других расширениях сценариев для виртуальной машины см. в статье [Обзор расширений и компонентов виртуальной машины](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2e24-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

