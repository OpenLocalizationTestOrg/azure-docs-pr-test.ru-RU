---
title: "Управление учетными записями хранилища Azure стек | Документы Microsoft"
description: "Узнайте, как найти, управление, восстановление и освободить учетных записей хранилища Azure стека"
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
ms.openlocfilehash: 6e14bd6312135b45984a82099e68a934ec2a4a70
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="371d2-103">Управление учетными записями хранения в стек Azure</span><span class="sxs-lookup"><span data-stu-id="371d2-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="371d2-104">Узнайте, как управлять учетными записями хранилища Azure стека для поиска, восстановление и освобождения пространства хранения, исходя из потребностей бизнеса.</span><span class="sxs-lookup"><span data-stu-id="371d2-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="371d2-105"><a name="find"></a>Найти учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="371d2-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="371d2-106">Можно просмотреть список учетных записей хранения в регионе в Azure стека с помощью:</span><span class="sxs-lookup"><span data-stu-id="371d2-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="371d2-107">В веб-браузер перейдите к https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="371d2-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="371d2-108">Войдите на портал администрирования стек Azure как оператор облака (с использованием учетных данных, предоставленные во время развертывания)</span><span class="sxs-lookup"><span data-stu-id="371d2-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="371d2-109">Найдите на панели мониторинга по умолчанию — **область управления** списке и нажмите кнопку область, необходимо просмотреть.</span><span class="sxs-lookup"><span data-stu-id="371d2-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span></span> <span data-ttu-id="371d2-110">Например **(локальный**).</span><span class="sxs-lookup"><span data-stu-id="371d2-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="371d2-111">Выберите **хранения** из **поставщиков ресурсов** списка.</span><span class="sxs-lookup"><span data-stu-id="371d2-111">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="371d2-112">Теперь, в колонке администратора поставщика ресурсов хранилища – прокрутите вниз до **учетные записи хранения** и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="371d2-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="371d2-113">Страницы приведен список учетных записей хранения в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="371d2-113">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="371d2-114">По умолчанию отображаются первые 10 учетных записей.</span><span class="sxs-lookup"><span data-stu-id="371d2-114">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="371d2-115">Вы можете получить более, щелкнув **дополнительной загрузки** ссылку в нижней части списка.</span><span class="sxs-lookup"><span data-stu-id="371d2-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="371d2-116">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="371d2-116">OR</span></span>

<span data-ttu-id="371d2-117">Если вы заинтересованы в определенной учетной записи хранения — вы можете **фильтрации и получения соответствующих учетных записей** только.</span><span class="sxs-lookup"><span data-stu-id="371d2-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="371d2-118">**Для фильтрации для учетных записей:**</span><span class="sxs-lookup"><span data-stu-id="371d2-118">**To filter for accounts:**</span></span>

1. <span data-ttu-id="371d2-119">Нажмите кнопку **фильтра** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="371d2-119">Click **Filter** at the top of the blade.</span></span>
2. <span data-ttu-id="371d2-120">В колонке фильтр, он позволяет указать **имя учетной записи**, **идентификатор подписки** или **состояние** для точной настройки в списке учетных записей хранилища для отображения.</span><span class="sxs-lookup"><span data-stu-id="371d2-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="371d2-121">Используйте их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="371d2-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="371d2-122">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="371d2-122">Click **Update**.</span></span> <span data-ttu-id="371d2-123">Список следует обновить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="371d2-123">The list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="371d2-124">Чтобы сбросить фильтр: щелкните **фильтра**, очистить выбранные элементы и обновлять.</span><span class="sxs-lookup"><span data-stu-id="371d2-124">To reset the filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="371d2-125">Поле поиска (в верхней части колонки список учетных записей хранилища) позволяет выделить тексту, выбранному в списке учетных записей.</span><span class="sxs-lookup"><span data-stu-id="371d2-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="371d2-126">Это очень удобно в случае, если полное имя или идентификатор легко недоступен.</span><span class="sxs-lookup"><span data-stu-id="371d2-126">This is really handy in the case when the full name or id is not easily available.</span></span>

<span data-ttu-id="371d2-127">Произвольный текст здесь можно использовать для поиска учетной записи, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="371d2-127">You can use free text here to help find the account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="371d2-128">Просмотрите сведения об учетной записи</span><span class="sxs-lookup"><span data-stu-id="371d2-128">Look at account details</span></span>
<span data-ttu-id="371d2-129">После того как вы нашли учетные записи, которые вас интересуют просмотра, можно щелкнуть определенной учетной записи для просмотра определенных сведений.</span><span class="sxs-lookup"><span data-stu-id="371d2-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span></span> <span data-ttu-id="371d2-130">Открывается новая колонка с учетные данные, такие как: тип учетной записи, время создания, расположение и т. д.</span><span class="sxs-lookup"><span data-stu-id="371d2-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="371d2-131">Восстановление удаленной учетной записи</span><span class="sxs-lookup"><span data-stu-id="371d2-131">Recover a deleted account</span></span>
<span data-ttu-id="371d2-132">Возможно, в ситуации, когда необходимо для восстановления удаленной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="371d2-132">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="371d2-133">В стеке Azure есть очень простой способ сделать это:</span><span class="sxs-lookup"><span data-stu-id="371d2-133">In Azure Stack there is a very simple way to do that:</span></span>

1. <span data-ttu-id="371d2-134">Перейдите к списку учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="371d2-134">Browse to the storage accounts list.</span></span> <span data-ttu-id="371d2-135">В разделе [найти учетную запись хранения](#find) в этом разделе для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="371d2-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="371d2-136">Найдите этой конкретной учетной записи в списке.</span><span class="sxs-lookup"><span data-stu-id="371d2-136">Locate that particular account in the list.</span></span> <span data-ttu-id="371d2-137">Необходимо фильтровать.</span><span class="sxs-lookup"><span data-stu-id="371d2-137">You may need to filter.</span></span>
3. <span data-ttu-id="371d2-138">Проверьте *состояние* учетной записи.</span><span class="sxs-lookup"><span data-stu-id="371d2-138">Check the *state* of the account.</span></span> <span data-ttu-id="371d2-139">Должно быть указано **Deleted**.</span><span class="sxs-lookup"><span data-stu-id="371d2-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="371d2-140">Выберите учетную запись, которая открывает колонку сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="371d2-140">Click the account which opens the account details blade.</span></span>
5. <span data-ttu-id="371d2-141">На основе этой колонки найдите **восстановить** кнопку и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="371d2-141">On top of this blade, locate the **Recover** button and click it.</span></span>
6. <span data-ttu-id="371d2-142">Нажмите кнопку **Да** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="371d2-142">Click **Yes** to confirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="371d2-143">Восстановления находится в *обработать... Подождите* для указывает на то, что она выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="371d2-143">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="371d2-144">Также можно щелкнуть значок «колокольчика» в верхней части портала, чтобы просмотреть ход выполнения указаний.</span><span class="sxs-lookup"><span data-stu-id="371d2-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="371d2-145">После восстановленной учетная запись успешно синхронизирован, он может использоваться повторно.</span><span class="sxs-lookup"><span data-stu-id="371d2-145">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="371d2-146">Некоторые проблемы</span><span class="sxs-lookup"><span data-stu-id="371d2-146">Some Gotchas</span></span>
* <span data-ttu-id="371d2-147">Учетной записи удаленных отобразится состояние в качестве **за пределы хранения**.</span><span class="sxs-lookup"><span data-stu-id="371d2-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="371d2-148">Это означает, что срок хранения превысил удаленной учетной записи и не может быть восстановлен.</span><span class="sxs-lookup"><span data-stu-id="371d2-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="371d2-149">На удаленной учетной записи не отображается в списке учетных записей.</span><span class="sxs-lookup"><span data-stu-id="371d2-149">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="371d2-150">Это может означать, что удаленная учетная запись уже была сбора мусора.</span><span class="sxs-lookup"><span data-stu-id="371d2-150">This could mean that the deleted account has already been garbage collected.</span></span> <span data-ttu-id="371d2-151">В этом случае его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="371d2-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="371d2-152">В разделе [освобождения пространства](#reclaim) в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="371d2-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="371d2-153">Установить срок хранения</span><span class="sxs-lookup"><span data-stu-id="371d2-153">Set the retention period</span></span>
<span data-ttu-id="371d2-154">Настройка срока хранения позволяет оператор облака указать период времени в дней (от 0 до 9999 дней), в течение которых любой удаленной учетной записи потенциально могут быть восстановлены.</span><span class="sxs-lookup"><span data-stu-id="371d2-154">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="371d2-155">Срок хранения по умолчанию равно 15 дней.</span><span class="sxs-lookup"><span data-stu-id="371d2-155">The default retention period is set to 15 days.</span></span> <span data-ttu-id="371d2-156">При установке значения «0» означает, что любой удаленной учетной записи немедленно выходит за хранение и помеченных для периодическую сборку мусора.</span><span class="sxs-lookup"><span data-stu-id="371d2-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="371d2-157">**Чтобы изменить срок хранения:**</span><span class="sxs-lookup"><span data-stu-id="371d2-157">**To change the retention period:**</span></span>

1. <span data-ttu-id="371d2-158">В веб-браузер перейдите к https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="371d2-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="371d2-159">Войдите на портал администрирования стек Azure как оператор облака (с использованием учетных данных, предоставленные во время развертывания)</span><span class="sxs-lookup"><span data-stu-id="371d2-159">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="371d2-160">Найдите на панели мониторинга по умолчанию — **область управления** списке и нажмите кнопку область, необходимо изучить — например **(локальный**).</span><span class="sxs-lookup"><span data-stu-id="371d2-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="371d2-161">Выберите **хранения** из **поставщиков ресурсов** списка.</span><span class="sxs-lookup"><span data-stu-id="371d2-161">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="371d2-162">Нажмите кнопку **параметры** вверху, чтобы открыть колонку параметров.</span><span class="sxs-lookup"><span data-stu-id="371d2-162">Click **Settings** at the top to open the setting blade.</span></span>
6. <span data-ttu-id="371d2-163">Нажмите кнопку **конфигурации** затем измените значения срока хранения.</span><span class="sxs-lookup"><span data-stu-id="371d2-163">Click **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="371d2-164">Задайте количество дней, а затем сохраните его.</span><span class="sxs-lookup"><span data-stu-id="371d2-164">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="371d2-165">Это значение немедленно и задать для всего региона.</span><span class="sxs-lookup"><span data-stu-id="371d2-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="371d2-166"><a name="reclaim"></a>Освобождения пространства</span><span class="sxs-lookup"><span data-stu-id="371d2-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="371d2-167">Одним из побочных эффектов наличия срок хранения является удаленной учетной записи продолжает потребления мощностей, пока они поступают из срока хранения.</span><span class="sxs-lookup"><span data-stu-id="371d2-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="371d2-168">Как оператор облако может потребоваться возможность освободить место удаленной учетной записи, даже если еще не истек срок хранения.</span><span class="sxs-lookup"><span data-stu-id="371d2-168">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="371d2-169">Можно освободить с помощью PowerShell или портала емкости.</span><span class="sxs-lookup"><span data-stu-id="371d2-169">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="371d2-170">**Для освобождения пространства с помощью портала:**</span><span class="sxs-lookup"><span data-stu-id="371d2-170">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="371d2-171">Перейдите к колонке учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="371d2-171">Navigate to the storage accounts blade.</span></span> <span data-ttu-id="371d2-172">В разделе [найти учетную запись хранения](#find).</span><span class="sxs-lookup"><span data-stu-id="371d2-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="371d2-173">Нажмите кнопку **освобождения пространства** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="371d2-173">Click **Reclaim space** at the top of the blade.</span></span>
3. <span data-ttu-id="371d2-174">Прочтите сообщение и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="371d2-174">Read the message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="371d2-175">Дождитесь, пока уведомление об успехе см. в разделе значок колокольчика на портале.</span><span class="sxs-lookup"><span data-stu-id="371d2-175">Wait for success notification See the bell icon on the portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="371d2-176">Обновите страницу учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="371d2-176">Refresh the Storage accounts page.</span></span> <span data-ttu-id="371d2-177">Удаленные учетные записи больше не отображаются в списке, так как они были удалены.</span><span class="sxs-lookup"><span data-stu-id="371d2-177">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="371d2-178">Можно также использовать PowerShell явно переопределить срок хранения и немедленно освобождения пространства.</span><span class="sxs-lookup"><span data-stu-id="371d2-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="371d2-179">**Для освобождения пространства с помощью PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="371d2-179">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="371d2-180">Убедитесь, что Azure PowerShell установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="371d2-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="371d2-181">Если нет, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="371d2-181">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="371d2-182">Чтобы установить последнюю версию Azure PowerShell и связать ее с подпиской Azure, в разделе [описывается установка и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="371d2-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="371d2-183">Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="371d2-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="371d2-184">Выполните следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="371d2-184">Run the following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="371d2-185">При выполнении этого командлета можно удалить без возможности восстановления учетной записи и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="371d2-185">If you run this cmdlet you permanently delete the account and its contents.</span></span> <span data-ttu-id="371d2-186">Восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="371d2-186">It is not recoverable.</span></span> <span data-ttu-id="371d2-187">Это следует используйте с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="371d2-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="371d2-188">Дополнительные сведения см. в [документации стек Azure powershell.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="371d2-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="371d2-189">Перенос контейнера</span><span class="sxs-lookup"><span data-stu-id="371d2-189">Migrate a container</span></span>
<span data-ttu-id="371d2-190">Из-за неравномерной хранилища, используемые клиентами оператор облако может найти один или более базовых клиента общих папок с помощью больше места, чем другие.</span><span class="sxs-lookup"><span data-stu-id="371d2-190">Due to uneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="371d2-191">В этом случае оператор облака можно попытаться Освободите место на этом ресурсе нагрузкой путем миграции некоторых контейнеров больших двоичных объектов еще одну общую папку вручную.</span><span class="sxs-lookup"><span data-stu-id="371d2-191">If this occurs, the cloud operator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span></span> 

<span data-ttu-id="371d2-192">Необходимо использовать PowerShell для миграции контейнеров.</span><span class="sxs-lookup"><span data-stu-id="371d2-192">You must use PowerShell to migrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="371d2-193">Миграция контейнер больших двоичных объектов не поддерживает динамическую миграцию и в настоящее время является операцией вне сети.</span><span class="sxs-lookup"><span data-stu-id="371d2-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="371d2-194">Во время миграции и до завершения базового BLOB-объектов в этот контейнер не может использоваться и «вне сети».</span><span class="sxs-lookup"><span data-stu-id="371d2-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="371d2-195">**Чтобы перенести контейнеры с помощью PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="371d2-195">**To migrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="371d2-196">Убедитесь, что Azure PowerShell установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="371d2-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="371d2-197">Если нет, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="371d2-197">If not, use the following instructions:</span></span>
    * <span data-ttu-id="371d2-198">Чтобы установить последнюю версию Azure PowerShell и связать ее с подпиской Azure, в разделе [описывается установка и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="371d2-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="371d2-199">Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="371d2-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="371d2-200">Получите имя фермы:</span><span class="sxs-lookup"><span data-stu-id="371d2-200">Get the farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="371d2-201">Получение общих папок:</span><span class="sxs-lookup"><span data-stu-id="371d2-201">Get the shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="371d2-202">Получите контейнеры для одного общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="371d2-202">Get the containers for a given share.</span></span> <span data-ttu-id="371d2-203">Обратите внимание, что количество и намерением необязательные параметры:</span><span class="sxs-lookup"><span data-stu-id="371d2-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="371d2-204">Затем проверьте $containers:</span><span class="sxs-lookup"><span data-stu-id="371d2-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="371d2-205">Получите наиболее общие папки назначения для миграции контейнера:</span><span class="sxs-lookup"><span data-stu-id="371d2-205">Get the best destination shares for the container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="371d2-206">Затем проверьте $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="371d2-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="371d2-207">Начнем миграции для контейнера, обратите внимание, что это реализацию async, поэтому один цикл все контейнеры в общей папке и отслеживать состояние с помощью идентификатора возвращенные задания.</span><span class="sxs-lookup"><span data-stu-id="371d2-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="371d2-208">Затем проверьте $jobId:</span><span class="sxs-lookup"><span data-stu-id="371d2-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="371d2-209">Проверьте состояние задания миграции по идентификатору задания. По завершении миграции контейнера MigrationStatus имеет значение «Completed».</span><span class="sxs-lookup"><span data-stu-id="371d2-209">Check status of the migration job by its job id. When the container migration finishes, MigrationStatus is set to “Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="371d2-210">Вы можете отменить задание миграции в процессе выполнения.</span><span class="sxs-lookup"><span data-stu-id="371d2-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="371d2-211">Это является асинхронной операцией и могут отслеживаться с помощью $jobid еще раз:</span><span class="sxs-lookup"><span data-stu-id="371d2-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="371d2-212">Можно проверить состояние отмены миграции еще раз:</span><span class="sxs-lookup"><span data-stu-id="371d2-212">You can check the status of the migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  