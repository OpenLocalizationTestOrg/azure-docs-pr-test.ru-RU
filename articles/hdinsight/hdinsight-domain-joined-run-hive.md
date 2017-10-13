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
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Настройка политик Hive в присоединенном к домену кластере HDInsight (предварительная версия)
Узнайте, как настроить политики Apache Ranger для Hive. В этой статье вы создадите две политики Ranger, чтобы ограничить доступ к таблице hivesampletable. Таблица hivesampletable поставляется с кластерами HDInsight. После настройки политик подключитесь к таблицам Hive в HDInsight с помощью Excel и драйвера ODBC.

## <a name="prerequisites"></a>Предварительные требования
* Присоединенный к домену кластер HDInsight. См. статью [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Настройка присоединенных к домену кластеров HDInsight).
* Рабочая станция с Office 2016, Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.

## <a name="connect-to-apache-ranger-admin-ui"></a>Подключение к пользовательскому интерфейсу администратора Apache Ranger
**Подключение к пользовательскому интерфейсу администратора Ranger**

1. В браузере подключитесь к пользовательскому интерфейсу администратора Ranger по URL-адресу https://&lt;имя_кластера >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger использует учетные данные, отличающиеся от учетных данных кластера Hadoop. Чтобы браузеры не использовали кэшированные учетные данные Hadoop, подключитесь к пользовательскому интерфейсу администратора Ranger в новом окне браузера в режиме InPrivate.
   >
   >
2. Войдите, используя имя пользователя и пароль домена администратора кластера.

    ![Домашняя страница Ranger для подключенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    В настоящее время Ranger работает только с Yarn и Hive.

## <a name="create-domain-users"></a>Создание пользователей домена
При работе со статьей [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Настройка присоединенных к домену кластеров HDInsight) вы создали два пользователя: hiveruser1 и hiveuser2. В этом руководстве вы будете использовать эти две учетные записи.

## <a name="create-ranger-policies"></a>Создание политик Ranger
В этом разделе вы создадите две политики Ranger для доступа к таблице hivesampletable. Вам нужно будет предоставить разрешение select для разных наборов столбцов. Оба пользователя созданы при выполнении указаний статьи о [настройке присоединенных к домену кластеров HDInsight](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).  В следующем разделе вы протестируете две политики в Excel.

**Создание политик Ranger**

1. Откройте пользовательский интерфейс администратора Ranger. См. раздел [Подключение к пользовательскому интерфейсу администратора Apache Ranger](#connect-to-apache-ranager-admin-ui).
2. Щелкните **&lt;имя_кластера>_hive** в разделе **Hive**. Отобразятся две предварительно настроенные политики.
3. Щелкните **Добавить новую политику**, а затем введите следующие значения.

   * Имя политики: read-hivesampletable-all.
   * База данных Hive: по умолчанию.
   * Таблица: hivesampletable.
   * Столбец Hive: *.
   * Пользователь: hiveuser1.
   * Разрешения: select.

     ![Настойка политики Hive Ranger для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Если пользователь домена не указан в поле "Выберите пользователя", подождите несколько минут для синхронизации Ranger с AAD.
     >
     >
4. Щелкните **Добавить**, чтобы сохранить политику.
5. Повторите последние два шага, чтобы создать еще одну политику со следующими свойствами.

   * Имя политики: read-hivesampletable-devicemake.
   * База данных Hive: по умолчанию.
   * Таблица: hivesampletable.
   * Столбец Hive: clientid, devicemake.
   * Пользователь: hiveuser2.
   * Разрешения: select.

## <a name="create-hive-odbc-data-source"></a>Создание источника данных Hive ODBC
Инструкции см. в разделе [Создание источника данных Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).  

    Свойство|Description (Описание)
    ---|---
    Имя источника данных|Присвойте имя источнику данных
    Узел|Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net. Например, myHDICluster.azurehdinsight.net
    Порт|Используйте <strong>443</strong>. (Этот порт был изменен с 563 на 443.)
    База данных|Используйте <strong>значение по умолчанию</strong>.
    Тип сервера Hive|Выберите <strong>Hive Server 2</strong>.
    Механизм|Выберите <strong>Служба Azure HDInsight</strong>.
    Путь HTTP|Оставьте пустым.
    Имя пользователя|Укажите hiveuser1@contoso158.onmicrosoft.com. Обновите имя домена, если оно отличается.
    Пароль|Введите пароль для hiveuser1.
    </table>

Щелкните **Проверка** перед сохранением источника данных.

## <a name="import-data-into-excel-from-hdinsight"></a>Импорт данных в Excel из службы HDInsight
В последнем разделе вы настроили две политики.  У hiveuser1 есть разрешение select на все столбцы, а у hiveuser2 — на два столбца. В этом разделе вы выполните олицетворение двух пользователей для импорта данных в Excel.

1. Откройте новую или существующую рабочую книгу в Excel.
2. На вкладке **Данные** щелкните **From Other Data Sources** (Из других источников данных), а затем выберите **Из мастера подключения к данным**, чтобы запустить **мастер подключения к данным**.

    ![Откройте мастер подключения к данным][img-hdi-simbahiveodbc.excel.dataconnection]
3. Выберите **ODBC DSN** в качестве источника данных и нажмите кнопку **Далее**.
4. В источниках данных ODBC выберите имя источника данных, созданного на предыдущем шаге, и нажмите кнопку **Далее**.
5. Повторно введите в мастере пароль для кластера и нажмите кнопку **ОК**. Подождите открытие диалогового окна **Выбор базы данных и таблицы** . Это может занять несколько секунд.
6. Выберите **hivesampletable**, а затем нажмите кнопку **Далее**.
7. Нажмите кнопку **Готово**
8. В диалоговом окне **Импорт данных** можно изменить или указать запрос. Для этого щелкните **Свойства**. Это может занять несколько секунд.
9. Выберите вкладку **Определение**. Текст команды:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   В соответствии с заданными политиками Ranger у hiveuser1 есть разрешение select на все столбцы.  Поэтому этот запрос срабатывает с учетными данными hiveuser1, но не с учетными данными hiveuser2.

   ![Свойства подключения][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Нажмите **OK** , чтобы закрыть диалоговое окно "Свойства подключения".
11. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Импорт данных**.  
12. Введите пароль для hiveuser1 еще раз и нажмите кнопку **ОК**. Пройдет несколько секунд, прежде чем данные будут импортированы в Excel. После этого отобразятся 11 столбцов с данными.

Проверка второй политики (read-hivesampletable-devicemake), созданной в предыдущем разделе

1. Добавьте новый лист в Excel.
2. Выполните последнюю процедуру для импорта данных.  Единственное изменение заключается в том, что нужно использовать учетные данные hiveuser2, а не hiveuser1. При этом произойдет сбой, так как у hiveuser2 есть разрешение только на просмотр двух столбцов. Появится следующая ошибка:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Выполните ту же процедуру для импорта данных. На этот раз используйте учетные данные hiveuser2 и измените инструкцию FROM в предложении SELECT:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    на:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    После этого импортируются два столбца с данными.

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).
* Сведения об управлении присоединенными к домену кластерами HDInsight см. в [этой статье](hdinsight-domain-joined-manage.md).
* Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Сведения о подключении к Hive с помощью Hive JDBC см. в статье [Подключение к Hive в Azure HDInsight с помощью драйвера Hive JDBC](hdinsight-connect-hive-jdbc-driver.md).
* Сведения о подключении Excel к Hadoop с помощью Hive ODBC см. в статье [Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).
* Сведения о подключении Excel к Hadoop с помощью Power Query см. в [этой статье](hdinsight-connect-excel-power-query.md).
