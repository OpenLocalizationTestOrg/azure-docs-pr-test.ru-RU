---
title: "aaaSupported типов ресурсов с помощью исправности ресурсов Azure | Документы Microsoft"
description: "Поддерживаемые типы ресурсов в службе работоспособности ресурсов Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Типы ресурсов и проверки работоспособности в службе работоспособности ресурсов Azure
Ниже приведен полный список всех hello проверок, выполняемых через исправности ресурсов по типам ресурсов.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Выполняемые проверки|
|---|
|<ul><li>Все узлы кэша hello функционируют и под управлением?</li><li>Hello кэш доступен в центре обработки данных hello?</li><li>Имеет кэш достигнуто максимальное число подключений для hello приветствия?</li><li> Исчерпано кэша hello ее доступной памяти </li><li>Hello кэша наблюдается большое количество ошибок страниц физической памяти?</li><li>Hello кэша в условиях интенсивной нагрузки?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Выполняемые проверки|
|---|
|<ul> <li>Любой из конечных точек hello была остановлена, удален или неправильно настроенных?</li><li>Дополнительный портал hello доступен для операций настройки CDN?</li><li>Существуют проблемы постоянную установку с hello конечных точек CDN?</li><li>Пользователи конфигурацию можно изменить hello ресурсами CDN?</li><li>Изменения конфигурации публикуют скоростью hello ожидалось?</li><li>Управляющие пользователей с помощью hello портал Azure, PowerShell или hello API конфигурации CDN hello</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Выполняемые проверки|
|---|
|<ul><li>Сервер узла hello настройки и выполнения?</li><li>Загрузка операционной системы узла hello выполнила?</li><li>Подготовленная hello контейнер виртуальной машины и включении?</li><li>Существует ли сетевое подключение между узлом hello и hello учетной записи хранилища?</li><li>Hello загрузку hello гостевая операционная система выполнила?</li><li>Есть ли назначенные работы по техническому обслуживанию?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Выполняемые проверки|
|---|
|<ul><li>Учетная запись hello доступен в центре обработки данных hello?</li><li>Hello Когнитивных служб поставщика ресурсов доступны?</li><li>Hello Когнитивных службы в соответствующие области hello?</li><li>Можно прочитать операции в учетной записи хранения hello, удерживая hello метаданных ресурсов?</li><li>Был достигнут квоты вызовов hello API?</li><li>Достигнут лимит чтения для вызова hello API?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Выполняемые проверки|
|---|
|<ul><li>Hello размещение этой виртуальной машины, копирование и запуск сервера?</li><li>Загрузка операционной системы узла hello выполнила?</li><li>Подготовленная hello контейнер виртуальной машины и включении?</li><li>Существует ли сетевое подключение между узлом hello и hello учетной записи хранилища?</li><li>Hello загрузку hello гостевая операционная система выполнила?</li><li>Есть ли назначенные работы по техническому обслуживанию?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Выполняемые проверки|
|---|
|<ul><li>Можно пользователей, которых отправки заданий в аналитике Озера tooData в hello области?</li><li>Сделать hello запуска и завершения успешно в области Основные задания?</li><li>Список можно элементы каталога в регионе hello пользователей?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Выполняемые проверки|
|---|
|<ul><li>Могут ли пользователи отправлять хранилища Озера данных tooData в регионе hello?</li><li>Пользователи загружать данные из хранилища Озера данных в регионе hello</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Выполняемые проверки|
|---|
|<ul><li>Появились ли базы данных или коллекцию запросов, не выполненных из-за недоступности службы DocumentDB tooa?</li><li>Внесены все запросы документов, не выполненных из-за недоступности службы DocumentDB tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Выполняемые проверки|
|---|
|<ul><li>Подключен ли hello туннель VPN?</li><li>Нет конфликтов конфигурации в hello подключения?</li><li>Hello предварительные общие ключи правильно настроены?</li><li>Доступен hello VPN-устройство локальной?</li><li>Существуют ли несоответствия в политике безопасности IPSec/IKE hello?</li><li>Такое подключение S2S VPN hello правильно подготовленные или в состоянии сбоя</li><li>Возможности подключения VNET-VNET hello правильно подготовленные или в состоянии сбоя</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Выполняемые проверки|
|---|
|<ul><li>Доступна из шлюза VPN hello hello Интернет?</li><li>Hello VPN-шлюза в ждущем режиме?</li><li>Выполняется ли hello службы VPN на hello шлюза?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Выполняемые проверки|
|---|
|<ul><li> Выполняются операции среды выполнения, как регистрации, установки или отправки приветствия имен?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Выполняемые проверки|
|---|
|<ul><li>Операционная система узла hello настройки и выполнения?</li><li>Доступна hello workspaceCollection из вне hello центра обработки данных?</li><li>Hello поставщика ресурсов PowerBI доступны?</li><li>Hello PowerBI службы hello соответствующие области?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Выполняемые проверки|
|---|
|<ul><li>Можно было выполнять операции диагностики hello кластера?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Выполняемые проверки|
|---|
|<ul><li> Появились ли база данных toohello входа?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Выполняемые проверки|
|---|
|<ul><li>Являются все узлы hello, где выполняется копирование и запуск задания hello?</li><li>Было невозможно toostart hello задания?</li><li>Существуют ли запланированные обновления среды выполнения?</li><li>— Задание hello в ожидаемом состоянии (например работает или остановлена клиентом)?</li><li>Hello задания произошла исключений памяти?</li><li>Существуют ли запланированные обновления вычислительной среды?</li><li>Hello диспетчер выполнения (план управления) доступны?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Выполняемые проверки|
|---|
|<ul><li>Сервер узла hello настройки и выполнения?</li><li>Работает ли служба Internet Information Services?</li><li>Выполняется ли hello балансировки нагрузки?</li><li>Hello плана веб-службы доступен в центре обработки данных hello?</li><li>Доступен hello хранилища учетной записи размещения hello узлов содержимого для фермы серверов hello??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Выполняемые проверки|
|---|
|<ul><li>Сервер узла hello настройки и выполнения?</li><li>Работает ли сервер Internet Information?</li><li>Выполняется ли hello балансировки нагрузки?</li><li>Веб-приложения hello доступен в центре обработки данных hello?</li><li>Hello учетной записи хранилища, на котором размещена hello доступного содержимого сайта?</li></ul>|

# <a name="next-steps"></a>Дальнейшие действия
-  В разделе [tooAzure введение работоспособность службы](service-health-overview.md) и [tooAzure введение исправности ресурсов](resource-health-overview.md) toounderstand Дополнительные сведения об их. 
-  [Azure Resource Health FAQ](resource-health-faq.md) (Часто задаваемые вопросы о службе работоспособности ресурсов Azure)
- Настройте оповещения о проблемах, связанных с работоспособностью. Дополнительные сведения см. в статье [Создание оповещений журнала действий для уведомлений службы](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 