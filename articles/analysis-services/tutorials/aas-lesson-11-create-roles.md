---
title: "Учебник по службам Azure Analysis Services: занятие 11 \"Создание ролей\" | Документы Майкрософт"
description: "Описание создания ролей в учебном проекте служб Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="9bf8e-103">Занятие 11. Создание ролей</span><span class="sxs-lookup"><span data-stu-id="9bf8e-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9bf8e-104">На этом занятии мы создадим роли.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-104">In this lesson, you create roles.</span></span> <span data-ttu-id="9bf8e-105">Роли обеспечивают безопасность данных и объектов базы данных модели, разрешая доступ только тем пользователям, которые являются членами роли.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="9bf8e-106">Каждая роль определяется с помощью одного разрешения: "Нет", "Чтение", "Чтение и обработка", "Обработка" или "Администратор".</span><span class="sxs-lookup"><span data-stu-id="9bf8e-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="9bf8e-107">Роли можно определить во время создания модели с помощью диспетчера ролей.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="9bf8e-108">После развертывания модели ролями можно управлять с помощью SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="9bf8e-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9bf8e-109">Дополнительные сведения см.в статье [Роли](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="9bf8e-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="9bf8e-110">Создание ролей не является обязательным для прохождения этого учебника.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="9bf8e-111">По умолчанию учетная запись, с использованием которой вы выполнили вход, предоставляет права администратора для работы с моделью.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="9bf8e-112">А чтобы разрешить другим корпоративным пользователям просматривать модель с помощью клиента отчетов, необходимо создать хотя бы одну роль с разрешениями на чтение и добавить этих пользователей в качестве членов роли.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="9bf8e-113">Мы создадим три роли.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="9bf8e-114">**Менеджер по продажам** — эта роль может включать пользователей вашей организации, которым вы ходите предоставить права на чтение всех объектов и данных модели.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="9bf8e-115">**Аналитик по сбыту в США** — эта роль может включать пользователей вашей организации, для которых требуется только возможность просмотра данных, связанных с продажами в США.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="9bf8e-116">Для этой роли будет использоваться формула DAX для определения *фильтра строк*, который позволит членам роли просматривать данные только по США.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="9bf8e-117">**Администратор** — эта роль может включать пользователей, для которых требуются права администратора, то есть неограниченный доступ и разрешения для выполнения административных задач в базе данных модели.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="9bf8e-118">Поскольку учетные записи пользователей и групп Windows в вашей организации уникальны, вы можете добавить в роль учетные записи из вашей организации.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="9bf8e-119">Однако в рамках этого учебника участников роли можно не указывать.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="9bf8e-120">Вы сможете проверить влияние каждой роли позже в ходе занятия 12 ("Анализ в Excel").</span><span class="sxs-lookup"><span data-stu-id="9bf8e-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="9bf8e-121">Предполагаемое время выполнения этого занятия: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="9bf8e-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9bf8e-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9bf8e-122">Prerequisites</span></span>  
<span data-ttu-id="9bf8e-123">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="9bf8e-124">Прежде чем выполнять задачи в этом разделе, необходимо завершить предыдущее занятие: [Занятие 10. Создание разделов](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="9bf8e-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="9bf8e-125">Создание ролей</span><span class="sxs-lookup"><span data-stu-id="9bf8e-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="9bf8e-126">Создание роли пользователя "Менеджер по продажам"</span><span class="sxs-lookup"><span data-stu-id="9bf8e-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="9bf8e-127">В обозревателе табличных моделей щелкните правой кнопкой мыши **Роли** > **Роли**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="9bf8e-128">В диспетчере ролей нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="9bf8e-129">Щелкните новую роль, а затем в столбце **Имя** присвойте роли имя **Менеджер по продажам**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="9bf8e-130">В столбце **Разрешения** щелкните раскрывающийся список и выберите разрешение **Чтение**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="9bf8e-132">Дополнительно: откройте вкладку **Члены**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="9bf8e-133">В диалоговом окне **Выбор пользователей или групп** укажите пользователей или группы Windows из вашей организации, которым вы хотите назначить эту роль.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="9bf8e-134">Создание роли пользователя "Аналитик по сбыту в США"</span><span class="sxs-lookup"><span data-stu-id="9bf8e-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="9bf8e-135">В диспетчере ролей нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="9bf8e-136">Переименуйте роль в **Аналитик по сбыту в США**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="9bf8e-137">Предоставьте этой роли разрешение **Чтение**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="9bf8e-138">Перейдите на вкладку "Фильтры строк", а затем только для таблицы **DimGeography** в столбце "Фильтр DAX" введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="9bf8e-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="9bf8e-139">Формула фильтра строк должна разрешаться в логическое значение (TRUE/FALSE).</span><span class="sxs-lookup"><span data-stu-id="9bf8e-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="9bf8e-140">С помощью этой формулы вы указываете, что для пользователя будут отображаться только строки с определенным значением кода страны или региона — США.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="9bf8e-142">Дополнительно: откройте вкладку **Члены**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="9bf8e-143">В диалоговом окне **Выбор пользователей или групп** укажите пользователей или группы Windows из вашей организации, которым вы хотите назначить эту роль.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="9bf8e-144">Создание роли пользователя "Администратор"</span><span class="sxs-lookup"><span data-stu-id="9bf8e-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="9bf8e-145">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="9bf8e-146">Переименуйте роль в **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="9bf8e-147">Предоставьте этой роли разрешение **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="9bf8e-148">Дополнительно: откройте вкладку **Члены**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="9bf8e-149">В диалоговом окне **Выбор пользователей или групп** укажите пользователей или группы Windows из вашей организации, которым вы хотите назначить эту роль.</span><span class="sxs-lookup"><span data-stu-id="9bf8e-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="9bf8e-150">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="9bf8e-150">What's next?</span></span>
<span data-ttu-id="9bf8e-151">[Занятие 12. Анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="9bf8e-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
