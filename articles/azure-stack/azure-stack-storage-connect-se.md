---
title: "Подключаться к подписке Azure стека обозреватель хранилищ"
description: "Узнайте, как подключаться к подписке Azure стека Exporer хранилища"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 3c1ee7665da41c0fae9ddd492127495fe7e5581b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription"></a><span data-ttu-id="98445-103">Подключаться к подписке Azure стека обозреватель хранилищ</span><span class="sxs-lookup"><span data-stu-id="98445-103">Connect Storage Explorer to an Azure Stack subscription</span></span>

<span data-ttu-id="98445-104">Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, предназначенное для упрощения работы с данными стека хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="98445-104">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="98445-105">Существует несколько средств доступными для перемещения данных в и из стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98445-105">There are several tools avaialble to move data to and from Azure Stack Storage.</span></span> <span data-ttu-id="98445-106">Дополнительные сведения см. в разделе [средств для хранилища Azure стек передачи данных](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="98445-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="98445-107">В этой статье вы узнаете, как соединиться с учетных записей хранилища Azure стека с помощью обозревателя хранилищ.</span><span class="sxs-lookup"><span data-stu-id="98445-107">In this article, you learn how to connect to your Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="98445-108">Если вы не установили обозреватель хранилищ, [загрузки](http://www.storageexplorer.com/) и и установить его.</span><span class="sxs-lookup"><span data-stu-id="98445-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="98445-109">После подключения к подписке Azure стека можно использовать [обозреватель хранилищ Azure статьи](../vs-azure-tools-storage-manage-with-storage-explorer.md) для работы с данными Azure стека.</span><span class="sxs-lookup"><span data-stu-id="98445-109">After you connect to your Azure Stack subscription, you can use the [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="98445-110">Подготовка подписки Azure стека</span><span class="sxs-lookup"><span data-stu-id="98445-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="98445-111">Вам нужен доступ к рабочему столу стек Azure хост-компьютера или VPN-подключения для обозревателя хранилищ, доступ к подписке Azure стека.</span><span class="sxs-lookup"><span data-stu-id="98445-111">You need access to the Azure Stack host machine's desktop or a VPN connection for Storage Explorer to access the Azure Stack subscription.</span></span> <span data-ttu-id="98445-112">Дополнительные сведения о настройке VPN-подключения в Azure Stack см. в разделе [Подключение c VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="98445-112">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="98445-113">Пакет средств разработки стек Azure необходимо экспортировать корневой сертификат центра Azure стека.</span><span class="sxs-lookup"><span data-stu-id="98445-113">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span></span>

### <a name="to-export-and-then-import-the-azure-stack-certificate"></a><span data-ttu-id="98445-114">Чтобы экспортировать и импортировать сертификат стек Azure</span><span class="sxs-lookup"><span data-stu-id="98445-114">To export and then import the Azure Stack certificate</span></span>

1. <span data-ttu-id="98445-115">Откройте `mmc.exe` на машине узла Azure стека или локальный компьютер через VPN-подключения в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="98445-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span></span> 

2. <span data-ttu-id="98445-116">В меню **Файл** выберите **Добавить или удалить оснастку**, затем добавьте **сертификаты** для управления **учетной записью** **локального компьютера**.</span><span class="sxs-lookup"><span data-stu-id="98445-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="98445-117">В разделе **\Trusted Root Certification Authorities\Certificates Root\Certificated консоли (локальный компьютер)** найти **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="98445-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Загрузка корневого сертификата Azure Stack с помощью mmc.exe][25]

4. <span data-ttu-id="98445-119">Щелкните правой кнопкой мыши сертификат, выберите **все задачи** > **Экспорт**, а затем следуйте инструкциям, чтобы экспортировать сертификат с **X.509 в кодировке Base-64 (. (CER)**.</span><span class="sxs-lookup"><span data-stu-id="98445-119">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="98445-120">Экспортированный сертификат будет использоваться на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="98445-120">The exported certificate will be used in the next step.</span></span>
5. <span data-ttu-id="98445-121">Запустите проводник хранилища (Предварительная версия), и если вы видите **подключение к хранилищу Azure** диалогового окна поле, отмените его.</span><span class="sxs-lookup"><span data-stu-id="98445-121">Start Storage Explorer (Preview), and if you see the **Connect to Azure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="98445-122">На **изменить** последовательно выберите пункты **SSL-сертификаты**, а затем нажмите кнопку **импорта сертификатов**.</span><span class="sxs-lookup"><span data-stu-id="98445-122">On the **Edit** menu, point to **SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="98445-123">Используйте диалоговое окно выбора файла, чтобы найти и открыть сертификат, изученный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="98445-123">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span></span>

    <span data-ttu-id="98445-124">После импорта вам будет предложено перезапустить обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="98445-124">After importing, you are prompted to restart Storage Explorer.</span></span>

    ![Импорт сертификата в обозреватель хранилищ (предварительная версия)][27]

<span data-ttu-id="98445-126">Теперь вы готовы подключаться к подписке Azure стека обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="98445-126">Now you are ready to connect Storage Explorer to an Azure Stack subscription.</span></span>

### <a name="to-connect-an-azure-stack-subscription"></a><span data-ttu-id="98445-127">Для подключения подписки на стек Azure</span><span class="sxs-lookup"><span data-stu-id="98445-127">To connect an Azure Stack subscription</span></span>


1. <span data-ttu-id="98445-128">После перезапуска обозревателя хранилищ (предварительная версия) откройте меню **Изменить** и убедитесь, что **Target Azure Stack** (Целевой объект Azure Stack) выбран.</span><span class="sxs-lookup"><span data-stu-id="98445-128">After Storage Explorer (Preview) restarts, select the **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="98445-129">В противном случае выберите его и перезапустите обозреватель хранилищ, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="98445-129">If it is not selected, select it, and then restart Storage Explorer for the change to take effect.</span></span> <span data-ttu-id="98445-130">Эта настройка необходима для совместимости со средой Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98445-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![Проверка установки флажка Target Azure Stack (Целевой объект Azure Stack)][28]

7. <span data-ttu-id="98445-132">На панели слева щелкните **Управление учетными записями**.</span><span class="sxs-lookup"><span data-stu-id="98445-132">In the left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="98445-133">Отобразятся все учетные записи Майкрософт, в которые вы вошли.</span><span class="sxs-lookup"><span data-stu-id="98445-133">All the Microsoft accounts that you are signed in to are displayed.</span></span>

8. <span data-ttu-id="98445-134">Чтобы подключиться к учетной записи Azure Stack, выберите **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="98445-134">To connect to the Azure Stack account, select **Add an account**.</span></span>

    ![Добавление учетной записи Azure Stack][29]

9. <span data-ttu-id="98445-136">В **подключение к хранилищу Azure** диалогового **среды Azure**выберите **среду стека Azure используйте**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="98445-136">In the **Connect to Azure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="98445-137">Чтобы войти в учетную запись стек Azure, который связан с по крайней мере одну подписку Azure стека, заполните **войти в среду Azure стека** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="98445-137">To sign in with the Azure Stack account that's associated with at least one active Azure Stack subscription, fill in the **Sign in to Azure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="98445-138">Ниже приведены подробные сведения о каждом поле диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="98445-138">The details for each field are as follows:</span></span>

    * <span data-ttu-id="98445-139">**Имя среды.** Это поле может настраивать пользователь.</span><span class="sxs-lookup"><span data-stu-id="98445-139">**Environment name**: The field can be customized by user.</span></span>
    * <span data-ttu-id="98445-140">**ARM resource endpoint** (Конечная точка ресурса ARM). Примеры конечной точки ресурсов ARM:</span><span class="sxs-lookup"><span data-stu-id="98445-140">**ARM resource endpoint**: The samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="98445-141">Для оператора облака:</span><span class="sxs-lookup"><span data-stu-id="98445-141">For cloud operator:</span></span><br> <span data-ttu-id="98445-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="98445-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="98445-143">Для клиента:</span><span class="sxs-lookup"><span data-stu-id="98445-143">For tenant:</span></span><br> <span data-ttu-id="98445-144">https://Management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="98445-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="98445-145">**Идентификатор клиента**: необязательно.</span><span class="sxs-lookup"><span data-stu-id="98445-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="98445-146">Значение задается, только если необходимо указать каталог.</span><span class="sxs-lookup"><span data-stu-id="98445-146">The value is given only when the directory must be specified.</span></span>

12. <span data-ttu-id="98445-147">Выполнив вход с помощью учетной записи Azure Stack, на панели слева вы увидите подписки Azure Stack, связанные с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="98445-147">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="98445-148">Выберите подписки Azure Stack, с которыми вы собираетесь работать, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="98445-148">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="98445-149">(Чтобы выбрать или очистить все подписки Azure Stack, установите флажок **Все подписки**. Чтобы отменить выбор, снимите флажок.)</span><span class="sxs-lookup"><span data-stu-id="98445-149">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

    ![Выбор подписок Azure Stack после заполнения диалогового окна Custom Cloud Environment (Пользовательская облачная среда)][30]  
    <span data-ttu-id="98445-151">На панели слева отобразятся все учетные записи хранения, связанные с выбранными подписками Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98445-151">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![Список учетных записей хранения, включая учетные записи подписки Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="98445-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98445-153">Next steps</span></span>
* [<span data-ttu-id="98445-154">Приступая к работе с обозреватель хранилищ (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="98445-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="98445-155">Хранилища Azure стека: различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="98445-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="98445-156">Дополнительные сведения о хранилище Azure см. в разделе [ознакомление с хранилищем Microsoft Azure](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="98445-156">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
