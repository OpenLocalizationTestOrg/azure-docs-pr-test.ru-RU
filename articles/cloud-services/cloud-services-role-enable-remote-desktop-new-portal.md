---
title: "Активация подключения к удаленному рабочему столу для роли в облачных службах Azure | Документация Майкрософт"
description: "Настройка приложения в облачной службе Azure для удаленного подключения."
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="6f718-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="6f718-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f718-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f718-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="6f718-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f718-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="6f718-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f718-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="6f718-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f718-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="6f718-108">С помощью удаленного рабочего стола обеспечивается доступ к рабочему столу экземпляра, работающего в Azure.</span><span class="sxs-lookup"><span data-stu-id="6f718-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="6f718-109">Подключение к удаленному рабочему столу позволяет диагностировать и устранять неполадки выполняющегося приложения.</span><span class="sxs-lookup"><span data-stu-id="6f718-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="6f718-110">Во время разработки можно разрешить подключения к удаленному рабочему столу для роли, включив модули удаленного рабочего стола в определение службы или включив удаленный рабочий стол с помощью расширения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="6f718-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="6f718-111">Рекомендуется использовать расширение удаленного рабочего стола, так как удаленный рабочий стол можно включить даже после развертывания приложения без необходимости повторного развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="6f718-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="6f718-112">Настройка удаленного рабочего стола на портале Azure</span><span class="sxs-lookup"><span data-stu-id="6f718-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="6f718-113">На портале Azure используется подход с расширением удаленного рабочего стола, поэтому удаленный рабочий стол можно включить даже после развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="6f718-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="6f718-114">В колонке **Удаленный рабочий стол** облачной службы можно включить удаленный рабочий стол, изменить учетную запись локального администратора для подключения к виртуальным машинам, выбрать сертификат для проверки подлинности, а также установить срок его действия.</span><span class="sxs-lookup"><span data-stu-id="6f718-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="6f718-115">Щелкните **Облачные службы**, выберите имя облачной службы, а затем — **Удаленный рабочий стол**.</span><span class="sxs-lookup"><span data-stu-id="6f718-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="6f718-117">Включите удаленный рабочий стол для отдельной или для всех ролей, а затем установите переключатель в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="6f718-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="6f718-118">Введите в соответствующих полях имя пользователя, пароль, срок действия и сертификат.</span><span class="sxs-lookup"><span data-stu-id="6f718-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="6f718-120">Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="6f718-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="6f718-121">Если в роли установлен сертификат для шифрования пароля, перезапуск не производится.</span><span class="sxs-lookup"><span data-stu-id="6f718-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="6f718-122">Чтобы не выполнять перезапуск, [загрузите сертификат для облачной службы](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) и вернитесь в диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6f718-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="6f718-123">В разделе **Роли** выберите роль, которую требуется обновить, или щелкните **Все**, чтобы задать все роли.</span><span class="sxs-lookup"><span data-stu-id="6f718-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="6f718-124">По завершении обновления настроек нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6f718-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="6f718-125">Активация возможности принимать подключения для роли может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6f718-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="6f718-126">Удаленное подключение к экземплярам ролей</span><span class="sxs-lookup"><span data-stu-id="6f718-126">Remote into role instances</span></span>
<span data-ttu-id="6f718-127">После включения удаленного рабочего стола для роли вы можете инициировать подключение непосредственно с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6f718-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="6f718-128">Щелкните **Экземпляры**, чтобы открыть колонку **Экземпляры**.</span><span class="sxs-lookup"><span data-stu-id="6f718-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="6f718-129">Выберите экземпляр роли, где настроен удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="6f718-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="6f718-130">Щелкните **Подключиться**, чтобы скачать RDP-файл для экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="6f718-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="6f718-132">Щелкните **Открыть**, а затем — **Подключить**, чтобы установить подключение к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="6f718-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="6f718-133">Если облачная служба защищена NSG, может потребоваться создать правила, разрешающие передачу трафика через порты **3389** и **20000**.</span><span class="sxs-lookup"><span data-stu-id="6f718-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="6f718-134">Удаленный рабочий стол использует порт **3389**.</span><span class="sxs-lookup"><span data-stu-id="6f718-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="6f718-135">В экземплярах облачной службы реализована балансировка нагрузки, поэтому вы не можете напрямую управлять подключением к экземпляру.</span><span class="sxs-lookup"><span data-stu-id="6f718-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="6f718-136">Агенты *RemoteForwarder* и *RemoteAccess* управляют трафиком RDP и позволяют клиенту отправлять файлы cookie по RDP и указывать отдельный экземпляр для подключения.</span><span class="sxs-lookup"><span data-stu-id="6f718-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="6f718-137">Агентам *RemoteForwarder* и *RemoteAccess* требуется, чтобы порт **20000*** был открыт. При использовании группы безопасности сети он может быть заблокирован.</span><span class="sxs-lookup"><span data-stu-id="6f718-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f718-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6f718-138">Additional resources</span></span>

<span data-ttu-id="6f718-139">[Настройка облачных служб](cloud-services-how-to-configure.md)
[Часто задаваемые вопросы об облачных службах](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6f718-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
