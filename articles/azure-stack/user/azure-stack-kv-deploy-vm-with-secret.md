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
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a>Создание виртуальной машины путем извлечения пароля, хранящихся в хранилище ключей

При необходимости передачи безопасное значение, таких как пароль во время развертывания, можно хранить значения как секрет в хранилище ключей Azure стека и ссылаться на него в шаблоны Azure Resource Manager. Вам не нужно вручную ввести секретный код при каждом развертывании ресурсов, можно также указать пользователей, которые или субъекты-службы можно получить доступ к секрета. 

В этой статье мы рассмотрим шаги, необходимые для развертывания виртуальной машины Windows Azure стека, получая пароль, который хранится в хранилище ключей. Поэтому пароль никогда не помещается в виде обычного текста в файле параметров шаблона. Можно использовать следующие действия из пакета средств разработки стек Azure или из внешнего клиента при подключении через виртуальную частную сеть.

## <a name="prerequisites"></a>Предварительные требования
 
* Необходимо необходимо подписаться на предложение, которая включает службу хранилища ключей.  
* [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)  
* [Настройка среды PowerShell пользователя Azure стека.](azure-stack-powershell-configure-user.md)

Следующие шаги описывают процесс, необходимый для создания виртуальной машины, получая пароль, которые хранятся в хранилище ключей:

1. Создание секрета хранилища ключей.
2. Обновите файл azuredeploy.parameters.json.
3. Разверните шаблон.

## <a name="create-a-key-vault-secret"></a>Создание секрета хранилища ключей

Следующий скрипт создает хранилище ключей и сохраняет пароль в виде секрета хранилища ключей. Используйте `-EnabledForDeployment` параметр при создании хранилища ключей. Этот параметр гарантирует, что хранилище ключей можно ссылаться с помощью шаблонов диспетчера ресурсов Azure.

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

При выполнении предыдущего сценария выходные данные содержат секретный URI. Запишите этот URI. Вам нужно сослаться на него в [развертывание Windows виртуальной машины с паролем в хранилище ключей шаблона](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv). Загрузить [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) папки на компьютере разработчика. Эта папка содержит `azuredeploy.json` и `azuredeploy.parameters.json` файлы, которые требуется в следующих шагах.

Изменить `azuredeploy.parameters.json` файл в соответствии с вашей среды значения. Особый интерес имеют имя хранилища, группа ресурсов хранилища и секретный код URI (как созданных в ходе предыдущего сценария). Следующий файл приведен пример файла параметров:

## <a name="update-the-azuredeployparametersjson-file"></a>Обновить файл azuredeploy.parameters.json

Измените файл azuredeploy.parameters.json KeyVault, URI, secretName adminUsername значений виртуальной машины в соответствии с вашей средой. Следующий файл JSON показан пример файла параметров шаблона. 

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

Теперь можно разверните шаблон с помощью следующего сценария PowerShell:

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
При развертывании шаблона произведут следующий результат:

![Выходные данные развертывания](media/azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание примера приложения с хранилищем ключей](azure-stack-kv-sample-app.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)

