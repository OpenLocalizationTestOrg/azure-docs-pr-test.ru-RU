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
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Настройка политик Hive в присоединенном к домену кластере HDInsight (предварительная версия)
Узнайте, как политики tooconfigure круг Apache Hive. В этой статье создайте hivesampletable toohello два круг политики toorestrict доступа. Hello hivesampletable поставляется с кластерами HDInsight. После настройки политики hello вы используете Excel и ODBC драйвера tooconnect tooHive таблиц в HDInsight.

## <a name="prerequisites"></a>Предварительные требования
* Присоединенный к домену кластер HDInsight. См. статью [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Настройка присоединенных к домену кластеров HDInsight).
* Рабочая станция с Office 2016, Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.

## <a name="connect-tooapache-ranger-admin-ui"></a>Подключение tooApache круг пользовательского интерфейса администратора
**tooconnect tooRanger пользовательского интерфейса администратора**

1. С помощью браузера подключитесь tooRanger пользовательского интерфейса администратора. Hello URL-адрес: https://&lt;Имя_кластера >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger использует учетные данные, отличающиеся от учетных данных кластера Hadoop. обозреватели tooprevent, кэшированные Hadoop, используя учетные данные используют новый toohello tooconnect окна браузера inprivate круг пользовательского интерфейса администратора.
   >
   >
2. Войдите, используя имя пользователя домена администратора кластера hello и пароль:

    ![Домашняя страница Ranger для подключенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    В настоящее время Ranger работает только с Yarn и Hive.

## <a name="create-domain-users"></a>Создание пользователей домена
При работе со статьей [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Настройка присоединенных к домену кластеров HDInsight) вы создали два пользователя: hiveruser1 и hiveuser2. В этом учебнике будет использовать учетная запись hello два пользователя.

## <a name="create-ranger-policies"></a>Создание политик Ranger
В этом разделе вы создадите две политики Ranger для доступа к таблице hivesampletable. Вам нужно будет предоставить разрешение select для разных наборов столбцов. Оба пользователя созданы при выполнении указаний статьи о [настройке присоединенных к домену кластеров HDInsight](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).  В следующем разделе hello тестировании hello две политики в Excel.

**toocreate круг политики**

1. Откройте пользовательский интерфейс администратора Ranger. В разделе [подключения tooApache пользовательского интерфейса администратора круг](#connect-to-apache-ranager-admin-ui).
2. Щелкните **&lt;имя_кластера>_hive** в разделе **Hive**. Отобразятся две предварительно настроенные политики.
3. Нажмите кнопку **добавить новую политику**, а затем введите hello следующие значения:

   * Имя политики: read-hivesampletable-all.
   * База данных Hive: по умолчанию.
   * Таблица: hivesampletable.
   * Столбец Hive: *.
   * Пользователь: hiveuser1.
   * Разрешения: select.

     ![Настойка политики Hive Ranger для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Если пользователь домена не заполняется в Выбор пользователя, подождите несколько секунд для toosync круг с AAD.
     >
     >
4. Нажмите кнопку **добавить** toosave hello политики.
5. Повторите toocreate последних двух этапов hello еще одну политику с hello следующие свойства:

   * Имя политики: read-hivesampletable-devicemake.
   * База данных Hive: по умолчанию.
   * Таблица: hivesampletable.
   * Столбец Hive: clientid, devicemake.
   * Пользователь: hiveuser2.
   * Разрешения: select.

## <a name="create-hive-odbc-data-source"></a>Создание источника данных Hive ODBC
Hello инструкции можно найти в [источника данных ODBC Hive создать](hdinsight-connect-excel-hive-odbc-driver.md).  

    Свойство|Description (Описание)
    ---|---
    Имя источника данных|Предоставьте имя источника данных tooyour
    Узел|Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net. Например, myHDICluster.azurehdinsight.net
    Порт|Используйте <strong>443</strong>. (Этот порт был изменен из 563 too443.)
    База данных|Используйте <strong>значение по умолчанию</strong>.
    Тип сервера Hive|Выберите <strong>Hive Server 2</strong>.
    Механизм|Выберите <strong>Служба Azure HDInsight</strong>.
    Путь HTTP|Оставьте пустым.
    Имя пользователя|Укажите hiveuser1@contoso158.onmicrosoft.com. Обновите hello доменное имя, если он отличается.
    Пароль|Пароль hiveuser1 hello.
    </table>

Убедитесь, что tooclick **тест** перед сохранением hello источника данных.

## <a name="import-data-into-excel-from-hdinsight"></a>Импорт данных в Excel из службы HDInsight
В последнем разделе hello вы настроили две политики.  hiveuser1 имеет разрешение select на все столбцы hello hello и hiveuser2 hello разрешение select на два столбца. В этом разделе олицетворять hello два пользователя tooimport данных в Excel.

1. Откройте новую или существующую рабочую книгу в Excel.
2. Из hello **данные** щелкните **из других источников данных**и нажмите кнопку **от мастера подключения к данным** toolaunch hello **мастераподключениякданным**.

    ![Откройте мастер подключения к данным][img-hdi-simbahiveodbc.excel.dataconnection]
3. Выберите **ODBC DSN** как hello источника данных, а затем щелкните **Далее**.
4. Из источников данных ODBC, имя, созданную в предыдущем шаге hello источника данных выберите hello и нажмите кнопку **Далее**.
5. Повторно введите пароль hello кластера hello в мастере приветствия и нажмите кнопку **ОК**. Дождитесь hello **Выбор базы данных и таблицы** tooopen диалогового окна. Это может занять несколько секунд.
6. Выберите **hivesampletable**, а затем нажмите кнопку **Далее**.
7. Нажмите кнопку **Готово**
8. В hello **импорта данных** диалоговое окно, можно изменить или указать запрос hello. Таким образом, щелкните toodo **свойства**. Это может занять несколько секунд.
9. Нажмите кнопку hello **определение** текст команды вкладку hello:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Политиками hello круг определенным вами hiveuser1 имеет разрешение select на все столбцы hello.  Поэтому этот запрос срабатывает с учетными данными hiveuser1, но не с учетными данными hiveuser2.

   ![Свойства подключения][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Нажмите кнопку **ОК** диалоговое окно свойств подключения tooclose hello.
11. Нажмите кнопку **ОК** tooclose hello **импорта данных** диалогового окна.  
12. Повторно введите пароль hello hiveuser1 и нажмите кнопку **ОК**. Он занимает несколько секунд перед импортированных tooExcel получает данные. После этого отобразятся 11 столбцов с данными.

Вторая политика hello tootest (чтения hivesampletable devicemake), созданный в разделе последнего hello

1. Добавьте новый лист в Excel.
2. Выполните hello последней процедуры tooimport hello данных.  Hello единственным изменением, которое будет производиться — toouse hiveuser2 учетные данные вместо hiveuser1 элемента. Это будет ошибкой, поскольку hiveuser2 имеет только два столбца toosee разрешение. Вы должны получить hello следующая ошибка:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Выполните hello же процедура tooimport данных. На этот раз используйте учетные данные hiveuser2 и также измените hello инструкции select из:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    на:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    После этого импортируются два столбца с данными.

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).
* Сведения об управлении присоединенными к домену кластерами HDInsight см. в [этой статье](hdinsight-domain-joined-manage.md).
* Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Подключение Hive с помощью Hive JDBC, в разделе [подключения tooHive на Azure HDInsight с помощью драйвера Hive JDBC hello](hdinsight-connect-hive-jdbc-driver.md)
* TooHadoop соединения Excel с использованием Hive ODBC, в разделе [tooHadoop Excel подключиться с hello диска Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)
* TooHadoop соединения Excel с помощью Power Query, в разделе [tooHadoop Excel подключиться с помощью Power Query](hdinsight-connect-excel-power-query.md)
