---
title: "Учебник группы доступности сервера - виртуальных машинах Azure - aaaSQL | Документы Microsoft"
description: "В этом учебнике показано как toocreate всегда на группы доступности SQL Server на виртуальных машинах Azure."
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
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="34870-103">Настройка группы доступности AlwaysOn на виртуальной машине Azure вручную</span><span class="sxs-lookup"><span data-stu-id="34870-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="34870-104">В этом учебнике показано как toocreate всегда на группы доступности SQL Server на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="34870-105">весь учебник Hello создается группа доступности с репликой базы данных на двух серверах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="34870-106">**Примерное время**: занимает около 30 минут toocomplete после hello предварительных условий.</span><span class="sxs-lookup"><span data-stu-id="34870-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="34870-107">Hello диаграмме построения в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="34870-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="34870-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="34870-109">Prerequisites</span></span>

<span data-ttu-id="34870-110">Hello учебнике предполагается, что у вас есть базовое представление о SQL Server группы доступности AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="34870-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="34870-111">Если вы хотите узнать больше, ознакомьтесь с разделом [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="34870-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="34870-112">Hello следующей таблице перечислены необходимые условия hello необходимые toocomplete перед запуском этого учебника.</span><span class="sxs-lookup"><span data-stu-id="34870-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="34870-113">Требование</span><span class="sxs-lookup"><span data-stu-id="34870-113">Requirement</span></span> |<span data-ttu-id="34870-114">Описание</span><span class="sxs-lookup"><span data-stu-id="34870-114">Description</span></span> |
|----- |----- |----- |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="34870-116">Два сервера SQL Server</span><span class="sxs-lookup"><span data-stu-id="34870-116">Two SQL Servers</span></span> | <span data-ttu-id="34870-117">В группе доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="34870-118">В отдельном домене.</span><span class="sxs-lookup"><span data-stu-id="34870-118">- In a single domain</span></span> <br/> <span data-ttu-id="34870-119">С установленным компонентом отказоустойчивой кластеризации.</span><span class="sxs-lookup"><span data-stu-id="34870-119">- With Failover Clustering feature installed</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="34870-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="34870-121">Windows Server</span></span> | <span data-ttu-id="34870-122">Файловый ресурс для свидетеля кластера.</span><span class="sxs-lookup"><span data-stu-id="34870-122">File share for cluster witness</span></span> |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="34870-124">Учетная запись службы SQL Server</span><span class="sxs-lookup"><span data-stu-id="34870-124">SQL Server service account</span></span> | <span data-ttu-id="34870-125">Доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="34870-125">Domain account</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="34870-127">Учетная запись службы агента SQL Server</span><span class="sxs-lookup"><span data-stu-id="34870-127">SQL Server Agent service account</span></span> | <span data-ttu-id="34870-128">Доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="34870-128">Domain account</span></span> |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="34870-130">Открытые порты брандмауэра</span><span class="sxs-lookup"><span data-stu-id="34870-130">Firewall ports open</span></span> | <span data-ttu-id="34870-131">SQL Server: порт **1433** для экземпляра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="34870-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="34870-132">Конечная точка зеркального отображения базы данных: порт **5022** или любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="34870-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="34870-133">Проба Azure Load Balancer: порт **59999** или любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="34870-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="34870-135">Добавление компонента отказоустойчивой кластеризации</span><span class="sxs-lookup"><span data-stu-id="34870-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="34870-136">Этот компонент нужен на обоих серверах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-136">Both SQL Servers require this feature</span></span> |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="34870-138">Доменная учетная запись для установки</span><span class="sxs-lookup"><span data-stu-id="34870-138">Installation domain account</span></span> | <span data-ttu-id="34870-139">Локальный администратор на каждом сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="34870-140">Участник фиксированной роли сервера SQL Server sysadmin для каждого экземпляра SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="34870-141">Перед началом hello учебника необходимо слишком[выполните предварительные требования для создания группы доступности AlwaysOn в виртуальных машинах Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="34870-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="34870-142">Если эти условия являются уже завершена, можно легко слишком[создания кластеров](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="34870-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="34870-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="34870-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="34870-144">После приветствия необходимые условия выполнены hello первым шагом является toocreate отказоустойчивый кластер Windows Server с двумя серверами SQL Sever и следящего сервера.</span><span class="sxs-lookup"><span data-stu-id="34870-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="34870-145">RDP toohello первого SQL Server, используя учетную запись домена с правами администратора на серверах SQL и hello следящий сервер.</span><span class="sxs-lookup"><span data-stu-id="34870-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="34870-146">Если вы следовали hello [документ необходимых компонентов](virtual-machines-windows-portal-sql-availability-group-prereq.md), вы создали учетную запись называется **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="34870-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="34870-147">Используйте ее.</span><span class="sxs-lookup"><span data-stu-id="34870-147">Use this account.</span></span>

2. <span data-ttu-id="34870-148">В hello **диспетчера сервера** панели мониторинга, выберите **средства**, а затем нажмите кнопку **Диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="34870-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="34870-149">Hello левой панели щелкните правой кнопкой мыши **Диспетчер отказоустойчивости кластеров**, а затем нажмите кнопку **создать кластер**.</span><span class="sxs-lookup"><span data-stu-id="34870-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="34870-150">![Создание кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="34870-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="34870-151">В hello мастера создания кластера, создайте кластер с одним узлом, настроив hello страницы с параметрами hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="34870-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="34870-152">Страница</span><span class="sxs-lookup"><span data-stu-id="34870-152">Page</span></span> | <span data-ttu-id="34870-153">Параметры</span><span class="sxs-lookup"><span data-stu-id="34870-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="34870-154">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="34870-154">Before You Begin</span></span> |<span data-ttu-id="34870-155">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="34870-155">Use defaults</span></span> |
   | <span data-ttu-id="34870-156">Выбор серверов</span><span class="sxs-lookup"><span data-stu-id="34870-156">Select Servers</span></span> |<span data-ttu-id="34870-157">Тип hello, имя первого SQL Server в **введите имя сервера** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="34870-158">Предупреждение проверки</span><span class="sxs-lookup"><span data-stu-id="34870-158">Validation Warning</span></span> |<span data-ttu-id="34870-159">Выберите **проверяет, но мне не требуется поддержка Майкрософт для этого кластера, а не требуется проверка toorun hello. После нажатия кнопки Далее продолжить создание кластера hello**.</span><span class="sxs-lookup"><span data-stu-id="34870-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="34870-160">Точка доступа для hello администрирование кластера</span><span class="sxs-lookup"><span data-stu-id="34870-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="34870-161">Введите имя кластера, например **SQLAGCluster1**, в поле **Имя кластера**.</span><span class="sxs-lookup"><span data-stu-id="34870-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="34870-162">Подтверждение</span><span class="sxs-lookup"><span data-stu-id="34870-162">Confirmation</span></span> |<span data-ttu-id="34870-163">Используйте параметры по умолчанию, если вы не используете дисковые пространства.</span><span class="sxs-lookup"><span data-stu-id="34870-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="34870-164">См. Примечание hello после этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="34870-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="34870-165">Настройка IP-адреса кластера hello</span><span class="sxs-lookup"><span data-stu-id="34870-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="34870-166">В **Диспетчер отказоустойчивости кластеров**, прокрутите вниз слишком**основные ресурсы кластера** и разверните hello сведения о кластере.</span><span class="sxs-lookup"><span data-stu-id="34870-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="34870-167">Вы увидите обоих hello **имя** и hello **IP-адрес** ресурсы hello **сбой** состояния.</span><span class="sxs-lookup"><span data-stu-id="34870-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="34870-168">Hello ресурс IP-адреса не удается подключить из-за hello кластеру назначен hello же IP-адрес как самой машины hello, поэтому очень повторяющийся адрес.</span><span class="sxs-lookup"><span data-stu-id="34870-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="34870-169">Щелкните правой кнопкой мыши hello сбой **IP-адрес** ресурсов, а затем щелкните **свойства**.</span><span class="sxs-lookup"><span data-stu-id="34870-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Свойства кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="34870-171">Выберите **статический IP-адрес** и укажите доступный адрес из подсети, где hello SQL Server в текстовом поле адрес hello.</span><span class="sxs-lookup"><span data-stu-id="34870-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="34870-172">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="34870-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="34870-173">В hello **основные ресурсы кластера** щелкните правой кнопкой мыши имя кластера, щелкните **перевести в оперативный режим**.</span><span class="sxs-lookup"><span data-stu-id="34870-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="34870-174">Подождите, пока оба ресурса будут подключены.</span><span class="sxs-lookup"><span data-stu-id="34870-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="34870-175">Когда ресурс имени кластера hello станет доступной, hello сервер DC обновится новой учетной записи компьютера AD.</span><span class="sxs-lookup"><span data-stu-id="34870-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="34870-176">Используйте этот AD hello toorun учетной записи службы кластерные группы доступности в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="34870-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="34870-177"><a name="addNode"></a>Добавить hello других toocluster SQL Server</span><span class="sxs-lookup"><span data-stu-id="34870-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="34870-178">Добавить hello других toohello кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="34870-179">В дереве обозревателя hello, щелкните правой кнопкой мыши кластер hello и нажмите кнопку **добавления узла**.</span><span class="sxs-lookup"><span data-stu-id="34870-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Добавить toohello узла кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="34870-181">В hello **мастер добавления узла**, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="34870-182">В hello **Выбор серверов** добавьте hello второго SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="34870-183">Имя сервера типа hello в **введите имя сервера** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="34870-184">Когда будете готовы, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="34870-185">В hello **предупреждение проверки** щелкните **нет** (в рабочем сценарии необходимо выполнить проверочные тесты hello).</span><span class="sxs-lookup"><span data-stu-id="34870-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="34870-186">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="34870-187">В hello **Подтверждение** страницы при использовании дисковых пространств, hello снимите флажок **Добавление всех допустимых хранилищ toohello кластера.**</span><span class="sxs-lookup"><span data-stu-id="34870-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Подтверждение добавления узла](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="34870-189">Если вы используете дисковые пространства и не снимите флажок **Добавление всех допустимых хранилищ toohello кластера**, Windows hello виртуальные диски отсоединяет во время процесса кластеризации hello.</span><span class="sxs-lookup"><span data-stu-id="34870-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="34870-190">В результате они не отображаются в диспетчере дисков или проводнике только после удаления из кластера hello hello дисковых пространств и повторно подключены с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34870-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="34870-191">Дисковые пространства группируют несколько дисков в пулы toostorage.</span><span class="sxs-lookup"><span data-stu-id="34870-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="34870-192">Дополнительные сведения см. в статье [Обзор дисковых пространств](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="34870-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="34870-193">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-193">Click **Next**.</span></span>

1. <span data-ttu-id="34870-194">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="34870-194">Click **Finish**.</span></span>

   <span data-ttu-id="34870-195">Диспетчер отказоустойчивости кластеров показывает, что кластер имеет новый узел и указанный в hello **узлы** контейнера.</span><span class="sxs-lookup"><span data-stu-id="34870-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="34870-196">Выйдите из сеанса удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="34870-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="34870-197">Добавление файлового ресурса кворума кластера</span><span class="sxs-lookup"><span data-stu-id="34870-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="34870-198">В этом примере кластера Windows hello использует файл общего ресурса toocreate кворума кластера.</span><span class="sxs-lookup"><span data-stu-id="34870-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="34870-199">В этом руководстве используется кворум "Большинство узлов и общих файловых ресурсов".</span><span class="sxs-lookup"><span data-stu-id="34870-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="34870-200">Дополнительные сведения см. в разделе [Общее представление о конфигурациях кворума в отказоустойчивом кластере](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="34870-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="34870-201">Подключите следящий сервер toohello файл общий ресурс элемента с сеанс удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="34870-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="34870-202">В **диспетчере сервера** щелкните **Инструменты**.</span><span class="sxs-lookup"><span data-stu-id="34870-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="34870-203">Щелкните **Управление компьютером**.</span><span class="sxs-lookup"><span data-stu-id="34870-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="34870-204">Щелкните **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="34870-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="34870-205">Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.</span><span class="sxs-lookup"><span data-stu-id="34870-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="34870-207">Используйте **общих мастер создания папки** toocreate общую папку.</span><span class="sxs-lookup"><span data-stu-id="34870-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="34870-208">На **путь к папке**, нажмите кнопку **Обзор** и найдите или создайте путь к общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="34870-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="34870-209">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-209">Click **Next**.</span></span>

1. <span data-ttu-id="34870-210">В **имя, описание и параметры** проверьте hello сетевое имя и путь.</span><span class="sxs-lookup"><span data-stu-id="34870-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="34870-211">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-211">Click **Next**.</span></span>

1. <span data-ttu-id="34870-212">В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**.</span><span class="sxs-lookup"><span data-stu-id="34870-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="34870-213">Щелкните **Настраиваемые…**.</span><span class="sxs-lookup"><span data-stu-id="34870-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="34870-214">В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="34870-215">Убедитесь, что данный кластер hello hello toocreate учетная запись, используемая имеет полный доступ.</span><span class="sxs-lookup"><span data-stu-id="34870-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="34870-217">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="34870-217">Click **OK**.</span></span>

1. <span data-ttu-id="34870-218">В окне **Разрешения для общей папки** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="34870-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="34870-219">Еще раз нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="34870-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="34870-220">Выйдите из сервера hello</span><span class="sxs-lookup"><span data-stu-id="34870-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="34870-221">Настройка кворума кластера</span><span class="sxs-lookup"><span data-stu-id="34870-221">Configure cluster quorum</span></span>

<span data-ttu-id="34870-222">Затем задайте hello кворума кластера.</span><span class="sxs-lookup"><span data-stu-id="34870-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="34870-223">Первый узел кластера toohello подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="34870-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="34870-224">В **Диспетчер отказоустойчивости кластеров**, щелкните правой кнопкой мыши кластер hello, откройте пункт слишком**дополнительные действия**и нажмите кнопку **настроить параметры кворума кластера...** .</span><span class="sxs-lookup"><span data-stu-id="34870-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="34870-226">В **мастере настройки кворума кластера** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="34870-227">В **Выбор параметра конфигурации кворума**, выберите **Выбор свидетеля кворума hello**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="34870-228">В окне **Выбрать свидетель кворума** щелкните **Настроить файловый ресурс-свидетель**.</span><span class="sxs-lookup"><span data-stu-id="34870-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="34870-229">Windows Server 2016 поддерживает облако-свидетель.</span><span class="sxs-lookup"><span data-stu-id="34870-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="34870-230">При выборе этого типа свидетеля файловый ресурс-свидетель не требуется.</span><span class="sxs-lookup"><span data-stu-id="34870-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="34870-231">Дополнительные сведения см. в разделе [Развертывание облачного следящего сервера для отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="34870-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="34870-232">В этом руководстве используется файловый ресурс-свидетель, который поддерживается в предыдущих операционных системах.</span><span class="sxs-lookup"><span data-stu-id="34870-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="34870-233">На **Настройка файлового ресурса-свидетеля**, тип hello путь к общей папке hello, вы создали.</span><span class="sxs-lookup"><span data-stu-id="34870-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="34870-234">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-234">Click **Next**.</span></span>

1. <span data-ttu-id="34870-235">Проверьте параметры hello на **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="34870-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="34870-236">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-236">Click **Next**.</span></span>

1. <span data-ttu-id="34870-237">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="34870-237">Click **Finish**.</span></span>

<span data-ttu-id="34870-238">Основные ресурсы кластера Hello настроены файловый ресурс-свидетель.</span><span class="sxs-lookup"><span data-stu-id="34870-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="34870-239">Включение групп доступности</span><span class="sxs-lookup"><span data-stu-id="34870-239">Enable Availability Groups</span></span>

<span data-ttu-id="34870-240">Затем включите hello **группы доступности AlwaysOn** компонентов.</span><span class="sxs-lookup"><span data-stu-id="34870-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="34870-241">Выполните эти шаги для обоих серверов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="34870-242">Из hello **запустить** экрана, запустить **диспетчер конфигурации SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="34870-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="34870-243">В дереве обозревателя hello выберите **служб SQL Server**, щелкните правой кнопкой мыши hello **SQL Server (MSSQLSERVER)** службы и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="34870-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="34870-244">Нажмите кнопку hello **высокий уровень доступности AlwaysOn** , затем выберите **включить группы доступности AlwaysOn**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="34870-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Включение групп доступности AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="34870-246">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="34870-246">Click **Apply**.</span></span> <span data-ttu-id="34870-247">Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="34870-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="34870-248">Перезапустите службу SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="34870-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="34870-249">Повторите эти действия на hello другие серверы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="34870-250">Создание базы данных на hello первого SQL Server</span><span class="sxs-lookup"><span data-stu-id="34870-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="34870-251">Запустите RDP hello файл toohello первого SQL Server в домене учетной записи, то есть членом роли sysadmin предопределенной роли сервера.</span><span class="sxs-lookup"><span data-stu-id="34870-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="34870-252">Откройте среду SQL Server Management Studio и подключитесь toohello первого SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="34870-253">В **обозревателе объектов** щелкните правой кнопкой мыши **Базы данных** и выберите пункт **Новая база данных**.</span><span class="sxs-lookup"><span data-stu-id="34870-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="34870-254">В поле **Имя базы данных** введите **MyDB1**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="34870-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="34870-255"><a name="backupshare"></a>Создание общего ресурса для резервных копий</span><span class="sxs-lookup"><span data-stu-id="34870-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="34870-256">На hello первого SQL Server в **диспетчера сервера**, нажмите кнопку **средства**.</span><span class="sxs-lookup"><span data-stu-id="34870-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="34870-257">Щелкните **Управление компьютером**.</span><span class="sxs-lookup"><span data-stu-id="34870-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="34870-258">Щелкните **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="34870-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="34870-259">Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.</span><span class="sxs-lookup"><span data-stu-id="34870-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="34870-261">Используйте **общих мастер создания папки** toocreate общую папку.</span><span class="sxs-lookup"><span data-stu-id="34870-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="34870-262">На **путь к папке**, нажмите кнопку **Обзор** и найдите или создайте путь к общей папке с резервной копии hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="34870-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="34870-263">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-263">Click **Next**.</span></span>

1. <span data-ttu-id="34870-264">В **имя, описание и параметры** проверьте hello сетевое имя и путь.</span><span class="sxs-lookup"><span data-stu-id="34870-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="34870-265">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-265">Click **Next**.</span></span>

1. <span data-ttu-id="34870-266">В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**.</span><span class="sxs-lookup"><span data-stu-id="34870-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="34870-267">Щелкните **Настраиваемые…**.</span><span class="sxs-lookup"><span data-stu-id="34870-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="34870-268">В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="34870-269">Убедитесь, что hello SQL Server и агент SQL Server учетные записи служб для обоих серверов имеют полный доступ.</span><span class="sxs-lookup"><span data-stu-id="34870-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="34870-271">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="34870-271">Click **OK**.</span></span>

1. <span data-ttu-id="34870-272">В окне **Разрешения для общей папки** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="34870-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="34870-273">Еще раз нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="34870-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="34870-274">Создайте полную резервную копию базы данных hello</span><span class="sxs-lookup"><span data-stu-id="34870-274">Take a full backup of hello database</span></span>

<span data-ttu-id="34870-275">Необходимо tooback копирование hello новую базу данных tooinitialize hello цепочку журналов.</span><span class="sxs-lookup"><span data-stu-id="34870-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="34870-276">Если резервная копия hello новой базы данных не выполняется, он не включен в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="34870-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="34870-277">В **обозревателя объектов**щелкните hello базы данных, укажите слишком**задач...** , нажмите кнопку **резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="34870-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="34870-278">Нажмите кнопку **ОК** tootake местоположение резервных копий по умолчанию toohello полного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="34870-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="34870-279">Создание группы доступности hello</span><span class="sxs-lookup"><span data-stu-id="34870-279">Create hello Availability Group</span></span>
<span data-ttu-id="34870-280">Теперь будут готовы tooconfigure, группу доступности с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="34870-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="34870-281">Создание базы данных на hello первого SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="34870-282">Отключите полной резервной копии и резервной копии журнала транзакций базы данных hello</span><span class="sxs-lookup"><span data-stu-id="34870-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="34870-283">Hello восстановление полной и второй сервер SQL с hello toohello резервные копии журналов **NORECOVERY** параметр</span><span class="sxs-lookup"><span data-stu-id="34870-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="34870-284">Создание группы доступности hello (**AG1**) с синхронной фиксацией, автоматической отработки отказа и вторичные реплики для чтения</span><span class="sxs-lookup"><span data-stu-id="34870-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="34870-285">Создание группы доступности hello:</span><span class="sxs-lookup"><span data-stu-id="34870-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="34870-286">В сеансе удаленного рабочего стола toohello первого SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="34870-287">В **обозревателе объектов** в SSMS щелкните правой кнопкой мыши **Высокая доступность AlwaysOn** и выберите пункт **Мастер создания групп доступности**.</span><span class="sxs-lookup"><span data-stu-id="34870-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Запуск мастера создания групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="34870-289">В hello **Введение** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="34870-290">В hello **Указание имени группы доступности** введите имя для hello группы доступности, например **AG1**в **имя группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="34870-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="34870-291">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-291">Click **Next**.</span></span>

    ![Мастер создания групп доступности, ввод имени групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="34870-293">В hello **Выбор баз данных** , выберите вашу базу данных и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="34870-294">Hello базы данных предварительным требованиям hello для группы доступности из-за выполнения по крайней мере одну полную резервную копию на hello целевой первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="34870-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Мастер создания групп доступности, выбор баз данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="34870-296">В hello **Выбор реплик** щелкните **добавления реплики**.</span><span class="sxs-lookup"><span data-stu-id="34870-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Мастер создания групп доступности, указание реплик](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="34870-298">Hello **подключения tooServer** появится диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="34870-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="34870-299">Имя типа hello hello второго сервера в **имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="34870-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="34870-300">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="34870-300">Click **Connect**.</span></span>

   <span data-ttu-id="34870-301">Вернитесь в hello **Выбор реплик** страницы, вы увидите hello второго сервера, перечисленные в **реплик доступности**.</span><span class="sxs-lookup"><span data-stu-id="34870-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="34870-302">Настройте hello реплики следующим образом.</span><span class="sxs-lookup"><span data-stu-id="34870-302">Configure hello replicas as follows.</span></span>

   ![Мастер создания групп доступности, указание реплик (завершено)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="34870-304">Нажмите кнопку **конечные точки** toosee hello конечную точку зеркального отображения для этой группы доступности.</span><span class="sxs-lookup"><span data-stu-id="34870-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="34870-305">Используйте hello же порт использовался при установке hello [правило брандмауэра для конечных точек зеркального отображения базы данных](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="34870-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="34870-307">В hello **Выбор начальной синхронизации данных** выберите **полного** и укажите общую сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="34870-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="34870-308">Для расположения hello использовать hello [резервном ресурсе, который вы создали](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="34870-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="34870-309">В примере hello, он был **\\\\\<первого SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="34870-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="34870-310">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="34870-311">Полная синхронизация принимает полную резервную копию базы данных hello на hello первого экземпляра SQL Server и его восстановления toohello второй экземпляр.</span><span class="sxs-lookup"><span data-stu-id="34870-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="34870-312">Полная синхронизация не рекомендуется для больших баз данных, так как может занимать много времени.</span><span class="sxs-lookup"><span data-stu-id="34870-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="34870-313">Это время можно уменьшить, вручную создается резервная копия базы данных hello и их восстановление с `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="34870-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="34870-314">Если база данных hello уже восстановлена с `NO RECOVERY` на hello второй сервер SQL перед настройкой hello группы доступности, выберите **только присоединение**.</span><span class="sxs-lookup"><span data-stu-id="34870-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="34870-315">Резервное копирование hello tootake после настройки hello группы доступности, выберите **пропустить начальную синхронизацию данных**.</span><span class="sxs-lookup"><span data-stu-id="34870-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="34870-317">В hello **проверки** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="34870-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="34870-318">Эта страница должна выглядеть примерно toohello после изображения:</span><span class="sxs-lookup"><span data-stu-id="34870-318">This page should look similar toohello following image:</span></span>

    ![Мастер создания групп доступности, проверка](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="34870-320">Имеется предупреждение для конфигурации прослушивателя hello, так как вы не настроили прослушиватель группы доступности.</span><span class="sxs-lookup"><span data-stu-id="34870-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="34870-321">Можно игнорировать это предупреждение, поскольку на виртуальных машинах Azure создать прослушиватель hello после создания hello балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="34870-322">В hello **Сводка** щелкните **Готово**, а затем подождите, пока мастер hello настраивает hello новой группы доступности.</span><span class="sxs-lookup"><span data-stu-id="34870-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="34870-323">В hello **выполняется** страницы, можно щелкнуть **Дополнительные сведения о** tooview hello подробные хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="34870-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="34870-324">После завершения работы мастера hello, проверять hello **результатов** tooverify страницы, hello группа доступности успешно создана.</span><span class="sxs-lookup"><span data-stu-id="34870-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Мастер создания групп доступности, результаты](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="34870-326">Нажмите кнопку **закрыть** tooexit приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="34870-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="34870-327">Проверьте hello группы доступности</span><span class="sxs-lookup"><span data-stu-id="34870-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="34870-328">В **обозревателе объектов** разверните элемент **Высокая доступность AlwaysOn**, а затем — элемент **Группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="34870-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="34870-329">Теперь вы увидите hello новой группы доступности в этом контейнере.</span><span class="sxs-lookup"><span data-stu-id="34870-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="34870-330">Щелкните правой кнопкой мыши hello группы доступности и нажмите кнопку **Показать панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="34870-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Отображение панели мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="34870-332">Ваш **панели мониторинга AlwaysOn** должен выглядеть примерно toothis.</span><span class="sxs-lookup"><span data-stu-id="34870-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Панель мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="34870-334">Вы увидите реплики hello, режим отработки отказа hello каждого состояния синхронизации реплики и hello.</span><span class="sxs-lookup"><span data-stu-id="34870-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="34870-335">В **диспетчере отказоустойчивости кластеров** щелкните свой кластер.</span><span class="sxs-lookup"><span data-stu-id="34870-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="34870-336">Выберите **Роли**.</span><span class="sxs-lookup"><span data-stu-id="34870-336">Select **Roles**.</span></span> <span data-ttu-id="34870-337">Имя группы доступности Hello, которая использовалась — это роль в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="34870-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="34870-338">Так как вы не настроили прослушиватель, у этой группы доступности нет IP-адреса для подключений клиентов.</span><span class="sxs-lookup"><span data-stu-id="34870-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="34870-339">После создания балансировки нагрузки Azure, вы настроите hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="34870-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="34870-341">Не предпринимайте toofail через hello группы доступности из hello диспетчера отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="34870-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="34870-342">Все операции отработки отказов следует выполнять через **панель мониторинга AlwaysOn** в SSMS.</span><span class="sxs-lookup"><span data-stu-id="34870-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="34870-343">Дополнительные сведения см. в разделе [ограничения на использование hello Диспетчер отказоустойчивости кластеров с группами доступности](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="34870-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="34870-344">На этом этапе имеется группа доступности с репликами в двух экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="34870-345">Hello группы доступности можно перемещать между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="34870-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="34870-346">Не удается подключиться toohello группы доступности еще, так как у вас прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="34870-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="34870-347">В виртуальных машинах Azure hello прослушивателя необходимо подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="34870-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="34870-348">Hello следующим шагом является toocreate hello подсистемы балансировки нагрузки в Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="34870-349">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="34870-349">Create an Azure load balancer</span></span>

<span data-ttu-id="34870-350">Для группы доступности SQL Server на виртуальных машинах Azure необходима подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="34870-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="34870-351">Подсистема балансировки нагрузки Hello содержит hello IP-адрес для прослушивателя группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="34870-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="34870-352">В этом разделе перечислены как toocreate hello Подсистема балансировки загрузки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="34870-353">В hello портал Azure, перейдите в группу ресурсов toohello где экземпляры SQL Server и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="34870-354">Найдите **балансировщик нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="34870-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="34870-355">Выберите подсистемы балансировки нагрузки hello, опубликованные корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="34870-355">Choose hello load balancer published by Microsoft.</span></span>

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="34870-357">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="34870-357">Click **Create**.</span></span>
3. <span data-ttu-id="34870-358">Настройте следующие параметры для балансировки нагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="34870-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="34870-359">Настройка</span><span class="sxs-lookup"><span data-stu-id="34870-359">Setting</span></span> | <span data-ttu-id="34870-360">Поле</span><span class="sxs-lookup"><span data-stu-id="34870-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="34870-361">**Имя**</span><span class="sxs-lookup"><span data-stu-id="34870-361">**Name**</span></span> |<span data-ttu-id="34870-362">Используйте имя текст hello балансировки нагрузки, например **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="34870-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="34870-363">**Тип**</span><span class="sxs-lookup"><span data-stu-id="34870-363">**Type**</span></span> |<span data-ttu-id="34870-364">Внутренний</span><span class="sxs-lookup"><span data-stu-id="34870-364">Internal</span></span> |
   | <span data-ttu-id="34870-365">**Виртуальная сеть**</span><span class="sxs-lookup"><span data-stu-id="34870-365">**Virtual network**</span></span> |<span data-ttu-id="34870-366">Используйте имя hello hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="34870-367">**Подсеть**</span><span class="sxs-lookup"><span data-stu-id="34870-367">**Subnet**</span></span> |<span data-ttu-id="34870-368">Используйте имя hello hello подсети, hello виртуальной машины находится в.</span><span class="sxs-lookup"><span data-stu-id="34870-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="34870-369">**Назначение IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="34870-369">**IP address assignment**</span></span> |<span data-ttu-id="34870-370">Статическое</span><span class="sxs-lookup"><span data-stu-id="34870-370">Static</span></span> |
   | <span data-ttu-id="34870-371">**IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="34870-371">**IP address**</span></span> |<span data-ttu-id="34870-372">Используйте доступный адрес из подсети.</span><span class="sxs-lookup"><span data-stu-id="34870-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="34870-373">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="34870-373">**Subscription**</span></span> |<span data-ttu-id="34870-374">Используйте hello же подписке, что hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="34870-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="34870-375">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="34870-375">**Location**</span></span> |<span data-ttu-id="34870-376">Используйте hello же расположении, что hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="34870-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="34870-377">Hello Azure — колонка портала должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="34870-377">hello Azure portal blade should look like this:</span></span>

   ![Создание балансировщика нагрузки](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="34870-379">Нажмите кнопку **создать**, балансировки нагрузки toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="34870-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="34870-380">Подсистема балансировки нагрузки hello tooconfigure, необходимо toocreate внутреннего пула, проверки и набор правил балансировки нагрузки, hello.</span><span class="sxs-lookup"><span data-stu-id="34870-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="34870-381">Выполните следующие действия в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="34870-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="34870-382">Добавление внутреннего пула</span><span class="sxs-lookup"><span data-stu-id="34870-382">Add backend pool</span></span>

1. <span data-ttu-id="34870-383">В hello портал Azure перейдите tooyour группы доступности.</span><span class="sxs-lookup"><span data-stu-id="34870-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="34870-384">Может потребоваться только что созданный hello toorefresh hello представление toosee балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="34870-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Поиск подсистемы балансировки нагрузки в группе ресурсов](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="34870-386">Выберите hello подсистему балансировки нагрузки, нажмите кнопку **внутренние пулы**и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="34870-387">Задайте hello внутренний пул следующим образом:</span><span class="sxs-lookup"><span data-stu-id="34870-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="34870-388">Настройка</span><span class="sxs-lookup"><span data-stu-id="34870-388">Setting</span></span> | <span data-ttu-id="34870-389">Описание</span><span class="sxs-lookup"><span data-stu-id="34870-389">Description</span></span> | <span data-ttu-id="34870-390">Пример</span><span class="sxs-lookup"><span data-stu-id="34870-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="34870-391">**Имя**</span><span class="sxs-lookup"><span data-stu-id="34870-391">**Name**</span></span> | <span data-ttu-id="34870-392">Введите текстовое имя.</span><span class="sxs-lookup"><span data-stu-id="34870-392">Type a text name</span></span> | <span data-ttu-id="34870-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="34870-393">SQLLBBE</span></span>
   | <span data-ttu-id="34870-394">**Сопоставлено с**</span><span class="sxs-lookup"><span data-stu-id="34870-394">**Associated to**</span></span> | <span data-ttu-id="34870-395">Выберите из списка</span><span class="sxs-lookup"><span data-stu-id="34870-395">Pick from list</span></span> | <span data-ttu-id="34870-396">Группа доступности</span><span class="sxs-lookup"><span data-stu-id="34870-396">Availability set</span></span>
   | <span data-ttu-id="34870-397">**группа доступности;**</span><span class="sxs-lookup"><span data-stu-id="34870-397">**Availability set**</span></span> | <span data-ttu-id="34870-398">Используйте имя набора доступности hello, что виртуальные машины SQL Server находятся в</span><span class="sxs-lookup"><span data-stu-id="34870-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="34870-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="34870-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="34870-400">**Виртуальные машины**</span><span class="sxs-lookup"><span data-stu-id="34870-400">**Virtual machines**</span></span> |<span data-ttu-id="34870-401">Здравствуйте, два имени виртуальной Машины сервера SQL Azure</span><span class="sxs-lookup"><span data-stu-id="34870-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="34870-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="34870-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="34870-403">Введите имя пула серверной части hello hello.</span><span class="sxs-lookup"><span data-stu-id="34870-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="34870-404">Щелкните **+ Добавить виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="34870-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="34870-405">Для группы доступности hello выберите группу доступности hello, hello, в которых находятся серверы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="34870-406">Для виртуальных машин включают оба hello серверов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34870-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="34870-407">Не включайте hello файл общей папке следящего сервера.</span><span class="sxs-lookup"><span data-stu-id="34870-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="34870-408">Нажмите кнопку **ОК** toocreate hello внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="34870-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="34870-409">Зонд hello наборов</span><span class="sxs-lookup"><span data-stu-id="34870-409">Set hello probe</span></span>

1. <span data-ttu-id="34870-410">Выберите hello подсистему балансировки нагрузки, нажмите кнопку **зонды работоспособности**и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="34870-411">Настройте пробу работоспособности hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="34870-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="34870-412">Настройка</span><span class="sxs-lookup"><span data-stu-id="34870-412">Setting</span></span> | <span data-ttu-id="34870-413">Описание</span><span class="sxs-lookup"><span data-stu-id="34870-413">Description</span></span> | <span data-ttu-id="34870-414">Пример</span><span class="sxs-lookup"><span data-stu-id="34870-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="34870-415">**Имя**</span><span class="sxs-lookup"><span data-stu-id="34870-415">**Name**</span></span> | <span data-ttu-id="34870-416">текст</span><span class="sxs-lookup"><span data-stu-id="34870-416">Text</span></span> | <span data-ttu-id="34870-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="34870-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="34870-418">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="34870-418">**Protocol**</span></span> | <span data-ttu-id="34870-419">Выберите протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="34870-419">Choose TCP</span></span> | <span data-ttu-id="34870-420">TCP</span><span class="sxs-lookup"><span data-stu-id="34870-420">TCP</span></span> |
   | <span data-ttu-id="34870-421">**Порт**</span><span class="sxs-lookup"><span data-stu-id="34870-421">**Port**</span></span> | <span data-ttu-id="34870-422">Любой неиспользуемый порт.</span><span class="sxs-lookup"><span data-stu-id="34870-422">Any unused port</span></span> | <span data-ttu-id="34870-423">59999</span><span class="sxs-lookup"><span data-stu-id="34870-423">59999</span></span> |
   | <span data-ttu-id="34870-424">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="34870-424">**Interval**</span></span>  | <span data-ttu-id="34870-425">пытается Hello промежуток времени между проверки в секундах</span><span class="sxs-lookup"><span data-stu-id="34870-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="34870-426">5</span><span class="sxs-lookup"><span data-stu-id="34870-426">5</span></span> |
   | <span data-ttu-id="34870-427">**Пороговое значение сбоя**</span><span class="sxs-lookup"><span data-stu-id="34870-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="34870-428">число последовательных сбоев пробы, которое должно происходить для виртуальной машины toobe, считаются неисправное Hello</span><span class="sxs-lookup"><span data-stu-id="34870-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="34870-429">2</span><span class="sxs-lookup"><span data-stu-id="34870-429">2</span></span> |

1. <span data-ttu-id="34870-430">Нажмите кнопку **ОК** проверки работоспособности tooset hello.</span><span class="sxs-lookup"><span data-stu-id="34870-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="34870-431">Задайте правила подсистемы балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="34870-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="34870-432">Выберите hello подсистему балансировки нагрузки, нажмите кнопку **правила подсистемы балансировки нагрузки**и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="34870-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="34870-433">Задайте следующим правила балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="34870-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="34870-434">Настройка</span><span class="sxs-lookup"><span data-stu-id="34870-434">Setting</span></span> | <span data-ttu-id="34870-435">Описание</span><span class="sxs-lookup"><span data-stu-id="34870-435">Description</span></span> | <span data-ttu-id="34870-436">Пример</span><span class="sxs-lookup"><span data-stu-id="34870-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="34870-437">**Имя**</span><span class="sxs-lookup"><span data-stu-id="34870-437">**Name**</span></span> | <span data-ttu-id="34870-438">текст</span><span class="sxs-lookup"><span data-stu-id="34870-438">Text</span></span> | <span data-ttu-id="34870-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="34870-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="34870-440">**Frontend IP address** (Интерфейсный IP-адрес)</span><span class="sxs-lookup"><span data-stu-id="34870-440">**Frontend IP address**</span></span> | <span data-ttu-id="34870-441">Выберите адрес.</span><span class="sxs-lookup"><span data-stu-id="34870-441">Choose an address</span></span> |<span data-ttu-id="34870-442">Используйте адрес hello, созданный при создании hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="34870-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="34870-443">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="34870-443">**Protocol**</span></span> | <span data-ttu-id="34870-444">Выберите протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="34870-444">Choose TCP</span></span> |<span data-ttu-id="34870-445">TCP</span><span class="sxs-lookup"><span data-stu-id="34870-445">TCP</span></span> |
   | <span data-ttu-id="34870-446">**Порт**</span><span class="sxs-lookup"><span data-stu-id="34870-446">**Port**</span></span> | <span data-ttu-id="34870-447">Использовать hello порт для экземпляра SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="34870-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="34870-448">1433</span><span class="sxs-lookup"><span data-stu-id="34870-448">1433</span></span> |
   | <span data-ttu-id="34870-449">**Серверный порт**</span><span class="sxs-lookup"><span data-stu-id="34870-449">**Backend Port**</span></span> | <span data-ttu-id="34870-450">Это поле не используется, если задан плавающий IP-адрес для прямого ответа от сервера.</span><span class="sxs-lookup"><span data-stu-id="34870-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="34870-451">1433</span><span class="sxs-lookup"><span data-stu-id="34870-451">1433</span></span> |
   | <span data-ttu-id="34870-452">**Проба**</span><span class="sxs-lookup"><span data-stu-id="34870-452">**Probe**</span></span> |<span data-ttu-id="34870-453">Hello имя, указанное для пробы hello</span><span class="sxs-lookup"><span data-stu-id="34870-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="34870-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="34870-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="34870-455">**Сохранение сеанса**</span><span class="sxs-lookup"><span data-stu-id="34870-455">**Session Persistence**</span></span> | <span data-ttu-id="34870-456">Раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="34870-456">Drop down list</span></span> | <span data-ttu-id="34870-457">**None**</span><span class="sxs-lookup"><span data-stu-id="34870-457">**None**</span></span> |
   | <span data-ttu-id="34870-458">**Время ожидания простоя**</span><span class="sxs-lookup"><span data-stu-id="34870-458">**Idle Timeout**</span></span> | <span data-ttu-id="34870-459">Откройте TCP-подключение tookeep минут</span><span class="sxs-lookup"><span data-stu-id="34870-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="34870-460">4.</span><span class="sxs-lookup"><span data-stu-id="34870-460">4</span></span> |
   | <span data-ttu-id="34870-461">**Плавающий IP-адрес (прямой ответ от сервера)**</span><span class="sxs-lookup"><span data-stu-id="34870-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="34870-462">Включено</span><span class="sxs-lookup"><span data-stu-id="34870-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="34870-463">Параметры прямого ответа от сервера задаются во время создания.</span><span class="sxs-lookup"><span data-stu-id="34870-463">Direct server return is set during creation.</span></span> <span data-ttu-id="34870-464">Их невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="34870-464">It cannot be changed.</span></span>

1. <span data-ttu-id="34870-465">Нажмите кнопку **ОК** правила подсистемы балансировки нагрузки tooset hello.</span><span class="sxs-lookup"><span data-stu-id="34870-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="34870-466"><a name="configure-listener"></a>Настройте прослушиватель hello</span><span class="sxs-lookup"><span data-stu-id="34870-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="34870-467">Далее самое toodo Hello — tooconfigure прослушивателя группы доступности в отказоустойчивом кластере hello.</span><span class="sxs-lookup"><span data-stu-id="34870-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="34870-468">В этом учебнике показано, как toocreate прослушиватель один - один ILB IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="34870-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="34870-469">один или несколько прослушивателей, с помощью одного или нескольких IP-адресов в разделе toocreate [прослушивателя Создание группы доступности и балансировки нагрузки | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34870-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="34870-470">Настройка порта прослушивателя</span><span class="sxs-lookup"><span data-stu-id="34870-470">Set listener port</span></span>

<span data-ttu-id="34870-471">В SQL Server Management Studio установите hello прослушиваемый порт.</span><span class="sxs-lookup"><span data-stu-id="34870-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="34870-472">Запустите SQL Server Management Studio и подключитесь toohello первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="34870-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="34870-473">Перейдите в слишком**высокий уровень доступности AlwaysOn** | **группы доступности** | **прослушиватели группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="34870-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="34870-474">Теперь вы увидите имя прослушивателя hello, созданный в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="34870-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="34870-475">Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="34870-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="34870-476">В hello **порт** укажите hello номер порта для прослушивателя группы доступности hello $EndpointPort ранее с помощью hello (по умолчанию hello — 1433), затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="34870-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="34870-477">Теперь у вас есть группа доступности SQL Server на виртуальных машинах Azure в режиме Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34870-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="34870-478">Toolistener тестирования подключения</span><span class="sxs-lookup"><span data-stu-id="34870-478">Test connection toolistener</span></span>

<span data-ttu-id="34870-479">подключение к tootest hello:</span><span class="sxs-lookup"><span data-stu-id="34870-479">tootest hello connection:</span></span>

1. <span data-ttu-id="34870-480">Tooa RDP сервера SQL в hello виртуальных сетевых, но не собственные hello реплики.</span><span class="sxs-lookup"><span data-stu-id="34870-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="34870-481">Можно использовать другие серверы SQL Server в кластере hello hello.</span><span class="sxs-lookup"><span data-stu-id="34870-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="34870-482">Используйте **sqlcmd** программа tootest hello соединения.</span><span class="sxs-lookup"><span data-stu-id="34870-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="34870-483">Например, следующий скрипт hello устанавливает **sqlcmd** toohello первичной подключения через прослушиватель hello с проверкой подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="34870-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="34870-484">Если прослушиватель hello не использует порт hello по умолчанию порт (1433), укажите порт hello в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="34870-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="34870-485">Например hello следующие команды sqlcmd подключается tooa прослушивания по порту 1435:</span><span class="sxs-lookup"><span data-stu-id="34870-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="34870-486">Hello SQLCMD подключения автоматически подключается toowhichever экземпляра SQL Server узлов hello первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="34870-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="34870-487">Убедитесь, что открыт порт hello, указываемые на брандмауэре hello и серверов SQL.</span><span class="sxs-lookup"><span data-stu-id="34870-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="34870-488">Оба сервера требуют входящее правило для hello TCP-порт, который можно использовать.</span><span class="sxs-lookup"><span data-stu-id="34870-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="34870-489">Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="34870-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="34870-490">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34870-490">Next steps</span></span>

- <span data-ttu-id="34870-491">[Добавление IP адрес tooa подсистемы балансировки нагрузки для второй группы доступности](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="34870-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
