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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="01c44-103">Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="01c44-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="01c44-104">Задача 3. Настройка административной группы</span><span class="sxs-lookup"><span data-stu-id="01c44-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="01c44-105">В рамках этой задачи конфигурации вы создадите административную группу в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01c44-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="01c44-106">Эта специальная административная группа называется *Администраторы контроллера домена AAD*.</span><span class="sxs-lookup"><span data-stu-id="01c44-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="01c44-107">Члены этой группы предоставляются права администратора на компьютерах, присоединенных к домену toohello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="01c44-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="01c44-108">На компьютерах, присоединенных к домену эта группа добавляется toohello группы «Администраторы».</span><span class="sxs-lookup"><span data-stu-id="01c44-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="01c44-109">Кроме того члены этой группы можно использовать машины удаленно присоединенных toodomain tooconnect удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="01c44-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="01c44-110">Нет разрешений администратора домена или администратора предприятия на hello управляемый домен, созданный с помощью доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="01c44-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="01c44-111">На управляемые домены эти разрешения защищены службой hello и не становятся доступны toousers в рамках клиента hello.</span><span class="sxs-lookup"><span data-stu-id="01c44-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="01c44-112">Тем не менее, можно использовать hello специальных административных Создание группы в этой конфигурации задачи tooperform некоторые привилегированные операции.</span><span class="sxs-lookup"><span data-stu-id="01c44-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="01c44-113">Эти операции включают toohello компьютеров к домену, принадлежащий группы администрирования toohello на присоединенных к домену компьютерах и Настройка групповой политики.</span><span class="sxs-lookup"><span data-stu-id="01c44-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="01c44-114">Hello мастер автоматически создаст hello административную группу в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01c44-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="01c44-115">Эта группа называется "Администраторы AAD DC".</span><span class="sxs-lookup"><span data-stu-id="01c44-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="01c44-116">При наличии существующей группы с таким именем в каталоге Azure AD hello мастер выбирает эту группу.</span><span class="sxs-lookup"><span data-stu-id="01c44-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="01c44-117">Можно настроить с помощью hello членство в группе **группу администраторов** страницу мастера.</span><span class="sxs-lookup"><span data-stu-id="01c44-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="01c44-118">членство в группе tooconfigure, нажмите кнопку **Администраторы контроллера домена AAD**.</span><span class="sxs-lookup"><span data-stu-id="01c44-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Настройка членства в группе](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="01c44-120">Нажмите кнопку hello **добавление членов** кнопку tooadd пользователей из вашей группы администраторов toohello каталог Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01c44-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="01c44-121">Закончив, нажмите кнопку **ОК** toomove на toohello **Сводка** на странице приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="01c44-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="01c44-122">На hello **Сводка** приветствия мастера просмотрите параметры конфигурации hello hello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="01c44-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="01c44-123">Можно вернуться к нему tooany шаге мастера toomake hello изменяется, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="01c44-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="01c44-124">Закончив, нажмите кнопку **ОК** toocreate hello создать управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="01c44-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Сводка](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="01c44-126">Вы увидите уведомление, которое отображает hello ход выполнения развертывания доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01c44-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="01c44-127">Щелкните уведомление hello toosee подробные ход выполнения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="01c44-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Уведомление — выполняется развертывание](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="01c44-129">Подготовка управляемого домена</span><span class="sxs-lookup"><span data-stu-id="01c44-129">Provision your managed domain</span></span>
<span data-ttu-id="01c44-130">Hello процесс подготовки управляемого домена может занять час tooan.</span><span class="sxs-lookup"><span data-stu-id="01c44-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="01c44-131">Во время развертывания можно выполнить поиск «доменных служб» hello **Найдите ресурсы** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="01c44-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="01c44-132">Выберите **доменные службы Azure AD** из результатов поиска hello.</span><span class="sxs-lookup"><span data-stu-id="01c44-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="01c44-133">Hello **доменные службы Azure AD** колонке перечислены hello управляемый домен, который подготавливается в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="01c44-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Поиск подготавливаемого управляемого домена](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="01c44-135">Щелкните имя hello toosee hello управляемого домена (например, «contoso100.com») Дополнительные сведения о домене hello.</span><span class="sxs-lookup"><span data-stu-id="01c44-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Доменные службы — состояние подготовки](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="01c44-137">Hello **Обзор** вкладке отображается в настоящее время идет подготовка домена hello.</span><span class="sxs-lookup"><span data-stu-id="01c44-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="01c44-138">Не удается настроить hello управляемого домена до полной инициализации.</span><span class="sxs-lookup"><span data-stu-id="01c44-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="01c44-139">Это может потребоваться до часа tooan вашей toobe управляемый домен полностью подготовлены.</span><span class="sxs-lookup"><span data-stu-id="01c44-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="01c44-140">Доменные службы - вкладка обзора во время hello состояние подготовки</span><span class="sxs-lookup"><span data-stu-id="01c44-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="01c44-141">Здравствуйте, когда управляемый домен hello полностью подготовлены, **Обзор** вкладке отображается состояние домена hello как **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="01c44-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="01c44-143">На hello **свойства** вкладке появится два IP-адреса, в какой домен контроллеров доступны для hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="01c44-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Доменные службы — вкладка "Свойства" после полной подготовки](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="01c44-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01c44-145">Next step</span></span>
[<span data-ttu-id="01c44-146">Задача 4: обновите параметры DNS hello для hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="01c44-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
