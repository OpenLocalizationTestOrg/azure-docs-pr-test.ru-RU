---
title: "с помощью изолированной среде Hadoop — эмулятор — Azure HDInsight aaaLearn | Документы Microsoft"
description: "обучающие материалы по с помощью toostart Здравствуйте экосистема Hadoop, настройкой изолированной среде Hadoop из Hortonworks на виртуальной машине Azure. "
keywords: "эмулятор hadoop,песочница hadoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Начало работы с песочницей Hadoop, эмулятором на виртуальной машине

Узнайте, как tooinstall hello Hadoop «песочнице» Hortonworks на виртуальную машину toolearn о Hadoop экосистема hello. "песочница" Hello предоставляет toolearn среде местного разработки о Hadoop, система распределенного файла Hadoop (HDFS) и отправки заданий. Если вы знакомы с Hadoop, вы можете начать использовать Hadoop в Azure, создав кластер HDInsight. Дополнительные сведения о том, как tooget работы см. в разделе [Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Предварительные требования
* [Oracle VirtualBox](https://www.virtualbox.org/). Скачайте и установите приложение [отсюда](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Загрузите и установите hello виртуальной машины
1. Обзор toohello [Hortonworks загружает](http://hortonworks.com/downloads/#sandbox).

2. Нажмите кнопку **загрузки VIRTUALBOX** toodownload hello последнюю Hortonworks "песочницы" на виртуальной Машине. Все запрашиваемые tooregister с Hortonworks перед началом загрузки hello. Он принимает один toodownload tootwo часов в зависимости от скорости сети.
   
    ![Изображение ссылки для скачивания песочницы Hortonworks для VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. Из Здравствуйте одной веб-странице, щелкните hello **импорта на Virtual Box** связать toodownload PDF-ФАЙЛ, содержащий инструкции по установке для hello виртуальной машины.

toodownload изолированной более старые версии HDP разверните hello архива:

![Архив песочницы Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Запустить виртуальную машину hello

1. Откройте Oracle VirtualBox на виртуальной машине.
2. Из hello **файл** меню, нажмите кнопку **устройство импорта**и укажите hello изображения Hortonworks "песочницы".
1. Выберите hello Hortonworks "песочницы", нажмите кнопку **запустить**, а затем **Обычный запуск**. После завершения процесса загрузки hello hello виртуальной машины она отображает инструкции имени входа.
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Откройте веб-браузер и перейдите toohello URL-адрес отображается (обычно http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Задание паролей для песочницы

1. Из hello **начать** hello Hortonworks "песочницы", выберите шаг **Дополнительные параметры представления**. Используйте hello сведения на этой странице toolog в песочнице toohello с помощью SSH. Используйте hello имя и пароль.
   
   > [!NOTE]
   > Если у вас установлен клиент SSH, можно использовать веб-SSH, предоставляемые в hello виртуальной машины в hello **http://localhost:4200 /**.
   > 
   
    Hello при первом подключении с помощью SSH, все запрашиваемые toochange hello пароль для учетной записи root hello. Введите новый пароль, используемый при входе с помощью SSH.

2. После входа введите hello следующую команду:
   
        ambari-admin-password-reset
   
    При появлении запроса введите пароль для учетной записи администратора Ambari hello. Это используется при доступе к hello Ambari веб-интерфейса.

## <a name="use-hive-commands"></a>Использование команд Hive

1. В изолированной toohello SSH подключения используйте следующие командной оболочки Hive hello toostart hello:
   
        hive
2. После запуска оболочки hello, используйте следующие таблицы tooview hello, имеющиеся в "песочнице" hello hello:
   
        show tables;
3. Используйте hello следующую tooretrieve 10 строк из hello `sample_07` таблицы:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте, как toouse Visual Studio с hello Hortonworks "песочницы"](hdinsight-hadoop-emulator-visual-studio.md)
* [Изучение ropes hello объекта hello Hortonworks "песочницы"](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/) (Руководство по началу работы с Hadoop)

