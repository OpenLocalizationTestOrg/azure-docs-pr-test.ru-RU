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
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a>Создание виртуальной машины, получая hello пароль, которые хранятся в хранилище ключей

При необходимости toopass безопасное значение, таких как пароль во время развертывания, можно хранить значения как секрет в хранилище ключей Azure стека и ссылаться на него в шаблоны Azure Resource Manager hello. Нет необходимости toomanually введите секрет hello при каждом развертывании hello ресурсы, можно также указать, какие пользователи или субъекты-службы доступа к секрет hello. 

В этой статье мы рассмотрим toodeploy необходимые шаги hello виртуальной машины Windows Azure стека, получая hello пароль, который хранится в хранилище ключей. Таким образом hello пароль никогда не помещается в виде обычного текста в файле параметров шаблона hello. Можно использовать следующие действия из hello пакет средств разработки стек Azure или из внешнего клиента при подключении через виртуальную частную сеть.

## <a name="prerequisites"></a>Предварительные требования

* Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей Azure hello.  
* Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.  
* [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)  
* [Настройка среды PowerShell hello Azure стека пользователя.](azure-stack-powershell-configure-user.md)

Hello следующие шаги описывают процесс, необходимый hello toocreate виртуальной машины, получая hello пароль, которые хранятся в хранилище ключей.

1. Создание секрета хранилища ключей.
2. Обновите файл azuredeploy.parameters.json hello.
3. Развертывание шаблона hello.

## <a name="create-a-key-vault-secret"></a>Создание секрета хранилища ключей

Hello следующий скрипт создает хранилище ключей и сохраняет пароль в хранилище ключей hello как секрет. Используйте hello `-EnabledForDeployment` параметр при создании хранилища ключей hello. Этот параметр гарантирует, что хранилище ключей, hello можно ссылаться из шаблонов диспетчера ресурсов Azure.

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

При выполнении предыдущего сценария hello выход hello включает hello секрет URI. Запишите этот URI. У вас есть tooreference в hello [развертывание Windows виртуальной машины с паролем в хранилище ключей шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password). Загрузите hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) папки на компьютере разработчика. Эта папка содержит hello `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые понадобятся в hello дальнейшие действия.

Изменение hello `azuredeploy.parameters.json` файл в соответствии с tooyour значений среды. Hello особый интерес имеют имя хранилища hello, группа ресурсов хранилища hello и секрет hello URI (как созданных в ходе предыдущего сценария hello). следующие файл Hello приведен пример файла параметров:

## <a name="update-hello-azuredeployparametersjson-file"></a>Обновить файл azuredeploy.parameters.json hello

Измените файл azuredeploy.parameters.json hello hello KeyVault, URI, secretName adminUsername значений виртуальной машины hello согласно вашей среде. Hello следующий файл JSON показан пример hello файл параметров шаблона. 

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

## <a name="template-deployment"></a>Развертывание шаблона

Теперь можно разверните hello шаблона с использованием hello следующий сценарий PowerShell:

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
При развертывании шаблона hello приводит hello следующие выходные данные:

![Выходные данные развертывания](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание примера приложения с хранилищем ключей](azure-stack-kv-sample-app.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)

