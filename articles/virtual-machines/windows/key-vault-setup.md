---
title: "Настройка Key Vault для виртуальных машин Windows в Azure Resource Manager | Документация Майкрософт"
description: "Узнайте, как настроить хранилище ключей для использования с виртуальной машиной Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="0b8e0-103">Настройка хранилища ключей для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b8e0-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0b8e0-104">В стеке Azure Resource Manager секреты или сертификаты моделируются как ресурсы, которые предоставляются поставщиком ресурсов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="0b8e0-105">Чтобы больше узнать о хранилище ключей, ознакомьтесь с разделом [Что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0b8e0-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="0b8e0-106">Чтобы хранилище ключей можно было использовать для виртуальных машин Azure Resource Manager, свойству **EnabledForDeployment** хранилища ключей должно быть присвоено значение true.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="0b8e0-107">Это можно сделать на различных клиентах.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="0b8e0-108">Хранилище ключей должно быть создано в тех же подписке и расположении, что и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="0b8e0-109">Использование PowerShell для настройки хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0b8e0-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="0b8e0-110">Сведения о создании хранилища ключей с помощью PowerShell см. в разделе [Приступая к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="0b8e0-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="0b8e0-111">Для новых хранилищ ключей можно использовать этот командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0b8e0-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="0b8e0-112">Для существующих хранилищ ключей можно использовать этот командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0b8e0-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="0b8e0-113">Использование интерфейса командной строки для настройки хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0b8e0-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="0b8e0-114">Сведения об использовании интерфейса командной строки (CLI) для создания хранилища ключей см. в статье [Управление хранилищем ключей с помощью CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="0b8e0-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="0b8e0-115">Чтобы использовать интерфейс командной строки, необходимо сначала создать хранилище ключей, а затем назначить политику развертывания.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="0b8e0-116">Это можно сделать с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0b8e0-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="0b8e0-117">Использование шаблонов для настройки хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0b8e0-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="0b8e0-118">При использовании шаблона свойству `enabledForDeployment` ресурса хранилища ключей нужно присвоить значение `true`.</span><span class="sxs-lookup"><span data-stu-id="0b8e0-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="0b8e0-119">Сведения о других параметрах, которые можно настроить при создании хранилища ключей с помощью шаблонов, см. в статье [Создание хранилища ключей](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="0b8e0-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
