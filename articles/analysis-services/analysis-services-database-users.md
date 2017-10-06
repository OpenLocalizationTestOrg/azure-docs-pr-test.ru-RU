---
title: "aaaManage базы данных, ролей и пользователей в Azure Analysis Services | Документы Microsoft"
description: "Узнайте, как toomanage базы данных, ролей и пользователей на сервере служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="eba9d-103">Управление ролями и пользователями базы данных</span><span class="sxs-lookup"><span data-stu-id="eba9d-103">Manage database roles and users</span></span>

<span data-ttu-id="eba9d-104">На уровне базы данных модели hello все пользователи должны принадлежать роли tooa.</span><span class="sxs-lookup"><span data-stu-id="eba9d-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="eba9d-105">Роли определяют пользователей с определенной разрешения для базы данных model hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="eba9d-106">Любой пользователь или группа безопасности добавлены tooa роли необходимо настроить учетную запись в клиенте Azure AD в hello ту же подписку сервер hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="eba9d-107">Определение ролей имеет разные в зависимости от используемого средства hello, но эффект hello Здравствуйте, одинаково.</span><span class="sxs-lookup"><span data-stu-id="eba9d-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="eba9d-108">Разрешения ролей включают следующие:</span><span class="sxs-lookup"><span data-stu-id="eba9d-108">Role permissions include:</span></span>
*  <span data-ttu-id="eba9d-109">**Администратор** -пользователи имеют полные разрешения для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="eba9d-110">Роли базы данных с разрешениями администратора и администраторы сервера — это не одно и тоже.</span><span class="sxs-lookup"><span data-stu-id="eba9d-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="eba9d-111">**Процесс** -пользователи могут подключаться tooand выполнения процесса операций в базе данных hello и анализировать данные модели базы данных.</span><span class="sxs-lookup"><span data-stu-id="eba9d-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="eba9d-112">**Чтение** -пользователи могут использовать клиент приложения tooconnect tooand анализ модели базы данных.</span><span class="sxs-lookup"><span data-stu-id="eba9d-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="eba9d-113">При создании проекта табличной модели, вы создаете роли и добавление пользователей или групп toothose ролей с помощью диспетчера ролей в SSDT.</span><span class="sxs-lookup"><span data-stu-id="eba9d-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="eba9d-114">При развернутом tooa, с помощью SSMS [командлеты PowerShell для служб Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), или [языке скриптов табличных моделей](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) или удалить роли и члены пользователя.</span><span class="sxs-lookup"><span data-stu-id="eba9d-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="eba9d-115">tooadd или управления ролями и пользователями в SSDT</span><span class="sxs-lookup"><span data-stu-id="eba9d-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="eba9d-116">Выберите в SSDT **Обозреватель табличных моделей**, а затем щелкните правой кнопкой мыши **Роли**.</span><span class="sxs-lookup"><span data-stu-id="eba9d-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="eba9d-117">В **диспетчере ролей** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eba9d-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="eba9d-118">Введите имя для роли hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="eba9d-119">По умолчанию hello имя роли по умолчанию hello номер, последовательно увеличивающийся для каждой новой роли.</span><span class="sxs-lookup"><span data-stu-id="eba9d-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="eba9d-120">Рекомендуется ввести имя, ясно определяющее тип члена hello, например, финансовые менеджеры или специалисты по кадрам.</span><span class="sxs-lookup"><span data-stu-id="eba9d-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="eba9d-121">Выберите один из hello следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="eba9d-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="eba9d-122">Разрешение</span><span class="sxs-lookup"><span data-stu-id="eba9d-122">Permission</span></span>|<span data-ttu-id="eba9d-123">Описание</span><span class="sxs-lookup"><span data-stu-id="eba9d-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="eba9d-124">**None**</span><span class="sxs-lookup"><span data-stu-id="eba9d-124">**None**</span></span>|<span data-ttu-id="eba9d-125">Члены не могут изменять схему модели hello и просматривать данные.</span><span class="sxs-lookup"><span data-stu-id="eba9d-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="eba9d-126">**чтение**</span><span class="sxs-lookup"><span data-stu-id="eba9d-126">**Read**</span></span>|<span data-ttu-id="eba9d-127">Члены могут запрашивать данные (с учетом фильтров строк), но не могут изменять схему модели hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="eba9d-128">**Чтение и обработка**</span><span class="sxs-lookup"><span data-stu-id="eba9d-128">**Read and Process**</span></span>|<span data-ttu-id="eba9d-129">Члены могут запрашивать данные (на основе фильтров строк) и выполнения процесса и обработать все операции, но не могут изменять схему модели hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="eba9d-130">**Описание процесса**</span><span class="sxs-lookup"><span data-stu-id="eba9d-130">**Process**</span></span>|<span data-ttu-id="eba9d-131">Участники могут выполнять операции обработки и массовой обработки,</span><span class="sxs-lookup"><span data-stu-id="eba9d-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="eba9d-132">Не могут изменять схему модели hello и просматривать данные.</span><span class="sxs-lookup"><span data-stu-id="eba9d-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="eba9d-133">**Администратор**</span><span class="sxs-lookup"><span data-stu-id="eba9d-133">**Administrator**</span></span>|<span data-ttu-id="eba9d-134">Члены могут изменять схему модели hello и просматривать все данные.</span><span class="sxs-lookup"><span data-stu-id="eba9d-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="eba9d-135">При наличии роли hello Создание чтение или разрешение на чтение и процесса, можно добавить фильтры строк с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="eba9d-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="eba9d-136">Нажмите кнопку hello **фильтры строк** , а затем выберите таблицу, затем щелкните hello **фильтр DAX** поле, а затем введите формулу DAX.</span><span class="sxs-lookup"><span data-stu-id="eba9d-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="eba9d-137">Щелкните **Участники** > **Добавить внешнего участника**.</span><span class="sxs-lookup"><span data-stu-id="eba9d-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="eba9d-138">В разделе **Добавить внешнего участника** введите пользователей или группы в клиенте Azure AD, указав адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="eba9d-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="eba9d-139">После того как вы нажмете кнопку "ОК" и закроете диспетчер ролей, роли и участники ролей появятся в обозревателе табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="eba9d-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Роли и пользователи в обозревателе табличных моделей](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="eba9d-141">Развертывание сервера tooyour Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="eba9d-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="eba9d-142">tooadd или управления ролями и пользователями в среде SSMS</span><span class="sxs-lookup"><span data-stu-id="eba9d-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="eba9d-143">роли и пользователи tooa tooadd развернутой базе данных модели, должны быть toohello подключенного сервера, администратор сервера или уже в роли базы данных с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="eba9d-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="eba9d-144">В обозревателе объекта щелкните правой кнопкой мыши **Роли** > **Новая роль**.</span><span class="sxs-lookup"><span data-stu-id="eba9d-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="eba9d-145">В области **Создание роли** введите имя и описание роли.</span><span class="sxs-lookup"><span data-stu-id="eba9d-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="eba9d-146">Выберите разрешение.</span><span class="sxs-lookup"><span data-stu-id="eba9d-146">Select a permission.</span></span>
   |<span data-ttu-id="eba9d-147">Разрешение</span><span class="sxs-lookup"><span data-stu-id="eba9d-147">Permission</span></span>|<span data-ttu-id="eba9d-148">Описание</span><span class="sxs-lookup"><span data-stu-id="eba9d-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="eba9d-149">**Полный доступ (администратор)**</span><span class="sxs-lookup"><span data-stu-id="eba9d-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="eba9d-150">Члены могут изменять схему модели hello, обработки и просматривать все данные.</span><span class="sxs-lookup"><span data-stu-id="eba9d-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="eba9d-151">**Обработка базы данных**</span><span class="sxs-lookup"><span data-stu-id="eba9d-151">**Process database**</span></span>|<span data-ttu-id="eba9d-152">Участники могут выполнять операции обработки и массовой обработки,</span><span class="sxs-lookup"><span data-stu-id="eba9d-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="eba9d-153">Не могут изменять схему модели hello и просматривать данные.</span><span class="sxs-lookup"><span data-stu-id="eba9d-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="eba9d-154">**чтение**</span><span class="sxs-lookup"><span data-stu-id="eba9d-154">**Read**</span></span>|<span data-ttu-id="eba9d-155">Члены могут запрашивать данные (с учетом фильтров строк), но не могут изменять схему модели hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="eba9d-156">Щелкните **Членство**, а затем введите пользователя или группу в клиенте Azure AD, указав адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="eba9d-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Добавить пользователя](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="eba9d-158">Если hello роль, которую вы создаете имеет разрешение на чтение, можно добавить фильтры строк с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="eba9d-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="eba9d-159">Нажмите кнопку **фильтры строк**, выберите таблицу, а затем введите формулу DAX в hello **фильтр DAX** поля.</span><span class="sxs-lookup"><span data-stu-id="eba9d-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="eba9d-160">tooadd ролей и пользователей, используя сценарий TMSL</span><span class="sxs-lookup"><span data-stu-id="eba9d-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="eba9d-161">Можно выполнить сценарий TMSL в окно XMLA hello в SSMS или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eba9d-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="eba9d-162">Используйте hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) команда и hello [ролей](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) объекта.</span><span class="sxs-lookup"><span data-stu-id="eba9d-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="eba9d-163">**Пример скрипта TMSL**</span><span class="sxs-lookup"><span data-stu-id="eba9d-163">**Sample TMSL script**</span></span>

<span data-ttu-id="eba9d-164">В этом образце внешнего пользователя B2B и группы добавляются toohello аналитик роли с разрешениями на чтение для базы данных SalesBI hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="eba9d-165">Оба hello внешний пользователь и группа должна находиться в одном клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eba9d-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="eba9d-166">tooadd ролей и пользователей с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="eba9d-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="eba9d-167">Hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) модуль предоставляет базы данных для определенных задач управления командлеты и hello общего назначения командлета Invoke-ASCmd, принимающий запроса табличной языка скриптов модели (TMSL) или сценария.</span><span class="sxs-lookup"><span data-stu-id="eba9d-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="eba9d-168">Hello следующие командлеты используются для управления ролями базы данных и пользователей.</span><span class="sxs-lookup"><span data-stu-id="eba9d-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="eba9d-169">Командлет</span><span class="sxs-lookup"><span data-stu-id="eba9d-169">Cmdlet</span></span>|<span data-ttu-id="eba9d-170">Описание</span><span class="sxs-lookup"><span data-stu-id="eba9d-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="eba9d-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="eba9d-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="eba9d-172">Добавьте роль члена tooa базы данных.</span><span class="sxs-lookup"><span data-stu-id="eba9d-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="eba9d-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="eba9d-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="eba9d-174">Удаление участника из роли базы данных.</span><span class="sxs-lookup"><span data-stu-id="eba9d-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="eba9d-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="eba9d-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="eba9d-176">Выполнение сценария TMSL.</span><span class="sxs-lookup"><span data-stu-id="eba9d-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="eba9d-177">Фильтры строк</span><span class="sxs-lookup"><span data-stu-id="eba9d-177">Row filters</span></span>  
<span data-ttu-id="eba9d-178">Фильтры строк определяют, какие строки в таблице могут запросить участники определенной роли.</span><span class="sxs-lookup"><span data-stu-id="eba9d-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="eba9d-179">Фильтры строк определяются для каждой таблицы в модели с помощью формул DAX.</span><span class="sxs-lookup"><span data-stu-id="eba9d-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="eba9d-180">Они могут быть определены только для ролей с разрешениями "Чтение" и "Чтение и обработка".</span><span class="sxs-lookup"><span data-stu-id="eba9d-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="eba9d-181">По умолчанию Если фильтр строк не задан для конкретной таблицы, члены могут просматривать все строки в таблице hello Если перекрестная фильтрация применяется из другой таблицы.</span><span class="sxs-lookup"><span data-stu-id="eba9d-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="eba9d-182">Фильтры строк требуется формулу DAX, которое должно вычисляться tooa значение TRUE или FALSE, toodefine hello строк, которые могут запрашиваться членами этой роли.</span><span class="sxs-lookup"><span data-stu-id="eba9d-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="eba9d-183">Не удается запросить строки, не включенные в формулу DAX hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="eba9d-184">Например, hello таблицы Customers с hello, следующее выражение фильтры строк, *= клиентов [Страна] = «США»*, члены роли Sales hello распознает только клиентов из США hello.</span><span class="sxs-lookup"><span data-stu-id="eba9d-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="eba9d-185">Фильтры строк применяются toohello указан строк и строк.</span><span class="sxs-lookup"><span data-stu-id="eba9d-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="eba9d-186">Если таблица содержит несколько связей, фильтры применяют защиту hello связи, которая является активной.</span><span class="sxs-lookup"><span data-stu-id="eba9d-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="eba9d-187">Фильтры строк пересекаются с другими фильтрами строк, определенными для связанных таблиц, например:</span><span class="sxs-lookup"><span data-stu-id="eba9d-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="eba9d-188">Таблица</span><span class="sxs-lookup"><span data-stu-id="eba9d-188">Table</span></span>|<span data-ttu-id="eba9d-189">Выражение DAX</span><span class="sxs-lookup"><span data-stu-id="eba9d-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="eba9d-190">Регион</span><span class="sxs-lookup"><span data-stu-id="eba9d-190">Region</span></span>|<span data-ttu-id="eba9d-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="eba9d-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="eba9d-192">Категория продукта</span><span class="sxs-lookup"><span data-stu-id="eba9d-192">ProductCategory</span></span>|<span data-ttu-id="eba9d-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="eba9d-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="eba9d-194">Транзакции</span><span class="sxs-lookup"><span data-stu-id="eba9d-194">Transactions</span></span>|<span data-ttu-id="eba9d-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="eba9d-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="eba9d-196">Hello итоге получается, что члены можно запросить строк данных, где hello клиенты находятся в США hello, hello Категория продуктов — велосипеды, а год hello — 2016.</span><span class="sxs-lookup"><span data-stu-id="eba9d-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="eba9d-197">Пользователи не могут запрашивать транзакции за пределами США hello транзакции, которые не велосипедов и транзакции не 2016 если они не являются членами другой роли, которая предоставляет такие разрешения.</span><span class="sxs-lookup"><span data-stu-id="eba9d-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="eba9d-198">Можно использовать фильтр hello *=FALSE()*, toodeny доступ tooall строк для всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="eba9d-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba9d-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eba9d-199">Next steps</span></span>
  <span data-ttu-id="eba9d-200">[Управление администраторами сервера](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="eba9d-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="eba9d-201">Управление службами Azure Analysis Services с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="eba9d-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="eba9d-202">Справочник по языку TMSL</span><span class="sxs-lookup"><span data-stu-id="eba9d-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

