---
title: "Azure доменных служб Active Directory: Создание группы администраторов hello Azure AD DC | Документы Microsoft"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="9800e-103">Включение Azure доменных служб Active Directory с помощью hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="9800e-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="9800e-104">В этой статье описываются и рассматриваются задачи настройки hello, необходимые для вас tooenable Active Directory домена служб Azure (Azure AD DS) для вашего клиента Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9800e-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="9800e-105">[**Попробуйте вместо этого использовать новый интерфейс портала hello Azure (Предварительная версия)**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9800e-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="9800e-106">Задача 1: Создание группы «Администраторы» контроллера домена hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9800e-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="9800e-107">Первая задача Hello — toocreate административной группы в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9800e-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="9800e-108">Эта специальная административная группа называется *Администраторы контроллера домена AAD*.</span><span class="sxs-lookup"><span data-stu-id="9800e-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="9800e-109">Члены этой группы предоставляются административные разрешения на компьютеры, присоединенные к домену toohello управляемых доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9800e-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="9800e-110">На компьютерах, присоединенных к домену эта группа добавляется toohello группы «Администраторы».</span><span class="sxs-lookup"><span data-stu-id="9800e-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="9800e-111">Кроме того члены этой группы можно использовать машины удаленно присоединенных toodomain tooconnect удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="9800e-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="9800e-112">Нет разрешений администратора домена или администратора предприятия на hello управляемый домен, созданный с помощью доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9800e-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9800e-113">На управляемые домены эти разрешения защищены службой hello и не становятся доступны toousers в рамках клиента hello.</span><span class="sxs-lookup"><span data-stu-id="9800e-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="9800e-114">Тем не менее, можно использовать hello специальных административных Создание группы в этой конфигурации задачи tooperform некоторые привилегированные операции.</span><span class="sxs-lookup"><span data-stu-id="9800e-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="9800e-115">Эти операции включают toohello компьютеров к домену, принадлежащий группы администрирования toohello на присоединенных к домену компьютерах и Настройка групповой политики.</span><span class="sxs-lookup"><span data-stu-id="9800e-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="9800e-116">В этой задаче конфигурации создать административную группу hello и добавить одного или нескольких пользователей в группе toohello каталога.</span><span class="sxs-lookup"><span data-stu-id="9800e-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="9800e-117">toocreate hello административной группы Azure доменных служб Active Directory, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="9800e-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="9800e-118">Go toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9800e-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9800e-119">В левой области hello выберите hello **Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9800e-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="9800e-120">Выберите клиент Azure AD hello (каталог), для которого требуется доменных служб tooenable Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9800e-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9800e-121">Для каждого каталога Azure AD можно создать только один домен.</span><span class="sxs-lookup"><span data-stu-id="9800e-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="9800e-123">На hello **Предварительный просмотр каталога** щелкните hello **группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9800e-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="9800e-124">Щелкните клиента tooyour Azure AD группы, в области задач hello hello нижней части окна hello tooadd **добавить группу**.</span><span class="sxs-lookup"><span data-stu-id="9800e-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![Кнопка Добавить группу Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="9800e-126">В hello **добавить группу** диалогового окна поле, создайте группу с именем **Администраторы контроллера домена AAD**и задайте **тип группы** слишком**безопасности**.</span><span class="sxs-lookup"><span data-stu-id="9800e-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="9800e-127">tooenable доступ в том же домене управляемых доменных служб Active Directory Azure, создайте группу с указанным именем точно.</span><span class="sxs-lookup"><span data-stu-id="9800e-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Добавить группу Hello-диалоговое окно](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="9800e-129">В hello **описание** введите описание, которое позволяет другим toounderstand, что эта группа предоставляет административные разрешения в доменных службах Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9800e-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="9800e-130">После создания группы hello, щелкните имя tooview hello группы его свойства.</span><span class="sxs-lookup"><span data-stu-id="9800e-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="9800e-131">tooadd пользователей в качестве членов группы hello hello нижней части окна hello щелкните hello **добавить членов** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9800e-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Кнопка "Добавить участников"](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="9800e-133">В hello **добавление членов** диалоговое окно, выберите hello пользователей, которые должны быть членами этой группы и нажмите кнопку hello значком на hello внизу справа.</span><span class="sxs-lookup"><span data-stu-id="9800e-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Добавить группу пользователей tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="9800e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9800e-135">Next step</span></span>
[<span data-ttu-id="9800e-136">Задача 2. Создание или выбор виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="9800e-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
