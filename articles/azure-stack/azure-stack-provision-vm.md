---
title: "aaaCreate теста виртуальной Машины в Azure стек | Документы Microsoft"
description: "Узнайте, как tooprovision теста виртуальной Машины в стеке Azure как оператор облака."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="6e562-103">Создать тестовую виртуальную машину в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6e562-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="6e562-104">Как оператор облака toovalidate теста виртуальной машины можно создать развертывание стека Azure.</span><span class="sxs-lookup"><span data-stu-id="6e562-104">As a cloud operator, you can create a test virtual machine toovalidate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="6e562-105">Прежде чем можно подготовить виртуальные машины, необходимо [добавьте hello ознакомительную версию Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="6e562-105">Before you can provision virtual machines, you must [add hello Windows Server 2016 Evaluation image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="6e562-106">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6e562-106">Create a virtual machine</span></span>
1. <span data-ttu-id="6e562-107">На узле пакет средств разработки Azure стека hello [входа в](azure-stack-connect-azure-stack.md) toohello Администратор портала (`https://adminportal.local.azurestack.external`) и нажмите кнопку **New** > **вычислений**  >  **Windows Server 2016 Datacenter Eval** > **создания**.</span><span class="sxs-lookup"><span data-stu-id="6e562-107">On hello Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) toohello administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="6e562-108">В hello **основы** колонке введите **имя**, **имя пользователя**, и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="6e562-108">In hello **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="6e562-109">Выберите **подписку**.</span><span class="sxs-lookup"><span data-stu-id="6e562-109">Choose a **Subscription**.</span></span> <span data-ttu-id="6e562-110">Создание **группы ресурсов**, или выберите существующий и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6e562-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="6e562-111">В hello **выберите размер** колонке нажмите кнопку **A1 Standard**, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="6e562-111">In hello **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="6e562-112">В hello **параметры** колонке примите значения по умолчанию hello и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="6e562-112">In hello **Settings** blade, accept hello defaults and click **OK**</span></span>
5. <span data-ttu-id="6e562-113">В hello **Сводка** колонка, щелкните **ОК** toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e562-113">In hello **Summary** blade, click **OK** toocreate hello virtual machine.</span></span>  
6. <span data-ttu-id="6e562-114">toosee новой виртуальной машины, нажмите кнопку **все ресурсы**, а затем найдите hello виртуальную машину и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="6e562-114">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="6e562-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e562-115">Next steps</span></span>
[<span data-ttu-id="6e562-116">С помощью hello порталы администратора и пользователя в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6e562-116">Using hello administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
