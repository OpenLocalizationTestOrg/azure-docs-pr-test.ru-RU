---
title: "решения по управлению Azure Log Analytics aaaAdd | Документы Microsoft"
description: "Решения для управления Operations Management Suite (OMS) и Log Analytics представляют собой коллекцию логики, визуализации и правил получения данных, предоставляющую метрики, связанные с определенной проблемной областью."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Добавление рабочей tooyour анализа журналов Azure управление решениями

Решения для управления Log Analytics представляют собой коллекцию **логики**, **визуализации** и **правил получения данных**, предоставляющую метрики, связанные с определенной проблемной областью. В этой статье перечислены поддерживаемые анализа журналов решения для управления и показано, как tooadd и remove для рабочей области с помощью hello портал Azure. Можно также добавить решения на портале OMS hello, с помощью коллекции решений hello.

Решения для управления позволяют получить более подробные данные для:

* изучения и более быстрого решения проблем с работоспособностью;
* сбора и сопоставления различных типов машинных данных;
* Помочь заблаговременно решать, которые предоставляет решение hello.

> [!NOTE]
> Служба аналитики журналов включает функции поиска журналов, вам требуется tooinstall tooenable решение управления его. Тем не менее вы получаете визуализации данных, предлагаемые запросы поиска и аналитики путем добавления рабочей tooyour решений управления.

В этой статье вы добавить управления решения tooa рабочей области с помощью портала Azure Marketplace hello. После добавления решения данные собираются с серверов hello в инфраструктуре и отправляются toohello службой OMS. Обработка по приветствия службой OMS обычно занимает несколько минут tooan час. После hello служба обрабатывает данные hello, его можно просмотреть в OMS.

Если решение для управления больше не нужно, его можно удалить. При удалении решение управления, его данные не отправляются tooOMS. Если вы находитесь на бесплатной ценовой категории hello, удаление решения может снизить hello количества данных, помогая расти дневной квоты данных.

## <a name="view-available-management-solutions"></a>Просмотр доступных решений для управления

Hello Azure marketplace содержит список hello [решений по управлению для анализа журналов](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Решения для управления можно установить из Azure marketplace, щелкнув hello **компания** ссылку внизу hello каждого решения.

## <a name="add-a-management-solution"></a>Добавление решения для управления
1. Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com) с помощью вашей подписки Azure.
2. В hello **New** колонке под **Marketplace**выберите **мониторинг + управления**.
3. В hello **мониторинг + управления** колонка, щелкните **все**.  
    ![Колонка "Мониторинг и управление"](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello справа от **решения для управления**, нажмите кнопку **дополнительные**.
5. В hello **решений по управлению** колонке выберите решение управления, что требуется tooadd tooa область.  
    ![Колонка "Мониторинг и управление"](./media/log-analytics-add-solutions/management-solutions.png)  
6. В колонке решение управления hello, просмотрите сведения о решении по управлению hello и нажмите кнопку **создать**.
7. В hello *имя решения управления* колонке выберите рабочей области, что tooassociate решение для управления hello.
8. При необходимости измените параметры рабочей области для hello подписки Azure, группу ресурсов и расположение. Можно также выбрать **параметры службы автоматизации**. Щелкните **Создать**.  
    ![Рабочая область решения](./media/log-analytics-add-solutions/solution-workspace.png)  
9. с помощью решения по управлению hello, которые были добавлены рабочей tooyour toostart перехода слишком**анализа журналов** > **подписки** > ***имя рабочей области ***  >  **Обзор**. Появится новый элемент для вашего решения для управления. Щелкните tooopen плитки приветствия, ее и приступить к использованию решение hello после сбора данных для решения hello.

## <a name="remove-a-management-solution"></a>Удаление решения для управления

1. В hello [портал Azure](https://portal.azure.com), перейдите в слишком**анализа журналов** > **подписки** > ***имя рабочей области*** затем в hello ***имя рабочей области*** колонке нажмите кнопку **решения**.
2. В списке hello решений по управлению выберите нужных tooremove решения hello.
3. В колонке hello решения для рабочей области, щелкните **удалить**.  
    ![Удаление решения](./media/log-analytics-add-solutions/solution-delete.png)  
4. В диалоговом окне подтверждения hello, нажмите кнопку **Да**.

## <a name="offers-and-pricing-tiers"></a>Предложения и ценовые категории

Hello в следующей таблице определяет, какие решения управления принадлежит предложение tooeach Operations Management Suite.
Hello таблице также указаны hello ценовым категориям, доступные для каждого решения по управлению.
Все решения в следующей таблице hello доступны из hello Azure портал и hello коллекции решений на портале службы анализа журналов hello.

| Решение для управления                                                                       | ПРЕДЛОЖЕНИЕ                                                                     | Ценовые категории<sup>1</sup>                                                 | Примечания |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Анализ журнала действий](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | 90 дней данные доступны бесплатно.<br>Данные не регулируется cap toohello уровень Free |
| [Оценка AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Состояние репликации AD](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Недоступно tooadd из Azure portal или marketplace. |
| [Работоспособность агентов](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Данные не регулируется cap toohello уровень Free<br> Недоступно tooadd из Azure portal или marketplace. |
| [Управление оповещениями](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Недоступно tooadd из Azure portal или marketplace. |
| [Соединитель Application Insights (предварительная версия)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Гибридная рабочая роль службы автоматизации](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation and Control</li></ul>                                  | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации |
| [Анализ шлюзов приложений Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Анализ групп безопасности сети Azure](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Службы анализа SQL Azure (предварительная версия)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br>На&nbsp;узел&nbsp;(OMS)                                                                          | Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации|
| [Аналитика веб-приложений Azure](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
|[Архивация](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Анализ и аналитика</li></ul>                                   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)                                                                       | Требуется классическое резервное хранилище.<br> Недоступно tooadd из Azure portal или marketplace. |
| [Емкость и производительность (предварительная версия)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Отслеживание изменений](log-analytics-change-tracking.md)                                       | <ul><li>Automation and Control</li></ul>                                  | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации |
| [Контейнеры](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Соединитель управления ИТ-службами (предварительная версия)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> На&nbsp;узел&nbsp;(OMS)     | |
| HDInsight HBase Monitoring <br>(предварительная версия)                                                  | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Анализ хранилища ключей](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Недоступно tooadd из Azure portal или marketplace. |
| [Оценка вредоносных программ](log-analytics-malware.md)                                            | <ul><li>Служба "Безопасность и соответствие требованиям"</li></ul>                                 | Free<br> Автономный<br>На&nbsp;узел&nbsp;(OMS)                                                                           | При добавлении решения безопасности и соответствия требованиям hello после 19 июня 2017 г. [выставление счетов осуществляется на каждом узле](https://azure.microsoft.com/pricing/details/security-compliance/)независимо от того, рабочую область hello ценовой категории. Hello первых 60 дней свободны.  |
| [Монитор производительности сети](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Анализ и аналитика</li></ul>                                   | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | |
| [Аналитика Office 365 (предварительная версия)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Безопасность и аудит](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Security&nbsp;and&nbsp;Compliance</li></ul>                       | Free<br> Автономный<br>На&nbsp;узел&nbsp;(OMS)                                                                           | Это решения нужно для сбора журналов событий безопасности.<br>При добавлении решения безопасности и соответствия требованиям hello после 19 июня 2017 г. [выставление счетов осуществляется на каждом узле](https://azure.microsoft.com/pricing/details/security-compliance/)независимо от того, рабочую область hello ценовой категории. Hello первых 60 дней свободны. |
| [Анализ Service Fabric (предварительная версия)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Сопоставление служб (предварительная версия)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Анализ и аналитика</li></ul>                      | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Доступно в восточной части США, Западной Европе и западно-центральной части США.    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Анализ и аналитика</li></ul>                                   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)                                                                       | Требуется классическое хранилище Site Recovery.<br> Недоступно tooadd из Azure portal или marketplace. |
| [Оценка SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| Запуск и остановка виртуальных машин в нерабочее время<br>(предварительная версия)                                              | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Недоступно tooadd из Azure portal или marketplace. |
| [Оценка System Center Operations Manager (предварительная версия)](log-analytics-scom-assessment.md)  | <ul><li>Анализ и аналитика</li><li>Служба Log Analytics</li></ul>        | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Управление обновлениями](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation and Control</li></ul>                                  | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации |
| [Поддержка обновлений (предварительная версия)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Плата за данные или узлы не взимается.<br>Данные не субъекта toohello уровень Free крепления.<br> Недоступно tooadd из Azure portal или marketplace. |
| [Готовность к обновлению](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | Плата за данные или узлы не взимается.<br>Данные не субъекта toohello уровень Free крепления.<br> Недоступно tooadd из Azure portal или marketplace. |
| [Мониторинг VMware (предварительная версия)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> Стандартная<br> Премиум&nbsp;(OMS)<br> На&nbsp;ГБ&nbsp;(изолированное решение)<br> На&nbsp;узел&nbsp;(OMS)   | |
| [Wire Data 2.0 (предварительная версия)](log-analytics-wire-data.md)                                                                 | <ul><li>Анализ и аналитика</li></ul>                                   | Free<br> На&nbsp;узел&nbsp;(OMS)                                                                         | Доступно в восточной части США, Западной Европе и западно-центральной части США. |

<sup>1</sup> hello *Стандартная* и *Premium (OMS)* ценовые категории доступны только для пользователей, создавших предыдущих tooSeptember каталога рабочей их анализа журналов 21, 2016.

### <a name="community-provided-management-solutions"></a>Решения для управления от сообщества

Предоставленный сообщества решения доступны из hello [коллекции шаблонов Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) и прямой от авторов hello.

| Решение для управления               | ПРЕДЛОЖЕНИЕ                                                                     | Ценовые категории                         | Примечания |
| ---                               | ---                                                                       | ---                                   | ---   |
| Все решения от сообщества  | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Служба Log Analytics</li></ul>   | Free<br> На&nbsp;узел&nbsp;(OMS)     |   Требует вашего анализа журналов tooan toobe связанные рабочей учетной записи автоматизации |




## <a name="data-collection-details"></a>Сведения о сборе данных
Hello следующих таблицах приведены методы сбора данных и другие сведения о сборе данных для анализа журналов управления решения и источников данных. Hello таблиц разбиты на категории по решения предложений, которые соответствуют слишком[подписки ценовым категориям](https://go.microsoft.com/fwlink/?linkid=827926). Hello решения для анализа журналов действий — доступные tooall ценовым категориям бесплатно.

Здравствуйте, агент Windows аналитика журналов и hello System Center Operations Manager агент в основном являются одинаковыми. Агент Windows Hello включает дополнительные функциональные возможности tooallow его tooconnect toohello OMS рабочей области и маршрут, используя учетную запись-посредник. Если вы используете агент Operations Manager, должно быть целью как toocommunicate агента OMS с OMS. Агенты Operations Manager в этой таблице, агенты OMS, которые являются подключенных tooOperations диспетчера. В разделе [tooLog подключение Operations Manager Analytics](log-analytics-om-agents.md) сведения о подключении к существующей среде tooOMS Operations Manager.

> [!NOTE]
> Hello тип агента, используемого определяет способ отправки данных tooOMS, с hello следующие условия:
> - Можно использовать агент Windows hello или агента OMS, подключенных к Operations Manager.
> - При необходимости Operations Manager данные агента Operations Manager для решения hello всегда отправляется с помощью группы управления Operations Manager hello tooOMS. Кроме того при необходимости Operations Manager решением hello используется только агент Operations Manager hello.
> - Если Operations Manager не является обязательным и hello таблице показано, что данные агента Operations Manager отправляется tooOMS, с помощью hello группы управления, а затем данные агента Operations Manager всегда отправляется tooOMS, с помощью групп управления. Агенты Windows обхода группы управления hello и отправки данных по tooOMS напрямую.
> - Когда данные агента Operations Manager не отправляется с использованием группы управления, затем hello данные отправляются напрямую tooOMS — обход hello группы управления.

### <a name="insight--analytics--log-analytics"></a>Insight and Analytics и Log Analytics

| Решение для управления | Платформа | Microsoft Monitoring Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Анализ журнала действий | Таблицы Azure |   |   |   |   |   | при уведомлении |
| Оценка AD |Windows |&#8226; |&#8226; |  |  |&#8226; |7 дней |
| Состояние репликации AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 дней |
| Работоспособность агента | Windows и Linux | &#8226; | &#8226; |   |   | &#8226; | 1 минута |
| Управление оповещениями (Nagios) |Linux |&#8226; |  |  |  |  |при получении |
| Управление оповещениями (Zabbix) |Linux |&#8226; |  |  |  |  |1 минута |
| Управление оповещениями (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 минуты |
| Соединитель Application Insights (предварительная версия) | Таблицы Azure |   |   |   |   |   | при уведомлении |
| Анализ шлюзов приложений Azure | Таблицы Azure |   |   |   |   |   | при уведомлении |
| Анализ групп безопасности сети Azure | Таблицы Azure |   |   |   |   |   | при уведомлении |
| Службы анализа SQL Azure (предварительная версия) |Windows |  |  |  |  |  | 10 минут |
| Управление емкостью; |Windows |&#8226; |&#8226; |  |  |&#8226; |при получении |
| Контейнеры | Windows и Linux | &#8226; | &#8226; |   |   |   | 3 минуты |
| анализ хранилища ключей. |Windows |  |  |  |  |  |при уведомлении |
| Монитор производительности сети | Windows | &#8226; | &#8226; |   |   |   | Подтверждения TCP выполняются каждые 5 секунд, данные отправляются каждые 3 минуты |
| Office 365 Analytics (предварительная версия) |Windows |  |  |  |  |  |при уведомлении |
| Анализ Service Fabric |Windows |  |  |&#8226; |  |  |5 мин |
| Схема услуги | Windows и Linux | &#8226; | &#8226; |   |   |   | 15 секунд |
| Оценка SQL |Windows |&#8226; |&#8226; |  |  |&#8226; |7 дней |
| SurfaceHub |Windows |&#8226; |  |  |  |  |при получении |
| Оценка System Center Operations Manager (предварительная версия) | Windows | &#8226; | &#8226; |   |   | &#8226; | 7 дней |
| Анализ обновлений (предварительная версия) | Windows | &#8226; |   |   |   |   | 2 дня |
| Мониторинг VMware (предварительная версия) | Linux | &#8226; |   |   |   |   | 3 минуты |
| Проводные данные |Windows (2012 R2/8.1 или более поздней версии) |&#8226; |&#8226; |  |  |  | 1 минута |


### <a name="automation--control"></a>Автоматизация и контроль

| Решение для управления | Платформа | Microsoft Monitoring Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Гибридная рабочая роль службы автоматизации | Windows | &#8226; | &#8226; |   |   |   | Недоступно |
| Отслеживание изменений |Windows |&#8226; |&#8226; |  |  |&#8226; |ежечасно |
| Отслеживание изменений |Linux |&#8226; |  |  |  |  |ежечасно |
| управление обновлениями; | Windows |&#8226; |&#8226; |  |  |&#8226; |не меньше 2 раз в день и через 15 минут после установки обновления |

### <a name="security--compliance"></a>Безопасность и соответствие требованиям

| Решение для управления | Платформа | Microsoft Monitoring Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Оценка защиты от вредоносных программ |Windows |&#8226; |&#8226; |  |  |&#8226; |ежечасно |
| Безопасность и аудит <sup>1</sup> | Windows и Linux | Частично | Частично | Частично |   | Частично | Различная |

<sup>1</sup> hello безопасности и аудита решения могут собирать журналы из агентов Windows, Operations Manager и Linux. Сведения о сборе данных приведены в разделе [Источники данных](#data-sources).

- syslog
- Журналы событий безопасности Windows
- Журналы брандмауэра Windows
- Журналы событий Windows



### <a name="protection--recovery"></a>Защита и восстановление

| Решение для управления | Платформа | Microsoft Monitoring Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Архивация | Таблицы Azure |   |   |   |   |   | Недоступно |
| Azure Site Recovery | Таблицы Azure |   |   |   |   |   | Недоступно |


### <a name="data-sources"></a>Источники данных


| Источник данных | Платформа | Microsoft Monitoring Agent | Агент Operations Manager | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| журналы действий Azure; |Windows |  |  |  |  |  |при уведомлении |
| Журналы диагностики Azure |Windows |  |  |  |  |  |при уведомлении |
| Диагностические метрики Azure |Windows |  |  |  |  |  |при уведомлении |
| Трассировка событий Windows |Windows |  |  |&#8226; |  |  |5 мин |
| Журналы IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 мин |
| Счетчики производительности |Windows |&#8226; |&#8226; |  |  |  |по расписанию, не менее 10 секунд |
| Счетчики производительности |Linux |&#8226; |  |  |  |  |по расписанию, не менее 10 секунд |
| syslog |Linux |&#8226; |  |  |  |  |Из хранилища Azure — 10 минут, из агента — при получении |
| Журналы событий безопасности Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |для хранилища Azure: 10 мин; для hello агента: по поступлении |
| Журналы брандмауэра Windows |Windows |&#8226; |&#8226; |  |  |  |при получении |
| Журналы событий Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |для хранилища Azure: 10 мин; для hello агента: по поступлении |



## <a name="preview-management-solutions-and-features"></a>Предварительные версии решений для управления и компонентов
Запуск службы и devops методы, не могут toopartner с клиентов toodevelop компонентов и решений.

Во время получения личной предварительной версии мы предоставить небольшой группы клиенты доступа tooan раннее реализация hello компоненты или решения toogain обратной связи и вносить улучшения. Ранняя реализация включает минимум функций и операционных возможностей.

Наша цель — вещей tootry быстро, чтобы мы могли найти, что работает и что не работает. Мы итерацию этот процесс, пока hello отзывов пользователей hello личной предварительной версии сообщает, что все готово для общедоступной предварительной версии.

Во время hello общедоступной предварительной версии мы освободить hello компоненты или решения для всех пользователей tooget дополнительные отзывы и проверить наши масштабирование и эффективность. На этом этапе

* Функции предварительной версии отображаются на вкладке Параметры hello и можно включить любой пользователь.
* Предварительная версия решения добавляются через hello коллекции или с помощью скрипта.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Что нужно знать о предварительных версиях компонентов и решений?
Мы сообщаем о новых функциях и решения для управления, и мы рады, что работа с toodevelop вы их.

Предварительные версии компонентов и решений подходят не для всех. Перед запросом toojoin личной предварительной версии или включение общедоступной предварительной версии, убедитесь, что работаете ОК то, что находится в стадии разработки.

При включении функцию предварительного просмотра через портал hello, появится предупреждение о том, что hello компонент находится в предварительной версии.

#### <a name="for-both-private-and-public-preview"></a>Для *закрытых* и *общедоступных* предварительных версий
Hello следующая информация применима tooboth открытых и закрытых предварительного просмотра:

* Они могут работать некорректно.
  * Выдает диапазона не дополнительный недовольство через toosomething не работает во всех.
* Рекомендуется ограничить toohave preview hello отрицательно повлиять на ваши системы или среды.
  * Мы пытаемся tooavoid отрицательное вещей, которые возникают ситуации toohello систем, которые вы используете с OMS, но некоторые неожиданные вещей.
* Возможна потеря или повреждение данных.
* Мы можем попросить вы toocollect журналы диагностики или других данных toohelp устранения неполадок.
* функция Hello или решения могут быть удалены (временно или постоянно).
  * Основаны на нашем данных во время предварительного просмотра hello мы может решить функций hello версии toonot или решения.
* Предварительные версии могут не работать или тестироваться со всеми конфигурациями; кроме того, мы можем ограничить следующее.
  * Здравствуйте, операционных систем, которые можно использовать (например, функция может применяться только tooLinux во время предварительного просмотра).
  * Здравствуйте, тип агента (MMA, Operations Manager), который можно использовать (например, компонент не может работать с Operations Manager во время предварительного просмотра).  
* Предварительный просмотр решений и компонентов не покрывается hello соглашение об уровне обслуживания.
* Работа с предварительными версиями компонентов потребует платы за использование.
* Функции и возможности, необходимые для функции hello / toobe решение полезно возможно, отсутствует или является неполным.
* Компоненты и решения могут быть доступны не во всех регионах.
* Компоненты и решения могут быть не локализованы.
* Компоненты и решения могут иметь ограничение на количество hello пользователей или устройств, которые можно использовать.
* Может потребоваться toouse сценариев tooperform конфигурации и tooenable hello решения или компонент.
* Hello пользовательского интерфейса (UI) является неполным и может измениться из tooday день.
* Общедоступные предварительные версии могут не подойти для ваших рабочих или критически важных систем.

#### <a name="for-private-preview"></a>Для *закрытых* предварительных версий
В выше элементов toohello сложения hello следующую информацию — Предварительный просмотр конкретных tooprivate:

* Мы предполагаем tooprovide нам отзыв о своем опыте работы, чтобы мы могли принимать hello компонент или решение, лучше.
* Мы можем обращаться к вам за отзывами с помощью опросов, по телефону и по электронной почте.
* Предварительные версии могут работать некорректно.
* Для участия может потребоваться заключить соглашение о неразглашении, так как предварительные версии могут включать в себя конфиденциальное содержимое.
  * Перед ведения блогов, работа с Twitter или в противном случае взаимодействия с третьими сторонами свяжитесь с hello руководителя программы, отвечающий за toounderstand hello Предварительный просмотр каких-либо ограничений на раскрытие.
* Предварительные версии не стоит использовать в рабочих и критически важных системах.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Получение доступа tooprivate предварительных версий компонентов и решений
Мы приглашаем предварительных версий tooprivate клиентов через несколькими различными способами в зависимости от hello предварительного просмотра.

* Ответы на опросы клиентов ежемесячные hello и дальнейшие нам разрешение toofollow вам повышает вероятность того, что приглашенных tooa личной предварительной версии.
* Ваше участие в тестировании может быть предложено менеджером по работе с клиентами Майкрософт.
* Данные о регистрации опубликованы в Twitter [msopsmgmt](https://twitter.com/msopsmgmt)
* Данные о регистрации распространяются на общественных мероприятиях — ищите нас на собраниях, конференциях и в онлайн-сообществах.

## <a name="next-steps"></a>Дальнейшие действия
* [Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные данные, собранные решения для управления.
