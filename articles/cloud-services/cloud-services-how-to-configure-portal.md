---
title: "aaaHow tooconfigure облачной службы (портал) | Документы Microsoft"
description: "Узнайте, как tooconfigure облачных служб в Azure. Дополнительные сведения конфигурации tooupdate hello облачной службы и настраивают экземпляры toorole удаленного доступа. В этих примерах используются hello портал Azure."
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
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="673b9-105">Как tooConfigure облачных служб</span><span class="sxs-lookup"><span data-stu-id="673b9-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="673b9-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="673b9-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="673b9-107">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="673b9-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="673b9-108">Можно настроить параметры наиболее часто используемые hello для облачной службы в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="673b9-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="673b9-109">Или, если вам нравится tooupdate файлы конфигурации напрямую, загрузите tooupdate файла конфигурации службы, а затем отправьте hello обновления файла и обновление hello облачной службы с hello изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="673b9-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="673b9-110">В любом случае hello обновления конфигурации применяются tooall экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="673b9-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="673b9-111">Можно также управлять hello экземпляров роли облачной службы или удаленного рабочего стола в них.</span><span class="sxs-lookup"><span data-stu-id="673b9-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="673b9-112">Azure можете только обеспечить доступность службы 99,95% при hello обновлений конфигурации при наличии по крайней мере двух экземпляров роли для каждой роли.</span><span class="sxs-lookup"><span data-stu-id="673b9-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="673b9-113">Которая позволяет одной виртуальной машины tooprocess клиентские запросы других hello в процессе обновления.</span><span class="sxs-lookup"><span data-stu-id="673b9-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="673b9-114">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="673b9-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="673b9-115">Изменение облачной службы</span><span class="sxs-lookup"><span data-stu-id="673b9-115">Change a cloud service</span></span>
<span data-ttu-id="673b9-116">После открытия hello [портал Azure](https://portal.azure.com/), перейдите tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="673b9-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="673b9-117">Здесь можно управлять множеством параметров.</span><span class="sxs-lookup"><span data-stu-id="673b9-117">From here, you manage many aspects of it.</span></span>

![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="673b9-119">Hello **параметры** или **все параметры** ссылки будут открывать копию hello **параметры** колонки, где можно изменить hello **свойства**, измените hello **Конфигурации**, управлять hello **сертификаты**, программа установки **предупреждения правила**и управлять ими hello **пользователей** которые имеют доступ toothis облачной службы.</span><span class="sxs-lookup"><span data-stu-id="673b9-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Колонка параметров облачной службы Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="673b9-121">Управление версией гостевой ОС</span><span class="sxs-lookup"><span data-stu-id="673b9-121">Manage Guest OS version</span></span>

<span data-ttu-id="673b9-122">По умолчанию Azure периодически обновляет гостевой toohello последние поддерживаемые образа ОС в hello семейство ОС, заданные в конфигурации службы (.cscfg), такие как Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="673b9-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="673b9-123">Если вам требуется tootarget конкретной версии ОС, может быть задана в hello **конфигурации** колонку.</span><span class="sxs-lookup"><span data-stu-id="673b9-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Настройка версии ОС](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="673b9-125">В случае выбора конкретной версии ОС автоматические обновления операционной системы отключаются, а ответственность за установку исправлений ложится на вас.</span><span class="sxs-lookup"><span data-stu-id="673b9-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="673b9-126">Убедитесь, что экземпляры роли получают обновления, или может привести к уязвимостям toosecurity приложения.</span><span class="sxs-lookup"><span data-stu-id="673b9-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="673b9-127">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="673b9-127">Monitoring</span></span>
<span data-ttu-id="673b9-128">Можно добавлять оповещения tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="673b9-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="673b9-129">Щелкните **Параметры** > **Правила оповещений** > **Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="673b9-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="673b9-130">Здесь можно настроить оповещение.</span><span class="sxs-lookup"><span data-stu-id="673b9-130">From here, you can setup an alert.</span></span> <span data-ttu-id="673b9-131">С hello **метрика** раскрывающийся список, можно настроить оповещения для hello следующие типы данных.</span><span class="sxs-lookup"><span data-stu-id="673b9-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="673b9-132">Скорость чтения с диска</span><span class="sxs-lookup"><span data-stu-id="673b9-132">Disk read</span></span>
* <span data-ttu-id="673b9-133">Скорость записи на диск</span><span class="sxs-lookup"><span data-stu-id="673b9-133">Disk write</span></span>
* <span data-ttu-id="673b9-134">Входящая скорость сети</span><span class="sxs-lookup"><span data-stu-id="673b9-134">Network in</span></span>
* <span data-ttu-id="673b9-135">Исходящая скорость сети</span><span class="sxs-lookup"><span data-stu-id="673b9-135">Network out</span></span>
* <span data-ttu-id="673b9-136">Процент использования ЦП</span><span class="sxs-lookup"><span data-stu-id="673b9-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="673b9-137">Настройка мониторинга с использованием плиток метрик</span><span class="sxs-lookup"><span data-stu-id="673b9-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="673b9-138">Вместо использования **параметры** > **правила оповещения**, можно щелкнуть один из hello плитки с метрикой hello **мониторинг** раздел hello **облака Служба** колонку.</span><span class="sxs-lookup"><span data-stu-id="673b9-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Мониторинг облачной службы](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="673b9-140">Здесь можно настроить hello диаграммы, используемой Плитка hello, или добавить правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="673b9-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="673b9-141">Перезагрузка, повторное создание образа и использование удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="673b9-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="673b9-142">В настоящее время не удается настроить удаленный рабочий стол с помощью hello **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="673b9-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="673b9-143">Тем не менее, можно задать через hello [классический портал Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), либо с помощью [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="673b9-144">Во-первых щелкните экземпляр службы hello облака.</span><span class="sxs-lookup"><span data-stu-id="673b9-144">First, click on hello cloud service instance.</span></span>

![Экземпляр облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="673b9-146">В hello колонку, вы может инициировать подключение к удаленному рабочему столу, удаленно перезагрузить экземпляр hello, или удаленно экземпляр hello повторное создание образа (запуск с помощью нового образа).</span><span class="sxs-lookup"><span data-stu-id="673b9-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Кнопки экземпляра облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="673b9-148">Изменение CSCFG-файла</span><span class="sxs-lookup"><span data-stu-id="673b9-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="673b9-149">Может потребоваться tooreconfigure облачной службы через hello [файла конфигурации службы (cscfg)](cloud-services-model-and-package.md#cscfg) файла.</span><span class="sxs-lookup"><span data-stu-id="673b9-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="673b9-150">Сначала необходимо toodownload вашей .cscfg файл, измените его, а затем передать его.</span><span class="sxs-lookup"><span data-stu-id="673b9-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="673b9-151">Щелкните hello **параметры** значок или hello **все параметры** связать tooopen копирование hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="673b9-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="673b9-153">Щелкните hello **конфигурации** элемента.</span><span class="sxs-lookup"><span data-stu-id="673b9-153">Click on hello **Configuration** item.</span></span>

    ![Колонка «Конфигурация»](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="673b9-155">Щелкните hello **загрузки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="673b9-155">Click on hello **Download** button.</span></span>

    ![Загрузить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="673b9-157">После обновления файла конфигурации службы hello, загрузить и установить обновления конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="673b9-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Отправить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="673b9-159">Выберите файл cscfg hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="673b9-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="673b9-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="673b9-160">Next steps</span></span>
* <span data-ttu-id="673b9-161">Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="673b9-162">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="673b9-163">[Управление облачной службой](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="673b9-164">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
