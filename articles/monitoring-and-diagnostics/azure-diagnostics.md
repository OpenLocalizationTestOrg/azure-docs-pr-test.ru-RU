---
title: "Обзор системы диагностики Azure | Документация Майкрософт"
description: "Диагностику Azure можно использовать для отладки, оценки производительности, мониторинга, а также анализа трафика в облачных службах, на виртуальных машинах и в Service Fabric."
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 0c6e4d9d2a3744f607b72364f3944c700acd070c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="what-is-azure-diagnostics"></a>Что такое система диагностики Azure
Система диагностики Azure позволяет выполнять сбор диагностических данных в развернутом приложении. Можно использовать модуль диагностики из различных источников. В настоящее время поддерживаются и веб-роли, и рабочие роли облачной службы Azure, и виртуальные машины Azure под управлением Microsoft Windows и Service Fabric. Другие службы Azure располагают собственной диагностикой.

## <a name="data-you-can-collect"></a>Собираемые данные
Система диагностики Azure может собирать следующие типы данных:

| Источник данных | Описание |
| --- | --- |
| Счетчики производительности |Системные и пользовательские счетчики производительности |
| Журналы приложений |Сообщения трассировки, записанные вашим приложением |
| Журналы событий Windows |Информация, отправляемая системой ведения журналов событий Windows |
| Источник событий .NET |События записи кода с использованием класса .NET [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) |
| Журналы IIS |Информация о веб-сайтах IIS |
| Трассировка событий Windows на основе манифестов |События трассировки событий Windows, созданные любым процессом |
| Аварийные дампы |Информация о состоянии процесса в случае сбоя приложения |
| Пользовательские журналы ошибок |Журналы, созданные вашим приложением или службой |
| Журналы инфраструктуры системы диагностики Azure |Информация о самой системе диагностики |

Модуль диагностики Azure может переносить эти данные в учетную запись хранения Azure и отправлять их через такие службы, как [Application Insights](../application-insights/app-insights-cloudservices.md). Данные можно использовать для отладки и устранения неполадок, измерения производительности, мониторинга использования ресурсов, анализа трафика и планирования производительности, а также в целях аудита.

## <a name="versioning"></a>Управление версиями
См. [Журнал версий системы диагностики Microsoft Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Дальнейшие действия
Выберите службы, в которых вы хотите собирать данные диагностики, и выполните действия, описанные в перечисленных ниже статьях. Справку по отдельным задачам см. в общих статьях о диагностике Azure.

## <a name="web-apps"></a>Веб-приложения
Обратите внимание на то, что в веб-приложениях диагностика Azure не используется. Ищите аналогичные данные в статье [Включение ведения журнала диагностики для веб-приложений в службе приложений Azure](../app-service/web-sites-enable-diagnostic-log.md).

## <a name="cloud-services-using-azure-diagnostics"></a>Облачные службы с использованием диагностики Azure
* Если используется Visual Studio, см. статью [Отладка облачной службы или виртуальной машины Azure в Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md). В остальных случаях см. следующие статьи:
* [Мониторинг облачных служб](../cloud-services/cloud-services-how-to-monitor.md)
* [Включение системы диагностики Azure в облачных службах Azure](../cloud-services/cloud-services-dotnet-diagnostics.md)

Более подробные сведения см. в статьях:

* [Application Insights для облачных служб Azure](../application-insights/app-insights-cloudservices.md)
* [Трассировка потока в приложении облачных служб с помощью системы диагностики Azure](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Включение системы диагностики Azure на виртуальной машине под управлением Windows с помощью PowerShell](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Виртуальные машины с использованием диагностики Azure
* Если используется Visual Studio, см. статью [Отладка облачной службы или виртуальной машины Azure в Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md). В остальных случаях см. следующие статьи:
* [Включение диагностики на виртуальных машинах Azure](../virtual-machines-dotnet-diagnostics.md)

Более подробные сведения см. в статьях:

* [Включение системы диагностики Azure на виртуальной машине под управлением Windows с помощью PowerShell](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Создание виртуальной машины Windows с мониторингом и диагностикой с использованием шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric с использованием диагностики Azure
Начните со статьи [Мониторинг и диагностика состояния служб в локальной среде разработки](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). В дереве навигации слева от нее вы найдете ссылки на множество других статей по диагностике Service Fabric.

## <a name="general-azure-diagnostics-articles"></a>Общие статьи о диагностике Azure
* [Схема конфигурации системы диагностики Azure](https://msdn.microsoft.com/library/azure/mt634524.aspx) — узнайте, как изменить файл схемы для сбора и маршрутизации диагностических данных. Для изменения файла схемы можно также использовать Visual Studio.
* [Хранение и просмотр диагностических данных в хранилище Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) — узнайте названия таблиц и больших двоичных объектов, в которые записываются диагностические данные.
* Узнайте, как [использовать счетчики производительности в Azure](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Узнайте, как [направлять данные диагностики Azure в Application Insights](azure-diagnostics-configure-application-insights.md).
* Если возникнут проблемы с запуском диагностики или поиском данных в таблицах хранилища Azure, см. статью [Устранение неполадок с помощью системы диагностики Azure](azure-diagnostics-troubleshooting.md).
