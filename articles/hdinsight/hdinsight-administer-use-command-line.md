---
title: "aaaManage Hadoop кластеры, использующие Azure CLI - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как кластеров toouse hello интерфейса командной строки Azure toomanage Hadoop в Azure HDInsight. Hello Azure CLI работает в Windows, Mac и Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Управление кластерами Hadoop в HDInsight с помощью hello Azure CLI
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Узнайте, как toouse hello [интерфейса командной строки Azure](../cli-install-nodejs.md) toomanage Hadoop кластеров в Azure HDInsight. Hello Azure CLI реализуется в Node.js. Его можно использовать на любой платформе, которая поддерживает Node.js, включая Windows, Mac и Linux.

В этой статье рассматриваются только с помощью hello Azure CLI с HDInsight. Общие инструкции о том, как toouse Azure CLI см. в разделе [установить и настроить Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure CLI** -разделе [установить и настроить hello Azure CLI](../cli-install-nodejs.md) сведения об установке и настройке.
* **Подключение tooAzure**, с использованием hello следующую команду:
  
        azure login
  
    Дополнительные сведения о проверке подлинности с помощью рабочей или учебной учетной записи см. в разделе [подключение tooan подписки Azure из hello Azure CLI](../xplat-cli-connect.md).
* **Переключите режим диспетчера ресурсов Azure toohello**, с использованием hello следующую команду:
  
        azure config mode arm

Справка tooget использовать hello **-h** переключения.  Например:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Создать кластеры с hello CLI
В разделе [создание кластеров HDInsight с помощью hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Отображение сведений о кластере
Используйте следующие команды toolist hello и отображают сведения о кластере:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Представление командной строки списка кластеров][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Удаление кластеров
Используйте следующие команды toodelete кластера hello:

    azure hdinsight cluster delete <Cluster Name>

Можно также удалить кластер, удалив hello группы ресурсов, содержащий hello кластера. Обратите внимание, это приведет к удалению всех ресурсов группы hello, включая учетную запись хранения по умолчанию hello hello.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Масштабирование кластеров
hello toochange размер кластера Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Включение или отключение доступа по протоколу HTTP для кластера
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Включение или отключение доступа по протоколу RDP для кластера
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как tooperform разные HDInsight кластер задачи администрирования. toolearn более, см. следующие статьи hello.

* [Администрирование HDInsight с помощью портала Azure hello][hdinsight-admin-portal]
* [Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]
* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Как toouse hello Azure CLI][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Отображение кластеров"
