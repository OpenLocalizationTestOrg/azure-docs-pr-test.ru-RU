---
title: "Список учетных записей хранения Azure"
description: "Управление параметрами учетной записи хранения с помощью набора средств Azure для Eclipse"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="12259-103">Список учетных записей хранения Azure</span><span class="sxs-lookup"><span data-stu-id="12259-103">Azure Storage Account List</span></span>
<span data-ttu-id="12259-104">Учетные записи хранения Azure позволяют использовать расположения скачивания для JDK, сервера приложений и произвольных компонентов, а также для хранения состояния при использовании кэширования.</span><span class="sxs-lookup"><span data-stu-id="12259-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="12259-105">Eclipse ведет список известных учетных записей хранения, доступных вашим проектам в рабочей области Eclipse.</span><span class="sxs-lookup"><span data-stu-id="12259-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="12259-106">Чтобы открыть диалоговое окно **Учетные записи хранения**, которое используется для управления этим списком, в Eclipse щелкните **Окно**, **Настройки**, разверните узел **Azure** и выберите **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="12259-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="12259-107">Ниже показано диалоговое окно **Учетные записи хранения** .</span><span class="sxs-lookup"><span data-stu-id="12259-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="12259-108">Кроме того, это диалоговое окно можно открыть с помощью ссылки **Учетные записи** в диалоговых окнах, использующих учетные записи хранения, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="12259-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="12259-109">Вкладка **JDK** диалогового окна **Конфигурация сервера**.</span><span class="sxs-lookup"><span data-stu-id="12259-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="12259-110">Вкладка **Сервер** диалогового окна **Конфигурация сервера**.</span><span class="sxs-lookup"><span data-stu-id="12259-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="12259-111">Диалоговое окно **Добавить компонент** .</span><span class="sxs-lookup"><span data-stu-id="12259-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="12259-112">Диалоговое окно свойств **Кэширование** .</span><span class="sxs-lookup"><span data-stu-id="12259-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="12259-113">Импорт учетных записей хранения с помощью файла параметров публикации</span><span class="sxs-lookup"><span data-stu-id="12259-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="12259-114">В диалоговом окне **Учетные записи хранения** щелкните **Import from PUBLISH-SETTINGS file** (Импорт из PUBLISHSETTINGS-файла).</span><span class="sxs-lookup"><span data-stu-id="12259-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="12259-115">(Пропустите этот шаг, если вы уже сохранили файл параметров публикации на локальном компьютере.) В диалоговом окне **Import Subscription Information** (Импорт сведений о подписке) щелкните **Download PUBLISH-SETTINGS File** (Скачать PUBLISHSETTINGS-файл).</span><span class="sxs-lookup"><span data-stu-id="12259-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="12259-116">Если вы еще не вошли в учетную запись Azure, вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="12259-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="12259-117">Затем вам будет предложено сохранить файл параметров публикации Azure.</span><span class="sxs-lookup"><span data-stu-id="12259-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="12259-118">(Вы можете игнорировать инструкции, приведенные на страницах входа в систему, так как они предоставляются порталом Azure и предназначены для пользователей Visual Studio.) Сохраните его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="12259-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="12259-119">В диалоговом окне **Import Subscription Information** (Импорт сведений о подписке) нажмите кнопку **Обзор**, выберите файл параметров публикации, сохраненный ранее локально, и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="12259-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="12259-120">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Import Subscription Information** (Импорт сведений о подписке).</span><span class="sxs-lookup"><span data-stu-id="12259-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="12259-121">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="12259-121">To create a new storage account</span></span>
1. <span data-ttu-id="12259-122">В диалоговом окне **Учетные записи хранения** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="12259-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="12259-123">В диалоговом окне **Добавление учетной записи хранения** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="12259-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="12259-124">В диалоговом окне **Создать учетную запись хранения** укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="12259-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="12259-125">имя учетной записи хранения;</span><span class="sxs-lookup"><span data-stu-id="12259-125">Storage account name.</span></span>

   * <span data-ttu-id="12259-126">расположение учетной записи хранения;</span><span class="sxs-lookup"><span data-stu-id="12259-126">Location of the storage account.</span></span>

   * <span data-ttu-id="12259-127">описание учетной записи хранения;</span><span class="sxs-lookup"><span data-stu-id="12259-127">Description of the storage account.</span></span>

   * <span data-ttu-id="12259-128">подписка, к которой относится учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="12259-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="12259-129">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="12259-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="12259-130">Создание вашей учетной записи хранения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="12259-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="12259-131">После ее создания нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление учетной записи хранения**. Новая учетная запись хранения добавится в список доступных учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="12259-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="12259-132">Добавление существующей учетной записи хранения в список</span><span class="sxs-lookup"><span data-stu-id="12259-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="12259-133">Если у вас еще нет учетной записи хранения Azure, создайте ее, выполнив действия, описанные в приведенном выше разделе **Создание учетной записи хранения** .</span><span class="sxs-lookup"><span data-stu-id="12259-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="12259-134">(Кроме того, вы можете создать учетную запись хранения с помощью [портала управления Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="12259-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="12259-135">В диалоговом окне **Учетные записи хранения** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="12259-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="12259-136">В диалоговом окне **Добавление учетной записи хранения** введите значения для параметров **Имя** и **Ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="12259-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="12259-137">Имя и ключ доступа должны относиться к существующей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="12259-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="12259-138">Используйте раздел **Хранилище**[портала управления Azure][Azure Management Portal], чтобы просмотреть имена и ключи своих учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="12259-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="12259-139">Диалоговое окно **Добавление учетной записи хранения** будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="12259-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="12259-140">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="12259-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="12259-141">Изменение учетной записи хранения для использования нового ключа доступа</span><span class="sxs-lookup"><span data-stu-id="12259-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="12259-142">В диалоговом окне **Учетные записи хранения** щелкните учетную запись хранения, которую требуется изменить, и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="12259-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="12259-143">В диалоговом окне **Edit Storage Account Access Key** (Изменение ключа доступа учетной записи хранения) измените значение **Ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="12259-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="12259-144">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Edit Storage Account Access Key** (Изменение ключа доступа учетной записи хранения).</span><span class="sxs-lookup"><span data-stu-id="12259-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="12259-145">Удаление учетной записи хранения из списка, хранящегося в Eclipse</span><span class="sxs-lookup"><span data-stu-id="12259-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="12259-146">В диалоговом окне **Учетные записи хранения** щелкните учетную запись хранения, которую требуется изменить, и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="12259-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="12259-147">Нажмите кнопку **ОК** при появлении запроса на удаление учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="12259-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="12259-148">При удалении учетной записи хранения через диалоговое окно **Учетные записи хранения** она удаляется лишь из списка учетных записей хранения, который можно просмотреть в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="12259-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="12259-149">Сама учетная запись из подписки Azure не удаляется.</span><span class="sxs-lookup"><span data-stu-id="12259-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="12259-150">Кроме того, учетная запись хранения может снова появиться в списке, после того как Eclipse перезагрузит сведения о подписке.</span><span class="sxs-lookup"><span data-stu-id="12259-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="12259-151">См. также</span><span class="sxs-lookup"><span data-stu-id="12259-151">See Also</span></span>
<span data-ttu-id="12259-152">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12259-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="12259-153">[Установка набора средств Azure для Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12259-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="12259-154">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12259-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="12259-155">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="12259-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
