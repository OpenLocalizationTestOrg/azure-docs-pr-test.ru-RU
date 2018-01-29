---
title: "Публикация приложений Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как создать приложение HDInsight, а затем опубликовать его в Azure Marketplace."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/03/2018
ms.author: jgao
ms.openlocfilehash: 597ea68f063d02541132d275de815c1673369ae0
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2018
---
# <a name="publish-an-hdinsight-application-in-the-azure-marketplace"></a>Публикация приложения HDInsight в Azure Marketplace
Вы можете установить приложения Azure HDInsight в кластере HDInsight под управлением Linux. В этой статье описано, как опубликовать приложение HDInsight в Azure Marketplace. Общие сведения о публикации в Azure Marketplace см. в статье [Публикация предложения и управление им в Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

В приложениях HDInsight используется модель *с использованием собственной лицензии (BYOL)*. В сценарии BYOL поставщик приложения отвечает за предоставление лицензии пользователям приложения. С пользователей приложения плата взимается только за созданные ресурсы Azure, например кластер HDInsight, виртуальные машины и узлы кластера. Сейчас счета за само приложение не выставляются в Azure.

Дополнительные сведения см. в этих статьях о приложении HDInsight:

* [Установка сторонних приложений Hadoop в Azure HDInsight](hdinsight-apps-install-applications.md). Узнайте, как установить приложение HDInsight в кластерах.
* [Установка пользовательских приложений Hadoop в Azure HDInsight](hdinsight-apps-install-custom-applications.md). Узнайте, как устанавливать и тестировать пользовательские приложения HDInsight.

## <a name="prerequisites"></a>Технические условия
Чтобы отправить пользовательское приложение в Marketplace, необходимо сначала [создать и протестировать его](hdinsight-apps-install-custom-applications.md).

Также вы должны зарегистрировать учетную запись разработчика. Дополнительные сведения см. в статье [Публикация предложения и управление им в Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) и [Создание учетной записи разработчика Майкрософт](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-the-application"></a>Определение приложения
Публикация приложений в Marketplace осуществляется в два этапа. Сначала определите файл *createUiDef.json*. Файл createUiDef.json указывает, с какими кластерами совместимо ваше приложение. Затем опубликуйте шаблон с помощью портала Azure. Вот пример файла createUiDef.json:

```json
{
    "handler": "Microsoft.HDInsight",
    "version": "0.0.1-preview",
    "clusterFilters": {
        "types": ["Hadoop", "HBase", "Storm", "Spark"],
        "versions": ["3.6"]
    }
}
```

| Поле | ОПИСАНИЕ | Возможные значения |
| --- | --- | --- |
| types |Типы кластеров, совместимые с приложением. |Hadoop, HBase, Storm, Spark (или любое их сочетание) |
| versions |Версии кластеров HDInsight, совместимые с приложением. |3.4 |

## <a name="application-installation-script"></a>Сценарий установки приложения
После установки приложения в кластере (в имеющемся или в новом) создается граничный узел. Сценарий установки приложения выполняется на граничном узле.

  > [!IMPORTANT]
  > Имя сценария установки приложения должно быть уникальным для конкретного кластера и иметь следующий формат:
  > 
  > "name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Имя сценария состоит из трех частей:
  > 
  > * Префикс имени, который состоит из имени приложения или имени, которое связано с приложением.
  > * Дефис (-) для удобочитаемости.
  > * Уникальная строковая функция с именем приложения в качестве параметра.
  > 
  > В предыдущем примере в сохраненном списке действий сценария имя будет выглядеть так: **hue-install-v0-4wkahss55hlas**. Для дополнительной информации см. [пример полезных данных JSON](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 

Сценарий установки должен иметь следующие характеристики:
* Сценарий должен быть идемпотентным. Несколько вызовов сценария дают одинаковый результат.
* Сценарий должен иметь подходящую версию. Используйте другое расположение для сценария при обновлении или тестировании изменений. Таким образом, это не повлияет на пользователей, которые устанавливают приложение. 
* В сценарии есть необходимые вызовы для ведения журналов. Обычно устранить проблемы при установке приложения можно только с помощью журналов сценариев.
* Вызовы к внешним службам и ресурсам имеют достаточно повторных попыток, чтобы на установку не влияли временные неполадки сети.
* Если сценарий запускает службы на узлах, они отслеживаются и настраиваются для автоматического запуска в случае перезагрузки узла.

## <a name="package-the-application"></a>Создание пакета приложения
Создайте ZIP-файл, содержащий все необходимые файлы для установки приложений HDInsight. Используйте этот ZIP-файл, чтобы [опубликовать приложение](#publish-application). Этот ZIP-файл содержит следующие файлы:

* [createUiDefinition.json](#define-application);
* mainTemplate.json (пример см. в статье [Установка пользовательских приложений Hadoop в Azure HDInsight](hdinsight-apps-install-custom-applications.md));
* все необходимые сценарии.

> [!NOTE]
> Вы можете разместить файлы приложения (включая все файлы веб-приложения) на любой общедоступной конечной точке.
> 

## <a name="publish-the-application"></a>Публикация приложения
Чтобы опубликовать приложение HDInsight, сделайте следующее:

1. Войдите на [Портал публикации Azure](https://publish.windowsazure.com/).
2. В меню слева выберите **Solution templates** (Шаблоны решений).
3. Введите заголовок и нажмите **Create a new solution template** (Создать шаблон решения).
4. Щелкните **Create Dev Center account and join the Azure program** (Создать учетную запись центра разработчиков и присоединиться к программе Azure), чтобы зарегистрировать свою компанию, если вы еще этого не сделали.  Дополнительные сведения см. в статье [Создание учетной записи разработчика Майкрософт](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Выберите **Define some Topologies to get Started** (Определить некоторые топологии и начать работу). Шаблон решения служит родительским элементом для всех своих топологий. В одном шаблоне предложений или решения можно определить сразу несколько топологий. Когда предложение переходит к стадии промежуточного развертывания, вместе с ним отправляются все его топологии. 
6. Введите имя топологии, а затем выберите **+**.
7. Введите новую версию, а затем выберите **+**.
8. Отправьте ZIP-файл, созданный при [создании пакета приложения](#package-application).  
9. Выберите **Request Certification** (Запросить сертификацию). Команда сертификации Майкрософт проверяет файлы и выполняет сертификацию топологии.

## <a name="next-steps"></a>Дальнейшие действия
* Инструкции по [установке приложений HDInsight](hdinsight-apps-install-applications.md) в кластерах.
* Инструкции по [установке пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md) и развертывании в HDInsight неопубликованного приложения HDInsight.
* Инструкции по [настройке кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md) и добавлению других приложений. 
* Инструкции по [созданию кластера Hadoop под управлением Linux в HDInsight с помощью шаблонов Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
* Инструкции по [использованию пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md), чтобы получить доступ к кластеру HDInsight, а также тестировать и разместить приложения HDInsight.

