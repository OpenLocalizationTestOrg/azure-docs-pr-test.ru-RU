---
title: "журналы aaaIntegrate ресурсы Azure в вашей системы SIEM | Документы Microsoft"
description: "Узнайте о службе интеграции журналов Azure, ее основных возможностях и принципах работы."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Введение tooMicrosoft интеграции Azure log
Узнайте о службе интеграции журналов Azure, ее основных возможностях и принципах работы.

## <a name="overview"></a>Обзор

Интеграция журналов Azure — это свободного решение, которое позволяет toointegrate необработанные журналы по вашим ресурсам Azure в системах tooyour локальные сведения о безопасности и управления событий (SIEM).

Служба интеграции журналов Azure собирает события из журналов средства просмотра событий Windows, [журналов действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [оповещений центра безопасности Azure](../security-center/security-center-intro.md) и [журналов диагностики Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md), которые поступают из ресурсов Azure. Такая интеграция помогает решения SIEM предоставляют унифицированную панели мониторинга для всех средств, локально или в облаке hello, так что можно собрать корреляции, анализ и предупреждения для событий безопасности.

>[!NOTE]
В настоящее время hello поддерживается только в облаках, коммерческих Azure и Azure для государственных. Другие облака не поддерживаются.

![Служба интеграции журналов Azure][1]

## <a name="what-logs-can-i-integrate"></a>Какие журналы можно интегрировать?
Azure создает подробные журналы для каждой службы Azure. Эти журналы делятся на три типа.

* **Журналы службы управления и управления** более заметными hello [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) операций CREATE, UPDATE и DELETE. К этому типу относятся, например, журналы действий Azure.
* **Журналы плоскости данных** более заметными hello событий, возникающих в рамках использования hello ресурс Azure. Пример такого рода журнала: hello средства просмотра событий Windows **системы**, **безопасности**, и **приложения** каналов в виртуальной машине. Другой пример — ведение журнала диагностики, настраиваемое с помощью Azure Monitor.
* Журнал **Обработанные событий** предоставляет информацию о проанализированных событиях и оповещениях, обработанных от вашего имени. Примером события такого типа является оповещения центра Azure безопасности, где центр безопасности Azure обработаны и проанализированы подписки tooprovide оповещения соответствующих tooyour текущего уровня безопасности.

Интеграция журналов Azure поддерживает ArcSight, QRadar и Splunk. Во всех случаях обратитесь к поставщику вашего SIEM tooassess ли они имеют собственный соединитель. В некоторых случаях не потребуется toouse интеграции Azure журнала при собственного соединители. Дополнительные сведения о поддерживаемых журнала, посетите типы hello часто задаваемые вопросы.

>[!NOTE]
Хотя интеграции журналов Azure — это бесплатные решение, есть затраты на хранилище Azure, возникающие в результате хранения сведения файлов журналов hello.

Помощь сообщества доступна через hello [форум MSDN интеграции Azure журнала](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Форум по Hello предоставляет hello AzLog сообщества hello возможность toosupport друг с другом вопросы, ответы, советы и рекомендации по как tooget hello наиболее интеграционном журналов Azure. Кроме того команды hello интеграции журналов Azure отслеживает этот форум и поможет всякий раз, когда мы можем.

Можно также отправить [запрос в службу поддержки](../azure-supportability/how-to-create-azure-support-request.md). toodo это, выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.

## <a name="next-steps"></a>Дальнейшие действия
В этом документе можно было введено tooAzure журнала интеграции. toolearn больше о Azure журнала интеграции и hello типы журналов поддерживаются, см. ниже hello:

* [Служба интеграции журналов Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=53324) — посетите Центр загрузки, чтобы получить дополнительные сведения, изучить требования к системе и получить инструкции по установке службы интеграции журналов Azure.
* [Приступая к работе со службой интеграции журналов Azure](security-azure-log-integration-get-started.md) — в этом руководстве рассматривается установка службы интеграции журналов Azure и интеграция журналов из службы хранилища Azure WAD, журналов действий Azure, оповещений центра безопасности Azure и журналов аудита Azure Active Directory.
* [Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — в этой записи блога показано, как tooconfigure Azure журнала toowork интеграция с решениями партнеров Splunk и разработанное HP, IBM QRadar. Этот блог представляет нашей текущей позиции по настройке решения партнеров hello. Во всех случаях сначала обратиться toopartner решения документацией.
* [Действия и ASC предупреждений над syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) — в этой записи блога шаги hello toosend действия и центр безопасности Azure предупреждения через tooQRadar системного журнала
* [Azure log integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) (Служба интеграции журналов Azure: часто задаваемые вопросы) — эта статья содержит ответы на часто задаваемые вопросы об интеграции журналов Azure.
* [Интеграция центра обеспечения безопасности интеграции журнала предупреждений с помощью Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) — в этом документе показано, как центр безопасности Azure toosync предупреждения с интеграцией журналов Azure.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
