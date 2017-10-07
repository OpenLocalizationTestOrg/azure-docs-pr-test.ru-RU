---
title: "aaaInstall RStudio с сервером R в HDInsight - Azure | Документы Microsoft"
description: "Как tooinstall RStudio с сервером R в HDInsight."
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Установка RStudio с R Server в HDInsight

В этой статье описывается, как tooinstall hello сообщества (бесплатно) версия [RStudio сервера](https://www.rstudio.com/products/rstudio-server/) на hello граничного узла кластера с помощью пользовательского скрипта. RStudio Server предоставляет интегрированную среду разработки (IDE) на основе браузера, предназначенную для удаленных клиентов и широко используемую в Linux. Для языка R в настоящее время доступно множество интегрированных сред разработки, включая следующие:

- [Инструменты R для Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) от корпорации Майкрософт 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- [StatET](http://www.walware.de/goto/statet) на основе Eclipse от компании Walware

Hello преимущество установки RStudio сервера на приветствия граничного узла из кластера HDInsight — что она обеспечивает полной интегрированной СРЕДЫ разработки hello разработки и выполнения скриптов R с R Server на кластере hello. Эта конфигурация может быть значительно более производительны, чем использование по умолчанию hello R консоли.

> [!NOTE]
> Hello процедуру, описанную в данной статье применяется только в том случае, если вы не выбрали tooinstall RStudio Server community edition при подготовке кластера. При добавлении во время инициализации, затем tooaccess его щелкнуть hello **панели мониторинга сервера R** плитки в hello Azure портала запись для кластера, а затем в hello **R Studio Server** плитки. 

При желании toouse hello коммерчески лицензия Pro версии RStudio Server необходимо выполнить инструкции по установке hello из [RStudio сервера](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> При использовании кластера HDInsight, для которого R был установлен при помощи hello [действия сценария R установка](hdinsight-hadoop-r-scripts-linux.md), hello шагов в этом документе не будет работать правильно, как они требуют R Server в кластере HDInsight hello.
>
> 

## <a name="prerequisites"></a>Предварительные требования

* Кластер Azure HDInsight, на котором установлен R Server. Инструкции см. в статье [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md).
* Клиент SSH. Для дистрибутивах Linux и Unix или Macintosh OS X, hello `ssh` команда входит в состав операционной системы hello. Для Windows, мы рекомендуем [Cygwin](http://www.redhat.com/services/custom/cygwin/) с hello [параметр OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), или [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Установка RStudio на кластере hello, с помощью пользовательского сценария

Ниже приведены шаги hello.

1. Определите hello граничного узла кластера hello. Для кластера HDInsight с сервером R ниже приведен hello соглашение об именовании для головного узла и граничного узла.
   * Головной узел — `CLUSTERNAME-ssh.azurehdinsight.net`
   * Граничный узел — `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH в hello граничного узла кластера hello, используя шаблон именования hello, указанных на шаге 1. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Если вы подключены, становятся привилегированного пользователя на кластере hello. В сеансе SSH hello используйте hello следующую команду:

        sudo su -

4. Загрузите пользовательский сценарий hello tooinstall RStudio. Hello используйте следующую команду:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Изменить разрешения hello hello пользовательский файл скрипта и запустите сценарий hello. Используйте hello, следующие команды:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. При использовании пароля SSH во время создания кластера HDInsight с сервером R, можно пропустить этот шаг и продолжить toohello Далее. При использовании ключа SSH вместо toocreate hello кластера, необходимо задать пароль для пользователя SSH. Этот пароль необходимо при подключении tooRStudio. Выполните следующие команды hello.

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. При появлении запроса на ввод **текущего пароля Kerberos** нажмите клавишу **ВВОД**.  Обратите внимание, что `USERNAME` необходимо заменить именем пользователя SSH для кластера HDInsight. Если пароль успешно установлен, вы увидите hello следующие сообщения:

        passwd: password updated successfully

    Завершите сеанс SSH hello.

8. Создание кластера toohello туннель SSH, сопоставляя `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello HDInsight кластера toohello клиентского компьютера. Туннель SSH следует создать перед открытием нового сеанса браузера.

   * На стороне клиента Linux или клиента Windows с [Cygwin](http://www.redhat.com/services/custom/cygwin/), откройте сеанс терминала и использовать hello следующую команду:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Замените **USERNAME** пользователем SSH для кластера HDInsight и замените **CLUSTERNAME** с hello имя кластера HDInsight.
       Можно также использовать ключ SSH, а не пароль, добавив `-i id_rsa_key`.        
   * Если вы используете клиент Windows и PuTTY, выполните следующие действия:

     1. Откройте PuTTY и введите информацию о подключении.
     2. В hello **категории** toohello раздел левой части диалогового окна hello, разверните **подключения**, разверните **SSH**и выберите **туннели**.
     3. Укажите следующую информацию на hello hello **перенаправление портов параметры, управляющие SSH** формы:

        * **Порт источника** -порт на приветствия клиента обратиться в tooforward hello. Например, **8787**.
        * **Назначение** - hello назначения, который должен быть сопоставлен toohello локальный клиентский компьютер. Например, **localhost:8787**.

            ![Создание туннеля SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "создание туннеля SSH")

     4. Нажмите кнопку **добавить** tooadd hello параметры и нажмите кнопку **откройте** tooopen SSH-подключения.
     5. При появлении запроса выполните вход tooestablish сервера toohello туннель SSH сеанса и включить hello.

9. Откройте веб-браузер и введите URL-адреса учетом порта hello, введенное для hello туннеля hello:

        http://localhost:8787/ 

10. Все запрашиваемые tooenter hello SSH имя пользователя и пароль tooconnect toohello кластера. Если вы использовали SSH-ключ при создании кластера hello, необходимо ввести пароль hello, созданный на шаге 5.

    ![Подключение tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "создать туннель SSH")

11. tootest ли hello RStudio установки выполнена успешно, можно запустить тестовый сценарий, который выполняется на основе R задания MapReduce и Spark на кластере hello. toorun toodownload hello тестового скрипта в RStudio, вернитесь к предыдущему окну консоли SSH toohello и введите hello, следующие команды:

    *    При создании кластера Hadoop на языке R используйте эту команду:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    При создании кластера Spark на языке R используйте эту команду:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. В RStudio просмотреть тестовый сценарий, который вы загрузили hello. Дважды щелкните tooopen файл hello, выберите hello содержимое файла hello и нажмите кнопку **запуска**. Вы должны увидеть результаты hello в hello **консоли** панели:

   ![Проверьте установку hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "протестировать установку hello")

Можно было бы tootype `source(testhdi.r)` или `source(testhdi_spark.r)` tooexecute hello скрипта.

## <a name="see-also"></a>См. также

* [Compute context options for R Server on HDInsight clusters (Параметры контекста вычислений для R Server в кластерах HDInsight)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-storage.md)

