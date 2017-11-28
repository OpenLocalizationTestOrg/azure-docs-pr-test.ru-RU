---
title: "учетные записи хранения Azure стека aaaManage | Документы Microsoft"
description: "Узнайте, как toofind, управление, восстановление и освободить учетных записей хранилища Azure стека"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="207a3-103">Управление учетными записями хранения в стек Azure</span><span class="sxs-lookup"><span data-stu-id="207a3-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="207a3-104">Узнайте, как восстановить toomanage учетные записи хранения в toofind стека Azure и освобождения пространства хранения, исходя из потребностей бизнеса.</span><span class="sxs-lookup"><span data-stu-id="207a3-104">Learn how toomanage storage accounts in Azure Stack toofind, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="207a3-105"><a name="find"></a>Найти учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="207a3-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="207a3-106">список учетных записей хранения в регионе hello Hello можно просмотреть в Azure стека с помощью:</span><span class="sxs-lookup"><span data-stu-id="207a3-106">hello list of storage accounts in hello region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="207a3-107">В веб-браузер перейдите к https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="207a3-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="207a3-108">Войдите в toohello портала администрирования Azure стека как оператор облака (с использованием учетных данных, предоставленные во время развертывания)</span><span class="sxs-lookup"><span data-stu-id="207a3-108">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="207a3-109">На панели мониторинга по умолчанию hello — найти hello **область управления** списке и нажмите кнопку область hello требуется tooexplore.</span><span class="sxs-lookup"><span data-stu-id="207a3-109">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore.</span></span> <span data-ttu-id="207a3-110">Например **(локальный**).</span><span class="sxs-lookup"><span data-stu-id="207a3-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="207a3-111">Выберите **хранения** из hello **поставщиков ресурсов** списка.</span><span class="sxs-lookup"><span data-stu-id="207a3-111">Select **Storage** from hello **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="207a3-112">Теперь, в колонке администратора поставщика ресурсов хранилища hello – прокрутите вниз до hello **учетные записи хранения** и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="207a3-112">Now, on hello storage Resource Provider administrator blade – scroll down to hello **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="207a3-113">Полученная страница Hello — hello список учетных записей хранения в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="207a3-113">hello resulting page is hello list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="207a3-114">По умолчанию hello первые 10 отображаются учетные записи.</span><span class="sxs-lookup"><span data-stu-id="207a3-114">By default, hello first 10 accounts are displayed.</span></span> <span data-ttu-id="207a3-115">Вы можете toofetch несколько, щелкнув hello **дополнительной загрузки** ссылке hello нижней части списка hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-115">You can choose toofetch more by clicking hello  **Load more** link at hello bottom of hello list.</span></span>

<span data-ttu-id="207a3-116">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="207a3-116">OR</span></span>

<span data-ttu-id="207a3-117">Если вы заинтересованы в определенной учетной записи хранения — вы можете **фильтра и fetch hello соответствующие счета** только.</span><span class="sxs-lookup"><span data-stu-id="207a3-117">If you are interested in a particular storage account – you can **filter and fetch hello relevant accounts** only.</span></span>


<span data-ttu-id="207a3-118">**toofilter для учетных записей:**</span><span class="sxs-lookup"><span data-stu-id="207a3-118">**toofilter for accounts:**</span></span>

1. <span data-ttu-id="207a3-119">Нажмите кнопку **фильтра** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-119">Click **Filter** at hello top of hello blade.</span></span>
2. <span data-ttu-id="207a3-120">В колонке hello фильтр, он позволяет toospecify **имя учетной записи**, **идентификатор подписки** или **состояние** список hello toofine настройки хранилища учетных записей toobe отображается.</span><span class="sxs-lookup"><span data-stu-id="207a3-120">On hello Filter blade, it allows you toospecify **account name**, **subscription ID** or **status** toofine-tune hello list of storage accounts toobe displayed.</span></span> <span data-ttu-id="207a3-121">Используйте их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="207a3-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="207a3-122">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="207a3-122">Click **Update**.</span></span> <span data-ttu-id="207a3-123">Обновление списка Hello следует соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="207a3-123">hello list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="207a3-124">Фильтр hello tooreset: щелкните **фильтра**, очистить выбранные элементы и обновлять.</span><span class="sxs-lookup"><span data-stu-id="207a3-124">tooreset hello filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="207a3-125">поле поиска Hello (на hello в верхней части колонки список учетных записей хранилища hello) позволяет выделять hello выбран текст hello список учетных записей.</span><span class="sxs-lookup"><span data-stu-id="207a3-125">hello search text box (on hello top of hello storage accounts list blade) lets you highlight hello selected text in hello list of accounts.</span></span> <span data-ttu-id="207a3-126">Это очень удобно в случае hello в тех случаях, когда hello полное имя или идентификатор не легко доступны.</span><span class="sxs-lookup"><span data-stu-id="207a3-126">This is really handy in hello case when hello full name or id is not easily available.</span></span>

<span data-ttu-id="207a3-127">Можно использовать произвольный текст здесь toohelp найти hello учетной записи, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="207a3-127">You can use free text here toohelp find hello account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="207a3-128">Просмотрите сведения об учетной записи</span><span class="sxs-lookup"><span data-stu-id="207a3-128">Look at account details</span></span>
<span data-ttu-id="207a3-129">После нахождения hello учетных записей, что вы заинтересованы в просмотре можно щелкнуть tooview hello определенную учетную запись некоторые сведения.</span><span class="sxs-lookup"><span data-stu-id="207a3-129">Once you have located hello accounts you are interested in viewing, you can click hello particular account tooview certain details.</span></span> <span data-ttu-id="207a3-130">Новая колонка открывается с hello учетные данные, такие как: hello тип учетной записи hello, время создания, расположение, и т. д.</span><span class="sxs-lookup"><span data-stu-id="207a3-130">A new blade opens with hello account details such as: hello type of hello account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="207a3-131">Восстановление удаленной учетной записи</span><span class="sxs-lookup"><span data-stu-id="207a3-131">Recover a deleted account</span></span>
<span data-ttu-id="207a3-132">В ситуации, когда необходимо toorecover может быть удаленной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="207a3-132">You may be in a situation where you need toorecover a deleted account.</span></span>

<span data-ttu-id="207a3-133">В стеке Azure является toodo очень простым способом:</span><span class="sxs-lookup"><span data-stu-id="207a3-133">In Azure Stack there is a very simple way toodo that:</span></span>

1. <span data-ttu-id="207a3-134">Просмотрите список учетных записей хранилища toohello.</span><span class="sxs-lookup"><span data-stu-id="207a3-134">Browse toohello storage accounts list.</span></span> <span data-ttu-id="207a3-135">В разделе [найти учетную запись хранения](#find) в этом разделе для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="207a3-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="207a3-136">Найти этой конкретной учетной записи в списке hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-136">Locate that particular account in hello list.</span></span> <span data-ttu-id="207a3-137">Может потребоваться toofilter.</span><span class="sxs-lookup"><span data-stu-id="207a3-137">You may need toofilter.</span></span>
3. <span data-ttu-id="207a3-138">Проверьте hello *состояние* hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="207a3-138">Check hello *state* of hello account.</span></span> <span data-ttu-id="207a3-139">Должно быть указано **Deleted**.</span><span class="sxs-lookup"><span data-stu-id="207a3-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="207a3-140">Выберите учетную запись hello, который открывает колонку сведения учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-140">Click hello account which opens hello account details blade.</span></span>
5. <span data-ttu-id="207a3-141">На основе этой колонки найдите hello **восстановить** кнопку и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="207a3-141">On top of this blade, locate hello **Recover** button and click it.</span></span>
6. <span data-ttu-id="207a3-142">Нажмите кнопку **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="207a3-142">Click **Yes** tooconfirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="207a3-143">Hello восстановления находится в *обработать... Подождите* для указывает на то, что она выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="207a3-143">hello recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="207a3-144">Можно также щелкнуть значок «звонка» hello вверху hello hello портал, чтобы просмотреть ход выполнения указаний.</span><span class="sxs-lookup"><span data-stu-id="207a3-144">You can also click hello “bell” icon at hello top of hello portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="207a3-145">После восстановления hello учетная запись успешно синхронизирован, он может использоваться повторно.</span><span class="sxs-lookup"><span data-stu-id="207a3-145">Once hello recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="207a3-146">Некоторые проблемы</span><span class="sxs-lookup"><span data-stu-id="207a3-146">Some Gotchas</span></span>
* <span data-ttu-id="207a3-147">Учетной записи удаленных отобразится состояние в качестве **за пределы хранения**.</span><span class="sxs-lookup"><span data-stu-id="207a3-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="207a3-148">Это означает, что учетная запись удалена hello hello срок хранения превысил и не может быть восстановлен.</span><span class="sxs-lookup"><span data-stu-id="207a3-148">This means that hello deleted account has exceeded hello retention period and may not be recoverable.</span></span>
* <span data-ttu-id="207a3-149">Ваш удаленной учетной записи не отображается в списке учетных записей hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-149">Your deleted account does not show in hello accounts list.</span></span>
  
  <span data-ttu-id="207a3-150">Это может означать hello удалена учетная запись уже была сбора мусора.</span><span class="sxs-lookup"><span data-stu-id="207a3-150">This could mean that hello deleted account has already been garbage collected.</span></span> <span data-ttu-id="207a3-151">В этом случае его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="207a3-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="207a3-152">В разделе [освобождения пространства](#reclaim) в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="207a3-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-hello-retention-period"></a><span data-ttu-id="207a3-153">Настроить срок хранения hello</span><span class="sxs-lookup"><span data-stu-id="207a3-153">Set hello retention period</span></span>
<span data-ttu-id="207a3-154">Настройка срока хранения Hello позволяет toospecify оператор облако период времени в днях (от 0 до 9999 дней) во время любой удаленной учетную запись, которая потенциально может быть восстановлен.</span><span class="sxs-lookup"><span data-stu-id="207a3-154">hello retention period setting allows a cloud operator toospecify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="207a3-155">Hello срок хранения по умолчанию имеет значение too15 дней.</span><span class="sxs-lookup"><span data-stu-id="207a3-155">hello default retention period is set too15 days.</span></span> <span data-ttu-id="207a3-156">Установка значения hello слишком «0» означает, что любой удаленной учетной записи немедленно выходит за хранение и помеченных для периодическую сборку мусора.</span><span class="sxs-lookup"><span data-stu-id="207a3-156">Setting hello value too“0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="207a3-157">**срок хранения toochange hello:**</span><span class="sxs-lookup"><span data-stu-id="207a3-157">**toochange hello retention period:**</span></span>

1. <span data-ttu-id="207a3-158">В веб-браузер перейдите к https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="207a3-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="207a3-159">Войдите в toohello портала администрирования Azure стека как оператор облака (с использованием учетных данных, предоставленные во время развертывания)</span><span class="sxs-lookup"><span data-stu-id="207a3-159">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="207a3-160">На панели мониторинга по умолчанию hello — найти hello **область управления** списке и нажмите кнопку область hello требуется tooexplore — например **(локальный**).</span><span class="sxs-lookup"><span data-stu-id="207a3-160">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore – for example **(local**).</span></span>
4. <span data-ttu-id="207a3-161">Выберите **хранения** из hello **поставщиков ресурсов** списка.</span><span class="sxs-lookup"><span data-stu-id="207a3-161">Select **Storage** from hello **Resource Providers** list.</span></span>
5. <span data-ttu-id="207a3-162">Нажмите кнопку **параметры** в колонке параметр hello top tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-162">Click **Settings** at hello top tooopen hello setting blade.</span></span>
6. <span data-ttu-id="207a3-163">Нажмите кнопку **конфигурации** измените значение срока хранения hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-163">Click **Configuration** then edit hello retention period value.</span></span>

   <span data-ttu-id="207a3-164">Задайте hello количество дней, а затем сохраните его.</span><span class="sxs-lookup"><span data-stu-id="207a3-164">Set hello number of days and then save it.</span></span>
   
   <span data-ttu-id="207a3-165">Это значение немедленно и задать для всего региона.</span><span class="sxs-lookup"><span data-stu-id="207a3-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="207a3-166"><a name="reclaim"></a>Освобождения пространства</span><span class="sxs-lookup"><span data-stu-id="207a3-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="207a3-167">Одна из hello побочные эффекты с периодом хранения — что удаленной учетной записи продолжается tooconsume емкости, пока они поступают из срока хранения hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-167">One of hello side effects of having a retention period is that a deleted account continues tooconsume capacity until it comes out of hello retention period.</span></span> <span data-ttu-id="207a3-168">Как облако оператора, может потребоваться hello tooreclaim способом удален места учетной записи, хотя еще не истек срок хранения hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-168">As a cloud operator you may need a way tooreclaim hello deleted account space even though hello retention period has not yet expired.</span></span>

<span data-ttu-id="207a3-169">Емкость можно освободить с помощью портала hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="207a3-169">You can reclaim capacity using either hello portal or PowerShell.</span></span>

<span data-ttu-id="207a3-170">**емкость tooreclaim с помощью портала hello:**</span><span class="sxs-lookup"><span data-stu-id="207a3-170">**tooreclaim capacity using hello portal:**</span></span>
1. <span data-ttu-id="207a3-171">Перейдите в колонку учетные записи хранения toohello.</span><span class="sxs-lookup"><span data-stu-id="207a3-171">Navigate toohello storage accounts blade.</span></span> <span data-ttu-id="207a3-172">В разделе [найти учетную запись хранения](#find).</span><span class="sxs-lookup"><span data-stu-id="207a3-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="207a3-173">Нажмите кнопку **освобождения пространства** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-173">Click **Reclaim space** at hello top of hello blade.</span></span>
3. <span data-ttu-id="207a3-174">Прочтите сообщение hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="207a3-174">Read hello message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="207a3-175">Дождитесь значок колокольчика hello см. в разделе уведомления успеха на портале hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-175">Wait for success notification See hello bell icon on hello portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="207a3-176">Обновите страницу учетных записей хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-176">Refresh hello Storage accounts page.</span></span> <span data-ttu-id="207a3-177">Hello удалены учетные записи больше не отображаются в списке hello, так как они были удалены.</span><span class="sxs-lookup"><span data-stu-id="207a3-177">hello deleted accounts are no longer shown in hello list because they have been purged.</span></span>

<span data-ttu-id="207a3-178">Можно также использовать PowerShell tooexplicitly переопределение hello срок и немедленно освобождения пространства.</span><span class="sxs-lookup"><span data-stu-id="207a3-178">You can also use PowerShell tooexplicitly override hello retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="207a3-179">**емкость tooreclaim с помощью PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="207a3-179">**tooreclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="207a3-180">Убедитесь, что Azure PowerShell установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="207a3-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="207a3-181">В противном случае используется hello, следуя инструкциям:</span><span class="sxs-lookup"><span data-stu-id="207a3-181">If not, use hello following instructions:</span></span> 
   * <span data-ttu-id="207a3-182">tooinstall hello последнюю версию Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="207a3-182">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="207a3-183">Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="207a3-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="207a3-184">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-184">Run hello following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="207a3-185">При выполнении этого командлета можно удалить без возможности восстановления hello учетной записи и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="207a3-185">If you run this cmdlet you permanently delete hello account and its contents.</span></span> <span data-ttu-id="207a3-186">Восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="207a3-186">It is not recoverable.</span></span> <span data-ttu-id="207a3-187">Это следует используйте с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="207a3-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="207a3-188">Дополнительные сведения см. в разделе слишком[документацию по powershell Azure стека.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="207a3-188">For more details, refer too[Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="207a3-189">Перенос контейнера</span><span class="sxs-lookup"><span data-stu-id="207a3-189">Migrate a container</span></span>
<span data-ttu-id="207a3-190">Из-за toouneven хранилища, используемые клиентами оператор облако может найти один или более базовых клиента общих папок с помощью больше места, чем другие.</span><span class="sxs-lookup"><span data-stu-id="207a3-190">Due toouneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="207a3-191">В этом случае оператор облака hello может попытаться выполнить toofree достаточно места на общем ресурсе нагрузкой hello путем переноса некоторые папки tooanother контейнеров больших двоичных объектов вручную.</span><span class="sxs-lookup"><span data-stu-id="207a3-191">If this occurs, hello cloud operator can attempt toofree up some space on hello stressed share by manually migrating some blob containers tooanother share.</span></span> 

<span data-ttu-id="207a3-192">Необходимо использовать контейнеры toomigrate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="207a3-192">You must use PowerShell toomigrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="207a3-193">Миграция контейнер больших двоичных объектов не поддерживает динамическую миграцию и в настоящее время является операцией вне сети.</span><span class="sxs-lookup"><span data-stu-id="207a3-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="207a3-194">Во время миграции и до завершения hello базового BLOB-объектов в этом контейнере не может использоваться и «вне сети».</span><span class="sxs-lookup"><span data-stu-id="207a3-194">During migration and until it is complete hello underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="207a3-195">**toomigrate контейнеры с помощью PowerShell.**</span><span class="sxs-lookup"><span data-stu-id="207a3-195">**toomigrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="207a3-196">Убедитесь, что Azure PowerShell установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="207a3-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="207a3-197">В противном случае используется hello, следуя инструкциям:</span><span class="sxs-lookup"><span data-stu-id="207a3-197">If not, use hello following instructions:</span></span>
    * <span data-ttu-id="207a3-198">tooinstall hello последнюю версию Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="207a3-198">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="207a3-199">Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="207a3-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="207a3-200">Получите имя фермы hello:</span><span class="sxs-lookup"><span data-stu-id="207a3-200">Get hello farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="207a3-201">Получите общие папки hello:</span><span class="sxs-lookup"><span data-stu-id="207a3-201">Get hello shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="207a3-202">Получите контейнеры hello для одного общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="207a3-202">Get hello containers for a given share.</span></span> <span data-ttu-id="207a3-203">Обратите внимание, что количество и намерением необязательные параметры:</span><span class="sxs-lookup"><span data-stu-id="207a3-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="207a3-204">Затем проверьте $containers:</span><span class="sxs-lookup"><span data-stu-id="207a3-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="207a3-205">Получите hello, наиболее общие папки назначения для миграции hello контейнера:</span><span class="sxs-lookup"><span data-stu-id="207a3-205">Get hello best destination shares for hello container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="207a3-206">Затем проверьте $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="207a3-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="207a3-207">Начнем миграции для контейнера, обратите внимание, что это реализацию async, поэтому можно использовать один цикл все контейнеры общими ресурсами и отслеживать состояние hello, с помощью идентификатора задания, возвращаемый hello.</span><span class="sxs-lookup"><span data-stu-id="207a3-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track hello status using hello returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="207a3-208">Затем проверьте $jobId:</span><span class="sxs-lookup"><span data-stu-id="207a3-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="207a3-209">Проверьте состояние задания миграции hello по идентификатору задания. По завершении миграции контейнера hello MigrationStatus задано слишком «завершение».</span><span class="sxs-lookup"><span data-stu-id="207a3-209">Check status of hello migration job by its job id. When hello container migration finishes, MigrationStatus is set too“Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="207a3-210">Вы можете отменить задание миграции в процессе выполнения.</span><span class="sxs-lookup"><span data-stu-id="207a3-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="207a3-211">Это является асинхронной операцией и могут отслеживаться с помощью $jobid еще раз:</span><span class="sxs-lookup"><span data-stu-id="207a3-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="207a3-212">Можно проверить состояние hello hello отмены миграции еще раз:</span><span class="sxs-lookup"><span data-stu-id="207a3-212">You can check hello status of hello migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  