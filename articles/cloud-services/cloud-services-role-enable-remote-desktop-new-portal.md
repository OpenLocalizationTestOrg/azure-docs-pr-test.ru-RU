---
title: "aaaEnable подключение к удаленному рабочему столу для роли в облачных службах Azure | Документы Microsoft"
description: "Как tooconfigure azure облачной службы подключения удаленного рабочего стола tooallow приложения"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="6f631-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="6f631-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f631-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f631-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="6f631-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f631-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="6f631-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f631-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="6f631-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f631-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="6f631-108">Удаленный рабочий стол позволяет tooaccess hello системной роли, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="6f631-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="6f631-109">Можно использовать tootroubleshoot подключения удаленного рабочего стола и диагностировать проблемы с приложением во время его выполнения.</span><span class="sxs-lookup"><span data-stu-id="6f631-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="6f631-110">Можно включить удаленный рабочий стол в данной роли во время разработки, включая модули, удаленный рабочий стол hello в определении службы или вы можете tooenable удаленного рабочего стола через hello расширения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="6f631-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="6f631-111">Hello рекомендуется расширение удаленного рабочего стола hello toouse как можно включить удаленный рабочий стол, даже после развертывания приложения hello без необходимости tooredeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="6f631-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="6f631-112">Настроить удаленный рабочий стол из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f631-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="6f631-113">Hello портал Azure использует подход hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, даже после развертывания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6f631-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="6f631-114">Hello **удаленного рабочего стола** колонку для облачной службы позволяет tooenable удаленного рабочего стола, изменение hello локальную учетную запись администратора используется tooconnect toohello виртуальных машин, сертификат hello, используемые в проверке подлинности и задайте hello Дата окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="6f631-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="6f631-115">Нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="6f631-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="6f631-117">Выберите ли вы хотите tooenable удаленного рабочего стола для отдельных ролей или для всех ролей, а затем измените значение hello переключателя hello слишком**включено**.</span><span class="sxs-lookup"><span data-stu-id="6f631-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="6f631-118">Заполните поля hello требуется имя пользователя, пароль, срок действия и сертификата.</span><span class="sxs-lookup"><span data-stu-id="6f631-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="6f631-120">Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="6f631-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="6f631-121">tooprevent перезагрузки пароль hello hello сертификата используется tooencrypt должен устанавливаться на роли hello.</span><span class="sxs-lookup"><span data-stu-id="6f631-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="6f631-122">tooprevent перезагрузки [отправка сертификата для облачной службы hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , а затем возвращают toothis диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6f631-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="6f631-123">В **ролей**, выберите роль hello tooupdate или выберите **все** для всех ролей.</span><span class="sxs-lookup"><span data-stu-id="6f631-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="6f631-124">По завершении обновления настроек нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6f631-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="6f631-125">Может занять несколько минут, прежде чем экземпляры ролей готовы tooreceive подключений.</span><span class="sxs-lookup"><span data-stu-id="6f631-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="6f631-126">Удаленное подключение к экземплярам ролей</span><span class="sxs-lookup"><span data-stu-id="6f631-126">Remote into role instances</span></span>
<span data-ttu-id="6f631-127">После включения удаленного рабочего стола с ролями hello может инициировать подключение непосредственно из hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="6f631-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="6f631-128">Нажмите кнопку **экземпляров** tooopen hello **экземпляров** колонку.</span><span class="sxs-lookup"><span data-stu-id="6f631-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="6f631-129">Выберите экземпляр роли, где настроен удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="6f631-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="6f631-130">Нажмите кнопку **Connect** toodownload RDP-файла для экземпляра роли hello.</span><span class="sxs-lookup"><span data-stu-id="6f631-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="6f631-132">Нажмите кнопку **откройте** и затем **Connect** toostart hello подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="6f631-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="6f631-133">Если облачная служба находится на расстоянии за NSG, может потребоваться toocreate правила, разрешающие трафик через порты **3389** и **20000**.</span><span class="sxs-lookup"><span data-stu-id="6f631-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="6f631-134">Удаленный рабочий стол использует порт **3389**.</span><span class="sxs-lookup"><span data-stu-id="6f631-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="6f631-135">Экземпляров облачной службы, распределяются, поэтому не может напрямую управлять какой экземпляр tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="6f631-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="6f631-136">Hello *RemoteForwarder* и *RemoteAccess* агенты управления трафиком протокола удаленного рабочего СТОЛА и разрешить toosend клиента hello куки-файл протокола удаленного рабочего СТОЛА и tooconnect отдельного экземпляра, чтобы указать.</span><span class="sxs-lookup"><span data-stu-id="6f631-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="6f631-137">Hello *RemoteForwarder* и *RemoteAccess* агенты имеют этот порт **20000*** открыть, который может блокироваться, если у вас есть NSG.</span><span class="sxs-lookup"><span data-stu-id="6f631-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f631-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6f631-138">Additional resources</span></span>

<span data-ttu-id="6f631-139">[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6f631-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
