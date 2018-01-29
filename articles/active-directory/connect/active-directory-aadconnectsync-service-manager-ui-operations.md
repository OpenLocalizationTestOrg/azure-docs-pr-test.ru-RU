---
title: "Операции Synchronization Service Manager Azure AD Connect | Документация Майкрософт"
description: "Общие сведения о вкладке \"Operations\" (Операции) в Synchronization Service Manager для Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 91210edc3306b834cbd68f0f028845a7f36dd0b5
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="using-the-sync-service-manager-operations-tab"></a>Использование вкладки "Operations" (Операции) в Synchronization Service Manager

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

На вкладке "Operations" (Операции) отображаются результаты последних операций. Эта вкладка крайне важна для понимания и устранения неполадок.

## <a name="understand-the-information-visible-in-the-operations-tab"></a>Пояснение информации, отображаемой на вкладке "Operations" (Операции)
В верхней части отображены все операции выполнения в хронологическом порядке. По умолчанию журнал операций содержит сведения за последние семь дней, но эту цифру можно изменить с помощью [планировщика](active-directory-aadconnectsync-feature-scheduler.md). Вы можете найти любую операцию выполнения, которая не была завершена успешно. Вы также можете изменить порядок сортировки, щелкая заголовки.

Столбец **Status** (Состояние) является самым важным, он показывает наиболее серьезную проблему при выполнении. Ниже приводится краткая сводка наиболее распространенных состояний в порядке приоритета для анализа (где * означает, что возможно несколько строк ошибки).

| Status | Комментарий |
| --- | --- |
| stopped-* |Не удалось завершить выполнение. Например, если удаленная система не работает и с ней не удается связаться. |
| stopped-error-limit |Обнаружено более 5000 ошибок. Выполнение было автоматически остановлено из-за большого количества ошибок. |
| completed-\*-errors |Выполнение завершено, но есть ошибки (меньше 5000), которые необходимо изучить. |
| completed-\*-warnings |Запуск завершен, но некоторые данные не находятся в ожидаемом состоянии. Если обнаружены ошибки, такое сообщение обычно является указателем. Пока вы не исправили ошибки, не следует рассматривать предупреждения. |
| Успешное завершение |Проблемы отсутствуют. |

При выборе строки в нижней части отображаются сведения об этой операции выполнения. Слева внизу может отображаться список **Step #**(Шаг №). Он отображается, только если у вас в лесу несколько доменов, где каждый домен представлен шагом. Имя домена можно найти в разделе **Partition**(Секция). В разделе **Synchronization Statistics**(Статистика синхронизации) можно найти дополнительные сведения о числе обработанных изменений. Щелкая ссылки, можно получить список измененных объектов. Если у вас есть объекты с ошибкой, они отображаются в разделе **Synchronization Errors**(Ошибки синхронизации).

Дополнительные сведения см. в разделе [Устранение неполадок синхронизации объекта с Azure AD](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).

## <a name="next-steps"></a>Дополнительная информация
Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
