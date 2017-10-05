---
title: "Включение и отключение мониторинга виртуальной машины Azure"
description: "В этой статье описывается включение или отключение мониторинга виртуальной машины Azure"
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
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="83c3b-103">Включение и отключение мониторинга виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="83c3b-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="83c3b-104">В этом разделе описывается, как включить или отключить мониторинг виртуальных машин, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="83c3b-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="83c3b-105">Мониторинг можно включить или отключить с помощью портала или интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="83c3b-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83c3b-106">В этом документе описывается версия 2.3 диагностического расширения для Linux, которая признана нерекомендуемой.</span><span class="sxs-lookup"><span data-stu-id="83c3b-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="83c3b-107">Версия 2.3 будет поддерживаться до 30 июня 2018 г.</span><span class="sxs-lookup"><span data-stu-id="83c3b-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="83c3b-108">Вместо нее можно включить диагностическое расширение для Linux версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="83c3b-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="83c3b-109">Дополнительные сведения см. в [документации](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="83c3b-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="83c3b-110">Включение и отключение мониторинга через портал Azure</span><span class="sxs-lookup"><span data-stu-id="83c3b-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="83c3b-111">Вы можете включить мониторинг виртуальной машины Azure, который предоставляет данные о вашем экземпляре с интервалом в 1 минуту</span><span class="sxs-lookup"><span data-stu-id="83c3b-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="83c3b-112">(применяются изменения хранилища).</span><span class="sxs-lookup"><span data-stu-id="83c3b-112">(storage changes apply).</span></span> <span data-ttu-id="83c3b-113">В результате на диаграммах портала или с помощью API становятся доступными подробные диагностические данные для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="83c3b-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="83c3b-114">По умолчанию портал Azure обеспечивает мониторинг ограниченного набора метрик на основе узла.</span><span class="sxs-lookup"><span data-stu-id="83c3b-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="83c3b-115">Включить мониторинг метрик в виртуальной машине можно, когда виртуальная машина работает или остановлена.</span><span class="sxs-lookup"><span data-stu-id="83c3b-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="83c3b-116">Откройте портал Azure по адресу [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83c3b-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="83c3b-117">В левой панели навигации щелкните "Виртуальные машины".</span><span class="sxs-lookup"><span data-stu-id="83c3b-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="83c3b-118">В списке виртуальных машин выберите запущенный или остановленный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="83c3b-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="83c3b-119">Откроется колонка "Виртуальная машина".</span><span class="sxs-lookup"><span data-stu-id="83c3b-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="83c3b-120">Щелкните "Все параметры".</span><span class="sxs-lookup"><span data-stu-id="83c3b-120">Click All settings.</span></span>
* <span data-ttu-id="83c3b-121">Щелкните "Диагностика".</span><span class="sxs-lookup"><span data-stu-id="83c3b-121">Click Diagnostics.</span></span>
* <span data-ttu-id="83c3b-122">Измените состояние с "Вкл" на "Выкл".</span><span class="sxs-lookup"><span data-stu-id="83c3b-122">Change status to On or Off.</span></span> <span data-ttu-id="83c3b-123">В этой колонке также можно выбрать уровень детализации мониторинга для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="83c3b-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Включение и отключение мониторинга через портал Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="83c3b-125">Включение и отключение мониторинга с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="83c3b-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="83c3b-126">Чтобы включить мониторинг для виртуальной машины Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="83c3b-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="83c3b-127">Создайте файл (например, с именем PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="83c3b-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="83c3b-128">Включение расширения через Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="83c3b-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="83c3b-129">Дополнительные сведения см. в статье [Использование диагностического расширения Linux для мониторинга данных о состоянии и производительности виртуальных машин под управлением Linux](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83c3b-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
