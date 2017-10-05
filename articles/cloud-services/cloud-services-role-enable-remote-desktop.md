---
title: "Включение удаленного рабочего стола в облачной службе Azure | Документация Майкрософт"
description: "Настройка приложения в облачной службе Azure для удаленного подключения."
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
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="cbe53-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="cbe53-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cbe53-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="cbe53-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="cbe53-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="cbe53-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="cbe53-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbe53-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="cbe53-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbe53-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="cbe53-108">Во время разработки можно разрешить подключения к удаленному рабочему столу для роли, включив модули удаленного рабочего стола в определение службы или включив удаленный рабочий стол с помощью расширения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cbe53-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="cbe53-109">Рекомендуется использовать расширение удаленного рабочего стола, так как удаленный рабочий стол можно включить даже после развертывания приложения без необходимости повторного развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="cbe53-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="cbe53-110">Настройка удаленного рабочего стола на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="cbe53-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="cbe53-111">На классическом портале Azure используется подход с расширением удаленного рабочего стола, поэтому удаленный рабочий стол можно включить даже после развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="cbe53-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="cbe53-112">На странице **Настройка** облачной службы можно включить удаленный рабочий стол, изменить учетную запись локального администратора для подключения к виртуальным машинам, выбрать сертификат для проверки подлинности, а также установить срок его действия.</span><span class="sxs-lookup"><span data-stu-id="cbe53-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="cbe53-113">Щелкните **Облачные службы**, выберите имя облачной службы, а затем — **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="cbe53-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="cbe53-114">Нажмите кнопку **Уд. доступ** внизу.</span><span class="sxs-lookup"><span data-stu-id="cbe53-114">Click the **Remote** button at the bottom.</span></span>

    ![Удаленный доступ к облачным службам](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="cbe53-116">Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="cbe53-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="cbe53-117">Если в роли установлен сертификат для шифрования пароля, перезапуск не производится.</span><span class="sxs-lookup"><span data-stu-id="cbe53-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="cbe53-118">Чтобы не выполнять перезапуск, [загрузите сертификат для облачной службы](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) и вернитесь в диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="cbe53-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="cbe53-119">В разделе **Роли** выберите роль, которую требуется обновить, или щелкните **Все**, чтобы задать все роли.</span><span class="sxs-lookup"><span data-stu-id="cbe53-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="cbe53-120">Внесите любые из следующих изменений:</span><span class="sxs-lookup"><span data-stu-id="cbe53-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="cbe53-121">Чтобы включить удаленный рабочий стол, установите флажок **Включить удаленный рабочий стол** .</span><span class="sxs-lookup"><span data-stu-id="cbe53-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="cbe53-122">Если доступ к удаленному рабочему столу не требуется, снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="cbe53-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="cbe53-123">Создайте учетную запись, которая будет использоваться в подключениях к удаленному рабочему столу в экземплярах роли.</span><span class="sxs-lookup"><span data-stu-id="cbe53-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="cbe53-124">Обновите пароль существующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cbe53-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="cbe53-125">Выберите сертификат, который будет использоваться для аутентификации: новый или переданный с помощью раздела **Отправка** на странице **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="cbe53-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="cbe53-126">Измените срок действия для конфигурации удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cbe53-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="cbe53-127">По завершении обновления настроек нажмите кнопку **OK** (флажок).</span><span class="sxs-lookup"><span data-stu-id="cbe53-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="cbe53-128">Удаленное подключение к экземплярам ролей</span><span class="sxs-lookup"><span data-stu-id="cbe53-128">Remote into role instances</span></span>
<span data-ttu-id="cbe53-129">После включения удаленного рабочего стола для роли можно удаленно подключаться к экземпляру роли с помощью различных средств.</span><span class="sxs-lookup"><span data-stu-id="cbe53-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="cbe53-130">Подключение к экземпляру роли на классическом портале Azure:</span><span class="sxs-lookup"><span data-stu-id="cbe53-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="cbe53-131">Щелкните **Экземпляры**, чтобы открыть страницу **Экземпляры**.</span><span class="sxs-lookup"><span data-stu-id="cbe53-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="cbe53-132">Выберите экземпляр роли, где настроен удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="cbe53-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="cbe53-133">Нажмите **Подключить**и следуйте инструкциям для открытия рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cbe53-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="cbe53-134">Щелкните **Открыть**, а затем — **Подключить**, чтобы установить подключение к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="cbe53-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="cbe53-135">Удаленное подключение к экземпляру роли с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbe53-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="cbe53-136">В обозревателе сервера Visual Studio выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cbe53-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="cbe53-137">Разверните узел **Azure** > **Cloud Services** > **[имя облачной службы]**.</span><span class="sxs-lookup"><span data-stu-id="cbe53-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="cbe53-138">Разверните узел **Промежуточные** или **Рабочие**.</span><span class="sxs-lookup"><span data-stu-id="cbe53-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="cbe53-139">Разверните нужную роль.</span><span class="sxs-lookup"><span data-stu-id="cbe53-139">Expand the individual role.</span></span>
4. <span data-ttu-id="cbe53-140">Щелкните правой кнопкой мыши по одному из экземпляров роли, выберите **Подключиться с помощью удаленного рабочего стола...**, а затем введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="cbe53-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![Удаленный рабочий стол обозревателя сервера](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="cbe53-142">Получение RDP-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbe53-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="cbe53-143">RDP-файл можно получить с помощью командлета [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cbe53-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="cbe53-144">Затем с помощью этого файла вы сможете подключаться к облачной службе по протоколу удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cbe53-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="cbe53-145">Загрузка RDP-файла через API REST управления службами программным способом</span><span class="sxs-lookup"><span data-stu-id="cbe53-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="cbe53-146">Вы можете загрузить RDP-файл с помощью операции REST [Загрузить RDP-файл](https://msdn.microsoft.com/library/jj157183.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cbe53-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="cbe53-147">Настройка удаленного рабочего стола в файле определения службы</span><span class="sxs-lookup"><span data-stu-id="cbe53-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="cbe53-148">Этот метод позволяет включить удаленный рабочий стол для приложения во время разработки.</span><span class="sxs-lookup"><span data-stu-id="cbe53-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="cbe53-149">Этот подход требует, чтобы зашифрованные пароли хранились в файле конфигурации службы. При этом любые изменения конфигурации удаленного рабочего стола потребуют повторного развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="cbe53-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="cbe53-150">Если вы хотите избежать этих недостатков, следует использовать подход с расширением удаленного рабочего стола, который описан выше.</span><span class="sxs-lookup"><span data-stu-id="cbe53-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="cbe53-151">Для [включения подключения к удаленному рабочему столу](../vs-azure-tools-remote-desktop-roles.md) с помощью файла определения службы можно воспользоваться Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbe53-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="cbe53-152">Следующие шаги описывают изменения, которые необходимо произвести в файлах модели службы, чтобы включить удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="cbe53-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="cbe53-153">Visual Studio автоматически выполнит эти изменения при публикации.</span><span class="sxs-lookup"><span data-stu-id="cbe53-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="cbe53-154">Настройка подключения в модели службы</span><span class="sxs-lookup"><span data-stu-id="cbe53-154">Set up the connection in the service model</span></span>
<span data-ttu-id="cbe53-155">Используйте элемент **Imports** для импорта модулей **RemoteAccess** и **RemoteForwarder** в файле [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef).</span><span class="sxs-lookup"><span data-stu-id="cbe53-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="cbe53-156">Файл определения службы должен быть таким, как показано в примере ниже, с добавленным элементом `<Imports>` .</span><span class="sxs-lookup"><span data-stu-id="cbe53-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

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
<span data-ttu-id="cbe53-157">Файл [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) должен быть таким, как показано в следующем примере, с добавлением элементов `<ConfigurationSettings>` и `<Certificates>`.</span><span class="sxs-lookup"><span data-stu-id="cbe53-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="cbe53-158">Указанный сертификат необходимо [загрузить в облачную службу](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cbe53-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="cbe53-159">дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cbe53-159">Additional Resources</span></span>
<span data-ttu-id="cbe53-160">[Настройка облачных служб](cloud-services-how-to-configure.md)
[Часто задаваемые вопросы об облачных службах](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="cbe53-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
