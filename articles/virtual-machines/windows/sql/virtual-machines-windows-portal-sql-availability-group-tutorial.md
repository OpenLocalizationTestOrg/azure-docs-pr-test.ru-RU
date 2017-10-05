---
title: "Руководство по использованию групп доступности SQL Server и виртуальных машин Azure | Документация Майкрософт"
description: "В этом руководстве показано, как создать группу доступности AlwaysOn SQL Server на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="e0b71-103">Настройка группы доступности AlwaysOn на виртуальной машине Azure вручную</span><span class="sxs-lookup"><span data-stu-id="e0b71-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="e0b71-104">В этом руководстве показано, как создать группу доступности AlwaysOn SQL Server на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="e0b71-105">Полная версия руководства позволяет создать группу доступности с репликой базы данных на двух серверах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="e0b71-106">**Оценка времени**. Потребуется около 30 минут (при условии, что предварительные требования уже выполнены).</span><span class="sxs-lookup"><span data-stu-id="e0b71-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="e0b71-107">На схеме ниже показаны шаги, которые описываются в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="e0b71-107">The diagram illustrates what you build in the tutorial.</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="e0b71-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0b71-109">Prerequisites</span></span>

<span data-ttu-id="e0b71-110">К данному руководству можно переходить, если у вас имеются базовое представление о группах доступности AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="e0b71-111">Если вы хотите узнать больше, ознакомьтесь с разделом [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0b71-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="e0b71-112">В следующей таблице перечислены предварительные условия, которые необходимо выполнить перед изучением данного руководства.</span><span class="sxs-lookup"><span data-stu-id="e0b71-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="e0b71-113">Требование</span><span class="sxs-lookup"><span data-stu-id="e0b71-113">Requirement</span></span> |<span data-ttu-id="e0b71-114">Описание</span><span class="sxs-lookup"><span data-stu-id="e0b71-114">Description</span></span> |
|----- |----- |----- |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="e0b71-116">Два сервера SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-116">Two SQL Servers</span></span> | <span data-ttu-id="e0b71-117">В группе доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="e0b71-118">В отдельном домене.</span><span class="sxs-lookup"><span data-stu-id="e0b71-118">- In a single domain</span></span> <br/> <span data-ttu-id="e0b71-119">С установленным компонентом отказоустойчивой кластеризации.</span><span class="sxs-lookup"><span data-stu-id="e0b71-119">- With Failover Clustering feature installed</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="e0b71-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-121">Windows Server</span></span> | <span data-ttu-id="e0b71-122">Файловый ресурс для свидетеля кластера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-122">File share for cluster witness</span></span> |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="e0b71-124">Учетная запись службы SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-124">SQL Server service account</span></span> | <span data-ttu-id="e0b71-125">Доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="e0b71-125">Domain account</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="e0b71-127">Учетная запись службы агента SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-127">SQL Server Agent service account</span></span> | <span data-ttu-id="e0b71-128">Доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="e0b71-128">Domain account</span></span> |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="e0b71-130">Открытые порты брандмауэра</span><span class="sxs-lookup"><span data-stu-id="e0b71-130">Firewall ports open</span></span> | <span data-ttu-id="e0b71-131">SQL Server: порт **1433** для экземпляра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e0b71-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="e0b71-132">Конечная точка зеркального отображения базы данных: порт **5022** или любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="e0b71-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="e0b71-133">Проба Azure Load Balancer: порт **59999** или любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="e0b71-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="e0b71-135">Добавление компонента отказоустойчивой кластеризации</span><span class="sxs-lookup"><span data-stu-id="e0b71-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="e0b71-136">Этот компонент нужен на обоих серверах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-136">Both SQL Servers require this feature</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="e0b71-138">Доменная учетная запись для установки</span><span class="sxs-lookup"><span data-stu-id="e0b71-138">Installation domain account</span></span> | <span data-ttu-id="e0b71-139">Локальный администратор на каждом сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="e0b71-140">Участник фиксированной роли сервера SQL Server sysadmin для каждого экземпляра SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="e0b71-141">Прежде чем приступить к этому руководству, необходимо [настроить необходимые компонентов для создания групп доступности AlwaysOn на виртуальных машинах Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="e0b71-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="e0b71-142">Если эти предварительные условия уже выполнены, то можно перейти к [созданию кластера](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="e0b71-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="e0b71-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Создание кластера</span><span class="sxs-lookup"><span data-stu-id="e0b71-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="e0b71-144">Первым шагом после выполнения предварительных условий является создание отказоустойчивого кластера Windows Server, включающего в себя два сервера SQL Server и следящий сервер.</span><span class="sxs-lookup"><span data-stu-id="e0b71-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="e0b71-145">Подключитесь по протоколу RDP к первому серверу SQL Server, используя доменную учетную запись с правами администратора для обоих серверов SQL Server и следящего сервера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="e0b71-146">Если вы следовали указаниям в [документе с предварительными требованиями](virtual-machines-windows-portal-sql-availability-group-prereq.md), то уже создали учетную запись **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="e0b71-147">Используйте ее.</span><span class="sxs-lookup"><span data-stu-id="e0b71-147">Use this account.</span></span>

2. <span data-ttu-id="e0b71-148">На панели мониторинга **Диспетчер серверов** выберите **Инструменты**, а затем **Диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="e0b71-149">В левой области щелкните правой кнопкой мыши **Диспетчер отказоустойчивости кластеров** и выберите **Создать кластер**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="e0b71-150">![Создание кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="e0b71-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="e0b71-151">В мастере создания кластеров создайте кластер с одним узлом, поэтапно настроив параметры на всех страницах, как указано в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="e0b71-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="e0b71-152">Страница</span><span class="sxs-lookup"><span data-stu-id="e0b71-152">Page</span></span> | <span data-ttu-id="e0b71-153">Параметры</span><span class="sxs-lookup"><span data-stu-id="e0b71-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="e0b71-154">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e0b71-154">Before You Begin</span></span> |<span data-ttu-id="e0b71-155">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="e0b71-155">Use defaults</span></span> |
   | <span data-ttu-id="e0b71-156">Выбор серверов</span><span class="sxs-lookup"><span data-stu-id="e0b71-156">Select Servers</span></span> |<span data-ttu-id="e0b71-157">Введите имя первого сервера SQL Server в поле **Введите имя сервера** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="e0b71-158">Предупреждение проверки</span><span class="sxs-lookup"><span data-stu-id="e0b71-158">Validation Warning</span></span> |<span data-ttu-id="e0b71-159">Выберите вариант **Нет. Для этого кластера не требуется поддержка корпорации Майкрософт, поэтому нет необходимости выполнять проверочные тесты. После нажатия кнопки "Далее" продолжить создание кластера**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="e0b71-160">Точка доступа для администрирования кластера</span><span class="sxs-lookup"><span data-stu-id="e0b71-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="e0b71-161">Введите имя кластера, например **SQLAGCluster1**, в поле **Имя кластера**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="e0b71-162">Подтверждение</span><span class="sxs-lookup"><span data-stu-id="e0b71-162">Confirmation</span></span> |<span data-ttu-id="e0b71-163">Используйте параметры по умолчанию, если вы не используете дисковые пространства.</span><span class="sxs-lookup"><span data-stu-id="e0b71-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="e0b71-164">Ознакомьтесь с примечанием после этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="e0b71-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="e0b71-165">Настройка IP-адреса кластера</span><span class="sxs-lookup"><span data-stu-id="e0b71-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="e0b71-166">В **диспетчере отказоустойчивости кластеров** прокрутите вниз до раздела **Ресурсы ядра кластера** и разверните сведения о кластере.</span><span class="sxs-lookup"><span data-stu-id="e0b71-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="e0b71-167">Вы увидите ресурсы **Имя** и **IP-адрес** с состоянием **Ошибка**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="e0b71-168">Ресурс IP-адреса невозможно подключить к сети, так как кластеру назначен тот же IP-адрес, что и виртуальной машине, то есть он повторяется.</span><span class="sxs-lookup"><span data-stu-id="e0b71-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="e0b71-169">Щелкните правой кнопкой мыши ресурс **IP-адреса** в состоянии сбоя и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Свойства кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="e0b71-171">Выберите **Статический IP-адрес** и укажите в текстовом поле "Адрес" доступный адрес из подсети, в которой находится сервер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="e0b71-172">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="e0b71-173">В разделе **Ресурсы ядра кластера** щелкните правой кнопкой мыши имя кластера и выберите **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="e0b71-174">Подождите, пока оба ресурса будут подключены.</span><span class="sxs-lookup"><span data-stu-id="e0b71-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="e0b71-175">Когда ресурс имени кластера подключится, он добавит на контроллер домена новую учетную запись компьютера Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="e0b71-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="e0b71-176">Эта учетная запись впоследствии будет использоваться для запуска кластерной службы группы доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="e0b71-177"><a name="addNode"></a>Добавление в кластер другого сервера SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="e0b71-178">Добавьте в кластер другой сервер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="e0b71-179">В дереве браузера щелкните правой кнопкой мыши кластер и выберите **Добавить узел**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Добавление узла в кластер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="e0b71-181">В **мастере добавления узлов** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="e0b71-182">На странице **Выбор серверов** добавьте второй сервер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="e0b71-183">Введите имя этого сервера в поле **Введите имя сервера** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="e0b71-184">Когда будете готовы, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="e0b71-185">На странице **Предупреждение проверки** нажмите кнопку **Нет** (в рабочем сценарии следует выполнить проверочные тесты).</span><span class="sxs-lookup"><span data-stu-id="e0b71-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="e0b71-186">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="e0b71-187">Если вы используете дисковые пространства, то на странице **Подтверждение** снимите флажок **Добавление всех допустимых хранилищ в кластер**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Подтверждение добавления узла](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="e0b71-189">Если вы используете дисковые пространства и не сняли флажок **Добавление всех допустимых хранилищ в кластер**, то Windows отключит виртуальные диски во время процесса кластеризации.</span><span class="sxs-lookup"><span data-stu-id="e0b71-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="e0b71-190">Как следствие, они не отобразятся в диспетчере дисков или Explorer, пока дисковые пространства не будут удалены из кластера и повторно подключены с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0b71-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="e0b71-191">Дисковые пространства группируют несколько дисков в пулы носителей.</span><span class="sxs-lookup"><span data-stu-id="e0b71-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="e0b71-192">Дополнительные сведения см. в статье [Обзор дисковых пространств](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="e0b71-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="e0b71-193">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-193">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-194">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e0b71-194">Click **Finish**.</span></span>

   <span data-ttu-id="e0b71-195">Диспетчер отказоустойчивости кластеров показывает, что в кластере появился новый узел. Он отображается в контейнере **Nodes**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="e0b71-196">Выйдите из сеанса удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e0b71-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="e0b71-197">Добавление файлового ресурса кворума кластера</span><span class="sxs-lookup"><span data-stu-id="e0b71-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="e0b71-198">В этом примере кластер Windows использует файловый ресурс для создания кворума кластера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="e0b71-199">В этом руководстве используется кворум "Большинство узлов и общих файловых ресурсов".</span><span class="sxs-lookup"><span data-stu-id="e0b71-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="e0b71-200">Дополнительные сведения см. в разделе [Общее представление о конфигурациях кворума в отказоустойчивом кластере](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0b71-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="e0b71-201">Подключитесь к рядовому серверу файлового ресурса-свидетеля с помощью сеанса удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e0b71-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="e0b71-202">В **диспетчере сервера** щелкните **Инструменты**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="e0b71-203">Щелкните **Управление компьютером**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="e0b71-204">Щелкните **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="e0b71-205">Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="e0b71-207">Используйте **мастер создания общих ресурсов**, чтобы создать общий ресурс.</span><span class="sxs-lookup"><span data-stu-id="e0b71-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="e0b71-208">Рядом с полем **Путь к папке** нажмите кнопку **Обзор** и укажите путь к общей папке, или создайте его, указав в этом поле.</span><span class="sxs-lookup"><span data-stu-id="e0b71-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="e0b71-209">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-209">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-210">В окне **Имя, описание и параметры** проверьте имя и путь общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0b71-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="e0b71-211">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-211">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-212">В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="e0b71-213">Щелкните **Настраиваемые…**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="e0b71-214">В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="e0b71-215">Убедитесь, что у учетной записи, используемой для создания кластера, имеется полный доступ.</span><span class="sxs-lookup"><span data-stu-id="e0b71-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="e0b71-217">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-217">Click **OK**.</span></span>

1. <span data-ttu-id="e0b71-218">В окне **Разрешения для общей папки** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="e0b71-219">Еще раз нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="e0b71-220">Выйдите с сервера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="e0b71-221">Настройка кворума кластера</span><span class="sxs-lookup"><span data-stu-id="e0b71-221">Configure cluster quorum</span></span>

<span data-ttu-id="e0b71-222">Теперь настройте кворум кластера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="e0b71-223">Подключитесь к первому узлу кластера с помощью сеанса удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e0b71-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="e0b71-224">В **диспетчере отказоустойчивости кластеров** щелкните кластер правой кнопкой мыши, наведите указатель на пункт **Дополнительные действия** и щелкните **Настройка параметров кворума кластера**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="e0b71-226">В **мастере настройки кворума кластера** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="e0b71-227">В окне **Выбор параметра конфигурации кворума** щелкните **Выбрать свидетель кворума** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="e0b71-228">В окне **Выбрать свидетель кворума** щелкните **Настроить файловый ресурс-свидетель**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="e0b71-229">Windows Server 2016 поддерживает облако-свидетель.</span><span class="sxs-lookup"><span data-stu-id="e0b71-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="e0b71-230">При выборе этого типа свидетеля файловый ресурс-свидетель не требуется.</span><span class="sxs-lookup"><span data-stu-id="e0b71-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="e0b71-231">Дополнительные сведения см. в разделе [Развертывание облачного следящего сервера для отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="e0b71-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="e0b71-232">В этом руководстве используется файловый ресурс-свидетель, который поддерживается в предыдущих операционных системах.</span><span class="sxs-lookup"><span data-stu-id="e0b71-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="e0b71-233">В поле **Настройка файлового ресурса-свидетеля** введите путь к созданному общему ресурсу.</span><span class="sxs-lookup"><span data-stu-id="e0b71-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="e0b71-234">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-234">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-235">Проверьте параметры в окне **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="e0b71-236">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-236">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-237">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e0b71-237">Click **Finish**.</span></span>

<span data-ttu-id="e0b71-238">Теперь ресурсы ядра кластера настроены для использования файлового ресурса-свидетеля.</span><span class="sxs-lookup"><span data-stu-id="e0b71-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="e0b71-239">Включение групп доступности</span><span class="sxs-lookup"><span data-stu-id="e0b71-239">Enable Availability Groups</span></span>

<span data-ttu-id="e0b71-240">Далее следует включить функцию **групп доступности AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="e0b71-241">Выполните эти шаги для обоих серверов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="e0b71-242">На **начальном экране** запустите **Диспетчер конфигурации SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="e0b71-243">В дереве обозревателя выберите **Службы SQL Server**, затем щелкните правой кнопкой мыши службу **SQL Server (MSSQLSERVER)** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="e0b71-244">Выберите вкладку **Высокая доступность AlwaysOn**, затем щелкните **Включить группы доступности AlwaysOn**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e0b71-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Включение групп доступности AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="e0b71-246">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-246">Click **Apply**.</span></span> <span data-ttu-id="e0b71-247">Нажмите кнопку **ОК** во всплывающем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="e0b71-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="e0b71-248">Перезапустите службу SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="e0b71-249">Повторите эти действия на другом сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="e0b71-250">Создание базы данных на первом сервере SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0b71-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="e0b71-251">Запустите RDP-файл подключения к первому серверу SQL Server с доменной учетной записью, которая является участником фиксированной серверной роли sysadmin.</span><span class="sxs-lookup"><span data-stu-id="e0b71-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="e0b71-252">Откройте SQL Server Management Studio и подключитесь к первому серверу SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="e0b71-253">В **обозревателе объектов** щелкните правой кнопкой мыши **Базы данных** и выберите пункт **Новая база данных**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="e0b71-254">В поле **Имя базы данных** введите **MyDB1**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="e0b71-255"><a name="backupshare"></a>Создание общего ресурса для резервных копий</span><span class="sxs-lookup"><span data-stu-id="e0b71-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="e0b71-256">На первом сервере SQL Server в **диспетчере сервера** щелкните **Инструменты**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="e0b71-257">Щелкните **Управление компьютером**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="e0b71-258">Щелкните **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="e0b71-259">Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="e0b71-261">Используйте **мастер создания общих ресурсов**, чтобы создать общий ресурс.</span><span class="sxs-lookup"><span data-stu-id="e0b71-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="e0b71-262">Рядом с полем **Путь к папке** нажмите кнопку **Обзор** и укажите путь к общей папке резервных копий баз данных, или создайте его, указав в этом поле.</span><span class="sxs-lookup"><span data-stu-id="e0b71-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="e0b71-263">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-263">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-264">В окне **Имя, описание и параметры** проверьте имя и путь общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0b71-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="e0b71-265">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-265">Click **Next**.</span></span>

1. <span data-ttu-id="e0b71-266">В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="e0b71-267">Щелкните **Настраиваемые…**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="e0b71-268">В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="e0b71-269">Убедитесь, что учетные записи службы SQL Server и агента службы SQL Server для обоих серверов имеют полный доступ.</span><span class="sxs-lookup"><span data-stu-id="e0b71-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="e0b71-271">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-271">Click **OK**.</span></span>

1. <span data-ttu-id="e0b71-272">В окне **Разрешения для общей папки** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="e0b71-273">Еще раз нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="e0b71-274">Создание полной резервной копии базы данных</span><span class="sxs-lookup"><span data-stu-id="e0b71-274">Take a full backup of the database</span></span>

<span data-ttu-id="e0b71-275">Необходимо создать резервную копию новой базы данных, чтобы инициализировать цепочку журналов.</span><span class="sxs-lookup"><span data-stu-id="e0b71-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="e0b71-276">Если не создать резервную копию новой базы данных, то ее невозможно будет добавить в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="e0b71-277">В **обозревателе объектов** щелкните правой кнопкой мыши базу данных, наведите указатель на пункт **Задачи…** и щелкните **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="e0b71-278">Нажмите кнопку **ОК**, чтобы создать полную резервную копию в расположении архива по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e0b71-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="e0b71-279">Создание группы доступности</span><span class="sxs-lookup"><span data-stu-id="e0b71-279">Create the Availability Group</span></span>
<span data-ttu-id="e0b71-280">Теперь все готово к настройке группы доступности. Для этого выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="e0b71-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="e0b71-281">Создайте базу данных на первом сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="e0b71-282">Создание полной резервной копии и резервной копии журнала транзакций базы данных.</span><span class="sxs-lookup"><span data-stu-id="e0b71-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="e0b71-283">Восстановите полную резервную копию и резервную копию журналов на второй сервер SQL Server с параметром **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="e0b71-284">Создайте группу доступности (**AG1**) с синхронной фиксацией, автоматической отработкой отказа и доступными для чтения вторичными репликами.</span><span class="sxs-lookup"><span data-stu-id="e0b71-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="e0b71-285">Создание группы доступности</span><span class="sxs-lookup"><span data-stu-id="e0b71-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="e0b71-286">Откройте сеанс удаленного рабочего стола для первого сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="e0b71-287">В **обозревателе объектов** в SSMS щелкните правой кнопкой мыши **Высокая доступность AlwaysOn** и выберите пункт **Мастер создания групп доступности**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Запуск мастера создания групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="e0b71-289">На странице **Введение** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="e0b71-290">На странице **Указание имени группы доступности** в поле **Имя группы доступности** введите имя группы доступности (например, **AG1**).</span><span class="sxs-lookup"><span data-stu-id="e0b71-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="e0b71-291">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-291">Click **Next**.</span></span>

    ![Мастер создания групп доступности, ввод имени групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="e0b71-293">На странице **Выбор баз данных** выберите свою базу данных и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e0b71-294">Эта база данных отвечает требованиям для создания группы доступности, так как вы создали для нее как минимум одну полную резервную копию на соответствующей первичной реплике.</span><span class="sxs-lookup"><span data-stu-id="e0b71-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![Мастер создания групп доступности, выбор баз данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="e0b71-296">На странице **Указание реплик** нажмите кнопку **Добавить реплику**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Мастер создания групп доступности, указание реплик](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="e0b71-298">Появится диалоговое окно **Подключение к серверу** .</span><span class="sxs-lookup"><span data-stu-id="e0b71-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="e0b71-299">Введите имя второго сервера в поле **Имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="e0b71-300">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-300">Click **Connect**.</span></span>

   <span data-ttu-id="e0b71-301">На странице **Указание реплик** в списке **Реплики доступности** должен отобразиться второй сервер.</span><span class="sxs-lookup"><span data-stu-id="e0b71-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="e0b71-302">Настройте реплики, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="e0b71-302">Configure the replicas as follows.</span></span>

   ![Мастер создания групп доступности, указание реплик (завершено)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="e0b71-304">Щелкните **Конечные точки**, чтобы просмотреть конечную точку зеркального отображения базы данных для этой группы доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="e0b71-305">Используйте тот же порт, что и при настройке [правила брандмауэра для конечных точек зеркального отображения базы данных](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="e0b71-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="e0b71-307">На странице **Выбор начальной синхронизации данных** выберите **Полная** и укажите сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="e0b71-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="e0b71-308">Это должен быть [созданный вами общий ресурс для резервных копий](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="e0b71-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="e0b71-309">В примере это была папка **\\\\\<First SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="e0b71-310">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e0b71-311">При полной синхронизации полная резервная копия базы данных создается на первом экземпляре SQL Server и восстанавливается на втором экземпляре.</span><span class="sxs-lookup"><span data-stu-id="e0b71-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="e0b71-312">Полная синхронизация не рекомендуется для больших баз данных, так как может занимать много времени.</span><span class="sxs-lookup"><span data-stu-id="e0b71-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="e0b71-313">Это время можно сократить, вручную создав резервную копию базы данных и восстановив ее с параметром `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="e0b71-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="e0b71-314">Если база данных уже была восстановлена с параметром `NO RECOVERY` на втором сервере SQL Server перед настройкой группы доступности, выберите переключатель **Только присоединение**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="e0b71-315">Если вы хотите создать резервную копию после настройки группы доступности, выберите переключатель **Пропустить начальную синхронизацию данных**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="e0b71-317">На странице **Проверка** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="e0b71-318">Эта страница должна выглядеть, как на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="e0b71-318">This page should look similar to the following image:</span></span>

    ![Мастер создания групп доступности, проверка](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="e0b71-320">Появится предупреждение о конфигурации прослушивателя группы доступности, так как он еще не настроен.</span><span class="sxs-lookup"><span data-stu-id="e0b71-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="e0b71-321">Это предупреждение можно игнорировать, так как на виртуальных машинах Azure создать прослушиватель можно и после создания Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e0b71-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="e0b71-322">На странице **Сводка** нажмите кнопку **Готово**, затем подождите, пока мастер настроит новую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="e0b71-323">На странице **Ход выполнения** вы можете нажать кнопку **Дополнительные сведения**, чтобы просмотреть подробности хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="e0b71-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="e0b71-324">Завершив работу с мастером, проверьте содержимое страницы **Результаты**, чтобы убедиться в том, что группа доступности успешно создана.</span><span class="sxs-lookup"><span data-stu-id="e0b71-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![Мастер создания групп доступности, результаты](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="e0b71-326">Нажмите кнопку **Закрыть**, чтобы выйти из мастера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="e0b71-327">Проверка группы доступности</span><span class="sxs-lookup"><span data-stu-id="e0b71-327">Check the Availability Group</span></span>

1. <span data-ttu-id="e0b71-328">В **обозревателе объектов** разверните элемент **Высокая доступность AlwaysOn**, а затем — элемент **Группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="e0b71-329">Теперь в этом контейнере должна появиться новая группа доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="e0b71-330">Щелкните ее правой кнопкой мыши и выберите пункт **Show Dashboard** (Показать панель мониторинга).</span><span class="sxs-lookup"><span data-stu-id="e0b71-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![Отображение панели мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="e0b71-332">**Панель мониторинга AlwaysOn** должна иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="e0b71-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![Панель мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="e0b71-334">Вы увидите реплики, режим отработки отказа для каждой из них и состояние синхронизации.</span><span class="sxs-lookup"><span data-stu-id="e0b71-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="e0b71-335">В **диспетчере отказоустойчивости кластеров** щелкните свой кластер.</span><span class="sxs-lookup"><span data-stu-id="e0b71-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="e0b71-336">Выберите **Роли**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-336">Select **Roles**.</span></span> <span data-ttu-id="e0b71-337">Имя группы доступности, которое вы использовали, представляет собой роль в кластере.</span><span class="sxs-lookup"><span data-stu-id="e0b71-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="e0b71-338">Так как вы не настроили прослушиватель, у этой группы доступности нет IP-адреса для подключений клиентов.</span><span class="sxs-lookup"><span data-stu-id="e0b71-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="e0b71-339">Вы настроите прослушиватель после создания Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e0b71-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="e0b71-341">Не пытайтесь выполнить отработку отказа для группы доступности через диспетчер отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="e0b71-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="e0b71-342">Все операции отработки отказов следует выполнять через **панель мониторинга AlwaysOn** в SSMS.</span><span class="sxs-lookup"><span data-stu-id="e0b71-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="e0b71-343">Дополнительные сведения см. в статье [Отказоустойчивая кластеризация и группы доступности AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0b71-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="e0b71-344">На этом этапе имеется группа доступности с репликами в двух экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="e0b71-345">Группу доступности можно перемещать между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="e0b71-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="e0b71-346">Пока что подключиться к группе доступности невозможно, так как отсутствует прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="e0b71-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="e0b71-347">В виртуальных машинах Azure для прослушивателя требуется подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="e0b71-348">Следующий шаг — создание подсистемы балансировки нагрузки в Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="e0b71-349">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e0b71-349">Create an Azure load balancer</span></span>

<span data-ttu-id="e0b71-350">Для группы доступности SQL Server на виртуальных машинах Azure необходима подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="e0b71-351">Подсистема балансировки нагрузки хранит IP-адрес для прослушивателя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="e0b71-352">В этом разделе кратко описывается, как создать подсистему балансировки нагрузки на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="e0b71-353">На портале Azure перейдите к группе ресурсов, содержащей ваши серверы SQL Server, и щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="e0b71-354">Найдите **балансировщик нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="e0b71-355">Выберите подсистему балансировки нагрузки, опубликованную корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e0b71-355">Choose the load balancer published by Microsoft.</span></span>

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="e0b71-357">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-357">Click **Create**.</span></span>
3. <span data-ttu-id="e0b71-358">Настройте следующие параметры для балансировщика нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e0b71-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="e0b71-359">Настройка</span><span class="sxs-lookup"><span data-stu-id="e0b71-359">Setting</span></span> | <span data-ttu-id="e0b71-360">Поле</span><span class="sxs-lookup"><span data-stu-id="e0b71-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="e0b71-361">**Имя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-361">**Name**</span></span> |<span data-ttu-id="e0b71-362">Используйте для подсистемы балансировки нагрузки текстовое имя, например **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="e0b71-363">**Тип**</span><span class="sxs-lookup"><span data-stu-id="e0b71-363">**Type**</span></span> |<span data-ttu-id="e0b71-364">Внутренний</span><span class="sxs-lookup"><span data-stu-id="e0b71-364">Internal</span></span> |
   | <span data-ttu-id="e0b71-365">**Виртуальная сеть**</span><span class="sxs-lookup"><span data-stu-id="e0b71-365">**Virtual network**</span></span> |<span data-ttu-id="e0b71-366">Используйте имя виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="e0b71-367">**Подсеть**</span><span class="sxs-lookup"><span data-stu-id="e0b71-367">**Subnet**</span></span> |<span data-ttu-id="e0b71-368">Используйте имя подсети, в которой находится виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e0b71-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="e0b71-369">**Назначение IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="e0b71-369">**IP address assignment**</span></span> |<span data-ttu-id="e0b71-370">Статическое</span><span class="sxs-lookup"><span data-stu-id="e0b71-370">Static</span></span> |
   | <span data-ttu-id="e0b71-371">**IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="e0b71-371">**IP address**</span></span> |<span data-ttu-id="e0b71-372">Используйте доступный адрес из подсети.</span><span class="sxs-lookup"><span data-stu-id="e0b71-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="e0b71-373">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="e0b71-373">**Subscription**</span></span> |<span data-ttu-id="e0b71-374">Используйте подписку, в которой находится виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e0b71-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="e0b71-375">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="e0b71-375">**Location**</span></span> |<span data-ttu-id="e0b71-376">Используйте расположение, в котором находится виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e0b71-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="e0b71-377">Колонка портала Azure должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e0b71-377">The Azure portal blade should look like this:</span></span>

   ![Создание балансировщика нагрузки](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="e0b71-379">Щелкните **Создать**, чтобы создать подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="e0b71-380">Для настройки подсистемы балансировки нагрузки необходимо создать внутренний пул, пробу и задать правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="e0b71-381">Это можно сделать на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="e0b71-382">Добавление внутреннего пула</span><span class="sxs-lookup"><span data-stu-id="e0b71-382">Add backend pool</span></span>

1. <span data-ttu-id="e0b71-383">На портале Azure перейдите к своей группе доступности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="e0b71-384">Может потребоваться обновить представление, чтобы отобразить только что созданную подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Поиск подсистемы балансировки нагрузки в группе ресурсов](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="e0b71-386">Выберите подсистему балансировки нагрузки, щелкните **Серверные пулы** и нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="e0b71-387">Задайте следующие параметры внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="e0b71-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="e0b71-388">Настройка</span><span class="sxs-lookup"><span data-stu-id="e0b71-388">Setting</span></span> | <span data-ttu-id="e0b71-389">Описание</span><span class="sxs-lookup"><span data-stu-id="e0b71-389">Description</span></span> | <span data-ttu-id="e0b71-390">Пример</span><span class="sxs-lookup"><span data-stu-id="e0b71-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="e0b71-391">**Имя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-391">**Name**</span></span> | <span data-ttu-id="e0b71-392">Введите текстовое имя.</span><span class="sxs-lookup"><span data-stu-id="e0b71-392">Type a text name</span></span> | <span data-ttu-id="e0b71-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="e0b71-393">SQLLBBE</span></span>
   | <span data-ttu-id="e0b71-394">**Сопоставлено с**</span><span class="sxs-lookup"><span data-stu-id="e0b71-394">**Associated to**</span></span> | <span data-ttu-id="e0b71-395">Выберите из списка</span><span class="sxs-lookup"><span data-stu-id="e0b71-395">Pick from list</span></span> | <span data-ttu-id="e0b71-396">Группа доступности</span><span class="sxs-lookup"><span data-stu-id="e0b71-396">Availability set</span></span>
   | <span data-ttu-id="e0b71-397">**группа доступности;**</span><span class="sxs-lookup"><span data-stu-id="e0b71-397">**Availability set**</span></span> | <span data-ttu-id="e0b71-398">Используйте имя группы доступности, в которой находятся виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="e0b71-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="e0b71-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="e0b71-400">**Виртуальные машины**</span><span class="sxs-lookup"><span data-stu-id="e0b71-400">**Virtual machines**</span></span> |<span data-ttu-id="e0b71-401">Имена двух виртуальных машин SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b71-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="e0b71-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="e0b71-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="e0b71-403">Введите имя для внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="e0b71-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="e0b71-404">Щелкните **+ Добавить виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="e0b71-405">Выберите группу доступности, содержащую серверы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="e0b71-406">В качестве виртуальных машин выберите оба сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="e0b71-407">Не следует добавлять сервер файлового ресурса-свидетеля.</span><span class="sxs-lookup"><span data-stu-id="e0b71-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="e0b71-408">Нажмите кнопку **ОК**, чтобы создать внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="e0b71-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="e0b71-409">Настройка пробы</span><span class="sxs-lookup"><span data-stu-id="e0b71-409">Set the probe</span></span>

1. <span data-ttu-id="e0b71-410">Выберите подсистему балансировки нагрузки, щелкните **Health probes** (Пробы работоспособности) и нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="e0b71-411">Настройте следующие параметры пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="e0b71-412">Настройка</span><span class="sxs-lookup"><span data-stu-id="e0b71-412">Setting</span></span> | <span data-ttu-id="e0b71-413">Описание</span><span class="sxs-lookup"><span data-stu-id="e0b71-413">Description</span></span> | <span data-ttu-id="e0b71-414">Пример</span><span class="sxs-lookup"><span data-stu-id="e0b71-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="e0b71-415">**Имя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-415">**Name**</span></span> | <span data-ttu-id="e0b71-416">текст</span><span class="sxs-lookup"><span data-stu-id="e0b71-416">Text</span></span> | <span data-ttu-id="e0b71-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="e0b71-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="e0b71-418">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="e0b71-418">**Protocol**</span></span> | <span data-ttu-id="e0b71-419">Выберите протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="e0b71-419">Choose TCP</span></span> | <span data-ttu-id="e0b71-420">TCP</span><span class="sxs-lookup"><span data-stu-id="e0b71-420">TCP</span></span> |
   | <span data-ttu-id="e0b71-421">**Порт**</span><span class="sxs-lookup"><span data-stu-id="e0b71-421">**Port**</span></span> | <span data-ttu-id="e0b71-422">Любой неиспользуемый порт.</span><span class="sxs-lookup"><span data-stu-id="e0b71-422">Any unused port</span></span> | <span data-ttu-id="e0b71-423">59999</span><span class="sxs-lookup"><span data-stu-id="e0b71-423">59999</span></span> |
   | <span data-ttu-id="e0b71-424">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="e0b71-424">**Interval**</span></span>  | <span data-ttu-id="e0b71-425">Промежуток времени между повторными попытками выполнения пробы в секундах.</span><span class="sxs-lookup"><span data-stu-id="e0b71-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="e0b71-426">5</span><span class="sxs-lookup"><span data-stu-id="e0b71-426">5</span></span> |
   | <span data-ttu-id="e0b71-427">**Пороговое значение сбоя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="e0b71-428">Число последовательных сбоев пробы, после которых виртуальная машина будет считаться неработоспособной.</span><span class="sxs-lookup"><span data-stu-id="e0b71-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="e0b71-429">2</span><span class="sxs-lookup"><span data-stu-id="e0b71-429">2</span></span> |

1. <span data-ttu-id="e0b71-430">Нажмите кнопку **ОК**, чтобы задать пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="e0b71-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="e0b71-431">Настройка правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e0b71-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="e0b71-432">Выберите подсистему балансировки нагрузки, щелкните **Правила балансировки нагрузки** и нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="e0b71-433">Настройте следующие правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="e0b71-434">Настройка</span><span class="sxs-lookup"><span data-stu-id="e0b71-434">Setting</span></span> | <span data-ttu-id="e0b71-435">Описание</span><span class="sxs-lookup"><span data-stu-id="e0b71-435">Description</span></span> | <span data-ttu-id="e0b71-436">Пример</span><span class="sxs-lookup"><span data-stu-id="e0b71-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="e0b71-437">**Имя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-437">**Name**</span></span> | <span data-ttu-id="e0b71-438">текст</span><span class="sxs-lookup"><span data-stu-id="e0b71-438">Text</span></span> | <span data-ttu-id="e0b71-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="e0b71-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="e0b71-440">**Frontend IP address** (Интерфейсный IP-адрес)</span><span class="sxs-lookup"><span data-stu-id="e0b71-440">**Frontend IP address**</span></span> | <span data-ttu-id="e0b71-441">Выберите адрес.</span><span class="sxs-lookup"><span data-stu-id="e0b71-441">Choose an address</span></span> |<span data-ttu-id="e0b71-442">Используйте адрес, который был создан при создании подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="e0b71-443">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="e0b71-443">**Protocol**</span></span> | <span data-ttu-id="e0b71-444">Выберите протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="e0b71-444">Choose TCP</span></span> |<span data-ttu-id="e0b71-445">TCP</span><span class="sxs-lookup"><span data-stu-id="e0b71-445">TCP</span></span> |
   | <span data-ttu-id="e0b71-446">**Порт**</span><span class="sxs-lookup"><span data-stu-id="e0b71-446">**Port**</span></span> | <span data-ttu-id="e0b71-447">Используйте порт экземпляра SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="e0b71-448">1433</span><span class="sxs-lookup"><span data-stu-id="e0b71-448">1433</span></span> |
   | <span data-ttu-id="e0b71-449">**Серверный порт**</span><span class="sxs-lookup"><span data-stu-id="e0b71-449">**Backend Port**</span></span> | <span data-ttu-id="e0b71-450">Это поле не используется, если задан плавающий IP-адрес для прямого ответа от сервера.</span><span class="sxs-lookup"><span data-stu-id="e0b71-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="e0b71-451">1433</span><span class="sxs-lookup"><span data-stu-id="e0b71-451">1433</span></span> |
   | <span data-ttu-id="e0b71-452">**Проба**</span><span class="sxs-lookup"><span data-stu-id="e0b71-452">**Probe**</span></span> |<span data-ttu-id="e0b71-453">Имя, указанное для пробы.</span><span class="sxs-lookup"><span data-stu-id="e0b71-453">The name you specified for the probe</span></span> | <span data-ttu-id="e0b71-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="e0b71-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="e0b71-455">**Сохранение сеанса**</span><span class="sxs-lookup"><span data-stu-id="e0b71-455">**Session Persistence**</span></span> | <span data-ttu-id="e0b71-456">Раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="e0b71-456">Drop down list</span></span> | <span data-ttu-id="e0b71-457">**None**</span><span class="sxs-lookup"><span data-stu-id="e0b71-457">**None**</span></span> |
   | <span data-ttu-id="e0b71-458">**Время ожидания простоя**</span><span class="sxs-lookup"><span data-stu-id="e0b71-458">**Idle Timeout**</span></span> | <span data-ttu-id="e0b71-459">Интервал (в минутах), в течение которого подключение TCP остается открытым.</span><span class="sxs-lookup"><span data-stu-id="e0b71-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="e0b71-460">4</span><span class="sxs-lookup"><span data-stu-id="e0b71-460">4</span></span> |
   | <span data-ttu-id="e0b71-461">**Плавающий IP-адрес (прямой ответ от сервера)**</span><span class="sxs-lookup"><span data-stu-id="e0b71-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="e0b71-462">Включено</span><span class="sxs-lookup"><span data-stu-id="e0b71-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="e0b71-463">Параметры прямого ответа от сервера задаются во время создания.</span><span class="sxs-lookup"><span data-stu-id="e0b71-463">Direct server return is set during creation.</span></span> <span data-ttu-id="e0b71-464">Их невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="e0b71-464">It cannot be changed.</span></span>

1. <span data-ttu-id="e0b71-465">Нажмите кнопку **ОК**, чтобы задать правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0b71-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="e0b71-466"><a name="configure-listener"></a>Настройка прослушивателя</span><span class="sxs-lookup"><span data-stu-id="e0b71-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="e0b71-467">Далее нужно настроить прослушиватель группы доступности в отказоустойчивом кластере.</span><span class="sxs-lookup"><span data-stu-id="e0b71-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b71-468">В этом руководстве показано, как создать отдельный прослушиватель с одним IP-адресом внутренней подсистемы балансировки нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="e0b71-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="e0b71-469">Чтобы создать один или несколько прослушивателей с использованием одного или нескольких IP-адресов, ознакомьтесь со статьей [Configure one or more Always On Availability Group Listeners - Resource Manager](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Настройка одного или нескольких прослушивателей группы доступности AlwaysOn в модели Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="e0b71-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="e0b71-470">Настройка порта прослушивателя</span><span class="sxs-lookup"><span data-stu-id="e0b71-470">Set listener port</span></span>

<span data-ttu-id="e0b71-471">Настройте порт прослушивателя в SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e0b71-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="e0b71-472">Запустите SQL Server Management Studio и подключитесь к основной реплике.</span><span class="sxs-lookup"><span data-stu-id="e0b71-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="e0b71-473">Перейдите в раздел **Высокий уровень доступности AlwaysOn** | **Группы доступности** | **Прослушиватели группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="e0b71-474">Теперь вы увидите имя прослушивателя, созданного в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="e0b71-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="e0b71-475">Щелкните правой кнопкой мыши имя прослушивателя и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="e0b71-476">В поле **Порт** укажите номер порта для прослушивателя группы доступности с помощью использованного ранее параметра $EndpointPort (по умолчанию использовалось значение 1433) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0b71-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="e0b71-477">Теперь у вас есть группа доступности SQL Server на виртуальных машинах Azure в режиме Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0b71-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="e0b71-478">Проверка подключения к прослушивателю</span><span class="sxs-lookup"><span data-stu-id="e0b71-478">Test connection to listener</span></span>

<span data-ttu-id="e0b71-479">Чтобы проверить подключение:</span><span class="sxs-lookup"><span data-stu-id="e0b71-479">To test the connection:</span></span>

1. <span data-ttu-id="e0b71-480">Подключитесь по протоколу RDP к серверу SQL Server, который находится в той же виртуальной сети, но не содержит реплику.</span><span class="sxs-lookup"><span data-stu-id="e0b71-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="e0b71-481">Можно использовать другой сервер SQL Server в кластере.</span><span class="sxs-lookup"><span data-stu-id="e0b71-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="e0b71-482">Для проверки подключения используйте служебную программу **sqlcmd** .</span><span class="sxs-lookup"><span data-stu-id="e0b71-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="e0b71-483">Например, в следующем сценарии **sqlcmd** подключается к основной реплике через прослушиватель с использованием аутентификации Windows.</span><span class="sxs-lookup"><span data-stu-id="e0b71-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="e0b71-484">Если прослушиватель использует порт, отличный от порта по умолчанию (1433), укажите порт в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="e0b71-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="e0b71-485">Например, следующая команда sqlcmd подключается к прослушивателю через порт 1435.</span><span class="sxs-lookup"><span data-stu-id="e0b71-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="e0b71-486">sqlcmd автоматически подключается к любому экземпляру SQL Server, на котором размещена основная реплика.</span><span class="sxs-lookup"><span data-stu-id="e0b71-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="e0b71-487">Указанный порт должен быть открыт в брандмауэре обоих серверов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0b71-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="e0b71-488">Для обоих серверов требуется правило для входящего трафика используемого TCP-порта.</span><span class="sxs-lookup"><span data-stu-id="e0b71-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="e0b71-489">Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0b71-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="e0b71-490">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0b71-490">Next steps</span></span>

- <span data-ttu-id="e0b71-491">[Добавление в подсистему балансировки нагрузки IP-адреса для второй группы доступности](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="e0b71-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
