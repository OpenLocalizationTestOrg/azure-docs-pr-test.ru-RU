---
title: "Установка RStudio с R Server в кластере HDInsight — Azure | Документы Майкрософт"
description: "Сведения об установке RStudio с R Server в кластере HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Установка RStudio с R Server в HDInsight

В этой статье описывается, как установить бесплатную версию [RStudio Server](https://www.rstudio.com/products/rstudio-server/) для сообщества на граничном узле кластера с помощью пользовательского скрипта. RStudio Server предоставляет интегрированную среду разработки (IDE) на основе браузера, предназначенную для удаленных клиентов и широко используемую в Linux. Для языка R в настоящее время доступно множество интегрированных сред разработки, включая следующие:

- [Инструменты R для Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) от корпорации Майкрософт 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- [StatET](http://www.walware.de/goto/statet) на основе Eclipse от компании Walware

Преимуществом установки RStudio Server на граничном узле кластера HDInsight является получение доступа ко всем функциональным возможностям IDE для разработки и выполнения скриптов R с использованием R Server в кластере. Такая конфигурация может обеспечивать значительно более высокую производительность по сравнению с консолью R.

> [!NOTE]
> Процедура, описанная в этой статье, подходит только в том случае, если вы не выбрали установку выпуска RStudio Server для сообщества при подготовке кластера. Если вы добавили его во время подготовки, то для доступа к нему можете щелкнуть плитку **Панели мониторинга R Server** в записи портала Azure для своего кластера, а затем щелкнуть плитку **R Studio Server**. 

Если вы хотите использовать коммерческую версию RStudio Server Pro, необходимо выполнить инструкции по установке из [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Если вы используете кластер, для которого среда R была установлена с помощью [действия по установке скрипта R](hdinsight-hadoop-r-scripts-linux.md), приведенные в этом документе инструкции не будут работать правильно, так как для них требуется сервер R Server в кластере HDInsight.
>
> 

## <a name="prerequisites"></a>Предварительные требования

* Кластер Azure HDInsight, на котором установлен R Server. Инструкции см. в статье [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md).
* Клиент SSH. В дистрибутивах Linux и Unix и Macintosh OS X команда `ssh` входит в состав операционной системы. Для Windows мы рекомендуем [Cygwin](http://www.redhat.com/services/custom/cygwin/) (с [параметром OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU)) или [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a>Установка RStudio в кластере с помощью пользовательского скрипта

Для этого выполните следующие действия:

1. Определите граничный узел кластера. Ниже указано соглашение об именовании головных и граничных узлов для кластера HDInsight с R Server.
   * Головной узел — `CLUSTERNAME-ssh.azurehdinsight.net`
   * Граничный узел — `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. Подключитесь к граничному узлу кластера по протоколу SSH, используя схему именования, приведенную в шаге 1. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. После подключения используйте учетные данные привилегированного пользователя в кластере. В сеансе SSH используйте следующую команду:

        sudo su -

4. Скачайте пользовательский скрипт для установки RStudio. Используйте следующую команду:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Измените разрешения для файла пользовательского скрипта и запустите скрипт. Используйте следующие команды:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Если при создании кластера HDInsight с R Server использовался пароль SSH, можно пропустить этот шаг и перейти к следующему. Если вместо него для создания кластера использовался ключ SSH, необходимо задать пароль для пользователя SSH. Этот пароль понадобится при подключении к RStudio. Выполните следующие команды:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. При появлении запроса на ввод **текущего пароля Kerberos** нажмите клавишу **ВВОД**.  Обратите внимание, что `USERNAME` необходимо заменить именем пользователя SSH для кластера HDInsight. В случае успешной установки пароля появится следующее сообщение:

        passwd: password updated successfully

    Выйдите из сеанса SSH.

8. Создайте туннель SSH для кластера, сопоставив `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` в кластере HDInsight с клиентским компьютером. Туннель SSH следует создать перед открытием нового сеанса браузера.

   * В клиенте Linux или Windows с [Cygwin](http://www.redhat.com/services/custom/cygwin/) откройте сеанс терминала и введите следующую команду:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Замените **USERNAME** именем пользователя SSH для кластера HDInsight, а **CLUSTERNAME** — именем кластера HDInsight.
       Можно также использовать ключ SSH, а не пароль, добавив `-i id_rsa_key`.        
   * Если вы используете клиент Windows и PuTTY, выполните следующие действия:

     1. Откройте PuTTY и введите информацию о подключении.
     2. В разделе **Категории** в левой части диалогового окна последовательно разверните **Подключение**, **SSH** и выберите **Туннели**.
     3. Введите следующую информацию в форме **Параметры, управляющие перенаправлением портов SSH** :

        * **Порт источника** — порт на стороне клиента, трафик которого нужно перенаправлять. Например, **8787**.
        * **Назначение** — место назначения, которое следует сопоставить с локальным клиентским компьютером. Например, **localhost:8787**.

            ![Создание туннеля SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "создание туннеля SSH")

     4. Щелкните **Добавить**, чтобы добавить параметры, а затем щелкните **Открыть**, чтобы открыть подключение SSH.
     5. При появлении запроса войдите на сервер. При этом будет установлен сеанс SSH и включен туннель.

9. Откройте браузер и введите следующий URL-адрес с учетом порта, введенного для туннеля:

        http://localhost:8787/ 

10. Появится запрос на ввод имени пользователя и пароля SSH для подключения к кластеру. Если при создании кластера использовался ключ SSH, необходимо ввести пароль, созданный в шаге 5.

    ![Подключение к R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "создание туннеля SSH")

11. Чтобы проверить успешность установки RStudio, можно запустить тестовый скрипт, выполняющий задания MapReduce и Spark на языке R в кластере. Чтобы скачать тестовый скрипт для запуска в RStudio, вернитесь в консоль SSH и введите следующие команды:

    *    При создании кластера Hadoop на языке R используйте эту команду:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    При создании кластера Spark на языке R используйте эту команду:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. В RStudio появится скачанный тестовый скрипт. Дважды щелкните файл, чтобы открыть его, выделите содержимое файла и нажмите кнопку **Run** (Запустить). Результаты появятся в области **Console** (Консоль).

   ![Проверка установки](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "проверка установки")

Еще один вариант — ввести `source(testhdi.r)` или `source(testhdi_spark.r)` для выполнения скрипта.

## <a name="see-also"></a>Дополнительные материалы

* [Compute context options for R Server on HDInsight clusters (Параметры контекста вычислений для R Server в кластерах HDInsight)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-storage.md)

