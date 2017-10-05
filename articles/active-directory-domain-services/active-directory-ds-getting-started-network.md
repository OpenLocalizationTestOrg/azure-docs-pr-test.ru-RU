---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение доменных служб Azure Active Directory с помощью портала Azure (предварительная версия)"
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
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="b6e25-103">Включение доменных служб Azure Active Directory с помощью портала Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b6e25-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="b6e25-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b6e25-104">Before you begin</span></span>
<span data-ttu-id="b6e25-105">См. статью [Рекомендации по сетям для доменных служб Azure AD](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b6e25-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="b6e25-106">Задача 2. Настройка сетевых параметров</span><span class="sxs-lookup"><span data-stu-id="b6e25-106">Task 2: configure network settings</span></span>
<span data-ttu-id="b6e25-107">Следующая задача по настройке — создать виртуальную сеть Azure c выделенной подсетью.</span><span class="sxs-lookup"><span data-stu-id="b6e25-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="b6e25-108">Вам потребуется включить доменные службы Azure Active Directory в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="b6e25-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="b6e25-109">Можно также выбрать существующую виртуальную сеть и создать выделенную подсеть внутри нее.</span><span class="sxs-lookup"><span data-stu-id="b6e25-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="b6e25-110">Щелкните **Виртуальная сеть**, чтобы выбрать виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="b6e25-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="b6e25-111">В колонке **Выбор виртуальной сети** представлены все имеющиеся виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="b6e25-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="b6e25-112">Отображаются только виртуальные сети, принадлежащие к группе ресурсов и расположению Azure, которые выбраны странице **Основное** мастера.</span><span class="sxs-lookup"><span data-stu-id="b6e25-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="b6e25-113">Выберите виртуальную сеть, в которой следует включить доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6e25-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="b6e25-114">Нажмите **Создать новую**, если требуется создать новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="b6e25-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="b6e25-115">Для доменных служб Azure Active Directory настоятельно рекомендуется использовать выделенную подсеть.</span><span class="sxs-lookup"><span data-stu-id="b6e25-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b6e25-116">Если выбрать существующую виртуальную сеть, [создайте выделенную подсеть с помощью расширения виртуальных сетей](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), а затем выберите эту подсеть.</span><span class="sxs-lookup"><span data-stu-id="b6e25-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Выбор виртуальной сети](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="b6e25-118">Нажмите **Подсети**, чтобы выбрать выделенную подсеть в этой виртуальной сети, в которой необходимо включить новый управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="b6e25-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="b6e25-119">В колонке **Создать подсеть** укажите имя подсети, а затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b6e25-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="b6e25-120">Например, можно создать подсеть с именем "DomainServices", чтобы другие администраторы смогли с легкостью понять, что развернуто в подсети.</span><span class="sxs-lookup"><span data-stu-id="b6e25-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Выбор подсети в виртуальной сети](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="b6e25-122">**Рекомендации по выбору подсети**</span><span class="sxs-lookup"><span data-stu-id="b6e25-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="b6e25-123">Используйте выделенную подсеть для доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b6e25-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b6e25-124">Не развертывайте другие виртуальные машины в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="b6e25-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="b6e25-125">Такая конфигурация позволяет настроить группы безопасности сети (NSG) для рабочих нагрузок и виртуальных машин без нарушения целостности управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="b6e25-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="b6e25-126">Дополнительные сведения см. в статье [Рекомендации по сетям для доменных служб Azure AD](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b6e25-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="b6e25-127">Не используйте подсеть шлюза для развертывания доменных служб Azure Active Directory, поскольку это не является поддерживаемой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="b6e25-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="b6e25-128">Убедитесь в том, что в выбранной подсети имеется достаточное доступное адресное пространство — не менее 3–5 доступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="b6e25-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="b6e25-129">По завершении нажмите **ОК** для перехода на страницу **Группа администраторов** в мастере.</span><span class="sxs-lookup"><span data-stu-id="b6e25-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="b6e25-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6e25-130">Next step</span></span>
[<span data-ttu-id="b6e25-131">Задача 3. Настройка административной группы и включение доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6e25-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
