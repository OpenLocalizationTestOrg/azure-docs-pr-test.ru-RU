---
title: "aaaKey секрета хранилища с помощью шаблона диспетчера ресурсов | Документы Microsoft"
description: "Показывает, как toopass секрет из ключа в хранилище как параметр во время развертывания."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Использовать хранилище ключей toopass безопасного параметра во время развертывания

При необходимости toopass безопасное значение (например, пароля) в качестве параметра во время развертывания можно получить значение hello из [хранилище ключей Azure](../key-vault/key-vault-whatis.md). Получить значение hello, ссылаясь на хранилище ключей hello и секретного кода в файле параметров. значение Hello никогда не предоставляется, поскольку можно ссылаться только на его идентификатор хранилища ключей. Нет необходимости toomanually введите hello значение hello секрет при каждом развертывании ресурсов hello. хранилище ключей Hello могут существовать в чем hello группы ресурсов, которые развертываются на другую подписку. При задании hello хранилища ключей, включении идентификатор hello подписки.

При создании хранилища ключей hello установите hello *enabledForTemplateDeployment* свойство слишком*true*. Если задать это значение tootrue, разрешают доступ из шаблонов диспетчера ресурсов во время развертывания.  

## <a name="deploy-a-key-vault-and-secret"></a>Развертывание хранилища ключей и секретного кода

хранилище ключей toocreate и секретный код, используйте PowerShell или Azure CLI. Обратите внимание, что хранилище ключей, hello включена поддержка развертывания шаблонов. 

Для интерфейса командной строки Azure:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Для PowerShell используйте команду:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Включить toohello секрет доступа

При использовании нового ключа хранилища или уже существующей, убедитесь, что этой hello развертывание шаблона hello пользователю секрет hello. Развертывание шаблон, который ссылается секрета пользователя Hello должен иметь hello `Microsoft.KeyVault/vaults/deploy/action` разрешения для хранилища ключей hello. Hello [владельца](../active-directory/role-based-access-built-in-roles.md#owner) и [участника](../active-directory/role-based-access-built-in-roles.md#contributor) роли обоих предоставлять такой доступ. Можно также создать [пользовательской роли](../active-directory/role-based-access-control-custom-roles.md) , предоставляет такое разрешение и добавить роль toothat hello пользователя. Сведения о добавлении tooa роли пользователя см. в разделе [назначить пользователя роли tooadministrator в Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Ссылка на секрет со статическим идентификатором

шаблон Hello, получает секрета хранилища ключей, в том, как и любой другой шаблон. Причина этого заключается в **ссылаться hello хранилища ключей в файле параметров hello, не hello шаблон.** Например следующий шаблон hello развертывает базу данных SQL, которая содержит пароль администратора. параметр пароля Hello задается tooa защищенной строки. Но hello шаблона не указано, откуда это значение.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Теперь создайте файл параметров для hello предшествующий шаблона. В файле параметров hello укажите параметр, который совпадает с именем hello параметра hello в шаблоне hello. Значение параметра hello ссылаться на hello секрета из хранилища ключей hello. Передав идентификатор ресурса хранилища ключей hello hello и hello имя секрета hello ссылаться секрет hello. В следующем примере hello hello секрета хранилища ключей должен уже существовать, и указать статическое значение для его идентификатора ресурса.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Ссылка на секрет с динамическим идентификатором

Hello предыдущего раздела было показано, как toopass идентификатор статический ресурс для hello ключа хранилища секрета. Однако в некоторых сценариях требуется tooreference секрета хранилища ключей, которая зависит от основываются на текущем развертывании hello. В этом случае вы не можете hello жестко идентификатор ресурса в файле параметров hello. К сожалению невозможно создать динамически hello идентификатор ресурса в файле параметров hello, так как шаблон выражения не разрешены в файле параметров hello.

toodynamically создавать hello идентификатор ресурса для секрета хранилища ключей, необходимо переместить ресурсом hello секрет hello в вложенных шаблонов. В шаблоне master добавить вложенный шаблон hello и передать в параметр, который содержит идентификатор ресурса hello создана динамически.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Дальнейшие действия
* Общие сведения о хранилищах ключей см. в разделе [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).
* Полные примеры использования ссылок на секреты ключей приведены [здесь](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

