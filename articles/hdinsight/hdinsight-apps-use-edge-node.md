---
title: "aaaUse пустые краевым узлам на кластеров Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Как tooadd edge пустой узел tooan HDInsight кластер, который можно использовать в качестве клиента и затем теста или узла приложения HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Использование пустых граничных узлов в кластерах Hadoop в HDInsight

Узнайте, как tooadd пустой ребро кластера HDInsight tooan узла. Пустой граничного узла — это виртуальная машина Linux с hello же клиентские средства установлен и настроен как hello headnodes, но ни одна служба Hadoop под управлением. Hello граничного узла можно использовать для доступа к кластеру hello, тестирования клиентские приложения и размещение клиентских приложений. 

При создании кластера hello, можно добавить существующий кластер HDInsight edge пустой узел tooan, tooa новый кластер. Добавление пустого граничного узла осуществляется с помощью шаблона Azure Resource Manager.  Hello следующий пример демонстрирует, как это можно сделать с помощью шаблона:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Как показано в образце hello, при необходимости можно вызвать [записать действие в скрипт](hdinsight-hadoop-customize-cluster-linux.md) tooperform дополнительной настройки, таких как установка [оттенка Apache](hdinsight-hadoop-hue-linux.md) в hello граничного узла. сценарий действие Hello сценарий должен быть общедоступным Интернете hello.  Например если сценарий hello хранится в хранилище Azure, используйте общедоступных контейнеров или общедоступных больших двоичных объектов.

размер виртуальной машины узел edge Hello требования hello HDInsight кластера рабочий узел виртуальной машины размера. Hello рекомендуется работника размеры виртуальных машин на узле, см. в разделе [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

После создания граничного узла можно подключиться toohello граничного узла с помощью SSH и запустить клиент кластера Hadoop hello tooaccess средства в HDInsight.

> [!WARNING] 
> Возможность использования пустого граничного узла с HDInsight доступна в предварительной версии. Пользовательские компоненты, установленные на hello граничного узла получать ограниченную техническую поддержку от Майкрософт. В результате могут быть устранены возникающие проблемы. Или может быть ссылка toocommunity ресурсы для получения дополнительной помощи. Hello ниже приведены некоторые hello большинство активными узлами для получения справки из hello сообщества:
>
> * [Форум MSDN для HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> При использовании технологии Apache может быть помощника может toofind через hello сайтов проектов Apache на [http://apache.org](http://apache.org), такие как hello [Hadoop](http://hadoop.apache.org/) сайта.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Добавить существующий кластер узла tooan edge
В этом разделе используется tooadd шаблона диспетчера ресурсов edge узел tooan существующий кластер HDInsight.  шаблон диспетчера ресурсов Hello можно найти в [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). шаблон диспетчера ресурсов Hello вызывает действие скрипта, расположенный в https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. сценарий Hello не выполняет каких-либо действий.  Это toodemonstrate вызов действия скрипта из шаблона диспетчера ресурсов.

**tooadd tooan edge пустой узел существующего кластера**

1. Создайте кластер HDInsight, если его еще нет.  Ознакомьтесь со статьей [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов Azure в hello портал Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Настройте hello следующие свойства:
   
   * **Подписки**: выберите подписку Azure, используемый для создания кластера hello.
   * **Группа ресурсов**: hello выберите группы ресурсов, используемой для hello существующего кластера HDInsight.
   * **Расположение**: выберите расположение hello hello существующего кластера HDInsight.
   * **Имя кластера**: Введите имя существующего кластера HDInsight hello.
   * **Ребро размер узла**: выберите один из размеров виртуальных Машин hello. Hello размер виртуальной машины должны соответствовать требованиям к размеру hello рабочих узла виртуальной машины. Hello рекомендуется работника размеры виртуальных машин на узле, см. в разделе [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Ребро префикса узла**: hello значение по умолчанию — **новый**.  Используется значение по умолчанию hello, является имя узла edge hello **новый edgenode**.  Можно настроить префикс hello из портала hello. Можно также настроить hello полное имя из шаблона hello.

4. Проверьте **я принимаю условия, указанных выше, toohello**, а затем нажмите кнопку **покупки** toocreate hello граничного узла.

>[!IMPORTANT]
> Убедитесь, что группы ресурсов Azure hello tooselect hello существующих кластеров HDInsight.  В противном случае ошибки hello сообщение «Невозможно выполнить запрошенную операцию для вложенных ресурсов. Родительский ресурс &lt;ClusterName> не найден."

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Добавление граничного узла при создании кластера
В этом разделе можно использовать диспетчер ресурсов шаблона toocreate HDInsight с граничного узла.  шаблон диспетчера ресурсов Hello можно найти в hello [коллекции шаблонов быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). шаблон диспетчера ресурсов Hello вызывает действие скрипта, расположенный в https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. сценарий Hello не выполняет каких-либо действий.  Это toodemonstrate вызов действия скрипта из шаблона диспетчера ресурсов.

**tooadd tooan edge пустой узел существующего кластера**

1. Создайте кластер HDInsight, если его еще нет.  Ознакомьтесь со статьей [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов Azure в hello портал Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Настройте hello следующие свойства:
   
   * **Подписки**: выберите подписку Azure, используемый для создания кластера hello.
   * **Группа ресурсов**: создать новую группу ресурсов, используемых для hello кластера.
   * **Расположение**: выберите расположение для группы ресурсов hello.
   * **Имя кластера**: Введите имя для нового кластера toocreate hello.
   * **Имя входа пользователя кластера**: Введите имя пользователя Hadoop HTTP hello.  имя по умолчанию Hello — **администратора**.
   * **Имя входа пароль кластера**: Введите пароль пользователя Hadoop HTTP hello.
   * **SSH имя пользователя**: Введите имя пользователя SSH hello. имя по умолчанию Hello — **sshuser**.
   * **SSH пароль**: Введите пароль пользователя для SSH hello.
   * **Установите действие сценария**: оставьте значение по умолчанию hello в этом учебнике.
     
     Некоторые свойства были жестко задано в шаблоне hello: тип кластера, число узлов кластера рабочих, размер границы узла и имя узла Edge.
4. Проверьте **я принимаю условия, указанных выше, toohello**и нажмите кнопку **покупки** toocreate hello кластер с граничного узла hello.

## <a name="access-an-edge-node"></a>Доступ к граничному узлу
Hello граничного узла ssh конечная точка является &lt;EdgeNodeName >.&lt; Имя_кластера >-ssh.azurehdinsight.net:22.  Например, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

Hello граничного узла отображается как приложение на hello портал Azure.  Hello портала дает hello hello tooaccess сведения ребро узла с помощью SSH.

**Конечная точка SSH узел tooverify hello edge**

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Откройте hello кластера HDInsight с граничного узла.
3. Нажмите кнопку **приложений** из кластера колонки hello. Должны появиться hello граничного узла.  имя по умолчанию Hello — **новый edgenode**.
4. Щелкните узел edge hello. Вы увидите конечной точки для SSH hello.

**Куст toouse на hello граничного узла**

1. Используйте SSH tooconnect toohello граничного узла. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. После подключения toohello граничного узла с помощью SSH, используйте следующие командной консоли Hive hello tooopen hello:
   
        hive
3. Выполните следующие команды tooshow Hive таблицы в кластере hello hello.
   
        show tables;

## <a name="delete-an-edge-node"></a>Удаление граничного узла
Граничного узла можно удалить из hello портал Azure.

**tooaccess граничного узла**

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Откройте hello кластера HDInsight с граничного узла.
3. Нажмите кнопку **приложений** из кластера колонки hello. Появится список граничных узлов.  
4. Щелкните правой кнопкой мыши hello граничного узла toodelete и нажмите кнопку **удалить**.
5. Нажмите кнопку **Да** tooconfirm.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как tooadd граничного узла и как tooaccess hello граничного узла. toolearn более, см. следующие статьи hello.

* [Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.
* [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как toodeploy неопубликованные приложения tooHDInsight HDInsight.
* [Публикация приложений HDInsight](hdinsight-apps-publish-applications.md): Узнайте, как toopublish вашего пользовательского tooAzure приложения Marketplace HDInsight.
* [MSDN: Установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Узнайте, как toodefine HDInsight приложений.
* [Настроить кластеры HDInsight под управлением Linux, с помощью сценария действия](hdinsight-hadoop-customize-cluster-linux.md): Узнайте, как toouse действие сценария tooinstall дополнительные приложения.
* [Создавать кластеры под управлением Linux Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Узнайте, как кластеры toocreate шаблонов диспетчера ресурсов toocall HDInsight.

