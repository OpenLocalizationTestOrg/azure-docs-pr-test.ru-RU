---
title: "Развертывание виртуальной машины с сертификатом, безопасно хранящиеся на стек Azure | Документы Microsoft"
description: "Узнайте, как развертывание виртуальной машины и отправить сертификат на него с помощью хранилища ключей Azure стека"
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
ms.openlocfilehash: 29ccdc9eca9911b2f550f9e09da83d0b1d30f9db
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="85b55-103">Создание виртуальной машины и включение сертификатов, полученных из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="85b55-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="85b55-104">Эта статья поможет вам для создания виртуальной машины в Azure стека и принудительной сертификаты на него.</span><span class="sxs-lookup"><span data-stu-id="85b55-104">This article helps you to create a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="85b55-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="85b55-105">Prerequisites</span></span>

* <span data-ttu-id="85b55-106">Необходимо необходимо подписаться на предложение, которая включает службу хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="85b55-106">You must must subscribe to an offer that includes the Key Vault service.</span></span> 
* [<span data-ttu-id="85b55-107">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="85b55-107">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="85b55-108">Настройка среды PowerShell пользователя стек Azure</span><span class="sxs-lookup"><span data-stu-id="85b55-108">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="85b55-109">Хранилище ключей Azure стека используется для хранения сертификатов.</span><span class="sxs-lookup"><span data-stu-id="85b55-109">A key vault in Azure Stack is used to store certificates.</span></span> <span data-ttu-id="85b55-110">Сертификаты полезны в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="85b55-110">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="85b55-111">Например рассмотрим сценарий, когда имеется виртуальной машины в Azure стека, на котором выполняется приложение, которое требуется сертификат.</span><span class="sxs-lookup"><span data-stu-id="85b55-111">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="85b55-112">Этот сертификат используется для шифрования для проверки подлинности в Active Directory, или для SSL на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="85b55-112">This certificate can be used for encrypting, for authenticating to Active Directory, or for SSL on a website.</span></span> <span data-ttu-id="85b55-113">Наличие сертификата в хранилище ключей помогают убедитесь в том, что он является безопасным.</span><span class="sxs-lookup"><span data-stu-id="85b55-113">Having the certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="85b55-114">В этой статье мы рассмотрим шаги, необходимые для передачи сертификата на виртуальной машине Windows Azure стека.</span><span class="sxs-lookup"><span data-stu-id="85b55-114">In this article, we walk you through the steps required to push a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="85b55-115">При подключении через виртуальную частную сеть, можно использовать следующие действия из пакета средств разработки стек Azure или из внешнего клиента на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="85b55-115">You can use these steps either from the Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="85b55-116">Следующие шаги описывают процесс, необходимый для принудительной отправки сертификата на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="85b55-116">The following steps describe the process required to push a certificate onto the virtual machine:</span></span>

1. <span data-ttu-id="85b55-117">Создание секрета хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="85b55-117">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="85b55-118">Обновите файл azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="85b55-118">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="85b55-119">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="85b55-119">Deploy the template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="85b55-120">Создание секрета хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="85b55-120">Create a Key Vault secret</span></span>

<span data-ttu-id="85b55-121">Следующий скрипт создает сертификат в формате PFX, создает хранилище ключей и сохраняет сертификат в хранилище ключей в качестве секрета.</span><span class="sxs-lookup"><span data-stu-id="85b55-121">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span></span> <span data-ttu-id="85b55-122">Необходимо использовать `-EnabledForDeployment` параметр при создании хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="85b55-122">You must use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="85b55-123">Этот параметр гарантирует, что хранилище ключей можно ссылаться с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="85b55-123">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

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

<span data-ttu-id="85b55-124">При выполнении предыдущего сценария выходные данные содержат секретный URI.</span><span class="sxs-lookup"><span data-stu-id="85b55-124">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="85b55-125">Запишите этот URI.</span><span class="sxs-lookup"><span data-stu-id="85b55-125">Make a note of this URI.</span></span> <span data-ttu-id="85b55-126">Вам нужно сослаться на него в [сертификат Push шаблона диспетчера ресурсов](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate).</span><span class="sxs-lookup"><span data-stu-id="85b55-126">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate).</span></span> <span data-ttu-id="85b55-127">Загрузить [шаблона виртуальной машины push сертификатов windows](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate) папки на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="85b55-127">Download the [vm-push-certificate-windows template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate) folder onto your development computer.</span></span> <span data-ttu-id="85b55-128">Эта папка содержит `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые требуется в следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="85b55-128">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="85b55-129">Изменить `azuredeploy.parameters.json` файл в соответствии с вашей среды значения.</span><span class="sxs-lookup"><span data-stu-id="85b55-129">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="85b55-130">Особый интерес имеют имя хранилища, группа ресурсов хранилища и секретный код URI (как созданных в ходе предыдущего сценария).</span><span class="sxs-lookup"><span data-stu-id="85b55-130">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="85b55-131">Следующий файл приведен пример файла параметров:</span><span class="sxs-lookup"><span data-stu-id="85b55-131">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="85b55-132">Обновить файл azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="85b55-132">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="85b55-133">Измените файл azuredeploy.parameters.json vaultName, секретный URI, VmName и других значений в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="85b55-133">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="85b55-134">Следующий файл JSON показан пример файла параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="85b55-134">The following JSON file shows an example of the template parameters file:</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="85b55-135">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="85b55-135">Deploy the template</span></span>

<span data-ttu-id="85b55-136">Теперь можно разверните шаблон с помощью следующего сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="85b55-136">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="85b55-137">При развертывании шаблона произведут следующий результат:</span><span class="sxs-lookup"><span data-stu-id="85b55-137">When the template is deployed successfully, it results in the following output:</span></span>

![Выходные данные развертывания](media/azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="85b55-139">При развертывании виртуальной машины Azure стека помещает сертификата на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="85b55-139">When this virtual machine is deployed, Azure Stack pushes the certificate onto the virtual machine.</span></span> <span data-ttu-id="85b55-140">Сертификат добавляется в расположении LocalMachine сертификат в хранилище сертификатов, введенные пользователем в Windows.</span><span class="sxs-lookup"><span data-stu-id="85b55-140">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span> <span data-ttu-id="85b55-141">В Linux, сертификат помещается в каталоге /var/lib/waagent файл с именем &lt;UppercaseThumbprint&gt;.crt для X509 файл сертификата и &lt;UppercaseThumbprint&gt;.prv для закрытого ключа .</span><span class="sxs-lookup"><span data-stu-id="85b55-141">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="85b55-142">Прекратить использование сертификатов</span><span class="sxs-lookup"><span data-stu-id="85b55-142">Retire certificates</span></span>

<span data-ttu-id="85b55-143">В предыдущем разделе мы показали, чтобы отправить новый сертификат на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="85b55-143">In the preceding section, we showed you how to push a new certificate onto a virtual machine.</span></span> <span data-ttu-id="85b55-144">Старый сертификат будет по-прежнему на виртуальной машине, и он не может быть удален.</span><span class="sxs-lookup"><span data-stu-id="85b55-144">Your old certificate is still on the virtual machine, and it can't be removed.</span></span> <span data-ttu-id="85b55-145">Однако более раннюю версию секрета можно отключить с помощью `Set-AzureKeyVaultSecretAttribute` командлета.</span><span class="sxs-lookup"><span data-stu-id="85b55-145">However, you can disable the older version of the secret by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="85b55-146">Ниже приведен пример использования этого командлета.</span><span class="sxs-lookup"><span data-stu-id="85b55-146">The following is an example usage of this cmdlet.</span></span> <span data-ttu-id="85b55-147">Обязательно замените имя хранилища, секретное имя и значения версии в соответствии с вашей среды:</span><span class="sxs-lookup"><span data-stu-id="85b55-147">Make sure to replace the vault name, secret name, and version values according to your environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="85b55-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85b55-148">Next steps</span></span>

* [<span data-ttu-id="85b55-149">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="85b55-149">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="85b55-150">Разрешить приложению доступ к хранилищу ключей</span><span class="sxs-lookup"><span data-stu-id="85b55-150">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)


