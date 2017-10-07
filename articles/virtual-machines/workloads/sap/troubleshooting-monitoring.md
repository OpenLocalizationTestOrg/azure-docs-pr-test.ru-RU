---
title: "aaaTroubleshooting и мониторинга для SAP HANA в Azure (большие экземпляры) | Документы Microsoft"
description: "Сведения об устранении неполадок и мониторинге архитектуры решения \"SAP HANA в Azure (крупные экземпляры)\"."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Как tootroubleshoot и мониторинга SAP HANA (крупных экземпляров) в Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Мониторинг архитектуры SAP HANA в Azure (крупные экземпляры)

SAP HANA в Azure (большие экземпляры) ничем не отличается от любое другое развертывание IaaS — необходимо toomonitor что hello ОС и приложения hello — это и как их использовать hello следующие ресурсы:

- ЦП
- Память
- пропускная способность сети;
- Дисковое пространство

Виртуальные машины Azure должен toofigure перечисленных выше классов ресурсов hello достаточны или ли получить эти исчерпаны. Вот более подробно на каждом из различных классов hello.

**Потребление ресурсов ЦП:** hello отношение, которое определено SAP для определенных рабочую нагрузку для HANA — принудительно toomake обязательно должен иметь достаточно ЦП ресурсы доступны toowork через hello данные, хранящиеся в памяти. Тем не менее может возникнуть ситуация, где HANA выполняется дольше ЦП на выполнение запросов из-за toomissing индексы или аналогичные проблемы. Это означает, что необходимо отслеживать потребление ресурсов ЦП hello HANA большом экземпляре единицы, а также ресурсов ЦП, потребляемых hello конкретными службами HANA.

**Потребление памяти:** является важным toomonitor из в HANA, а также за пределами HANA на устройстве hello. В пределах HANA отслеживать как hello данных занимает место в выделенной памяти в toostay порядке в пределах hello необходимые размеры руководством по SAP HANA. Также можно toomonitor потребление памяти на hello большом экземпляре уровня toomake том, что дополнительные установленные не HANA программного обеспечения не потребляют слишком много памяти и таким образом конкурируют HANA памяти.

**Пропускная способность сети:** hello шлюза виртуальной сети Azure имеет ограничения по пропускной способности данных, перемещение в hello виртуальной сети Azure, так бывает полезно toomonitor hello данных, полученных всеми hello Azure виртуальные машины в виртуальной сети toofigure, насколько близко являются ограничения toohello hello Azure номер SKU, выбранных для шлюза. На устройстве HANA большом экземпляре hello он делает смысле toomonitor входящий и исходящий сетевой трафик также и отслеживания tookeep hello томов, которые выполняются со временем.

**Дисковое пространство.** Потребление дискового пространства обычно увеличивается с течением времени. Это происходит по многим причинам, самые распространенные из которых — увеличение объема данных, создание резервных копий журнала транзакций, хранение файлов трассировки и выполнение моментальных снимков хранилища. Таким образом является важным toomonitor использования места на диске и управлять дисковым пространством hello, связанный с единицей большом экземпляре HANA hello.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Мониторинг и устранение неполадок со стороны HANA

В порядке tooeffectively Анализ проблем связанных tooSAP HANA в Azure (большие экземпляры), очень полезно toonarrow вниз hello основную причину проблемы. SAP опубликовала большой объем документации toohelp вы.

Применимые производительности HANA связанные tooSAP часто задаваемые вопросы можно найти в hello следующие примечания по SAP:

- [SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Примечание SAP № 2222200. Часто задаваемые вопросы: сеть SAP HANA)
- [SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Примечание SAP № 2100040. Часто задаваемые вопросы: ЦП SAP HANA)
- [SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 199997. Часто задаваемые вопросы: память SAP HANA)
- [SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Примечание SAP № 200000. Часто задаваемые вопросы: оптимизация производительности SAP HANA)
- [SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Примечание SAP № 199930. Часто задаваемые вопросы: анализ операций ввода-вывода SAP HANA)
- [SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 2177064. Часто задаваемые вопросы: перезапуск и сбои службы SAP HANA)

**Оповещения SAP HANA**

В качестве первого шага в журнале hello текущего SAP HANA предупреждения. В SAP HANA Studio перейдите слишком**консоли администрирования: предупреждений: Показать: все предупреждения**. На этой вкладке будет показывать все предупреждения SAP HANA для конкретных значений (Свободная физическая память, ЦП, т. д.), которые выходят за пределы hello задать минимальное и максимальное пороговых значений. По умолчанию проверки автоматически обновляются каждые 15 минут.

![В SAP HANA Studio перейдите tooAdministration консоли: предупреждений: Показать: все оповещения](./media/troubleshooting-monitoring/image1-show-alerts.png)

**ЦП**

Для запуска из-за tooimproper порогового значения предупреждения разрешение является значение по умолчанию toohello tooreset или более рационального пороговое значение.

![Значение по умолчанию toohello сброса или более рационального пороговое значение](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Hello следующие оповещения могут указывать на проблемы ресурсов ЦП:

- использование ЦП узла (оповещение 5);
- последняя операция точки сохранения (оповещение 28);
- длительность точки сохранения (оповещение 54).

Вы можете заметить высокую нагрузку на ЦП на базе данных SAP HANA из одного из следующих hello:

- для текущего использования ЦП или использования ЦП в прошлом возникает оповещение 5 (использование ЦП узла);
- Hello ЦП отображаются на экране приветствия Обзор

![На экране приветствия Обзор отображается ЦП](./media/troubleshooting-monitoring/image3-cpu-usage.png)

График нагрузки Hello могут отображаться высокую нагрузку на ЦП, или высокий уровень потребления в hello за последние:

![граф нагрузки Hello может показывать высокий уровень загруженности ЦП или высокий уровень потребления hello за последние](./media/troubleshooting-monitoring/image4-load-graph.png)

Запускается из-за использования ЦП toohigh предупреждение может быть вызвано по нескольким причинам, включая, но не ограничиваясь: выполнения определенных операций, загрузку данных, зависание заданий, долго выполняющихся инструкций SQL и производительности неправильный запрос (например, с помощью BW на HANA кубы).

См. toohello [SAP HANA Устранение неполадок: вызывает, связанных с ЦП и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) сайта подробные шаги по устранению неполадок.

**Операционная система**

Одним из наиболее важных hello проверяет для SAP HANA в Linux — toomake, что, отключены прозрачный огромный страниц см. в разделе [&#2131662; Примечание SAP — прозрачный огромный страниц (THP) на серверах SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Можно проверить, разрешены ли прозрачный огромный страницы через следующую команду Linux hello: **классификатором /sys/kernel/mm/transparent\_hugepage или не включен**
- Если _всегда_ заключается в квадратные скобки, как показано ниже, означает, включить hello прозрачный огромный страниц: [всегда] madvise никогда не; Если _никогда не_ заключено в квадратные скобки, как показано ниже, это означает, что hello прозрачный Огромный страницы отключены: всегда madvise [никогда не]

Hello следующую команду Linux должен возвращать ничего: **rpm - qa | grep ulimit.** Если _ulimit_ установлено, удалите его немедленно.

**Память**

Можно заметить, что сумма hello памяти, выделенной с помощью hello SAP HANA базы данных больше, чем ожидалось. Hello следующие оповещения указывают на проблемы с большим объемом памяти использования:

- использование физической памяти узла (оповещение 1);
- использование памяти сервера доменных имен (оповещение 12);
- общее использование памяти таблиц хранилища столбцов (оповещение 40);
- использование памяти служб (оповещение 43);
- использование памяти основного хранилища таблиц хранилища столбцов (оповещение 45);
- файлы дампа среды выполнения (оповещение 46).

См. toohello [SAP HANA Устранение неполадок: проблем с памятью](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) сайта подробные шаги по устранению неполадок.

**Сеть**

См. слишком[&#2081065; Примечание SAP — Устранение неполадок сети SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) и выполнять процедуры устранения неполадок в этой заметке SAP hello сети.

1. Анализ времени кругового пути между сервером и клиентом.
  О. Запустить сценарий SQL hello [ _HANA\_сети\_клиенты_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Выполните анализ обмена данными между узлами.
  О. Запустите скрипт SQL [ _HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Выполните команду Linux **ifconfig** (hello вывода показывает, если выполняются какие-либо потери пакетов).
4. Выполните команду Linux **tcpdump**.

Кроме того, используйте Привет открыть источник [IPERF](https://iperf.fr/) средства (или схожий) toomeasure реальной сети производительности приложения.

Ссылки toohello [Устранение SAP HANA: производительность сети и проблем с подключением к](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) сайта подробные шаги по устранению неполадок.

**Хранилище**

С точки зрения конечного пользователя приложения (или hello системе в целом) работает медленно, не отвечает или даже может показаться toohang при возникновении проблем с производительностью ввода-вывода. В hello **тома** вкладку в SAP HANA Studio, вы увидите hello присоединенного тома и какие томов используются каждой службы.

![Hello вкладке тома в SAP HANA Studio можно увидеть hello присоединенного тома, а также какие тома используются всеми службами](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Подключенные к нему тома в нижней части экрана приветствия, на котором вы увидите подробные сведения о hello hello тома, такие как файлы и статистику ввода-вывода.

![Подключенные к нему тома в нижней части экрана приветствия, на котором вы увидите подробные сведения о hello hello тома, такие как файлы и статистику ввода-вывода](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

См. toohello [SAP HANA Устранение неполадок: операций ввода-вывода связанных основные причины и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) и [SAP HANA Устранение неполадок: диск связанных основные причины и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) сайта подробные шаги по устранению неполадок.

**Средства диагностики**

Выполните проверку работоспособности SAP HANA с помощью HANA\_Configuration\_Minichecks. Это средство возвращает потенциальные критические технические проблемы, которые должны вызвать оповещения в SAP HANA Studio.

См. слишком[&#1969700; Примечание SAP — коллекцию инструкций SQL для SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) и загрузите файл вложенного toothat hello SQL Statements.zip Примечание. Сохраните этот ZIP-файл на локальный жесткий диск hello.

В Studio SAP HANA в hello **сведения о системе** щелкните правой кнопкой мыши в hello **имя** столбца и выберите команду **импорта инструкции SQL**.

![В Studio SAP HANA, на вкладке hello системные сведения щелкните правой кнопкой мыши имя столбца hello и импорта инструкции SQL select](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Файл SQL Statements.zip SELECT hello хранится локально, а папка с hello соответствующих инструкций SQL, которые будут импортированы. На этом этапе приветствия эти инструкции SQL могут выполняться много разных проверок диагностики.

Например, требования к пропускной способности tootest репликации системы SAP HANA, щелкните правой кнопкой мыши hello **пропускной способности** инструкции в разделе **репликации: пропускной способности** и выберите **откройте** в консоли SQL.

полную инструкцию SQL Hello открывает допускающему toobe входные параметры (раздел "изменения") изменен, а затем запускается.

![Разрешает toobe входные параметры (раздел "изменения") изменен, а затем запускается открывает Hello полную инструкцию SQL](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Еще один пример — щелкните правой кнопкой мыши на hello инструкции в разделе **репликации: Обзор**. Выберите **Execute** hello контекстном меню:

![Еще один пример — щелкните правой кнопкой мыши в инструкциях hello в группе репликации: Обзор. Выберите из контекстного меню hello Execute](./media/troubleshooting-monitoring/image9-import-statements-c.png)

После этого отобразятся сведения, которые помогут в устранении неполадок.

![После этого отобразятся сведения, которые помогут в устранении неполадок](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Здравствуйте, одинаково для HANA\_конфигурации\_Minichecks и установите флажок для любого _X_ метки в hello _C_ столбца (критический).

Пример выходных данных

**HANA\_Configuration\_MiniChecks\_Rev102.01 + 1** для общих проверок SAP HANA.

![HANA\_Configuration\_MiniChecks\_Rev102.01 + 1 для общих проверок SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview** для получения общих сведений о том, какие службы SAP HANA запущены в данный момент.

![HANA\_Services\_Overview для получения общих сведений о том, какие службы SAP HANA запущены в данный момент](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics** для получения сведений о службе SAP HANA (ЦП, память и т. д.).

![HANA\_Services\_Statistics для получения сведений о службе SAP HANA ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_конфигурации\_Обзор\_Rev110 +** Общие сведения об экземпляре SAP HANA hello.

![HANA\_конфигурации\_Обзор\_Rev110 + Общие сведения об экземпляре SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_конфигурации\_параметры\_Rev70 +** toocheck параметров SAP HANA.

![HANA\_конфигурации\_параметры\_Rev70 + toocheck параметров SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

