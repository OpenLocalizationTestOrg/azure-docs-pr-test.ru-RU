---
title: "aaaEnable или отключение мониторинга виртуальных Машин Azure"
description: "Описывает способ tooEnable или отключение мониторинга виртуальных Машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="0bf32-103">Включение и отключение мониторинга виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="0bf32-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="0bf32-104">В этом разделе описывается, как tooenable или отключите мониторинг на виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf32-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="0bf32-105">Можно включить или отключить мониторинг с помощью портала hello или интерфейса командной строки Azure для Mac, Linux и Windows (hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="0bf32-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bf32-106">В этом документе описываются версии 2.3 hello диагностического расширения Linux, которое рекомендуется к использованию.</span><span class="sxs-lookup"><span data-stu-id="0bf32-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="0bf32-107">Версия 2.3 будет поддерживаться до 30 июня 2018 г.</span><span class="sxs-lookup"><span data-stu-id="0bf32-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="0bf32-108">Вместо этого можно включить версии 3.0 hello диагностического расширения для Linux.</span><span class="sxs-lookup"><span data-stu-id="0bf32-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="0bf32-109">Дополнительные сведения см. в разделе [hello документации](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0bf32-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="0bf32-110">Включить / отключить мониторинг через hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0bf32-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="0bf32-111">Вы можете включить мониторинг виртуальной машины Azure, который предоставляет данные о вашем экземпляре с интервалом в 1 минуту</span><span class="sxs-lookup"><span data-stu-id="0bf32-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="0bf32-112">(применяются изменения хранилища).</span><span class="sxs-lookup"><span data-stu-id="0bf32-112">(storage changes apply).</span></span> <span data-ttu-id="0bf32-113">Подробные диагностические данные затем становится доступным для hello ВМ hello портала диаграммах или с помощью hello API.</span><span class="sxs-lookup"><span data-stu-id="0bf32-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="0bf32-114">По умолчанию портал Azure обеспечивает мониторинг ограниченного набора метрик на основе узла.</span><span class="sxs-lookup"><span data-stu-id="0bf32-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="0bf32-115">Вы можете включить наблюдение за показателей в виртуальной Машине при приветствия Виртуальная машина запущена или остановлена.</span><span class="sxs-lookup"><span data-stu-id="0bf32-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="0bf32-116">Откройте hello Azure портала в [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bf32-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="0bf32-117">В hello навигации слева выберите виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="0bf32-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="0bf32-118">На виртуальных машинах hello список выберите экземпляр запущенной или остановленной.</span><span class="sxs-lookup"><span data-stu-id="0bf32-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="0bf32-119">Открывает колонку Hello «Виртуальная машина».</span><span class="sxs-lookup"><span data-stu-id="0bf32-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="0bf32-120">Щелкните "Все параметры".</span><span class="sxs-lookup"><span data-stu-id="0bf32-120">Click All settings.</span></span>
* <span data-ttu-id="0bf32-121">Щелкните "Диагностика".</span><span class="sxs-lookup"><span data-stu-id="0bf32-121">Click Diagnostics.</span></span>
* <span data-ttu-id="0bf32-122">Изменить состояние tooOn или Off.</span><span class="sxs-lookup"><span data-stu-id="0bf32-122">Change status tooOn or Off.</span></span> <span data-ttu-id="0bf32-123">Также можно выбрать на этом уровне hello колонке мониторинга сведения tooenable требуется для вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0bf32-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Включить / отключить мониторинг через портал Azure hello.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="0bf32-125">Включение и отключение мониторинга с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="0bf32-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="0bf32-126">tooenable мониторинг на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf32-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="0bf32-127">Создайте файл (например, с именем PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="0bf32-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="0bf32-128">Включите расширение hello через Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0bf32-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="0bf32-129">Дополнительные сведения см. в разделе [производительности и диагностических данных с помощью диагностического расширения Linux tooMonitor Linux VM](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0bf32-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
