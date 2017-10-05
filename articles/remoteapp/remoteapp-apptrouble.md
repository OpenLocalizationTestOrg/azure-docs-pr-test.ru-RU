---
title: "Устранение неполадок Azure RemoteApp — ошибки запуска и подключения приложений | Документация Майкрософт"
description: "Узнайте, как устранять неполадки при запуске и подключении к приложениям в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fc9d538991adce7fc13e9654b9a7c6d113d03fde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="5e7a5-103">Устранение неполадок Azure RemoteApp — ошибки запуска и подключения приложений</span><span class="sxs-lookup"><span data-stu-id="5e7a5-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5e7a5-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5e7a5-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="5e7a5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5e7a5-106">Ошибки запуска приложений, размещенных в Azure RemoteApp, могут возникать по разным причинам.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span></span> <span data-ttu-id="5e7a5-107">В этой статье описывается ряд причин и приводятся сообщения об ошибках, которые могут получать пользователи во время запуска приложений.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span></span> <span data-ttu-id="5e7a5-108">Здесь также рассматриваются сбои подключения.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-108">It also talks about connection failures.</span></span> <span data-ttu-id="5e7a5-109">(Однако в этой статье не описываются проблемы, связанные со входом в клиент Azure RemoteApp.)</span><span class="sxs-lookup"><span data-stu-id="5e7a5-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span></span>  

<span data-ttu-id="5e7a5-110">Ознакомьтесь со сведениями о распространенных ошибках, связанных со сбоями запуска и подключения приложений.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-110">Read on for information about common error messages due to app launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="5e7a5-111">Выполняется настройка... Повторите попытку через 10 минут.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="5e7a5-112">Эта ошибка означает, что RemoteApp Azure увеличивает свой масштаб для удовлетворения потребностей пользователей в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span></span> <span data-ttu-id="5e7a5-113">Для этого в фоновом режиме создаются дополнительные экземпляры виртуальных машин RemoteApp Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span></span> <span data-ttu-id="5e7a5-114">Обычно процесс занимает около пяти минут, но он может продолжаться и до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-114">Typically this takes around five minutes but can take up to 10 minutes.</span></span> <span data-ttu-id="5e7a5-115">В некоторых случаях это происходит не так уж быстро, а ресурсы нужны немедленно.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="5e7a5-116">Примером является сценарий "9:00", когда доступ к вашему приложению в Azure RemoteApp требуется большому количеству пользователей одновременно.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span></span> <span data-ttu-id="5e7a5-117">В этом случае мы можем включить **режим увеличения объема ресурсов** на внутреннем сервере.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-117">If this happens to you we can enable **capacity mode** on the back end.</span></span> <span data-ttu-id="5e7a5-118">Для этого отправьте запрос в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-118">To do this open an Azure Support ticket.</span></span> <span data-ttu-id="5e7a5-119">Не забудьте указать в запросе свой идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-119">Be certain to include your subscription ID in the request.</span></span>  

![Выполняется настройка](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a><span data-ttu-id="5e7a5-121">Не удается автоматически повторно подключиться к вашим приложениям. Запустите приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-121">Could not auto-reconnect to your applications, please re-launch your application</span></span>
<span data-ttu-id="5e7a5-122">Это сообщение об ошибке часто отображается, если вы использовали Azure RemoteApp, а затем перевели ПК в спящий режим больше чем на 4 часа, и после этого вывели ПК из спящего режима. Клиент Azure RemoteApp пытался автоматически повторно подключиться, но время ожидания было превышено.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="5e7a5-123">Попросите пользователей вернуться в приложение и попытаться открыть его из клиента Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span></span>

![Не удалось автоматически повторно подключиться к вашим приложениям.](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a><span data-ttu-id="5e7a5-125">Проблемы с временным профилем</span><span class="sxs-lookup"><span data-stu-id="5e7a5-125">Problems with the temp profile</span></span>
<span data-ttu-id="5e7a5-126">Эта ошибка возникает, если не удалось подключить профиль пользователя (диск профиля пользователя) и пользователь получил временный профиль.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span></span>  <span data-ttu-id="5e7a5-127">Администраторы должны перейти к коллекции на портале Azure, открыть вкладку **Сеансы** и попытаться **вывести** пользователя из системы.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span></span> <span data-ttu-id="5e7a5-128">Будет осуществлен принудительный выход из сеанса, после чего пользователь должен попытаться запустить приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span></span> <span data-ttu-id="5e7a5-129">В случае неудачи обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="5e7a5-130">Прекращена работа Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5e7a5-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="5e7a5-131">Это сообщение об ошибке означает, что в клиенте Azure RemoteApp возникли неполадки и он должен быть перезапущен.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span></span> <span data-ttu-id="5e7a5-132">Попросите пользователей нажать кнопку **Закрыть программу** , а затем снова запустить клиент Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span></span>  <span data-ttu-id="5e7a5-133">Если проблема не исчезнет, отправьте запрос в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-133">If the issue continues open and Azure Support ticket.</span></span>

![Прекращена работа Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a><span data-ttu-id="5e7a5-135">Возникла ошибка при доступе к этому ресурсу через подключение к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="5e7a5-136">Повторите попытку подключения или обратитесь к системному администратору</span><span class="sxs-lookup"><span data-stu-id="5e7a5-136">Retry the connection or contact your system administrator</span></span>
<span data-ttu-id="5e7a5-137">Это общее сообщение об ошибке — обратитесь в службу поддержки Azure, чтобы мы могли разобраться в причинах ошибки.</span><span class="sxs-lookup"><span data-stu-id="5e7a5-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![Общее сообщение Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

