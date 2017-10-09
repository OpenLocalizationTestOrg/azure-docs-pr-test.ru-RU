---
title: "политики aaaConfigure Hive в HDInsight домену - Azure | Документы Microsoft"
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
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="419d4-103">Настройка политик Hive в присоединенном к домену кластере HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="419d4-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="419d4-104">Узнайте, как политики tooconfigure круг Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="419d4-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="419d4-105">В этой статье создайте hivesampletable toohello два круг политики toorestrict доступа.</span><span class="sxs-lookup"><span data-stu-id="419d4-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="419d4-106">Hello hivesampletable поставляется с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="419d4-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="419d4-107">После настройки политики hello вы используете Excel и ODBC драйвера tooconnect tooHive таблиц в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="419d4-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="419d4-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="419d4-108">Prerequisites</span></span>
* <span data-ttu-id="419d4-109">Присоединенный к домену кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="419d4-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="419d4-110">См. статью [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Настройка присоединенных к домену кластеров HDInsight).</span><span class="sxs-lookup"><span data-stu-id="419d4-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="419d4-111">Рабочая станция с Office 2016, Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="419d4-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="419d4-112">Подключение tooApache круг пользовательского интерфейса администратора</span><span class="sxs-lookup"><span data-stu-id="419d4-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="419d4-113">**tooconnect tooRanger пользовательского интерфейса администратора**</span><span class="sxs-lookup"><span data-stu-id="419d4-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="419d4-114">С помощью браузера подключитесь tooRanger пользовательского интерфейса администратора.</span><span class="sxs-lookup"><span data-stu-id="419d4-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="419d4-115">Hello URL-адрес: https://&lt;Имя_кластера >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="419d4-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="419d4-116">Ranger использует учетные данные, отличающиеся от учетных данных кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="419d4-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="419d4-117">обозреватели tooprevent, кэшированные Hadoop, используя учетные данные используют новый toohello tooconnect окна браузера inprivate круг пользовательского интерфейса администратора.</span><span class="sxs-lookup"><span data-stu-id="419d4-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="419d4-118">Войдите, используя имя пользователя домена администратора кластера hello и пароль:</span><span class="sxs-lookup"><span data-stu-id="419d4-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Домашняя страница Ranger для подключенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="419d4-120">В настоящее время Ranger работает только с Yarn и Hive.</span><span class="sxs-lookup"><span data-stu-id="419d4-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="419d4-121">Создание пользователей домена</span><span class="sxs-lookup"><span data-stu-id="419d4-121">Create Domain users</span></span>
<span data-ttu-id="419d4-122">При работе со статьей [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Настройка присоединенных к домену кластеров HDInsight) вы создали два пользователя: hiveruser1 и hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="419d4-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="419d4-123">В этом учебнике будет использовать учетная запись hello два пользователя.</span><span class="sxs-lookup"><span data-stu-id="419d4-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="419d4-124">Создание политик Ranger</span><span class="sxs-lookup"><span data-stu-id="419d4-124">Create Ranger policies</span></span>
<span data-ttu-id="419d4-125">В этом разделе вы создадите две политики Ranger для доступа к таблице hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="419d4-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="419d4-126">Вам нужно будет предоставить разрешение select для разных наборов столбцов.</span><span class="sxs-lookup"><span data-stu-id="419d4-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="419d4-127">Оба пользователя созданы при выполнении указаний статьи о [настройке присоединенных к домену кластеров HDInsight](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="419d4-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="419d4-128">В следующем разделе hello тестировании hello две политики в Excel.</span><span class="sxs-lookup"><span data-stu-id="419d4-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="419d4-129">**toocreate круг политики**</span><span class="sxs-lookup"><span data-stu-id="419d4-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="419d4-130">Откройте пользовательский интерфейс администратора Ranger.</span><span class="sxs-lookup"><span data-stu-id="419d4-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="419d4-131">В разделе [подключения tooApache пользовательского интерфейса администратора круг](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="419d4-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="419d4-132">Щелкните **&lt;имя_кластера>_hive** в разделе **Hive**.</span><span class="sxs-lookup"><span data-stu-id="419d4-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="419d4-133">Отобразятся две предварительно настроенные политики.</span><span class="sxs-lookup"><span data-stu-id="419d4-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="419d4-134">Нажмите кнопку **добавить новую политику**, а затем введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="419d4-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="419d4-135">Имя политики: read-hivesampletable-all.</span><span class="sxs-lookup"><span data-stu-id="419d4-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="419d4-136">База данных Hive: по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="419d4-136">Hive Database: default</span></span>
   * <span data-ttu-id="419d4-137">Таблица: hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="419d4-137">table: hivesampletable</span></span>
   * <span data-ttu-id="419d4-138">Столбец Hive: *.</span><span class="sxs-lookup"><span data-stu-id="419d4-138">Hive column: *</span></span>
   * <span data-ttu-id="419d4-139">Пользователь: hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="419d4-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="419d4-140">Разрешения: select.</span><span class="sxs-lookup"><span data-stu-id="419d4-140">Permissions: select</span></span>

     ![Настойка политики Hive Ranger для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="419d4-142">.</span><span class="sxs-lookup"><span data-stu-id="419d4-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="419d4-143">Если пользователь домена не заполняется в Выбор пользователя, подождите несколько секунд для toosync круг с AAD.</span><span class="sxs-lookup"><span data-stu-id="419d4-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="419d4-144">Нажмите кнопку **добавить** toosave hello политики.</span><span class="sxs-lookup"><span data-stu-id="419d4-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="419d4-145">Повторите toocreate последних двух этапов hello еще одну политику с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="419d4-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="419d4-146">Имя политики: read-hivesampletable-devicemake.</span><span class="sxs-lookup"><span data-stu-id="419d4-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="419d4-147">База данных Hive: по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="419d4-147">Hive Database: default</span></span>
   * <span data-ttu-id="419d4-148">Таблица: hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="419d4-148">table: hivesampletable</span></span>
   * <span data-ttu-id="419d4-149">Столбец Hive: clientid, devicemake.</span><span class="sxs-lookup"><span data-stu-id="419d4-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="419d4-150">Пользователь: hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="419d4-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="419d4-151">Разрешения: select.</span><span class="sxs-lookup"><span data-stu-id="419d4-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="419d4-152">Создание источника данных Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="419d4-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="419d4-153">Hello инструкции можно найти в [источника данных ODBC Hive создать](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="419d4-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="419d4-154">Свойство</span><span class="sxs-lookup"><span data-stu-id="419d4-154">Property</span></span>|<span data-ttu-id="419d4-155">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="419d4-155">Description</span></span>
    ---|---
    <span data-ttu-id="419d4-156">Имя источника данных</span><span class="sxs-lookup"><span data-stu-id="419d4-156">Data Source Name</span></span>|<span data-ttu-id="419d4-157">Предоставьте имя источника данных tooyour</span><span class="sxs-lookup"><span data-stu-id="419d4-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="419d4-158">Узел</span><span class="sxs-lookup"><span data-stu-id="419d4-158">Host</span></span>|<span data-ttu-id="419d4-159">Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="419d4-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="419d4-160">Например, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="419d4-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="419d4-161">Порт</span><span class="sxs-lookup"><span data-stu-id="419d4-161">Port</span></span>|<span data-ttu-id="419d4-162">Используйте <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="419d4-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="419d4-163">(Этот порт был изменен из 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="419d4-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="419d4-164">База данных</span><span class="sxs-lookup"><span data-stu-id="419d4-164">Database</span></span>|<span data-ttu-id="419d4-165">Используйте <strong>значение по умолчанию</strong>.</span><span class="sxs-lookup"><span data-stu-id="419d4-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="419d4-166">Тип сервера Hive</span><span class="sxs-lookup"><span data-stu-id="419d4-166">Hive Server Type</span></span>|<span data-ttu-id="419d4-167">Выберите <strong>Hive Server 2</strong>.</span><span class="sxs-lookup"><span data-stu-id="419d4-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="419d4-168">Механизм</span><span class="sxs-lookup"><span data-stu-id="419d4-168">Mechanism</span></span>|<span data-ttu-id="419d4-169">Выберите <strong>Служба Azure HDInsight</strong>.</span><span class="sxs-lookup"><span data-stu-id="419d4-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="419d4-170">Путь HTTP</span><span class="sxs-lookup"><span data-stu-id="419d4-170">HTTP Path</span></span>|<span data-ttu-id="419d4-171">Оставьте пустым.</span><span class="sxs-lookup"><span data-stu-id="419d4-171">Leave it blank.</span></span>
    <span data-ttu-id="419d4-172">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="419d4-172">User Name</span></span>|<span data-ttu-id="419d4-173">Укажите hiveuser1@contoso158.onmicrosoft.com. Обновите hello доменное имя, если он отличается.</span><span class="sxs-lookup"><span data-stu-id="419d4-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="419d4-174">Пароль</span><span class="sxs-lookup"><span data-stu-id="419d4-174">Password</span></span>|<span data-ttu-id="419d4-175">Пароль hiveuser1 hello.</span><span class="sxs-lookup"><span data-stu-id="419d4-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="419d4-176">Убедитесь, что tooclick **тест** перед сохранением hello источника данных.</span><span class="sxs-lookup"><span data-stu-id="419d4-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="419d4-177">Импорт данных в Excel из службы HDInsight</span><span class="sxs-lookup"><span data-stu-id="419d4-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="419d4-178">В последнем разделе hello вы настроили две политики.</span><span class="sxs-lookup"><span data-stu-id="419d4-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="419d4-179">hiveuser1 имеет разрешение select на все столбцы hello hello и hiveuser2 hello разрешение select на два столбца.</span><span class="sxs-lookup"><span data-stu-id="419d4-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="419d4-180">В этом разделе олицетворять hello два пользователя tooimport данных в Excel.</span><span class="sxs-lookup"><span data-stu-id="419d4-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="419d4-181">Откройте новую или существующую рабочую книгу в Excel.</span><span class="sxs-lookup"><span data-stu-id="419d4-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="419d4-182">Из hello **данные** щелкните **из других источников данных**и нажмите кнопку **от мастера подключения к данным** toolaunch hello **мастераподключениякданным**.</span><span class="sxs-lookup"><span data-stu-id="419d4-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="419d4-183">![Откройте мастер подключения к данным][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="419d4-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="419d4-184">Выберите **ODBC DSN** как hello источника данных, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="419d4-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="419d4-185">Из источников данных ODBC, имя, созданную в предыдущем шаге hello источника данных выберите hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="419d4-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="419d4-186">Повторно введите пароль hello кластера hello в мастере приветствия и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="419d4-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="419d4-187">Дождитесь hello **Выбор базы данных и таблицы** tooopen диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="419d4-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="419d4-188">Это может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="419d4-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="419d4-189">Выберите **hivesampletable**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="419d4-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="419d4-190">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="419d4-190">Click **Finish**.</span></span>
8. <span data-ttu-id="419d4-191">В hello **импорта данных** диалоговое окно, можно изменить или указать запрос hello.</span><span class="sxs-lookup"><span data-stu-id="419d4-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="419d4-192">Таким образом, щелкните toodo **свойства**.</span><span class="sxs-lookup"><span data-stu-id="419d4-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="419d4-193">Это может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="419d4-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="419d4-194">Нажмите кнопку hello **определение** текст команды вкладку hello:</span><span class="sxs-lookup"><span data-stu-id="419d4-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="419d4-195">Политиками hello круг определенным вами hiveuser1 имеет разрешение select на все столбцы hello.</span><span class="sxs-lookup"><span data-stu-id="419d4-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="419d4-196">Поэтому этот запрос срабатывает с учетными данными hiveuser1, но не с учетными данными hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="419d4-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="419d4-197">![Свойства подключения][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="419d4-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="419d4-198">Нажмите кнопку **ОК** диалоговое окно свойств подключения tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="419d4-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="419d4-199">Нажмите кнопку **ОК** tooclose hello **импорта данных** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="419d4-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="419d4-200">Повторно введите пароль hello hiveuser1 и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="419d4-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="419d4-201">Он занимает несколько секунд перед импортированных tooExcel получает данные.</span><span class="sxs-lookup"><span data-stu-id="419d4-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="419d4-202">После этого отобразятся 11 столбцов с данными.</span><span class="sxs-lookup"><span data-stu-id="419d4-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="419d4-203">Вторая политика hello tootest (чтения hivesampletable devicemake), созданный в разделе последнего hello</span><span class="sxs-lookup"><span data-stu-id="419d4-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="419d4-204">Добавьте новый лист в Excel.</span><span class="sxs-lookup"><span data-stu-id="419d4-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="419d4-205">Выполните hello последней процедуры tooimport hello данных.</span><span class="sxs-lookup"><span data-stu-id="419d4-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="419d4-206">Hello единственным изменением, которое будет производиться — toouse hiveuser2 учетные данные вместо hiveuser1 элемента.</span><span class="sxs-lookup"><span data-stu-id="419d4-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="419d4-207">Это будет ошибкой, поскольку hiveuser2 имеет только два столбца toosee разрешение.</span><span class="sxs-lookup"><span data-stu-id="419d4-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="419d4-208">Вы должны получить hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="419d4-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="419d4-209">Выполните hello же процедура tooimport данных.</span><span class="sxs-lookup"><span data-stu-id="419d4-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="419d4-210">На этот раз используйте учетные данные hiveuser2 и также измените hello инструкции select из:</span><span class="sxs-lookup"><span data-stu-id="419d4-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="419d4-211">на:</span><span class="sxs-lookup"><span data-stu-id="419d4-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="419d4-212">После этого импортируются два столбца с данными.</span><span class="sxs-lookup"><span data-stu-id="419d4-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="419d4-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="419d4-213">Next steps</span></span>
* <span data-ttu-id="419d4-214">Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="419d4-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="419d4-215">Сведения об управлении присоединенными к домену кластерами HDInsight см. в [этой статье](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="419d4-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="419d4-216">Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="419d4-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="419d4-217">Подключение Hive с помощью Hive JDBC, в разделе [подключения tooHive на Azure HDInsight с помощью драйвера Hive JDBC hello](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="419d4-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="419d4-218">TooHadoop соединения Excel с использованием Hive ODBC, в разделе [tooHadoop Excel подключиться с hello диска Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="419d4-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="419d4-219">TooHadoop соединения Excel с помощью Power Query, в разделе [tooHadoop Excel подключиться с помощью Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="419d4-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
