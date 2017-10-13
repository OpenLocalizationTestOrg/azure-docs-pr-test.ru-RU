---
title: "Создание тестовой виртуальной Машине в Azure стек | Документы Microsoft"
description: "Узнайте, как подготовка тестовой виртуальной Машине в стеке Azure как оператор облака."
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
ms.date: 9/25/2017
ms.author: erikje
ms.openlocfilehash: 233cf4df53af6a49e5fe4c5d51e112d8196a7530
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="d78b5-103">Создать тестовую виртуальную машину в стек Azure</span><span class="sxs-lookup"><span data-stu-id="d78b5-103">Create a test virtual machine in Azure Stack</span></span>

<span data-ttu-id="d78b5-104">*Применяется к: Azure стека пакет средств разработки*</span><span class="sxs-lookup"><span data-stu-id="d78b5-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="d78b5-105">Как оператор стек Azure можно создать тестовую виртуальную машину для проверки вашей [стека Azure](azure-stack-poc.md) развертывания пакет средств разработки.</span><span class="sxs-lookup"><span data-stu-id="d78b5-105">As an Azure Stack operator, you can create a test virtual machine to validate your [Azure Stack](azure-stack-poc.md) Developer Kit deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="d78b5-106">Прежде чем можно подготовить виртуальные машины, необходимо [добавить образ Windows Server 2016 Evaluation в стек Azure Marketplace](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="d78b5-106">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="d78b5-107">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d78b5-107">Create a virtual machine</span></span>
1. <span data-ttu-id="d78b5-108">На узле пакет средств разработки Azure стека [входа](azure-stack-connect-azure-stack.md) портал администратора (`https://adminportal.local.azurestack.external`) и нажмите кнопку **New** > **вычислений**  >  **Windows Server 2016 Datacenter Eval** > **создания**.</span><span class="sxs-lookup"><span data-stu-id="d78b5-108">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="d78b5-109">В **основы** колонке введите **имя**, **имя пользователя**, и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d78b5-109">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="d78b5-110">Выберите **подписку**.</span><span class="sxs-lookup"><span data-stu-id="d78b5-110">Choose a **Subscription**.</span></span> <span data-ttu-id="d78b5-111">Создание **группы ресурсов**, или выберите существующий и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d78b5-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="d78b5-112">В **выберите размер** колонке нажмите кнопку **A1 Standard**, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="d78b5-112">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="d78b5-113">В **параметры** колонке примите значения по умолчанию и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="d78b5-113">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="d78b5-114">В **Сводка** колонка, щелкните **ОК** для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d78b5-114">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="d78b5-115">Для просмотра на новую виртуальную машину, щелкните **все ресурсы**, а затем найдите виртуальную машину и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="d78b5-115">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="d78b5-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d78b5-116">Next steps</span></span>
[<span data-ttu-id="d78b5-117">С помощью порталы администратора и пользователя в стек Azure</span><span class="sxs-lookup"><span data-stu-id="d78b5-117">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
