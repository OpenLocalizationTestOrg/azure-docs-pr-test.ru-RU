---
title: "aaaInstall сторонние приложения Hadoop в Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooinstall сторонние приложения Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Установка сторонних приложений Hadoop в Azure HDInsight

В этой статье вы узнаете, как tooinstall уже опубликованные сторонние приложения Hadoop в Azure HDInsight. Инструкции по установке собственного приложения см. в статье [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md).

Пользователи могут устанавливать приложения HDInsight в кластере HDInsight под управлением Linux. Разработчиками этих приложений могут быть корпорация Майкрософт, независимые поставщики программного обеспечения или вы сами.  

Сейчас опубликовано четыре приложения:

* **DDS DATAIKU на HDInsight**: Dataiku DSS (Studio обработки и анализа данных) — это программное обеспечение, и позволяющая данных tooprototype специалистов (специалисты по анализу данных, бизнес-аналитики, разработчики...), построение и развертывание высокой конкретных служб, которые преобразования необработанных данных в прогнозы существенных бизнеса.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) предлагает аналитикам toodiscover интерактивный способ, анализировать и визуализировать результаты hello на большие наборы данных. По запросу в дополнительных источников данных легко toodiscover новые связи и получать ответы hello быстро.
* **Сборщик данных Streamsets для HDnsight** предоставляет полнофункциональную интегрированной среды разработки (IDE) позволяет разработки, тестирования, развертывания и управлять any к any приема конвейеры, подготавливая потока и раздел данных что включают ряд преобразования в потоке, не компилируя toowrite пользовательский код. 
* **Cask CDAP для HDInsight** предоставляет hello сначала единой платформы интеграции для больших данных, уменьшение hello tooproduction времени для данных приложений и данных Озера на 80%. Это приложение поддерживает только стандартные кластеры HBase 3.4.
* **Искусственный интеллект H2O. для HDInsight (бета-версия)** H2O. Sparkling воды поддерживает следующие распределенные алгоритмы hello: GLM, упрощенный алгоритм Байеса, распределенных случайных леса, градиента повышение приоритета машине, глубоких нейронных сетей, глубокого изучения, K-средние, PCA, Обобщенный низкий моделей ранжирования, обнаружение аномалий и Autoencoders.
* **Kyligence Analytics Platform** (KAP) — хранилище данных корпоративного уровня на платформе Apache Kylin и Apache Hadoop, которое обеспечивает обработку запросов в больших масштабируемых наборах данных с задержкой менее секунды и упрощает анализ данных для бизнес-пользователей и аналитиков. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex на HDInsight позволяет быстрее аналитики toobusiness tooget клиентов, предоставляя приема самообслуживания данных и подготовки из любого источника toohello облако Microsoft Azure Платформа.
* **Сервер заданий Spark для исполнителя Spark KNIME** сервер задания Spark для исполнителя Spark KNIME — используется tooconnect hello платформы аналитики KNIME tooHDInsight кластеров.

Hello инструкции, приведенные в этой статье с помощью портала Azure. Можно также Экспорт шаблона диспетчера ресурсов Azure hello из портала hello или получить копию hello шаблона диспетчера ресурсов от поставщиков и использовать Azure PowerShell и шаблон hello toodeploy Azure CLI.  Дополнительные сведения см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight с помощью шаблонов Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Предварительные требования
Если требуется tooinstall HDInsight приложений в существующем кластере HDInsight необходимо иметь кластер HDInsight. разделе toocreate, [создавать кластеры](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Вы также можете установить приложения HDInsight во время создания кластера HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Установка приложений tooexisting кластеров
Hello следующей процедуре показано, как tooinstall HDInsight приложений tooan существующего кластера HDInsight.

**tooinstall приложение HDInsight**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** в левом меню hello.  Если этот параметр не отображается, щелкните **Больше служб**, а затем выберите **Кластеры HDInsight**.
3. Щелкните кластер HDInsight.  Если у вас нет кластера, сначала его необходимо создать.  См. [этот раздел](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Нажмите кнопку **приложений** под hello **конфигурации** категории. Отобразится список установленных приложений. Если не удается найти приложения, это означает, что нет ни одного приложения для этой версии hello кластера HDInsight.
   
    ![Меню портала для приложений HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Нажмите кнопку **добавить** hello колонке меню. 
   
    ![Установленные приложения HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Отобразится список существующих приложений HDInsight.
   
    ![Доступные приложения HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Выберите один из приложения hello, примите условия использования hello и нажмите кнопку **выберите**.

Вы можете просматривать состояние установки hello из портала уведомления hello (щелкните значок колокольчика hello в верхней части hello hello портала). После hello установки приложения, приложение hello появится в колонке установленные приложения hello.

## <a name="install-applications-during-cluster-creation"></a>Установка приложения во время создания кластера
У вас есть hello параметр tooinstall HDInsight приложений при создании кластера. Во время процесса hello HDInsight приложения устанавливаются после создания кластера hello и находится в рабочем состоянии hello. Hello следующей процедуре показано, как tooinstall HDInsight приложений при создании кластера.

**tooinstall приложение HDInsight**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Щелкните **Создать**, **Данные+аналитика**, а затем — **HDInsight**.
3. Введите **имя кластера**: оно должно быть глобально уникальным.
4. Нажмите кнопку **подписки** tooselect hello подписки Azure, используемый для hello кластера.
5. Щелкните **Выберите тип кластера**, а затем выберите следующие значения:
   
   * **Тип кластера**: Если вы не знаете, какие toochoose, выберите **Hadoop**. Это наиболее популярных кластера типа hello.
   * **Операционная система**: выберите значение **Linux**.
   * **Версия**: использовать версию по умолчанию hello, если вы не знаете, какие toochoose. Дополнительные сведения см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)
   * **Кластер уровня**: Azure HDInsight представляет предложения облака hello большие наборы данных в двух категориях: уровней Standard и Premium. Дополнительные сведения см. в разделе [Уровни кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Нажмите кнопку **приложений**, выберите один из hello опубликованных приложений и нажмите кнопку **выберите**.
7. Нажмите кнопку **учетные данные** и затем введите пароль для пользователя с правами администратора hello. Необходимо также tooenter **имя пользователя SSH** и либо **пароль** или **ОТКРЫТЫЙ ключ**, являющееся используется tooauthenticate hello SSH пользователя. С помощью открытого ключа — hello рекомендованный подход. Нажмите кнопку **выберите** в hello нижней toosave hello учетные данные конфигурации.
8. Нажмите кнопку **источника данных**, выберите один из существующих учетных записей хранения hello или создать новый toobe учетной записи хранилища, используется в качестве учетной записи хранения по умолчанию hello для hello кластера.
9. Нажмите кнопку **группы ресурсов** tooselect существующий ресурс группы, или нажмите кнопку **New** toocreate новую группу ресурсов
10. На hello **новый кластер HDInsight** колонки, убедитесь, что **tooStartboard ПИН-код** выбран и нажмите кнопку **создать**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Отображение списка установленных приложений HDInsight и их свойств
портал Hello показывает список hello установленные приложения HDInsight для кластера, а также свойств каждого установленного приложения hello.

**Свойства приложения и отображения HDInsight toolist**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** в левом меню hello.  Если меню не отображается, нажмите кнопку **Обзор**, а затем щелкните **Кластеры HDInsight**.
3. Щелкните кластер HDInsight.
4. Из hello **параметры** колонка, щелкните **приложений** под hello **Общие** категории. Колонка установленные приложения Hello перечислены hello установки приложения. 
   
    ![Установленные приложения HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Выберите один из свойства hello tooshow приложения hello установлен. Здравствуйте колонке списков свойств:
   
   * Имя приложения— имя вашего приложения.
   * Состояние — состояние вашего приложения. 
   * Веб-страницы: hello URL-адрес веб-приложения hello, что вы развернули toohello граничного узла. учетные данные Hello — так же, как пользователь hello HTTP учетные данные, которые настроены для кластера hello приветствия.
   * Конечная точка HTTP: hello учетные данные представляют Привет, так же, как пользователь hello HTTP учетные данные, которые настроены для кластера hello. 
   * Конечная точка SSH: можно использовать SSH tooconnect toohello граничного узла. учетные данные SSH Hello, так же, как пользователь SSH hello учетные данные, которые настроены для кластера hello приветствия. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
6. Щелкните правой кнопкой мыши приложение hello toodelete приложение и нажмите кнопку **удалить** hello контекстном меню.

## <a name="connect-toohello-edge-node"></a>Подключить узел toohello edge
Можно подключить toohello граничного узла с помощью HTTP и SSH. можно найти сведения о конечной точке Hello hello [портала](#list-installed-hdinsight-apps-and-properties). См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

учетные данные конечной точки HTTP Hello, учетные данные пользователя hello HTTP, настроенные для кластера HDInsight hello; учетные данные конечной точки SSH Hello, SSH hello учетные данные, которые были настроены для кластера HDInsight hello.

## <a name="troubleshoot"></a>Устранение неполадок
В разделе [Устранение неполадок при установке hello](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Дальнейшие действия
* [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как toodeploy неопубликованные приложения tooHDInsight HDInsight.
* [Публикация приложений HDInsight](hdinsight-apps-publish-applications.md): Узнайте, как toopublish вашего пользовательского tooAzure приложения Marketplace HDInsight.
* [MSDN: Установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Узнайте, как toodefine HDInsight приложений.
* [Настроить кластеры HDInsight под управлением Linux, с помощью сценария действия](hdinsight-hadoop-customize-cluster-linux.md): Узнайте, как toouse действие сценария tooinstall дополнительные приложения.
* [Создавать кластеры под управлением Linux Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Узнайте, как кластеры toocreate шаблонов диспетчера ресурсов toocall HDInsight.
* [Используйте пустой краевым узлам в HDInsight](hdinsight-apps-use-edge-node.md): Узнайте, как toouse пустой ребро узла для доступа к кластеру HDInsight, тестирование приложений HDInsight и размещение приложений HDInsight.

