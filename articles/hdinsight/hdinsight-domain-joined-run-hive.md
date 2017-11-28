---
title: "Настройка политик Hive в присоединенном к домену кластере HDInsight — Azure | Документы Майкрософт"
description: "Дополнительные сведения"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="9b882-103">Настройка политик Hive в присоединенном к домену кластере HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="9b882-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="9b882-104">Узнайте, как настроить политики Apache Ranger для Hive.</span><span class="sxs-lookup"><span data-stu-id="9b882-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="9b882-105">В этой статье вы создадите две политики Ranger, чтобы ограничить доступ к таблице hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9b882-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="9b882-106">Таблица hivesampletable поставляется с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b882-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="9b882-107">После настройки политик подключитесь к таблицам Hive в HDInsight с помощью Excel и драйвера ODBC.</span><span class="sxs-lookup"><span data-stu-id="9b882-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b882-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9b882-108">Prerequisites</span></span>
* <span data-ttu-id="9b882-109">Присоединенный к домену кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b882-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="9b882-110">См. статью [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Настройка присоединенных к домену кластеров HDInsight).</span><span class="sxs-lookup"><span data-stu-id="9b882-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="9b882-111">Рабочая станция с Office 2016, Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="9b882-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="9b882-112">Подключение к пользовательскому интерфейсу администратора Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="9b882-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="9b882-113">**Подключение к пользовательскому интерфейсу администратора Ranger**</span><span class="sxs-lookup"><span data-stu-id="9b882-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="9b882-114">В браузере подключитесь к пользовательскому интерфейсу администратора Ranger</span><span class="sxs-lookup"><span data-stu-id="9b882-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="9b882-115">по URL-адресу https://&lt;имя_кластера >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="9b882-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9b882-116">Ranger использует учетные данные, отличающиеся от учетных данных кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9b882-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="9b882-117">Чтобы браузеры не использовали кэшированные учетные данные Hadoop, подключитесь к пользовательскому интерфейсу администратора Ranger в новом окне браузера в режиме InPrivate.</span><span class="sxs-lookup"><span data-stu-id="9b882-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="9b882-118">Войдите, используя имя пользователя и пароль домена администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="9b882-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Домашняя страница Ranger для подключенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="9b882-120">В настоящее время Ranger работает только с Yarn и Hive.</span><span class="sxs-lookup"><span data-stu-id="9b882-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="9b882-121">Создание пользователей домена</span><span class="sxs-lookup"><span data-stu-id="9b882-121">Create Domain users</span></span>
<span data-ttu-id="9b882-122">При работе со статьей [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Настройка присоединенных к домену кластеров HDInsight) вы создали два пользователя: hiveruser1 и hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="9b882-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="9b882-123">В этом руководстве вы будете использовать эти две учетные записи.</span><span class="sxs-lookup"><span data-stu-id="9b882-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="9b882-124">Создание политик Ranger</span><span class="sxs-lookup"><span data-stu-id="9b882-124">Create Ranger policies</span></span>
<span data-ttu-id="9b882-125">В этом разделе вы создадите две политики Ranger для доступа к таблице hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9b882-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="9b882-126">Вам нужно будет предоставить разрешение select для разных наборов столбцов.</span><span class="sxs-lookup"><span data-stu-id="9b882-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="9b882-127">Оба пользователя созданы при выполнении указаний статьи о [настройке присоединенных к домену кластеров HDInsight](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="9b882-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="9b882-128">В следующем разделе вы протестируете две политики в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b882-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="9b882-129">**Создание политик Ranger**</span><span class="sxs-lookup"><span data-stu-id="9b882-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="9b882-130">Откройте пользовательский интерфейс администратора Ranger.</span><span class="sxs-lookup"><span data-stu-id="9b882-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="9b882-131">См. раздел [Подключение к пользовательскому интерфейсу администратора Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="9b882-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="9b882-132">Щелкните **&lt;имя_кластера>_hive** в разделе **Hive**.</span><span class="sxs-lookup"><span data-stu-id="9b882-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="9b882-133">Отобразятся две предварительно настроенные политики.</span><span class="sxs-lookup"><span data-stu-id="9b882-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="9b882-134">Щелкните **Добавить новую политику**, а затем введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="9b882-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="9b882-135">Имя политики: read-hivesampletable-all.</span><span class="sxs-lookup"><span data-stu-id="9b882-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="9b882-136">База данных Hive: по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9b882-136">Hive Database: default</span></span>
   * <span data-ttu-id="9b882-137">Таблица: hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9b882-137">table: hivesampletable</span></span>
   * <span data-ttu-id="9b882-138">Столбец Hive: *.</span><span class="sxs-lookup"><span data-stu-id="9b882-138">Hive column: *</span></span>
   * <span data-ttu-id="9b882-139">Пользователь: hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="9b882-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="9b882-140">Разрешения: select.</span><span class="sxs-lookup"><span data-stu-id="9b882-140">Permissions: select</span></span>

     ![Настойка политики Hive Ranger для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="9b882-142">.</span><span class="sxs-lookup"><span data-stu-id="9b882-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9b882-143">Если пользователь домена не указан в поле "Выберите пользователя", подождите несколько минут для синхронизации Ranger с AAD.</span><span class="sxs-lookup"><span data-stu-id="9b882-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="9b882-144">Щелкните **Добавить**, чтобы сохранить политику.</span><span class="sxs-lookup"><span data-stu-id="9b882-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="9b882-145">Повторите последние два шага, чтобы создать еще одну политику со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="9b882-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="9b882-146">Имя политики: read-hivesampletable-devicemake.</span><span class="sxs-lookup"><span data-stu-id="9b882-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="9b882-147">База данных Hive: по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9b882-147">Hive Database: default</span></span>
   * <span data-ttu-id="9b882-148">Таблица: hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9b882-148">table: hivesampletable</span></span>
   * <span data-ttu-id="9b882-149">Столбец Hive: clientid, devicemake.</span><span class="sxs-lookup"><span data-stu-id="9b882-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="9b882-150">Пользователь: hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="9b882-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="9b882-151">Разрешения: select.</span><span class="sxs-lookup"><span data-stu-id="9b882-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="9b882-152">Создание источника данных Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="9b882-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="9b882-153">Инструкции см. в разделе [Создание источника данных Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="9b882-154">Свойство</span><span class="sxs-lookup"><span data-stu-id="9b882-154">Property</span></span>|<span data-ttu-id="9b882-155">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="9b882-155">Description</span></span>
    ---|---
    <span data-ttu-id="9b882-156">Имя источника данных</span><span class="sxs-lookup"><span data-stu-id="9b882-156">Data Source Name</span></span>|<span data-ttu-id="9b882-157">Присвойте имя источнику данных</span><span class="sxs-lookup"><span data-stu-id="9b882-157">Give a name to your data source</span></span>
    <span data-ttu-id="9b882-158">Узел</span><span class="sxs-lookup"><span data-stu-id="9b882-158">Host</span></span>|<span data-ttu-id="9b882-159">Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9b882-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="9b882-160">Например, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="9b882-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="9b882-161">Порт</span><span class="sxs-lookup"><span data-stu-id="9b882-161">Port</span></span>|<span data-ttu-id="9b882-162">Используйте <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="9b882-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="9b882-163">(Этот порт был изменен с 563 на 443.)</span><span class="sxs-lookup"><span data-stu-id="9b882-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="9b882-164">База данных</span><span class="sxs-lookup"><span data-stu-id="9b882-164">Database</span></span>|<span data-ttu-id="9b882-165">Используйте <strong>значение по умолчанию</strong>.</span><span class="sxs-lookup"><span data-stu-id="9b882-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="9b882-166">Тип сервера Hive</span><span class="sxs-lookup"><span data-stu-id="9b882-166">Hive Server Type</span></span>|<span data-ttu-id="9b882-167">Выберите <strong>Hive Server 2</strong>.</span><span class="sxs-lookup"><span data-stu-id="9b882-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="9b882-168">Механизм</span><span class="sxs-lookup"><span data-stu-id="9b882-168">Mechanism</span></span>|<span data-ttu-id="9b882-169">Выберите <strong>Служба Azure HDInsight</strong>.</span><span class="sxs-lookup"><span data-stu-id="9b882-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="9b882-170">Путь HTTP</span><span class="sxs-lookup"><span data-stu-id="9b882-170">HTTP Path</span></span>|<span data-ttu-id="9b882-171">Оставьте пустым.</span><span class="sxs-lookup"><span data-stu-id="9b882-171">Leave it blank.</span></span>
    <span data-ttu-id="9b882-172">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="9b882-172">User Name</span></span>|<span data-ttu-id="9b882-173">Укажите hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9b882-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="9b882-174">Обновите имя домена, если оно отличается.</span><span class="sxs-lookup"><span data-stu-id="9b882-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="9b882-175">Пароль</span><span class="sxs-lookup"><span data-stu-id="9b882-175">Password</span></span>|<span data-ttu-id="9b882-176">Введите пароль для hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="9b882-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="9b882-177">Щелкните **Проверка** перед сохранением источника данных.</span><span class="sxs-lookup"><span data-stu-id="9b882-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="9b882-178">Импорт данных в Excel из службы HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b882-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="9b882-179">В последнем разделе вы настроили две политики.</span><span class="sxs-lookup"><span data-stu-id="9b882-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="9b882-180">У hiveuser1 есть разрешение select на все столбцы, а у hiveuser2 — на два столбца.</span><span class="sxs-lookup"><span data-stu-id="9b882-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="9b882-181">В этом разделе вы выполните олицетворение двух пользователей для импорта данных в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b882-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="9b882-182">Откройте новую или существующую рабочую книгу в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b882-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="9b882-183">На вкладке **Данные** щелкните **From Other Data Sources** (Из других источников данных), а затем выберите **Из мастера подключения к данным**, чтобы запустить **мастер подключения к данным**.</span><span class="sxs-lookup"><span data-stu-id="9b882-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="9b882-184">![Откройте мастер подключения к данным][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="9b882-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="9b882-185">Выберите **ODBC DSN** в качестве источника данных и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9b882-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="9b882-186">В источниках данных ODBC выберите имя источника данных, созданного на предыдущем шаге, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9b882-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="9b882-187">Повторно введите в мастере пароль для кластера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9b882-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="9b882-188">Подождите открытие диалогового окна **Выбор базы данных и таблицы** .</span><span class="sxs-lookup"><span data-stu-id="9b882-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="9b882-189">Это может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9b882-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="9b882-190">Выберите **hivesampletable**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9b882-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="9b882-191">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="9b882-191">Click **Finish**.</span></span>
8. <span data-ttu-id="9b882-192">В диалоговом окне **Импорт данных** можно изменить или указать запрос.</span><span class="sxs-lookup"><span data-stu-id="9b882-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="9b882-193">Для этого щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="9b882-193">To do so, click **Properties**.</span></span> <span data-ttu-id="9b882-194">Это может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9b882-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="9b882-195">Выберите вкладку **Определение**.</span><span class="sxs-lookup"><span data-stu-id="9b882-195">Click the **Definition** tab.</span></span> <span data-ttu-id="9b882-196">Текст команды:</span><span class="sxs-lookup"><span data-stu-id="9b882-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="9b882-197">В соответствии с заданными политиками Ranger у hiveuser1 есть разрешение select на все столбцы.</span><span class="sxs-lookup"><span data-stu-id="9b882-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="9b882-198">Поэтому этот запрос срабатывает с учетными данными hiveuser1, но не с учетными данными hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="9b882-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="9b882-199">![Свойства подключения][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="9b882-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="9b882-200">Нажмите **OK** , чтобы закрыть диалоговое окно "Свойства подключения".</span><span class="sxs-lookup"><span data-stu-id="9b882-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="9b882-201">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Импорт данных**.</span><span class="sxs-lookup"><span data-stu-id="9b882-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="9b882-202">Введите пароль для hiveuser1 еще раз и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9b882-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="9b882-203">Пройдет несколько секунд, прежде чем данные будут импортированы в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b882-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="9b882-204">После этого отобразятся 11 столбцов с данными.</span><span class="sxs-lookup"><span data-stu-id="9b882-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="9b882-205">Проверка второй политики (read-hivesampletable-devicemake), созданной в предыдущем разделе</span><span class="sxs-lookup"><span data-stu-id="9b882-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="9b882-206">Добавьте новый лист в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b882-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="9b882-207">Выполните последнюю процедуру для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="9b882-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="9b882-208">Единственное изменение заключается в том, что нужно использовать учетные данные hiveuser2, а не hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="9b882-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="9b882-209">При этом произойдет сбой, так как у hiveuser2 есть разрешение только на просмотр двух столбцов.</span><span class="sxs-lookup"><span data-stu-id="9b882-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="9b882-210">Появится следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="9b882-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="9b882-211">Выполните ту же процедуру для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="9b882-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="9b882-212">На этот раз используйте учетные данные hiveuser2 и измените инструкцию FROM в предложении SELECT:</span><span class="sxs-lookup"><span data-stu-id="9b882-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="9b882-213">на:</span><span class="sxs-lookup"><span data-stu-id="9b882-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="9b882-214">После этого импортируются два столбца с данными.</span><span class="sxs-lookup"><span data-stu-id="9b882-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b882-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b882-215">Next steps</span></span>
* <span data-ttu-id="9b882-216">Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="9b882-217">Сведения об управлении присоединенными к домену кластерами HDInsight см. в [этой статье](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="9b882-218">Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="9b882-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="9b882-219">Сведения о подключении к Hive с помощью Hive JDBC см. в статье [Подключение к Hive в Azure HDInsight с помощью драйвера Hive JDBC](hdinsight-connect-hive-jdbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="9b882-220">Сведения о подключении Excel к Hadoop с помощью Hive ODBC см. в статье [Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="9b882-221">Сведения о подключении Excel к Hadoop с помощью Power Query см. в [этой статье](hdinsight-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="9b882-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
