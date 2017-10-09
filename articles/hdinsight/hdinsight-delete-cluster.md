---
title: "aaaHow toodelete кластер HDInsight - Azure | Документы Microsoft"
description: "Сведения о hello различными способами, можно удалить кластер HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Удалить кластер HDInsight с помощью браузера, PowerShell или Azure CLI hello

Выставление счетов начинается после кластера и останавливается при удалении кластера hello кластера HDInsight. Кластеры оплачиваются поминутно, поэтому всегда следует удалять кластер, когда он больше не нужен. В этом документе вы узнаете, как hello toodelete кластера с помощью портала Azure, Azure PowerShell и hello Azure CLI 1.0.

> [!IMPORTANT]
> Удаление кластера HDInsight не приводит к удалению hello учетных записей хранилища Azure или хранилища Озера данных связана с кластером hello. Можно повторно использовать данные, хранящиеся в этих служб в будущем hello.

## <a name="azure-portal"></a>Портал Azure

1. Войдите в toohello [портал Azure](https://portal.azure.com) и выберите кластер HDInsight. Если ваш HDInsight кластер не закрепленных toohello панели мониторинга, можно поиск по имени, с помощью поля поиска hello.
   
    ![поиск по порталу](./media/hdinsight-delete-cluster/navbar.png)

2. После колонке hello открывается для hello кластера, выберите hello **удалить** значок. При появлении запроса выберите **Да** toodelete hello кластера.
   
    ![значок удаления](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

В командной строке PowerShell используйте hello, следующая команда toodelete hello кластера:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Замените **CLUSTERNAME** с hello имя кластера HDInsight.

## <a name="azure-cli-10"></a>Azure CLI 1.0

В строке используйте hello, следуя toodelete hello кластера:

    azure hdinsight cluster delete CLUSTERNAME

Замените **CLUSTERNAME** с hello имя кластера HDInsight.

> [!NOTE]
> Сейчас Azure CLI 2.0 не поддерживает удаление кластеров HDInsight (31 июля 2017 г.).