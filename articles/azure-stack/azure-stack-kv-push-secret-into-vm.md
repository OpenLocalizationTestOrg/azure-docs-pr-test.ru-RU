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
ms.openlocfilehash: 95008e783b2597895e870ceb3514bffbd4ab1dbf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a>Создание виртуальной машины и включение сертификатов, полученных из хранилища ключей

Эта статья поможет вам для создания виртуальной машины в Azure стека и принудительной сертификаты на него. 

## <a name="prerequisites"></a>Предварительные требования

* Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей Azure.  
* Пользователи должны [подписаться на предложение](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей.  
* [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)  
* [Настройка среды PowerShell пользователя стек Azure](azure-stack-powershell-configure-user.md)

Хранилище ключей Azure стека используется для хранения сертификатов. Сертификаты полезны в различных сценариях. Например рассмотрим сценарий, когда имеется виртуальной машины в Azure стека, на котором выполняется приложение, которое требуется сертификат. Этот сертификат используется для шифрования для проверки подлинности в Active Directory, или для SSL на веб-сайте. Наличие сертификата в хранилище ключей помогают убедитесь в том, что он является безопасным.

В этой статье мы рассмотрим шаги, необходимые для передачи сертификата на виртуальной машине Windows Azure стека. При подключении через виртуальную частную сеть, можно использовать следующие действия из пакета средств разработки стек Azure или из внешнего клиента на основе Windows.

Следующие шаги описывают процесс, необходимый для принудительной отправки сертификата на виртуальную машину.

1. Создание секрета хранилища ключей.
2. Обновите файл azuredeploy.parameters.json.
3. Развертывание шаблона

## <a name="create-a-key-vault-secret"></a>Создание секрета хранилища ключей

Следующий скрипт создает сертификат в формате PFX, создает хранилище ключей и сохраняет сертификат в хранилище ключей в качестве секрета. Необходимо использовать `-EnabledForDeployment` параметр при создании хранилища ключей. Этот параметр гарантирует, что хранилище ключей можно ссылаться с помощью шаблонов диспетчера ресурсов Azure.

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

При выполнении предыдущего сценария выходные данные содержат секретный URI. Запишите этот URI. Вам нужно сослаться на него в [сертификат Push шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows). Загрузить [шаблона виртуальной машины push сертификатов windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) папки на компьютере разработчика. Эта папка содержит `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые требуется в следующих шагах.

Изменить `azuredeploy.parameters.json` файл в соответствии с вашей среды значения. Особый интерес имеют имя хранилища, группа ресурсов хранилища и секретный код URI (как созданных в ходе предыдущего сценария). Следующий файл приведен пример файла параметров:

## <a name="update-the-azuredeployparametersjson-file"></a>Обновить файл azuredeploy.parameters.json

Измените файл azuredeploy.parameters.json vaultName, секретный URI, VmName и других значений в соответствии с вашей средой. Следующий файл JSON показан пример файла параметров шаблона. 

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

## <a name="deploy-the-template"></a>Развертывание шаблона

Теперь можно разверните шаблон с помощью следующего сценария PowerShell:

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

При развертывании шаблона произведут следующий результат:

![Выходные данные развертывания](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

При развертывании виртуальной машины Azure стека помещает сертификата на виртуальную машину. Сертификат добавляется в расположении LocalMachine сертификат в хранилище сертификатов, введенные пользователем в Windows. В Linux, сертификат помещается в каталоге /var/lib/waagent файл с именем &lt;UppercaseThumbprint&gt;.crt для X509 файл сертификата и &lt;UppercaseThumbprint&gt;.prv для закрытого ключа .

## <a name="retire-certificates"></a>Прекратить использование сертификатов

В предыдущем разделе мы показали, чтобы отправить новый сертификат на виртуальную машину. Старый сертификат будет по-прежнему на виртуальной машине, и он не может быть удален. Однако более раннюю версию секрета можно отключить с помощью `Set-AzureKeyVaultSecretAttribute` командлета. Ниже приведен пример использования этого командлета. Обязательно замените имя хранилища, секретное имя и значения версии в соответствии с вашей среды:

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>Дальнейшие действия

* [Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)
* [Разрешить приложению доступ к хранилищу ключей](azure-stack-kv-sample-app.md)


