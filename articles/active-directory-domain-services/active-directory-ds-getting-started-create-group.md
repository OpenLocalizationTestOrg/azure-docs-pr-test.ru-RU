---
title: "Доменные службы Azure Active Directory: создание группы администраторов контроллера домена Azure AD | Документация Майкрософт"
description: "Включение доменных служб Azure Active Directory с помощью классического портала Azure"
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="ed708-103">Включение доменных служб Azure Active Directory с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="ed708-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="ed708-104">В этой статье описываются и демонстрируются задачи по настройке, которые необходимо выполнить, чтобы включить доменные службы Azure Active Directory (Azure AD DS) для клиента Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed708-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="ed708-105">[**Попробуйте новый интерфейс предварительной версии портала Azure**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed708-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="ed708-106">Задача 1. Создание группы администраторов контроллера домена Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed708-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="ed708-107">Первой задачей является создание административной группы в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed708-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="ed708-108">Эта специальная административная группа называется *Администраторы контроллера домена AAD*.</span><span class="sxs-lookup"><span data-stu-id="ed708-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="ed708-109">Участникам этой группы предоставляются разрешения администратора для компьютеров, присоединенных к управляемому домену доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed708-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="ed708-110">На компьютерах, присоединенных к домену, эта группа добавляется в группу "Администраторы".</span><span class="sxs-lookup"><span data-stu-id="ed708-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="ed708-111">Кроме того, участники этой группы могут подключаться по протоколу удаленного рабочего стола к компьютерам, присоединенным к домену.</span><span class="sxs-lookup"><span data-stu-id="ed708-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="ed708-112">Вы не получаете разрешения администратора домена или администратора предприятия в управляемом домене, который вы создали с помощью доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed708-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ed708-113">В управляемых доменах эти разрешения зарезервированы службой и не становятся доступными для пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="ed708-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="ed708-114">В то же время для выполнения некоторых привилегированных операций можно использовать специальную административную группу, созданную в этой задаче по настройке.</span><span class="sxs-lookup"><span data-stu-id="ed708-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="ed708-115">Эти операции включают присоединение компьютеров к домену, добавление в группу администраторов на компьютерах, присоединенных к домену, и настройку групповой политики.</span><span class="sxs-lookup"><span data-stu-id="ed708-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="ed708-116">При выполнении этой задачи по настройке вы создадите административную группу и добавите в нее одного или нескольких пользователей из своего каталога.</span><span class="sxs-lookup"><span data-stu-id="ed708-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="ed708-117">Чтобы создать административную группу для доменных служб Azure Active Directory, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ed708-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="ed708-118">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ed708-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ed708-119">В области слева нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed708-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="ed708-120">Выберите клиент (каталог) Azure AD, для которого требуется включить доменные службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed708-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ed708-121">Для каждого каталога Azure AD можно создать только один домен.</span><span class="sxs-lookup"><span data-stu-id="ed708-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="ed708-123">На странице **предварительного просмотра каталога** щелкните вкладку **Группы**.</span><span class="sxs-lookup"><span data-stu-id="ed708-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="ed708-124">Чтобы добавить группу в свой клиент Azure AD, в области задач в нижней части окна щелкните **Добавить группу**.</span><span class="sxs-lookup"><span data-stu-id="ed708-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![Кнопка "Добавить группу"](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="ed708-126">В диалоговом окне **Добавление группы** создайте группу с именем **AAD DC Administrators** (Администраторы контроллера домена AAD), а для параметра **Тип группы** укажите **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="ed708-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="ed708-127">Для доступа внутри управляемого домена доменных служб Azure Active Directory создайте группу с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="ed708-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Диалоговое окно "Добавление группы"](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="ed708-129">В поле **Описание** введите описание, которое позволит другим пользователям понять, что эта группа предоставляет разрешения администратора в доменных службах Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="ed708-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="ed708-130">После создания группы щелкните имя группы, чтобы просмотреть ее свойства.</span><span class="sxs-lookup"><span data-stu-id="ed708-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="ed708-131">В нижней части окна нажмите кнопку **Добавить участников**, чтобы добавить пользователей в качестве участников этой группы.</span><span class="sxs-lookup"><span data-stu-id="ed708-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Кнопка "Добавить участников"](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="ed708-133">В диалоговом окне **Добавление участников** выберите пользователей, которые должны стать членами этой группы, а затем щелкните значок в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="ed708-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Добавление пользователей в группу администраторов](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="ed708-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed708-135">Next step</span></span>
[<span data-ttu-id="ed708-136">Задача 2. Создание или выбор виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="ed708-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
