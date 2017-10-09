---
title: "учетные данные развертывания службы приложения aaaAzure | Документы Microsoft"
description: "Узнайте, как toouse hello учетные данные развертывания службы приложений Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="31df7-103">Настройка учетных данных развертывания службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="31df7-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="31df7-104">[Служба приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) поддерживает два типа учетных данных для [развертывания локальной системы Git](app-service-deploy-local-git.md) и [развертывания FTP(S)](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="31df7-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="31df7-105">Они не являются hello то же, что учетные данные Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31df7-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="31df7-106">**Учетные данные уровня пользователя**: один набор учетных данных для учетной записи Azure всей hello.</span><span class="sxs-lookup"><span data-stu-id="31df7-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="31df7-107">Для любого приложения, в любую из своих подписок, hello Azure учетная запись имеет разрешение tooaccess может быть tooApp используется toodeploy службы.</span><span class="sxs-lookup"><span data-stu-id="31df7-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="31df7-108">Это набор учетных данных по умолчанию hello, настройте в **службы приложений** > **&lt;имя_приложения >** > **учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="31df7-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="31df7-109">Это также является hello набор по умолчанию, которая будет отображена в портале hello графического интерфейса пользователя (например hello **Обзор** и **свойства** вашего приложения [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="31df7-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="31df7-110">При делегировании доступа к ресурсам tooAzure посредством управления на основе доступа ролей (RBAC) или соадминистратором разрешения каждого Azure пользователя, который получает доступ tooan приложения можно использовать своих личных учетных данных уровня пользователя, пока не отменяется доступ.</span><span class="sxs-lookup"><span data-stu-id="31df7-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="31df7-111">Эти учетные данные развертывания не следует использовать совместно с другими пользователями Azure.</span><span class="sxs-lookup"><span data-stu-id="31df7-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="31df7-112">**Учетные данные на уровне приложения**. Это единый набор учетных данных для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="31df7-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="31df7-113">Это может быть только используемые toodeploy toothat приложения.</span><span class="sxs-lookup"><span data-stu-id="31df7-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="31df7-114">Hello учетные данные для каждого приложения создается автоматически при создании приложения, а также находится в приложение hello профиль публикации.</span><span class="sxs-lookup"><span data-stu-id="31df7-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="31df7-115">Нельзя вручную настроить учетные данные hello, но вы можете сбросить их для приложения в любое время.</span><span class="sxs-lookup"><span data-stu-id="31df7-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31df7-116">В порядке toogive кто-то toothese учетные данные для доступа через доступа на основе элемента управления (РОЛЕЙ), вы должны toomake их участника или более поздней версии на веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31df7-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="31df7-117">Средства чтения не разрешены toopublish и недоступен, поэтому эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="31df7-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="31df7-118"><a name="userscope"></a>Установка и сброс учетных данных на уровне пользователя</span><span class="sxs-lookup"><span data-stu-id="31df7-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="31df7-119">Учетные данные на уровне пользователя можно настроить в [колонке ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources) любого приложения.</span><span class="sxs-lookup"><span data-stu-id="31df7-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="31df7-120">Независимо от на какие приложения вам следует настроить эти учетные данные, он применяет tooall приложений и для всех подписок в Azure учетная запись.</span><span class="sxs-lookup"><span data-stu-id="31df7-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="31df7-121">tooconfigure учетные данные уровня пользователя:</span><span class="sxs-lookup"><span data-stu-id="31df7-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="31df7-122">В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="31df7-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31df7-123">На портале hello необходимо иметь хотя бы одно приложение перед обращением к колонке учетные данные развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="31df7-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="31df7-124">Однако при наличии hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), можно настроить учетные данные уровня пользователя без существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="31df7-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="31df7-125">Настройте hello имя пользователя и пароль и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="31df7-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="31df7-126">После задания учетных данных развертывания можно найти hello *Git* развертывания имени пользователя в вашем приложении **Обзор**,</span><span class="sxs-lookup"><span data-stu-id="31df7-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="31df7-127">а имя пользователя для развертывания *FTP* — в разделе **Свойства** для приложения.</span><span class="sxs-lookup"><span data-stu-id="31df7-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="31df7-128">Azure не отображает пароль развертывания на уровне пользователя.</span><span class="sxs-lookup"><span data-stu-id="31df7-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="31df7-129">Если вы забудете пароль hello, его нельзя восстановить.</span><span class="sxs-lookup"><span data-stu-id="31df7-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="31df7-130">Тем не менее можно сбросить учетные данные с помощью инструкции hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="31df7-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="31df7-131"><a name="appscope"></a>Установка и сброс учетных данных на уровне приложений</span><span class="sxs-lookup"><span data-stu-id="31df7-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="31df7-132">Для каждого приложения в службе приложений свои учетные данные уровня приложения хранятся в hello XML профиля публикации.</span><span class="sxs-lookup"><span data-stu-id="31df7-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="31df7-133">учетные данные уровня приложения hello tooget:</span><span class="sxs-lookup"><span data-stu-id="31df7-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="31df7-134">В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="31df7-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="31df7-135">Щелкните **Дополнительно** > **Получить профиль публикации**. Начнется загрузка файла с расширением .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="31df7-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="31df7-136">Откройте hello. Файл параметров публикации и найти hello `<publishProfile>` тег с атрибутом hello `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="31df7-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="31df7-137">Получите из него атрибуты `userName` и `password`.</span><span class="sxs-lookup"><span data-stu-id="31df7-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="31df7-138">Это учетные данные уровня приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31df7-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="31df7-139">Подобных учетных данных toohello уровня пользователя имя пользователя hello FTP развертывания имеет формат hello `<app_name>\<username>`, и имя пользователя развертывания Git hello является просто `<username>` без hello выше `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="31df7-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="31df7-140">учетные данные уровня приложения hello tooreset:</span><span class="sxs-lookup"><span data-stu-id="31df7-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="31df7-141">В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="31df7-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="31df7-142">Щелкните **Дополнительно** > **Сбросить профиль публикации**.</span><span class="sxs-lookup"><span data-stu-id="31df7-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="31df7-143">Нажмите кнопку **Да** Сброс tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="31df7-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="31df7-144">Действие reset Hello делает недействительными все загруженные ранее. Файлы параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="31df7-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31df7-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31df7-145">Next steps</span></span>

<span data-ttu-id="31df7-146">Узнайте, как toouse toodeploy эти учетные данные приложения из [local Git](app-service-deploy-local-git.md) или с помощью [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="31df7-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
