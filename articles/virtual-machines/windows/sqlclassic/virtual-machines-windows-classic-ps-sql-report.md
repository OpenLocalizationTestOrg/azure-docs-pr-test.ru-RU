---
title: "Использование PowerShell для создания виртуальных машин с помощью сервера отчетов, работающего в основном режиме | Документация Майкрософт"
description: "В этом разделе описывается процесс развертывания и настройки сервера отчетов собственного режима служб Reporting Services SQL Server на виртуальной машине Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="a4b54-103">Использование PowerShell для создания виртуальной машины Azure с помощью сервера отчетов, работающего в собственном режиме</span><span class="sxs-lookup"><span data-stu-id="a4b54-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="a4b54-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a4b54-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4b54-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a4b54-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a4b54-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="a4b54-107">В этом разделе описывается процесс развертывания и настройки сервера отчетов собственного режима служб Reporting Services SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="a4b54-108">Процедуры, описанные в этом документе, сочетают в себе выполняемые вручную действия для создания виртуальной машины и использование сценария Windows PowerShell для настройки служб Reporting Services на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="a4b54-109">Сценарий конфигурации включает в себя открытие порта брандмауэра для протоколов HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4b54-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="a4b54-110">Если протокол **HTTPS** на сервере отчетов не требуется, **пропустите шаг 2**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="a4b54-111">После создания виртуальной машины в шаге 1 перейдите в раздел "Использование сценария для настройки сервера отчетов и HTTP".</span><span class="sxs-lookup"><span data-stu-id="a4b54-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="a4b54-112">После выполнения сценария сервер отчетов будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="a4b54-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="a4b54-113">Предварительные требования и предположения</span><span class="sxs-lookup"><span data-stu-id="a4b54-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="a4b54-114">**Подписка Azure**: проверьте, какое количество ядер доступно в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="a4b54-115">При создании виртуальной машины рекомендуемого размера **A3** необходимо **4** доступных ядра.</span><span class="sxs-lookup"><span data-stu-id="a4b54-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="a4b54-116">При использовании виртуальной машины размера **A2** необходимо **2** доступных ядра.</span><span class="sxs-lookup"><span data-stu-id="a4b54-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="a4b54-117">Чтобы проверить ограничение для числа ядер в подписке, на классическом портале Azure щелкните элемент «ПАРАМЕТРЫ» на левой панели, а затем выберите «ИСПОЛЬЗОВАНИЕ» в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="a4b54-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="a4b54-118">Для увеличения квоты на ядра обратитесь в [службу поддержки Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="a4b54-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="a4b54-119">Дополнительные сведения о размере виртуальной машины см. в разделе [Размеры виртуальных машин в Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4b54-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a4b54-120">**Сценарии Windows PowerShell**: в данном разделе предполагается, что вы обладаете базовыми навыками работы с Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4b54-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="a4b54-121">Дополнительные сведения об использовании Windows PowerShell см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="a4b54-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="a4b54-122">Запуск Windows PowerShell в Windows Server</span><span class="sxs-lookup"><span data-stu-id="a4b54-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="a4b54-123">Приступая к работе с Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4b54-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="a4b54-124">Шаг 1. Подготовка виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="a4b54-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="a4b54-125">Перейдите на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="a4b54-126">Щелкните элемент **Виртуальные машины** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="a4b54-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![виртуальные машины microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="a4b54-128">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-128">Click **New**.</span></span>
   
    ![кнопка создания](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="a4b54-130">Щелкните **Из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-130">Click **From Gallery**.</span></span>
   
    ![новая виртуальная машина из коллекции](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="a4b54-132">Выберите **SQL Server 2014 RTM Standard — Windows Server 2012 R2** , а затем щелкните стрелку, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="a4b54-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="a4b54-134">Если вам необходима функция управляемых данными подписок в службах Reporting Services, выберите **SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="a4b54-135">Дополнительные сведения о выпусках SQL Server и поддержке различных функций см. на странице [Функции, поддерживаемые различными выпусками SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="a4b54-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="a4b54-136">На странице **Конфигурация виртуальной машины** измените следующие поля:</span><span class="sxs-lookup"><span data-stu-id="a4b54-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="a4b54-137">Если в поле **Дата выпуска версии**указано несколько значений, выберите самую последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="a4b54-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="a4b54-138">**Имя виртуальной машины**: имя машины также используется на следующей странице конфигурации в качестве DNS-имени облачной службы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4b54-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="a4b54-139">Это DNS-имя должно быть уникальным в пределах службы Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="a4b54-140">Рекомендуется настроить виртуальную машину с таким именем компьютера, которое описывает назначение данной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="a4b54-141">Например, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="a4b54-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="a4b54-142">**Уровень**: «Стандартный».</span><span class="sxs-lookup"><span data-stu-id="a4b54-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="a4b54-143">**Размер: A3**. Это рекомендуемый размер виртуальной машины для рабочих нагрузок SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4b54-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="a4b54-144">Если виртуальная машина используется только в качестве сервера отчетов, размера A2 достаточно, если только сервер отчетов не обрабатывает большой объем данных.</span><span class="sxs-lookup"><span data-stu-id="a4b54-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="a4b54-145">Для получения информации о ценах на виртуальные машины см. страницу [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="a4b54-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="a4b54-146">**Имя нового пользователя**. Указанное имя используется как имя администратора виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="a4b54-147">**Новый пароль** и **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="a4b54-148">Этот пароль используется для учетной записи администратора, поэтому рекомендуется использовать надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="a4b54-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="a4b54-149">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-149">Click **Next**.</span></span> <span data-ttu-id="a4b54-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="a4b54-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="a4b54-151">На следующей странице измените следующие поля:</span><span class="sxs-lookup"><span data-stu-id="a4b54-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="a4b54-152">**Облачная служба**: выберите **Создать новую облачную службу**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="a4b54-153">**DNS-имя облачной службы**. Это общедоступное DNS-имя облачной службы, связанной с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="a4b54-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="a4b54-154">По умолчанию используется имя, введенное в качестве имени виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="a4b54-155">Если в последующих разделах вы создадите доверенный SSL-сертификат, то в качестве значения параметра **Кому выдано** будет использоваться DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="a4b54-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="a4b54-156">**Регион, территориальная группа, виртуальная сеть**. Выберите регион, ближайший к конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="a4b54-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="a4b54-157">**Учетная запись хранения**. Используйте автоматически созданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a4b54-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="a4b54-158">**Группа доступности**: нет.</span><span class="sxs-lookup"><span data-stu-id="a4b54-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="a4b54-159">**Конечные точки**. Сохраните конечные точки **Удаленный рабочий стол** и **PowerShell**, а затем добавьте конечную точку HTTP или HTTPS в зависимости от вашей среды.</span><span class="sxs-lookup"><span data-stu-id="a4b54-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="a4b54-160">**HTTP**. Общий и частный порты по умолчанию имеют номер **80**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="a4b54-161">Обратите внимание, что при использовании частного порта, отличного от 80, следует изменить параметр **$HTTPport = 80** в сценарии HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4b54-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="a4b54-162">**HTTPS**. Общий и частный порты по умолчанию имеют номер **443**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="a4b54-163">Из соображений безопасности рекомендуется изменить частный порт и настроить брандмауэр и сервер отчетов на использование этого частного порта.</span><span class="sxs-lookup"><span data-stu-id="a4b54-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="a4b54-164">Дополнительную информацию о конечных точках см. в статье [Настройка связи с виртуальной машиной](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4b54-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="a4b54-165">Обратите внимание, что при использовании порта, отличного от 443, следует изменить параметр **$HTTPsport = 443** в сценарии HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4b54-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="a4b54-166">Нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="a4b54-166">Click next .</span></span> ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="a4b54-168">На последней странице мастера оставьте параметр по умолчанию **Установить агент ВМ**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="a4b54-169">В действиях, описанных в этом разделе, данный агент виртуальной машины не используется, но, если планируется сохранить эту виртуальную машину, агент и расширения позволят расширить ее возможности.</span><span class="sxs-lookup"><span data-stu-id="a4b54-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="a4b54-170">Дополнительные сведения об агенте ВМ см. в статье [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/) (Агент виртуальной машины и расширения. Часть 1).</span><span class="sxs-lookup"><span data-stu-id="a4b54-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="a4b54-171">Одним из установленных и запущенных расширений по умолчанию является BGINFO, которое отображает на рабочем столе виртуальной машины системные данные, такие как внутренний IP-адрес и свободное место на диске.</span><span class="sxs-lookup"><span data-stu-id="a4b54-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="a4b54-172">Щелкните «Готово».</span><span class="sxs-lookup"><span data-stu-id="a4b54-172">Click complete .</span></span> ![ОК](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="a4b54-174">Параметр **Состояние** виртуальной машины получает значение **Запуск (Подготовка)** во время процесса подготовки и значение **Выполняется**, когда виртуальная машина подготовлена и готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="a4b54-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="a4b54-175">Шаг 2. Создание сертификата сервера</span><span class="sxs-lookup"><span data-stu-id="a4b54-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="a4b54-176">Если протокол HTTPS на сервере отчетов не требуется, можно **пропустить шаг 2** и перейти к разделу **Использование сценария для настройки сервера отчетов и HTTP**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="a4b54-177">Воспользуйтесь сценарием HTTP, чтобы быстро настроить сервер отчетов и подготовить его к работе.</span><span class="sxs-lookup"><span data-stu-id="a4b54-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="a4b54-178">Для использования протокола HTTPS на виртуальной машине необходим доверенный SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="a4b54-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="a4b54-179">В зависимости от сценария можно использовать один из двух следующих способов:</span><span class="sxs-lookup"><span data-stu-id="a4b54-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="a4b54-180">Допустимый SSL-сертификат, выданный центром сертификации (ЦС) и являющийся доверенным для корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a4b54-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="a4b54-181">Сертификаты корневого ЦС должны распространяться по программе корневых сертификатов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a4b54-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="a4b54-182">Дополнительные сведения об этой программе см. на страницах [Программа корневых SSL-сертификатов Майкрософт (участвующие ЦС) Windows и Windows Phone 8](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) и [Общие сведения о программе корневых сертификатов корпорации Майкрософт](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="a4b54-183">Самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="a4b54-183">A self-signed certificate.</span></span> <span data-ttu-id="a4b54-184">Самозаверяющие сертификаты не рекомендуется использовать для рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="a4b54-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="a4b54-185">Использование сертификата, созданного доверенным центром сертификации (ЦС)</span><span class="sxs-lookup"><span data-stu-id="a4b54-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="a4b54-186">**Запросите сертификат сервера для веб-сайта из центра сертификации**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="a4b54-187">С помощью мастера сертификатов веб-сервера можно создать файл запроса на сертификат (Certreq.txt), который отправляется в центр сертификации, или создать запрос для сетевого центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="a4b54-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="a4b54-188">Например, службы сертификатов Майкрософт в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a4b54-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="a4b54-189">В зависимости от уровня контроля идентификации, обеспечиваемого сертификатом сервера, на утверждение запроса и отправку вам файла сертификата центру сертификации может потребоваться от нескольких дней до нескольких месяцев.</span><span class="sxs-lookup"><span data-stu-id="a4b54-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="a4b54-190">Дополнительные сведения о запросе сертификатов сервера см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="a4b54-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="a4b54-191">Использование [Certreq](https://technet.microsoft.com/library/cc725793.aspx).[](https://technet.microsoft.com/library/cc725793.aspx)</span><span class="sxs-lookup"><span data-stu-id="a4b54-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="a4b54-192">Средства безопасности для администрирования Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a4b54-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="a4b54-193">Средства безопасности для администрирования Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4b54-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="a4b54-194">Значение в поле **Кому выдан** доверенного SSL-сертификата должно совпадать со значением **DNS-имени облачной службы**, заданного для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="a4b54-195">**Установите сертификат сервера на веб-сервере**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="a4b54-196">Веб-сервер в этом случае представляет собой виртуальную машину, на которой размещен сервер отчетов, а веб-сайт создается позднее при настройке служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="a4b54-197">Дополнительные сведения об установке сертификата сервера на веб-сервере с помощью оснастки сертификатов MMC см. в разделе [Установка сертификата сервера](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="a4b54-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="a4b54-198">Если вы хотите использовать приведенный в этом разделе сценарий для настройки сервера отчетов, в качестве параметра сценария требуется указать значение сертификата **Отпечаток** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="a4b54-199">Сведения о том, как получить отпечаток сертификата, см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a4b54-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="a4b54-200">Назначьте сертификат сервера серверу отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="a4b54-201">Назначение завершается в следующем разделе после настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="a4b54-202">Использование самозаверяющего сертификата виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a4b54-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="a4b54-203">Самозаверяющий сертификат был создан на виртуальной машине при ее подготовке.</span><span class="sxs-lookup"><span data-stu-id="a4b54-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="a4b54-204">Имя этого сертификата совпадает с DNS-именем виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="a4b54-205">Во избежание ошибок сертификата необходимо, чтобы сертификат был доверенным как на самой виртуальной машине, а также для всех пользователей сайта.</span><span class="sxs-lookup"><span data-stu-id="a4b54-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="a4b54-206">Чтобы обеспечить доверие корневому ЦС сертификата на локальной виртуальной машине, добавьте этот сертификат в список **Доверенные корневые центры сертификации**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="a4b54-207">Ниже приведены сводные сведения о необходимых действиях.</span><span class="sxs-lookup"><span data-stu-id="a4b54-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="a4b54-208">Подробные инструкции по обеспечению доверия к ЦС см. в разделе [Установка сертификата сервера](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="a4b54-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="a4b54-209">На классическом портале Azure выберите виртуальную машину и щелкните команду подключения.</span><span class="sxs-lookup"><span data-stu-id="a4b54-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="a4b54-210">В зависимости от конфигурации браузера вам может быть предложено сохранить RDP-файл для подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![подключение к виртуальной машине Azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="a4b54-212">Используйте имя виртуальной машины, имя пользователя и пароль, которые были настроены при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="a4b54-213">Например, на следующем рисунке имя виртуальной машины — **ssrsnativecloud**, а имя пользователя — **testuser**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="a4b54-215">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="a4b54-215">Run mmc.exe.</span></span> <span data-ttu-id="a4b54-216">Дополнительные сведения см. в разделе [Практическое руководство. Просмотр сертификатов с помощью оснастки MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="a4b54-217">В меню **Файл** консольного приложения добавьте оснастку **Сертификаты**, при отображении запроса выберите **Учетная запись компьютера** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="a4b54-218">Выберите нужный **локальный компьютер** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="a4b54-219">Нажмите кнопку **ОК**, разверните узлы **Сертификаты — Личные** и щелкните элемент **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="a4b54-220">Имя сертификата совпадает с DNS-именем виртуальной машины и заканчивается на **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="a4b54-221">Щелкните правой кнопкой мыши имя сертификата и выберите пункт **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="a4b54-222">Разверните узел **Доверенные корневые центры сертификации**, щелкните правой кнопкой мыши элемент **Сертификаты** и выберите пункт **Вставить**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="a4b54-223">Для проверки дважды щелкните имя сертификата в области **Доверенные корневые центры сертификации** и убедитесь, что ошибки отсутствуют, а сам сертификат отображается.</span><span class="sxs-lookup"><span data-stu-id="a4b54-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="a4b54-224">Если вы хотите использовать приведенный в этом разделе сценарий HTTPS для настройки сервера отчетов, в качестве параметра сценария требуется указать значение сертификата **Отпечаток** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="a4b54-225">**Для получения значения отпечатка**воспользуйтесь приведенной ниже процедурой.</span><span class="sxs-lookup"><span data-stu-id="a4b54-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="a4b54-226">Существует также пример PowerShell по извлечению отпечатка в разделе [Использование сценария для настройки сервера отчетов и HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="a4b54-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="a4b54-227">Дважды щелкните имя сертификата, например ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="a4b54-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="a4b54-228">Откройте вкладку **Сведения** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="a4b54-229">Щелкните **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-229">Click **Thumbprint**.</span></span> <span data-ttu-id="a4b54-230">Значение отпечатка появится в поле сведений, например ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="a4b54-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="a4b54-231">Скопируйте отпечаток и сохраните значение для использования в дальнейшем либо отредактируйте сценарий прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="a4b54-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="a4b54-232">(*) Перед выполнением сценария удалите пробелы между парами значений.</span><span class="sxs-lookup"><span data-stu-id="a4b54-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="a4b54-233">Например, указанный выше отпечаток должен иметь вид ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="a4b54-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="a4b54-234">Назначьте сертификат сервера серверу отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="a4b54-235">Назначение завершается в следующем разделе после настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="a4b54-236">Если вы используете самозаверяющий SSL-сертификат, имя сертификата уже соответствует имени узла виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="a4b54-237">Таким образом, DNS-имя машины уже зарегистрировано на глобальном уровне и может использоваться с любого клиента.</span><span class="sxs-lookup"><span data-stu-id="a4b54-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="a4b54-238">Шаг 3. Настройка сервера отчетов</span><span class="sxs-lookup"><span data-stu-id="a4b54-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="a4b54-239">В этом разделе описывается настройка виртуальной машины в качестве сервера отчетов служб Reporting Services в собственном режиме.</span><span class="sxs-lookup"><span data-stu-id="a4b54-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="a4b54-240">Для настройки сервера отчетов можно использовать один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="a4b54-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="a4b54-241">Использование сценария для настройки сервера отчетов</span><span class="sxs-lookup"><span data-stu-id="a4b54-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="a4b54-242">Использование диспетчера конфигурации для настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="a4b54-243">Более подробные инструкции см. в разделе [Подключение к виртуальной машине и запуск диспетчера конфигурации служб Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="a4b54-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="a4b54-244">**Примечание о проверке подлинности.** Проверка подлинности Windows является рекомендуемым способом проверки подлинности и используется по умолчанию для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="a4b54-245">Только пользователи, которые настроены на виртуальной машине, могут осуществлять доступ к службам Reporting Services и назначаться ролям служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="a4b54-246">Использование сценария для настройки сервера отчетов и HTTP</span><span class="sxs-lookup"><span data-stu-id="a4b54-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="a4b54-247">Чтобы использовать сценарий Windows PowerShell для настройки сервера отчетов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a4b54-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="a4b54-248">Данная процедура настройки содержит указания для HTTP, но не для HTTPS:</span><span class="sxs-lookup"><span data-stu-id="a4b54-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="a4b54-249">На классическом портале Azure выберите виртуальную машину и щелкните команду подключения.</span><span class="sxs-lookup"><span data-stu-id="a4b54-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="a4b54-250">В зависимости от конфигурации браузера вам может быть предложено сохранить RDP-файл для подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![подключение к виртуальной машине Azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="a4b54-252">Используйте имя виртуальной машины, имя пользователя и пароль, которые были настроены при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="a4b54-253">Например, на следующем рисунке имя виртуальной машины — **ssrsnativecloud**, а имя пользователя — **testuser**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="a4b54-255">На виртуальной машине откройте **интегрированную среду сценариев Windows PowerShell** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4b54-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="a4b54-256">Интегрированная среда сценариев Windows PowerShell устанавливается по умолчанию в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a4b54-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="a4b54-257">Рекомендуется использовать интегрированную среду сценариев вместо стандартного окна Windows PowerShell, чтобы можно было вставить сценарий в эту среду, отредактировать его и выполнить.</span><span class="sxs-lookup"><span data-stu-id="a4b54-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="a4b54-258">В интегрированной среде сценариев Windows PowerShell откройте меню **Вид** и выберите **Показать область сценариев**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="a4b54-259">Скопируйте следующий сценарий и вставьте его в области сценариев интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4b54-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="a4b54-260">Если вы создали виртуальную машину с HTTP-портом, отличным от 80, измените параметр $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="a4b54-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="a4b54-261">Сценарий настроен для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="a4b54-262">Если вы хотите выполнить сценарий для служб Reporting Services, измените версию в пути пространства имен на значение v11 в операторе Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="a4b54-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="a4b54-263">Выполните скрипт.</span><span class="sxs-lookup"><span data-stu-id="a4b54-263">Run the script.</span></span>

<span data-ttu-id="a4b54-264">**Проверка**. Чтобы проверить работу базовых функций сервера отчетов, см. раздел [Проверка конфигурации](#verify-the-configuration) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a4b54-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="a4b54-265">Использование сценария для настройки сервера отчетов и HTTPS</span><span class="sxs-lookup"><span data-stu-id="a4b54-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="a4b54-266">Чтобы использовать Windows PowerShell для настройки сервера отчетов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a4b54-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="a4b54-267">Данная процедура настройки содержит указания для HTTPS, но не для HTTP:</span><span class="sxs-lookup"><span data-stu-id="a4b54-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="a4b54-268">На классическом портале Azure выберите виртуальную машину и щелкните команду подключения.</span><span class="sxs-lookup"><span data-stu-id="a4b54-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="a4b54-269">В зависимости от конфигурации браузера вам может быть предложено сохранить RDP-файл для подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![подключение к виртуальной машине Azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="a4b54-271">Используйте имя виртуальной машины, имя пользователя и пароль, которые были настроены при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="a4b54-272">Например, на следующем рисунке имя виртуальной машины — **ssrsnativecloud**, а имя пользователя — **testuser**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="a4b54-274">На виртуальной машине откройте **интегрированную среду сценариев Windows PowerShell** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4b54-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="a4b54-275">Интегрированная среда сценариев Windows PowerShell устанавливается по умолчанию в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a4b54-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="a4b54-276">Рекомендуется использовать интегрированную среду сценариев вместо стандартного окна Windows PowerShell, чтобы можно было вставить сценарий в эту среду, отредактировать его и выполнить.</span><span class="sxs-lookup"><span data-stu-id="a4b54-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="a4b54-277">Чтобы включить выполнение сценариев, выполните следующую команду Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4b54-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="a4b54-278">Для проверки политики можно выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4b54-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="a4b54-279">В **интегрированной среде сценариев Windows PowerShell** откройте меню **Вид** и выберите пункт **Показать область сценариев**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="a4b54-280">Скопируйте следующий сценарий и вставьте его в области сценариев интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4b54-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="a4b54-281">Измените параметр **$certificatehash** в сценарии:</span><span class="sxs-lookup"><span data-stu-id="a4b54-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="a4b54-282">Это **обязательный** параметр.</span><span class="sxs-lookup"><span data-stu-id="a4b54-282">This is a **required** parameter.</span></span> <span data-ttu-id="a4b54-283">Если вы не сохранили значение сертификата из предыдущих шагов, используйте один из следующих методов для копирования значение хэша сертификата из отпечатка сертификата:</span><span class="sxs-lookup"><span data-stu-id="a4b54-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="a4b54-284">На виртуальной машине откройте интегрированную среду сценариев Windows PowerShell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4b54-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="a4b54-285">Выходные данные будут выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a4b54-285">The output will look similar to the following.</span></span> <span data-ttu-id="a4b54-286">Если сценарий возвращает пустую строку, например, когда сертификат для виртуальной машины не настроен, см. раздел [Использование самозаверяющего сертификата виртуальных машин](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="a4b54-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="a4b54-287">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="a4b54-287">OR</span></span>
   * <span data-ttu-id="a4b54-288">На виртуальной машине выполните файл mmc.exe, а затем добавьте оснастку **Сертификаты** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="a4b54-289">В узле **Доверенные корневые центры сертификации** дважды щелкните имя сертификата.</span><span class="sxs-lookup"><span data-stu-id="a4b54-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="a4b54-290">При использовании самозаверяющего сертификата виртуальной машины имя сертификата совпадает с DNS-именем виртуальной машины и заканчивается на **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="a4b54-291">Откройте вкладку **Сведения** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="a4b54-292">Щелкните **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-292">Click **Thumbprint**.</span></span> <span data-ttu-id="a4b54-293">Значение отпечатка отображается в поле сведений, например af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48.</span><span class="sxs-lookup"><span data-stu-id="a4b54-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="a4b54-294">**Перед выполнением сценария**удалите пробелы между парами значений.</span><span class="sxs-lookup"><span data-stu-id="a4b54-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="a4b54-295">Например, af1160b64b288d890a8212ff6ba9c3664f319048.</span><span class="sxs-lookup"><span data-stu-id="a4b54-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="a4b54-296">Измените параметр **$httpsport** :</span><span class="sxs-lookup"><span data-stu-id="a4b54-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="a4b54-297">Если для конечной точки HTTPS использовался порт 443, обновлять этот параметр в сценарии не требуется.</span><span class="sxs-lookup"><span data-stu-id="a4b54-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="a4b54-298">В противном случае укажите значение порта, выбранное при настройке частной конечной точки HTTPS на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="a4b54-299">Измените параметр **$DNSName** :</span><span class="sxs-lookup"><span data-stu-id="a4b54-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="a4b54-300">Сценарий настроен для шаблона сертификата $DNSName="+".</span><span class="sxs-lookup"><span data-stu-id="a4b54-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="a4b54-301">Если вы не хотите настраивать привязку шаблона сертификата, закомментируйте $DNSName ="+"и включите следующую строку, полную ссылку $DNSNAme — ##$DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="a4b54-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="a4b54-302">Измените значение $DNSName, если не хотите использовать DNS-имя виртуальной машины для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="a4b54-303">Если этот параметр используется, сертификат также должен использовать это имя, а само имя следует глобально зарегистрировать на DNS-сервере.</span><span class="sxs-lookup"><span data-stu-id="a4b54-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="a4b54-304">Сценарий настроен для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="a4b54-305">Если вы хотите выполнить сценарий для служб Reporting Services, измените версию в пути пространства имен на значение v11 в операторе Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="a4b54-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="a4b54-306">Выполните скрипт.</span><span class="sxs-lookup"><span data-stu-id="a4b54-306">Run the script.</span></span>

<span data-ttu-id="a4b54-307">**Проверка**. Чтобы проверить работу базовых функций сервера отчетов, см. раздел [Проверка конфигурации](#verify-the-connection) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a4b54-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="a4b54-308">Чтобы проверить привязку сертификата, откройте командную строку с правами администратора и запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4b54-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="a4b54-309">Результат будет включать в себя следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a4b54-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="a4b54-310">Использование диспетчера конфигурации для настройки сервера отчетов</span><span class="sxs-lookup"><span data-stu-id="a4b54-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="a4b54-311">Если вы не хотите запускать сценарий PowerShell для настройки сервера отчетов, выполните действия, описанные в этом разделе, чтобы использовать диспетчер конфигурации служб Reporting Services в собственном режиме для настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="a4b54-312">На классическом портале Azure выберите виртуальную машину и щелкните команду подключения.</span><span class="sxs-lookup"><span data-stu-id="a4b54-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="a4b54-313">Используйте имя пользователя и пароль, которые были настроены при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![подключение к виртуальной машине Azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="a4b54-315">Запустите Центр обновления Windows и установите обновления для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="a4b54-316">Если требуется перезагрузка виртуальной машины, перезапустите ее и повторно подключитесь к ней с классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="a4b54-317">В меню "Пуск" на виртуальной машине введите **Reporting Services** и откройте **диспетчер конфигурации служб Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="a4b54-318">Оставьте значения по умолчанию для параметров **Имя сервера** и **Экземпляр сервера отчетов**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="a4b54-319">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-319">Click **Connect**.</span></span>
5. <span data-ttu-id="a4b54-320">Щелкните **URL-адрес веб-службы**на левой панели.</span><span class="sxs-lookup"><span data-stu-id="a4b54-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="a4b54-321">По умолчанию для служб Reporting Services задан HTTP-порт 80 с IP-адресом "Все назначенные".</span><span class="sxs-lookup"><span data-stu-id="a4b54-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="a4b54-322">Чтобы добавить HTTPS, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a4b54-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="a4b54-323">В поле **SSL-сертификат** выберите сертификат, который вы хотите использовать, например [имя виртуальной машины].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="a4b54-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="a4b54-324">Если сертификаты в списке отсутствуют, см. раздел **Шаг 2. Создание сертификата сервера** для получения сведений об установке сертификата и обеспечении доверия к нему на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="a4b54-325">В поле **SSL-порт**выберите значение 443.</span><span class="sxs-lookup"><span data-stu-id="a4b54-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="a4b54-326">Если вы настроили частную конечную точку HTTPS в виртуальной машине с другим частным портом, укажите это значение здесь.</span><span class="sxs-lookup"><span data-stu-id="a4b54-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="a4b54-327">Нажмите кнопку **Применить** и дождитесь завершения операции.</span><span class="sxs-lookup"><span data-stu-id="a4b54-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="a4b54-328">Щелкните элемент **База данных**на левой панели.</span><span class="sxs-lookup"><span data-stu-id="a4b54-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="a4b54-329">Щелкните **Изменение базы данных**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="a4b54-330">Щелкните элемент **Создать новую базу данных сервера отчетов** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="a4b54-331">Оставьте значение по умолчанию для параметра **Имя сервера**, в качестве которого используется имя виртуальной машины, а также оставьте для параметра **Тип проверки подлинности** значение по умолчанию **Текущий пользователь** — **Встроенная система безопасности**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="a4b54-332">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-332">Click **Next**.</span></span>
   4. <span data-ttu-id="a4b54-333">Оставьте значение по умолчанию для параметра **Имя базы данных** — **ReportServer** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="a4b54-334">Оставьте для параметра **Тип проверки подлинности** значение по умолчанию **Учетные данные службы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="a4b54-335">Щелкните элемент **Далее** on the **Далее** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="a4b54-336">Завершив настройку, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="a4b54-337">Щелкните элемент **URL-адрес диспетчера отчетов**на левой панели.</span><span class="sxs-lookup"><span data-stu-id="a4b54-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="a4b54-338">Оставьте для параметра **Виртуальный каталог** значение по умолчанию **Отчеты** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="a4b54-339">Щелкните **Выйти** , чтобы закрыть диспетчер конфигурации служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="a4b54-340">Шаг 4. Открытие порта в брандмауэре Windows</span><span class="sxs-lookup"><span data-stu-id="a4b54-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="a4b54-341">Этот раздел можно пропустить, если использовался один из сценариев для настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="a4b54-342">Такой сценарий содержит действие для открытия порта брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a4b54-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="a4b54-343">По умолчанию использовался порт 80 для HTTP и порт 443 для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4b54-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="a4b54-344">Для удаленного подключения к диспетчеру отчетов или серверу отчетов из виртуальной машины на ней должна присутствовать конечная точка TCP.</span><span class="sxs-lookup"><span data-stu-id="a4b54-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="a4b54-345">Необходимо открыть тот же самый порт в брандмауэре виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="a4b54-346">Эта конечная точка была создана при подготовке виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="a4b54-347">Данный раздел содержит основные сведения о том, как открыть порт брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a4b54-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="a4b54-348">Дополнительные сведения см. в статье [Настройка брандмауэра для доступа к серверу отчетов](https://technet.microsoft.com/library/bb934283.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="a4b54-349">Этот раздел можно пропустить, если использовался сценарий для настройки сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="a4b54-350">Такой сценарий содержит действие для открытия порта брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a4b54-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="a4b54-351">Если вы настроили для протокола HTTPS частный порт, отличный от 443, соответствующим образом измените следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="a4b54-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="a4b54-352">Чтобы открыть порт **443** в брандмауэре Windows, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a4b54-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="a4b54-353">Откройте окно Windows PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4b54-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="a4b54-354">Если при настройке конечной точки HTTPS на виртуальной машине вы использовали порт, отличный от 443, измените номер порта в следующей команде, а затем выполните ее:</span><span class="sxs-lookup"><span data-stu-id="a4b54-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="a4b54-355">Когда команда будет выполнена, в окне командной строки отобразится слово **ОК** .</span><span class="sxs-lookup"><span data-stu-id="a4b54-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="a4b54-356">Чтобы убедиться, что порт открыт, откройте окно Windows PowerShell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4b54-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="a4b54-357">Проверка конфигурации</span><span class="sxs-lookup"><span data-stu-id="a4b54-357">Verify the configuration</span></span>
<span data-ttu-id="a4b54-358">Чтобы убедиться, что базовые функции сервера отчетов теперь работают, откройте браузер с правами администратора и перейдите по следующим URL-адресам сервера отчетов и диспетчера отчетов:</span><span class="sxs-lookup"><span data-stu-id="a4b54-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="a4b54-359">На виртуальной машине перейдите по URL-адресу сервера отчетов:</span><span class="sxs-lookup"><span data-stu-id="a4b54-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="a4b54-360">На виртуальной машине перейдите по URL-адресу диспетчера отчетов:</span><span class="sxs-lookup"><span data-stu-id="a4b54-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="a4b54-361">На локальном компьютере перейдите к **удаленному** диспетчеру отчетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="a4b54-362">Соответствующим образом обновите DNS-имя в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a4b54-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="a4b54-363">При запросе пароля используйте учетные данные администратора, созданные при подготовке виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b54-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="a4b54-364">Имя пользователя имеет формат [домен] \[имя пользователя], где домен — это имя компьютера виртуальной машины, например ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="a4b54-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="a4b54-365">Если вы не используете HTTP**S**, удалите букву **s** в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="a4b54-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="a4b54-366">Сведения о создании дополнительных пользователей на виртуальной машине см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a4b54-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="a4b54-367">На локальном компьютере перейдите по URL-адресу удаленного сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="a4b54-368">Соответствующим образом обновите DNS-имя в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a4b54-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="a4b54-369">Если вы не используете HTTPS, удалите букву s в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="a4b54-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="a4b54-370">Создание пользователей и назначение ролей</span><span class="sxs-lookup"><span data-stu-id="a4b54-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="a4b54-371">После настройки и проверки сервера отчетов часто требуется создать одного или нескольких пользователей и назначить их ролям служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="a4b54-372">Дополнительную информацию см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="a4b54-372">For more information, see the following:</span></span>

* [<span data-ttu-id="a4b54-373">Создание локальной учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="a4b54-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="a4b54-374">[Предоставление пользователям доступа к серверу отчетов (диспетчеру отчетов)](https://msdn.microsoft.com/library/ms156034.aspx)</span><span class="sxs-lookup"><span data-stu-id="a4b54-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="a4b54-375">Создание назначений ролей и управление ими</span><span class="sxs-lookup"><span data-stu-id="a4b54-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="a4b54-376">Создание и публикация отчетов на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="a4b54-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="a4b54-377">В следующей таблице перечислены некоторые параметры, доступные для публикации существующих отчетов с локального компьютера на сервер отчетов, размещенный на виртуальной машине Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="a4b54-378">**Сценарий RS.exe**. Используйте сценарий RS.exe, чтобы скопировать элементы отчета с существующего сервера отчетов в виртуальную машину Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="a4b54-379">Дополнительные сведения см. в подразделе "С сервера отчетов в собственном режиме на другой сервер отчетов в собственном режиме — виртуальная машина Microsoft Azure" раздела [Образец скрипта программы rs.exe служб Reporting Services для копирования содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="a4b54-380">**Построитель отчетов**. Виртуальная машина включает в себя ClickOnce-версию построителя отчетов Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4b54-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="a4b54-381">Для первого запуска построителя отчетов на виртуальной машине выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a4b54-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="a4b54-382">Запустите браузер с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4b54-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="a4b54-383">Перейдите к диспетчеру отчетов на виртуальной машине и щелкните элемент **Построитель отчетов** на ленте.</span><span class="sxs-lookup"><span data-stu-id="a4b54-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="a4b54-384">Дополнительные сведения см. в статье [Установка, удаление и поддержка построителя отчетов](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="a4b54-385">**SQL Server Data Tools: виртуальная машина**. Если виртуальная машина была создана с помощью SQL Server 2012, компонент SQL Server Data Tools устанавливается на виртуальной машине и может использоваться для создания **проектов сервера отчетов** и отчетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="a4b54-386">SQL Server Data Tools может публиковать отчеты на сервере отчетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a4b54-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="a4b54-387">При создании виртуальной машины с помощью SQL Server 2014 можно установить SQL Server Data Tools — BI для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4b54-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="a4b54-388">Дополнительную информацию см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="a4b54-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="a4b54-389">Microsoft SQL Server Data Tools — бизнес-аналитика для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a4b54-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="a4b54-390">Microsoft SQL Server Data Tools — Business Intelligence для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a4b54-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="a4b54-391">SQL Server Data Tools и SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="a4b54-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="a4b54-392">**SQL Server Data Tools: удаленно**. Создайте на локальном компьютере проект служб Reporting Services в SQL Server Data Tools, содержащий отчеты служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="a4b54-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="a4b54-393">Настройте проект для подключения к URL-адресу веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a4b54-393">Configure the project to connect to the web service URL.</span></span>
  
    ![свойства проекта SSDT для проекта SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="a4b54-395">**Использование сценария**. Используйте сценарий для копирования содержимого сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="a4b54-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="a4b54-396">Дополнительные сведения см. в разделе [Образец скрипта программы rs.exe служб Reporting Services для копирования содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4b54-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="a4b54-397">Минимизация затрат на неиспользуемую виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="a4b54-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="a4b54-398">Чтобы свести к минимуму расходы на неиспользуемые виртуальные машины Azure, завершите работу виртуальной машины на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="a4b54-399">Если использовать для завершения работы виртуальной машины параметры электропитания Windows внутри нее, плата за эту виртуальную машину будет взиматься в полном объеме.</span><span class="sxs-lookup"><span data-stu-id="a4b54-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="a4b54-400">Для сокращения расходов необходимо завершить работу виртуальной машины на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b54-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="a4b54-401">Если виртуальная машина больше не нужна, не забудьте удалить ее и связанные с ней VHD-файлы во избежание расходов на хранение. Дополнительные сведения см. в разделе вопросов и ответов на странице [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="a4b54-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="a4b54-402">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="a4b54-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="a4b54-403">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="a4b54-403">Resources</span></span>
* <span data-ttu-id="a4b54-404">Аналогичные материалы, относящиеся к развертыванию SQL Server Business Intelligence и SharePoint 2013 с одним сервером, см. в статье [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx) (Использование PowerShell для создания ВМ Azure с помощью SQL Server BI и SharePoint 2013).</span><span class="sxs-lookup"><span data-stu-id="a4b54-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="a4b54-405">Похожие материалы о развертывании SQL Server Business Intelligence и SharePoint 2013 с несколькими серверами см. в статье [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx) (Развертывание Server Business Intelligence на виртуальных машинах Azure).</span><span class="sxs-lookup"><span data-stu-id="a4b54-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="a4b54-406">Общие сведения о развертываниях SQL Server Business Intelligence на виртуальных машинах Azure см. в статье [SQL Server Business Intelligence на виртуальных машинах Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a4b54-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="a4b54-407">Дополнительные сведения о стоимости вычислений Azure см. на вкладке "Виртуальные машины" [калькулятора цен Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="a4b54-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="a4b54-408">Материалы сообщества</span><span class="sxs-lookup"><span data-stu-id="a4b54-408">Community Content</span></span>
* <span data-ttu-id="a4b54-409">Пошаговые инструкции по созданию сервера отчетов служб Reporting Services в основном режиме без использования сценария см. в статье [Размещение служб SQL Reporting Services на виртуальной машине Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="a4b54-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="a4b54-410">Ссылки на другие ресурсы по работе SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="a4b54-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="a4b54-411">Обзор. SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="a4b54-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

