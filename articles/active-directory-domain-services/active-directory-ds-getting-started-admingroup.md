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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="fd8c7-103">Включение доменных служб Azure Active Directory с помощью портала Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="fd8c7-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="fd8c7-104">Задача 3. Настройка административной группы</span><span class="sxs-lookup"><span data-stu-id="fd8c7-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="fd8c7-105">В рамках этой задачи конфигурации вы создадите административную группу в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="fd8c7-106">Эта специальная административная группа называется *Администраторы контроллера домена AAD*.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="fd8c7-107">Участникам этой группы предоставляются разрешения администратора для компьютеров, присоединенных к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="fd8c7-108">На компьютерах, присоединенных к домену, эта группа добавляется в группу "Администраторы".</span><span class="sxs-lookup"><span data-stu-id="fd8c7-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="fd8c7-109">Кроме того, участники этой группы могут подключаться по протоколу удаленного рабочего стола к компьютерам, присоединенным к домену.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="fd8c7-110">Вы не получаете разрешения администратора домена или администратора предприятия в управляемом домене, который вы создали с помощью доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="fd8c7-111">В управляемых доменах эти разрешения зарезервированы службой и не становятся доступными для пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="fd8c7-112">В то же время для выполнения некоторых привилегированных операций можно использовать специальную административную группу, созданную в этой задаче по настройке.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="fd8c7-113">Эти операции включают присоединение компьютеров к домену, добавление в группу администраторов на компьютерах, присоединенных к домену, и настройку групповой политики.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="fd8c7-114">Мастер автоматически создает административную группу в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="fd8c7-115">Эта группа называется "Администраторы AAD DC".</span><span class="sxs-lookup"><span data-stu-id="fd8c7-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="fd8c7-116">Если у вас уже есть группа с таким именем в каталоге Azure AD, мастер выберет ее.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="fd8c7-117">Настроить членство в группе можно на странице **Группу администраторов** мастера.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="fd8c7-118">Чтобы настроить членство в группе, щелкните **Администраторы AAD DC**.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Настройка членства в группе](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="fd8c7-120">Нажмите кнопку **Добавить членов**, чтобы добавить пользователей из вашего каталога Azure AD в группу администраторов.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="fd8c7-121">Закончив, нажмите кнопку **ОК** для перехода на страницу **Сводка** мастера.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="fd8c7-122">На странице **Сводка** просмотрите параметры конфигурации для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="fd8c7-123">При необходимости можно вернуться к любому шагу мастера, чтобы внести изменения.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="fd8c7-124">По завершении нажмите кнопку **ОК**, чтобы создать управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Сводка](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="fd8c7-126">Вы увидите уведомление с отображением хода выполнения развертывания доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="fd8c7-127">Щелкните уведомление, чтобы просмотреть подробное описание хода развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Уведомление — выполняется развертывание](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="fd8c7-129">Подготовка управляемого домена</span><span class="sxs-lookup"><span data-stu-id="fd8c7-129">Provision your managed domain</span></span>
<span data-ttu-id="fd8c7-130">Процесс подготовки управляемого домена может занять до одного часа.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="fd8c7-131">Во время развертывания можно выполнить поиск, введя "доменные службы" в поле поиска **Поиск ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="fd8c7-132">В списке результатов выберите **Доменные службы Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="fd8c7-133">В колонке **Доменные службы Azure AD** будет указан подготавливаемый управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Поиск подготавливаемого управляемого домена](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="fd8c7-135">Щелкните имя управляемого домена (например, "contoso100.com") для получения дополнительных сведений о домене.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Доменные службы — состояние подготовки](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="fd8c7-137">На вкладке **Обзор** можно увидеть, что в настоящее время идет подготовка домена.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="fd8c7-138">Настроить управляемый домен можно только после его полной подготовки.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="fd8c7-139">Полная подготовка управляемого домена может длиться до часа.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="fd8c7-140">Доменные службы — вкладка "Обзор" во время состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="fd8c7-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="fd8c7-141">После полной подготовки управляемого домена на вкладке **Обзор** состояние домена отображается как **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="fd8c7-143">На вкладке **Свойства** отображаются два IP-адреса, по которым контроллеры домена доступны для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fd8c7-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Доменные службы — вкладка "Свойства" после полной подготовки](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="fd8c7-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd8c7-145">Next step</span></span>
[<span data-ttu-id="fd8c7-146">Задача 4. Обновление настроек DNS для виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="fd8c7-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
