---
title: "tooCreate PowerShell aaaUse ВМ с собственного сервера отчетов в режиме | Документы Microsoft"
description: "В этом разделе описываются и предоставляются пошаговые hello развертывание и настройку сервера отчетов собственный режим служб отчетов SQL Server на виртуальной машине Azure. "
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
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="60265-103">Использовать tooCreate PowerShell Azure ВМ с собственного режима сервера отчетов</span><span class="sxs-lookup"><span data-stu-id="60265-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="60265-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="60265-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="60265-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="60265-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="60265-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="60265-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="60265-107">В этом разделе описываются и предоставляются пошаговые hello развертывание и настройку сервера отчетов собственный режим служб отчетов SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="60265-108">Hello шаги в этом документе используется сочетание действий вручную toocreate hello виртуальной машины и сценарий Windows PowerShell tooconfigure Reporting Services на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="60265-109">Hello скрипт конфигурации включает Открытие порта брандмауэра для протоколов HTTP и HTTPs.</span><span class="sxs-lookup"><span data-stu-id="60265-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="60265-110">Если не требуется **HTTPS** на сервере отчетов hello **пропустите шаг 2**.</span><span class="sxs-lookup"><span data-stu-id="60265-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="60265-111">После создания виртуальной Машины hello в шаге 1, перейдите в раздел toohello использовать tooconfigure сценария hello сервер отчетов и HTTP.</span><span class="sxs-lookup"><span data-stu-id="60265-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="60265-112">После запуска сценария hello hello сервер отчетов будет готов toouse.</span><span class="sxs-lookup"><span data-stu-id="60265-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="60265-113">Предварительные требования и предположения</span><span class="sxs-lookup"><span data-stu-id="60265-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="60265-114">**Подписка Azure**: Проверьте hello количество ядер, доступных для вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="60265-115">Если вы создаете hello, рекомендуется использовать размер виртуальной Машины **A3**, требуется **4** доступных ядер.</span><span class="sxs-lookup"><span data-stu-id="60265-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="60265-116">При использовании виртуальной машины размера **A2** необходимо **2** доступных ядра.</span><span class="sxs-lookup"><span data-stu-id="60265-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="60265-117">Максимальное количество ядер hello tooverify для вашей подписки в hello классический портал Azure, щелкните параметры hello левой панели, а затем нажмите кнопку использование в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="60265-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="60265-118">tooincrease hello квоты ядер, обратитесь в службу [поддержки Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="60265-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="60265-119">Дополнительные сведения о размере виртуальной машины см. в разделе [Размеры виртуальных машин в Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60265-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="60265-120">**Скрипты Windows PowerShell**: hello раздела предполагает, что основные опыт работы с Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60265-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="60265-121">Дополнительные сведения об использовании Windows PowerShell см. в разделе hello следующее:</span><span class="sxs-lookup"><span data-stu-id="60265-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="60265-122">Запуск Windows PowerShell в Windows Server</span><span class="sxs-lookup"><span data-stu-id="60265-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="60265-123">Приступая к работе с Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="60265-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="60265-124">Шаг 1. Подготовка виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="60265-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="60265-125">Обзор toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="60265-126">Нажмите кнопку **виртуальные машины** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="60265-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![виртуальные машины microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="60265-128">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="60265-128">Click **New**.</span></span>
   
    ![кнопка создания](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="60265-130">Щелкните **Из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="60265-130">Click **From Gallery**.</span></span>
   
    ![новая виртуальная машина из коллекции](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="60265-132">Нажмите кнопку **SQL Server 2014 RTM Standard — Windows Server 2012 R2** и щелкните стрелку toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="60265-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="60265-134">Если вам требуются hello служб Reporting Services управляемые данными подписки, выберите **SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="60265-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="60265-135">Дополнительные сведения о выпусках SQL Server и поддержке функций см. в разделе [функции, поддерживаемые различными выпусками SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="60265-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="60265-136">На hello **конфигурации виртуальной машины** измените hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="60265-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="60265-137">Если имеется более одного **Дата выпуска версии**, выберите hello самой последней версии.</span><span class="sxs-lookup"><span data-stu-id="60265-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="60265-138">**Имя виртуальной машины**: hello имя компьютера используется на следующей странице конфигурации hello как имя DNS облачной службы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="60265-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="60265-139">имя DNS Hello должен быть уникальным для hello службы Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="60265-140">Рассмотрите возможность hello виртуальной Машины с именем компьютера, описывающий какие hello ВМ используется для.</span><span class="sxs-lookup"><span data-stu-id="60265-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="60265-141">Например, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="60265-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="60265-142">**Уровень**: «Стандартный».</span><span class="sxs-lookup"><span data-stu-id="60265-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="60265-143">**Размер: A3** hello рекомендуется использовать размер виртуальной Машины для рабочих нагрузок SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60265-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="60265-144">Если ВМ используется только как сервер отчетов, достаточно ВМ размера А2 если только сервер отчетов hello приходится обрабатывать значительные рабочие нагрузки.</span><span class="sxs-lookup"><span data-stu-id="60265-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="60265-145">Для получения информации о ценах на виртуальные машины см. страницу [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="60265-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="60265-146">**Новое имя пользователя**: hello именем создается с правами администратора на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="60265-147">**Новый пароль** и **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="60265-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="60265-148">Этот пароль используется для новой учетной записи администратора hello и рекомендуется использовать надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="60265-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="60265-149">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-149">Click **Next**.</span></span> <span data-ttu-id="60265-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="60265-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="60265-151">На следующей странице hello измените hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="60265-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="60265-152">**Облачная служба**: выберите **Создать новую облачную службу**.</span><span class="sxs-lookup"><span data-stu-id="60265-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="60265-153">**Облачные службы DNS-имя**: это hello открытому DNS-имени облачной службы, связанный с виртуальной Машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="60265-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="60265-154">Hello по умолчанию используется имя hello, введенного в hello имя виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="60265-155">Если на последующих этапах раздела hello Создание доверенного SSL-сертификата и затем hello DNS-имя используется для значения hello hello»**выдан**«hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="60265-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="60265-156">**Регион, территориальная группа или виртуальная сеть**: выберите hello области ближайший tooyour конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="60265-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="60265-157">**Учетная запись хранения**. Используйте автоматически созданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="60265-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="60265-158">**Группа доступности**: нет.</span><span class="sxs-lookup"><span data-stu-id="60265-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="60265-159">**Конечные ТОЧКИ** Keep hello **удаленного рабочего стола** и **PowerShell** конечные точки и затем добавить конечную точку HTTP или HTTPS, в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="60265-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="60265-160">**HTTP**: hello, общие и частные порты по умолчанию **80**.</span><span class="sxs-lookup"><span data-stu-id="60265-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="60265-161">Обратите внимание, что если вы используете частный порт, отличный от 80, измените **$HTTPport = 80** в скрипте http hello.</span><span class="sxs-lookup"><span data-stu-id="60265-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="60265-162">**HTTPS**: hello, общие и частные порты по умолчанию **443**.</span><span class="sxs-lookup"><span data-stu-id="60265-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="60265-163">Рекомендации по безопасности — toochange hello частный порт и настройте ваш брандмауэр и hello отчетов сервера toouse hello частный порт.</span><span class="sxs-lookup"><span data-stu-id="60265-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="60265-164">Дополнительные сведения о конечных точках см. в разделе [как tooSet Настройка обмена данными с виртуальной машиной](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60265-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="60265-165">Обратите внимание, что если используется другой порт, измените параметр hello **$HTTPsport = 443** в hello скрипт HTTPS.</span><span class="sxs-lookup"><span data-stu-id="60265-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="60265-166">Нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="60265-166">Click next .</span></span> ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="60265-168">На последней странице приветствия мастера hello, оставьте значение по умолчанию hello **установки агента виртуальной Машины hello** выбранных.</span><span class="sxs-lookup"><span data-stu-id="60265-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="60265-169">Hello действия, описанные в этом разделе не используют агент виртуальной Машины hello но если планируется tookeep эту виртуальную Машину, агент ВМ hello и расширения можно будет tooenhance he CM.</span><span class="sxs-lookup"><span data-stu-id="60265-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="60265-170">Дополнительные сведения о hello агент виртуальной Машины в разделе [агент ВМ и расширения — часть 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="60265-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="60265-171">Один запускающим рекламу расширения, установленные по умолчанию hello hello расширение BGINFO, который отображается на рабочем столе виртуальной Машины hello, системные сведения, такие как внутренний IP-адрес и свободного диска пространства.</span><span class="sxs-lookup"><span data-stu-id="60265-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="60265-172">Щелкните «Готово».</span><span class="sxs-lookup"><span data-stu-id="60265-172">Click complete .</span></span> ![ОК](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="60265-174">Hello **состояние** из виртуальной Машины отображается в виде hello **запуск (Подготовка)** во время процесса подготовки hello, а затем отображается как **под управлением** при hello виртуальная машина провизионирована и готова toouse.</span><span class="sxs-lookup"><span data-stu-id="60265-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="60265-175">Шаг 2. Создание сертификата сервера</span><span class="sxs-lookup"><span data-stu-id="60265-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="60265-176">Если не требуется HTTPS на сервере отчетов hello, вы можете **пропустите шаг 2** и перейдите в раздел toohello **использовать сервер отчетов hello tooconfigure скрипта и HTTP**.</span><span class="sxs-lookup"><span data-stu-id="60265-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="60265-177">Используйте hello HTTP сценария tooquickly Настройка сервера отчетов hello и hello отчетов, сервер будет готов toouse.</span><span class="sxs-lookup"><span data-stu-id="60265-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="60265-178">В порядке toouse HTTPS на hello виртуальной Машины необходим доверенный SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="60265-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="60265-179">В зависимости от вашего сценария можно использовать один из следующих двух методов hello:</span><span class="sxs-lookup"><span data-stu-id="60265-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="60265-180">Допустимый SSL-сертификат, выданный центром сертификации (ЦС) и являющийся доверенным для корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60265-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="60265-181">Сертификаты корневого ЦС Hello, требуется toobe распространяются через hello программы корневых сертификатов Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60265-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="60265-182">Дополнительные сведения об этой программе см. в разделе [Windows и программе корневых сертификатов для 8 Windows Phone SSL (член центра сертификации)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) и [toohello введение программы корневых сертификатов Майкрософт](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="60265-183">Самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="60265-183">A self-signed certificate.</span></span> <span data-ttu-id="60265-184">Самозаверяющие сертификаты не рекомендуется использовать для рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="60265-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="60265-185">toouse создать сертификат доверенного центра сертификации (ЦС)</span><span class="sxs-lookup"><span data-stu-id="60265-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="60265-186">**Запросите сертификат сервера для веб-сайта hello в центре сертификации**.</span><span class="sxs-lookup"><span data-stu-id="60265-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="60265-187">Можно использовать любой файл запроса сертификата (Certreq.txt), следует отправить tooa центром сертификации или toogenerate запрос для сетевого центра сертификации toogenerate приветствия мастера сертификатов веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="60265-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="60265-188">Например, службы сертификатов Майкрософт в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="60265-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="60265-189">В зависимости от уровня контроля идентификации, который обеспечивает сертификат сервера hello он несколько дней tooseveral месяцев в tooapprove центра сертификации hello запроса и выдачу файла сертификата.</span><span class="sxs-lookup"><span data-stu-id="60265-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="60265-190">Дополнительные сведения о запросе сертификатов сервера см. в следующем hello:</span><span class="sxs-lookup"><span data-stu-id="60265-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="60265-191">Использование [Certreq](https://technet.microsoft.com/library/cc725793.aspx).[](https://technet.microsoft.com/library/cc725793.aspx)</span><span class="sxs-lookup"><span data-stu-id="60265-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="60265-192">TooAdminister средств безопасности Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="60265-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="60265-193">TooAdminister средств безопасности Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="60265-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="60265-194">Hello **выдан** поле hello доверенного SSL-сертификат должен быть hello же, как hello **DNS-имя облачной службы** вы использовали для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="60265-195">**Установка сертификата сервера hello на веб-сервере hello**.</span><span class="sxs-lookup"><span data-stu-id="60265-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="60265-196">в этом случае Hello веб-сервера является hello виртуальной Машины, узлы hello сервера отчетов и веб-сайт hello создается позднее при настройке служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="60265-197">Дополнительные сведения об установке сертификата сервера hello на hello веб-сервере с помощью оснастки Certificate MMC hello см. в разделе [установить сертификат сервера](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="60265-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="60265-198">Если требуется toouse hello скрипт, приведенный в этом разделе, сервер отчетов tooconfigure hello, hello значение hello сертификатов **отпечаток** используется в качестве параметра скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="60265-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="60265-199">В подразделе hello Далее подробности о как tooobtain hello отпечаток сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="60265-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="60265-200">Назначение сервера отчетов toohello сертификат сервера hello.</span><span class="sxs-lookup"><span data-stu-id="60265-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="60265-201">При настройке сервера отчетов hello в следующем разделе hello завершения Hello назначения.</span><span class="sxs-lookup"><span data-stu-id="60265-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="60265-202">hello toouse самозаверяющего сертификата виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="60265-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="60265-203">Самозаверяющий сертификат был создан hello виртуальной Машины во время инициализации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="60265-204">Hello сертификат имеет точно такое же имя, как hello ВМ DNS-имя hello.</span><span class="sxs-lookup"><span data-stu-id="60265-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="60265-205">В ошибки сертификатов tooavoid заказ, она необходима, hello сертификат является доверенным на самой ВМ hello, а также всеми пользователями сайта hello.</span><span class="sxs-lookup"><span data-stu-id="60265-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="60265-206">tootrust hello корневого ЦС сертификата hello на hello локальной виртуальной Машины, добавьте hello сертификат toohello **доверенные корневые центры сертификации**.</span><span class="sxs-lookup"><span data-stu-id="60265-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="60265-207">Hello ниже приводится сводка необходимых шагов hello.</span><span class="sxs-lookup"><span data-stu-id="60265-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="60265-208">Подробные инструкции по как tootrust hello ЦС см. в разделе [установить сертификат сервера](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="60265-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="60265-209">Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить".</span><span class="sxs-lookup"><span data-stu-id="60265-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="60265-210">В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60265-212">Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="60265-213">Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="60265-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="60265-215">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="60265-215">Run mmc.exe.</span></span> <span data-ttu-id="60265-216">Дополнительные сведения см. в разделе [как: Просмотр сертификатов с hello оснастки MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="60265-217">В консольном приложении hello **файл** меню, добавить hello **сертификаты** оснастку, выберите **учетная запись компьютера** при появлении соответствующего запроса и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="60265-218">Выберите **локального компьютера** toomanage и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="60265-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="60265-219">Нажмите кнопку **ОК** и разверните hello **сертификаты — личных** узлов и нажмите кнопку **сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="60265-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="60265-220">Hello сертификат названные hello DNS-имя виртуальной Машины hello и заканчивается **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="60265-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="60265-221">Щелкните правой кнопкой мыши имя сертификата hello и нажмите кнопку **копирования**.</span><span class="sxs-lookup"><span data-stu-id="60265-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="60265-222">Разверните hello **доверенные корневые центры сертификации** узел и щелкните правой кнопкой **сертификаты** и нажмите кнопку **вставить**.</span><span class="sxs-lookup"><span data-stu-id="60265-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="60265-223">toovalidate, double, щелкните имя сертификата hello под **доверенные корневые центры сертификации** и убедитесь, что отсутствуют ошибки, и вы видите свой сертификат.</span><span class="sxs-lookup"><span data-stu-id="60265-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="60265-224">Если требуется toouse hello HTTPS скрипт, приведенный в этом разделе, сервер отчетов tooconfigure hello, hello значение hello сертификатов **отпечаток** используется в качестве параметра скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="60265-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="60265-225">**Значение отпечатка hello tooget**, выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="60265-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="60265-226">В разделе имеется также отпечаток PowerShell tooretrieve образец hello [сервер отчетов сценария tooconfigure hello и HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="60265-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="60265-227">Дважды щелкните имя сертификата hello, например ssrsnativecloud.cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="60265-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="60265-228">Нажмите кнопку hello **сведения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="60265-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="60265-229">Щелкните **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="60265-229">Click **Thumbprint**.</span></span> <span data-ttu-id="60265-230">значение Hello hello отпечатка появится в поле сведений о hello, например a6 08 3В df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="60265-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="60265-231">Скопируйте отпечаток hello и сохранить значение hello на более поздний срок или изменить скрипт hello сейчас.</span><span class="sxs-lookup"><span data-stu-id="60265-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="60265-232">(*) Перед запуском сценария hello, удалите hello пробелы между парами значений hello.</span><span class="sxs-lookup"><span data-stu-id="60265-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="60265-233">Например hello отпечаток, отмеченный ранее, теперь будет a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="60265-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="60265-234">Назначение сервера отчетов toohello сертификат сервера hello.</span><span class="sxs-lookup"><span data-stu-id="60265-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="60265-235">При настройке сервера отчетов hello в следующем разделе hello завершения Hello назначения.</span><span class="sxs-lookup"><span data-stu-id="60265-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="60265-236">Если вы используете самозаверяющий сертификат SSL, hello имя на сертификате hello уже соответствует hello узла hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="60265-237">Таким образом hello DNS hello машины уже зарегистрирована глобально и может осуществляться из любого клиента.</span><span class="sxs-lookup"><span data-stu-id="60265-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="60265-238">Шаг 3: Настройка сервера отчетов hello</span><span class="sxs-lookup"><span data-stu-id="60265-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="60265-239">В этом разделе описывается настройка hello виртуальной Машины, как сервер отчетов собственного режима служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="60265-240">Можно использовать один из следующий сервер отчетов hello tooconfigure методы hello:</span><span class="sxs-lookup"><span data-stu-id="60265-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="60265-241">Использовать hello сценария tooconfigure hello сервер отчетов</span><span class="sxs-lookup"><span data-stu-id="60265-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="60265-242">Здравствуйте, tooConfigure используйте диспетчер конфигурации сервера отчетов.</span><span class="sxs-lookup"><span data-stu-id="60265-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="60265-243">Подробные инструкции см. раздел hello [toohello подключение виртуальной машины и начала hello диспетчер конфигурации служб Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="60265-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="60265-244">**Примечание о проверке подлинности:** hello, рекомендуется использовать метод проверки подлинности — проверка подлинности Windows и проверка подлинности служб Reporting Services по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="60265-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="60265-245">Только пользователи, которые настроены на hello виртуальной Машины могут обращаться к службам отчетов и назначения ролей, служб tooReporting.</span><span class="sxs-lookup"><span data-stu-id="60265-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="60265-246">Использовать сценарий tooconfigure hello сервер отчетов и HTTP</span><span class="sxs-lookup"><span data-stu-id="60265-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="60265-247">toouse hello Windows PowerShell скрипт tooconfigure hello сервера отчетов, полный hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="60265-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="60265-248">Hello Настройка включает HTTP, HTTPS не:</span><span class="sxs-lookup"><span data-stu-id="60265-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="60265-249">Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить".</span><span class="sxs-lookup"><span data-stu-id="60265-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="60265-250">В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60265-252">Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="60265-253">Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="60265-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="60265-255">Откройте на hello виртуальной Машины, **интегрированной среды Сценариев Windows PowerShell** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="60265-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="60265-256">Hello интегрированной среды Сценариев PowerShell устанавливается по умолчанию в Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="60265-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="60265-257">Рекомендуется использовать hello ISE вместо стандартного окна Windows PowerShell, чтобы вставить скрипт hello в hello интегрированной среды Сценариев, измените сценарий hello и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="60265-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="60265-258">В Windows PowerShell ISE щелкните hello **представление** меню и нажмите кнопку **Показать область сценариев**.</span><span class="sxs-lookup"><span data-stu-id="60265-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="60265-259">Скопируйте следующий скрипт hello и вставьте сценарий hello в области сценариев интегрированной среды Сценариев Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="60265-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
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
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
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
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
5. <span data-ttu-id="60265-260">Если вы создали hello виртуальной Машины с HTTP-порт, отличный от 80, измените параметр hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="60265-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="60265-261">сценарий Hello в настоящее время настроен для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="60265-262">Скрипт hello toorun для служб Reporting Services, измените часть версии приветствия имен toohello пути hello слишком «v11» в инструкции Get-WmiObject hello.</span><span class="sxs-lookup"><span data-stu-id="60265-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="60265-263">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="60265-263">Run hello script.</span></span>

<span data-ttu-id="60265-264">**Проверка**: tooverify работы hello базовых функций сервера отчетов в разделе hello [конфигурации hello Убедитесь](#verify-the-configuration) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="60265-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="60265-265">Сервер отчетов сценария tooconfigure hello и HTTPS</span><span class="sxs-lookup"><span data-stu-id="60265-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="60265-266">toouse Windows PowerShell tooconfigure hello сервера отчетов, полный hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="60265-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="60265-267">Конфигурация Hello включает HTTPS, а не HTTP.</span><span class="sxs-lookup"><span data-stu-id="60265-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="60265-268">Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить".</span><span class="sxs-lookup"><span data-stu-id="60265-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="60265-269">В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60265-271">Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="60265-272">Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="60265-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="60265-274">Откройте на hello виртуальной Машины, **интегрированной среды Сценариев Windows PowerShell** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="60265-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="60265-275">Hello интегрированной среды Сценариев PowerShell устанавливается по умолчанию в Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="60265-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="60265-276">Рекомендуется использовать hello ISE вместо стандартного окна Windows PowerShell, чтобы вставить скрипт hello в hello интегрированной среды Сценариев, измените сценарий hello и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="60265-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="60265-277">выполнение скриптов, запустите следующую команду Windows PowerShell hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="60265-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="60265-278">Можно выполнять следующие политики hello tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="60265-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="60265-279">В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку hello **представление** меню и нажмите кнопку **Показать область сценариев**.</span><span class="sxs-lookup"><span data-stu-id="60265-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="60265-280">Скопируйте hello следующий скрипт и вставьте его в области сценариев интегрированной среды Сценариев Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="60265-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
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
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
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
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
6. <span data-ttu-id="60265-281">Изменение hello **$certificatehash** параметр в скрипте hello:</span><span class="sxs-lookup"><span data-stu-id="60265-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="60265-282">Это **обязательный** параметр.</span><span class="sxs-lookup"><span data-stu-id="60265-282">This is a **required** parameter.</span></span> <span data-ttu-id="60265-283">Если вы не сохраняли значение сертификата hello hello предыдущих шагах, используйте один из hello следующую хэш-значения методов toocopy hello сертификата из отпечатка сертификата hello.:</span><span class="sxs-lookup"><span data-stu-id="60265-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="60265-284">На hello виртуальной Машины откройте Windows PowerShell ISE и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="60265-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="60265-285">Hello результат будет выглядеть примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="60265-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="60265-286">Если hello скрипт возвращает пустую строку, hello виртуальная машина не имеет сертификата, настроенного для примера см. в разделе разделе hello [toouse hello самозаверяющего сертификата виртуальных машин](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="60265-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="60265-287">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="60265-287">OR</span></span>
   * <span data-ttu-id="60265-288">На hello mmc.exe запуска виртуальной Машины, а затем добавьте hello **сертификаты** оснастки.</span><span class="sxs-lookup"><span data-stu-id="60265-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="60265-289">В разделе hello **доверенные корневые центры сертификации** дважды щелкните имя своего сертификата.</span><span class="sxs-lookup"><span data-stu-id="60265-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="60265-290">При использовании самозаверяющего сертификата ВМ hello hello сертификат hello названные hello DNS-имя виртуальной Машины hello и заканчивается **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="60265-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="60265-291">Нажмите кнопку hello **сведения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="60265-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="60265-292">Щелкните **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="60265-292">Click **Thumbprint**.</span></span> <span data-ttu-id="60265-293">значение Hello hello отпечатка появится в поле сведений о hello, например af 11 60 b6 4b d 28 8 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="60265-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="60265-294">**Перед запуском сценария hello**, удалите hello пробелы между парами значений hello.</span><span class="sxs-lookup"><span data-stu-id="60265-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="60265-295">Например, af1160b64b288d890a8212ff6ba9c3664f319048.</span><span class="sxs-lookup"><span data-stu-id="60265-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="60265-296">Изменение hello **$httpsport** параметр:</span><span class="sxs-lookup"><span data-stu-id="60265-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="60265-297">Если используется порт 443 для конечной точки HTTPS hello, то вам не требуется tooupdate этот параметр в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="60265-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="60265-298">В противном случае используйте значение порта hello, выбранных при настройке частной конечной точки HTTPS hello на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="60265-299">Изменение hello **$DNSName** параметр:</span><span class="sxs-lookup"><span data-stu-id="60265-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="60265-300">скрипт Hello настроен для шаблона сертификата $DNSName = «+».</span><span class="sxs-lookup"><span data-stu-id="60265-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="60265-301">В противном случае tooconfigure не требуется для привязки шаблона сертификата, закомментируйте $DNSName = "+ «и включите следующие линии ссылку $DNSNAme полный hello, ## $DNSName="$server.cloudapp.net hello».</span><span class="sxs-lookup"><span data-stu-id="60265-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="60265-302">Измените значение hello $DNSName, если не хотите, чтобы DNS-имя toouse hello виртуальной машины для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="60265-303">При использовании параметра hello hello сертификат также должен использовать это имя и зарегистрировать имя hello глобально на DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="60265-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="60265-304">сценарий Hello в настоящее время настроен для служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="60265-305">Скрипт hello toorun для служб Reporting Services, измените часть версии приветствия имен toohello пути hello слишком «v11» в инструкции Get-WmiObject hello.</span><span class="sxs-lookup"><span data-stu-id="60265-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="60265-306">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="60265-306">Run hello script.</span></span>

<span data-ttu-id="60265-307">**Проверка**: tooverify работы hello базовых функций сервера отчетов в разделе hello [конфигурации hello Убедитесь](#verify-the-connection) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="60265-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="60265-308">привязки сертификата hello tooverify откройте командную строку с правами администратора и запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="60265-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="60265-309">Hello результат будет содержать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="60265-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="60265-310">Hello tooConfigure используйте диспетчер конфигурации сервера отчетов</span><span class="sxs-lookup"><span data-stu-id="60265-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="60265-311">Если не требуется toorun сценария PowerShell hello tooconfigure сервер отчетов hello, выполните действия hello в этот раздел toouse hello служб отчетов собственного режима сервера configuration manager tooconfigure hello отчета.</span><span class="sxs-lookup"><span data-stu-id="60265-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="60265-312">Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить".</span><span class="sxs-lookup"><span data-stu-id="60265-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="60265-313">Используйте hello имя пользователя и пароль, настроенные при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="60265-315">Запустите Центр обновления Windows и установите toohello обновления виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="60265-316">Если требуется перезагрузка hello виртуальной Машины, перезапустите hello виртуальной Машины и повторного подключения toohello виртуальной Машины из hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="60265-317">В меню Пуск hello на hello виртуальной Машины введите **служб Reporting Services** и откройте **диспетчер конфигурации служб Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="60265-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="60265-318">Оставьте значения по умолчанию hello **имя сервера** и **экземпляра сервера отчетов**.</span><span class="sxs-lookup"><span data-stu-id="60265-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="60265-319">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="60265-319">Click **Connect**.</span></span>
5. <span data-ttu-id="60265-320">Hello левой панели щелкните **URL веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="60265-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="60265-321">По умолчанию для служб Reporting Services задан HTTP-порт 80 с IP-адресом "Все назначенные".</span><span class="sxs-lookup"><span data-stu-id="60265-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="60265-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="60265-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="60265-323">В **SSL-сертификат**: hello выберите сертификат, который будет toouse, например [имя виртуальной Машины]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="60265-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="60265-324">Если сертификаты не указаны, в разделе hello **шаг 2: Создание сертификата сервера** сведения о hello как tooinstall и отношения доверия сертификата на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="60265-325">В поле **SSL-порт**выберите значение 443.</span><span class="sxs-lookup"><span data-stu-id="60265-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="60265-326">Если вы настроили частной конечной точки HTTPS hello в hello виртуальной Машины с другой частный порт, укажите это значение здесь.</span><span class="sxs-lookup"><span data-stu-id="60265-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="60265-327">Нажмите кнопку **применить** и дождитесь toocomplete операции hello.</span><span class="sxs-lookup"><span data-stu-id="60265-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="60265-328">Hello левой панели щелкните **базы данных**.</span><span class="sxs-lookup"><span data-stu-id="60265-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="60265-329">Щелкните **Изменение базы данных**.</span><span class="sxs-lookup"><span data-stu-id="60265-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="60265-330">Щелкните элемент **Создать новую базу данных сервера отчетов** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="60265-331">Оставьте по умолчанию hello **имя сервера**: виде hello виртуальной Машины именем и оставьте по умолчанию hello **тип проверки подлинности** как **текущего пользователя** — **встроенной безопасности**.</span><span class="sxs-lookup"><span data-stu-id="60265-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="60265-332">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-332">Click **Next**.</span></span>
   4. <span data-ttu-id="60265-333">Оставьте по умолчанию hello **имя базы данных** как **ReportServer** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="60265-334">Оставьте по умолчанию hello **тип проверки подлинности** как **учетные данные службы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="60265-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="60265-335">Нажмите кнопку **Далее** на hello **Сводка** страницы.</span><span class="sxs-lookup"><span data-stu-id="60265-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="60265-336">После завершения настройки hello, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="60265-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="60265-337">Hello левой панели щелкните **URL-адрес диспетчера отчетов**.</span><span class="sxs-lookup"><span data-stu-id="60265-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="60265-338">Оставьте по умолчанию hello **виртуальный каталог** как **отчеты** и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="60265-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="60265-339">Нажмите кнопку **выхода** tooclose hello диспетчер конфигурации служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="60265-340">Шаг 4. Открытие порта в брандмауэре Windows</span><span class="sxs-lookup"><span data-stu-id="60265-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="60265-341">Если используется один сервер отчетов hello tooconfigure сценарии hello, этот раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="60265-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="60265-342">скрипт Hello включено порт брандмауэра hello tooopen шаг.</span><span class="sxs-lookup"><span data-stu-id="60265-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="60265-343">по умолчанию Hello был порт 80 для HTTP и порт 443 для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="60265-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="60265-344">tooconnect удаленно tooReport Manager или hello-отчетов на hello виртуальной Машины требуется Server на виртуальной машине hello, конечной точке TCP.</span><span class="sxs-lookup"><span data-stu-id="60265-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="60265-345">Это обязательный tooopen hello же порт в брандмауэре ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="60265-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="60265-346">Конечная точка Hello был создан во время инициализации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="60265-347">В этом разделе приведены базовые сведения о как tooopen hello порт брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="60265-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="60265-348">Дополнительные сведения см. в статье [Настройка брандмауэра для доступа к серверу отчетов](https://technet.microsoft.com/library/bb934283.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="60265-349">Если используется сервер отчетов hello tooconfigure сценария hello, этот раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="60265-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="60265-350">скрипт Hello включено порт брандмауэра hello tooopen шаг.</span><span class="sxs-lookup"><span data-stu-id="60265-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="60265-351">Если вы настроили частный порт для протокола HTTPS, отличный от 443, измените следующий сценарий соответствующим образом hello.</span><span class="sxs-lookup"><span data-stu-id="60265-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="60265-352">порт tooopen **443** на hello брандмауэр Windows, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="60265-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="60265-353">Откройте окно Windows PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="60265-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="60265-354">Если используется другой порт, при настройке конечной точки HTTPS hello на hello виртуальной Машины, обновите порт hello в hello следующую команду, затем выполните команду hello:</span><span class="sxs-lookup"><span data-stu-id="60265-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="60265-355">После выполнения команды hello **ОК** отображается hello из командной строки.</span><span class="sxs-lookup"><span data-stu-id="60265-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="60265-356">tooverify, что открыт порт hello, откройте окно Windows PowerShell и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="60265-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="60265-357">Проверка конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="60265-357">Verify hello configuration</span></span>
<span data-ttu-id="60265-358">tooverify, теперь работает hello базовых функций сервера отчетов, откройте браузер с правами администратора, и сообщала диспетчера отчетов URL-адреса для сервера ad обзора toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="60265-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="60265-359">На hello ВМ откройте URL-адрес сервера отчетов toohello.</span><span class="sxs-lookup"><span data-stu-id="60265-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="60265-360">На hello ВМ откройте URL-адрес диспетчера отчетов toohello.</span><span class="sxs-lookup"><span data-stu-id="60265-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="60265-361">На локальном компьютере, откройте toohello **удаленного** диспетчера отчетов на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="60265-362">Обновите DNS-именем hello в hello следующий пример соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="60265-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="60265-363">При появлении запроса пароля используйте hello учетные данные администратора, созданный во время инициализации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="60265-364">имя пользователя Hello уже hello [домен]\[имя пользователя] формате, где имя компьютера ВМ hello, например ssrsnativecloud\testuser hello домена.</span><span class="sxs-lookup"><span data-stu-id="60265-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="60265-365">Если вы не используете HTTP**S**, удалите hello **s** в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="60265-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="60265-366">В разделе hello следующего раздела приведены сведения о создании дополнительных пользователей на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="60265-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="60265-367">С локального компьютера перейдите на URL-адрес сервера отчетов для удаленного toohello.</span><span class="sxs-lookup"><span data-stu-id="60265-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="60265-368">Обновите DNS-именем hello в hello следующий пример соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="60265-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="60265-369">Если вы не используете HTTPS, удалите hello s в URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="60265-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="60265-370">Создание пользователей и назначение ролей</span><span class="sxs-lookup"><span data-stu-id="60265-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="60265-371">После настройке и проверке hello сервером отчетов, общие задачи администрирования является toocreate одного или нескольких пользователей и назначить пользователей tooReporting служб ролей.</span><span class="sxs-lookup"><span data-stu-id="60265-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="60265-372">Дополнительные сведения см. в разделе hello следующее:</span><span class="sxs-lookup"><span data-stu-id="60265-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="60265-373">Создание локальной учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="60265-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="60265-374">[Предоставление пользователю доступа tooa сервера отчетов (диспетчер отчетов)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="60265-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="60265-375">Создание назначений ролей и управление ими</span><span class="sxs-lookup"><span data-stu-id="60265-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="60265-376">tooCreate и публиковать отчеты toohello виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="60265-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="60265-377">Hello следующей таблице перечислены некоторые hello параметры доступные toopublish существующие отчеты с сервера отчетов toohello компьютера в локальной среде, размещенной на виртуальной машине Microsoft Azure hello:</span><span class="sxs-lookup"><span data-stu-id="60265-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="60265-378">**Скрипт RS.exe**: RS.exe используйте скрипт toocopy отчета товары и сервер tooyour существующих отчетов виртуальной машине Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="60265-379">Дополнительные сведения см. в разделе hello раздел «tooNative собственный режим режиме — виртуальная машина Microsoft Azure» в [tooMigrate сценарий Sample Reporting Services rs.exe содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="60265-380">**Построитель отчетов**: hello виртуальной машины включает щелкните hello-версии ClickOnce построителя отчетов Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60265-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="60265-381">hello построителя отчетов toostart впервые hello виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="60265-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="60265-382">Запустите браузер с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="60265-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="60265-383">Обзор диспетчера tooreport на виртуальной машине hello и нажмите кнопку **построитель** на ленте «hello».</span><span class="sxs-lookup"><span data-stu-id="60265-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="60265-384">Дополнительные сведения см. в статье [Установка, удаление и поддержка построителя отчетов](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="60265-385">**SQL Server Data Tools: ВМ**: Если вы создали hello виртуальной Машины с SQL Server 2012, то SQL Server Data Tools, установленной на виртуальной машине hello и может принимать используется toocreate **проектов сервера отчетов** и отчеты о виртуальных hello компьютер.</span><span class="sxs-lookup"><span data-stu-id="60265-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="60265-386">SQL Server Data Tools можно опубликовать сервер отчетов toohello hello отчетов на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="60265-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="60265-387">Если вы создали hello виртуальной Машины с SQL server 2014, можно установить SQL Server Data Tools — BI для visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60265-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="60265-388">Дополнительные сведения см. в разделе hello следующее:</span><span class="sxs-lookup"><span data-stu-id="60265-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="60265-389">Microsoft SQL Server Data Tools — бизнес-аналитика для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="60265-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="60265-390">Microsoft SQL Server Data Tools — Business Intelligence для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="60265-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="60265-391">SQL Server Data Tools и SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="60265-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="60265-392">**SQL Server Data Tools: удаленно**. Создайте на локальном компьютере проект служб Reporting Services в SQL Server Data Tools, содержащий отчеты служб Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="60265-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="60265-393">Настройте URL hello проекта tooconnect toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="60265-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![свойства проекта SSDT для проекта SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="60265-395">**Использовать сценарий**: используйте содержимого сервера отчетов toocopy сценария.</span><span class="sxs-lookup"><span data-stu-id="60265-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="60265-396">Дополнительные сведения см. в разделе [tooMigrate сценарий Sample Reporting Services rs.exe содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="60265-397">Минимизация затрат, если вы не используете hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="60265-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="60265-398">плата за toominimize для виртуальных машин Azure не во время работы завершить работу hello виртуальной Машины из классического портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="60265-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="60265-399">При использовании параметров электропитания Windows hello внутри виртуальной Машины tooshut вниз hello ВМ взимается плата hello же сумму для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60265-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="60265-400">Оплата tooreduce, требуется tooshut вниз hello виртуальной Машины в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60265-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="60265-401">Если вы больше не нужна hello виртуальной Машины, запомнить hello toodelete ВМ и hello плата хранение tooavoid связанный VHD файлов. Дополнительные сведения см. раздел hello вопросы и ответы на [сведения о ценах на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="60265-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="60265-402">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="60265-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="60265-403">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="60265-403">Resources</span></span>
* <span data-ttu-id="60265-404">Аналогичное содержимое связанных tooa развертывания одного сервера SQL Server Business Intelligence и SharePoint 2013, см. [tooCreate с помощью Windows PowerShell ВМ Azure с SQL Server BI и SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="60265-405">Аналогичные содержимого связанных tooa развертывания с несколькими серверами SQL Server Business Intelligence и SharePoint 2013. в разделе [развертывание SQL Server Business Intelligence в виртуальных машинах Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="60265-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="60265-406">Дополнительные сведения см. связанные toodeployments SQL Server Business Intelligence в виртуальных машинах в Azure, [SQL Server Business Intelligence в виртуальных машинах Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="60265-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="60265-407">Дополнительные сведения о hello стоимости вычислительных затрат Azure см. в разделе вкладка виртуальных машин hello [калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="60265-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="60265-408">Материалы сообщества</span><span class="sxs-lookup"><span data-stu-id="60265-408">Community Content</span></span>
* <span data-ttu-id="60265-409">Пошаговые инструкции по как toocreate Reporting Services собственный режим сервера отчетов без использования скриптов см. в разделе [размещение службы SQL Reporting на виртуальной машине Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="60265-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="60265-410">Ссылки tooother ресурсы для SQL Server в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="60265-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="60265-411">Обзор. SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="60265-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

