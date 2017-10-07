---
title: "aaaMonitoring и отвечает tooSecurity оповещения в Operations Management Suite безопасности и аудита решения | Документы Microsoft"
description: "Этот документ поможет вам toouse hello угроз аналитики параметр, доступный в OMS безопасности и аудита toomonitor и реагировать toosecurity предупреждения."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Наблюдение и обработка toosecurity оповещения в Operations Management Suite безопасности и аудита решения
Этот документ поможет вам используйте параметр аналитики угроз hello, доступные в OMS безопасности и аудита toomonitor и отвечать toosecurity предупреждения.

## <a name="what-is-oms"></a>Что такое OMS?
Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее. Дополнительные сведения об OMS, прочитайте статью hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Анализ угроз
В среде предприятия, где пользователи сети toohello широкий доступ и использовать различные устройства tooconnect toocorporate данные крайне важно можно активно отслеживать ресурсы и быстро отреагировать toosecurity инцидентов. Это конкретного, важные с точки зрения hello безопасности жизненного цикла, так как некоторые кибербезопасности, угроз не могут вызвать предупреждения или подозрительных действий, которые могут быть идентифицированы техническими средствами традиционных безопасности. 

С помощью hello **анализ угроз** параметр доступные в OMS безопасность и аудит, ИТ-администраторы можно идентифицировать угроз безопасности hello среде, например, определить, если определенный компьютер является частью [ ботнет](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Компьютеры может стать узлов в ботнет, когда злоумышленник незаконно установки вредоносных программ, которые тайно подключается этой команды toohello компьютера и управления. Также с его помощью можно выявить потенциальные угрозы, поступающие по нелегальным каналам связи, таким как [даркнет](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

В порядке toobuild этот анализ угроз, OMS безопасность и аудит использовать данные поступают из нескольких источников в Microsoft. OMS безопасность и аудит будет использовать этот данных tooidentify потенциальных угроз в вашей среде.

Hello области аналитики угроз состоит по три основных варианта:

* Серверы с вредоносным исходящим трафиком
* Типы обнаруженных угроз
* Карта анализа угроз

> [!NOTE]
> Обзор этих разделов см. в статье [Приступая к работе с решением "Безопасность и аудит" Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Отвечать на запросы toosecurity оповещения
Один из шагов hello [нарушениях безопасности](https://technet.microsoft.com/library/cc512623.aspx) процесс — серьезность hello tooidentify hello под угрозу безопасность системы. На этом этапе необходимо выполнить следующие задачи hello:

* Определить характер hello атаки hello
* Определить hello атаки происхождения
* Определите назначение hello hello атаки. Hello атаки, в частности, направленных на определенные сведения об организации tooacquire или ее случайного?
* Определять под сомнение системах hello
* Определить hello файлы, которые были прочитаны и определить чувствительность hello этих файлов

Можно использовать **анализ угроз** сведения в OMS безопасность и аудит toohelp решения этих задач. Выполните шаги hello ниже tooaccess это **анализ угроз** параметры:

1. В hello **Microsoft Operations Management Suite** основной панели мониторинга щелкните **безопасность и аудит** плитки.
   
    ![Безопасность и аудит](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. В hello **безопасность и аудит** панели мониторинга, вы увидите hello **анализ угроз** параметры в правом hello, как показано ниже:
   
    ![Анализ угроз](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Эти три плитки позволит получить общие сведения о текущем угроз hello. В hello **сервера с исходящим вредоносным трафиком** можно будет tooidentify при наличии любого компьютера, которое вы наблюдаете (внутри или за пределами вашей сети), отправляющего toohello вредоносного трафика Интернета. 

Hello **обнаружил угроз** плитки отображается сводка hello угроз, которые являются текущими в состоянии «hello подстановки», если щелкнуть эту плитку находятся дополнительные сведения об этих угроз как показано на следующем рисунке:

![Типы обнаруженных угроз](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

Щелкнув угрозу, можно получить дополнительные сведения о ней. пример Hello представлены дополнительные сведения об Ботнет:

![Дополнительные сведения об угрозе](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Как описано в начале этого раздела hello, эти сведения могут быть очень полезны при ветвь реагирования на события. Он также может быть важные во время криминальных расследований, которых требуется источника hello toofind hello атак, какая система была скомпрометирована и hello временной шкалы. В этом отчете, можно легко определить некоторые основные сведения о hello атак, например: hello источника атаки hello, hello локального IP-адреса, был скомпрометирован и hello текущим состоянием сеанса подключения hello. 

Hello **карты аналитики угроз** поможет tooidentify hello текущего расположения земного шара hello, имеющих вредоносного трафика. Существует (входящий) оранжевый и красный (исходящих) со стрелками в этой карте определяющие направление трафика hello, если щелкнуть одну из этих кнопок со стрелками, она будет отображаться hello тип угрозы и hello направление трафика, как показано ниже:

![Карта анализа угроз](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Можно просмотреть демонстрацию на порядок toouse этой возможности во время реагирования на события обработки, просмотра презентации hello [борьбы с угрозами безопасности центра обработки данных с помощью интерактивной анализ, с помощью Operations Management Suite](https://myignite.microsoft.com/videos/5000) доставлено на Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Отвечать на запросы toodistinct вредоносные IP-адреса доступ
В некоторых случаях можно заметить потенциально вредоносные IP-адреса, поступившие с одного отслеживаемого компьютера:

![Карта анализа угроз](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Это предупреждение и других в hello одной категории, создаются через систему безопасности OMS за счет использования [анализ угроз Microsoft](https://youtu.be/O4WtxgUrDc8). Hello данных аналитики угроз является собираемым корпорацией Майкрософт, а также приобрести от ведущих поставщиков аналитики угроз. Эти данные часто обновляется и адаптировать перемещение toofast угроз. Из-за характера tooits, его следует использовать в сочетании с другими источниками информации о безопасности при [исследование](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) предупреждение системы безопасности. 

## <a name="customize-alerts-received-via-e-mail"></a>Настройка оповещений, получаемых по электронной почте

Вы можете указать, кто из пользователей будет получать оповещения при активации предупреждений безопасности компонентом безопасности OMS. Этот параметр доступен в разделе Обзор / Здравствуйте, параметры на панели мониторинга OMS:

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>См. также
В этом документе вы узнали, каким образом toouse hello **анализ угроз** параметр в OMS безопасность и аудит оповещения toosecurity toorespond решения. toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.

* [Общие сведения об Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Приступая к работе с решением "Безопасность и аудит" Operations Management Suite](oms-security-getting-started.md)
* [Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite](oms-security-monitoring-resources.md)

