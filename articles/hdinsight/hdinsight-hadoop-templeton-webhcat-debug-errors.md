---
title: "aaaUnderstand и устранение ошибок WebHCat на HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как распространенные ошибки tooabout возвращенных WebHCat на HDInsight и как tooresolve их."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Понимание и устранение ошибок, полученных из WebHCat в HDInsight

Дополнительные сведения об ошибках, полученное при использовании WebHCat с HDInsight и о том, как tooresolve их. WebHCat используется внутренне клиентские средства, такие как Azure PowerShell и hello Озера Data Tools для Visual Studio.

## <a name="what-is-webhcat"></a>Что такое WebHCat

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) — это REST API для [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), уровень управления таблицами и хранилищем данных для Hadoop. WebHCat включена по умолчанию в кластерах HDInsight и используется заданиями toosubmit различные средства, получить состояние задания, т. д., не входя в кластере toohello.

## <a name="modifying-configuration"></a>Изменение конфигурации

> [!IMPORTANT]
> Некоторые из hello ошибок, перечисленных в этом документе возникают из-за превышения заданного максимума. При шаг разрешение hello указывается, что можно изменить значение, необходимо использовать один hello после изменения hello tooperform:

* Для **Windows** кластеров: используйте значение hello tooconfigure действие сценария во время создания кластера. Для получения дополнительных сведений обратитесь к разделу [Разработка сценариев Action Script](hdinsight-hadoop-script-actions.md).

* Для **Linux** кластеров: значение hello toomodify Ambari использования (веб- или REST API). Для получения дополнительных сведений обратитесь к разделу [Управления HDInsight с помощью Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Конфигурация по умолчанию

При превышении следующие значения по умолчанию hello можно привести к снижению производительности WebHCat или привести к ошибкам.

| Настройка | Действие | Значение по умолчанию |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |Здравствуйте, максимальное количество заданий, которые могут быть активными одновременно (ожидающие или выполняемые) |10 000 |
| [templeton.exec.max-procs][max-procs] |Максимальное число запросов, которые могут обрабатываться параллельно Hello |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |сохраняются Hello, сколько дней журнал заданий |7 дней |

## <a name="too-many-requests"></a>Слишком много запросов

**Код состояния HTTP**: 429

| Причина: | Способы устранения: |
| --- | --- |
| Вы превысили hello максимальное число параллельных запросов обслуживается WebHCat в минуту (по умолчанию 20) |Уменьшить tooensure вашей рабочей нагрузки, не отправлять больше, чем hello максимальное число одновременных запросов или увеличить hello ограничение одновременных запросов на изменение `templeton.exec.max-procs`. Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration). |

## <a name="server-unavailable"></a>Сервер недоступен

**Код состояния HTTP**: 503

| Причина: | Способы устранения: |
| --- | --- |
| Этот код состояния обычно происходит во время отработки отказа между hello первичной и вторичной головному узлу кластера hello |Подождите две минуты, а затем повторите операцию hello |

## <a name="bad-request-content-could-not-find-job"></a>Неправильный запрос содержимого: не удалось найти задание

**Код состояния HTTP**: 400

| Причина: | Способы устранения: |
| --- | --- |
| Сведения о заданиях, были очищены, журнал заданий hello очистки |срок хранения по умолчанию Hello для журнала заданий составляет 7 дней. срок хранения по умолчанию Hello может быть изменен путем изменения `mapreduce.jobhistory.max-age-ms`. Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration). |
| Задание был прекращен из-за tooa перехода на другой ресурс |Повторите попытку отправки заданий для копирования tootwo минут |
| Был использован недопустимый идентификатор задания |Проверьте правильность идентификатора задания hello |

## <a name="bad-gateway"></a>Недопустимый шлюз

**Код состояния HTTP**: 502

| Причина: | Способы устранения: |
| --- | --- |
| Внутренняя сборка мусора выполняется в hello WebHCat процесса |Дождитесь toofinish сбора мусора и перезапуск службы WebHCat hello |
| Время ожидания истекло, Ожидание ответа от службы ResourceManager hello. Эта ошибка может возникать, когда hello число активных приложений становится более hello настроен (по умолчанию 10 000) |Подождите выполняющихся заданий toocomplete или увеличить ограничение одновременных заданий hello, изменив `yarn.scheduler.capacity.maximum-applications`. Дополнительные сведения см. в разделе hello [изменение конфигурации](#modifying-configuration) раздела. |
| Попытка tooretrieve все задания через hello [GET/Jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) вызова при `Fields` задано слишком`*` |Не пытайтесь получить сведения о *всех* заданиях. Вместо этого используйте `jobid` tooretrieve сведения о заданиях, только больше определенных идентификатор задания. Или не используйте `Fields` |
| Hello службы WebHCat не работает во время отработки отказа головному узлу |Подождите 2 минуты и повторите операцию hello |
| В настоящий момент более 500 заданий, отправленных через WebHCat, находятся в режиме ожидания |Дождитесь завершения текущих заданий, находящихся в режиме ожидания, перед отправкой новых заданий |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
