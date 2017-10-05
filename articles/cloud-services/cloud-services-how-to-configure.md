---
title: "Настройка облачной службы с помощью классического портала | Документация Майкрософт"
description: "Узнайте, как настроить облачные службы в Azure. Как обновить конфигурацию облачной службы и настроить удаленный доступ к экземплярам роли."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 39bb294c96ce0c12d91cf8b3488ac3e1a7b2f7b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="4a56b-104">Настройка облачных служб</span><span class="sxs-lookup"><span data-stu-id="4a56b-104">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a56b-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4a56b-105">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="4a56b-106">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="4a56b-106">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
> 
> 

<span data-ttu-id="4a56b-107">Часто используемые параметры облачной службы можно настроить на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4a56b-107">You can configure the most commonly used settings for a cloud service in the Azure classic portal.</span></span> <span data-ttu-id="4a56b-108">Также можно напрямую изменить файлы конфигурации. Для этого загрузите и измените нужный файл, а затем отправьте его для обновления конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4a56b-108">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="4a56b-109">В любом случае обновления конфигурации применяются ко всем экземплярам ролей.</span><span class="sxs-lookup"><span data-stu-id="4a56b-109">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="4a56b-110">Классический портал Azure также позволяет [активировать подключение к удаленному рабочему столу для роли в облачных службах Azure](cloud-services-role-enable-remote-desktop.md)</span><span class="sxs-lookup"><span data-stu-id="4a56b-110">The Azure classic portal also allows you to [enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span></span>

<span data-ttu-id="4a56b-111">При наличии как минимум двух экземпляров для каждой роли в процессе обновления конфигурации Azure обеспечивается доступность службы в течение 99,95 % времени.</span><span class="sxs-lookup"><span data-stu-id="4a56b-111">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="4a56b-112">Такая конфигурация позволяет обрабатывать запросы клиентов на одной виртуальной машине во время обновления другой.</span><span class="sxs-lookup"><span data-stu-id="4a56b-112">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="4a56b-113">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="4a56b-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="4a56b-114">Изменение облачной службы</span><span class="sxs-lookup"><span data-stu-id="4a56b-114">Change a cloud service</span></span>
1. <span data-ttu-id="4a56b-115">На [классическом портале Azure](http://manage.windowsazure.com/) щелкните **Облачные службы**, а затем выберите имя облачной службы и щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="4a56b-115">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
   
    ![Страница «Конфигурация»](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    <span data-ttu-id="4a56b-117">На странице **Настройка** можно задать параметры мониторинга, обновить настройки ролей, а также выбрать гостевую операционную систему и семейство для экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="4a56b-117">On the **Configure** page, you can configure monitoring, update role settings, and choose the guest operating system and family for role instances.</span></span> 
2. <span data-ttu-id="4a56b-118">В параметрах **мониторинга**задайте уровень "Подробно" или "Минимальный" и настройте строки подключения диагностики, необходимые для подробного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="4a56b-118">In **monitoring**, set the monitoring level to Verbose or Minimal, and configure the diagnostics connection strings that are required for verbose monitoring.</span></span>
3. <span data-ttu-id="4a56b-119">Для ролей службы, сгруппированных по ролям, можно обновить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="4a56b-119">For service roles (grouped by role), you can update the following settings:</span></span>
   
    * <span data-ttu-id="4a56b-120">**Настройки** — измените значения параметров конфигурации, определенных в элементах *ConfigurationSettings* файла конфигурации службы (CSCFG-файла).</span><span class="sxs-lookup"><span data-stu-id="4a56b-120">**Settings** Modify the values of miscellaneous configuration settings that are specified in the *ConfigurationSettings* elements of the service configuration (.cscfg) file.</span></span>

    * <span data-ttu-id="4a56b-121">**Сертификаты**</span><span class="sxs-lookup"><span data-stu-id="4a56b-121">**Certificates**</span></span>  
        <span data-ttu-id="4a56b-122">— измените отпечаток сертификата, используемый при SSL-шифровании для роли.</span><span class="sxs-lookup"><span data-stu-id="4a56b-122">Change the certificate thumbprint that's being used in SSL encryption for a role.</span></span> <span data-ttu-id="4a56b-123">Чтобы сменить сертификат, загрузите новый сертификат на странице **Сертификаты** .</span><span class="sxs-lookup"><span data-stu-id="4a56b-123">To change a certificate, you must first upload the new certificate (on the **Certificates** page).</span></span> <span data-ttu-id="4a56b-124">После этого обновите отпечаток сертификата в строке в параметрах роли.</span><span class="sxs-lookup"><span data-stu-id="4a56b-124">Then update the thumbprint in the certificate string displayed in the role settings.</span></span>
4. <span data-ttu-id="4a56b-125">В параметрах **операционной системы** можно задать версию или семейство ОС для экземпляров роли, а также выбрать параметр **Автоматически**, который позволяет включить автоматическое обновление текущей версии ОС.</span><span class="sxs-lookup"><span data-stu-id="4a56b-125">In **operating system**, you can change the operating system family or version for role instances, or choose **Automatic** to enable automatic updates of the current operating system version.</span></span> <span data-ttu-id="4a56b-126">Настройки ОС распространяются на веб-роли и рабочие роли, но не влияют на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="4a56b-126">The operating system settings apply to web roles and worker roles, but do not affect Virtual Machines.</span></span>
   
    <span data-ttu-id="4a56b-127">В процессе развертывания на все экземпляры роли устанавливается последняя версия ОС с включенным по умолчанию автоматическим обновлением.</span><span class="sxs-lookup"><span data-stu-id="4a56b-127">During deployment, the most recent operating system version is installed on all role instances, and the operating systems are updated automatically by default.</span></span> 
   
    <span data-ttu-id="4a56b-128">Если требования к совместимости кода предусматривают работу с облачной службой в другой версии операционной системы, можно выбрать нужные версию и семейство ОС.</span><span class="sxs-lookup"><span data-stu-id="4a56b-128">If you need for your cloud service to run on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span></span> <span data-ttu-id="4a56b-129">При выборе конкретной версии ОС автоматическое обновление для облачной службы приостанавливается.</span><span class="sxs-lookup"><span data-stu-id="4a56b-129">When you choose a specific operating system version, automatic operating system updates for the cloud service are suspended.</span></span> <span data-ttu-id="4a56b-130">В этом случае необходимо настроить обновление операционных систем.</span><span class="sxs-lookup"><span data-stu-id="4a56b-130">You will need to ensure the operating systems receive updates.</span></span>
   
    <span data-ttu-id="4a56b-131">Если в последней версии ОС все проблемы с совместимостью приложений устранены, установите значение параметра **Автоматически**, чтобы включить автоматическое обновление операционной системы.</span><span class="sxs-lookup"><span data-stu-id="4a56b-131">If you resolve all compatibility issues that your apps have with the most recent operating system version, you can enable automatic operating system updates by setting the operating system version to **Automatic**.</span></span> 
   
    ![Параметры ОС](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. <span data-ttu-id="4a56b-133">Чтобы сохранить параметры конфигурации и передать их в экземпляры ролей, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4a56b-133">To save your configuration settings, and push them to the role instances, click **Save**.</span></span> <span data-ttu-id="4a56b-134">(Чтобы отменить изменения, нажмите кнопку **Отменить**.) Кнопки **Сохранить** и **Отменить** добавляются в панель команд после изменения параметра.</span><span class="sxs-lookup"><span data-stu-id="4a56b-134">(Click **Discard** to cancel the changes.) **Save** and **Discard** are added to the command bar after you change a setting.</span></span>

## <a name="update-a-cloud-service-configuration-file"></a><span data-ttu-id="4a56b-135">Обновление файла конфигурации облачной службы</span><span class="sxs-lookup"><span data-stu-id="4a56b-135">Update a cloud service configuration file</span></span>
1. <span data-ttu-id="4a56b-136">Загрузите файл конфигурации облачной службы (CSCFG) с текущей конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="4a56b-136">Download a cloud service configuration file (.cscfg) with the current configuration.</span></span> <span data-ttu-id="4a56b-137">На странице **Настройка** облачной службы щелкните **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="4a56b-137">On the **Configure** page for the cloud service, click **Download**.</span></span> <span data-ttu-id="4a56b-138">Далее выберите команды **Сохранить** или **Сохранить как**, чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="4a56b-138">Then click **Save**, or click **Save As** to save the file.</span></span>
2. <span data-ttu-id="4a56b-139">Чтобы применить обновления конфигурации, передайте новый файл в службу:</span><span class="sxs-lookup"><span data-stu-id="4a56b-139">After you update the service configuration file, upload and apply the configuration updates:</span></span>
   
   1. <span data-ttu-id="4a56b-140">На странице **Настройка** щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="4a56b-140">On the **Configure** page, click **Upload**.</span></span>
      
       ![Отправка конфигурации](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. <span data-ttu-id="4a56b-142">На вкладке **Файл конфигурации** нажмите кнопку **Обзор**, чтобы выбрать обновленный CSCFG-файл.</span><span class="sxs-lookup"><span data-stu-id="4a56b-142">In **Configuration file**, use **Browse** to select the updated .cscfg file.</span></span>
   3. <span data-ttu-id="4a56b-143">Если в облачной службе содержатся роли с одним экземпляром, установите флажок **Применить, даже если одна или несколько ролей содержат отдельный экземпляр** , чтобы обеспечить обновление конфигурации ролей.</span><span class="sxs-lookup"><span data-stu-id="4a56b-143">If your cloud service contains any roles that have only one instance, select the **Apply configuration even if one or more roles contain a single instance** check box to enable the configuration updates for the roles to proceed.</span></span>
      
       <span data-ttu-id="4a56b-144">Если для каждой роли не определены как минимум два экземпляра, Azure не гарантирует доступность службы в течение 99,95 % времени в процессе обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a56b-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span></span> <span data-ttu-id="4a56b-145">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="4a56b-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
   4. <span data-ttu-id="4a56b-146">Нажмите кнопку **OK** (флажок).</span><span class="sxs-lookup"><span data-stu-id="4a56b-146">Click **OK** (checkmark).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a56b-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a56b-147">Next steps</span></span>
* <span data-ttu-id="4a56b-148">Узнайте, как [развернуть облачную службу](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4a56b-148">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="4a56b-149">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4a56b-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="4a56b-150">[Управляйте облачной службой](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4a56b-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* [<span data-ttu-id="4a56b-151">Активация подключения к удаленному рабочему столу для роли в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="4a56b-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>](cloud-services-role-enable-remote-desktop.md)
* <span data-ttu-id="4a56b-152">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="4a56b-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

