---
title: "aaaGet работы с сервером R в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocreate Apache усилить в кластере HDInsight, включающей сервер R и отправьте сценарий R в кластере hello."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Приступая к работе с R Server в HDInsight

HDInsight включает toobe параметр R Server интегрированы с кластером HDInsight. Этот параметр позволяет R-скриптов toouse Spark и MapReduce toorun распределенных вычислений. В этом документе вы узнаете, как toocreate сервера R на кластер HDInsight, а затем выполнения R-сценарий, который демонстрирует использование Spark для распределенных вычислений R.


## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure. Статья перейдите toohello [бесплатной пробной версии Microsoft Azure получить](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) Дополнительные сведения.
* **Клиент Secure Shell (SSH)**: клиент SSH используется tooremotely подключения кластера HDInsight toohello и выполнения команд непосредственно в кластере hello. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).
* **Ключи SSH (необязательно)**: hello SSH учетная запись, используемая tooconnect toohello кластера с помощью пароля или открытый ключ можно защитить. С помощью пароля проще и позволяет вам tooget работы без необходимости toocreate пару открытого и закрытого ключей. Тем не менее использовать ключ безопаснее.

> [!NOTE]
> Hello в этом документе предполагается, что вы используете пароль.


## <a name="automated-cluster-creation"></a>Автоматизированное создание кластера

Можно автоматизировать создание hello серверов HDInsight R, с помощью диспетчера ресурсов Azure шаблоны, hello SDK, а также PowerShell.

* toocreate R Server, с помощью шаблона управления ресурсами Azure, в разделе [развертывания кластера HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* toocreate значение R Server с помощью hello .NET SDK, в разделе [создавать кластеры под управлением Linux в HDInsight с помощью hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server с помощью powershell, см. в статье hello на [создание сервера R на HDInsight с помощью PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Создать кластер hello hello портал Azure

1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Выберите **Создать** -> **Аналитика** -> **HDInsight**.

    ![Изображение, на котором показано создание нового кластера](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. В hello **быстрое создание** возникают, введите имя кластера hello в hello **имя кластера** поля. Если у вас несколько подписок Azure, используйте hello **подписки** входа tooselect hello один требуется toouse.

    ![Выбор имени кластера и подписки](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Выберите **кластера типа** tooopen hello **конфигурации кластера** колонку. На hello **конфигурации кластера** колонке выберите hello следующие параметры:

    * **Тип кластера**: R Server.
    * **Версия**: hello выберите версию tooinstall R Server на кластере hello. в настоящее время доступная версия Hello ***9.1 R Server (HDI 3.6)***. Заметки о выпуске для hello доступные версии R Server доступны [здесь](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **R Studio community edition для R Server**: это интегрированная среда разработки на основе браузера устанавливается по умолчанию на узле edge hello. Если вы предпочитаете toonot установить его, а затем снимите флажок "hello". При выборе toohave он установлен, hello URL-адрес для доступа к приветствия входа RStudio сервер находится в колонке приложения портала для кластера после ее создания.
    * Для других параметров оставьте hello в значения по умолчанию hello и использовать hello **выберите** toosave hello кластера тип кнопки.

        ![Снимок экрана колонки "Тип кластера"](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Введите **имя пользователя** и **пароль** для входа в кластер.

    Укажите **имя пользователя SSH**. SSH находится используется tooremotely подключения кластера с помощью toohello **Secure Shell (SSH)** клиента. В этом диалоговом окне, или после создания кластера hello (на вкладке конфигурации hello для hello кластера) можно указать hello пользователя SSH. R Server является настроенным tooexpect **имя пользователя SSH** из «remoteuser».  **Если используется другое имя пользователя, необходимо выполнить дополнительные действия после создания кластера hello.**

    Оставьте поле hello, проверяется на **использовать одинаковый пароль в качестве учетной записи кластера** toouse **пароль** как hello тип проверки подлинности, если вы предпочитаете использовать открытый ключ.  Необходимо tooaccess пары открытого и закрытого ключей R Server на кластере hello посредством удаленного клиента, как, например, RTVS, RStudio или другого рабочего стола интегрированной среды разработки. При установке hello RStudio Server community edition необходимо toochoose пароль SSH.     

    toocreate и используйте пару открытого и закрытого ключей, снимите флажок **использовать одинаковый пароль в качестве учетной записи кластера** , а затем выберите **ОТКРЫТЫЙ ключ** и выполните следующие действия. При выполнении этих указаний предполагается, что установлена среда Cygwin с программой ssh-keygen или эквивалентным средством.

    * Создать пару открытого и закрытого ключей из командной строки hello переносного компьютера:

        ssh-keygen -t rsa -b 2048

    * Выполните запрос tooname hello файл ключа, а затем введите парольную фразу для повышения безопасности. Экран должен выглядеть примерно hello после изображения:

        ![Командная строка SSH в Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Эта команда создает файл закрытого ключа и файл открытого ключа в формате PUB имя < имя_файла закрытый ключ > hello, например furiosa и furiosa.pub.

        ![Каталог SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Затем укажите hello файла открытого ключа (&#42;. pub) при назначении HDI кластера учетные данные и окончательный своей группы ресурсов и область и выберите **Далее**.

        ![Колонка учетных данных](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Изменить разрешения для закрытого keyfile hello переносного компьютера:

        chmod 600 <имя_файла_закрытого ключа>

   * Используйте файл закрытого ключа hello с SSH для удаленного входа:

        ssh –i <имя_файла_закрытого_ключа> remoteuser@<hostname public ip>.

      Кроме того, как часть определения hello Hadoop Spark контекста вычислений R сервера на приветствия клиента. В разделе hello **с помощью Microsoft R Server как клиент Hadoop** подраздела в [создать контекст вычислений для Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Hello быстрое создание переходов, которые toohello **хранения** колонке учетной записи для хранения tooselect hello toobe параметры, используемые для первичного расположения hello hello HDFS файловой системы, используемой кластером hello. Выберите новую или существующую учетную запись хранения Azure или существующую учетную запись Data Lake Store.

    - При выборе учетной записи хранилища Azure, выбрав выбран существующую учетную запись хранения **выберите учетную запись хранения** и выбрав соответствующий счет hello. Создание учетной записи с помощью hello **создать новый** ссылку в hello **выберите учетную запись хранения** раздела.

      > [!NOTE]
      > При выборе **New** необходимо ввести имя для новой учетной записи хранения hello. Зеленый флажок отображается, если принимается имя hello.

      Hello **контейнер по умолчанию** имя toohello значения по умолчанию hello кластера. Оставьте это значение по умолчанию значение hello.

      Если был выбран новый параметр учетной записи хранилища prompt tooselect **расположение** является данный tooselect какой области toocreate hello учетной записи хранилища.  

         ![Колонка "Источник данных"](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Выбор расположения hello для источника данных по умолчанию hello также устанавливает hello расположение кластера HDInsight hello. Hello кластер и по умолчанию источник данных должен быть в hello одного региона.

    - Если вы хотите toouse существующее хранилище Озера данных, выберите hello toouse учетной записи хранения ADLS кластер и добавьте hello *добавить* toohello удостоверение tooyour кластера tooallow доступа к магазину. Дополнительные сведения об этом процессе см. в статье [Создание кластера HDInsight с хранилищем Data Lake Store с помощью портала Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Используйте hello **выберите** конфигурации источника данных hello toosave кнопки.


7. Hello **Сводка** колонке выведет toovalidate все параметры. Здесь можно изменить ваш **размер кластера** toomodify hello количества серверов в кластере, а также указать любой **скрипт действия** требуется toorun. Если нет уверенности, что требуется больший размер кластера, оставьте hello число узлов рабочих ролей по умолчанию hello `4`. Hello оценочная стоимость hello кластера отображается в колонке hello.

    ![Сводка по кластерам](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > При необходимости можно изменить размер кластера позже через портал hello (**кластера** -> **параметры** -> **кластера масштабирования**) tooincrease или Уменьшите число рабочих узлов в hello.  Это изменение размера можно использовать на переход из состояния простоя работу кластера hello не во время работы, или добавление потребностях hello toomeet крупных задач.
   >
   >

   Некоторые факторы tookeep в виду при планировании размера вашего кластера, узлы данных hello и hello граничного узла включают:  

   * Hello производительность распределенных анализа R Server Spark при пропорционально toohello число рабочих узлов hello данных велик.  

   * R Server анализ производительности Hello линейно hello размер анализируемые данные. Например:  

     * Для данных небольшого toomodest производительности лучше при анализе в локальный контекст вычислений на hello граничного узла.  Дополнительные сведения о сценариях hello, при которых локального hello и Spark вычислительных контекстов лучше всего работают см. в разделе параметры контекста вычислений R Server на HDInsight.<br>
     * При входе в toohello граничного узла, выполнить сценарий R, а затем выполняются все, кроме hello функциям rx ScaleR <strong>локально</strong> на hello граничного узла. Поэтому hello памяти и количество ядер hello edge узла должен определяться соответствующим образом. Здравствуйте, же правило применяется при использовании R Server на HDI качестве контекста удаленных вычислений на ноутбуке.

     ![Колонка "Ценовые категории узла"](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Используйте hello **выберите** кнопку toosave hello узел цены конфигурации.

   Обратите внимание на ссылку для **скачивания шаблона и параметров**. Щелкните этот сценарии toodisplay ссылки, используемые tooautomate hello создания кластера с выбранной конфигурацией hello. Эти сценарии также доступны из hello Azure портала запись для кластера после его создания.

   > [!NOTE]
   > Потребуется некоторое время для hello кластера toobe создана, обычно около 20 минут. Используйте плитки приветствия на начальной панели hello или hello **уведомления** входа на hello слева от toocheck страницы приветствия на процесс создания hello.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Подключение tooRStudio сервера

Если вы выбрали tooinclude RStudio Server community edition в вашей установке, то можно получить доступ к hello RStudio входа через два метода.

1. Go toohello URL-адреса (где **CLUSTERNAME** — имя кластера hello hello):

    https://**имя_кластера**.azurehdinsight.net/rstudio/.

2. Откройте hello запись для кластера в hello портал Azure, выберите hello **панели мониторинга сервера R** быструю ссылку и выбрав hello **R Studio мониторинга**:

     ![Панель мониторинга studio hello R доступа](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Панель мониторинга studio hello R доступа](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Независимо от того, используется метод hello hello при первом входе необходимо tooauthenticate дважды.  В первой проверки подлинности hello предоставляют hello *кластера Admin userid* и *пароль*. Во второй строке hello предоставляют hello *SSH userid* и *пароль*. Последующие журнала модулей требуются только hello *пароль SSH* и *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Подключить узел edge toohello R Server

Подключение tooR сервера граничного узла кластера HDInsight hello, с помощью SSH с hello команды:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Можно найти hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` адрес в hello портал Azure, затем выбрав кластера **все параметры** -> **приложения** -> **сценария RServer**. При этом отображаются сведения о конечной точке SSH для hello граничного узла hello.
>
> ![Изображение hello конечной точки SSH для hello граничного узла](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Если вы использовали toosecure пароль учетной записи пользователя SSH, не запрошенные tooenter его. Если используется открытый ключ, возможно, toouse hello `-i` toospecify параметр hello соответствующим закрытым ключом. Например:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Дополнительные сведения см. в разделе [tooHDInsight (Hadoop) с помощью SSH подключения](hdinsight-hadoop-linux-use-ssh-unix.md).

После подключения вы прибудете в запрос примерно следующие toohello:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Включение нескольких параллельных подключений пользователей

Можно включить несколько одновременных пользователей путем добавления дополнительных пользователей для hello граничного узла, на какие hello сообщества RStudio работает версия.

При создании кластера HDInsight необходимо указать двух пользователей: для HTTP и SSH.

![Параллельное подключение пользователя 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Кластер пользователя для входа**: пользователь с HTTP для проверки подлинности через шлюз hello HDInsight, используемых tooprotect hello HDInsight кластеры был создан. Этот пользователь HTTP является hello используется tooaccess Ambari пользовательского интерфейса, YARN пользовательского интерфейса, а также другие компоненты пользовательского интерфейса.
- **Безопасное имя пользователя Shell (SSH)**: tooaccess hello SSH пользователя кластера через безопасный оболочки. Этот пользователь является пользователем в системе Linux для всех hello головного узла, рабочих узлов и узлов edge hello. Чтобы можно было использовать безопасные оболочки tooaccess любой из узлов hello в удаленном кластере.

R Studio Server Community Hello, используемой в hello Microsoft R Server в кластере HDInsight типа принимает только Linux имя пользователя и пароль как механизм входа. Эта версия не поддерживает передачу токенов. Таким образом, если вы создали новый кластер и хотите tooaccess toouse R Studio, необходимо toolog в два раза.

- Сначала вход с использованием учетных данных пользователя hello HTTP через hello HDInsight шлюз: 

    ![Параллельное подключение пользователя 2а](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Затем используйте toolog учетные данные пользователя SSH hello в tooRStudio:
  
    ![Параллельное подключение пользователя 2б](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Сейчас при подготовке кластера HDInsight можно создать только одну учетную запись пользователя SSH. Поэтому tooenable кластеры tooaccess несколько пользователей Microsoft R Server на HDInsight, нужно toocreate дополнительных пользователей в системе Linux hello.

Поскольку сообщества RStudio сервер работает под управлением кластера hello граничного узла, существуют несколько шагов в здесь:

1. Используйте toolog пользователя SSH hello создан в toohello граничного узла
2. добавить нескольких пользователей Linux на граничный узел;
3. Сообщество RStudio версию использовать созданные пользователем hello

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Шаг 1: Используйте toolog пользователя SSH hello создан в toohello граничного узла

Загрузить все средства SSH (например, Putty) и использовать существующие toolog пользователя SSH hello в. Затем следуйте инструкциям hello в [подключения tooHDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello граничного узла. адрес узла Hello edge для R Server в кластере HDInsight: *имя_кластера ed ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Шаг 2. Добавление дополнительных пользователей Linux на граничный узел

tooadd граничного узла toohello пользователя, выполнения команд hello:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Вы должны увидеть следующие элементы, которые возвращаются hello. 

![Параллельное подключение пользователя 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

При появлении запроса «текущий пароль Kerberos:», просто нажмите клавиши **ввод** tooignore его. Hello `-m` в диалоговом окне `useradd` команда указывает, что hello система будет создавать домашнюю папку пользователя hello, необходимый для версия RStudio сообщества.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Шаг 3: Использование RStudio сообщества версии с созданные пользователем hello

Используйте созданные пользователем toolog hello в tooRStudio:

![Параллельное подключение пользователя 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Обратите внимание, что RStudio указывает, что вы используете hello нового пользователя (здесь, например, *sshuser6*) toolog hello кластера: 

![Параллельное подключение пользователя 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Вы можете также войти с использованием учетных данных исходной hello (по умолчанию — *sshuser*) одновременно в другом окне браузера.

Вы можете отправлять задания с помощью функций scaleR. Ниже приведен пример команды, используемые toorun hello задания:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Обратите внимание, что задания hello отправлен под другим именем пользователя в пользовательском Интерфейсе YARN:

![Параллельное подключение пользователя 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Обратите внимание также, hello новых добавленных пользователей нет корневого привилегии в системе Linux, но они имеют hello в одном получить доступ к файлам hello tooall в hello HDFS и WASB хранилище.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>С помощью консоли hello R

1. Из сеанса SSH hello используйте следующие командной консоли hello R toostart hello:  

        R

2. Вы увидите примерно toohello следующие выходные данные:
    
    R версии 3.2.2 (2015-08-14) — «Пожара Safety» авторское право (C) 2015 hello R Foundation для платформы статистических вычислений: x86_64-pc-linux-gnu (64-разрядная версия)

    R is free software and comes with ABSOLUTELY NO WARRANTY.
    Вы являетесь приветствия tooredistribute его при определенных условиях.
    Type 'license()' or 'licence()' for distribution details.

    Natural language support but running in an English locale

    R is a collaborative project with many contributors.
    Введите «contributors()» Дополнительные сведения и «citation()» на как пакеты toocite R или R в публикациях.

    Введите «demo()» для некоторых демонстрациям, «help()» для интерактивной справки или «help.start()» для toohelp интерфейс браузера HTML.
    Введите «q()» tooquit R.

    Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation

    Type 'readme()' for release notes.
    >

3. Из hello `>` запрос, можно ввести код R. R server содержит пакеты, которые позволяют вам tooeasily взаимодействовать с Hadoop и выполнения распределенных вычислений. Например можно используйте следующие команды tooview hello корневой hello по умолчанию файловой системы для кластера HDInsight hello hello:

    rxHadoopListFiles("/")

4. Также можно использовать hello WASB стиль адресации.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Использование R Server в HDI из удаленного экземпляра Microsoft R Server или клиента Microsoft R Client

Это возможно tooset контекст вычислений HDI Hadoop Spark toohello доступа из удаленного экземпляра Microsoft R Server или Microsoft R клиента, запущенного на настольном ПК или ноутбуке. В разделе **с помощью Microsoft R Server как клиент Hadoop** подразделов в hello [создание контекста вычислений для Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo таким образом, требуются следующие параметры при определении контекста вычислений RxSpark hello на вашем ноутбуке hello toospecify: hdfsShareDir shareDir, sshUsername, sshHostname sshSwitches и sshProfileScript. Например:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Использование контекста вычислений

Контекст вычислений позволяет toocontrol ли вычисление выполнить локально на узле edge hello или распределяется hello узлов в кластере HDInsight hello.

1. В RStudio сервер или консоль hello R (в сеанс SSH) используйте следующий код tooload пример данных в хранилище по умолчанию hello для HDInsight hello:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Теперь давайте создавать некоторые сведения о данных и определены два источника данных, чтобы мы могли работать с данными hello.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Запустим логистической регрессии hello данных с помощью hello Локальный Контекст вычислений.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Вы увидите выходные данные, заканчивающиеся строки аналогично toohello следующие:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Далее запустим hello же логистической регрессии, используя контекст Spark hello. контекст Spark Hello распределяет обработку всех hello рабочих узлов в кластере HDInsight hello hello.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Также можно использовать toodistribute вычислений MapReduce узлах кластера. Дополнительные сведения о контексте вычислений см. в статье с описанием [параметров контекста вычислений для R Server в HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>Распространение узлов toomultiple кода R

R Server позволяет легко использования существующего кода R и запустите его на нескольких узлах в кластере hello с помощью `rxExec`. Эта функция удобна при очистке параметров или моделировании. Hello следующий код является примером toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Если по-прежнему используется hello Spark или контекст MapReduce, эта команда возвращает значение имя_узла hello для hello рабочих узлов кода hello `(Sys.info()["nodename"])` выполняется на. Например на четыре узла кластера, ожидается, что tooreceive вывода аналогичные toohello следующее:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Доступ к данным в Hive и Parquet

Компонент, доступный в R Server 9.1 позволяет toodata прямой доступ в Hive и Parquet для использования функций ScaleR в контексте вычислений Spark hello. Эти возможности доступны в новых данных источника функций ScaleR RxHiveData и RxParquetData, работающие с использованием данных tooload Spark SQL непосредственно в кадр данных под Spark для анализа, ScaleR.  

После кода Hello предоставляет пример кода на использование новых функций hello.

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Дополнительные сведения об использование этих новых функций см hello R Server с использованием hello `?RxHivedata` и `?RxParquetData` команд.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Установка дополнительных пакетов R на hello граничного узла

Если необходима поддержка дополнительных пакетов R tooinstall на hello граничного узла, можно использовать `install.packages()` непосредственно из среды hello консоли R: При подключенном toohello ребро узел через SSH. Тем не менее если вам требуется tooinstall пакеты R на узлах рабочих hello hello кластера, необходимо использовать действие сценария.

Действия сценариев, Bash-скриптов, используемых toomake конфигурации изменения toohello HDInsight кластера или tooinstall дополнительное программное обеспечение, например дополнительных пакетов R. tooinstall дополнительных пакетов с помощью действия сценария, hello используйте следующие шаги:

> [!IMPORTANT]
> С помощью дополнительных пакетов R действия скрипта tooinstall может использоваться только после создания кластера hello. Не используйте эту процедуру при создании кластера как hello сценария зависит от сервера R, полностью установлен и настроен.
>
>

1. Из hello [портал Azure](https://portal.azure.com), выберите R-сервер в кластере HDInsight.

2. Из hello **параметры** колонке выберите **действия скрипта** и затем **отправить новый** toosubmit новое действие скрипта.

   ![Изображение колонки "Действия скрипта"](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Из hello **отправить действие скрипта** колонке предоставляют hello следующую информацию:

   * **Имя**: понятное имя tooidentify этот сценарий

   * **URI bash-скрипта**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Заголовок**: флажок для этого элемента должен быть **снят**.

   * **Рабочая роль**: флажок для этого элемента должен быть **установлен**.

   * **Пограничные узлы**: флажок для этого элемента должен быть **снят**.

   * **Zookeeper**: флажок для этого элемента должен быть **снят**.

   * **Параметры**: hello R пакеты toobe установлен. Например, `bitops stringr arules`

   * **Сохранить этот скрипт…**: флажок для этого элемента должен быть **установлен**.  

   > [!NOTE]
   > 1. По умолчанию все пакеты R установлены из моментального снимка репозитория Microsoft MRAN hello согласование с версией hello сервера R, который был установлен. Если требуется более новых версий пакетов tooinstall нет риску несовместимости. Тем не менее возможна установка такого рода, указав `useCRAN` как hello перечисления первый элемент hello пакета, например `useCRAN bitops, stringr, arules`.  
   > 2. Для некоторых пакетов R требуются дополнительные системные библиотеки Linux. Для удобства имеют предварительно установленное Затребован hello top 100 наиболее популярных пакетов r. зависимости hello. Тем не менее если пакеты R hello устанавливаемого необходимы библиотеки Помимо этих затем необходимо загрузить здесь используется базовый скрипт hello и добавить действия tooinstall hello системные библиотеки. Необходимо затем public tooa скрипт изменения hello передачи больших двоичных объектов контейнера в хранилище Azure и использовать пакеты hello tooinstall скрипт изменения hello.
   >    Дополнительные сведения см. в статье [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Добавление действия сценария](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Выберите **создать** toorun hello скрипта. После завершения сценария hello hello R-пакеты доступны на всех рабочих узлов.


## <a name="using-microsoft-r-server-operationalization"></a>Ввод в эксплуатацию для Microsoft R Server

По завершении моделирование данных вы ввода в эксплуатацию hello модели toomake прогнозов. tooconfigure для ввода в эксплуатацию Microsoft R Server, выполните следующие шаги hello.

Во-первых, ssh в hello граничного узла. Например, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

После использования ssh, измените каталог для соответствующей версии hello и sudo hello dotnet dll: 

- Для Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0 sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Для Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1 sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

tooconfigure Microsoft R Server ввода в эксплуатацию в одно поле конфигурации hello следующие:

1. Выберите Configure R Server for Operationalization (Настройка R Server для ввода в эксплуатацию).
2. Выберите "A. One-box (web + compute nodes)" (A. Универсальная (веб + вычислительные узлы)).
3. Введите пароль для hello **администратора** пользователя

![Универсальная конфигурация](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

В качестве дополнительного шага можно запустить диагностический тест, как показано ниже.

1. Выберите "6. Run diagnostic tests" (6. Запуск диагностических тестов).
2. Выберите "A. Test configuration" (А. Проверка конфигурации).
3. Введите имя пользователя admin и пароль, настроенный на предыдущем шаге.
4. Убедитесь, что общая проверка работоспособности проходит успешно (Overall Health = pass).
5. Программа администрирования hello выхода
6. Завершите сеанс SSH.

![Диагностика перед вводом в эксплуатацию](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Длительные задержки при использовании веб-службы на Spark**
>
>Если возникают значительные задержки при попытке tooconsume веб-службы с mrsdeploy функции в контексте вычислений Spark, может потребоваться tooadd некоторые отсутствующие папки. Spark приложения Hello принадлежит tooa пользователя с именем "*rserve2*" каждый раз, когда она вызывается из веб-службы с помощью функции mrsdeploy. toowork этой проблемы:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


На этом этапе будет завершена настройка hello для ввода в эксплуатацию. Теперь вы можете использовать mrsdeploy «hello» пакет в вашей toohello tooconnect RClient ввода в эксплуатацию на граничного узла и приступить к использованию, ее функции, такие как [удаленное выполнение](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) и [веб-службы](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). В зависимости от того, является ли кластер настроен в виртуальной сети или нет может понадобиться tooset копирование прямой туннелирования порта с помощью имени входа SSH. Hello следующих разделах объясняется, как tooset копирование этот туннель.

### <a name="rserver-cluster-on-virtual-network"></a>Кластер R Server в виртуальной сети

Убедитесь, что прохождение трафика через порт 12800 toohello граничного узла. Таким образом, можно использовать функция hello edge узла tooconnect toohello ввода в эксплуатацию.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Если hello `remoteLogin()` невозможно подключение toohello граничного узла, но можно SSH toohello граничного узла, затем требуется tooverify ли hello правило tooallow трафик через порт 12800 установлено должным образом или не. В случае продолжения tooface hello проблему можно обойти путем настройки прямого туннелирования порта с помощью SSH. Инструкции см. в следующем разделе hello.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Кластер RServer не настроен в виртуальной сети

Если ваш кластер не настроен в виртуальной сети или с подключением через виртуальную сеть возникают проблемы, можно использовать туннелирование с перенаправлением портов через SSH:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Также это можно настроить с помощью программы Putty.

![Подключение SSH через Putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Hello трафика с порта компьютера 12800 активен сеанс SSH, будут отправлены toohello граничного узла порт 12800 через сеанс SSH. Убедитесь, что вы используете `127.0.0.1:12800` в методе `remoteLogin()`. Регистрирует ввода в эксплуатацию toohello граничного узла через перенаправления портов.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Как tooscale Microsoft R Server ввода в эксплуатацию вычислительных узлов на HDInsight рабочих узлов

### <a name="decommission-hello-worker-nodes"></a>Списание узлы рабочих hello

Управление Microsoft R Server через Yarn сейчас не поддерживается. Hello рабочих узлов, не выводится из эксплуатации, hello Yarn диспетчер ресурсов не будет работать, как ожидается, поскольку он не будет знать о они занимают hello server ресурсов hello. В порядке tooavoid этой ситуации рекомендуется списание hello рабочих узлов, прежде чем масштабировать hello вычислительных узлов.

Действия toodecommissioning рабочих узлов:

* Войдите в консоль Ambari tooHDI кластера и нажмите на вкладке «узлы»
* Выберите рабочих узлов (toobe вывода из эксплуатации), щелкните «Действия» > «Выбранные узлы» > «Узлы» > щелкните «Включить режим обслуживания ON». Например в следующие изображения hello мы выбрали wn3 и wn4 toodecommission.  

   ![Вывод рабочих узлов из эксплуатации](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **DataNodes** (Узлы данных) и щелкните **Decommission** (Вывести из эксплуатации).
* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **NodeManagers** (Диспетчеры узлов) и щелкните **Decommission** (Вывести из эксплуатации).
* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **DataNodes** (Узлы данных) и щелкните **Stop** (Остановить).
* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **NodeManagers** (Диспетчеры узлов) и щелкните **Stop** (Остановить).
* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **Hosts** (Узлы) и щелкните **Stop All Components** (Остановить все компоненты).
* Снимите флажок hello рабочих узлов, а затем выберите hello головного узла
* Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **Hosts** (Узлы) > **Restart All Components** (Перезапустить все компоненты).

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Настройка вычислительных узлов на каждом из рабочих узлов, выведенных из эксплуатации

1. Поочередно откройте сеанс SSH для каждого рабочего узла, выведенного из эксплуатации.
2. Запустите служебную программу администрирования с помощью `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Введите «1» tooselect параметр «Настройка R Server для ввода в эксплуатацию».
4. Введите «c» tooselect параметр «C. Compute node" (C. Вычислительный узел). Это настраивает hello вычислительных узлов на узле hello работника.
5. Программа администрирования hello выхода.

### <a name="add-compute-nodes-details-on-web-node"></a>Добавление сведений о вычислительных узлах на веб-узел

После настройки всех списанных рабочих узлов toorun вычислительного узла, вернитесь на hello граничного узла и добавления узлов Отмененный рабочий IP-адресов в конфигурации узла для hello Microsoft R Server web:

* SSH в hello граничного узла.
* Запустите `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Найдите раздел «Идентификаторы URI» hello и добавьте рабочий узел IP-адрес и сведения о порте.

    ![Командная строка для выведенных из эксплуатации рабочих узлов](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Дальнейшие действия

Теперь следует понимать, как toocreate новый кластер HDInsight, включающий hello R Server и hello основные принципы использования hello консоль R из сеанса SSH. Hello следующих разделах описаны другие способы управления и работы с сервером R в HDInsight:

* [Добавить tooHDInsight RStudio сервера (если не устанавливается во время создания кластера)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Варианты контекста вычислений для R Server в HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-storage.md)
