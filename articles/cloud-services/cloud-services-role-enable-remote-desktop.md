---
title: "aaaEnable удаленного рабочего стола в облачной службе Azure | Документы Microsoft"
description: "Как tooconfigure azure облачной службы подключения удаленного рабочего стола tooallow приложения"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="ebe42-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="ebe42-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebe42-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebe42-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="ebe42-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebe42-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="ebe42-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebe42-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="ebe42-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebe42-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="ebe42-108">Можно включить удаленный рабочий стол в данной роли во время разработки, включая модули, удаленный рабочий стол hello в определении службы или вы можете tooenable удаленного рабочего стола через hello расширения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ebe42-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="ebe42-109">Hello рекомендуется расширение удаленного рабочего стола hello toouse как можно включить удаленный рабочий стол, даже после развертывания приложения hello без необходимости tooredeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="ebe42-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="ebe42-110">Настроить удаленный рабочий стол из hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebe42-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="ebe42-111">Hello классический портал Azure использует подход hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, даже после развертывания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="ebe42-112">Hello **Настройка** страницы для облачной службы можно tooenable удаленного рабочего стола, изменение hello локальную учетную запись администратора используется tooconnect toohello виртуальных машин, сертификат hello, используемые в проверке подлинности и задайте hello Дата окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="ebe42-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="ebe42-113">Нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="ebe42-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="ebe42-114">Нажмите кнопку hello **удаленного** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Удаленный доступ к облачным службам](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="ebe42-116">Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="ebe42-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="ebe42-117">tooprevent перезагрузки пароль hello hello сертификата используется tooencrypt должен устанавливаться на роли hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="ebe42-118">tooprevent перезагрузки [отправка сертификата для облачной службы hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , а затем возвращают toothis диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ebe42-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="ebe42-119">В **ролей**, выберите роль hello tooupdate или выберите **все** для всех ролей.</span><span class="sxs-lookup"><span data-stu-id="ebe42-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="ebe42-120">Внесите любые hello следующие отличия.</span><span class="sxs-lookup"><span data-stu-id="ebe42-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="ebe42-121">Удаленный рабочий стол, выберите hello tooenable **включить удаленный рабочий стол** флажок.</span><span class="sxs-lookup"><span data-stu-id="ebe42-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="ebe42-122">toodisable удаленного рабочего стола, hello, снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="ebe42-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="ebe42-123">Создайте toouse учетной записи подключения удаленного рабочего стола toohello экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="ebe42-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="ebe42-124">Обновление пароля hello hello существующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ebe42-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="ebe42-125">Выберите toouse отправленный сертификат для проверки подлинности (сертификат hello передачи с помощью **отправить** на hello **сертификаты** страницы) или создать новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="ebe42-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="ebe42-126">Измените дату окончания срока действия hello hello настройки удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ebe42-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="ebe42-127">По завершении обновления настроек нажмите кнопку **OK** (флажок).</span><span class="sxs-lookup"><span data-stu-id="ebe42-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="ebe42-128">Удаленное подключение к экземплярам ролей</span><span class="sxs-lookup"><span data-stu-id="ebe42-128">Remote into role instances</span></span>
<span data-ttu-id="ebe42-129">После включения удаленного рабочего стола с ролями hello можно удаленного в экземпляре роли через различные средства.</span><span class="sxs-lookup"><span data-stu-id="ebe42-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="ebe42-130">tooconnect tooa экземпляра роли из hello классического портала Azure:</span><span class="sxs-lookup"><span data-stu-id="ebe42-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="ebe42-131">Нажмите кнопку **экземпляров** tooopen hello **экземпляров** страницы.</span><span class="sxs-lookup"><span data-stu-id="ebe42-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="ebe42-132">Выберите экземпляр роли, где настроен удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="ebe42-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="ebe42-133">Нажмите кнопку **Connect**и выполните инструкции tooopen hello hello-рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ebe42-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="ebe42-134">Нажмите кнопку **откройте** и затем **Connect** toostart hello подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ebe42-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="ebe42-135">Используйте Visual Studio tooremote в экземпляр роли</span><span class="sxs-lookup"><span data-stu-id="ebe42-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="ebe42-136">В обозревателе сервера Visual Studio выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ebe42-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="ebe42-137">Разверните hello **Azure** > **облачные службы** > **[имя облачной службы]** узла.</span><span class="sxs-lookup"><span data-stu-id="ebe42-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="ebe42-138">Разверните узел **Промежуточные** или **Рабочие**.</span><span class="sxs-lookup"><span data-stu-id="ebe42-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="ebe42-139">Разверните роль отдельных hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="ebe42-140">Щелкните правой кнопкой мыши один из экземпляров роли hello, щелкните **подключиться с помощью удаленного рабочего стола...** , а затем введите hello имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="ebe42-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Удаленный рабочий стол обозревателя сервера](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="ebe42-142">Использовать файл протокола удаленного рабочего СТОЛА hello tooget PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebe42-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="ebe42-143">Можно использовать hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) tooretrieve hello командлет RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="ebe42-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="ebe42-144">Затем можно использовать hello RDP-файл с помощью удаленного рабочего стола tooaccess hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ebe42-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="ebe42-145">Программным образом Загрузите RDP-файл hello через hello API REST управления службами</span><span class="sxs-lookup"><span data-stu-id="ebe42-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="ebe42-146">Можно использовать hello [загрузить файл RDP](https://msdn.microsoft.com/library/jj157183.aspx) REST операции toodownload hello RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="ebe42-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="ebe42-147">tooconfigure удаленного рабочего стола в файле определения службы hello</span><span class="sxs-lookup"><span data-stu-id="ebe42-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="ebe42-148">Этот метод позволяет tooenable удаленного рабочего стола для приложения hello во время разработки.</span><span class="sxs-lookup"><span data-stu-id="ebe42-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="ebe42-149">Этот подход требует зашифрованные пароли храниться в конфигурации службы файлов и любые обновления toohello конфигурацию удаленного рабочего стола потребуется повторное развертывание приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="ebe42-150">Если требуется, чтобы tooavoid этих недостатков, следует использовать hello удаленного рабочего стола расширения на основе подход, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="ebe42-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="ebe42-151">Можно также использовать Visual Studio[включить подключение удаленного рабочего стола](../vs-azure-tools-remote-desktop-roles.md) подход файла определения службы hello.</span><span class="sxs-lookup"><span data-stu-id="ebe42-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="ebe42-152">Hello перечисленные ниже шаги описывают hello изменения toohello необходимые службы модели файлы tooenable удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ebe42-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="ebe42-153">Visual Studio автоматически выполнит эти изменения при публикации.</span><span class="sxs-lookup"><span data-stu-id="ebe42-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="ebe42-154">Настройка подключения hello в модели службы hello</span><span class="sxs-lookup"><span data-stu-id="ebe42-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="ebe42-155">Используйте hello **Imports** hello элемент tooimport **RemoteAccess** модуль и hello **RemoteForwarder** toohello модуль [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) файл.</span><span class="sxs-lookup"><span data-stu-id="ebe42-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="ebe42-156">Hello файла определения службы должен быть примерно toohello следующий пример с hello `<Imports>` добавлен элемент.</span><span class="sxs-lookup"><span data-stu-id="ebe42-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="ebe42-157">Hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) файла должен быть примерно toohello следующий пример, обратите внимание, hello `<ConfigurationSettings>` и `<Certificates>` элементы.</span><span class="sxs-lookup"><span data-stu-id="ebe42-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="ebe42-158">Hello указанный сертификат должен быть [отправлен toohello облачной службы](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="ebe42-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="ebe42-159">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ebe42-159">Additional Resources</span></span>
<span data-ttu-id="ebe42-160">[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ebe42-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
