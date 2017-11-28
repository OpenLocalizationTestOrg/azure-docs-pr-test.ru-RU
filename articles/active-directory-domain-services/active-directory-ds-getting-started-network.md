---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="84c42-103">Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="84c42-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="84c42-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="84c42-104">Before you begin</span></span>
<span data-ttu-id="84c42-105">См. слишком[сетевые аспекты для доменных служб Active Directory Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="84c42-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="84c42-106">Задача 2. Настройка сетевых параметров</span><span class="sxs-lookup"><span data-stu-id="84c42-106">Task 2: configure network settings</span></span>
<span data-ttu-id="84c42-107">Следующая задача конфигурации Hello является toocreate виртуальной сети Azure и выделенная подсеть внутри него.</span><span class="sxs-lookup"><span data-stu-id="84c42-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="84c42-108">Вам потребуется включить доменные службы Azure Active Directory в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="84c42-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="84c42-109">Можно также выбрать существующую виртуальную сеть и создать подсеть hello выделенных в нем.</span><span class="sxs-lookup"><span data-stu-id="84c42-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="84c42-110">Нажмите кнопку **виртуальная сеть** tooselect виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="84c42-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="84c42-111">На hello **виртуальной сети выберите** колонку, вы видите все существующие виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="84c42-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="84c42-112">Вы видите только hello виртуальных сетей, принадлежащих toohello группы ресурсов и расположение Azure, выбранные на hello **основы** страницу мастера.</span><span class="sxs-lookup"><span data-stu-id="84c42-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="84c42-113">Выберите hello виртуальную сеть, в которой следует использовать доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84c42-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="84c42-114">Нажмите кнопку **создать новый**, если вы предпочитаете toocreate новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="84c42-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="84c42-115">Для доменных служб Azure Active Directory настоятельно рекомендуется использовать выделенную подсеть.</span><span class="sxs-lookup"><span data-stu-id="84c42-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="84c42-116">Если вы выберете существующей виртуальной сети, [Создание выделенной подсети с помощью расширения виртуальных сетей hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , затем выберите этой подсети.</span><span class="sxs-lookup"><span data-stu-id="84c42-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Выбор виртуальной сети](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="84c42-118">Нажмите кнопку **подсети** toopick hello выделенной подсети в этой виртуальной сети, в течение которого tooenable нового управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="84c42-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="84c42-119">В hello **создать подсеть** , укажите имя для подсети hello и, при необходимости щелкните **ОК** после завершения работы.</span><span class="sxs-lookup"><span data-stu-id="84c42-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="84c42-120">Например можно создайте подсеть с именем hello «DomainServices», упрощая для других администраторов toounderstand что развернута в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="84c42-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Выберите подсеть внутри виртуальной сети hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="84c42-122">**Рекомендации по выбору подсети**</span><span class="sxs-lookup"><span data-stu-id="84c42-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="84c42-123">Используйте выделенную подсеть для доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84c42-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="84c42-124">Не развертывайте какой-либо подсети toothis виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="84c42-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="84c42-125">Эта конфигурация позволяет tooconfigure сетевой группы безопасности (Nsg) для рабочих нагрузок и виртуальных машин без нарушения управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="84c42-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="84c42-126">Дополнительные сведения см. в статье [Рекомендации по сетям для доменных служб Azure AD](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="84c42-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="84c42-127">Не устанавливайте hello подсеть шлюза для развертывания доменные службы Azure AD, так как он не является поддерживаемой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="84c42-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="84c42-128">Убедитесь, что достаточно доступное адресное пространство — по крайней мере 3-5 доступных IP-адресов этой подсети hello, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="84c42-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="84c42-129">Закончив, нажмите кнопку **ОК** toomove на toohello **группу администраторов** на странице приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="84c42-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="84c42-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84c42-130">Next step</span></span>
[<span data-ttu-id="84c42-131">Задача 3. Настройка административной группы и включение доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="84c42-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
