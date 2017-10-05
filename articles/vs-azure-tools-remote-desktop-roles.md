---
title: "Использование удаленного рабочего стола с ролями Azure | Документация Майкрософт"
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
ms.openlocfilehash: eab135d10c0d6df8ca72ac47d6804017a998a3d2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="652f0-103">Использование удаленного рабочего стола с ролями Azure</span><span class="sxs-lookup"><span data-stu-id="652f0-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="652f0-104">С помощью пакета SDK Azure и служб удаленных рабочих столов можно получать доступ к ролям Azure и виртуальным машинам, размещенным в Azure.</span><span class="sxs-lookup"><span data-stu-id="652f0-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="652f0-105">В Visual Studio можно настроить службы удаленных рабочих столов из проекта облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="652f0-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="652f0-106">Чтобы включить службы удаленных рабочих столов, необходимо создать рабочий проект, содержащий одну или несколько ролей, а затем опубликовать его в Azure.</span><span class="sxs-lookup"><span data-stu-id="652f0-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="652f0-107">К роли Azure следует обращаться только для разработки или устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="652f0-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="652f0-108">Каждая виртуальная машина предназначена для выполнения определенной роли в приложении Azure, а не для выполнения других клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="652f0-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span></span> <span data-ttu-id="652f0-109">Если вы хотите использовать Azure для размещения виртуальной машины, которую можно использовать для любых целей, см. статью «Доступ к виртуальным машинам Azure из обозревателя серверов».</span><span class="sxs-lookup"><span data-stu-id="652f0-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="652f0-110">Включение и использование удаленного рабочего стола для роли Azure</span><span class="sxs-lookup"><span data-stu-id="652f0-110">To enable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="652f0-111">В обозревателе решений откройте контекстное меню проекта облачной службы Azure и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="652f0-111">In Solution Explorer, open the shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="652f0-112">Откроется **мастер публикации приложений Azure** .</span><span class="sxs-lookup"><span data-stu-id="652f0-112">The **Publish Azure Application** wizard appears.</span></span>
   
    ![Команда «Опубликовать» для проекта облачной службы](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="652f0-114">В нижней части страницы **Параметры публикации Microsoft Azure** мастера установите флажок **Включить удаленный рабочий стол для всех ролей**.</span><span class="sxs-lookup"><span data-stu-id="652f0-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="652f0-115">Появится диалоговое окно **Конфигурация удаленного рабочего стола** .</span><span class="sxs-lookup"><span data-stu-id="652f0-115">The **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="652f0-116">В нижней части диалогового окна **Конфигурация удаленного рабочего стола** нажмите кнопку **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="652f0-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span></span> 
   
    <span data-ttu-id="652f0-117">Отобразится раскрывающийся список, с помощью которого можно создать или выбрать сертификат, чтобы шифровать учетные данные при подключении через удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="652f0-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="652f0-118">Из раскрывающегося списка выберите пункт **&lt;Создать>** либо существующий сертификат.</span><span class="sxs-lookup"><span data-stu-id="652f0-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span></span> 
   
    <span data-ttu-id="652f0-119">Если вы выбрали существующий сертификат, пропустите следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="652f0-119">If you choose an existing certificate, skip the following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="652f0-120">Сертификаты, необходимые для подключения к удаленному рабочему столу, отличаются от сертификатов, используемых для других операций в Azure.</span><span class="sxs-lookup"><span data-stu-id="652f0-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span></span> <span data-ttu-id="652f0-121">Сертификат удаленного доступа должен иметь закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="652f0-121">The remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="652f0-122">Появится диалоговое окно **Создание сертификата** .</span><span class="sxs-lookup"><span data-stu-id="652f0-122">The **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="652f0-123">Введите понятное имя для нового сертификата, а затем нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="652f0-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span></span> <span data-ttu-id="652f0-124">Новый сертификат появится в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="652f0-124">The new certificate appears in the dropdown list box.</span></span>
   2. <span data-ttu-id="652f0-125">В диалоговом окне **Конфигурация удаленного рабочего стола** введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="652f0-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="652f0-126">Нельзя использовать существующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="652f0-126">You can’t use an existing account.</span></span> <span data-ttu-id="652f0-127">Не указывайте Administrator как имя пользователя для новой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="652f0-127">Don’t specify Administrator as the user name for the new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="652f0-128">Если пароль не отвечает требованиям сложности, рядом с текстовым полем пароля появится красный значок.</span><span class="sxs-lookup"><span data-stu-id="652f0-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span></span> <span data-ttu-id="652f0-129">Пароль должен содержать прописные буквы, строчные буквы, а также цифры или символы.</span><span class="sxs-lookup"><span data-stu-id="652f0-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="652f0-130">Выберите дату окончания срока действия учетной записи, после которой подключения к удаленному рабочему столу будут заблокированы.</span><span class="sxs-lookup"><span data-stu-id="652f0-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="652f0-131">Указав все необходимые сведения, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="652f0-131">After you've provided all the required information, choose the **OK** button.</span></span>
      
       <span data-ttu-id="652f0-132">Несколько параметров, использующихся для включения служб удаленного доступа, добавляются в файлы CSCFG и CSDEF.</span><span class="sxs-lookup"><span data-stu-id="652f0-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="652f0-133">В мастере **Параметры публикации Microsoft Azure** нажмите кнопку **ОК**, когда будете готовы опубликовать облачную службу.</span><span class="sxs-lookup"><span data-stu-id="652f0-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span></span>
   
    <span data-ttu-id="652f0-134">Если вы не готовы к публикации, нажмите кнопку **Отменить** .</span><span class="sxs-lookup"><span data-stu-id="652f0-134">If you're not ready to publish, choose the **Cancel** button.</span></span> <span data-ttu-id="652f0-135">Параметры конфигурации будут сохранены, и вы сможете опубликовать облачную службу позже.</span><span class="sxs-lookup"><span data-stu-id="652f0-135">The configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="652f0-136">Подключение к роли Azure с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="652f0-136">Connect to an Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="652f0-137">Опубликовав облачную службу в Azure, можно входить в виртуальные машины, размещенные в Azure, с помощью обозревателя сервера.</span><span class="sxs-lookup"><span data-stu-id="652f0-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="652f0-138">В обозревателе сервера разверните узел **Azure** , а затем разверните узел для облачной службы и одну из ее ролей, чтобы отобразить список экземпляров.</span><span class="sxs-lookup"><span data-stu-id="652f0-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>
2. <span data-ttu-id="652f0-139">Откройте контекстное меню для узла экземпляра и выберите **Подключиться с помощью удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="652f0-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Подключение через удаленный рабочий стол](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="652f0-141">Введите имя пользователя и пароль, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="652f0-141">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="652f0-142">Вы вошли в удаленный сеанс.</span><span class="sxs-lookup"><span data-stu-id="652f0-142">You are now logged into your remote session.</span></span>

