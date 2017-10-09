---
title: "Доменные службы Azure Active Directory: создание или выбор виртуальной сети | Документация Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="c15ca-103">Создание или выбор виртуальной сети для доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15ca-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="c15ca-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c15ca-104">Before you begin</span></span>
<span data-ttu-id="c15ca-105">См. слишком[сетевые аспекты для доменных служб Active Directory Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="c15ca-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="c15ca-106">Задача 2. Создание виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="c15ca-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="c15ca-107">Следующая задача конфигурации Hello является toocreate виртуальной сети Azure и подсеть внутри него.</span><span class="sxs-lookup"><span data-stu-id="c15ca-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="c15ca-108">Вам потребуется включить доменные службы Azure Active Directory в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="c15ca-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="c15ca-109">Если вы предпочитаете toouse существующей виртуальной сети, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="c15ca-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="c15ca-110">Убедитесь, что hello виртуальной сети Azure можно создать или выбрать toouse с доменными службами Active Directory Azure, принадлежащий tooan регионе Azure, которая поддерживается Azure доменными службами Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c15ca-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="c15ca-111">tooascertain hello регионах Azure, в которых доступен доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="c15ca-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="c15ca-112">Запишите имя hello tooensure hello виртуальной сети, при включении доменных служб Active Directory Azure на шаге дальнейшей настройки выбрать hello справа виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c15ca-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="c15ca-113">toocreate Azure виртуальной сети, в которой будет tooenable Azure доменных служб Active Directory, выполните эти инструкции по настройке:</span><span class="sxs-lookup"><span data-stu-id="c15ca-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="c15ca-114">Go toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c15ca-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c15ca-115">Выберите в левой области hello **сетей**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="c15ca-116">![Узел "Сети"](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="c15ca-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="c15ca-117">Hello **виртуальных сетей** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="c15ca-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="c15ca-118">В области задач hello hello нижней части окна hello, выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="c15ca-120">Щелкните **Сетевые службы**, а затем выберите **Виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Виртуальная сеть — быстрое создание](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="c15ca-122">Нажмите кнопку toocreate виртуальной сети, **быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="c15ca-123">Укажите **имя** для виртуальной сети и рассмотрите возможность выполнения следующих hello:</span><span class="sxs-lookup"><span data-stu-id="c15ca-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="c15ca-124">Вы можете tooconfigure **адресное пространство** или **максимальное число виртуальных Машин** для этой сети.</span><span class="sxs-lookup"><span data-stu-id="c15ca-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="c15ca-125">Можно оставить hello **DNS-сервер** в **нет** сейчас.</span><span class="sxs-lookup"><span data-stu-id="c15ca-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="c15ca-126">После включения доменных служб Active Directory Azure, вы можете обновить приветствия.</span><span class="sxs-lookup"><span data-stu-id="c15ca-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="c15ca-127">В hello **расположение** раскрывающегося списка выберите поддерживаемом регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="c15ca-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="c15ca-128">tooascertain hello регионах Azure, в которых доступен доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="c15ca-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="c15ca-129">toocreate виртуальной сети, нажмите кнопку **Создание виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Создание виртуальной сети для доменных служб Azure Active Directory](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="c15ca-131">После создания виртуальной сети, выберите имя hello hello виртуальной сети и нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c15ca-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Создание подсети](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="c15ca-133">В разделе **адресное пространство виртуальной сети**, нажмите кнопку **добавить подсеть**, а затем укажите подсеть с именем hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Создание подсети для доменных служб Azure Active Directory](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="c15ca-135">toocreate Здравствуйте подсети, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c15ca-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="c15ca-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c15ca-136">Next step</span></span>
[<span data-ttu-id="c15ca-137">Задача 3. Включение доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15ca-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
