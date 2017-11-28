---
title: "aaaAzure расширение агента Наблюдатель сети виртуальной машины для Linux | Документы Microsoft"
description: "Развертывание hello агента Наблюдатель сети на виртуальной машине Linux с помощью расширения виртуальной машины."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="2a9b5-103">Расширение виртуальной машины агента Наблюдателя за сетями для Linux</span><span class="sxs-lookup"><span data-stu-id="2a9b5-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="2a9b5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2a9b5-104">Overview</span></span>

<span data-ttu-id="2a9b5-105">[Наблюдатель за сетями Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) — это служба мониторинга производительности, диагностики и анализа сети, позволяющая наблюдать за сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="2a9b5-106">Hello расширение виртуальной машины агента Наблюдатель сети является обязательным для некоторых функций hello Наблюдатель сети на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="2a9b5-107">Сюда входит запись сетевого трафика по запросу и другие дополнительные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="2a9b5-108">Этот документ сведения hello платформ и параметры развертывания hello расширение агента Наблюдатель сети виртуальной машины для Linux поддерживает.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a9b5-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2a9b5-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="2a9b5-110">операционная система</span><span class="sxs-lookup"><span data-stu-id="2a9b5-110">Operating system</span></span>

<span data-ttu-id="2a9b5-111">Hello расширение Agent Наблюдатель сети можно выполнять на этих дистрибутивов Linux:</span><span class="sxs-lookup"><span data-stu-id="2a9b5-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="2a9b5-112">Дистрибутив</span><span class="sxs-lookup"><span data-stu-id="2a9b5-112">Distribution</span></span> | <span data-ttu-id="2a9b5-113">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="2a9b5-113">Version</span></span> |
|---|---|
| <span data-ttu-id="2a9b5-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2a9b5-114">Ubuntu</span></span> | <span data-ttu-id="2a9b5-115">16.04 LTS, 14.04 LTS и 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2a9b5-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="2a9b5-116">Debian</span><span class="sxs-lookup"><span data-stu-id="2a9b5-116">Debian</span></span> | <span data-ttu-id="2a9b5-117">7 и 8</span><span class="sxs-lookup"><span data-stu-id="2a9b5-117">7 and 8</span></span> |
| <span data-ttu-id="2a9b5-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="2a9b5-118">RedHat</span></span> | <span data-ttu-id="2a9b5-119">6.x и 7.x</span><span class="sxs-lookup"><span data-stu-id="2a9b5-119">6.x and 7.x</span></span> |
| <span data-ttu-id="2a9b5-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="2a9b5-120">Oracle Linux</span></span> | <span data-ttu-id="2a9b5-121">7x</span><span class="sxs-lookup"><span data-stu-id="2a9b5-121">7x</span></span> |
| <span data-ttu-id="2a9b5-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="2a9b5-122">Suse</span></span> | <span data-ttu-id="2a9b5-123">11 и 12</span><span class="sxs-lookup"><span data-stu-id="2a9b5-123">11 and 12</span></span> |
| <span data-ttu-id="2a9b5-124">openSUSE</span><span class="sxs-lookup"><span data-stu-id="2a9b5-124">OpenSuse</span></span> | <span data-ttu-id="2a9b5-125">7.0</span><span class="sxs-lookup"><span data-stu-id="2a9b5-125">7.0</span></span> |
| <span data-ttu-id="2a9b5-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="2a9b5-126">CentOS</span></span> | <span data-ttu-id="2a9b5-127">7.0</span><span class="sxs-lookup"><span data-stu-id="2a9b5-127">7.0</span></span> |

<span data-ttu-id="2a9b5-128">Обратите внимание, что CoreOS в данный момент не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="2a9b5-129">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="2a9b5-129">Internet connectivity</span></span>

<span data-ttu-id="2a9b5-130">Некоторые функциональные возможности агента Наблюдатель сети hello требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="2a9b5-131">Без hello возможность tooestablish исходящих подключений некоторых функций hello агента Наблюдатель сети может работать неправильно или становятся недоступными.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="2a9b5-132">Дополнительные сведения см. в разделе hello [документации Наблюдатель сети](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="2a9b5-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="2a9b5-133">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="2a9b5-133">Extension schema</span></span>

<span data-ttu-id="2a9b5-134">Hello следующий JSON показана схема hello для hello расширение Agent Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="2a9b5-135">Hello расширение не требуется ни в настоящее время поддерживает все параметры, предоставленные пользователем и зависит от конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="2a9b5-136">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="2a9b5-136">Property values</span></span>

| <span data-ttu-id="2a9b5-137">Имя</span><span class="sxs-lookup"><span data-stu-id="2a9b5-137">Name</span></span> | <span data-ttu-id="2a9b5-138">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="2a9b5-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="2a9b5-139">версия_API</span><span class="sxs-lookup"><span data-stu-id="2a9b5-139">apiVersion</span></span> | <span data-ttu-id="2a9b5-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="2a9b5-140">2015-06-15</span></span> |
| <span data-ttu-id="2a9b5-141">publisher</span><span class="sxs-lookup"><span data-stu-id="2a9b5-141">publisher</span></span> | <span data-ttu-id="2a9b5-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="2a9b5-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="2a9b5-143">type</span><span class="sxs-lookup"><span data-stu-id="2a9b5-143">type</span></span> | <span data-ttu-id="2a9b5-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="2a9b5-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="2a9b5-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="2a9b5-145">typeHandlerVersion</span></span> | <span data-ttu-id="2a9b5-146">1.4</span><span class="sxs-lookup"><span data-stu-id="2a9b5-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="2a9b5-147">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="2a9b5-147">Template deployment</span></span>

<span data-ttu-id="2a9b5-148">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="2a9b5-149">можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure расширение Agent Наблюдатель сети во время развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="2a9b5-150">Развертывание с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2a9b5-150">Azure CLI deployment</span></span>

<span data-ttu-id="2a9b5-151">Hello Azure CLI можно используется toodeploy hello сетевых наблюдателей агента ВМ расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="2a9b5-152">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="2a9b5-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="2a9b5-153">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2a9b5-153">Troubleshooting</span></span>

<span data-ttu-id="2a9b5-154">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="2a9b5-155">Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующие команды, используя hello hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="2a9b5-156">Модуль выполнения выходной журнал toofiles в hello следовать каталога:</span><span class="sxs-lookup"><span data-stu-id="2a9b5-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="2a9b5-157">Поддержка</span><span class="sxs-lookup"><span data-stu-id="2a9b5-157">Support</span></span>

<span data-ttu-id="2a9b5-158">Если вам нужна дополнительная помощь в любой момент в этой статье, можно см. документации toohello Наблюдатель сети или обратитесь в службу hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="2a9b5-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="2a9b5-159">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="2a9b5-160">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="2a9b5-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="2a9b5-161">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="2a9b5-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
