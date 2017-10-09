---
title: "кластеры aaaCustomize Hadoop для hello командного процесса обработки и анализа данных | Документы Microsoft"
description: "Популярные модули Python становятся доступными в настраиваемых кластерах Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Настроить кластеры Azure HDInsight Hadoop для hello командного процесса обработки и анализа данных
Данной статье рассмотрены как кластер HDInsight Hadoop toocustomize путем установки 64-разрядных Anaconda (Python 2.7) на каждом узле кластера hello предоставляется в качестве службы HDInsight. Здесь также показано, как tooaccess hello головному узлу toosubmit пользовательские задания toohello кластера. Такая настройка позволяет многие популярные Python модули, которые включены в Anaconda, поскольку удобно доступна для использования в пользователя определенные функции (UDF), которые являются предназначен tooprocess записей Hive в кластере hello. Инструкции по hello процедуры, используемые в этом сценарии см. в разделе [как запросы Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

Hello следующее меню ссылки, описывающие возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello tootopics [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Настройка кластера Hadoop под управлением службы Azure HDInsight
Запуск toocreate настроенные кластера HDInsight Hadoop, войдя в систему слишком[**классический портал Azure**](https://manage.windowsazure.com/), нажмите кнопку **New** на hello слева вниз углу, а затем выберите службы данных HDINSIGHT -> -> **НАСТРАИВАЕМОЕ создание** toobring копирование hello **сведения о кластере** окна. 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Ввод hello имя кластера toobe hello, созданные на странице конфигурации 1 и примите значения по умолчанию для hello другие поля. Щелкните hello стрелка toogo toohello следующей странице конфигурации. 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

На странице конфигурации 2, введите число hello **УЗЛЫ данных**выберите hello **регион или ВИРТУАЛЬНАЯ сеть**и выберите размеры hello hello **ГОЛОВНОГО узла** и hello **Узел данных**. Щелкните hello стрелка toogo toohello следующей странице конфигурации.

> [!NOTE]
> Hello **регион или ВИРТУАЛЬНАЯ сеть** имеет toobe Здравствуйте таким же, как область hello hello учетной записи хранения, что будет toobe для hello кластера HDInsight Hadoop. В противном случае hello четвертой странице конфигурации учетной записи хранилища hello не отображаются на раскрывающийся список hello **имя учетной записи**.
> 
> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

На странице конфигурации 3 укажите имя пользователя и пароль для hello кластера HDInsight Hadoop. **Не** выберите hello *ввод hello куст или Метахранилище Oozie*. Нажмите кнопку hello стрелка toogo toohello следующей странице конфигурации. 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

На странице конфигурации 4 укажите имя учетной записи хранения hello, контейнер по умолчанию hello hello кластера HDInsight Hadoop. При выборе *создать контейнер по умолчанию* в hello **КОНТЕЙНЕР по умолчанию** раскрывающийся список, контейнер с помощью hello точно такое же имя, как будет создан кластер hello. Щелкните hello стрелка toogo toohello последней конфигурации страницы.

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

На последней hello **действия скрипта** «конфигурация» нажмите кнопку **добавьте действия скрипта** кнопку и заполнения поля текст hello hello следующие значения.

* **ИМЯ** -любую строку как имя действия сценария hello
* **Тип узла** — выберите значение **Все узлы**.
* **URI-адрес скрипта**  - —*http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* — это открытый контейнер в учетной записи хранения hello 
  * *getgoing* мы используем tooshare PowerShell скрипт файлы toofacilitate работы пользователей в Azure
* **ПАРАМЕТРЫ** — оставьте это поле пустым.

Щелкните флажок hello toostart Создание hello hello настроить кластер HDInsight Hadoop. 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Доступ к hello головного узла кластера Hadoop
Прежде чем можно обращаться из головного узла кластера Hadoop hello hello протокола удаленного рабочего СТОЛА необходимо включить кластера Hadoop toohello удаленного доступа в Azure. 

1. Войдите в toohello [ **классический портал Azure**](https://manage.windowsazure.com/)выберите **HDInsight** hello левой части экрана выберите кластер Hadoop из списка кластеров hello, щелкните hello  **КОНФИГУРАЦИЯ** , а затем щелкните hello **ВКЛЮЧИТЬ УДАЛЕННЫЙ** значок hello нижней части страницы приветствия.
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. В hello **настроить удаленный рабочий стол** , введите hello ИМЕНИ пользователя и пароля и выберите пункт hello Дата окончания срока действия для удаленного доступа. Нажмите кнопку hello флажок tooenable hello удаленного доступа toohello головного узла кластера Hadoop hello.
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> Hello имя пользователя и пароль для удаленного доступа hello не hello имя пользователя и пароль, используемый при создании кластера Hadoop hello. Это отдельный набор учетных данных. Кроме того Дата окончания срока действия hello hello удаленного доступа имеет toobe в течение 7 дней после hello текущую дату.
> 
> 

После включения удаленного доступа щелкните **CONNECT** внизу hello tooremote страницы приветствия на головном узле hello. Вход toohello головного узла кластера Hadoop hello, введя hello учетные данные пользователя удаленного доступа hello, указанный ранее.

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Hello следующим шагам в hello advanced analytics процесса сопоставлены в hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) и могут содержать действия, которые перемещение данных в HDInsight, а затем обрабатывают и образец он существует в процессе подготовки для обучения на основе данных hello с помощью машинного обучения Azure.

В разделе [как запросы Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) инструкции как tooaccess hello Python модулей, включенных в Anaconda из hello головного узла кластера hello в определяемые пользователем функции (UDF), которые используется tooprocess Hive записей, хранимых в кластере hello.

