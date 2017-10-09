---
title: "Идентификатор виртуальной Машины Azure Linux aaaGet | Документы Microsoft"
description: "Описывает, как tooget и использования Azure Linux VM уникальный идентификатор."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="de02a-103">Получение и использование уникального идентификатора виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="de02a-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="de02a-104">Уникальный идентификатор виртуальной машины Azure — это 128-разрядный идентификатор, закодированный и хранящийся в SMBIOS всех виртуальных машин IaaS Azure. В настоящее время его можно считать с помощью команды BIOS используемой платформы.</span><span class="sxs-lookup"><span data-stu-id="de02a-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="de02a-105">Уникальный идентификатор виртуальной машины Azure является свойством только для чтения.</span><span class="sxs-lookup"><span data-stu-id="de02a-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="de02a-106">Уникальный идентификатор виртуальной машины Azure не изменится до завершения работы с перезагрузкой (планового или внепланового), запуска и остановки отмены распределения, восстановления службы или восстановления на месте.</span><span class="sxs-lookup"><span data-stu-id="de02a-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="de02a-107">Тем не менее если hello ВМ моментальными снимками и скопированные toocreate новый экземпляр, настраивается новый ИД виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="de02a-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="de02a-108">Если старые виртуальные машины, созданные и запущен, так как эта новая функция получен распространен (18 сентябрь 2014 г.), перезапустите tooautomatically вашей виртуальной Машине получить Azure уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="de02a-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="de02a-109">Уникальный идентификатор виртуальной Машины Azure из tooaccess внутри hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="de02a-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="de02a-110">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="de02a-110">Create a VM</span></span>
<span data-ttu-id="de02a-111">Дополнительные сведения см. в статье о [создании виртуальной машины](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de02a-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="de02a-112">Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="de02a-112">Connect toohello VM</span></span>
<span data-ttu-id="de02a-113">Дополнительные сведения см. в статье об [использовании SSH в Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de02a-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="de02a-114">Запрос уникального идентификатора виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="de02a-114">Query VM Unique ID</span></span>
<span data-ttu-id="de02a-115">Команда (в примере используется **Ubuntu**).</span><span class="sxs-lookup"><span data-stu-id="de02a-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="de02a-116">Ожидаемый результат выполнения примера.</span><span class="sxs-lookup"><span data-stu-id="de02a-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="de02a-117">Из-за tooBig порядком битов hello фактический уникальный ИД виртуальной Машины в этом случае будет:</span><span class="sxs-lookup"><span data-stu-id="de02a-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="de02a-118">Уникальный идентификатор виртуальной Машины Azure можно использовать в различных сценариях ли hello ВМ работает в Azure или в локальной среде и может помочь лицензирования, отчетов или общие требования к отслеживанию, имеющиеся в развертываниях Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="de02a-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="de02a-119">Несколько независимых поставщиков программного обеспечения построения приложений и удостоверяет их в Azure может потребоваться tooidentify ВМ Azure на протяжении его жизненного цикла и tootell, если hello виртуальная машина работает на Azure, локально или на других поставщиков облачных услуг.</span><span class="sxs-lookup"><span data-stu-id="de02a-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="de02a-120">Этот идентификатор платформы, например могут помочь обнаружить, если программное обеспечение hello действующую лицензию или помочь toocorrelate источника tooits данных любой виртуальной Машины, например tooassist на задание правой показатели hello подходящей платформы, а также tootrack hello и сопоставлять эти показатели среди другие способы его использования.</span><span class="sxs-lookup"><span data-stu-id="de02a-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

