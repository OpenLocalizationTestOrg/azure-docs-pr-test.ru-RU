---
title: "aaaSet копию ключа хранилища для виртуальных машин Windows в диспетчере ресурсов Azure | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager."
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
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="17b14-103">Настройка хранилища ключей для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="17b14-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="17b14-104">В стеке диспетчера ресурсов Azure секреты или сертификаты моделируются в виде ресурсов, которые предоставляются поставщиком ресурсов hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="17b14-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="17b14-105">toolearn Дополнительные сведения о хранилище ключей. в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="17b14-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="17b14-106">Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello **EnabledForDeployment** свойства хранилища ключей должен быть указан tootrue.</span><span class="sxs-lookup"><span data-stu-id="17b14-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="17b14-107">Это можно сделать на различных клиентах.</span><span class="sxs-lookup"><span data-stu-id="17b14-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="17b14-108">потребности Hello хранилище ключей toobe, созданного в hello же подписке и расположении как hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="17b14-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="17b14-109">Используйте PowerShell tooset копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="17b14-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="17b14-110">toocreate хранилища ключей с помощью PowerShell см. в разделе [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="17b14-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="17b14-111">Для новых хранилищ ключей можно использовать этот командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="17b14-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="17b14-112">Для существующих хранилищ ключей можно использовать этот командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="17b14-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="17b14-113">Нам CLI tooset копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="17b14-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="17b14-114">toocreate хранилища ключей с помощью hello командной строки (CLI), в разделе [управление хранилище ключей с помощью CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="17b14-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="17b14-115">Для CLI у вас есть хранилища ключей toocreate hello перед назначением hello развертывания политики.</span><span class="sxs-lookup"><span data-stu-id="17b14-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="17b14-116">Это можно сделать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="17b14-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="17b14-117">Используйте шаблоны tooset копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="17b14-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="17b14-118">При использовании шаблона требуется tooset hello `enabledForDeployment` свойство слишком`true` для hello ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="17b14-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="17b14-119">Сведения о других параметрах, которые можно настроить при создании хранилища ключей с помощью шаблонов, см. в статье [Создание хранилища ключей](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="17b14-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
