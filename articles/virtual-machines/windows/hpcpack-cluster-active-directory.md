---
title: "кластер aaaHPC пакет с Azure Active Directory | Документы Microsoft"
description: "Узнайте, как кластер toointegrate 2016 пакета HPC в Azure с помощью Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="d8ead-103">Управление кластером пакета HPC в Azure с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8ead-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="d8ead-104">[Пакет Microsoft HPC 2016](https://technet.microsoft.com/library/cc514029) поддерживает интеграцию с [Azure Active Directory](../../active-directory/index.md) (Azure AD) для администраторов, развертывающих кластер пакета HPC в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8ead-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="d8ead-105">Выполните действия hello в этой статье для hello следующие задачи верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d8ead-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="d8ead-106">Интеграция кластера пакета HPC с клиентом Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ead-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="d8ead-107">Планирование заданий кластера HPC в Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="d8ead-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="d8ead-108">Интеграция решения кластера HPC Pack в Azure AD соответствует toointegrate стандартные действия, другие приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="d8ead-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="d8ead-109">В этой статье предполагается, что вы знакомы с основами пользовательского управления в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ead-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="d8ead-110">Дополнительные сведения и фона в разделе hello [документации Azure Active Directory](../../active-directory/index.md) и hello следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="d8ead-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="d8ead-111">Преимущества интеграции</span><span class="sxs-lookup"><span data-stu-id="d8ead-111">Benefits of integration</span></span>


<span data-ttu-id="d8ead-112">Azure Active Directory (Azure AD) представляет собой несколькими клиентами облачных каталогами и удостоверениями, предоставляющий доступ единого входа (SSO) toocloud решения.</span><span class="sxs-lookup"><span data-stu-id="d8ead-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="d8ead-113">Интеграция кластере HPC Pack в Azure AD может помочь достичь следующих целей hello:</span><span class="sxs-lookup"><span data-stu-id="d8ead-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="d8ead-114">Удалите hello традиционных контроллера домена Active Directory из кластера HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="d8ead-115">Это может помочь снизить затраты на обслуживание hello кластера в том случае, если это не требуется для вашей компании и ускорить процесс развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="d8ead-116">Использовать hello следующие преимущества, которые попадают в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d8ead-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="d8ead-117">Единый вход</span><span class="sxs-lookup"><span data-stu-id="d8ead-117">Single sign-on</span></span> 
    *   <span data-ttu-id="d8ead-118">С помощью локальных AD удостоверения для hello кластера HPC Pack в Azure</span><span class="sxs-lookup"><span data-stu-id="d8ead-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Среда Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="d8ead-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d8ead-120">Prerequisites</span></span>
* <span data-ttu-id="d8ead-121">**Кластер пакета HPC 2016, развернутый на виртуальных машинах Azure.** Дополнительные сведения см. в статье [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md) (Развертывание кластера пакета HPC 2016 в Azure).</span><span class="sxs-lookup"><span data-stu-id="d8ead-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="d8ead-122">Требуется DNS-имя головного узла hello hello и hello учетные данные администратора кластера для выполнения шагов hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d8ead-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d8ead-123">Интеграция Azure Active Directory не поддерживается в версиях пакета HPC до версии HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="d8ead-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="d8ead-124">**Клиентский компьютер** -требуется Windows или Windows Server клиентского компьютера слишком запущена HPC Pack клиентских служебных программ.</span><span class="sxs-lookup"><span data-stu-id="d8ead-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="d8ead-125">Если требуется только toouse hello HPC Pack веб-портала или API-интерфейса REST toosubmit задания, можно использовать любой клиентский компьютер по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="d8ead-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="d8ead-126">**Клиентские служебные программы пакета HPC** -установки на клиентском компьютере hello, доступные из центра загрузки Майкрософт hello hello бесплатный установочный пакет с помощью клиентских служебных программ пакета HPC hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="d8ead-127">Шаг 1: Регистрация сервера кластера HPC hello с клиентом Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ead-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="d8ead-128">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d8ead-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d8ead-129">Нажмите кнопку **Active Directory** в hello в левом меню и нажмите кнопку hello нужный каталог в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="d8ead-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="d8ead-130">Необходимо иметь разрешение tooaccess ресурсы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="d8ead-131">Щелкните **Пользователи** и убедитесь, что уже создана или настроена учетная запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="d8ead-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="d8ead-132">Щелкните **Приложения** > **Добавить** и выберите команду **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="d8ead-133">Введите следующую информацию в мастере hello hello:</span><span class="sxs-lookup"><span data-stu-id="d8ead-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="d8ead-134">**Имя** — HPCPackClusterServer.</span><span class="sxs-lookup"><span data-stu-id="d8ead-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="d8ead-135">**Тип** — выберите **Веб-приложение и/или веб-API**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="d8ead-136">**URL-адрес входа**- hello базовый URL-адрес для образца hello, который по умолчанию`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="d8ead-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="d8ead-137">**URI кода приложения** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="d8ead-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="d8ead-138">Замените `<Directory_name`> с hello полное имя вашего клиента Azure AD, например, `hpclocal.onmicrosoft.com`и замените `<application_name>` с именем hello были выбраны.</span><span class="sxs-lookup"><span data-stu-id="d8ead-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="d8ead-139">После добавления приложение hello щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="d8ead-140">Настройте hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="d8ead-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="d8ead-141">Для параметра **Приложение является мультитенантным** укажите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="d8ead-142">Выберите **Да** для **назначения пользователя. приложение требуется tooaccess**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="d8ead-143">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-143">Click **Save**.</span></span> <span data-ttu-id="d8ead-144">После того, как сохранение будет завершено, щелкните **Управление манифестом**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="d8ead-145">Это действие скачивает файл нотации объектов JavaScript (JSON) манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="d8ead-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="d8ead-146">Изменить манифест загружаются hello, найдя hello `appRoles` установку и добавление hello следующие роли приложения:</span><span class="sxs-lookup"><span data-stu-id="d8ead-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="d8ead-147">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-147">Save hello file.</span></span> <span data-ttu-id="d8ead-148">Hello портала щелкните **управление манифеста** > **отправить манифест**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="d8ead-149">Затем вы можете передать hello измененного манифест.</span><span class="sxs-lookup"><span data-stu-id="d8ead-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="d8ead-150">Щелкните **Пользователи**, выберите пользователя и щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="d8ead-151">Назначьте один из hello доступные роли (HpcUsers или HpcAdminMirror) toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="d8ead-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="d8ead-152">Повторите этот шаг, с помощью дополнительных пользователей в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="d8ead-153">Общие сведения о пользователях кластера см. в статье [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx) (Управление пользователями кластера).</span><span class="sxs-lookup"><span data-stu-id="d8ead-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="d8ead-154">toomanage пользователей, мы рекомендуем использовать колонки предварительной версии Azure Active Directory hello в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8ead-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="d8ead-155">Этап 2: Регистрация клиента кластера HPC hello с клиентом Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ead-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="d8ead-156">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d8ead-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d8ead-157">Нажмите кнопку **Active Directory** в hello в левом меню и нажмите кнопку hello нужный каталог в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="d8ead-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="d8ead-158">Необходимо иметь разрешение tooaccess ресурсы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="d8ead-159">Щелкните **Приложения** > **Добавить** и выберите команду **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="d8ead-160">Введите следующую информацию в мастере hello hello:</span><span class="sxs-lookup"><span data-stu-id="d8ead-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="d8ead-161">**Имя** — HPCPackClusterClient.</span><span class="sxs-lookup"><span data-stu-id="d8ead-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="d8ead-162">**Тип** — выберите **Native Client Apllication** (Собственное клиентское приложение).</span><span class="sxs-lookup"><span data-stu-id="d8ead-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="d8ead-163">**URI перенаправления** - `http://hpcclient`.</span><span class="sxs-lookup"><span data-stu-id="d8ead-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="d8ead-164">После добавления приложение hello щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="d8ead-165">Копировать hello **идентификатор клиента** значение и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="d8ead-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="d8ead-166">Оно понадобится позже при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="d8ead-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="d8ead-167">В **разрешения приложений tooother**, нажмите кнопку **добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="d8ead-168">Поиск и добавление приложения HpcPackClusterServer hello (созданного на шаге 1).</span><span class="sxs-lookup"><span data-stu-id="d8ead-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="d8ead-169">В hello **делегированные разрешения** раскрывающийся список, выберите **HpcClusterServer доступа**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="d8ead-170">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="d8ead-171">Шаг 3: Настройка кластера HPC hello</span><span class="sxs-lookup"><span data-stu-id="d8ead-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="d8ead-172">Подключите головного узла HPC Pack 2016 toohello в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8ead-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="d8ead-173">Запустите HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ead-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="d8ead-174">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="d8ead-175">где:</span><span class="sxs-lookup"><span data-stu-id="d8ead-175">where</span></span>

    * <span data-ttu-id="d8ead-176">`AADTenant`Указывает имя клиента Azure AD hello, такие как`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="d8ead-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="d8ead-177">`AADClientAppId`Указывает идентификатор hello клиента для приложения hello, созданный на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="d8ead-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="d8ead-178">Перезапустите службу HpcSchedulerStateful hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="d8ead-179">В кластере с несколькими головного узла можно выполнить следующие команды PowerShell hello головного узла tooswitch hello первичной реплике для службы HpcSchedulerStateful hello hello:</span><span class="sxs-lookup"><span data-stu-id="d8ead-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="d8ead-180">Шаг 4: Управление и отправлять задания с приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="d8ead-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="d8ead-181">tooinstall hello HPC Pack клиентские служебные программы на компьютере, загрузить файлы установки HPC Pack 2016 (полная установка) из центра загрузки Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="d8ead-182">При установке hello, выберите вариант установки hello для hello **клиентских служебных программ пакета HPC**.</span><span class="sxs-lookup"><span data-stu-id="d8ead-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="d8ead-183">hello сертификат, используемый во время установки tooprepare hello клиентский компьютер, [настройка кластера HPC](hpcpack-2016-cluster.md) на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="d8ead-184">Использовать стандартные Windows сертификатов управления процедуры tooinstall hello открытый сертификат toohello **Сертификаты — текущий пользователь** > **доверенные корневые центры сертификации** хранения.</span><span class="sxs-lookup"><span data-stu-id="d8ead-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="d8ead-185">Теперь можно выполнять команды hello пакета HPC или использовать графический Интерфейс диспетчера заданий HPC Pack hello toosubmit и управление заданиями кластера с помощью учетной записи hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ead-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="d8ead-186">Параметры отправки задания. в разделе [tooan HPC отправки заданий HPC Pack кластер в Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="d8ead-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="d8ead-187">При запуске кластера HPC Pack toohello tooconnect в Azure для hello впервые, откроется всплывающие окна.</span><span class="sxs-lookup"><span data-stu-id="d8ead-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="d8ead-188">Введите ваш toolog учетные данные Azure AD в.</span><span class="sxs-lookup"><span data-stu-id="d8ead-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="d8ead-189">токен Hello сохраняется в кэше.</span><span class="sxs-lookup"><span data-stu-id="d8ead-189">hello token is then cached.</span></span> <span data-ttu-id="d8ead-190">Более поздние версии кластера toohello подключений в Azure используйте hello в кэше маркер, если не снят изменения проверки подлинности или hello в кэше.</span><span class="sxs-lookup"><span data-stu-id="d8ead-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="d8ead-191">Например после выполнения предыдущих шагов hello, можно запросить для заданий с локального клиента следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8ead-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="d8ead-192">Полезные командлеты для отправки заданий с интеграцией Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ead-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="d8ead-193">Управление локальным кэшем токенов hello</span><span class="sxs-lookup"><span data-stu-id="d8ead-193">Manage hello local token cache</span></span>

<span data-ttu-id="d8ead-194">HPC Pack 2016 предоставляет два новых командлета HPC PowerShell toomanage hello локального маркера кэша.</span><span class="sxs-lookup"><span data-stu-id="d8ead-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="d8ead-195">Их можно использовать для отправки заданий в неинтерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="d8ead-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="d8ead-196">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="d8ead-197">Задать hello учетные данные для отправки заданий с помощью учетной записи hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ead-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="d8ead-198">В некоторых случаях может потребоваться задания hello toorun записью кластера HPC hello (присоединенных к домену кластер HPC, запуск от имени пользователя в одном домене, не присоединенных к домену кластер HPC, запуск от имени одного локального пользователя на головном узле hello).</span><span class="sxs-lookup"><span data-stu-id="d8ead-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="d8ead-199">Используйте следующие учетные данные hello tooset команды hello:</span><span class="sxs-lookup"><span data-stu-id="d8ead-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="d8ead-200">Затем отправьте задание hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d8ead-200">Then submit hello job as follows.</span></span> <span data-ttu-id="d8ead-201">Hello задания или задачи в разделе выполняется $localUser на hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="d8ead-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="d8ead-202">Если `–Credential` не указан с `Submit-HpcJob`, hello задания или задачи выполняется локальный пользователь сопоставленных как hello учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ead-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="d8ead-203">(кластер HPC hello создает локального пользователя с hello одинаковые имена, как hello задачу hello toorun учетной записи Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8ead-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="d8ead-204">Задайте расширенные данные для учетной записи Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="d8ead-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="d8ead-205">Это полезно при выполнении задания MPI на узлах Linux с помощью учетной записи hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ead-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="d8ead-206">Задайте расширенные данные для hello саму учетную запись Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ead-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="d8ead-207">Укажите подробные сведения и выполните задание от имени пользователя кластера HPC</span><span class="sxs-lookup"><span data-stu-id="d8ead-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

