---
title: "Анализ вариантов использования Azure CDN | Документация Майкрософт"
description: "Клиент может включить анализ журналов для Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: ce9ec021250a3548e23ad87273a9225cdf700c70
ms.sourcegitcommit: 7f1ce8be5367d492f4c8bb889ad50a99d85d9a89
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Анализ вариантов использования CDN Azure

Когда вы включите CDN для вашего приложения, вам, скорее всего, нужно будет отслеживать использование CDN, проверять работоспособность службы доставки и устранять возможные неполадки. Azure CDN позволяет делать это следующим образом. 

## <a name="core-analytics-via-azure-diagnostic-logs"></a>Базовая аналитика с использованием журналов диагностики Azure

Базовая аналитика доступна для всех конечных точек CDN, относящихся к профилям CDN Verizon (уровни "Стандартный" и "Премиум") и Akamai (уровень "Стандартный"). Журналы диагностики Azure разрешают экспортировать базовую аналитику в хранилище Azure, концентраторы событий или службу Log Analytics в Operations Management Suite (OMS). Log Analytics OMS предлагает решение с настраиваемыми диаграммами. См. дополнительные сведения о [журналах диагностики Azure](cdn-azure-diagnostic-logs.md).

## <a name="verizon-core-reports"></a>С помощью базовых отчетов Verizon

Как пользователь с Azure CDN с профилем Verizon "Стандартный" или "Премиум" вы можете просматривать базовые отчеты Verizon на вспомогательном портале Verizon. На портале Azure доступны базовые отчеты Verizon со множеством графиков и представлений. Их можно открыть с помощью параметра **Управление**. См. дополнительные сведения о [базовых отчетах Verizon](cdn-analyze-usage-patterns.md).

## <a name="verizon-custom-reports"></a>Настраиваемые отчеты Verizon

Как пользователь с Azure CDN с профилем Verizon "Стандартный" или "Премиум", вы можете просматривать настраиваемые отчеты Verizon на вспомогательном портале Verizon. Доступ к настраиваемым отчетам Verizon можно получить на портале Azure с помощью параметра **Управление**. На странице настраиваемых отчетов Verizon отображается число попаданий или данных, передаваемых для каждой граничной записи CName, принадлежащей профилю Azure CDN. Данные можно группировать по HTTP-коду ответа или состоянию кэша за любой период времени. См. дополнительные сведения о [настраиваемых отчетах Verizon](cdn-verizon-custom-reports.md).

## <a name="verizon-premium-reports"></a>Отчеты Verizon уровня "Премиум"

С помощью **Azure CDN от Verizon уровня "Премиум"** можно получить доступ к следующим отчетам:
   * [Расширенные HTTP-отчеты.](cdn-advanced-http-reports.md)
   * [Статистика в режиме реального времени.](cdn-real-time-stats.md)
   * [Производительность граничного узла](cdn-edge-performance.md)

