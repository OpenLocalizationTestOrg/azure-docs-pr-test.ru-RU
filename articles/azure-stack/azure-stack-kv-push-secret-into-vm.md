---
title: "aaaDeploy виртуальную машину с сертификатом, безопасно хранящиеся на стек Azure | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальной машины и принудительной сертификат на него с помощью ключа хранилища Azure стека"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="81f4d-103">Создание виртуальной машины и включение сертификатов, полученных из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="81f4d-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="81f4d-104">Эта статья поможет вам toocreate виртуальной машины в Azure стека и принудительной сертификаты на него.</span><span class="sxs-lookup"><span data-stu-id="81f4d-104">This article helps you toocreate a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81f4d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="81f4d-105">Prerequisites</span></span>

* <span data-ttu-id="81f4d-106">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей Azure hello.</span><span class="sxs-lookup"><span data-stu-id="81f4d-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="81f4d-107">Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="81f4d-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="81f4d-108">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81f4d-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="81f4d-109">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="81f4d-109">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="81f4d-110">Хранилище ключей Azure стека — используется toostore сертификаты.</span><span class="sxs-lookup"><span data-stu-id="81f4d-110">A key vault in Azure Stack is used toostore certificates.</span></span> <span data-ttu-id="81f4d-111">Сертификаты полезны в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="81f4d-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="81f4d-112">Например рассмотрим сценарий, когда имеется виртуальной машины в Azure стека, на котором выполняется приложение, которое требуется сертификат.</span><span class="sxs-lookup"><span data-stu-id="81f4d-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="81f4d-113">Этот сертификат используется для шифрования, для проверки подлинности tooActive каталога или для SSL на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="81f4d-113">This certificate can be used for encrypting, for authenticating tooActive Directory, or for SSL on a website.</span></span> <span data-ttu-id="81f4d-114">Наличие hello сертификат в хранилище ключей позволяет убедитесь в том, что он является безопасным.</span><span class="sxs-lookup"><span data-stu-id="81f4d-114">Having hello certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="81f4d-115">В этой статье мы рассмотрим toopush необходимые шаги hello сертификата на виртуальной машине Windows Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81f4d-115">In this article, we walk you through hello steps required toopush a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="81f4d-116">При подключении через виртуальную частную сеть, можно использовать следующие действия из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="81f4d-116">You can use these steps either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="81f4d-117">Hello следующие шаги описывают процесс, необходимый hello toopush сертификата на виртуальную машину hello:</span><span class="sxs-lookup"><span data-stu-id="81f4d-117">hello following steps describe hello process required toopush a certificate onto hello virtual machine:</span></span>

1. <span data-ttu-id="81f4d-118">Создание секрета хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="81f4d-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="81f4d-119">Обновите файл azuredeploy.parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="81f4d-119">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="81f4d-120">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="81f4d-120">Deploy hello template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="81f4d-121">Создание секрета хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="81f4d-121">Create a Key Vault secret</span></span>

<span data-ttu-id="81f4d-122">Hello следующий скрипт создает сертификат в формате PFX hello, создает хранилище ключей и сохраняет hello сертификат в хранилище ключей hello как секрет.</span><span class="sxs-lookup"><span data-stu-id="81f4d-122">hello following script creates a certificate in hello .pfx format, creates a key vault, and stores hello certificate in hello key vault as a secret.</span></span> <span data-ttu-id="81f4d-123">Необходимо использовать hello `-EnabledForDeployment` параметр при создании хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="81f4d-123">You must use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="81f4d-124">Этот параметр гарантирует, что хранилище ключей, hello можно ссылаться из шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="81f4d-124">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

<span data-ttu-id="81f4d-125">При выполнении предыдущего сценария hello выход hello включает hello секрет URI.</span><span class="sxs-lookup"><span data-stu-id="81f4d-125">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="81f4d-126">Запишите этот URI.</span><span class="sxs-lookup"><span data-stu-id="81f4d-126">Make a note of this URI.</span></span> <span data-ttu-id="81f4d-127">У вас есть tooreference в hello [Push-сертификатов tooWindows шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="81f4d-127">You have tooreference it in hello [Push certificate tooWindows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="81f4d-128">Загрузите hello [шаблона виртуальной машины push сертификатов windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) папки на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="81f4d-128">Download hello [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="81f4d-129">Эта папка содержит hello `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые понадобятся в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="81f4d-129">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="81f4d-130">Изменение hello `azuredeploy.parameters.json` файл в соответствии с tooyour значений среды.</span><span class="sxs-lookup"><span data-stu-id="81f4d-130">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="81f4d-131">Hello особый интерес имеют имя хранилища hello, группа ресурсов хранилища hello и секрет hello URI (как созданных в ходе предыдущего сценария hello).</span><span class="sxs-lookup"><span data-stu-id="81f4d-131">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="81f4d-132">следующие файл Hello приведен пример файла параметров:</span><span class="sxs-lookup"><span data-stu-id="81f4d-132">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="81f4d-133">Обновить файл azuredeploy.parameters.json hello</span><span class="sxs-lookup"><span data-stu-id="81f4d-133">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="81f4d-134">Измените файл azuredeploy.parameters.json hello hello vaultName, секретный URI, VmName и других значений в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="81f4d-134">Update hello azuredeploy.parameters.json file with hello vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="81f4d-135">Hello следующий файл JSON показан пример hello файл параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="81f4d-135">hello following JSON file shows an example of hello template parameters file:</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-hello-template"></a><span data-ttu-id="81f4d-136">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="81f4d-136">Deploy hello template</span></span>

<span data-ttu-id="81f4d-137">Теперь можно разверните hello шаблона с использованием hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="81f4d-137">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

<span data-ttu-id="81f4d-138">При развертывании шаблона hello приводит hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="81f4d-138">When hello template is deployed successfully, it results in hello following output:</span></span>

![Выходные данные развертывания](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="81f4d-140">При развертывании виртуальной машины Azure стека помещает hello сертификата на виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="81f4d-140">When this virtual machine is deployed, Azure Stack pushes hello certificate onto hello virtual machine.</span></span> <span data-ttu-id="81f4d-141">В Windows hello сертификат добавляется toohello расположение сертификата, с сертификатом hello хранилища, предоставлено пользователем hello LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="81f4d-141">In Windows, hello certificate is added toohello LocalMachine certificate location, with hello certificate store that hello user provided.</span></span> <span data-ttu-id="81f4d-142">В Linux, hello сертификат помещается в каталоге /var/lib/waagent hello, с именем файла hello &lt;UppercaseThumbprint&gt;.crt для файла сертификата hello X509 и &lt;UppercaseThumbprint&gt;.prv для hello закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="81f4d-142">In Linux, hello certificate is placed under hello /var/lib/waagent directory, with hello file name &lt;UppercaseThumbprint&gt;.crt for hello X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for hello private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="81f4d-143">Прекратить использование сертификатов</span><span class="sxs-lookup"><span data-stu-id="81f4d-143">Retire certificates</span></span>

<span data-ttu-id="81f4d-144">В предыдущих раздел hello, мы показали, как toopush нового сертификата на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="81f4d-144">In hello preceding section, we showed you how toopush a new certificate onto a virtual machine.</span></span> <span data-ttu-id="81f4d-145">Старый сертификат по-прежнему включено hello виртуальной машины, и он не может быть удален.</span><span class="sxs-lookup"><span data-stu-id="81f4d-145">Your old certificate is still on hello virtual machine, and it can't be removed.</span></span> <span data-ttu-id="81f4d-146">Тем не менее, можно отключить hello старую версию секрета hello с помощью hello `Set-AzureKeyVaultSecretAttribute` командлета.</span><span class="sxs-lookup"><span data-stu-id="81f4d-146">However, you can disable hello older version of hello secret by using hello `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="81f4d-147">Hello ниже приведен пример использования этого командлета.</span><span class="sxs-lookup"><span data-stu-id="81f4d-147">hello following is an example usage of this cmdlet.</span></span> <span data-ttu-id="81f4d-148">Сделать убедиться, что имя хранилища hello tooreplace секретное имя и значения версии в соответствии с tooyour среды:</span><span class="sxs-lookup"><span data-stu-id="81f4d-148">Make sure tooreplace hello vault name, secret name, and version values according tooyour environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="81f4d-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81f4d-149">Next steps</span></span>

* [<span data-ttu-id="81f4d-150">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="81f4d-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="81f4d-151">Разрешить приложение tooaccess хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="81f4d-151">Allow an application tooaccess Key Vault</span></span>](azure-stack-kv-sample-app.md)


