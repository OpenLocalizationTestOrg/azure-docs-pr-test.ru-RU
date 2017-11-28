---
title: "aaaAzure список учетных записей хранения"
description: "Управление параметров учетной записи хранилища с помощью hello набора средств Azure для Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="8e3e6-103">Список учетных записей хранения Azure</span><span class="sxs-lookup"><span data-stu-id="8e3e6-103">Azure Storage Account List</span></span>
<span data-ttu-id="8e3e6-104">Включение учетных записей хранилища Azure Загрузите toobe расположения, используемые для JDK, сервера приложений и произвольных компонентов, а также для хранения состояния при использовании кэширования.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="8e3e6-105">Eclipse ведет список известных учетных записей хранения, доступные tooyour проектов в рабочей области Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="8e3e6-106">tooopen hello **учетные записи хранения** отправной точкой является используется toomanage, список, в Eclipse, щелкните **окна**, нажмите кнопку **предпочтения**, разверните **Azure** , а затем нажмите кнопку **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="8e3e6-107">Hello ниже показан hello **учетные записи хранения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="8e3e6-108">Это диалоговое окно можно также открыть из **учетные записи** ссылку в диалоговых окнах, использующих учетные записи хранения, например hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8e3e6-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="8e3e6-109">Hello **JDK** вкладка hello **конфигурации сервера** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="8e3e6-110">Hello **сервера** вкладка hello **конфигурации сервера** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="8e3e6-111">Hello **добавить компонент** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="8e3e6-112">Hello **кэширование** диалоговое окно свойств.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="8e3e6-113">tooimport хранилищем учетных записей с помощью файла параметров публикации</span><span class="sxs-lookup"><span data-stu-id="8e3e6-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="8e3e6-114">В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **импорта данных из файла параметров публикации**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="8e3e6-115">(Пропустите этот шаг при сохранении публикации параметров файла tooyour локальном компьютере.) В hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку **загрузить файл параметров публикации**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="8e3e6-116">Если вы еще не выполнили вход в учетную запись Azure, появится запрос toolog в.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="8e3e6-117">Затем вам будет предложено toosave Azure файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="8e3e6-118">(Можно игнорировать hello инструкции, приведенные на страницах входа hello - они предоставляются hello портал Azure и предназначены для пользователей Visual Studio.) Сохраните tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="8e3e6-119">По-прежнему в hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку hello **Обзор** кнопку, выберите hello опубликовать файл параметров, который ранее сохранили локально и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="8e3e6-120">Нажмите кнопку **ОК** tooclose hello **Импорт сведений о подписке** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="8e3e6-121">toocreate новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="8e3e6-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="8e3e6-122">В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="8e3e6-123">В рамках hello **добавления учетной записи хранения** диалоговое окно, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="8e3e6-124">В рамках hello **новой учетной записи хранения** диалогового окна, укажите значения для следующего hello:</span><span class="sxs-lookup"><span data-stu-id="8e3e6-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="8e3e6-125">имя учетной записи хранения;</span><span class="sxs-lookup"><span data-stu-id="8e3e6-125">Storage account name.</span></span>

   * <span data-ttu-id="8e3e6-126">Расположение учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="8e3e6-127">Описание учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="8e3e6-128">Учетная запись хранения Hello подписки toowhich hello принадлежит.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="8e3e6-129">Нажмите кнопку **ОК** tooclose hello **новой учетной записи хранения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="8e3e6-130">Он может занять несколько минут для создания учетной записи toobe вашего хранилища система.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="8e3e6-131">После его создания, нажмите кнопку **ОК** tooclose hello **добавления учетной записи хранения** диалоговое окно и учетной записи хранилища будут добавлены toohello список доступных учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="8e3e6-132">tooadd существующего списка toohello учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="8e3e6-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="8e3e6-133">Если вы еще нет учетной записи, создайте его с хранилища Azure hello действий перечислены в hello **toocreate новый раздел учетной записи хранилища** выше.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="8e3e6-134">(Кроме того, можно создать новую учетную запись хранения в hello [портала управления Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="8e3e6-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="8e3e6-135">В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="8e3e6-136">В рамках hello **добавления учетной записи хранения** диалоговое окно, введите значения для **имя** и **ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="8e3e6-137">Hello учетной записи имя и ключ доступа должен быть существующей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="8e3e6-138">Используйте hello **хранения** раздел hello [портала управления Azure] [ Azure Management Portal] tooview вашей учетной записи хранения имен и ключей.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="8e3e6-139">Ваш **добавления учетной записи хранения** диалоговое окно будет выглядеть аналогично toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="8e3e6-140">Нажмите кнопку **ОК** tooclose hello **добавления учетной записи хранения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="8e3e6-141">toomodify toouse учетной записи хранилища новый ключ доступа</span><span class="sxs-lookup"><span data-stu-id="8e3e6-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="8e3e6-142">В рамках hello **учетные записи хранения** диалоговое окно, выберите учетную запись хранилища hello tooedit и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="8e3e6-143">В рамках hello **изменения ключа доступа учетной записи хранения** диалогового окна, изменения hello **ключ доступа** значение.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="8e3e6-144">Нажмите кнопку **ОК** tooclose hello **изменения ключа доступа учетной записи хранения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="8e3e6-145">tooremove учетную запись хранилища из списка hello, поддерживаемого в Eclipse</span><span class="sxs-lookup"><span data-stu-id="8e3e6-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="8e3e6-146">В рамках hello **учетные записи хранения** диалоговое окно, выберите учетную запись хранилища hello tooedit и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="8e3e6-147">Нажмите кнопку **ОК** при запрашиваемые tooremove hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="8e3e6-148">Удаление учетной записи хранения hello через hello **учетные записи хранения** диалогового окна удаляется только из hello список учетных записей хранения, можно просмотреть в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="8e3e6-149">Не удаляет hello учетной записи хранилища из подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="8e3e6-150">Кроме того учетной записи хранилища hello может снова появиться в списке после Eclipse перезагрузит hello сведения о вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="8e3e6-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="8e3e6-151">См. также</span><span class="sxs-lookup"><span data-stu-id="8e3e6-151">See Also</span></span>
<span data-ttu-id="8e3e6-152">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e3e6-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="8e3e6-153">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e3e6-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="8e3e6-154">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e3e6-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="8e3e6-155">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="8e3e6-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
