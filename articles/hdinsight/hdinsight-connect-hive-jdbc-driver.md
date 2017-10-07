---
title: "aaaQuery Hive через драйвер JDBC hello - Azure HDInsight | Документы Microsoft"
description: "Используйте драйвер JDBC hello от tooHadoop запросов приложения toosubmit Java Hive в HDInsight. Подключите программными средствами, а от клиента SQL белка hello."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="26a2b-104">Запрос Hive через драйвер JDBC hello в HDInsight</span><span class="sxs-lookup"><span data-stu-id="26a2b-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="26a2b-105">Узнайте, как драйвер JDBC hello toouse из toosubmit приложения Java Hive запрашивает tooHadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="26a2b-106">Hello сведения в этом документе показано, как tooconnect программно и с hello белка клиента SQL.</span><span class="sxs-lookup"><span data-stu-id="26a2b-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="26a2b-107">Дополнительные сведения о hello Hive интерфейса JDBC см. в разделе [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="26a2b-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26a2b-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26a2b-108">Prerequisites</span></span>

* <span data-ttu-id="26a2b-109">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="26a2b-110">Работают кластеры либо под управлением Linux, либо под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="26a2b-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="26a2b-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="26a2b-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="26a2b-112">Дополнительные сведения см. в разделе о [прекращении поддержки HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="26a2b-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="26a2b-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="26a2b-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="26a2b-114">SQuirreL представляет собой клиентское приложение JDBC.</span><span class="sxs-lookup"><span data-stu-id="26a2b-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="26a2b-115">Hello [Java Developer Kit (JDK) версии 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="26a2b-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="26a2b-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="26a2b-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="26a2b-117">Maven — проект создания системы проектов Java, используемый hello проект, связанный с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="26a2b-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="26a2b-118">Строка подключения JDBC</span><span class="sxs-lookup"><span data-stu-id="26a2b-118">JDBC connection string</span></span>

<span data-ttu-id="26a2b-119">Кластер HDInsight tooan соединения JDBC на платформе Azure становятся более 443 и hello трафик защищается с помощью протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="26a2b-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="26a2b-120">Hello открытый шлюза, который hello кластеров находятся за перенаправляет hello трафика toohello порт, который HiveServer2 факта прослушивания.</span><span class="sxs-lookup"><span data-stu-id="26a2b-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="26a2b-121">Hello ниже приведен пример строки подключения:</span><span class="sxs-lookup"><span data-stu-id="26a2b-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="26a2b-122">Замените `CLUSTERNAME` с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="26a2b-123">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="26a2b-123">Authentication</span></span>

<span data-ttu-id="26a2b-124">При установке соединения hello, необходимо использовать hello HDInsight кластер admin имя и пароль tooauthenticate toohello кластера шлюза.</span><span class="sxs-lookup"><span data-stu-id="26a2b-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="26a2b-125">При соединении с JDBC клиентов, таких как белка SQL, необходимо ввести имя администратора hello и пароль в параметрах клиента.</span><span class="sxs-lookup"><span data-stu-id="26a2b-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="26a2b-126">Из приложения Java необходимо использовать hello имя и пароль при установлении соединения.</span><span class="sxs-lookup"><span data-stu-id="26a2b-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="26a2b-127">Например hello ниже код Java открывает новое соединение с помощью строки подключения hello, имя администратора и пароль:</span><span class="sxs-lookup"><span data-stu-id="26a2b-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="26a2b-128">Подключение с использованием клиента SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="26a2b-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="26a2b-129">Белка SQL является клиентом JDBC, может быть используется tooremotely выполнения запросов Hive с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="26a2b-130">Hello следующие шаги предполагают, что вы уже установили белка SQL.</span><span class="sxs-lookup"><span data-stu-id="26a2b-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="26a2b-131">Скопируйте драйверы Hive JDBC hello из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="26a2b-132">Для **HDInsight под управлением Linux**, используйте hello следующие шаги, необходимые hello toodownload jar-файла.</span><span class="sxs-lookup"><span data-stu-id="26a2b-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="26a2b-133">Создайте каталог, содержащий файлы hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="26a2b-134">Например, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="26a2b-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="26a2b-135">Из командной строки используйте hello следующими командами toocopy hello файлы из кластера HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="26a2b-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="26a2b-136">Замените `USERNAME` с именем учетной записи пользователя hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="26a2b-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="26a2b-137">Замените `CLUSTERNAME` с именем кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="26a2b-138">Для **HDInsight под управлением Windows**, используйте hello следующие шаги toodownload hello jar-файла.</span><span class="sxs-lookup"><span data-stu-id="26a2b-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="26a2b-139">Из hello портал Azure, выберите ваш HDInsight кластер, а затем выберите hello **удаленного рабочего стола** значок.</span><span class="sxs-lookup"><span data-stu-id="26a2b-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Значок удаленного рабочего стола](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="26a2b-141">В колонке hello удаленного рабочего стола, используйте hello **Connect** кнопку tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="26a2b-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="26a2b-142">Если hello удаленный рабочий стол не включен, используйте форму hello tooprovide имя пользователя и пароль, а затем выберите **включить** tooenable удаленного рабочего стола для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Колонка удаленного рабочего стола](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="26a2b-144">После нажатия кнопки **Подключить** будет скачан RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="26a2b-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="26a2b-145">Используйте этот клиент удаленного рабочего стола hello toolaunch файлов.</span><span class="sxs-lookup"><span data-stu-id="26a2b-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="26a2b-146">При появлении запроса используйте hello имя пользователя и пароль для доступа к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="26a2b-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="26a2b-147">После подключения, скопируйте следующие файлы с локального компьютера сеанса удаленного рабочего стола tooyour hello hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="26a2b-148">Поместите их в локальный каталог с именем `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="26a2b-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="26a2b-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="26a2b-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="26a2b-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="26a2b-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="26a2b-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="26a2b-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="26a2b-152">версии Hello чисел, включенных в hello пути и имена файлов может быть разным для кластера.</span><span class="sxs-lookup"><span data-stu-id="26a2b-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="26a2b-153">Отключение сеанса удаленного рабочего стола hello после завершения копирования файлов hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="26a2b-154">Запустите приложение hello белка SQL.</span><span class="sxs-lookup"><span data-stu-id="26a2b-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="26a2b-155">Hello левого края окна hello, выберите **драйверы**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Hello левой части окна hello: вкладка драйверов](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="26a2b-157">Из значков hello вверху hello hello **драйверы** диалоговое окно, выберите hello  **+**  toocreate значок драйвера.</span><span class="sxs-lookup"><span data-stu-id="26a2b-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Значки драйверов](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="26a2b-159">В диалоговом окне Добавление драйвера hello добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="26a2b-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="26a2b-160">**Имя:** Hive.</span><span class="sxs-lookup"><span data-stu-id="26a2b-160">**Name**: Hive</span></span>
    * <span data-ttu-id="26a2b-161">**Пример URL-адреса:** `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="26a2b-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="26a2b-162">**Дополнительный путь к классу**: используйте hello добавить кнопку tooadd hello jar-файла загружены ранее</span><span class="sxs-lookup"><span data-stu-id="26a2b-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="26a2b-163">**Имя класса:** org.apache.hive.jdbc.HiveDriver.</span><span class="sxs-lookup"><span data-stu-id="26a2b-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![диалоговое окно "Добавить драйвер"](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="26a2b-165">Нажмите кнопку **ОК** toosave эти параметры.</span><span class="sxs-lookup"><span data-stu-id="26a2b-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="26a2b-166">Hello левой части окна hello белка SQL, выберите **псевдонимы**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="26a2b-167">Нажмите кнопку hello  **+**  toocreate значок псевдоним соединения.</span><span class="sxs-lookup"><span data-stu-id="26a2b-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![добавление нового псевдонима](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="26a2b-169">Используйте hello следующие значения для hello **добавить псевдоним** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="26a2b-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="26a2b-170">**Имя:** Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="26a2b-171">**Драйвер**: раскрывающийся список tooselect используйте hello hello **Hive** драйвера</span><span class="sxs-lookup"><span data-stu-id="26a2b-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="26a2b-172">**URL-адрес**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="26a2b-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="26a2b-173">Замените **CLUSTERNAME** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="26a2b-174">**Имя пользователя**: имя учетной записи входа hello кластера для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="26a2b-175">по умолчанию Hello — `admin`.</span><span class="sxs-lookup"><span data-stu-id="26a2b-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="26a2b-176">**Пароль**: hello пароль для учетной записи входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="26a2b-176">**Password**: hello password for hello cluster login account.</span></span>

 ![диалоговое окно "Добавить псевдоним"](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="26a2b-178">Используйте hello **тест** tooverify кнопки, hello подключение работает.</span><span class="sxs-lookup"><span data-stu-id="26a2b-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="26a2b-179">При **соединиться: Hive в HDInsight** откроется диалоговое окно, выберите **Connect** tooperform hello теста.</span><span class="sxs-lookup"><span data-stu-id="26a2b-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="26a2b-180">Если hello выполнен успешно, появится **подключение выполнено успешно** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="26a2b-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="26a2b-181">подключение hello toosave псевдоним, использовать hello **ОК** кнопку внизу hello hello **добавить псевдоним** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="26a2b-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="26a2b-182">Из hello **подключиться к** выберите в раскрывающемся списке вверху hello SQL белка **Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="26a2b-183">При появлении запроса выберите **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-183">When prompted, select **Connect**.</span></span>

    ![диалоговое окно подключения](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="26a2b-185">После подключения введите hello ниже запроса в диалоговом окне запроса SQL hello, а затем выберите hello **запуска** значок.</span><span class="sxs-lookup"><span data-stu-id="26a2b-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="26a2b-186">область результатов Hello должны показывать hello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![диалоговое окно запроса SQL с результатами запроса](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="26a2b-188">Подключение из примера приложения Java</span><span class="sxs-lookup"><span data-stu-id="26a2b-188">Connect from an example Java application</span></span>

<span data-ttu-id="26a2b-189">Пример использования tooquery клиента Java Hive в HDInsight доступна на [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="26a2b-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="26a2b-190">Следуйте инструкциям hello toobuild репозитория hello и запуск образца hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="26a2b-191">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="26a2b-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="26a2b-192">Произошла неожиданная ошибка при попытке tooopen SQL-соединение</span><span class="sxs-lookup"><span data-stu-id="26a2b-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="26a2b-193">**Симптомы**: при подключении кластера HDInsight tooan версии 3.3 или 3.4, может появиться сообщение об ошибке с произошла непредвиденная ошибка.</span><span class="sxs-lookup"><span data-stu-id="26a2b-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="26a2b-194">Hello трассировку стека для этой ошибки начинается со слова hello, следующие строки:</span><span class="sxs-lookup"><span data-stu-id="26a2b-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="26a2b-195">**Причина**: Эта ошибка возникает при несоответствии hello версию файла commons codec.jar hello, используемые белка и hello один необходимые компоненты Hive JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="26a2b-196">**Разрешение**: toofix эту ошибку, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="26a2b-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="26a2b-197">Загрузите файл jar кодек commons hello с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="26a2b-198">Выйти из белка, а затем перейдите toohello directory установленным белка в вашей системе.</span><span class="sxs-lookup"><span data-stu-id="26a2b-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="26a2b-199">В каталоге белка hello, hello `lib` directory замены hello существующих commons-codec.jar с hello загрузить один из кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="26a2b-200">Перезапустите SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="26a2b-200">Restart SQuirreL.</span></span> <span data-ttu-id="26a2b-201">При подключении tooHive на HDInsight больше не возникает ошибка Hello.</span><span class="sxs-lookup"><span data-stu-id="26a2b-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26a2b-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26a2b-202">Next steps</span></span>

<span data-ttu-id="26a2b-203">Теперь, когда вы узнали, как toouse toowork JDBC с Hive hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26a2b-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="26a2b-204">Отправка данных tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="26a2b-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="26a2b-205">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="26a2b-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="26a2b-206">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="26a2b-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="26a2b-207">Использование заданий MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="26a2b-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
