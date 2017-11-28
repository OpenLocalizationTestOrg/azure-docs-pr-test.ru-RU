---
title: "Учетные данные развертывания службы приложений Azure | Документация Майкрософт"
description: "Сведения об использовании учетных данных развертывания службы приложений Azure."
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
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="a7526-103">Настройка учетных данных развертывания службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a7526-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="a7526-104">[Служба приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) поддерживает два типа учетных данных для [развертывания локальной системы Git](app-service-deploy-local-git.md) и [развертывания FTP(S)](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a7526-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="a7526-105">Это не то же, что учетные данные Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7526-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="a7526-106">**Учетные данные на уровне пользователя**. Это единый набор учетных данных для всей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="a7526-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="a7526-107">С его помощью можно развернуть службу приложений для любого приложения и в любой подписке, на доступ к которой у этой учетной записи Azure есть права.</span><span class="sxs-lookup"><span data-stu-id="a7526-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="a7526-108">Этот набор учетных данных используется по умолчанию и настраивается в разделе **Службы приложений** > **&lt;имя_приложения>** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="a7526-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="a7526-109">Также именно это значение по умолчанию отображается на портале графического пользовательского интерфейса (например, в разделах **Обзор** и **Свойства** в [колонке ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources) приложения).</span><span class="sxs-lookup"><span data-stu-id="a7526-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7526-110">Когда вы делегируете доступ к ресурсам Azure с помощью управления доступом на основе ролей или прав соадминистратора, каждый пользователь Azure, получивший доступ к приложению, сможет использовать свои учетные данные на уровне пользователя, пока доступ не будет отозван.</span><span class="sxs-lookup"><span data-stu-id="a7526-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="a7526-111">Эти учетные данные развертывания не следует использовать совместно с другими пользователями Azure.</span><span class="sxs-lookup"><span data-stu-id="a7526-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="a7526-112">**Учетные данные на уровне приложения**. Это единый набор учетных данных для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="a7526-113">С его помощью можно развернуть только одно приложение.</span><span class="sxs-lookup"><span data-stu-id="a7526-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="a7526-114">Учетные данные для каждого приложения автоматически создаются при создании приложения. Их можно найти в профиле публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="a7526-115">Вы не можете указать эти учетные данные вручную, но в любой момент можете сбросить их для приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7526-116">Чтобы предоставить пользователю доступ к этим учетным данным через управление доступом на основе ролей, он должен иметь в веб-приложении роль участника или более высокую.</span><span class="sxs-lookup"><span data-stu-id="a7526-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="a7526-117">Читатели не могут выполнять публикацию, и поэтому они не могут получить эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="a7526-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="a7526-118"><a name="userscope"></a>Установка и сброс учетных данных на уровне пользователя</span><span class="sxs-lookup"><span data-stu-id="a7526-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="a7526-119">Учетные данные на уровне пользователя можно настроить в [колонке ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources) любого приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="a7526-120">Независимо от того, в каком приложении вы настроите эти учетные данные, они будут применяться для всех приложений и всех подписок в учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="a7526-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="a7526-121">Чтобы настроить учетные данные на уровне пользователя, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7526-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="a7526-122">На [портале Azure](https://portal.azure.com) щелкните "Служба приложений" > **&lt;любое_приложение>** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="a7526-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7526-123">Чтобы можно было открыть колонку учетных данных развертывания, на портале должно существовать хотя бы одно приложение.</span><span class="sxs-lookup"><span data-stu-id="a7526-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="a7526-124">Настроить учетные данные на уровне пользователя без приложения можно с помощью [интерфейса командной строки Azure](app-service-web-app-azure-resource-manager-xplat-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a7526-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="a7526-125">Укажите имя пользователя и пароль, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7526-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="a7526-126">Когда вы настроите учетные данные развертывания, имя пользователя для развертывания *Git* можно будет найти в разделе **Обзор** для приложения,</span><span class="sxs-lookup"><span data-stu-id="a7526-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="a7526-127">а имя пользователя для развертывания *FTP* — в разделе **Свойства** для приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="a7526-128">Azure не отображает пароль развертывания на уровне пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7526-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="a7526-129">Если вы забудете пароль, вы не сможете его восстановить.</span><span class="sxs-lookup"><span data-stu-id="a7526-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="a7526-130">Но вы всегда можете сбросить учетные данные, выполнив действия, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a7526-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="a7526-131"><a name="appscope"></a>Установка и сброс учетных данных на уровне приложений</span><span class="sxs-lookup"><span data-stu-id="a7526-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="a7526-132">Для каждого приложения, существующего в службе приложений, в XML-профиле публикации сохраняются учетные данные соответствующего уровня.</span><span class="sxs-lookup"><span data-stu-id="a7526-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="a7526-133">Получить такие учетные данные можно так.</span><span class="sxs-lookup"><span data-stu-id="a7526-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="a7526-134">На [портале Azure](https://portal.azure.com) щелкните "Служба приложений" > **&lt;любое_приложение>** > **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a7526-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="a7526-135">Щелкните **Дополнительно** > **Получить профиль публикации**. Начнется загрузка файла с расширением .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="a7526-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="a7526-136">Откройте полученный файл и найдите в нем тег `<publishProfile>` с атрибутом `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="a7526-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="a7526-137">Получите из него атрибуты `userName` и `password`.</span><span class="sxs-lookup"><span data-stu-id="a7526-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="a7526-138">Это и есть учетные данные на уровне приложения.</span><span class="sxs-lookup"><span data-stu-id="a7526-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="a7526-139">Как и в случае с учетными данными на уровне пользователя, имя пользователя для развертывания FTP имеет формат `<app_name>\<username>`, а имя пользователя для развертывания Git представляет собой `<username>`, без предшествующего `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="a7526-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="a7526-140">Так можно сбросить учетные данные на уровне приложения:</span><span class="sxs-lookup"><span data-stu-id="a7526-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="a7526-141">На [портале Azure](https://portal.azure.com) щелкните "Служба приложений" > **&lt;любое_приложение>** > **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a7526-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="a7526-142">Щелкните **Дополнительно** > **Сбросить профиль публикации**.</span><span class="sxs-lookup"><span data-stu-id="a7526-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="a7526-143">Нажмите кнопку **Да** для подтверждения изменения.</span><span class="sxs-lookup"><span data-stu-id="a7526-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="a7526-144">Операция сброса делает все ранее загруженные файлы .PublishSettings недействительными.</span><span class="sxs-lookup"><span data-stu-id="a7526-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7526-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7526-145">Next steps</span></span>

<span data-ttu-id="a7526-146">Узнайте, как использовать эти учетные данные для развертывания приложения из [локального репозитория Git](app-service-deploy-local-git.md) или с помощью [FTP(S)](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a7526-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
