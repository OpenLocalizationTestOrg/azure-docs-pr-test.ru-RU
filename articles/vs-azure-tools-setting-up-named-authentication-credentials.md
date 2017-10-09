---
title: "aaaSetting копии с именем учетные данные проверки подлинности | Документы Microsoft"
description: "Узнайте, как учетные данные tootooprovide, Visual Studio можно использовать tooauthenticate запросов tooAzure toopublish tooAzure приложения из Visual Studio или toomonitor существующую облачную службу... "
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
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="fe13f-103">Настройка именованных учетных данных для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="fe13f-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="fe13f-104">toopublish tooAzure приложения из Visual Studio или toomonitor существующую облачную службу, необходимо предоставить учетные данные, Visual Studio можно использовать tooauthenticate запрашивает tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe13f-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="fe13f-105">Есть несколько мест в Visual Studio, в которой можно войти в tooprovide эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fe13f-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="fe13f-106">Например, из hello обозреватель серверов, можно открыть контекстное меню hello hello **Azure** узел и выберите **подключения tooMicrosoft подписки Azure...** . При входе в сведения о подписке hello, связанный с учетной записью Azure доступен в Visual Studio и больше у вас есть toodo нечего.</span><span class="sxs-lookup"><span data-stu-id="fe13f-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="fe13f-107">Средства Azure также поддерживают прежний способ указания учетных данных, с помощью hello подписки (файл .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="fe13f-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="fe13f-108">В этой статье описывается способ, который все еще поддерживается в пакете Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="fe13f-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="fe13f-109">для проверки подлинности tooAzure необходимы Hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="fe13f-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="fe13f-110">идентификатор подписки;</span><span class="sxs-lookup"><span data-stu-id="fe13f-110">Your subscription ID</span></span>
* <span data-ttu-id="fe13f-111">действительный сертификат X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="fe13f-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="fe13f-112">Длина ключа сертификата X.509 v3 hello Hello должна быть не меньше 2048 бит.</span><span class="sxs-lookup"><span data-stu-id="fe13f-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="fe13f-113">Azure отклонит любой недействительный сертификат или сертификат, не соответствующий этому требованию.</span><span class="sxs-lookup"><span data-stu-id="fe13f-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="fe13f-114">Visual Studio использует идентификатор подписки вместе с данными сертификата hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fe13f-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="fe13f-115">Hello соответствующие учетные данные указываются в файле hello подписки (PUBLISHSETTINGS-файл), содержащий открытый ключ для сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="fe13f-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="fe13f-116">Hello файл подписки может содержать учетные данные для более чем одной подписке.</span><span class="sxs-lookup"><span data-stu-id="fe13f-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="fe13f-117">Можно изменить сведения о подписках hello hello **Создание или изменение подписки** диалоговое окно, как описано далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="fe13f-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="fe13f-118">Если вы хотите toocreate сертификат самостоятельно, можно ссылаться инструкциям toohello [Создание и отправка сертификата управления для Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) , а затем вручную Загрузите сертификат toohello hello [классический портал Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="fe13f-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="fe13f-119">Эти учетные данные, которые Visual Studio требуется toomanage, которые не являются облачными службами hello же учетные данные, которые требуется tooauthenticate запроса к службам хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fe13f-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="fe13f-120">Импорт, настройка или изменение учетных данных для аутентификации в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe13f-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="fe13f-121">Можно импортировать, настроить или изменить учетные данные проверки подлинности в hello **новую подписку** диалоговое окно открывается при выполнении hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fe13f-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="fe13f-122">В **обозревателя серверов**, откройте контекстное меню hello hello **Azure** узел, выберите **управление подписками и их фильтрация...** , выберите hello **сертификаты** , и выполните одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="fe13f-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="fe13f-123">Выберите **импорта** tooopen диалоговое окно Импорт подписок Microsoft Azure hello где можно загрузить файл подписки hello для hello в данный момент загружены подписки, обзора tooits расположения загрузки, а затем импортируйте его для использования в Проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="fe13f-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="fe13f-124">Выберите **New** tooopen диалоговое окно новой подписки hello где можно настроить новую подписку для использования при проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="fe13f-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="fe13f-125">Выберите **изменить** (выбрав своей активной подписке) tooopen диалоговое окно Изменение подписки hello где можно изменить существующую подписку для использования при проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="fe13f-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="fe13f-126">Hello следующей процедуре предполагается, что hello **новую подписку** используется диалоговое окно открытым.</span><span class="sxs-lookup"><span data-stu-id="fe13f-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="fe13f-127">tooset копирование учетных данных проверки подлинности в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe13f-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="fe13f-128">В hello **выбрать существующий сертификат** список проверки подлинности, выберите сертификат.</span><span class="sxs-lookup"><span data-stu-id="fe13f-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="fe13f-129">Выберите hello **Копировать полный путь hello** ссылку.</span><span class="sxs-lookup"><span data-stu-id="fe13f-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="fe13f-130">путь Hello hello сертификат (CER-файл) — скопированный toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="fe13f-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fe13f-131">toopublish приложения Azure из Visual Studio, необходимо отправить этот сертификат toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fe13f-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="fe13f-132">сертификат toohello hello tooupload портала Azure:</span><span class="sxs-lookup"><span data-stu-id="fe13f-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="fe13f-133">Откройте hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fe13f-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="fe13f-134">Если будет предложено, войдите в портал toohello и перейдите слишком**параметры**, **сертификаты управления**.</span><span class="sxs-lookup"><span data-stu-id="fe13f-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="fe13f-135">Выберите в области управления сертификатами hello **отправить**.</span><span class="sxs-lookup"><span data-stu-id="fe13f-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="fe13f-136">Выберите подписку Azure, вставьте полный путь hello hello CER-файл, который только что создана и выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="fe13f-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
