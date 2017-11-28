---
title: "средства Azure стека aaaDownload из GitHub | Документы Microsoft"
description: "Узнайте, как средства toodownload необходимые toowork со стеком Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="37426-103">Загрузить набор средств Azure стека из GitHub</span><span class="sxs-lookup"><span data-stu-id="37426-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="37426-104">Средства AzureStack является репозиторием GitHub, на котором размещена модули PowerShell можно использовать toomanage и развертывать ресурсы tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="37426-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use toomanage and deploy resources tooAzure Stack.</span></span> <span data-ttu-id="37426-105">Можно загрузить и использовать эти PowerShell модули toohello пакет средств разработки Azure стека или tooa на основе windows внешний клиент при планировании tooestablish VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="37426-105">You can download and use these PowerShell modules toohello Azure Stack Development Kit, or tooa windows-based external client if you are planning tooestablish VPN connectivity.</span></span> <span data-ttu-id="37426-106">tooobtain этих средств, клонирование репозитория GitHub hello или hello средства AzureStack папка загрузки.</span><span class="sxs-lookup"><span data-stu-id="37426-106">tooobtain these tools, clone hello GitHub repository or download hello AzureStack-Tools folder.</span></span> 

<span data-ttu-id="37426-107">репозиторий tooclone hello, загрузите [Git](https://git-scm.com/download/win) для Windows, откройте окно командной строки и выполните следующий скрипт hello:</span><span class="sxs-lookup"><span data-stu-id="37426-107">tooclone hello repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

<span data-ttu-id="37426-108">toodownload hello папке инструменты, запустите следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="37426-108">toodownload hello tools folder, run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a><span data-ttu-id="37426-109">Функциональные возможности, предоставляемые hello модулей</span><span class="sxs-lookup"><span data-stu-id="37426-109">Functionalities provided by hello modules</span></span>

<span data-ttu-id="37426-110">репозиторий Hello средства AzureStack содержит модули PowerShell, которые поддерживают следующие функции для стека Azure hello:</span><span class="sxs-lookup"><span data-stu-id="37426-110">hello AzureStack-Tools repository contains PowerShell modules that support hello following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="37426-111">Функции</span><span class="sxs-lookup"><span data-stu-id="37426-111">Functionality</span></span> | <span data-ttu-id="37426-112">Описание</span><span class="sxs-lookup"><span data-stu-id="37426-112">Description</span></span> | <span data-ttu-id="37426-113">Этот модуль, который можно использовать?</span><span class="sxs-lookup"><span data-stu-id="37426-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="37426-114">Возможности облака</span><span class="sxs-lookup"><span data-stu-id="37426-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="37426-115">Используйте этот модуль tooget hello возможности облачной среды облака.</span><span class="sxs-lookup"><span data-stu-id="37426-115">Use this module tooget hello cloud capabilities of a cloud.</span></span> <span data-ttu-id="37426-116">Например можно получить hello возможностей облака, такие как версия API, ресурсы диспетчера ресурсов Azure, расширения виртуальных Машин и т.д. для стека Azure и Azure облака, использующие этот модуль.</span><span class="sxs-lookup"><span data-stu-id="37426-116">For example, you can get hello cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="37426-117">Облако администраторов и пользователей.</span><span class="sxs-lookup"><span data-stu-id="37426-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="37426-118">Администрирование вычислений Azure стека</span><span class="sxs-lookup"><span data-stu-id="37426-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="37426-119">Используйте этот модуль tooadd или удалите образ виртуальной Машины из стека Azure marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="37426-119">Use this module tooadd or remove a VM image from hello Azure Stack marketplace.</span></span> | <span data-ttu-id="37426-120">Администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="37426-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="37426-121">Администрирование Azure инфраструктуры стека</span><span class="sxs-lookup"><span data-stu-id="37426-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="37426-122">Используйте этот модуль toomanage стека Azure инфраструктуры виртуальных машин, предупреждения, обновления и т. д.</span><span class="sxs-lookup"><span data-stu-id="37426-122">Use this module toomanage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="37426-123">Администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="37426-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="37426-124">Политика диспетчера ресурсов для стек Azure</span><span class="sxs-lookup"><span data-stu-id="37426-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="37426-125">Использовать этот модуль tooconfigure подписки Azure или групповую ресурс Azure с hello же управления версиями и доступность службы как стек Azure.</span><span class="sxs-lookup"><span data-stu-id="37426-125">Use this module tooconfigure an Azure subscription or an Azure resource group with hello same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="37426-126">Облако Администраторы и пользователи</span><span class="sxs-lookup"><span data-stu-id="37426-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="37426-127">Зарегистрировать в Azure</span><span class="sxs-lookup"><span data-stu-id="37426-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="37426-128">Используйте этот модуль tooregister экземпляра комплект средств для разработки с Azure.</span><span class="sxs-lookup"><span data-stu-id="37426-128">Use this module tooregister your development kit instance with Azure.</span></span> <span data-ttu-id="37426-129">После регистрации, можно загрузить элементы marketplace hello из Azure и использовать их в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="37426-129">After registering, you can download hello marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="37426-130">Администраторов облака</span><span class="sxs-lookup"><span data-stu-id="37426-130">Cloud administrators</span></span> |
| [<span data-ttu-id="37426-131">Развертывания Azure стека</span><span class="sxs-lookup"><span data-stu-id="37426-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="37426-132">Используйте этот модуль tooprepare hello Azure стека узла компьютера toodeploy и повторное развертывание с помощью образа Azure стека виртуального жесткого Disk(VHD) hello.</span><span class="sxs-lookup"><span data-stu-id="37426-132">Use this module tooprepare hello Azure Stack host computer toodeploy and redeploy by using hello Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="37426-133">Администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="37426-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="37426-134">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="37426-134">Connecting tooAzure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="37426-135">Используйте этот экземпляр модуля tooconnect tooan стека Azure через PowerShell и tooconfigure tooAzure подключения VPN стека.</span><span class="sxs-lookup"><span data-stu-id="37426-135">Use this module tooconnect tooan Azure Stack instance through PowerShell and tooconfigure VPN connectivity tooAzure Stack.</span></span> | <span data-ttu-id="37426-136">Облако Администраторы и пользователи</span><span class="sxs-lookup"><span data-stu-id="37426-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="37426-137">Администрирование служб Azure стека</span><span class="sxs-lookup"><span data-stu-id="37426-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="37426-138">Azure стека администраторы могут использовать этот модуль toocreate, обеспечивают клиента по умолчанию с неограниченной квоты, между службами вычислений, хранения, сеть и хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="37426-138">Azure Stack administrators can use this module toocreate a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="37426-139">Администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="37426-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="37426-140">Проверяющий элемент управления шаблона</span><span class="sxs-lookup"><span data-stu-id="37426-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="37426-141">Используйте этот модуль tooverify, если существующий или новый шаблон может быть развернутой tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="37426-141">Use this module tooverify if an existing or a new template can be deployed tooAzure Stack.</span></span> | <span data-ttu-id="37426-142">Облако Администраторы и пользователи</span><span class="sxs-lookup"><span data-stu-id="37426-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="37426-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37426-143">Next steps</span></span>
* [<span data-ttu-id="37426-144">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="37426-144">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="37426-145">Подключение через виртуальную частную сеть tooAzure пакет средств разработки стека</span><span class="sxs-lookup"><span data-stu-id="37426-145">Connect tooAzure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
