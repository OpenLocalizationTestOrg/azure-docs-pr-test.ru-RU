---
title: "aaaConnect tooHadoop Excel с hello Hive драйвер ODBC - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooset копирование и использование hello драйвер Microsoft Hive ODBC для tooquery данные Excel в кластерах HDInsight из Microsoft Excel."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="a8393-104">Подключение Excel tooHadoop в Azure HDInsight с драйвером Microsoft Hive ODBC hello</span><span class="sxs-lookup"><span data-stu-id="a8393-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="a8393-105">В решении для больших данных Майкрософт компоненты Microsoft Business Intelligence (BI) интегрируется с Apache Hadoop кластеры, которые были развернуты hello Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8393-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="a8393-106">Примером такой интеграции — hello возможность tooconnect Excel toohello Hive хранилище данных кластера Hadoop в HDInsight с помощью hello драйвера Microsoft Hive Open Database Connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="a8393-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="a8393-107">Также возможно tooconnect hello данные, связанные с кластера HDInsight и другим источникам данных, включая других (отличных от HDInsight) Hadoop, кластеров из Excel с помощью hello надстройки Microsoft Power Query для Excel.</span><span class="sxs-lookup"><span data-stu-id="a8393-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="a8393-108">Сведения об установке и использовании Power Query см. в разделе [tooHDInsight Excel подключиться с помощью Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="a8393-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="a8393-109">Хотя hello шаги в этой статье может использоваться с любой ОС Linux или кластера HDInsight под управлением Windows, Windows необходима для hello клиентской рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="a8393-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="a8393-110">**Предварительные требования**:</span><span class="sxs-lookup"><span data-stu-id="a8393-110">**Prerequisites**:</span></span>

<span data-ttu-id="a8393-111">Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a8393-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="a8393-112">**Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a8393-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="a8393-113">разделе toocreate, [Приступая к работе с Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="a8393-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="a8393-114">**Рабочая станция** с Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="a8393-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="a8393-115">Установка драйвера Microsoft Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="a8393-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="a8393-116">Загрузите и установите драйвер Microsoft ODBC Hive hello [центра загрузки Майкрософт][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="a8393-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="a8393-117">Этот драйвер можно установить на 32-разрядной или 64-разрядной версии Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 и Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a8393-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="a8393-118">драйвер Hello допускает подключения tooAzure HDInsight (версия 1.6 и более поздние версии) и эмулятор Azure HDInsight (v.1.0.0.0 и более поздние версии).</span><span class="sxs-lookup"><span data-stu-id="a8393-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="a8393-119">Должны установить hello версию, соответствующую версии hello приложения hello, где использовать драйвер ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="a8393-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="a8393-120">В этом учебнике hello драйвер используется в Office Excel.</span><span class="sxs-lookup"><span data-stu-id="a8393-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="a8393-121">Создание источника данных Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="a8393-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="a8393-122">Hello следующие шаги показывают, как toocreate Hive источника данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="a8393-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="a8393-123">Windows 8 или Windows 10, нажмите начальный экран приветствия Windows ключа tooopen hello, а затем введите **источники данных**.</span><span class="sxs-lookup"><span data-stu-id="a8393-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="a8393-124">Нажмите кнопку **Настройка источников данных ODBC (32-разр.)** или **Настройка источников данных ODBC (64-разр.)** в зависимости от версии Office.</span><span class="sxs-lookup"><span data-stu-id="a8393-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="a8393-125">Если вы используете Windows 7, выберите **Источники данных ODBC (32-разр.)** или **Источники данных ODBC (64-разр.)** в разделе **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="a8393-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="a8393-126">Вы увидите hello **администратор источников данных ODBC** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a8393-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="a8393-127">![Администратор источников данных ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Настройка DSN с помощью администратора источников данных ODBC")</span><span class="sxs-lookup"><span data-stu-id="a8393-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="a8393-128">От пользователя DNS, нажмите кнопку **добавить** tooopen hello **Создание нового источника данных** мастера.</span><span class="sxs-lookup"><span data-stu-id="a8393-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="a8393-129">Выберите **Драйвер Microsoft Hive ODBC** и щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a8393-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="a8393-130">Вы увидите hello **Microsoft Hive ODBC DNS установки драйвера** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a8393-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="a8393-131">Введите или выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a8393-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="a8393-132">Свойство</span><span class="sxs-lookup"><span data-stu-id="a8393-132">Property</span></span> | <span data-ttu-id="a8393-133">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8393-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a8393-134">Имя источника данных</span><span class="sxs-lookup"><span data-stu-id="a8393-134">Data Source Name</span></span> |<span data-ttu-id="a8393-135">Предоставьте имя источника данных tooyour</span><span class="sxs-lookup"><span data-stu-id="a8393-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="a8393-136">Узел</span><span class="sxs-lookup"><span data-stu-id="a8393-136">Host</span></span> |<span data-ttu-id="a8393-137">Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a8393-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="a8393-138">Например, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="a8393-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="a8393-139">Порт</span><span class="sxs-lookup"><span data-stu-id="a8393-139">Port</span></span> |<span data-ttu-id="a8393-140">Используйте <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="a8393-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="a8393-141">(Этот порт был изменен из 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="a8393-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="a8393-142">База данных</span><span class="sxs-lookup"><span data-stu-id="a8393-142">Database</span></span> |<span data-ttu-id="a8393-143">Используйте <strong>значение по умолчанию</strong>.</span><span class="sxs-lookup"><span data-stu-id="a8393-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="a8393-144">Механизм</span><span class="sxs-lookup"><span data-stu-id="a8393-144">Mechanism</span></span> |<span data-ttu-id="a8393-145">Выберите <strong>Служба Azure HDInsight</strong>.</span><span class="sxs-lookup"><span data-stu-id="a8393-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="a8393-146">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="a8393-146">User Name</span></span> |<span data-ttu-id="a8393-147">Введите имя пользователя HTTP кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8393-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="a8393-148">имя пользователя по умолчанию Hello <strong>администратора</strong>.</span><span class="sxs-lookup"><span data-stu-id="a8393-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="a8393-149">Пароль</span><span class="sxs-lookup"><span data-stu-id="a8393-149">Password</span></span> |<span data-ttu-id="a8393-150">Введите пароль пользователя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8393-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="a8393-151">Существуют некоторые важные параметры toobe, учитывать при нажатии кнопки **Дополнительно**:</span><span class="sxs-lookup"><span data-stu-id="a8393-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="a8393-152">Параметр</span><span class="sxs-lookup"><span data-stu-id="a8393-152">Parameter</span></span> | <span data-ttu-id="a8393-153">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8393-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a8393-154">Использовать исходный запрос</span><span class="sxs-lookup"><span data-stu-id="a8393-154">Use Native Query</span></span> |<span data-ttu-id="a8393-155">При этом, драйвер ODBC hello не предпринимает tooconvert TSQL в HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a8393-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="a8393-156">Следует использовать только при 100% уверенности в отправке действительных инструкций HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a8393-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="a8393-157">При подключении tooSQL сервера или базы данных SQL Azure, следует оставить этот флажок снят.</span><span class="sxs-lookup"><span data-stu-id="a8393-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="a8393-158">Строки, загружаемые для каждого блока</span><span class="sxs-lookup"><span data-stu-id="a8393-158">Rows fetched per block</span></span> |<span data-ttu-id="a8393-159">При получении большого количества записей, настройки этого параметра может быть обязательным tooensure оптимальную производительность.</span><span class="sxs-lookup"><span data-stu-id="a8393-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="a8393-160">Длина столбца строки по умолчанию, длина столбца двоичного кода, масштаб столбца десятичных значений</span><span class="sxs-lookup"><span data-stu-id="a8393-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="a8393-161">Тип данных Hello длины и точности могут повлиять на способ возвращаются данные.</span><span class="sxs-lookup"><span data-stu-id="a8393-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="a8393-162">Они могут вызывать toobe неверные сведения, возвращаемые из-за tooloss точности и/или усечения.</span><span class="sxs-lookup"><span data-stu-id="a8393-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="a8393-163">![Дополнительные параметры](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Дополнительные параметры конфигурации DSN")</span><span class="sxs-lookup"><span data-stu-id="a8393-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="a8393-164">Нажмите кнопку **тест** источника данных tootest hello.</span><span class="sxs-lookup"><span data-stu-id="a8393-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="a8393-165">При правильной настройке источника данных hello показывает *тесты успешно ЗАВЕРШЕНА!*.</span><span class="sxs-lookup"><span data-stu-id="a8393-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="a8393-166">Нажмите кнопку **ОК** tooclose hello проверить диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a8393-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="a8393-167">Hello нового источника данных должны отображаться на hello **администратор источников данных ODBC**.</span><span class="sxs-lookup"><span data-stu-id="a8393-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="a8393-168">Нажмите кнопку **ОК** tooexit приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="a8393-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="a8393-169">Импорт данных в Excel из службы HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8393-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="a8393-170">Hello следующие шаги описывают hello как tooimport данные из таблицы Hive в книгу Excel с использованием источника данных ODBC hello, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="a8393-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="a8393-171">Откройте новую или существующую рабочую книгу в Excel.</span><span class="sxs-lookup"><span data-stu-id="a8393-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="a8393-172">Из hello **данные** щелкните **получить данные**, нажмите кнопку **из других источников**и нажмите кнопку **из ODBC** toolaunch hello  **Мастер подключения данных**.</span><span class="sxs-lookup"><span data-stu-id="a8393-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="a8393-173">![Открытие мастера подключения к данным](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Открытие мастера подключения к данным")</span><span class="sxs-lookup"><span data-stu-id="a8393-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="a8393-174">Имя, созданный в последнем разделе hello источника данных выберите hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8393-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="a8393-175">Введите имя пользователя Hadoop (имя по умолчанию hello-admin) и hello пароль и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a8393-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="a8393-176">В навигаторе разверните узлы **HIVE**, **по умолчанию**, выберите **hivesampletable**, а затем нажмите кнопку **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="a8393-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="a8393-177">Он занимает несколько секунд перед импортированных tooExcel получает данные.</span><span class="sxs-lookup"><span data-stu-id="a8393-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="a8393-178">![Навигатор ODBC Hive в HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Открытие мастера подключения данных")</span><span class="sxs-lookup"><span data-stu-id="a8393-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="a8393-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8393-179">Next steps</span></span>
<span data-ttu-id="a8393-180">В этой статье вы узнали, как toouse hello данные tooretrieve драйвера Microsoft Hive ODBC из hello службы HDInsight в Excel.</span><span class="sxs-lookup"><span data-stu-id="a8393-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="a8393-181">Аналогичным образом могут получать данные из службы HDInsight hello в базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a8393-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="a8393-182">Это также возможно tooupload данных в службу HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8393-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="a8393-183">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="a8393-183">toolearn more, see:</span></span>

* <span data-ttu-id="a8393-184">[Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="a8393-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="a8393-185">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a8393-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a8393-186">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="a8393-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


