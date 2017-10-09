---
title: "приложения aaaPublish HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как toocreate и публикация приложений HDInsight."
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
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Публикация приложений HDInsight в hello Azure Marketplace
Пользователи могут устанавливать приложения HDInsight в кластере HDInsight под управлением Linux. Разработчиками этих приложений могут быть корпорация Майкрософт, независимые поставщики программного обеспечения или вы сами. В этой статье вы узнаете, как toopublish HDInsight приложения в Azure Marketplace hello.  Общие сведения о публикации в Azure Marketplace hello см. в разделе [публикации toohello предложение Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

HDInsight приложения используют hello *принеси свой собственный лицензии (BYOL)* модели, где поставщик приложение отвечает за лицензирование tooend приложения hello-пользователей и конечным пользователям только взимается по Azure для ресурсов hello они Создайте, например кластера HDInsight hello и его виртуальных машин и узлов. В настоящее время выставления счетов для самого приложения hello не осуществляется с помощью Azure.

Другие статьи о приложениях HDInsight:

* [Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.
* [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как tooinstall и тестирования пользовательских приложений HDInsight.

## <a name="prerequisites"></a>Предварительные требования
toosubmit ваш marketplace toohello пользовательское приложение, вы должны создания и тестирования вашего приложения. См. следующие статьи hello.

* [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как tooinstall и тестирования пользовательских приложений HDInsight.

Также необходимо зарегистрировать учетную запись разработчика. В разделе [публикации toohello предложение Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) и [создать учетную запись разработчика Майкрософт](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Определение приложения
Для публикации приложений toohello Azure Marketplace осуществляются два шага.  Сначала определяется **createUiDef.json** tooindicate файл, который кластеры приложения совместим с; и затем опубликовать шаблон hello из hello портал Azure. Привет, в следующем разделе приведен пример файла createUiDef.json.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Поле | Описание | Возможные значения |
| --- | --- | --- |
| types |типы кластера Hello, совместимые с приложение hello. |Hadoop, HBase, Storm, Spark (или любое их сочетание). |
| tiers |уровни кластера Hello, совместимые с приложение hello. |"Стандартный", "Премиум" (или оба). |
| versions |Hello типы кластера HDInsight, совместимые с приложение hello. |3.4 |

## <a name="application-install-script"></a>Сценарий установки приложения
При установке приложения на кластере (существующий или новый), создается граничного узла и на нем выполняется сценарий установки приложения hello.
  > [!IMPORTANT]
  > Имя Hello имен сценария установки приложения hello должно быть уникальным для определенного кластера с hello следующая формата.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Обратите внимание, что существует имя скрипта toohello трех частей:
  > 
  > 1. Скрипт имя префикс, который должно включать в себя имя приложения hello или соответствующие toohello имя приложения.
  > 2. Дефис (-) для удобства чтения.
  > 3. Функция уникальная строка с именем приложения hello как hello параметра.
  > 
  > Пример: hello выше заканчивается становится: оттенок install-v0-4wkahss55hlas в hello сохраняются в списке действий скрипта. Пример полезных данных JSON см. здесь: [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
сценарий установки Hello необходимо иметь следующие характеристики hello.
1. Убедитесь, что скрипт hello идемпотентными. Несколько вызовов должен сформировать скрипт toohello hello того же результата.
2. сценарий Hello, должно осуществляться должным образом. Используйте другое расположение для скрипта hello при обновлении или тестирования изменений, чтобы клиенты, пытающиеся приложения hello tooinstall не затрагиваются. 
3. Добавьте сценарии toohello достаточно ведения журнала в каждой точке. Обычно hello журналы сценариев, единственным способом toodebug hello проблемы с установкой приложения.
4. Убедитесь, что вызовы tooexternal services или ресурсов достаточно попыток установки hello не страдала от временных неполадок сети.
5. Если сценарий является запуск служб на узлах hello, убедитесь, что службы hello отслеживаются и настроить toostart автоматически в случае перезагрузки узла.

## <a name="package-application"></a>Пакет приложения
Создайте ZIP-файл, который содержит все необходимые файлы для установки приложений HDInsight. Требуется hello ZIP-файл в [публикации приложения](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. См. пример из статьи [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md).
* Все необходимые скрипты.

> [!NOTE]
> Здравствуйте, файлы приложения (включая файлы веб-приложения, если есть) может располагаться на любой общедоступный конечной точки.
> 

## <a name="publish-application"></a>публикации приложения
Выполните следующие шаги toopublish HDInsight приложения hello.

1. Войдите на toohello [портал публикации Azure](https://publish.windowsazure.com/).
2. Нажмите кнопку **шаблоны решений** из левой toocreate hello шаблона решения.
3. Введите заголовок и нажмите кнопку **Создать шаблон решения**.
4. Нажмите кнопку **учетная запись центра разработки для создания и объединения hello Azure программы** tooregister вашей компании, если вы еще не сделали этого.  См. статью [Создание учетной записи разработчика Майкрософт](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Нажмите кнопку **определяют некоторые топологии tooget Started**. Шаблон решения является его топологии tooall «родительский». В одном шаблоне предложений или решения можно определить сразу несколько топологий. При передаче toostaging предложение, то при переносе со всеми топологиями. 
6. Введите имя топологии и нажмите кнопку hello "плюс".
7. Введите новую версию и нажмите кнопку "плюс" hello.
8. Отправка hello ZIP-файл, подготовленного на [упаковки приложения](#package-application).  
9. Щелкните **Request Certification**(Запросить сертификацию). Hello Microsoft сертификации рассмотрит файлы hello и сертификация hello топологии.

## <a name="next-steps"></a>Дальнейшие действия
* [Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.
* [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как toodeploy неопубликованные приложения tooHDInsight HDInsight.
* [Настроить кластеры HDInsight под управлением Linux, с помощью сценария действия](hdinsight-hadoop-customize-cluster-linux.md): Узнайте, как toouse действие сценария tooinstall дополнительные приложения.
* [Создавать кластеры под управлением Linux Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Узнайте, как кластеры toocreate шаблонов диспетчера ресурсов toocall HDInsight.
* [Используйте пустой краевым узлам в HDInsight](hdinsight-apps-use-edge-node.md): Узнайте, как toouse пустой ребро узла для доступа к кластеру HDInsight, тестирование приложений HDInsight и размещение приложений HDInsight.

