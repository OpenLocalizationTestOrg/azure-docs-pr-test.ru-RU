---
title: "aaaDeploy ВМ с паролем, безопасно хранящиеся на стек Azure | Документы Microsoft"
description: "Узнайте, как toodeploy ВМ с помощью пароля хранятся в хранилище ключей Azure стека"
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
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a><span data-ttu-id="9bd17-103">Создание виртуальной машины, получая hello пароль, которые хранятся в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="9bd17-103">Create a virtual machine by retrieving hello password stored in a Key Vault</span></span>

<span data-ttu-id="9bd17-104">При необходимости toopass безопасное значение, таких как пароль во время развертывания, можно хранить значения как секрет в хранилище ключей Azure стека и ссылаться на него в шаблоны Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-104">When you need toopass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in hello Azure Resource Manager templates.</span></span> <span data-ttu-id="9bd17-105">Нет необходимости toomanually введите секрет hello при каждом развертывании hello ресурсы, можно также указать, какие пользователи или субъекты-службы доступа к секрет hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-105">You do not need toomanually enter hello secret each time you deploy hello resources, you can also specify which users or service principals can access hello secret.</span></span> 

<span data-ttu-id="9bd17-106">В этой статье мы рассмотрим toodeploy необходимые шаги hello виртуальной машины Windows Azure стека, получая hello пароль, который хранится в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9bd17-106">In this article, we walk you through hello steps required toodeploy a Windows virtual machine in Azure Stack by retrieving hello password that is stored in a Key Vault.</span></span> <span data-ttu-id="9bd17-107">Таким образом hello пароль никогда не помещается в виде обычного текста в файле параметров шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-107">Therefore hello password is never put in plain text in hello template parameter file.</span></span> <span data-ttu-id="9bd17-108">Можно использовать следующие действия из hello пакет средств разработки стек Azure или из внешнего клиента при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="9bd17-108">You can use these steps either from hello Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bd17-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9bd17-109">Prerequisites</span></span>

* <span data-ttu-id="9bd17-110">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="9bd17-111">Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-111">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="9bd17-112">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="9bd17-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="9bd17-113">Настройка среды PowerShell hello Azure стека пользователя.</span><span class="sxs-lookup"><span data-stu-id="9bd17-113">Configure hello Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="9bd17-114">Hello следующие шаги описывают процесс, необходимый hello toocreate виртуальной машины, получая hello пароль, которые хранятся в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9bd17-114">hello following steps describe hello process required toocreate a virtual machine by retrieving hello password stored in a Key Vault:</span></span>

1. <span data-ttu-id="9bd17-115">Создание секрета хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9bd17-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="9bd17-116">Обновите файл azuredeploy.parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-116">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="9bd17-117">Развертывание шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-117">Deploy hello template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="9bd17-118">Создание секрета хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="9bd17-118">Create a Key Vault secret</span></span>

<span data-ttu-id="9bd17-119">Hello следующий скрипт создает хранилище ключей и сохраняет пароль в хранилище ключей hello как секрет.</span><span class="sxs-lookup"><span data-stu-id="9bd17-119">hello following script creates a key vault, and stores a password in hello key vault as a secret.</span></span> <span data-ttu-id="9bd17-120">Используйте hello `-EnabledForDeployment` параметр при создании хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="9bd17-120">Use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="9bd17-121">Этот параметр гарантирует, что хранилище ключей, hello можно ссылаться из шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd17-121">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

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

<span data-ttu-id="9bd17-122">При выполнении предыдущего сценария hello выход hello включает hello секрет URI.</span><span class="sxs-lookup"><span data-stu-id="9bd17-122">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="9bd17-123">Запишите этот URI.</span><span class="sxs-lookup"><span data-stu-id="9bd17-123">Make a note of this URI.</span></span> <span data-ttu-id="9bd17-124">У вас есть tooreference в hello [развертывание Windows виртуальной машины с паролем в хранилище ключей шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span><span class="sxs-lookup"><span data-stu-id="9bd17-124">You have tooreference it in hello [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="9bd17-125">Загрузите hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) папки на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="9bd17-125">Download hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="9bd17-126">Эта папка содержит hello `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые понадобятся в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="9bd17-126">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="9bd17-127">Изменение hello `azuredeploy.parameters.json` файл в соответствии с tooyour значений среды.</span><span class="sxs-lookup"><span data-stu-id="9bd17-127">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="9bd17-128">Hello особый интерес имеют имя хранилища hello, группа ресурсов хранилища hello и секрет hello URI (как созданных в ходе предыдущего сценария hello).</span><span class="sxs-lookup"><span data-stu-id="9bd17-128">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="9bd17-129">следующие файл Hello приведен пример файла параметров:</span><span class="sxs-lookup"><span data-stu-id="9bd17-129">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="9bd17-130">Обновить файл azuredeploy.parameters.json hello</span><span class="sxs-lookup"><span data-stu-id="9bd17-130">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="9bd17-131">Измените файл azuredeploy.parameters.json hello hello KeyVault, URI, secretName adminUsername значений виртуальной машины hello согласно вашей среде.</span><span class="sxs-lookup"><span data-stu-id="9bd17-131">Update hello azuredeploy.parameters.json file with hello KeyVault URI, secretName, adminUsername of hello virtual machine values as per your environment.</span></span> <span data-ttu-id="9bd17-132">Hello следующий файл JSON показан пример hello файл параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="9bd17-132">hello following JSON file shows an example of hello template parameters file:</span></span> 

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

## <a name="template-deployment"></a><span data-ttu-id="9bd17-133">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="9bd17-133">Template deployment</span></span>

<span data-ttu-id="9bd17-134">Теперь можно разверните hello шаблона с использованием hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9bd17-134">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
<span data-ttu-id="9bd17-135">При развертывании шаблона hello приводит hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9bd17-135">When hello template is deployed successfully, it results in hello following output:</span></span>

![Выходные данные развертывания](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="9bd17-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bd17-137">Next steps</span></span>
[<span data-ttu-id="9bd17-138">Развертывание примера приложения с хранилищем ключей</span><span class="sxs-lookup"><span data-stu-id="9bd17-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="9bd17-139">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="9bd17-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

