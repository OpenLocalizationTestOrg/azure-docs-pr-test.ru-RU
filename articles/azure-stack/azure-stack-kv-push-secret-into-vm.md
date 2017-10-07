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
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a>Создание виртуальной машины и включение сертификатов, полученных из хранилища ключей

Эта статья поможет вам toocreate виртуальной машины в Azure стека и принудительной сертификаты на него. 

## <a name="prerequisites"></a>Предварительные требования

* Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей Azure hello.  
* Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.  
* [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)  
* [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md)

Хранилище ключей Azure стека — используется toostore сертификаты. Сертификаты полезны в различных сценариях. Например рассмотрим сценарий, когда имеется виртуальной машины в Azure стека, на котором выполняется приложение, которое требуется сертификат. Этот сертификат используется для шифрования, для проверки подлинности tooActive каталога или для SSL на веб-сайте. Наличие hello сертификат в хранилище ключей позволяет убедитесь в том, что он является безопасным.

В этой статье мы рассмотрим toopush необходимые шаги hello сертификата на виртуальной машине Windows Azure стека. При подключении через виртуальную частную сеть, можно использовать следующие действия из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows.

Hello следующие шаги описывают процесс, необходимый hello toopush сертификата на виртуальную машину hello:

1. Создание секрета хранилища ключей.
2. Обновите файл azuredeploy.parameters.json hello.
3. Развертывание шаблона hello

## <a name="create-a-key-vault-secret"></a>Создание секрета хранилища ключей

Hello следующий скрипт создает сертификат в формате PFX hello, создает хранилище ключей и сохраняет hello сертификат в хранилище ключей hello как секрет. Необходимо использовать hello `-EnabledForDeployment` параметр при создании хранилища ключей hello. Этот параметр гарантирует, что хранилище ключей, hello можно ссылаться из шаблонов диспетчера ресурсов Azure.

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

При выполнении предыдущего сценария hello выход hello включает hello секрет URI. Запишите этот URI. У вас есть tooreference в hello [Push-сертификатов tooWindows шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows). Загрузите hello [шаблона виртуальной машины push сертификатов windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) папки на компьютере разработчика. Эта папка содержит hello `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые понадобятся в hello дальнейшие действия.

Изменение hello `azuredeploy.parameters.json` файл в соответствии с tooyour значений среды. Hello особый интерес имеют имя хранилища hello, группа ресурсов хранилища hello и секрет hello URI (как созданных в ходе предыдущего сценария hello). следующие файл Hello приведен пример файла параметров:

## <a name="update-hello-azuredeployparametersjson-file"></a>Обновить файл azuredeploy.parameters.json hello

Измените файл azuredeploy.parameters.json hello hello vaultName, секретный URI, VmName и других значений в соответствии с вашей средой. Hello следующий файл JSON показан пример hello файл параметров шаблона. 

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

## <a name="deploy-hello-template"></a>Развертывание шаблона hello

Теперь можно разверните hello шаблона с использованием hello следующий сценарий PowerShell:

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

При развертывании шаблона hello приводит hello следующие выходные данные:

![Выходные данные развертывания](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

При развертывании виртуальной машины Azure стека помещает hello сертификата на виртуальную машину hello. В Windows hello сертификат добавляется toohello расположение сертификата, с сертификатом hello хранилища, предоставлено пользователем hello LocalMachine. В Linux, hello сертификат помещается в каталоге /var/lib/waagent hello, с именем файла hello &lt;UppercaseThumbprint&gt;.crt для файла сертификата hello X509 и &lt;UppercaseThumbprint&gt;.prv для hello закрытый ключ.

## <a name="retire-certificates"></a>Прекратить использование сертификатов

В предыдущих раздел hello, мы показали, как toopush нового сертификата на виртуальную машину. Старый сертификат по-прежнему включено hello виртуальной машины, и он не может быть удален. Тем не менее, можно отключить hello старую версию секрета hello с помощью hello `Set-AzureKeyVaultSecretAttribute` командлета. Hello ниже приведен пример использования этого командлета. Сделать убедиться, что имя хранилища hello tooreplace секретное имя и значения версии в соответствии с tooyour среды:

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>Дальнейшие действия

* [Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)
* [Разрешить приложение tooaccess хранилища ключей](azure-stack-kv-sample-app.md)


