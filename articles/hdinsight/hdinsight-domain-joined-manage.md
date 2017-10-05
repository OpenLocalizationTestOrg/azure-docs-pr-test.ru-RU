---
title: "Управление присоединенными к домену кластерами HDInsight в Azure | Документы Майкрософт"
description: "Узнайте, как управлять присоединенными к домену кластерами HDInsight"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="203f3-103">Управление присоединенными к домену кластерами HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="203f3-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="203f3-104">Узнайте, что такое пользователи и роли в кластерах HDInsight, присоединенных к домену, и как управлять присоединенными к домену кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="203f3-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="203f3-105">Пользователи в присоединенном к домену кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="203f3-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="203f3-106">Кластер HDInsight, который находится вне домена, имеет две учетные записи пользователя, которые создаются вместе с кластером.</span><span class="sxs-lookup"><span data-stu-id="203f3-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="203f3-107">**Администратор Ambari**: эта учетная запись называется также *Пользователь Hadoop* или *Пользователь HTTP*.</span><span class="sxs-lookup"><span data-stu-id="203f3-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="203f3-108">Эта учетная запись используется для входа на Ambari по адресу https://&lt;имя_кластера >.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="203f3-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="203f3-109">Ее также можно использовать для выполнения запросов по представлениям Ambari, выполнения заданий с помощью внешних средств (PowerShell, Templeton, Visual Studio и т. п.) и для проверки подлинности с помощью драйвера Hive ODBC и средств бизнес-аналитики (Excel, PowerBI или Tableau).</span><span class="sxs-lookup"><span data-stu-id="203f3-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="203f3-110">**Пользователь SSH**: эта учетная запись позволяет создать SSH-подключение и выполнять команды sudo.</span><span class="sxs-lookup"><span data-stu-id="203f3-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="203f3-111">Она имеет привилегии администратора для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="203f3-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="203f3-112">Для кластера HDInsight, присоединенного к домену, в дополнение к администратору Ambari и пользователю SSH создаются еще три пользователя.</span><span class="sxs-lookup"><span data-stu-id="203f3-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="203f3-113">**Администратор Ranger**: это локальная учетная запись администратора Apache Ranger.</span><span class="sxs-lookup"><span data-stu-id="203f3-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="203f3-114">Она не является пользователем домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="203f3-114">It is not an active directory domain user.</span></span> <span data-ttu-id="203f3-115">Эту учетную запись можно использовать для настройки политик, создания других пользователей-администраторов или делегированных администраторов (чтобы они могли управлять политиками).</span><span class="sxs-lookup"><span data-stu-id="203f3-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="203f3-116">По умолчанию используется имя пользователя *admin* и такой же пароль, как для администратора Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="203f3-117">Этот пароль можно изменить на странице настроек в Ranger.</span><span class="sxs-lookup"><span data-stu-id="203f3-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="203f3-118">**Пользователь домена и администратор кластера**: это пользователь домена Active Directory, который является администратором кластера Hadoop, а также служб Ambari и Ranger.</span><span class="sxs-lookup"><span data-stu-id="203f3-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="203f3-119">Учетные данные этого пользователя нужно предоставить во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="203f3-120">Этот пользователь имеет следующие права.</span><span class="sxs-lookup"><span data-stu-id="203f3-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="203f3-121">Присоединение компьютеров к домену и помещение их в определенное подразделение, которое указывается во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="203f3-122">Создание субъектов-служб в определенном подразделении, которое указывается во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="203f3-123">Создание обратных записей DNS.</span><span class="sxs-lookup"><span data-stu-id="203f3-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="203f3-124">Обратите внимание, что эти права есть и у других пользователей AD.</span><span class="sxs-lookup"><span data-stu-id="203f3-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="203f3-125">В пределах кластера существуют некоторые конечные точки (например, Templeton), которые не управляются службой Ranger, и следовательно не являются безопасными.</span><span class="sxs-lookup"><span data-stu-id="203f3-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="203f3-126">Такие конечные точки закрываются для всех пользователей, за исключением пользователя домена и администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="203f3-127">**Обычный**: во время создания кластера можно указать несколько групп Active Directory.</span><span class="sxs-lookup"><span data-stu-id="203f3-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="203f3-128">Пользователи в эти группах будут синхронизированы с Ranger и Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="203f3-129">Эти пользователи являются пользователями домена и будут иметь доступ только к конечным точкам, которые управляются службой Ranger (например, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="203f3-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="203f3-130">Для этих пользователей применяются все политики RBAC и правила аудита.</span><span class="sxs-lookup"><span data-stu-id="203f3-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="203f3-131">Роли в присоединенном к домену кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="203f3-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="203f3-132">В домене HDInsight существуют следующие роли:</span><span class="sxs-lookup"><span data-stu-id="203f3-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="203f3-133">администратор кластера;</span><span class="sxs-lookup"><span data-stu-id="203f3-133">Cluster Administrator</span></span>
* <span data-ttu-id="203f3-134">оператор кластера;</span><span class="sxs-lookup"><span data-stu-id="203f3-134">Cluster Operator</span></span>
* <span data-ttu-id="203f3-135">администратора служб;</span><span class="sxs-lookup"><span data-stu-id="203f3-135">Service Administrator</span></span>
* <span data-ttu-id="203f3-136">оператор службы;</span><span class="sxs-lookup"><span data-stu-id="203f3-136">Service Operator</span></span>
* <span data-ttu-id="203f3-137">пользователь кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-137">Cluster User</span></span>

<span data-ttu-id="203f3-138">**Просмотр разрешений для этих ролей**</span><span class="sxs-lookup"><span data-stu-id="203f3-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="203f3-139">Откройте пользовательский интерфейс управления Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="203f3-140">См. раздел [Вход в пользовательский интерфейс управления Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="203f3-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="203f3-141">В меню слева щелкните **Роли**.</span><span class="sxs-lookup"><span data-stu-id="203f3-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="203f3-142">Щелкните синий вопросительный знак, чтобы просмотреть разрешения.</span><span class="sxs-lookup"><span data-stu-id="203f3-142">Click the blue question mark to see the permissions:</span></span>

    ![Роли в присоединенном к домену кластере HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="203f3-144">Вход в пользовательский интерфейс управления Ambari</span><span class="sxs-lookup"><span data-stu-id="203f3-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="203f3-145">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="203f3-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="203f3-146">Откройте колонку для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="203f3-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="203f3-147">См. раздел [Отображение кластеров](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="203f3-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="203f3-148">В меню сверху щелкните **Панель мониторинга**, чтобы открыть Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="203f3-149">Войдите в Ambari, используя имя пользователя и пароль пользователя домена и администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="203f3-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="203f3-150">Щелкните раскрывающееся меню **Администратор** в правом верхнем углу, затем нажмите кнопку **Управление Ambari**.</span><span class="sxs-lookup"><span data-stu-id="203f3-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Управление Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="203f3-152">Пользовательский интерфейс выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="203f3-152">The UI looks like:</span></span>

    ![Интерфейс управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="203f3-154">Список пользователей домена, синхронизированных из Active Directory</span><span class="sxs-lookup"><span data-stu-id="203f3-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="203f3-155">Откройте пользовательский интерфейс управления Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="203f3-156">См. раздел [Вход в пользовательский интерфейс управления Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="203f3-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="203f3-157">В меню слева щелкните **Users**(Пользователи).</span><span class="sxs-lookup"><span data-stu-id="203f3-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="203f3-158">Вы увидите всех пользователей, синхронизированных в кластер HDInsight из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="203f3-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Список пользователей в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="203f3-160">Список групп домена, синхронизированных из Active Directory</span><span class="sxs-lookup"><span data-stu-id="203f3-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="203f3-161">Откройте пользовательский интерфейс управления Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="203f3-162">См. раздел [Вход в пользовательский интерфейс управления Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="203f3-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="203f3-163">В меню слева щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="203f3-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="203f3-164">Вы увидите все группы, синхронизированные в кластер HDInsight из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="203f3-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Список групп в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="203f3-166">Настройка разрешений для представлений Hive</span><span class="sxs-lookup"><span data-stu-id="203f3-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="203f3-167">Откройте пользовательский интерфейс управления Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="203f3-168">См. раздел [Вход в пользовательский интерфейс управления Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="203f3-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="203f3-169">В меню слева щелкните **Представления**.</span><span class="sxs-lookup"><span data-stu-id="203f3-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="203f3-170">Щелкните **HIVE**, чтобы открыть подробную информацию.</span><span class="sxs-lookup"><span data-stu-id="203f3-170">Click **HIVE** to show the details.</span></span>

    ![Представления Hive в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="203f3-172">Щелкните ссылку **Представление Hive**, чтобы настроить представления Hive.</span><span class="sxs-lookup"><span data-stu-id="203f3-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="203f3-173">Выполните прокрутку вниз до раздела **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="203f3-173">Scroll down to the **Permissions** section.</span></span>

    ![Настройка разрешений для представлений Hive в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="203f3-175">Щелкните **Добавить пользователя** или **Добавить группу**, а затем укажите пользователей или группы, которые могут использовать представления Hive.</span><span class="sxs-lookup"><span data-stu-id="203f3-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="203f3-176">Настройка ролей для пользователей</span><span class="sxs-lookup"><span data-stu-id="203f3-176">Configure users for the roles</span></span>
 <span data-ttu-id="203f3-177">Список ролей и разрешений см. в разделе [Роли в присоединенном к домену кластере HDInsight](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="203f3-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="203f3-178">Откройте пользовательский интерфейс управления Ambari.</span><span class="sxs-lookup"><span data-stu-id="203f3-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="203f3-179">См. раздел [Вход в пользовательский интерфейс управления Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="203f3-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="203f3-180">В меню слева щелкните **Роли**.</span><span class="sxs-lookup"><span data-stu-id="203f3-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="203f3-181">Щелкните **Добавить пользователя** или **Добавить группу**, чтобы назначить роли для пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="203f3-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="203f3-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="203f3-182">Next steps</span></span>
* <span data-ttu-id="203f3-183">Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="203f3-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="203f3-184">Сведения о настройке политик Hive и выполнении запросов Hive для присоединенного к домену кластера HDInsight см. [здесь](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="203f3-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="203f3-185">Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="203f3-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
