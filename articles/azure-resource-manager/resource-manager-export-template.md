---
title: "шаблон диспетчера ресурсов Azure aaaExport | Документы Microsoft"
description: "Используйте Управление ресурсов Azure tooexport шаблон в существующую группу ресурсов."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="09f7b-103">Экспорт шаблона Azure Resource Manager из существующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="09f7b-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="09f7b-104">В этой статье вы узнаете, как tooexport шаблона диспетчера ресурсов от существующих ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="09f7b-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="09f7b-105">Можно использовать, созданного шаблона toogain лучше понять синтаксис шаблона.</span><span class="sxs-lookup"><span data-stu-id="09f7b-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="09f7b-106">Существует два способа tooexport шаблона:</span><span class="sxs-lookup"><span data-stu-id="09f7b-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="09f7b-107">Вы можете экспортировать hello **фактическое шаблон, используемый для развертывания**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="09f7b-108">экспортированный шаблон Hello включает все параметры hello и переменные, точно так, как они выглядели в исходном шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="09f7b-109">Этот подход полезен при развертывании ресурсы с помощью портала hello и требуется toosee hello шаблона toocreate эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="09f7b-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="09f7b-110">Этот шаблон удобно использовать.</span><span class="sxs-lookup"><span data-stu-id="09f7b-110">This template is readily usable.</span></span> 
* <span data-ttu-id="09f7b-111">Вы можете экспортировать **созданный шаблон, который представляет текущее состояние группы ресурсов hello hello**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="09f7b-112">экспортированный шаблон Hello не основывается на любой шаблон, который использовался для развертывания.</span><span class="sxs-lookup"><span data-stu-id="09f7b-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="09f7b-113">Вместо этого он создает шаблон, который является моментальным снимком, группа ресурсов «hello».</span><span class="sxs-lookup"><span data-stu-id="09f7b-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="09f7b-114">экспортированный шаблон Hello имеет много жестко запрограммированных значений и, возможно, не все параметры, как обычно при определении.</span><span class="sxs-lookup"><span data-stu-id="09f7b-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="09f7b-115">Этот подход полезен, если вы изменили после развертывания группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="09f7b-116">Перед использованием в этот шаблон обычно требуется внести изменения.</span><span class="sxs-lookup"><span data-stu-id="09f7b-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="09f7b-117">В этом разделе показаны оба подхода через портал hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="09f7b-118">Развертывание ресурсов</span><span class="sxs-lookup"><span data-stu-id="09f7b-118">Deploy resources</span></span>
<span data-ttu-id="09f7b-119">Давайте начнем, развернув tooAzure ресурсов, который можно использовать для экспорта в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="09f7b-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="09f7b-120">Если уже есть группа ресурсов в подписке, что требуется шаблон tooa tooexport, этот раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="09f7b-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="09f7b-121">Hello оставшейся части этой статьи предполагается, что вы развернули hello веб-приложения и решения базы данных SQL, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="09f7b-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="09f7b-122">При использовании другого решения работы может немного отличаться, но являются tooexport шаблон действия hello hello таким же.</span><span class="sxs-lookup"><span data-stu-id="09f7b-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="09f7b-123">В hello [портал Azure](https://portal.azure.com)выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![Выбор нового](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="09f7b-125">Поиск **веб-приложение + SQL** и выберите его из доступных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![Поиск элемента "Веб-приложение и SQL"](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="09f7b-127">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-127">Select **Create**.</span></span>

      ![Выбор создания](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="09f7b-129">Укажите hello необходимые значения для hello веб-приложения и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="09f7b-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="09f7b-130">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-130">Select **Create**.</span></span>

      ![Указание значений SQL и веб-приложения](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="09f7b-132">Hello развертывания может занять около минуты.</span><span class="sxs-lookup"><span data-stu-id="09f7b-132">hello deployment may take a minute.</span></span> <span data-ttu-id="09f7b-133">После завершения развертывания hello подписки содержит решение hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="09f7b-134">Просмотр шаблона из журнала развертываний</span><span class="sxs-lookup"><span data-stu-id="09f7b-134">View template from deployment history</span></span>
1. <span data-ttu-id="09f7b-135">Go toohello колонки группы ресурсов для новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09f7b-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="09f7b-136">Обратите внимание, что этой колонке hello отображается результат последнего развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="09f7b-137">Щелкните эту ссылку.</span><span class="sxs-lookup"><span data-stu-id="09f7b-137">Select this link.</span></span>
   
      ![колонка группы ресурсов](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="09f7b-139">Можно просмотреть журнал развертывания для группы hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="09f7b-140">В вашем случае hello колонки, скорее всего, перечислены только одно развертывание.</span><span class="sxs-lookup"><span data-stu-id="09f7b-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="09f7b-141">Выберите его.</span><span class="sxs-lookup"><span data-stu-id="09f7b-141">Select this deployment.</span></span>
   
     ![последнее развертывание](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="09f7b-143">Hello колонке Сводка hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="09f7b-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="09f7b-144">Сводка Hello включает hello состояние развертывания hello, операций и значения hello, предоставленный для параметров.</span><span class="sxs-lookup"><span data-stu-id="09f7b-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="09f7b-145">toosee hello шаблона, который использовался для развертывания hello, выберите **Просмотр шаблона**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![просмотр сводки по развертыванию](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="09f7b-147">Диспетчер ресурсов получает hello следующие семь файлы автоматически:</span><span class="sxs-lookup"><span data-stu-id="09f7b-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="09f7b-148">**Шаблон** -hello шаблон, определяющий hello инфраструктуры для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="09f7b-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="09f7b-149">При создании учетной записи хранилища hello через портал hello, диспетчер ресурсов использовать toodeploy шаблона его и сохранить для дальнейшего использования этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="09f7b-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="09f7b-150">**Параметры** -файл параметров, можно использовать toopass значений, во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="09f7b-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="09f7b-151">Он содержит hello значения, указанные во время первого развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="09f7b-152">Эти значения можно изменить при повторном развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="09f7b-153">**CLI** -можно использовать шаблон hello toodeploy сценария файл Azure интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="09f7b-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="09f7b-154">**CLI 2.0** -можно использовать шаблон hello toodeploy сценария файл Azure интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="09f7b-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="09f7b-155">**PowerShell** -файл сценария Azure PowerShell можно использовать шаблон toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="09f7b-156">**.NET** -класс .NET, можно использовать шаблон toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="09f7b-157">**Ruby** -класс Ruby, можно использовать шаблон toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="09f7b-158">Hello файлы могут быть доступны по ссылкам по колонке hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="09f7b-159">По умолчанию hello колонке отображает шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-159">By default, hello blade displays hello template.</span></span>
      
       ![Просмотреть шаблон](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="09f7b-161">Этот шаблон представляет собой фактическое шаблона hello используемых toocreate, веб-приложения и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="09f7b-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="09f7b-162">Обратите внимание, что он содержит параметры, позволяющие tooprovide различные значения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="09f7b-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="09f7b-163">toolearn Дополнительные сведения о структуре hello шаблона, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="09f7b-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="09f7b-164">Экспорт шаблона hello из группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="09f7b-164">Export hello template from resource group</span></span>
<span data-ttu-id="09f7b-165">Если вы вручную изменить ресурсы или добавить ресурсы в несколько развертываний, получение шаблона из журнала развертывания hello не отражает текущее состояние группы ресурсов hello hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="09f7b-166">В этом разделе показано, как шаблон, который отражает tooexport hello текущее состояние группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="09f7b-167">Нельзя экспортировать шаблон для группы ресурсов, которая содержит более 200 ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09f7b-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="09f7b-168">шаблон hello tooview для группы ресурсов, выберите **сценарий автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![экспорт группы ресурсов](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="09f7b-170">Диспетчер ресурсов для оценки hello ресурсов в группе ресурсов hello и создает шаблон для этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09f7b-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="09f7b-171">Не все типы ресурсов поддерживают hello экспорта шаблона функции.</span><span class="sxs-lookup"><span data-stu-id="09f7b-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="09f7b-172">Может появиться сообщение о том, имеется проблема с экспортом hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="09f7b-173">Вы узнаете, как toohandle те проблемы в hello [исправление проблемы при экспорте](#fix-export-issues) раздела.</span><span class="sxs-lookup"><span data-stu-id="09f7b-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="09f7b-174">Снова появиться hello шесть файлов, которые можно использовать решение tooredeploy hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="09f7b-175">Тем не менее этот шаблон hello времени будет немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="09f7b-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="09f7b-176">Обратите внимание, что hello созданного шаблона содержит меньшее число параметров, чем шаблон hello в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="09f7b-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="09f7b-177">Кроме того многие hello значения (например, расположение и значения номера SKU) жестко запрограммированы в этот шаблон, а не принимает значение параметра.</span><span class="sxs-lookup"><span data-stu-id="09f7b-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="09f7b-178">Перед повторным использованием этого шаблона, может потребоваться tooedit шаблона hello toomake лучше использовать параметры.</span><span class="sxs-lookup"><span data-stu-id="09f7b-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="09f7b-179">У вас есть два способа для продолжения toowork с помощью этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="09f7b-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="09f7b-180">Можно загрузить шаблон hello и работать с ним локально с помощью редактора JSON.</span><span class="sxs-lookup"><span data-stu-id="09f7b-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="09f7b-181">Также можно сохранить библиотека tooyour шаблонов hello и работать с ним через портал hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="09f7b-182">Если вы знакомы с помощью редактора JSON, например [VS Code](https://code.visualstudio.com/) или [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), может потребоваться, загрузив шаблон hello локально и с помощью этого редактора.</span><span class="sxs-lookup"><span data-stu-id="09f7b-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="09f7b-183">toowork локально, выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-183">toowork locally, select **Download**.</span></span>
   
      ![скачивание шаблона](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="09f7b-185">Если вы не настроены с помощью редактора JSON, может потребоваться редактирования шаблона hello через портал hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="09f7b-186">Hello оставшейся части этой статьи предполагается, что вы сохранили библиотека tooyour шаблонов hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="09f7b-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="09f7b-187">Однако сделать hello же изменения синтаксиса шаблона toohello ли локально работа с редактором JSON или через портал hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="09f7b-188">Выберите toowork через портал hello **добавить toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![добавить toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="09f7b-190">При добавлении библиотеки шаблонов toohello, дайте шаблону hello, имя и описание.</span><span class="sxs-lookup"><span data-stu-id="09f7b-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="09f7b-191">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-191">Then, select **Save**.</span></span>
   
     ![задание значений шаблона](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="09f7b-193">Выберите шаблон, сохраненный в библиотеке, tooview **дополнительные службы**, тип **шаблоны** toofilter результатов установите **шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![поиск шаблонов](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="09f7b-195">Выберите шаблон hello с именем hello сохранения.</span><span class="sxs-lookup"><span data-stu-id="09f7b-195">Select hello template with hello name you saved.</span></span>
   
      ![выбор шаблона](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="09f7b-197">Настройка шаблона hello</span><span class="sxs-lookup"><span data-stu-id="09f7b-197">Customize hello template</span></span>
<span data-ttu-id="09f7b-198">работает Hello экспортированный шаблон нормально, если требуется toocreate hello же и веб-приложения базы данных SQL для всех развертываний.</span><span class="sxs-lookup"><span data-stu-id="09f7b-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="09f7b-199">Но Resource Manager обеспечивает более гибкое развертывание.</span><span class="sxs-lookup"><span data-stu-id="09f7b-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="09f7b-200">В этой статье показано, как параметры tooadd для hello базы данных, имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="09f7b-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="09f7b-201">Можно использовать этот же подход tooadd большую гибкость для других значений в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="09f7b-202">toocustomize hello шаблона, выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![отображение шаблона](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="09f7b-204">Выберите шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-204">Select hello template.</span></span>
   
     ![изменение шаблона](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="09f7b-206">значения hello может toopass toobe, toospecify может возникнуть во время развертывания, добавьте следующие два параметра toohello hello **параметры** раздела hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="09f7b-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="09f7b-207">новые параметры toouse hello, замените определение сервера SQL hello hello **ресурсов** раздела.</span><span class="sxs-lookup"><span data-stu-id="09f7b-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="09f7b-208">Обратите внимание, что **administratorLogin** и **administratorLoginPassword** теперь используют значения параметров.</span><span class="sxs-lookup"><span data-stu-id="09f7b-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="09f7b-209">Выберите **ОК** после редактирования шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="09f7b-210">Выберите **Сохранить** toosave hello изменения toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="09f7b-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![сохранение шаблона](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="09f7b-212">tooredeploy hello обновить шаблон, выберите **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="09f7b-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![развертывание шаблона](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="09f7b-214">Укажите значения параметров и выберите ресурсов группы toodeploy hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09f7b-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="09f7b-215">Устранение проблем при экспорте</span><span class="sxs-lookup"><span data-stu-id="09f7b-215">Fix export issues</span></span>
<span data-ttu-id="09f7b-216">Не все типы ресурсов поддерживают hello экспорта шаблона функции.</span><span class="sxs-lookup"><span data-stu-id="09f7b-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="09f7b-217">tooresolve эту проблему, вручную добавить отсутствующие ресурсы hello обратно в шаблон.</span><span class="sxs-lookup"><span data-stu-id="09f7b-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="09f7b-218">сообщение об ошибке Hello включает hello типы ресурсов, которые невозможно экспортировать.</span><span class="sxs-lookup"><span data-stu-id="09f7b-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="09f7b-219">Найдите этот тип ресурса в [справочнике по шаблонам](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="09f7b-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="09f7b-220">Например, toomanually Добавление шлюза виртуальной сети см. в разделе [ссылка на шаблон Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="09f7b-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="09f7b-221">Проблемы при экспорте могут возникать, только если шаблон экспортируется из группы ресурсов, а не из журнала развертываний.</span><span class="sxs-lookup"><span data-stu-id="09f7b-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="09f7b-222">При развертывании последнего точно представляет текущее состояние группы ресурсов hello hello, следует экспортировать шаблон hello из журнала развертывания hello, а не из группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="09f7b-223">Экспортируйте только из группы ресурсов после внесения изменений toohello ресурсов группы, не определенные в одном шаблоне.</span><span class="sxs-lookup"><span data-stu-id="09f7b-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="09f7b-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09f7b-224">Next steps</span></span>
<span data-ttu-id="09f7b-225">Вы узнали, каким образом tooexport шаблон на основе ресурсов, которые вы создали на портале hello.</span><span class="sxs-lookup"><span data-stu-id="09f7b-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="09f7b-226">Вы можете развернуть шаблон с помощью [PowerShell](resource-group-template-deploy.md), [интерфейса командной строки Azure](resource-group-template-deploy-cli.md) или [REST API](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="09f7b-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="09f7b-227">tooexport шаблона с помощью PowerShell. в статье toosee [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="09f7b-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="09f7b-228">tooexport шаблона с помощью Azure CLI см. в статье toosee [используйте hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="09f7b-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

