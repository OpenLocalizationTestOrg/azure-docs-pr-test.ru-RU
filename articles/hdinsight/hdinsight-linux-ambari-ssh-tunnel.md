---
title: "aaaUse SSH туннелирования tooaccess Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse toosecurely туннель SSH Обзор веб-ресурсов, размещенных на узлах под управлением Linux HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Использовать туннелирование SSH tooaccess Ambari web пользовательского интерфейса, JobHistory, NameNode, Oozie и других веб-интерфейсы пользователя

Кластеры HDInsight под управлением Linux предоставления пользовательского интерфейса web tooAmbari доступ через Интернет hello, но некоторые функции hello пользовательского интерфейса не имеют. Например hello веб-интерфейса для других служб, подключаемых через Ambari. Для обеспечения полной функциональности hello Ambari web пользовательского интерфейса необходимо использовать head кластера toohello туннеля SSH.

## <a name="why-use-an-ssh-tunnel"></a>Причины для использования туннеля SSH

Некоторые из меню hello в Ambari работают только через туннель SSH. Для этих меню используются веб-сайты и службы, выполняющиеся на узлах других типов, например рабочих узлах. Часто эти веб-узлы не защищены, поэтому не предоставляют безопасные toodirectly их на hello Интернет.

Привет, следуя пользовательских веб-интерфейсов требуется туннель SSH:

* Журнал заданий
* узел имен;
* стеки потоков;
* веб-интерфейс Oozie
* веб-интерфейс главного узла и журналов HBase

При использовании действия скрипта toocustomize кластера никаких служб или программ, установке, предоставляющих веб-интерфейса требуется туннель SSH. Например при установке оттенка с помощью действия сценария, необходимо использовать SSH туннеля tooaccess hello оттенка пользовательского веб-интерфейса.

> [!IMPORTANT]
> Если у вас есть tooHDInsight прямой доступ через виртуальную сеть, не обязательно toouse туннеля SSH. Пример прямого доступа к HDInsight через виртуальную сеть, в разделе hello [HDInsight подключения tooyour локальной сети](connect-on-premises-network.md) документа.

## <a name="what-is-an-ssh-tunnel"></a>Что такое туннель SSH?

[Secure Shell (SSH) туннелирование](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) направляет трафик tooa порт на локальной рабочей станции. Hello трафик направляется через SSH подключения tooyour HDInsight головного узла кластера. запрос Hello определяется, как если бы она была создана на головном узле hello. ответ Hello направляется обратно через туннель hello tooyour-рабочей станции.

## <a name="prerequisites"></a>Предварительные требования

* Клиент SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* Веб-браузер, может быть настроен прокси-серверов SOCKS5 toouse.

    > [!WARNING]
    > Поддержка прокси-сервера SOCKS Hello, встроенная в Windows не поддерживает SOCKS5 и не работает с hello в данном пошаговом руководстве. Hello следующие браузеры используют параметры прокси-сервера Windows и не в настоящее время работают с hello в данном пошаговом руководстве:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome также зависит от параметров прокси-сервера Windows hello. Но можно установить расширения, которые поддерживают SOCKS5. Рекомендуется использовать [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Создает туннель, с помощью команды SSH hello

Используйте hello следующая команда toocreate туннель SSH, с помощью hello `ssh` команды. Замените **USERNAME** пользователем SSH для кластера HDInsight и замените **CLUSTERNAME** с hello имя кластера HDInsight:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Эта команда создает подключение, которое направляет трафик toolocal порт 9876 toohello кластера через SSH. доступны следующие параметры Hello.

* **D 9876** -hello локальный порт, который перенаправляет трафик через туннель hello.
* **C** — сжатие всех данных, так как веб-трафик преимущественно состоит из текста;
* **2** -force SSH tootry протокол версии 2 только.
* **q** — тихий режим;
* **T** — отключение распределения псевдотелетайпа, так как выполняется только перенаправление порта;
* **n** — предотвращение считывания с STDIN, так как выполняется только перенаправление порта;
* **N** — запрет на выполнение удаленной команды, так как выполняется только перенаправление порта;
* **f** -выполняются в фоновом режиме hello.

После завершения выполнения команды hello tooport трафик 9876 на локальном компьютере hello является перенаправленное toohello головного узла кластера.

## <a name="useputty"></a>Создание туннеля с помощью PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) — это графический клиент SSH для Windows. Используйте следующие шаги toocreate туннель SSH, с помощью PuTTY hello.

1. Откройте PuTTY и введите информацию о подключении. Если вы не знакомы с PuTTY, см. раздел hello [PuTTY документации (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. В hello **категории** toohello раздел левой части диалогового окна hello, разверните **подключения**, разверните **SSH**и выберите **туннели**.

3. Укажите следующую информацию на hello hello **перенаправление портов параметры, управляющие SSH** формы:
   
   * **Порт источника** -порт на приветствия клиента обратиться в tooforward hello. Например, **9876**.

   * **Назначение** -hello SSH-адрес для кластера HDInsight под управлением Linux hello. Например, **mycluster-ssh.azurehdinsight.net**.

   * **Динамическая** — включает динамическую маршрутизацию прокси-сервера SOCKS.
     
     ![изображение параметров туннелирования](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Нажмите кнопку **добавить** tooadd hello параметры и нажмите кнопку **откройте** tooopen SSH-подключения.

5. При появлении запроса выполните вход toohello сервера.

## <a name="use-hello-tunnel-from-your-browser"></a>Используйте туннеля hello из браузера

> [!IMPORTANT]
> Hello шагов в hello используйте этот раздел браузера Mozilla FireFox, поскольку она обеспечивает hello одинаковые параметры прокси-сервера на всех платформах. Другими современными браузерами, например Google Chrome, может потребоваться расширение, например toowork FoxyProxy с hello туннеля.

1. Настройка обозревателя toouse hello **localhost** и hello порт, который использовался при создании туннеля hello как **SOCKS v5** прокси-сервера. Ниже показано, как выглядят параметры Firefox hello. Если используется другой порт, чем 9876 измените toohello порт hello тот, который используется:
   
    ![изображение параметров Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > При выборе **удаленного DNS** разрешает запросы доменных имен (DNS) с помощью hello кластера HDInsight. Этот параметр разрешает DNS с помощью hello головного узла кластера hello.

2. Убедитесь, что туннель hello работает, перейдя по адресу сайта, таких как [http://www.whatismyip.com/](http://www.whatismyip.com/). Hello IP возвращается один используемого центра обработки данных Microsoft Azure hello.

## <a name="verify-with-ambari-web-ui"></a>Проверка для веб-интерфейса Ambari

После установления hello кластера используйте следующие шаги tooverify из hello Ambari Web доступен веб-службы пользовательских интерфейсов hello:

1. В браузере перейдите toohttp://headnodehost:8080. Hello `headnodehost` адрес передаются через hello туннеля toohello кластера и разрешить toohello головному узлу, на котором Ambari работает на. При появлении запроса введите имя пользователя администратора hello (администратор) и пароль для кластера. Может потребоваться еще раз, hello Ambari web пользовательского интерфейса. В этом случае введите сведения hello.

   > [!NOTE]
   > При использовании hello http://headnodehost:8080 адрес tooconnect toohello кластера, при подключении через туннель hello. Безопасность обмена данными с использованием туннеля SSH hello вместо HTTPS. tooconnect более hello Интернет с использованием HTTPS, используйте https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — имя кластера hello hello.

2. Hello Ambari веб-интерфейса выберите из списка hello hello левой стороны страницы приветствия HDFS.

    ![Изображение с выбранным пунктом HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. При отображении hello сведения о службе HDFS, выберите **быстрые ссылки**. Появится список головного узла кластера hello. Выберите один из головного узла hello, а затем выберите **NameNode пользовательского интерфейса**.

    ![Развернуть образ с меню QuickLinks hello](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > При выборе меню __Быстрые ссылки__ может появиться индикатор ожидания. Это может произойти, если подключение к Интернету медленное. Подождите минуту или две для hello toobe данных, полученных с сервера hello, а затем повторите попытку hello список.
   >
   > Некоторые записи в hello **быстрые ссылки** меню может быть обрезана hello правой части экрана приветствия. В этом случае разверните меню hello, с помощью мыши и использовать hello со стрелкой вправо ключа tooscroll hello экрана toohello правой toosee hello rest меню «hello».

4. Отображается примерно toohello страницы, после изображения.

    ![Изображение hello NameNode пользовательского интерфейса](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Обратите внимание, hello URL-адрес для этой страницы; он должен выглядеть слишком**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088 и кластером**. Этот URI используется hello внутреннее полное доменное имя (FQDN) узла hello и доступен только при использовании туннель SSH.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toocreate и используйте туннель SSH см. следующий документ для других способов toouse Ambari hello:

* [Управление кластерами HDInsight с помощью Ambari](hdinsight-hadoop-manage-ambari.md)

Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

