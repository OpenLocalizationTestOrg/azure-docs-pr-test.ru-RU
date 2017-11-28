---
<span data-ttu-id="8d25c-101">Заголовок: aaa «занятие учебника Azure Analysis Services 11: Создание ролей | Документы Microsoft» Описание: описание, как роли toocreate в hello проекта tutorial служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8d25c-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="8d25c-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="8d25c-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="8d25c-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="8d25c-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="8d25c-104">Занятие 11. Создание ролей</span><span class="sxs-lookup"><span data-stu-id="8d25c-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8d25c-105">На этом занятии мы создадим роли.</span><span class="sxs-lookup"><span data-stu-id="8d25c-105">In this lesson, you create roles.</span></span> <span data-ttu-id="8d25c-106">Роли обеспечивают безопасность данных и объектов базы данных модели, ограничивая доступ tooonly тех пользователей, которые являются членами роли.</span><span class="sxs-lookup"><span data-stu-id="8d25c-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="8d25c-107">Каждая роль определяется с помощью одного разрешения: "Нет", "Чтение", "Чтение и обработка", "Обработка" или "Администратор".</span><span class="sxs-lookup"><span data-stu-id="8d25c-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="8d25c-108">Роли можно определить во время создания модели с помощью диспетчера ролей.</span><span class="sxs-lookup"><span data-stu-id="8d25c-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="8d25c-109">После развертывания модели ролями можно управлять с помощью SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8d25c-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="8d25c-110">toolearn более, в разделе [ролей](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="8d25c-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="8d25c-111">Создание ролей является не обязательным toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="8d25c-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="8d25c-112">По умолчанию hello учетную запись, которую вы выполнили вход с правами администратора на hello модели.</span><span class="sxs-lookup"><span data-stu-id="8d25c-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="8d25c-113">Однако для других пользователей в вашей организации toobrowse с помощью отчетов клиента, необходимо создать хотя бы одну роль чтения разрешения и добавить этих пользователей в качестве членов.</span><span class="sxs-lookup"><span data-stu-id="8d25c-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="8d25c-114">Мы создадим три роли.</span><span class="sxs-lookup"><span data-stu-id="8d25c-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="8d25c-115">**Менеджер по продажам** — эта роль может включать пользователей вашей организации, для которого требуется toohave чтения разрешение tooall модели объектов и данных.</span><span class="sxs-lookup"><span data-stu-id="8d25c-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="8d25c-116">**Аналитик продаж в США** — эта роль может включать пользователей вашей организации, для которого требуется только данные могут toobrowse toobe связанные toosales в hello США.</span><span class="sxs-lookup"><span data-stu-id="8d25c-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="8d25c-117">Для этой роли, используйте toodefine формул DAX *фильтр строк*, ограничивающий элементы toobrowse только данные для hello США.</span><span class="sxs-lookup"><span data-stu-id="8d25c-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="8d25c-118">**Администратор** — эта роль может включать пользователей, для которых требуется разрешение администратора toohave, открывающее неограниченный доступ и разрешения tooperform административных задач в базе данных моделью hello.</span><span class="sxs-lookup"><span data-stu-id="8d25c-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="8d25c-119">Так как учетные записи пользователей и групп Windows в вашей организации являются уникальными, можно добавить учетные записи из toomembers вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8d25c-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="8d25c-120">Однако в этом учебнике вы можно не заполнять hello членов.</span><span class="sxs-lookup"><span data-stu-id="8d25c-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="8d25c-121">Проверить действие hello каждой из ролей позже в занятии 12: анализ в Excel.</span><span class="sxs-lookup"><span data-stu-id="8d25c-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="8d25c-122">Предполагаемое время toocomplete на этом занятии: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="8d25c-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8d25c-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d25c-123">Prerequisites</span></span>  
<span data-ttu-id="8d25c-124">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="8d25c-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="8d25c-125">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 10: Создание разделов](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="8d25c-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="8d25c-126">Создание ролей</span><span class="sxs-lookup"><span data-stu-id="8d25c-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="8d25c-127">toocreate роли пользователя менеджера по продажам</span><span class="sxs-lookup"><span data-stu-id="8d25c-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="8d25c-128">В обозревателе табличных моделей щелкните правой кнопкой мыши **Роли** > **Роли**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="8d25c-129">В диспетчере ролей нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="8d25c-130">Щелкните новую роль hello, а затем в hello **имя** столбца, переименовать роль hello слишком**менеджера по продажам**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="8d25c-131">В hello **разрешений** столбец, нажмите кнопку раскрывающегося списка hello, а затем выберите hello **чтения** разрешение.</span><span class="sxs-lookup"><span data-stu-id="8d25c-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="8d25c-133">Необязательно: Щелкните hello **элементы** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8d25c-134">В hello **Выбор пользователей или групп** диалогового окна введите hello пользователей или групп Windows из вашей организации требуется tooinclude в роли hello.</span><span class="sxs-lookup"><span data-stu-id="8d25c-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="8d25c-135">toocreate роли пользователя аналитика продаж в США</span><span class="sxs-lookup"><span data-stu-id="8d25c-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="8d25c-136">В диспетчере ролей нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="8d25c-137">Переименование роли hello слишком**аналитика продаж в США**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="8d25c-138">Предоставьте этой роли разрешение **Чтение**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="8d25c-139">На вкладке hello фильтры строк, а затем для hello **DimGeography** только в таблицу столбец фильтр DAX hello, тип hello следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="8d25c-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="8d25c-140">Формула фильтра строк должно разрешаться tooa значение Boolean (TRUE или FALSE).</span><span class="sxs-lookup"><span data-stu-id="8d25c-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="8d25c-141">С помощью этой формулы указывается, что только строки с hello код страны или региона значение равным «US», отображается toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="8d25c-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="8d25c-143">Необязательно: Щелкните hello **элементы** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8d25c-144">В hello **Выбор пользователей или групп** диалогового окна введите hello пользователей или групп Windows из вашей организации требуется tooinclude в роли hello.</span><span class="sxs-lookup"><span data-stu-id="8d25c-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="8d25c-145">toocreate ролью пользователя администратора</span><span class="sxs-lookup"><span data-stu-id="8d25c-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="8d25c-146">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="8d25c-147">Переименование роли hello слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="8d25c-148">Предоставьте этой роли разрешение **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="8d25c-149">Необязательно: Щелкните hello **элементы** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d25c-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8d25c-150">В hello **Выбор пользователей или групп** диалогового окна введите hello пользователей или групп Windows из вашей организации требуется tooinclude в роли hello.</span><span class="sxs-lookup"><span data-stu-id="8d25c-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="8d25c-151">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="8d25c-151">What's next?</span></span>
<span data-ttu-id="8d25c-152">[Занятие 12. Анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="8d25c-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
