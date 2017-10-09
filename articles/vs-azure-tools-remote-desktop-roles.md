---
title: "aaaUsing удаленного рабочего стола с ролями Azure | Документы Microsoft"
description: "Использование удаленного рабочего стола с ролями Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="09b74-103">Использование удаленного рабочего стола с ролями Azure</span><span class="sxs-lookup"><span data-stu-id="09b74-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="09b74-104">С помощью hello Azure SDK и службы удаленных рабочих столов, можно получить доступ к ролям Azure и виртуальным машинам, размещенным в Azure.</span><span class="sxs-lookup"><span data-stu-id="09b74-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="09b74-105">В Visual Studio можно настроить службы удаленных рабочих столов из проекта облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="09b74-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="09b74-106">Службы удаленных рабочих столов tooenable, следует создать рабочий проект, содержащий одну или несколько ролей, а затем опубликовать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="09b74-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09b74-107">К роли Azure следует обращаться только для разработки или устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="09b74-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="09b74-108">Здравствуйте, назначение каждой виртуальной машины является toorun определенной роли в приложении Azure не toorun других клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="09b74-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="09b74-109">Если вы хотите toouse Azure toohost виртуальной машины, который можно использовать для любых целей, см. доступ к виртуальных машин Azure из обозревателя серверов.</span><span class="sxs-lookup"><span data-stu-id="09b74-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="09b74-110">tooenable и использование удаленного рабочего стола для роли Azure</span><span class="sxs-lookup"><span data-stu-id="09b74-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="09b74-111">В обозревателе решений откройте контекстное меню проекта облачной службы hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="09b74-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="09b74-112">Hello **публикации приложения Azure** откроется окно мастера.</span><span class="sxs-lookup"><span data-stu-id="09b74-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Команда «Опубликовать» для проекта облачной службы](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="09b74-114">Внизу hello **параметры публикации Microsoft Azure** страница приветствия мастера выберите hello **включить удаленный рабочий стол** для всех ролей флажок.</span><span class="sxs-lookup"><span data-stu-id="09b74-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="09b74-115">Hello **конфигурация удаленного рабочего стола** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="09b74-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="09b74-116">Внизу hello hello **конфигурация удаленного рабочего стола** диалогового окна выберите hello **Дополнительно** кнопки.</span><span class="sxs-lookup"><span data-stu-id="09b74-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="09b74-117">Отобразится раскрывающийся список, с помощью которого можно создать или выбрать сертификат, чтобы шифровать учетные данные при подключении через удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="09b74-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="09b74-118">В раскрывающемся списке «hello» выберите  **&lt;Создать >**, или выберите существующий сертификат из списка hello.</span><span class="sxs-lookup"><span data-stu-id="09b74-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="09b74-119">Если выбрать существующий сертификат, пропустите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="09b74-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09b74-120">Hello сертификаты, необходимые для удаленного рабочего стола, отличаются от hello сертификатов, которые используются для работы в Azure.</span><span class="sxs-lookup"><span data-stu-id="09b74-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="09b74-121">Hello удаленного доступа сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="09b74-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="09b74-122">Hello **Create Certificate** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="09b74-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="09b74-123">Введите понятное имя для нового сертификата hello, а затем выберите hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="09b74-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="09b74-124">Появится новый сертификат Hello в hello раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="09b74-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="09b74-125">В hello **конфигурация удаленного рабочего стола** диалогового окна введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="09b74-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="09b74-126">Нельзя использовать существующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="09b74-126">You can’t use an existing account.</span></span> <span data-ttu-id="09b74-127">Не указывайте администратора как hello имя пользователя для новой учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="09b74-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="09b74-128">Если hello пароль не соответствует требованиям сложности hello, далее поле toohello пароля появится красный значок.</span><span class="sxs-lookup"><span data-stu-id="09b74-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="09b74-129">Hello пароль должен содержать прописные буквы, строчные буквы и цифры или символы.</span><span class="sxs-lookup"><span data-stu-id="09b74-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="09b74-130">Выберите дату, на учетную запись, которая hello истекает, и после которого подключения удаленного рабочего стола будут заблокированы.</span><span class="sxs-lookup"><span data-stu-id="09b74-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="09b74-131">После предоставляемых Здравствуйте, все необходимые сведения, выберите hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="09b74-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="09b74-132">Несколько параметров, включите службы удаленного доступа, добавляются в файлах cscfg и csdef toohello.</span><span class="sxs-lookup"><span data-stu-id="09b74-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="09b74-133">В hello **параметры публикации Microsoft Azure** мастера выберите hello **ОК** кнопку, когда вы будете готовы toopublish облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09b74-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="09b74-134">Если вы не готовы toopublish, выберите hello **отменить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="09b74-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="09b74-135">параметры конфигурации Hello сохраняются, и можно опубликовать облачную службу позже.</span><span class="sxs-lookup"><span data-stu-id="09b74-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="09b74-136">Подключение к удаленному рабочему столу tooan роли Azure</span><span class="sxs-lookup"><span data-stu-id="09b74-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="09b74-137">После публикации облачной службы в Azure, можно использовать toolog обозреватель серверов в виртуальные машины hello, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="09b74-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="09b74-138">В обозревателе серверов разверните hello **Azure** узел, а затем раскройте узел hello облачной службы и одну из его ролей toodisplay список экземпляров.</span><span class="sxs-lookup"><span data-stu-id="09b74-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="09b74-139">Откройте контекстное меню узла экземпляра hello и выберите **подключиться с помощью удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="09b74-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Подключение через удаленный рабочий стол](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="09b74-141">Введите имя пользователя hello и пароль, который вы создали ранее.</span><span class="sxs-lookup"><span data-stu-id="09b74-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="09b74-142">Вы вошли в удаленный сеанс.</span><span class="sxs-lookup"><span data-stu-id="09b74-142">You are now logged into your remote session.</span></span>

