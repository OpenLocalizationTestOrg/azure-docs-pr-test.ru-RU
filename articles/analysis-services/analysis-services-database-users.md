---
title: "Управление ролями и пользователями базы данных в службах Azure Analysis Services | Документация Майкрософт"
description: "Узнайте, как управлять ролями и пользователями базы данных на сервере служб Analysis Services в Azure."
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
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="f043f-103">Управление ролями и пользователями базы данных</span><span class="sxs-lookup"><span data-stu-id="f043f-103">Manage database roles and users</span></span>

<span data-ttu-id="f043f-104">На уровне шаблона базы данных всем пользователям должна быть назначена роль.</span><span class="sxs-lookup"><span data-stu-id="f043f-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="f043f-105">Роли определяют пользователей с определенными разрешениями для шаблона базы данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="f043f-106">Любой пользователь или группа безопасности, добавленные в роль, должны иметь учетную запись в клиенте Azure AD в одной подписке с сервером.</span><span class="sxs-lookup"><span data-stu-id="f043f-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="f043f-107">Способ определения ролей отличается в зависимости от используемого средства, но на результат это не влияет.</span><span class="sxs-lookup"><span data-stu-id="f043f-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="f043f-108">Разрешения ролей включают следующие:</span><span class="sxs-lookup"><span data-stu-id="f043f-108">Role permissions include:</span></span>
*  <span data-ttu-id="f043f-109">**Администратор**. Пользователи имеют полный набор прав в отношении базы данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="f043f-110">Роли базы данных с разрешениями администратора и администраторы сервера — это не одно и тоже.</span><span class="sxs-lookup"><span data-stu-id="f043f-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="f043f-111">**Процесс**. Пользователи могут подключаться к базе данных и выполнять операции обработки, а также анализировать данные шаблона базы данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="f043f-112">**Чтение**. Пользователи могут использовать клиентское приложение, чтобы подключиться к шаблону базы данных и анализировать его данные.</span><span class="sxs-lookup"><span data-stu-id="f043f-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="f043f-113">При создании проекта табличной модели вы можете создать роли и добавить пользователей или группы в эти роли с помощью диспетчера ролей в SSDT.</span><span class="sxs-lookup"><span data-stu-id="f043f-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="f043f-114">При развертывании на сервере вы можете использовать SSMS, [командлеты PowerShell для служб Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx) или [язык сценариев табличной модели](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL), чтобы добавить или удалить роли и участников пользователей.</span><span class="sxs-lookup"><span data-stu-id="f043f-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="f043f-115">Чтобы добавить роли и пользователей в SSDT или управлять ими, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f043f-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="f043f-116">Выберите в SSDT **Обозреватель табличных моделей**, а затем щелкните правой кнопкой мыши **Роли**.</span><span class="sxs-lookup"><span data-stu-id="f043f-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="f043f-117">В **диспетчере ролей** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f043f-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="f043f-118">Введите имя для роли.</span><span class="sxs-lookup"><span data-stu-id="f043f-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="f043f-119">По умолчанию имя стандартной роли последовательно нумеруется для каждой новой роли.</span><span class="sxs-lookup"><span data-stu-id="f043f-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="f043f-120">Мы рекомендуем ввести имя, которое четко определяет тип участника, например "Финансовые менеджеры" или "Специалисты по кадровым вопросам".</span><span class="sxs-lookup"><span data-stu-id="f043f-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="f043f-121">Выберите одно из следующих разрешений:</span><span class="sxs-lookup"><span data-stu-id="f043f-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="f043f-122">Разрешение</span><span class="sxs-lookup"><span data-stu-id="f043f-122">Permission</span></span>|<span data-ttu-id="f043f-123">Описание</span><span class="sxs-lookup"><span data-stu-id="f043f-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="f043f-124">**None**</span><span class="sxs-lookup"><span data-stu-id="f043f-124">**None**</span></span>|<span data-ttu-id="f043f-125">Участники не могут изменять схему шаблона и запрашивать данные.</span><span class="sxs-lookup"><span data-stu-id="f043f-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f043f-126">**чтение**</span><span class="sxs-lookup"><span data-stu-id="f043f-126">**Read**</span></span>|<span data-ttu-id="f043f-127">Участники могут запрашивать данные (на основе фильтров строк), но не могут изменять схему шаблона.</span><span class="sxs-lookup"><span data-stu-id="f043f-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="f043f-128">**Чтение и обработка**</span><span class="sxs-lookup"><span data-stu-id="f043f-128">**Read and Process**</span></span>|<span data-ttu-id="f043f-129">Участники могут запрашивать данные (на основе фильтров на уровне строк), а также выполнять операции обработки и массовой обработки, но не могут изменять схему шаблона.</span><span class="sxs-lookup"><span data-stu-id="f043f-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="f043f-130">**Описание процесса**</span><span class="sxs-lookup"><span data-stu-id="f043f-130">**Process**</span></span>|<span data-ttu-id="f043f-131">Участники могут выполнять операции обработки и массовой обработки,</span><span class="sxs-lookup"><span data-stu-id="f043f-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f043f-132">но не могут изменять схему шаблона и запрашивать данные.</span><span class="sxs-lookup"><span data-stu-id="f043f-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f043f-133">**Администратор**</span><span class="sxs-lookup"><span data-stu-id="f043f-133">**Administrator**</span></span>|<span data-ttu-id="f043f-134">Участники могут изменять схему шаблона и выполнять запрос всех данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="f043f-135">Если у роли, которую вы создаете, есть разрешения "Чтение" или "Чтение и обработка", вы можете добавить фильтры строк с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="f043f-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f043f-136">Щелкните вкладку **Фильтры строк**, выберите таблицу, а затем щелкните поле **Фильтр DAX** и введите формулу DAX.</span><span class="sxs-lookup"><span data-stu-id="f043f-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="f043f-137">Щелкните **Участники** > **Добавить внешнего участника**.</span><span class="sxs-lookup"><span data-stu-id="f043f-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="f043f-138">В разделе **Добавить внешнего участника** введите пользователей или группы в клиенте Azure AD, указав адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f043f-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="f043f-139">После того как вы нажмете кнопку "ОК" и закроете диспетчер ролей, роли и участники ролей появятся в обозревателе табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="f043f-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Роли и пользователи в обозревателе табличных моделей](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="f043f-141">Выполните развертывание на сервере Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f043f-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="f043f-142">Добавление ролей и пользователей в SSDT и управление ими</span><span class="sxs-lookup"><span data-stu-id="f043f-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="f043f-143">Чтобы добавить роли и пользователей в развернутый шаблон базы данных, вы должны быть подключены к серверу от имени администратора сервера или роли базы данных с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="f043f-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="f043f-144">В обозревателе объекта щелкните правой кнопкой мыши **Роли** > **Новая роль**.</span><span class="sxs-lookup"><span data-stu-id="f043f-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="f043f-145">В области **Создание роли** введите имя и описание роли.</span><span class="sxs-lookup"><span data-stu-id="f043f-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="f043f-146">Выберите разрешение.</span><span class="sxs-lookup"><span data-stu-id="f043f-146">Select a permission.</span></span>
   |<span data-ttu-id="f043f-147">Разрешение</span><span class="sxs-lookup"><span data-stu-id="f043f-147">Permission</span></span>|<span data-ttu-id="f043f-148">Описание</span><span class="sxs-lookup"><span data-stu-id="f043f-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="f043f-149">**Полный доступ (администратор)**</span><span class="sxs-lookup"><span data-stu-id="f043f-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="f043f-150">Участники могут изменять схему шаблона, обрабатывать и запрашивать все данные.</span><span class="sxs-lookup"><span data-stu-id="f043f-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="f043f-151">**Обработка базы данных**</span><span class="sxs-lookup"><span data-stu-id="f043f-151">**Process database**</span></span>|<span data-ttu-id="f043f-152">Участники могут выполнять операции обработки и массовой обработки,</span><span class="sxs-lookup"><span data-stu-id="f043f-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f043f-153">но не могут изменять схему шаблона и запрашивать данные.</span><span class="sxs-lookup"><span data-stu-id="f043f-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="f043f-154">**чтение**</span><span class="sxs-lookup"><span data-stu-id="f043f-154">**Read**</span></span>|<span data-ttu-id="f043f-155">Участники могут запрашивать данные (на основе фильтров строк), но не могут изменять схему шаблона.</span><span class="sxs-lookup"><span data-stu-id="f043f-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="f043f-156">Щелкните **Членство**, а затем введите пользователя или группу в клиенте Azure AD, указав адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f043f-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Добавить пользователя](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="f043f-158">Если у роли, которую вы создаете, есть разрешение "Чтение", вы можете добавить фильтры строк с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="f043f-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f043f-159">Щелкните **Фильтры строк**, выберите таблицу, а затем введите формулу DAX в поле **Фильтр DAX**.</span><span class="sxs-lookup"><span data-stu-id="f043f-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="f043f-160">Добавление ролей и пользователей с помощью сценария TMSL</span><span class="sxs-lookup"><span data-stu-id="f043f-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="f043f-161">Вы можете выполнить сценарий TMSL в окне XMLA в SSMS или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f043f-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="f043f-162">Используйте команду [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) и объект [Роли](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl).</span><span class="sxs-lookup"><span data-stu-id="f043f-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="f043f-163">**Пример скрипта TMSL**</span><span class="sxs-lookup"><span data-stu-id="f043f-163">**Sample TMSL script**</span></span>

<span data-ttu-id="f043f-164">В этом примере внешний пользователь B2B и группа добавляются в роль "Аналитик" с разрешениями на чтение для базы данных SalesBI.</span><span class="sxs-lookup"><span data-stu-id="f043f-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="f043f-165">Внешний пользователь и группа должны находиться в одном клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f043f-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
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

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="f043f-166">Добавление ролей и пользователей с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f043f-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="f043f-167">Модуль [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) предоставляет командлеты для конкретных задач управления базой данных, а также командлет общего назначения Invoke-ASCmd, который принимает запрос TMSL или сценарий.</span><span class="sxs-lookup"><span data-stu-id="f043f-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="f043f-168">Следующие командлеты используются для управления ролями базы данных и пользователями.</span><span class="sxs-lookup"><span data-stu-id="f043f-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="f043f-169">Командлет</span><span class="sxs-lookup"><span data-stu-id="f043f-169">Cmdlet</span></span>|<span data-ttu-id="f043f-170">Описание</span><span class="sxs-lookup"><span data-stu-id="f043f-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="f043f-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f043f-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="f043f-172">Добавление участника в роль базы данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="f043f-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f043f-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="f043f-174">Удаление участника из роли базы данных.</span><span class="sxs-lookup"><span data-stu-id="f043f-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="f043f-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="f043f-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="f043f-176">Выполнение сценария TMSL.</span><span class="sxs-lookup"><span data-stu-id="f043f-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="f043f-177">Фильтры строк</span><span class="sxs-lookup"><span data-stu-id="f043f-177">Row filters</span></span>  
<span data-ttu-id="f043f-178">Фильтры строк определяют, какие строки в таблице могут запросить участники определенной роли.</span><span class="sxs-lookup"><span data-stu-id="f043f-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="f043f-179">Фильтры строк определяются для каждой таблицы в модели с помощью формул DAX.</span><span class="sxs-lookup"><span data-stu-id="f043f-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="f043f-180">Они могут быть определены только для ролей с разрешениями "Чтение" и "Чтение и обработка".</span><span class="sxs-lookup"><span data-stu-id="f043f-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="f043f-181">По умолчанию если фильтр строк не определен для конкретной таблицы, участники могут запросить все строки в таблице при условии, что не применена перекрестная фильтрация из другой таблицы.</span><span class="sxs-lookup"><span data-stu-id="f043f-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="f043f-182">Фильтрам строк требуется формула DAX, которая должна возвращать значение TRUE или FALSE, чтобы определить строки, которые могут запросить участники этой определенной роли.</span><span class="sxs-lookup"><span data-stu-id="f043f-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="f043f-183">Строки, не включенные в формулу DAX, запросить нельзя.</span><span class="sxs-lookup"><span data-stu-id="f043f-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="f043f-184">Например, в таблице "Заказчики" с выражением фильтров строк *=Customers [Country] = “USA”* участники роли "Продажи" могут видеть только заказчиков из США.</span><span class="sxs-lookup"><span data-stu-id="f043f-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="f043f-185">Фильтры строк применяются к указанным строкам и связанным с ними строкам.</span><span class="sxs-lookup"><span data-stu-id="f043f-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="f043f-186">Если таблица содержит несколько связей, фильтры применяют защиту к активной связи.</span><span class="sxs-lookup"><span data-stu-id="f043f-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="f043f-187">Фильтры строк пересекаются с другими фильтрами строк, определенными для связанных таблиц, например:</span><span class="sxs-lookup"><span data-stu-id="f043f-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="f043f-188">Таблица</span><span class="sxs-lookup"><span data-stu-id="f043f-188">Table</span></span>|<span data-ttu-id="f043f-189">Выражение DAX</span><span class="sxs-lookup"><span data-stu-id="f043f-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="f043f-190">Регион</span><span class="sxs-lookup"><span data-stu-id="f043f-190">Region</span></span>|<span data-ttu-id="f043f-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="f043f-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="f043f-192">Категория продукта</span><span class="sxs-lookup"><span data-stu-id="f043f-192">ProductCategory</span></span>|<span data-ttu-id="f043f-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="f043f-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="f043f-194">Транзакции</span><span class="sxs-lookup"><span data-stu-id="f043f-194">Transactions</span></span>|<span data-ttu-id="f043f-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="f043f-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="f043f-196">В конечном результате участники могут запрашивать следующие строки данных: для региона — США, для категории продукта — велосипед, для года — 2016.</span><span class="sxs-lookup"><span data-stu-id="f043f-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="f043f-197">Пользователи не могут запрашивать транзакции за пределами США, транзакции, не связанные с велосипедами, а также транзакции, произошедшие не в 2016 году, пока они не станут участниками другой роли, предоставляющей эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="f043f-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="f043f-198">Вы можете использовать фильтр *=FALSE()*, чтобы запретить доступ ко всем строкам для всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="f043f-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f043f-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f043f-199">Next steps</span></span>
  <span data-ttu-id="f043f-200">[Управление администраторами сервера](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="f043f-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="f043f-201">Управление службами Azure Analysis Services с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f043f-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="f043f-202">Справочник по языку TMSL</span><span class="sxs-lookup"><span data-stu-id="f043f-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

