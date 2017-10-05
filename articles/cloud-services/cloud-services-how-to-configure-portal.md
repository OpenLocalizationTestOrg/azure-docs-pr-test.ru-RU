---
title: "Настройка облачной службы с помощью портала | Документация Майкрософт"
description: "Узнайте, как настроить облачные службы в Azure. Как обновить конфигурацию облачной службы и настроить удаленный доступ к экземплярам роли. В этих примерах используется портал Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="cab48-105">Настройка облачных служб</span><span class="sxs-lookup"><span data-stu-id="cab48-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cab48-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="cab48-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="cab48-107">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="cab48-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="cab48-108">Часто используемые параметры облачной службы можно настроить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cab48-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="cab48-109">Также можно напрямую изменить файлы конфигурации. Для этого загрузите и измените нужный файл, а затем отправьте его для обновления конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="cab48-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="cab48-110">В любом случае обновления конфигурации применяются ко всем экземплярам ролей.</span><span class="sxs-lookup"><span data-stu-id="cab48-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="cab48-111">Также вы можете управлять экземплярами ролей облачной службы или подключиться к ним с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cab48-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="cab48-112">При наличии как минимум двух экземпляров для каждой роли в процессе обновления конфигурации Azure обеспечивается доступность службы в течение 99,95 % времени.</span><span class="sxs-lookup"><span data-stu-id="cab48-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="cab48-113">Такая конфигурация позволяет обрабатывать запросы клиентов на одной виртуальной машине во время обновления другой.</span><span class="sxs-lookup"><span data-stu-id="cab48-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="cab48-114">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="cab48-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="cab48-115">Изменение облачной службы</span><span class="sxs-lookup"><span data-stu-id="cab48-115">Change a cloud service</span></span>
<span data-ttu-id="cab48-116">Откройте [портал Azure](https://portal.azure.com/)и перейдите к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="cab48-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="cab48-117">Здесь можно управлять множеством параметров.</span><span class="sxs-lookup"><span data-stu-id="cab48-117">From here, you manage many aspects of it.</span></span>

![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="cab48-119">Ссылки **Параметры** или **Все параметры** позволяют открыть колонку **Параметры**, где вы можете изменять **свойства** и **конфигурацию**, настраивать **правила оповещений**, а также управлять **сертификатами** и доступом **пользователей** к этой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="cab48-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Колонка параметров облачной службы Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="cab48-121">Управление версией гостевой ОС</span><span class="sxs-lookup"><span data-stu-id="cab48-121">Manage Guest OS version</span></span>

<span data-ttu-id="cab48-122">По умолчанию Azure периодически обновляет гостевые ОС до последнего поддерживаемого образа в семействе ОС, указанном в конфигурации службы (CSCFG-файл), например Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="cab48-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="cab48-123">Если требуется использовать конкретную версию ОС, ее можно задать в колонке **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="cab48-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Настройка версии ОС](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="cab48-125">В случае выбора конкретной версии ОС автоматические обновления операционной системы отключаются, а ответственность за установку исправлений ложится на вас.</span><span class="sxs-lookup"><span data-stu-id="cab48-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="cab48-126">Вы должны обеспечить установку обновлений в экземплярах роли, иначе система безопасности вашего приложения будет уязвима.</span><span class="sxs-lookup"><span data-stu-id="cab48-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="cab48-127">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="cab48-127">Monitoring</span></span>
<span data-ttu-id="cab48-128">Вы можете включить оповещения в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="cab48-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="cab48-129">Щелкните **Параметры** > **Правила оповещений** > **Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="cab48-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="cab48-130">Здесь можно настроить оповещение.</span><span class="sxs-lookup"><span data-stu-id="cab48-130">From here, you can setup an alert.</span></span> <span data-ttu-id="cab48-131">Раскрывающийся список **Метрика** позволяет настроить оповещение для следующих типов данных.</span><span class="sxs-lookup"><span data-stu-id="cab48-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="cab48-132">Скорость чтения с диска</span><span class="sxs-lookup"><span data-stu-id="cab48-132">Disk read</span></span>
* <span data-ttu-id="cab48-133">Скорость записи на диск</span><span class="sxs-lookup"><span data-stu-id="cab48-133">Disk write</span></span>
* <span data-ttu-id="cab48-134">Входящая скорость сети</span><span class="sxs-lookup"><span data-stu-id="cab48-134">Network in</span></span>
* <span data-ttu-id="cab48-135">Исходящая скорость сети</span><span class="sxs-lookup"><span data-stu-id="cab48-135">Network out</span></span>
* <span data-ttu-id="cab48-136">Процент использования ЦП</span><span class="sxs-lookup"><span data-stu-id="cab48-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="cab48-137">Настройка мониторинга с использованием плиток метрик</span><span class="sxs-lookup"><span data-stu-id="cab48-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="cab48-138">Вместо элементов **Параметры** > **Правила оповещений** вы можете щелкнуть любую из плиток с метриками в разделе **Мониторинг** в колонке **Облачная служба**.</span><span class="sxs-lookup"><span data-stu-id="cab48-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Мониторинг облачной службы](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="cab48-140">Здесь можно настроить диаграммы для этой плитки или добавить правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="cab48-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="cab48-141">Перезагрузка, повторное создание образа и использование удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="cab48-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="cab48-142">Сейчас на **портале Azure**нельзя настроить использование удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="cab48-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="cab48-143">Но вы можете настроить его с помощью [классического портала Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) или [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cab48-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="cab48-144">Щелкните экземпляр облачной службы.</span><span class="sxs-lookup"><span data-stu-id="cab48-144">First, click on the cloud service instance.</span></span>

![Экземпляр облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="cab48-146">Откроется колонка, в которой вы можете инициировать подключение к удаленному рабочему столу, удаленно перезагрузить или пересоздать (заново развернуть из образа) экземпляр.</span><span class="sxs-lookup"><span data-stu-id="cab48-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Кнопки экземпляра облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="cab48-148">Изменение CSCFG-файла</span><span class="sxs-lookup"><span data-stu-id="cab48-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="cab48-149">Иногда возникает потребность изменить настройки облачной службы, сохраненные в файле [конфигурации службы (CSCFG)](cloud-services-model-and-package.md#cscfg) .</span><span class="sxs-lookup"><span data-stu-id="cab48-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="cab48-150">Для этого следует скачать CSCFG-файл, изменить его и отправить обратно.</span><span class="sxs-lookup"><span data-stu-id="cab48-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="cab48-151">Щелкните значок **Параметры** или выберите **Все параметры**, чтобы открыть колонку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="cab48-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="cab48-153">Выберите элемент **Конфигурация** .</span><span class="sxs-lookup"><span data-stu-id="cab48-153">Click on the **Configuration** item.</span></span>

    ![Колонка «Конфигурация»](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="cab48-155">Нажмите кнопку **Загрузить** .</span><span class="sxs-lookup"><span data-stu-id="cab48-155">Click on the **Download** button.</span></span>

    ![Загрузить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="cab48-157">Чтобы применить обновления конфигурации, передайте новый файл в службу:</span><span class="sxs-lookup"><span data-stu-id="cab48-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Отправить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="cab48-159">Выберите файл .cscfg и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cab48-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab48-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cab48-160">Next steps</span></span>
* <span data-ttu-id="cab48-161">Узнайте, как [развернуть облачную службу](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cab48-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="cab48-162">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cab48-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="cab48-163">[Управление облачной службой](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cab48-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="cab48-164">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cab48-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
