---
title: "кластеры HDInsight, присоединенных к домену aaaManage - Azure | Документы Microsoft"
description: "Узнайте, как toomanage HDInsight, присоединенных к домену кластеров"
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
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Управление присоединенными к домену кластерами HDInsight (предварительная версия)
Узнайте hello пользователей и ролей hello в HDInsight, присоединенных к домену, и как toomanage HDInsight, присоединенных к домену кластеры.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Пользователи в присоединенном к домену кластере HDInsight.
Кластер HDInsight, не присоединенных к домену имеет две учетные записи пользователя, которые создаются во время создания кластера hello.

* **Администратор Ambari**: эта учетная запись называется также *Пользователь Hadoop* или *Пользователь HTTP*. Эту учетную запись можно использовать toolog на tooAmbari адресу https://&lt;имя_кластера >. azurehdinsight.net. Он также могут быть используется toorun запросы на Ambari представления, выполнять задания через внешние средства (т. е. PowerShell, Templeton, Visual Studio) и проверять подлинность с драйвером Hive ODBC hello и средств бизнес-Аналитики (т. е. Excel, PowerBI или Tableau).
* **Пользователь SSH**: эта учетная запись позволяет создать SSH-подключение и выполнять команды sudo. Она имеет привилегии корневой toohello виртуальных машин Linux.

Кластер HDInsight, присоединенных к домену имеет три новых пользователей в пользователя администратора и SSH tooAmbari сложения.

* **Круг admin**: Эта учетная запись является учетной записью администратора локальной круг Apache hello. Она не является пользователем домена Active Directory. Этой учетной записи можно использовать toosetup политики и после выполнения других пользователей "Администраторы" или полномочные администраторы (так, что эти пользователи могут управлять политиками). По умолчанию является имя пользователя hello *администратора* и Здравствуйте hello пароль, так же, как hello Ambari пароль администратора. можно обновить пароль Hello в страницы параметров hello в круг.
* **Пользователь домена администратора кластера**: Эта учетная запись является пользователем домена active directory, назначенный в качестве Здравствуйте, администратор кластера Hadoop, включая Ambari и круг. Учетные данные этого пользователя нужно предоставить во время создания кластера. Этот пользователь имеет hello следующие права:

  * Домену машины toohello и поместите их в пределах hello Подразделение, которое указывается во время создания кластера.
  * Создайте субъекты-службы в пределах hello Подразделение, которое указывается во время создания кластера.
  * Создание обратных записей DNS.

    Примечание hello других пользователей AD есть эти права.

    Существуют некоторые конечные точки в пределах кластера hello (например, Templeton) которых не управляется круг и поэтому не являются безопасными. Эти конечные точки блокированы для всех пользователей, кроме hello кластера администратор домена.
* **Обычный**: во время создания кластера можно указать несколько групп Active Directory. Hello пользователей в этих группах будет синхронизирован tooRanger и Ambari. Эти пользователи пользователей домена и будет иметь tooonly круг с управлением конечные точки доступа (например, Hiveserver2). Все hello RBAC политик и аудита будет применимо toothese пользователей.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Роли в присоединенном к домену кластере HDInsight
HDInsight, присоединенных к домену имеют hello следующих ролей:

* администратор кластера;
* оператор кластера;
* администратора служб;
* оператор службы;
* пользователь кластера.

**toosee hello разрешений этих ролей**

1. Откройте пользовательский Интерфейс управления Ambari hello.  В разделе [Привет открыть пользовательского интерфейса управления Ambari](#open-the-ambari-management-ui).
2. Hello в левом меню, щелкните **ролей**.
3. Нажмите кнопку hello синий вопросительный знак toosee hello разрешения:

    ![Роли в присоединенном к домену кластере HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Откройте пользовательский Интерфейс управления Ambari hello
1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Откройте колонку для кластера HDInsight. См. раздел [Отображение кластеров](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Нажмите кнопку **мониторинга** в верхнем меню hello tooopen Ambari.
4. Войдите в систему tooAmbari, используя имя пользователя домена администратора кластера hello и пароль.
5. Нажмите кнопку hello **администратора** раскрывающееся меню в правом верхнем углу приветствия и нажмите кнопку **управления Ambari**.

    ![Управление Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Hello пользовательского интерфейса выглядит следующим образом.

    ![Интерфейс управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Список пользователей домена hello, синхронизированные из Active Directory
1. Откройте пользовательский Интерфейс управления Ambari hello.  В разделе [Привет открыть пользовательского интерфейса управления Ambari](#open-the-ambari-management-ui).
2. Hello в левом меню, щелкните **пользователей**. Вы увидите все пользователи hello, синхронизированные с кластером HDInsight toohello Active Directory.

    ![Список пользователей в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Список групп домена hello, синхронизированные из Active Directory
1. Откройте пользовательский Интерфейс управления Ambari hello.  В разделе [Привет открыть пользовательского интерфейса управления Ambari](#open-the-ambari-management-ui).
2. Hello в левом меню, щелкните **группы**. Вы увидите все группы hello, синхронизированные с кластером HDInsight toohello Active Directory.

    ![Список групп в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Настройка разрешений для представлений Hive
1. Откройте пользовательский Интерфейс управления Ambari hello.  В разделе [Привет открыть пользовательского интерфейса управления Ambari](#open-the-ambari-management-ui).
2. Hello в левом меню, щелкните **представления**.
3. Нажмите кнопку **HIVE** tooshow hello сведения.

    ![Представления Hive в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Нажмите кнопку hello **Hive представление** связать tooconfigure Hive представления.
5. Прокрутите вниз toohello **разрешений** раздела.

    ![Настройка разрешений для представлений Hive в интерфейсе управления Ambari для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Нажмите кнопку **добавить пользователя** или **добавить группу**, а затем укажите hello пользователей или групп, которые можно использовать представления Hive.

## <a name="configure-users-for-hello-roles"></a>Настройка пользователей для роли hello
 toosee список ролей и их разрешениях см. в разделе [кластеров HDInsight ролей из присоединенных к домену](#roles-of-domain---joined-hdinsight-clusters).

1. Откройте пользовательский Интерфейс управления Ambari hello.  В разделе [Привет открыть пользовательского интерфейса управления Ambari](#open-the-ambari-management-ui).
2. Hello в левом меню, щелкните **ролей**.
3. Нажмите кнопку **добавить пользователя** или **добавить группу** ролей toodifferent tooassign пользователей и групп.

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о настройке присоединенного к домену кластера HDInsight см. в [этой статье](hdinsight-domain-joined-configure.md).
* Сведения о настройке политик Hive и выполнении запросов Hive для присоединенного к домену кластера HDInsight см. [здесь](hdinsight-domain-joined-run-hive.md).
* Сведения о выполнении запросов Hive с помощью SSH в присоединенных к домену кластерах HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
