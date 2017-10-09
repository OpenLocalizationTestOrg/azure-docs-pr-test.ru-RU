---
title: "aaaUse Финиксе Apache и белка с ОС Windows Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Финиксе Apache в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Использование Apache Phoenix и SQuirreL с кластерами HBase под управлением Windows в HDinsight
Узнайте, как toouse [Финиксе Apache](http://phoenix.apache.org/) в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight. Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше). Hello Финиксе грамматики. в разделе [грамматики Финиксе](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Hello Финиксе сведения о версии в HDInsight, в разделе [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Hello шагов в работают только этот документ для кластеров HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения об использовании Phoenix в HDInsight под управлением Linux см. в статье [Использование Apache Phoenix с кластерами HBase под управлением Linux в HDinsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Использование SQLLine
[SQLLine](http://sqlline.sourceforge.net/) является tooexecute служебной программы командной строки SQL.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем использовать SQLLine, необходимо иметь следующие hello.

* **Кластер HBase в HDInsight.** Сведения о подготовке кластера HBase см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started].
* **Подключите кластер HBase toohello посредством протокола удаленного рабочего стола hello**. Инструкции см. в разделе [кластеров управление Hadoop в HDInsight с помощью классического портала Azure hello][hdinsight-manage-portal].

**toofind hello имени узла**

1. Откройте **командной строки Hadoop** с рабочего стола hello.
2. Выполните следующие команды tooget hello DNS-суффикс hello.

        ipconfig

    Запишите **DNS-суффикс, зависящий от подключения**. Например, *myhbasecluster.f5.internal.cloudapp.net*. При подключении tooan HBase кластера, необходимо будет tooone tooconnect из Zookeepers hello, используя полное доменное имя. Каждый кластер HDInsight содержит 3 Zookeeper. Их имена — *zookeeper0*, *zookeeper1* и *zookeeper2*. Hello полное доменное имя будет примерно *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Откройте **командной строки Hadoop** с рабочего стола hello.
2. Выполните следующие команды tooopen SQLLine hello.

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    Hello команды, используемые в образце hello:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Дополнительные сведения см. в разделе [SQLLine manual](http://sqlline.sourceforge.net/#manual) (Руководство по SQLLine) и [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).

## <a name="use-squirrel"></a>Использование SQuirreL
[Клиент SQL белка](http://squirrel-sql.sourceforge.net/) — это графическая программа Java, позволяют tooview структура hello JDBC совместимую базу данных, Обзор hello данные в таблицах, команд SQL и т. д. Это может быть tooApache используется tooconnect Финиксе на HDInsight.

В этом разделе показано, как tooinstall и настройте белка на рабочей станции tooconnect tooan HBase кластера в HDInsight через VPN.

### <a name="prerequisites"></a>Предварительные требования
Перед выполнением процедуры hello, необходимо иметь следующие hello.

* Кластер HBase развернуть tooan виртуальную сеть Azure с виртуальной машины DNS.  Инструкции см. в статье [Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet].

* Получение hello HBase кластера кластера DNS подключения-суффикс. tooget его RDP в кластер hello, а затем выполните команду IPConfig.  DNS-суффикс Hello похожа на:

        myhbase.b7.internal.cloudapp.net
* Скачать и установить [Microsoft Visual Studio Express для Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) на рабочую станцию. Необходимо будет makecert из пакета toocreate hello свой сертификат.  
* Загрузить и установить среду [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) на рабочую станцию.  Для SQL-клиента SQuirreL версии 3.0 и выше требуется JRE версии 1.6 или выше.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Настройка toohello подключение точка-сеть VPN виртуальной сети Azure
Настройка VPN-подключения «точка-сайт» предусматривает 3 шага:

1. [Настройка виртуальной сети и шлюза динамической маршрутизации](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Создание сертификатов](#Create-your-certificates)
3. [Настройка VPN-клиента](#Configure-your-VPN-client)

В разделе [Настройка tooan подключение точка-сеть VPN виртуальной сети Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) для получения дополнительной информации.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Настройка виртуальной сети и шлюза динамической маршрутизации
Обеспечить вы подготовили кластер HBase в виртуальной сети Azure (см. предварительные требования hello для этого раздела). Hello следующим шагом является tooconfigure подключение точка сеть.

**подключение точка сеть tooconfigure hello**

1. Войдите в toohello [классический портал Azure][azure-portal].
2. В левой части экрана приветствия щелкните **СЕТЕЙ**.
3. Нажмите кнопку создания виртуальной сети hello (см. [HBase подготовки кластеров в виртуальной сети Azure][hdinsight-hbase-provision-vnet]).
4. Нажмите кнопку **Настройка** сверху hello.
5. В hello **подключение точка сеть** выберите **Настройка подключения «точка сеть»**.
6. Настройка **НАЧАЛЬНЫЙ IP-адрес** и **CIDR** адрес toospecify hello IP-адресов из которого клиенты VPN будут получать IP-адрес при подключении. Hello диапазон не пересекается с другими hello диапазонами, выделенными в локальной сети и hello виртуальной сети Azure, вы будете подключаться. Например, если выбран диапазон 10.0.0.0/20 для виртуальной сети, для пространства клиентских адресов можно выбрать 10.1.0.0/24. Если вы выбрали 10.0.0.0/20 для hello виртуальной сети, можно выбрать 10.1.0.0/24 hello клиента адресного пространства. В разделе hello [точка-сеть] [ vnet-point-to-site-connectivity] более подробную информацию.
7. В разделе пространства адресов виртуальной сети hello, нажмите кнопку **добавить подсеть шлюза**.
8. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.
9. Нажмите кнопку **Да** tooconfirm hello изменений. Дождитесь завершения внесения изменения перед выполнением следующей процедуры toohello hello hello системой.

**toocreate шлюз динамической маршрутизации**

1. Hello классический портал Azure, щелкните **МОНИТОРИНГА** из hello вверху страницы приветствия.
2. Нажмите кнопку **создать ШЛЮЗ** из hello внизу страницы приветствия.
3. Нажмите кнопку **Да** tooconfirm. Подождите, пока создается hello шлюза.
4. Нажмите кнопку **МОНИТОРИНГА** сверху hello.  Вы увидите графическую диаграмму hello виртуальной сети.

    ![Схема виртуальной сети Azure «точка-сайт»][img-vnet-diagram]

    Hello показан 0 клиентских подключений. После внесения toohello подключения виртуальной сети, число hello будет обновленные tooone.

#### <a name="create-your-certificates"></a>Создание сертификатов
Одним из способов toocreate — сертификат X.509 с помощью hello средство создания сертификатов (makecert.exe), входящая в состав [Microsoft Visual Studio Express для Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate самозаверяющий корневой сертификат**

1. На рабочей станции откройте окно командной строки.
2. Перейдите в папку средств Visual Studio toohello.
3. следующую команду в следующем примере hello Hello создать и установить корневой сертификат в хранилище личных сертификатов hello на рабочей станции и также создать соответствующий CER-файл, который позднее будет отправлен toohello классический портал Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Изменение каталога toohello нужного hello, расположенных в, где требуется toouse для hello сертификата имя hello HBaseVnetVPNRootCertificate toobe файл .cer.

    Не закрывайте окно командной строки hello.  Он понадобится в следующей процедуре hello.

   > [!NOTE]
   > Поскольку был создан корневой сертификат, из которого будут создаваться сертификаты клиента, можно tooexport этот сертификат и его закрытый ключ и сохраните его в безопасном месте tooa, откуда его можно восстановить.
   >
   >

**toocreate сертификат клиента**

* Из hello же командную строку (он имеет toobe на hello же компьютере, где была создана hello корневой сертификат. Hello сертификат клиента должен быть создан из hello корневого сертификата), выполнения hello следующую команду:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate — имя сертификата корневого hello.  Он имеет имя toomatch hello корневого сертификата.  

    Hello корневой сертификат и сертификат клиента hello хранятся в хранилище личных сертификатов на компьютере. Используйте certmgr.msc tooverify.

    ![Схема виртуальной сети Azure "точка — сеть"][img-certificate]

    Сертификат клиента должны устанавливаться на каждом компьютере, что требуется tooconnect toohello виртуальной сети. Рекомендуется создавать уникальные клиентские сертификаты для каждого компьютера, которые должны tooconnect toohello виртуальной сети. tooexport hello клиентских сертификатов, используйте certmgr.msc.

**tooupload hello корневой сертификат toohello классический портал Azure**

1. Hello классический портал Azure, щелкните **сети** hello левой части экрана.
2. Щелкните hello виртуальной сети, где развертывается кластер HBase.
3. Нажмите кнопку **СЕРТИФИКАТЫ** сверху hello.
4. Нажмите кнопку **отправить** из hello вниз и укажите файл корневого сертификата hello, созданную в процедуре hello перед последней. Подождите, пока сертификат hello импортированы.
5. Нажмите кнопку **МОНИТОРИНГА** hello верхней части страницы.  Hello виртуального диаграмма показывает состояние hello.

#### <a name="configure-your-vpn-client"></a>Настройка VPN-клиента
**toodownload и установите пакет клиента VPN hello**

1. На странице панели МОНИТОРИНГА hello hello виртуальной сети, в разделе "быстрый обзор" hello щелкните **загрузки hello пакет VPN-клиента для 64-разрядных** или **загрузки hello пакет клиента VPN 32-разрядных** на основе вашего версия операционной системы рабочей станции.
2. Нажмите кнопку **запуска** tooinstall hello пакета.
3. В строке приветствия безопасности, нажмите кнопку **Подробнее**и нажмите кнопку **выполнения изменение**.
4. Нажмите кнопку **Да** дважды.

**tooconnect tooVPN**

1. На рабочем столе hello рабочей станции щелкните значок сети hello hello панели задач. Должно отобразиться VPN-подключения с именем вашей виртуальной сети.
2. Щелкните имя подключения VPN hello.
3. Щелкните **Подключить**.

**hello tootest подключение VPN, разрешения имен при домена**

* Hello рабочей станции, откройте командную строку и ping один hello следующие имена приведенные hello HBase кластера DNS-суффикс — myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Установка и настройка SQuirreL на рабочей станции
**tooinstall белка**

1. Загрузите hello клиента белка SQL jar-файл из [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Открытие и запуск hello jar-файл. Он требует hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Нажмите кнопку **Далее** дважды.
4. Укажите путь к которому у вас есть hello разрешение на запись и нажмите кнопку **Далее**.

  > [!NOTE]
  > устанавливается в папку по умолчанию Hello в папке C:\Program Files\squirrel-sql-3.6 hello.  Путь toothis toowrite заказа установщик hello должны быть предоставлены права администратора hello. Откройте командную строку от имени администратора, перейдите в папку bin в tooJava и затем запустите:
  >
  >     Java.exe-jar [hello путь hello белка jar-файл]
5. Нажмите кнопку **ОК** tooconfirm Создание hello целевой каталог.
6. по умолчанию Hello — tooinstall hello базы и стандартных пакетов.  Щелкните **Далее**.
7. Нажмите кнопку **Далее** дважды, а затем нажмите **Готово**.

**драйвер Финиксе tooinstall hello**

Hello Финиксе драйвер jar-файл находится на кластер HBase hello. путь Hello — примерно следующее toohello, основанных на версиях hello.

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Требуется toocopy его tooyour рабочей станции под hello [папка установки белка] / lib пути.  Hello простым способом является tooRDP в hello кластера, а затем используйте файл копирования и вставки (CTRL + C и CTRL + V) toocopy его tooyour рабочей станции.

**tooadd tooSQuirreL драйвер Phoenix**

1. Откройте SQL-клиент SQuirreL на рабочей станции.
2. Нажмите кнопку hello **драйвер** вкладке слева hello.
3. Из hello **драйверы** меню, нажмите кнопку **новый драйвер**.
4. Введите hello следующую информацию:

   * **Имя**: Phoenix
   * **Пример URL-адреса**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Имя класса**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Пользователь все нижнего регистра в hello пример URL-адреса. Можно использовать весь набор zookeeper в случае, если один из них не работает.  имена узлов Hello: zookeeper0, zookeeper1 и zookeeper2.
     >
     >

     ![Драйвер HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. Нажмите кнопку **ОК**.

**toocreate кластер HBase toohello псевдоним**

1. Щелкните hello белка, **псевдонимы** вкладке слева hello.
2. Из hello **псевдонимы** меню, нажмите кнопку **новый псевдоним**.
3. Введите hello следующую информацию:

   * **Имя**: hello имя кластера HBase hello или любое имя, вы предпочитаете.
   * **Драйвер**: Phoenix.  Это должно соответствовать имени драйвера hello, созданный в последней процедуры hello.
   * **URL-адрес**: hello, URL-адрес копируется из конфигурации драйвера. Убедитесь, что toouser все строчные.
   * **Имя пользователя**: может быть любой текстовой строкой.  Поскольку здесь использовать VPN-подключение имя пользователя hello вообще не используется.
   * **Пароль**: может быть любой текстовой строкой.

     ![Драйвер HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. Нажмите **Проверить**.
5. Щелкните **Подключить**. Когда он создает соединение hello белка выглядит следующим образом.

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun теста**

1. Нажмите кнопку hello **SQL** вкладки справа Далее toohello **объектов** вкладки.
2. Скопируйте и вставьте следующий код hello:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Нажмите кнопку выполнения hello.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Перейдите назад toohello **объектов** вкладки.
5. Разверните имя псевдонима hello, а затем разверните **таблицы**.  Вы увидите новую таблицу hello, перечисленных в разделе.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как toouse Финиксе Apache в HDInsight.  toolearn более, см.

* [Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.
* [Подготовка кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]: С интеграцией виртуальной сети кластеров HBase может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую.
* [Настройка репликации HBase HDInsight](hdinsight-hbase-replication.md): Узнайте, как tooconfigure HBase репликации между двумя центрами обработки данных Azure.
* [Анализ мнений Twitter с HBase в HDInsight][hbase-twitter-sentiment]: Узнайте, как toodo в режиме реального времени [анализ мнений](http://en.wikipedia.org/wiki/Sentiment_analysis) больших данных с помощью кластера Hadoop в HDInsight HBase.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
