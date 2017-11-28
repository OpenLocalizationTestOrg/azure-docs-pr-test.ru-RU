---
title: "Обозреватель хранилищ aaaConnect tooan подписки стек Azure"
description: "Узнайте, как tooan tooconnect Exporer хранилища Azure стека подписки"
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
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a><span data-ttu-id="61f3b-103">Подключение подписки Azure стека tooan обозреватель хранилищ</span><span class="sxs-lookup"><span data-stu-id="61f3b-103">Connect Storage Explorer tooan Azure Stack subscription</span></span>

<span data-ttu-id="61f3b-104">Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, позволяющее tooeasily работы с данными стека хранилища Azure для Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="61f3b-104">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="61f3b-105">Существует несколько tooand средства доступными toomove данные из стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="61f3b-105">There are several tools avaialble toomove data tooand from Azure Stack Storage.</span></span> <span data-ttu-id="61f3b-106">Дополнительные сведения см. в разделе [средств для хранилища Azure стек передачи данных](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="61f3b-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="61f3b-107">В этой статье вы узнаете, как tooconnect tooyour хранилища Azure стека учетных записей с помощью обозревателя хранилищ.</span><span class="sxs-lookup"><span data-stu-id="61f3b-107">In this article, you learn how tooconnect tooyour Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="61f3b-108">Если вы не установили обозреватель хранилищ, [загрузки](http://www.storageexplorer.com/) и и установить его.</span><span class="sxs-lookup"><span data-stu-id="61f3b-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="61f3b-109">После подключения подписки tooyour стека Azure можно использовать hello [обозреватель хранилищ Azure статьи](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork с данными Azure стека.</span><span class="sxs-lookup"><span data-stu-id="61f3b-109">After you connect tooyour Azure Stack subscription, you can use hello [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="61f3b-110">Подготовка подписки Azure стека</span><span class="sxs-lookup"><span data-stu-id="61f3b-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="61f3b-111">Требуется доступ к рабочего стола toohello стека Azure хост-компьютера или VPN-подключения для hello стек Azure Storage Explorer tooaccess подписки.</span><span class="sxs-lookup"><span data-stu-id="61f3b-111">You need access toohello Azure Stack host machine's desktop or a VPN connection for Storage Explorer tooaccess hello Azure Stack subscription.</span></span> <span data-ttu-id="61f3b-112">tooset копирование tooAzure подключения VPN стека, в статье toolearn [подключения tooAzure стека с помощью VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="61f3b-112">toolearn how tooset up a VPN connection tooAzure Stack, see [Connect tooAzure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="61f3b-113">Hello Azure стека Development Kit требуется сертификат корневого центра Azure стека hello tooexport.</span><span class="sxs-lookup"><span data-stu-id="61f3b-113">For hello Azure Stack Development Kit, you need tooexport hello Azure Stack authority root certificate.</span></span>

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a><span data-ttu-id="61f3b-114">tooexport, а затем импортировать сертификат Azure стека hello</span><span class="sxs-lookup"><span data-stu-id="61f3b-114">tooexport and then import hello Azure Stack certificate</span></span>

1. <span data-ttu-id="61f3b-115">Откройте `mmc.exe` на машине узла Azure стека или локальный компьютер с tooAzure подключения VPN стека.</span><span class="sxs-lookup"><span data-stu-id="61f3b-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection tooAzure Stack.</span></span> 

2. <span data-ttu-id="61f3b-116">В **файл**выберите **добавить или удалить оснастку**и затем добавьте **сертификаты** toomanage **учетная запись компьютера** из **локального Компьютер**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** toomanage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="61f3b-117">В разделе **\Trusted Root Certification Authorities\Certificates Root\Certificated консоли (локальный компьютер)** найти **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Загрузить hello Azure стека корневого сертификата через mmc.exe][25]

4. <span data-ttu-id="61f3b-119">Сертификат hello щелкните правой кнопкой мыши, выберите **все задачи** > **Экспорт**и следуйте hello инструкции tooexport hello сертификат с **Base64-кодировке X.509 (. (CER)**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-119">Right-click hello certificate, select **All Tasks** > **Export**, and then follow hello instructions tooexport hello certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="61f3b-120">Hello экспортированный сертификат будет использоваться в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="61f3b-120">hello exported certificate will be used in hello next step.</span></span>
5. <span data-ttu-id="61f3b-121">Запустите проводник хранилища (Предварительная версия), и если вы видите hello **подключения tooAzure хранения** диалогового окна поле, отмените его.</span><span class="sxs-lookup"><span data-stu-id="61f3b-121">Start Storage Explorer (Preview), and if you see hello **Connect tooAzure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="61f3b-122">На hello **изменить** меню выберите пункт слишком**SSL-сертификаты**и нажмите кнопку **импорта сертификатов**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-122">On hello **Edit** menu, point too**SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="61f3b-123">Используйте hello файл выбора диалогового окна поле toofind и откройте hello сертификата, экспортированного в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="61f3b-123">Use hello file picker dialog box toofind and open hello certificate that you exported in hello previous step.</span></span>

    <span data-ttu-id="61f3b-124">После импорта, запрашиваемые toorestart обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="61f3b-124">After importing, you are prompted toorestart Storage Explorer.</span></span>

    ![Импортируйте сертификат hello в обозреватель хранилищ (Предварительная версия)][27]

<span data-ttu-id="61f3b-126">Теперь все готово tooconnect подписки Azure стека tooan обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="61f3b-126">Now you are ready tooconnect Storage Explorer tooan Azure Stack subscription.</span></span>

### <a name="tooconnect-an-azure-stack-subscription"></a><span data-ttu-id="61f3b-127">tooconnect подписка стек Azure</span><span class="sxs-lookup"><span data-stu-id="61f3b-127">tooconnect an Azure Stack subscription</span></span>


1. <span data-ttu-id="61f3b-128">После перезапуска обозревателя хранилищ (Предварительная версия) выберите hello **изменить** меню и убедитесь, что **стека Azure целевой** выбран.</span><span class="sxs-lookup"><span data-stu-id="61f3b-128">After Storage Explorer (Preview) restarts, select hello **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="61f3b-129">Если не выбран, выберите его и перезапустите обозреватель хранилищ для hello изменение tootake эффекта.</span><span class="sxs-lookup"><span data-stu-id="61f3b-129">If it is not selected, select it, and then restart Storage Explorer for hello change tootake effect.</span></span> <span data-ttu-id="61f3b-130">Эта настройка необходима для совместимости со средой Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="61f3b-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![Проверка установки флажка Target Azure Stack (Целевой объект Azure Stack)][28]

7. <span data-ttu-id="61f3b-132">Выберите в левой области hello **управление учетными записями**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-132">In hello left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="61f3b-133">Что вы вошли в tooare отображаются все клиенты Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="61f3b-133">All hello Microsoft accounts that you are signed in tooare displayed.</span></span>

8. <span data-ttu-id="61f3b-134">Выберите tooconnect toohello учетная запись Azure стека, **добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-134">tooconnect toohello Azure Stack account, select **Add an account**.</span></span>

    ![Добавление учетной записи Azure Stack][29]

9. <span data-ttu-id="61f3b-136">В hello **подключения tooAzure хранения** диалогового **среды Azure**выберите **среду стека Azure используйте**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-136">In hello **Connect tooAzure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="61f3b-137">toosign вход с помощью hello Azure стека учетной записи, связанной с по крайней мере одну подписку Azure стека, заполните hello **входа в среду стека tooAzure** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="61f3b-137">toosign in with hello Azure Stack account that's associated with at least one active Azure Stack subscription, fill in hello **Sign in tooAzure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="61f3b-138">Ниже приведены сведения о Hello для каждого поля:</span><span class="sxs-lookup"><span data-stu-id="61f3b-138">hello details for each field are as follows:</span></span>

    * <span data-ttu-id="61f3b-139">**Имя среды**: hello поле может настраиваться пользователем.</span><span class="sxs-lookup"><span data-stu-id="61f3b-139">**Environment name**: hello field can be customized by user.</span></span>
    * <span data-ttu-id="61f3b-140">**Конечная точка ресурса ARM**: hello образцы конечных точек ресурсов диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="61f3b-140">**ARM resource endpoint**: hello samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="61f3b-141">Для оператора облака:</span><span class="sxs-lookup"><span data-stu-id="61f3b-141">For cloud operator:</span></span><br> <span data-ttu-id="61f3b-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="61f3b-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="61f3b-143">Для клиента:</span><span class="sxs-lookup"><span data-stu-id="61f3b-143">For tenant:</span></span><br> <span data-ttu-id="61f3b-144">https://Management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="61f3b-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="61f3b-145">**Идентификатор клиента**: необязательно.</span><span class="sxs-lookup"><span data-stu-id="61f3b-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="61f3b-146">Получает значение Hello только в том случае, если необходимо указать каталог hello.</span><span class="sxs-lookup"><span data-stu-id="61f3b-146">hello value is given only when hello directory must be specified.</span></span>

12. <span data-ttu-id="61f3b-147">После успешного входа с учетной записью Azure стека hello левой заполняется hello Azure стека подписок, связанных с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="61f3b-147">After you successfully sign in with an Azure Stack account, hello left pane is populated with hello Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="61f3b-148">Выберите подписки Azure стека hello, toowork с и затем выберите **применить**.</span><span class="sxs-lookup"><span data-stu-id="61f3b-148">Select hello Azure Stack subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="61f3b-149">(Установив или сняв hello **все подписки** переключает флажок, если выбрать все или ни один из hello в списке подписок Azure стека.)</span><span class="sxs-lookup"><span data-stu-id="61f3b-149">(Selecting or clearing hello **All subscriptions** check box toggles selecting all or none of hello listed Azure Stack subscriptions.)</span></span>

    ![Выберите подписки Azure стека hello после заполнения диалогового окна пользовательского облачной среде hello][30]  
    <span data-ttu-id="61f3b-151">Hello левая панель содержит учетные записи хранения hello, связанные с подписками Azure стека hello выбран.</span><span class="sxs-lookup"><span data-stu-id="61f3b-151">hello left pane displays hello storage accounts associated with hello selected Azure Stack subscriptions.</span></span>

    ![Список учетных записей хранения, включая учетные записи подписки Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="61f3b-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61f3b-153">Next steps</span></span>
* [<span data-ttu-id="61f3b-154">Приступая к работе с обозреватель хранилищ (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="61f3b-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="61f3b-155">Хранилища Azure стека: различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="61f3b-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="61f3b-156">toolearn Дополнительные сведения о хранилище Azure в разделе [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="61f3b-156">toolearn more about Azure Storage, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
