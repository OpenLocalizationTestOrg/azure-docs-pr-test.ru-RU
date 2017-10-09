---
title: "такие же возможности Office 365 на любом устройстве с Azure RemoteApp hello aaaGet | Документы Microsoft"
description: "Узнайте, как tooshare любое приложение Office 365 с пользователями с помощью Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="d672d-103">Get hello же взаимодействие с Office 365 на любом устройстве с Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d672d-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d672d-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d672d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d672d-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="d672d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d672d-106">В этой статье рассматривается как toodeploy Office 365 на любом устройстве вашей компании.</span><span class="sxs-lookup"><span data-stu-id="d672d-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="d672d-107">Пользователи могут получать hello те же возможности и пользовательского интерфейса experience на Android, Apple и Windows.</span><span class="sxs-lookup"><span data-stu-id="d672d-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="d672d-108">Это достигается с помощью платформы Azure RemoteApp — она позволяет размещать Office 365 на масштабируемых виртуальных машинах Azure, к которым подключаются пользователи.</span><span class="sxs-lookup"><span data-stu-id="d672d-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="d672d-109">Такой набор виртуальных машин называется «облачной коллекцией».</span><span class="sxs-lookup"><span data-stu-id="d672d-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="d672d-110">Создание облачной коллекции</span><span class="sxs-lookup"><span data-stu-id="d672d-110">Create a cloud collection</span></span>
<span data-ttu-id="d672d-111">После создания учетной записи Azure пройти слишком**RemoteApp** , щелкнув ссылку hello на hello слева.</span><span class="sxs-lookup"><span data-stu-id="d672d-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="d672d-112">![Отображение на портале Azure hello Azure RemoteApp](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="d672d-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="d672d-113">Затем продолжить, щелкнув **новый** на нижней hello и «быстрое создание» коллекции.</span><span class="sxs-lookup"><span data-stu-id="d672d-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="d672d-114">Укажите имя, регион hello, hello подписки, план hello и образ hello «Proffesional Office 2013», который мы предоставляем.</span><span class="sxs-lookup"><span data-stu-id="d672d-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="d672d-115">![Создание диалогового окна](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="d672d-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="d672d-116">После завершения процесса создания коллекции hello формы hello должна начаться.</span><span class="sxs-lookup"><span data-stu-id="d672d-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="d672d-117">Это может занять tooan часа.</span><span class="sxs-lookup"><span data-stu-id="d672d-117">This may take up tooan hour or so.</span></span>

![Waiting](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="d672d-119">После завершения процесса hello, он будет выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d672d-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="d672d-120">Если щелкнуть **Публикация**, вы увидите, что основная часть приложений Office уже опубликована.</span><span class="sxs-lookup"><span data-stu-id="d672d-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="d672d-121">![Созданная коллекция](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="d672d-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Опубликованные приложения](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="d672d-123">На этом этапе можно добавить несколько пользователей, имеющих коллекции toothis доступа, нажав кнопку **доступа пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d672d-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="d672d-124">![настройка доступа пользователей](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="d672d-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="d672d-125">Теперь давайте испытать подключение tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="d672d-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="d672d-126">Подключение tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="d672d-126">Connect tooOffice 365</span></span>
<span data-ttu-id="d672d-127">Мы будем перейдите слишком[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), прокрутите список вниз и нажмите кнопку **загрузить клиенты** tooinstall hello Azure RemoteApp клиента на устройстве hello, вы работаете.</span><span class="sxs-lookup"><span data-stu-id="d672d-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="d672d-128">снимки экрана приветствия ниже предназначены для Windows.</span><span class="sxs-lookup"><span data-stu-id="d672d-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="d672d-129">После запуска приложения hello запрашивается toosign учетной записью Майкрософт (ранее называвшиеся «Live ID»), используйте hello того же, как учетная запись Azure сейчас.</span><span class="sxs-lookup"><span data-stu-id="d672d-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="d672d-130">Выполнив вход, вы увидите уведомление о новых приглашениях, щелкнув которое, вы откроете список представленного ниже вида.</span><span class="sxs-lookup"><span data-stu-id="d672d-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="d672d-131">Примите приглашение hello, соответствующий вашей электронной почты владельца учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="d672d-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Новое приглашение](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="d672d-133">Экран с новыми приглашениями.</span><span class="sxs-lookup"><span data-stu-id="d672d-133">What it looks like when there are new invitations.</span></span>

![Принятие приглашения](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="d672d-135">После принятия приглашения hello вы увидите все приложения Office hello в клиенте hello Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d672d-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Список приложений](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="d672d-137">При нажатии кнопки на любом из этих приложений, hello следует запустить на hello виртуальной машины Azure и должно быть задано!</span><span class="sxs-lookup"><span data-stu-id="d672d-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="d672d-138">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="d672d-138">Enjoy!</span></span>

![запуск](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

