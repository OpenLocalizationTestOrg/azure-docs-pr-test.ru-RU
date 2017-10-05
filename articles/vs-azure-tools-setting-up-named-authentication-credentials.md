---
title: "Настройка именованных учетных данных для аутентификации | Документация Майкрософт"
description: "Узнайте, как указать учетные данные, которые Visual Studio сможет использовать для проверки подлинности запросов к Azure, чтобы опубликовать приложение из Visual Studio в Azure или отслеживать существующую облачную службу. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="8210b-103">Настройка именованных учетных данных для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8210b-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="8210b-104">Чтобы опубликовать приложение из Visual Studio в Azure или отслеживать существующую облачную службу, необходимо предоставить учетные данные, которые Visual Studio сможет использовать для проверки подлинности запросов к Azure.</span><span class="sxs-lookup"><span data-stu-id="8210b-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="8210b-105">Эти учетные данные можно указывать в разных разделах Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8210b-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="8210b-106">Например, откройте в обозревателе сервера контекстное меню узла **Azure** и выберите пункт **Подключиться к подписке Microsoft Azure**. Когда вы входите в систему, сведения о подписке, связанные с учетной записью Azure, становятся доступными в Visual Studio, поэтому больше ничего делать не нужно.</span><span class="sxs-lookup"><span data-stu-id="8210b-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="8210b-107">Инструменты Azure также поддерживают прежний способ предоставления учетных данных с помощью файла подписки (файла PUBLISHSETTINGS).</span><span class="sxs-lookup"><span data-stu-id="8210b-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="8210b-108">В этой статье описывается способ, который все еще поддерживается в пакете Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="8210b-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="8210b-109">Для проверки подлинности в Azure необходимы следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="8210b-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="8210b-110">идентификатор подписки;</span><span class="sxs-lookup"><span data-stu-id="8210b-110">Your subscription ID</span></span>
* <span data-ttu-id="8210b-111">действительный сертификат X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="8210b-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="8210b-112">Длина ключа сертификата X.509 v3 должна составлять как минимум 2048 бит.</span><span class="sxs-lookup"><span data-stu-id="8210b-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="8210b-113">Azure отклонит любой недействительный сертификат или сертификат, не соответствующий этому требованию.</span><span class="sxs-lookup"><span data-stu-id="8210b-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="8210b-114">Visual Studio использует в качестве учетных данных ваш идентификатор подписки и данные сертификата.</span><span class="sxs-lookup"><span data-stu-id="8210b-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="8210b-115">Соответствующие учетные данные указываются в файле подписки (файл PUBLISHSETTINGS), который содержит открытый ключ для сертификата.</span><span class="sxs-lookup"><span data-stu-id="8210b-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="8210b-116">Файл подписки может содержать учетные данные нескольких подписок.</span><span class="sxs-lookup"><span data-stu-id="8210b-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="8210b-117">Вы можете изменить сведения о подписке в диалоговом окне **Создать/Изменить подписку** , как описано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8210b-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="8210b-118">Если вы хотите создать сертификат самостоятельно, следуйте инструкциям в статье [Общие сведения о сертификатах для облачных служб Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) и вручную передайте сертификат на [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="8210b-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="8210b-119">Эти учетные данные, которые требуются Visual Studio для управления облачными службами, не совпадают с учетными данными, необходимыми для проверки подлинности запроса к службам хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8210b-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="8210b-120">Импорт, настройка или изменение учетных данных для аутентификации в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8210b-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="8210b-121">Вы можете импортировать, настроить или изменить учетные данные для аутентификации в диалоговом окне **Новая подписка**, которое появится после выполнения следующего действия:</span><span class="sxs-lookup"><span data-stu-id="8210b-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="8210b-122">В **обозревателе сервера** откройте контекстное меню узла **Azure**, выберите **Управление подписками и их фильтрация...**, затем откройте вкладку **Сертификаты** и выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="8210b-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="8210b-123">Выберите **Импорт**, чтобы открылось диалоговое окно "Импорт подписок Microsoft Azure", в котором можно скачать файл подписок для загруженной в настоящий момент подписки. Перейдите в расположение для скачивания этого файла, а затем импортируйте его для использования при аутентификации.</span><span class="sxs-lookup"><span data-stu-id="8210b-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="8210b-124">Выберите **Создать**, чтобы открылось диалоговое окно "Создание подписки", в котором можно настроить новую подписку для использования при аутентификации.</span><span class="sxs-lookup"><span data-stu-id="8210b-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="8210b-125">Выберите **Изменить** (после того, как выбрали активную подписку), чтобы открылось диалоговое окно "Изменение подписки", в котором можно изменить существующую подписку для использования при аутентификации.</span><span class="sxs-lookup"><span data-stu-id="8210b-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="8210b-126">Следующая процедура предполагает, что диалоговое окно **Новая подписка** открыто.</span><span class="sxs-lookup"><span data-stu-id="8210b-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="8210b-127">Настройка учетных данных для проверки подлинности в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8210b-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="8210b-128">Выберите сертификат в списке **Выберите существующий сертификат для аутентификации** .</span><span class="sxs-lookup"><span data-stu-id="8210b-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="8210b-129">Выберите ссылку **Скопировать полный путь**.</span><span class="sxs-lookup"><span data-stu-id="8210b-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="8210b-130">Путь к сертификату (CER-файлу) будет скопирован в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8210b-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8210b-131">Чтобы опубликовать приложение Azure из Visual Studio, следует передать этот сертификат на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8210b-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="8210b-132">Чтобы передать сертификат на портал Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8210b-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="8210b-133">Откройте [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8210b-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="8210b-134">Если отобразится запрос, войдите на портал и перейдите в раздел **Параметры**, а затем — **Сертификаты управления**.</span><span class="sxs-lookup"><span data-stu-id="8210b-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="8210b-135">В области сертификатов управления выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="8210b-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="8210b-136">Выберите подписку Azure, вставьте полный путь к CER-файлу, который вы только что создали, и выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="8210b-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
