---
title: "Развертывание виртуальной Машины с паролем, безопасно хранящиеся на стек Azure | Документы Microsoft"
description: "Дополнительные сведения о развертывании ВМ с помощью пароля, хранящихся в хранилище ключей Azure стека"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: 3292a2dfefc17e5034c66122a3eab24d6c03e694
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a><span data-ttu-id="d9916-103">Создание виртуальной машины путем извлечения пароля, хранящихся в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="d9916-103">Create a virtual machine by retrieving the password stored in a Key Vault</span></span>

<span data-ttu-id="d9916-104">При необходимости передачи безопасное значение, таких как пароль во время развертывания, можно хранить значения как секрет в хранилище ключей Azure стека и ссылаться на него в шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9916-104">When you need to pass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in the Azure Resource Manager templates.</span></span> <span data-ttu-id="d9916-105">Вам не нужно вручную ввести секретный код при каждом развертывании ресурсов, можно также указать пользователей, которые или субъекты-службы можно получить доступ к секрета.</span><span class="sxs-lookup"><span data-stu-id="d9916-105">You do not need to manually enter the secret each time you deploy the resources, you can also specify which users or service principals can access the secret.</span></span> 

<span data-ttu-id="d9916-106">В этой статье мы рассмотрим шаги, необходимые для развертывания виртуальной машины Windows Azure стека, получая пароль, который хранится в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d9916-106">In this article, we walk you through the steps required to deploy a Windows virtual machine in Azure Stack by retrieving the password that is stored in a Key Vault.</span></span> <span data-ttu-id="d9916-107">Поэтому пароль никогда не помещается в виде обычного текста в файле параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="d9916-107">Therefore the password is never put in plain text in the template parameter file.</span></span> <span data-ttu-id="d9916-108">Можно использовать следующие действия из пакета средств разработки стек Azure или из внешнего клиента при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="d9916-108">You can use these steps either from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9916-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9916-109">Prerequisites</span></span>
 
* <span data-ttu-id="d9916-110">Необходимо необходимо подписаться на предложение, которая включает службу хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d9916-110">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="d9916-111">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d9916-111">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="d9916-112">Настройка среды PowerShell пользователя Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d9916-112">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="d9916-113">Следующие шаги описывают процесс, необходимый для создания виртуальной машины, получая пароль, которые хранятся в хранилище ключей:</span><span class="sxs-lookup"><span data-stu-id="d9916-113">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="d9916-114">Создание секрета хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d9916-114">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="d9916-115">Обновите файл azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="d9916-115">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="d9916-116">Разверните шаблон.</span><span class="sxs-lookup"><span data-stu-id="d9916-116">Deploy the template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="d9916-117">Создание секрета хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="d9916-117">Create a Key Vault secret</span></span>

<span data-ttu-id="d9916-118">Следующий скрипт создает хранилище ключей и сохраняет пароль в виде секрета хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d9916-118">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="d9916-119">Используйте `-EnabledForDeployment` параметр при создании хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d9916-119">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="d9916-120">Этот параметр гарантирует, что хранилище ключей можно ссылаться с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d9916-120">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

<span data-ttu-id="d9916-121">При выполнении предыдущего сценария выходные данные содержат секретный URI.</span><span class="sxs-lookup"><span data-stu-id="d9916-121">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="d9916-122">Запишите этот URI.</span><span class="sxs-lookup"><span data-stu-id="d9916-122">Make a note of this URI.</span></span> <span data-ttu-id="d9916-123">Вам нужно сослаться на него в [развертывание Windows виртуальной машины с паролем в хранилище ключей шаблона](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span><span class="sxs-lookup"><span data-stu-id="d9916-123">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span></span> <span data-ttu-id="d9916-124">Загрузить [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) папки на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="d9916-124">Download the [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) folder onto your development computer.</span></span> <span data-ttu-id="d9916-125">Эта папка содержит `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые требуется в следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="d9916-125">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="d9916-126">Изменить `azuredeploy.parameters.json` файл в соответствии с вашей среды значения.</span><span class="sxs-lookup"><span data-stu-id="d9916-126">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="d9916-127">Особый интерес имеют имя хранилища, группа ресурсов хранилища и секретный код URI (как созданных в ходе предыдущего сценария).</span><span class="sxs-lookup"><span data-stu-id="d9916-127">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="d9916-128">Следующий файл приведен пример файла параметров:</span><span class="sxs-lookup"><span data-stu-id="d9916-128">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="d9916-129">Обновить файл azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="d9916-129">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="d9916-130">Измените файл azuredeploy.parameters.json KeyVault, URI, secretName adminUsername значений виртуальной машины в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="d9916-130">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="d9916-131">Следующий файл JSON показан пример файла параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="d9916-131">The following JSON file shows an example of the template parameters file:</span></span> 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a><span data-ttu-id="d9916-132">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="d9916-132">Template deployment</span></span>

<span data-ttu-id="d9916-133">Теперь можно разверните шаблон с помощью следующего сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d9916-133">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
<span data-ttu-id="d9916-134">При развертывании шаблона произведут следующий результат:</span><span class="sxs-lookup"><span data-stu-id="d9916-134">When the template is deployed successfully, it results in the following output:</span></span>

![Выходные данные развертывания](media/azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="d9916-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9916-136">Next steps</span></span>
[<span data-ttu-id="d9916-137">Развертывание примера приложения с хранилищем ключей</span><span class="sxs-lookup"><span data-stu-id="d9916-137">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="d9916-138">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="d9916-138">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

