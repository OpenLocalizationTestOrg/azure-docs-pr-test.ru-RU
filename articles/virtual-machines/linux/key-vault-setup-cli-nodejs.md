---
title: "aaaSet копирование хранилища ключей для виртуальных машин Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager с hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="5a320-103">Настройка хранилища ключей для виртуальных машин диспетчера ресурсов Azure с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a320-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="5a320-104">В стеке диспетчера ресурсов Azure hello секреты или сертификаты моделируются в виде ресурсов, которые предоставляются поставщиком ресурсов hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5a320-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="5a320-105">toolearn Дополнительные сведения о хранилище ключей Azure, в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="5a320-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="5a320-106">Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello *EnabledForDeployment* свойства хранилища ключей должен быть указан tootrue.</span><span class="sxs-lookup"><span data-stu-id="5a320-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="5a320-107">Это можно сделать на различных клиентах.</span><span class="sxs-lookup"><span data-stu-id="5a320-107">You can do this in various clients.</span></span> <span data-ttu-id="5a320-108">В этой статье показано, как tooset копии хранилища ключей для использования с виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="5a320-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="5a320-109">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="5a320-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="5a320-110">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello</span><span class="sxs-lookup"><span data-stu-id="5a320-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="5a320-111">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="5a320-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5a320-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="5a320-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="5a320-113">Использовать tooset CLI 1.0 копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5a320-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="5a320-114">toocreate хранилища ключей с помощью hello командной строки (CLI), в разделе [управление хранилище ключей с помощью CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="5a320-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="5a320-115">1.0 CLI у вас есть хранилища ключей hello toocreate перед назначением hello развертывания политики.</span><span class="sxs-lookup"><span data-stu-id="5a320-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="5a320-116">Вы можете назначить hello политики с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5a320-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="5a320-117">Используйте шаблоны tooset копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5a320-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="5a320-118">При использовании шаблона необходимо tooset hello `enabledForDeployment` свойство слишком`true` для hello ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5a320-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="5a320-119">Сведения о других параметрах, которые можно настроить при создании хранилища ключей с помощью шаблонов, см. в статье [Создание хранилища ключей](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="5a320-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
