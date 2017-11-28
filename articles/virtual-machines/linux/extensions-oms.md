---
title: "aaaOMS расширение виртуальной машины Azure для Linux | Документы Microsoft"
description: "Разверните агент OMS hello на виртуальной машине Linux с помощью расширения виртуальной машины."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="86265-103">Расширение виртуальной машины OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="86265-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="86265-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="86265-104">Overview</span></span>

<span data-ttu-id="86265-105">Operations Management Suite (OMS) предоставляет возможности мониторинга, оповещений и внесения исправлений в соответствии с оповещениями для облачных и локальных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="86265-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="86265-106">расширение виртуальной машины агента OMS для Linux Hello публикации и поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="86265-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="86265-107">расширение Hello устанавливает агент OMS hello на виртуальных машинах Azure и регистрирует виртуальных машин в существующую рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="86265-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="86265-108">Этот документ сведения hello платформы, конфигурации и параметры развертывания hello расширение виртуальной машины OMS для Linux поддерживает.</span><span class="sxs-lookup"><span data-stu-id="86265-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86265-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="86265-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="86265-110">операционная система</span><span class="sxs-lookup"><span data-stu-id="86265-110">Operating system</span></span>

<span data-ttu-id="86265-111">для этих дистрибутивов Linux, можно запустить Hello расширение OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="86265-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="86265-112">Дистрибутив</span><span class="sxs-lookup"><span data-stu-id="86265-112">Distribution</span></span> | <span data-ttu-id="86265-113">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="86265-113">Version</span></span> |
|---|---|
| <span data-ttu-id="86265-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="86265-114">CentOS Linux</span></span> | <span data-ttu-id="86265-115">5, 6 и 7</span><span class="sxs-lookup"><span data-stu-id="86265-115">5, 6, and 7</span></span> |
| <span data-ttu-id="86265-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="86265-116">Oracle Linux</span></span> | <span data-ttu-id="86265-117">5, 6 и 7</span><span class="sxs-lookup"><span data-stu-id="86265-117">5, 6, and 7</span></span> |
| <span data-ttu-id="86265-118">Сервер Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="86265-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="86265-119">5, 6 и 7</span><span class="sxs-lookup"><span data-stu-id="86265-119">5, 6 and 7</span></span> |
| <span data-ttu-id="86265-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="86265-120">Debian GNU/Linux</span></span> | <span data-ttu-id="86265-121">6, 7 и 8</span><span class="sxs-lookup"><span data-stu-id="86265-121">6, 7, and 8</span></span> |
| <span data-ttu-id="86265-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="86265-122">Ubuntu</span></span> | <span data-ttu-id="86265-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="86265-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="86265-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="86265-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="86265-125">11 и 12</span><span class="sxs-lookup"><span data-stu-id="86265-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="86265-126">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="86265-126">Internet connectivity</span></span>

<span data-ttu-id="86265-127">Hello расширение агента OMS для Linux требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="86265-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="86265-128">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="86265-128">Extension schema</span></span>

<span data-ttu-id="86265-129">Hello следующий JSON показана схема hello для hello расширение OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="86265-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="86265-130">расширения Hello требуются hello ключ рабочей области идентификатора и рабочей области из рабочей области OMS целевой hello; Эти значения можно найти на портале OMS hello.</span><span class="sxs-lookup"><span data-stu-id="86265-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="86265-131">Так как ключ рабочей области hello должны рассматриваться как конфиденциальные данные, его должны храниться в защищенном Настройка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="86265-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="86265-132">Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="86265-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="86265-133">Обратите внимание, что в **workspaceId** и **workspaceKey** учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="86265-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="86265-134">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="86265-134">Property values</span></span>

| <span data-ttu-id="86265-135">Имя</span><span class="sxs-lookup"><span data-stu-id="86265-135">Name</span></span> | <span data-ttu-id="86265-136">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="86265-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="86265-137">версия_API</span><span class="sxs-lookup"><span data-stu-id="86265-137">apiVersion</span></span> | <span data-ttu-id="86265-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="86265-138">2015-06-15</span></span> |
| <span data-ttu-id="86265-139">publisher</span><span class="sxs-lookup"><span data-stu-id="86265-139">publisher</span></span> | <span data-ttu-id="86265-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="86265-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="86265-141">type</span><span class="sxs-lookup"><span data-stu-id="86265-141">type</span></span> | <span data-ttu-id="86265-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="86265-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="86265-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="86265-143">typeHandlerVersion</span></span> | <span data-ttu-id="86265-144">1.4</span><span class="sxs-lookup"><span data-stu-id="86265-144">1.4</span></span> |
| <span data-ttu-id="86265-145">workspaceID (пример)</span><span class="sxs-lookup"><span data-stu-id="86265-145">workspaceId (e.g)</span></span> | <span data-ttu-id="86265-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="86265-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="86265-147">workspaceKey (пример)</span><span class="sxs-lookup"><span data-stu-id="86265-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="86265-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="86265-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="86265-149">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="86265-149">Template deployment</span></span>

<span data-ttu-id="86265-150">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86265-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="86265-151">Шаблоны представляют собой идеальный при развертывании одного или нескольких виртуальных машин, требующих после настройки развертывания, например tooOMS адаптации.</span><span class="sxs-lookup"><span data-stu-id="86265-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="86265-152">Образец шаблона диспетчера ресурсов, включает в себя расширение виртуальной Машины агента OMS hello можно найти на hello [Azure быстрого запуска коллекции](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="86265-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="86265-153">Hello конфигурации JSON для расширения виртуальной машины может быть вложена в ресурс виртуальной машины hello или помещается в корень hello или шаблон JSON диспетчера ресурсов верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="86265-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="86265-154">Размещение Hello конфигурации JSON hello влияет значение hello hello ресурсов именем и типом.</span><span class="sxs-lookup"><span data-stu-id="86265-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="86265-155">Дополнительные сведения см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="86265-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="86265-156">Hello в примере предполагается, что расширение OMS hello вложен в hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86265-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="86265-157">При вложении hello расширения ресурса, hello JSON помещается в hello `"resources": []` объекта hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86265-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="86265-158">При помещении hello расширения JSON в корне hello hello шаблона, имя ресурса hello ссылка toohello родительской виртуальной машиной и тип hello отражает hello вложенных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="86265-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="86265-159">Развертывание с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86265-159">Azure CLI deployment</span></span>

<span data-ttu-id="86265-160">Hello Azure CLI можно используется toodeploy hello ВМ агента OMS расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86265-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="86265-161">Замените ключ hello OMS и OMS код из рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="86265-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="86265-162">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="86265-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="86265-163">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="86265-163">Troubleshoot</span></span>

<span data-ttu-id="86265-164">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="86265-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="86265-165">Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующие команды, используя hello hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="86265-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="86265-166">Модуль выполнения выходных данных журнал toohello следующие файл:</span><span class="sxs-lookup"><span data-stu-id="86265-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="86265-167">Коды ошибок и их описание</span><span class="sxs-lookup"><span data-stu-id="86265-167">Error codes and their meanings</span></span>

| <span data-ttu-id="86265-168">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="86265-168">Error Code</span></span> | <span data-ttu-id="86265-169">Значение</span><span class="sxs-lookup"><span data-stu-id="86265-169">Meaning</span></span> | <span data-ttu-id="86265-170">Возможное действие</span><span class="sxs-lookup"><span data-stu-id="86265-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="86265-171">10</span><span class="sxs-lookup"><span data-stu-id="86265-171">10</span></span> | <span data-ttu-id="86265-172">Виртуальная машина уже подключенных tooan рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="86265-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="86265-173">tooconnect рабочей области для toohello hello виртуальной Машины указан в схеме расширения hello, задать stopOnMultipleConnections toofalse в общие параметры настройки или удалите это свойство.</span><span class="sxs-lookup"><span data-stu-id="86265-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="86265-174">Счет для этой виртуальной машины выставляется за каждую рабочую область, к которой она подключена.</span><span class="sxs-lookup"><span data-stu-id="86265-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="86265-175">11</span><span class="sxs-lookup"><span data-stu-id="86265-175">11</span></span> | <span data-ttu-id="86265-176">Недопустимый конфигурации указано toohello расширения</span><span class="sxs-lookup"><span data-stu-id="86265-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="86265-177">Выполните hello в предыдущих примерах tooset все значения свойств, необходимых для развертывания.</span><span class="sxs-lookup"><span data-stu-id="86265-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="86265-178">12</span><span class="sxs-lookup"><span data-stu-id="86265-178">12</span></span> | <span data-ttu-id="86265-179">Диспетчер пакетов dpkg Hello заблокирован</span><span class="sxs-lookup"><span data-stu-id="86265-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="86265-180">Убедитесь, что все dpkg операции обновления на компьютере hello завершена и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="86265-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="86265-181">20</span><span class="sxs-lookup"><span data-stu-id="86265-181">20</span></span> | <span data-ttu-id="86265-182">Преждевременный вызов операции включения</span><span class="sxs-lookup"><span data-stu-id="86265-182">Enable called prematurely</span></span> | <span data-ttu-id="86265-183">[Обновление hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="86265-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="86265-184">51</span><span class="sxs-lookup"><span data-stu-id="86265-184">51</span></span> | <span data-ttu-id="86265-185">Это расширение не поддерживается в операционной системе виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="86265-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="86265-186">55</span><span class="sxs-lookup"><span data-stu-id="86265-186">55</span></span> | <span data-ttu-id="86265-187">Не удается подключиться к службе Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="86265-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="86265-188">Проверьте, что hello система имеет доступ к Интернету или что предоставлено допустимое HTTP-прокси.</span><span class="sxs-lookup"><span data-stu-id="86265-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="86265-189">Кроме того Проверьте правильность hello кода hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="86265-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="86265-190">Дополнительные сведения об устранении неполадок можно найти на hello [руководство по устранению неполадок агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="86265-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="86265-191">Поддержка</span><span class="sxs-lookup"><span data-stu-id="86265-191">Support</span></span>

<span data-ttu-id="86265-192">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="86265-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="86265-193">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="86265-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="86265-194">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="86265-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="86265-195">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="86265-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
