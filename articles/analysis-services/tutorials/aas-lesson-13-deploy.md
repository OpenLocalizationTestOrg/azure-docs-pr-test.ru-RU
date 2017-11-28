---
<span data-ttu-id="b7bb7-101">Заголовок: aaa «занятие учебника Azure Analysis Services 13: развертывание | Документы Microsoft» Описание: описание как учебника hello toodeploy проекта служб Analysis Services tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="b7bb7-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="b7bb7-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b7bb7-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: ms.author 07-17/2017 г.: owend</span><span class="sxs-lookup"><span data-stu-id="b7bb7-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="b7bb7-104">Занятие 13. Развертывание</span><span class="sxs-lookup"><span data-stu-id="b7bb7-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b7bb7-105">На этом занятии вы настройку свойств развертывания; Указание tooand toodeploy сервера Azure Analysis Services имя модели hello.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="b7bb7-106">Затем можно развернуть экземпляр toothat hello модели.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="b7bb7-107">После развертывания модели, пользователи могут подключаться tooit с помощью клиентского приложения создания отчетов.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="b7bb7-108">toolearn более, в разделе [развертывания служб Analysis Services tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="b7bb7-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="b7bb7-109">Предполагаемое время toocomplete на этом занятии: **5 минут**</span><span class="sxs-lookup"><span data-stu-id="b7bb7-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b7bb7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b7bb7-110">Prerequisites</span></span>  
<span data-ttu-id="b7bb7-111">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b7bb7-112">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 12: анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="b7bb7-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="b7bb7-113">Необходимо иметь [разрешения администратора](../analysis-services-server-admins.md) on hello удаленных служб Analysis Services server toodeploy по порядку tooit.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="b7bb7-114">Если вы установили hello AdventureWorksDW2014 образца базы данных на локальном сервере SQL, и вы развертываете tooan служб Azure Analysis server модели, [локального шлюза данных](../analysis-services-gateway.md) является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="b7bb7-115">Развертывание модели hello</span><span class="sxs-lookup"><span data-stu-id="b7bb7-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="b7bb7-116">Свойства развертывания tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b7bb7-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="b7bb7-117">В **обозревателе решений**, щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта, а затем нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="b7bb7-118">В hello **страницы свойств Интернет-продаж AW** диалогового **сервер развертывания**, в hello **сервера** свойство, введите полный адрес сервера hello.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="b7bb7-120">В hello **базы данных** введите **Интернет-продаж Adventure Works**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="b7bb7-121">В hello **Имя_модели** введите **модель Интернет-продаж Adventure Works**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="b7bb7-122">Проверьте выбранные параметры и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="b7bb7-123">hello toodeploy Интернет-продаж Adventure Works</span><span class="sxs-lookup"><span data-stu-id="b7bb7-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="b7bb7-124">В **обозревателе решений**, щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта > **сборки**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="b7bb7-125">Щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта > **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="b7bb7-126">При развертывании служб Analysis Services tooAzure, может быть запрос tooenter вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="b7bb7-127">Укажите свою учетную запись в организации и пароль, например nancy@adventureworks.com. Это учетная запись должна быть в "Администраторы" на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="b7bb7-128">Развернуть Hello-диалоговое окно появляется и отображает состояние развертывания метаданных hello hello и каждая таблица, включенная в модель hello.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="b7bb7-130">После успешного завершения развертывания нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="b7bb7-131">Заключение</span><span class="sxs-lookup"><span data-stu-id="b7bb7-131">Conclusion</span></span>  
<span data-ttu-id="b7bb7-132">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b7bb7-132">Congratulations!</span></span> <span data-ttu-id="b7bb7-133">Вы создали и развернули свою первую табличную модель служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="b7bb7-134">Этот учебник помог вам выполнения типичных задач hello при создании табличной модели.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="b7bb7-135">Теперь, когда модель Интернет-продаж Adventure Works развернута, можно использовать SQL Server Management Studio toomanage hello модели; Создание скриптов обработки и плана резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="b7bb7-136">Теперь также позволяет пользователям подключаться toohello модели, с помощью клиентского приложения создания отчетов, таких как Microsoft Excel или Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7bb7-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="b7bb7-138">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="b7bb7-138">What's next?</span></span>
<span data-ttu-id="b7bb7-139">[Подключение с помощью Power BI](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="b7bb7-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="b7bb7-140">[Дополнительное занятие. Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="b7bb7-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="b7bb7-141">[Дополнительное занятие. Строки детализации](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="b7bb7-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="b7bb7-142">Дополнительное занятие. Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="b7bb7-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
