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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="745d7-103">Использовать хранилище ключей toopass безопасного параметра во время развертывания</span><span class="sxs-lookup"><span data-stu-id="745d7-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="745d7-104">При необходимости toopass безопасное значение (например, пароля) в качестве параметра во время развертывания можно получить значение hello из [хранилище ключей Azure](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="745d7-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="745d7-105">Получить значение hello, ссылаясь на хранилище ключей hello и секретного кода в файле параметров.</span><span class="sxs-lookup"><span data-stu-id="745d7-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="745d7-106">значение Hello никогда не предоставляется, поскольку можно ссылаться только на его идентификатор хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="745d7-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="745d7-107">Нет необходимости toomanually введите hello значение hello секрет при каждом развертывании ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="745d7-108">хранилище ключей Hello могут существовать в чем hello группы ресурсов, которые развертываются на другую подписку.</span><span class="sxs-lookup"><span data-stu-id="745d7-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="745d7-109">При задании hello хранилища ключей, включении идентификатор hello подписки.</span><span class="sxs-lookup"><span data-stu-id="745d7-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="745d7-110">При создании хранилища ключей hello установите hello *enabledForTemplateDeployment* свойство слишком*true*.</span><span class="sxs-lookup"><span data-stu-id="745d7-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="745d7-111">Если задать это значение tootrue, разрешают доступ из шаблонов диспетчера ресурсов во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="745d7-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="745d7-112">Развертывание хранилища ключей и секретного кода</span><span class="sxs-lookup"><span data-stu-id="745d7-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="745d7-113">хранилище ключей toocreate и секретный код, используйте PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="745d7-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="745d7-114">Обратите внимание, что хранилище ключей, hello включена поддержка развертывания шаблонов.</span><span class="sxs-lookup"><span data-stu-id="745d7-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="745d7-115">Для интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="745d7-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="745d7-116">Для PowerShell используйте команду:</span><span class="sxs-lookup"><span data-stu-id="745d7-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="745d7-117">Включить toohello секрет доступа</span><span class="sxs-lookup"><span data-stu-id="745d7-117">Enable access toohello secret</span></span>

<span data-ttu-id="745d7-118">При использовании нового ключа хранилища или уже существующей, убедитесь, что этой hello развертывание шаблона hello пользователю секрет hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="745d7-119">Развертывание шаблон, который ссылается секрета пользователя Hello должен иметь hello `Microsoft.KeyVault/vaults/deploy/action` разрешения для хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="745d7-120">Hello [владельца](../active-directory/role-based-access-built-in-roles.md#owner) и [участника](../active-directory/role-based-access-built-in-roles.md#contributor) роли обоих предоставлять такой доступ.</span><span class="sxs-lookup"><span data-stu-id="745d7-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="745d7-121">Можно также создать [пользовательской роли](../active-directory/role-based-access-control-custom-roles.md) , предоставляет такое разрешение и добавить роль toothat hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="745d7-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="745d7-122">Сведения о добавлении tooa роли пользователя см. в разделе [назначить пользователя роли tooadministrator в Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="745d7-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="745d7-123">Ссылка на секрет со статическим идентификатором</span><span class="sxs-lookup"><span data-stu-id="745d7-123">Reference a secret with static ID</span></span>

<span data-ttu-id="745d7-124">шаблон Hello, получает секрета хранилища ключей, в том, как и любой другой шаблон.</span><span class="sxs-lookup"><span data-stu-id="745d7-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="745d7-125">Причина этого заключается в **ссылаться hello хранилища ключей в файле параметров hello, не hello шаблон.**</span><span class="sxs-lookup"><span data-stu-id="745d7-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="745d7-126">Например следующий шаблон hello развертывает базу данных SQL, которая содержит пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="745d7-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="745d7-127">параметр пароля Hello задается tooa защищенной строки.</span><span class="sxs-lookup"><span data-stu-id="745d7-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="745d7-128">Но hello шаблона не указано, откуда это значение.</span><span class="sxs-lookup"><span data-stu-id="745d7-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="745d7-129">Теперь создайте файл параметров для hello предшествующий шаблона.</span><span class="sxs-lookup"><span data-stu-id="745d7-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="745d7-130">В файле параметров hello укажите параметр, который совпадает с именем hello параметра hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="745d7-131">Значение параметра hello ссылаться на hello секрета из хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="745d7-132">Передав идентификатор ресурса хранилища ключей hello hello и hello имя секрета hello ссылаться секрет hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="745d7-133">В следующем примере hello hello секрета хранилища ключей должен уже существовать, и указать статическое значение для его идентификатора ресурса.</span><span class="sxs-lookup"><span data-stu-id="745d7-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="745d7-134">Ссылка на секрет с динамическим идентификатором</span><span class="sxs-lookup"><span data-stu-id="745d7-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="745d7-135">Hello предыдущего раздела было показано, как toopass идентификатор статический ресурс для hello ключа хранилища секрета.</span><span class="sxs-lookup"><span data-stu-id="745d7-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="745d7-136">Однако в некоторых сценариях требуется tooreference секрета хранилища ключей, которая зависит от основываются на текущем развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="745d7-137">В этом случае вы не можете hello жестко идентификатор ресурса в файле параметров hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="745d7-138">К сожалению невозможно создать динамически hello идентификатор ресурса в файле параметров hello, так как шаблон выражения не разрешены в файле параметров hello.</span><span class="sxs-lookup"><span data-stu-id="745d7-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="745d7-139">toodynamically создавать hello идентификатор ресурса для секрета хранилища ключей, необходимо переместить ресурсом hello секрет hello в вложенных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="745d7-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="745d7-140">В шаблоне master добавить вложенный шаблон hello и передать в параметр, который содержит идентификатор ресурса hello создана динамически.</span><span class="sxs-lookup"><span data-stu-id="745d7-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="745d7-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="745d7-141">Next steps</span></span>
* <span data-ttu-id="745d7-142">Общие сведения о хранилищах ключей см. в разделе [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="745d7-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="745d7-143">Полные примеры использования ссылок на секреты ключей приведены [здесь](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="745d7-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

