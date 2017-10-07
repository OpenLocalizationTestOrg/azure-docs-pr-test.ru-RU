---
title: "Операции Synchronization Service Manager Azure AD Connect | Документация Майкрософт"
description: "Выяснить, вкладка \"операции\" hello в hello диспетчер службы синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
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
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>С помощью hello вкладку операции синхронизации Service Manager

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

Вкладка "операции" Hello показывает результаты hello из самой последней операции hello. На этой вкладке является ключа toounderstand и устранения неполадок.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Понять сведения hello отображается на вкладке операции hello
верхняя половина Hello показывает все фрагменты в хронологическом порядке. По умолчанию hello журнала операций хранит сведения о hello последние семь дней, но этот параметр можно изменить с помощью hello [планировщика](active-directory-aadconnectsync-feature-scheduler.md). Требуется toolook любое выполнение, отображают состояние успеха. Вы можете изменить сортировку, щелкая заголовки hello hello.

Hello **состояние** столбец является наиболее важную информацию о hello и отображает hello наиболее серьезной проблемы для запуска. Вот наиболее распространенные состояния hello в порядке приоритета tooinvestigate краткая сводка (где * указания нескольких строк возможна ошибка).

| Состояние | Комментарий |
| --- | --- |
| stopped-* |не удалось запустить Hello. Например если hello удаленной системы не работает и не удается связаться с. |
| stopped-error-limit |Обнаружено более 5000 ошибок. Запустите Hello автоматически остановлена из-за toohello большое количество ошибок. |
| completed-\*-errors |Hello выполнение завершилось, но имеются ошибки (не более 5000), которые должны быть рассмотрены. |
| completed-\*-warnings |Запустите Hello завершена, но некоторые данные не находится в состоянии ожидается hello. Если обнаружены ошибки, такое сообщение обычно является указателем. Пока вы не исправили ошибки, не следует рассматривать предупреждения. |
| Успешное завершение |Проблемы отсутствуют. |

При выборе строки нижней hello обновляет сведения hello tooshow этого запуска. toohello расстояние слева от нижней hello, может возникнуть фраза про список **шаг #**. Он отображается, только если у вас в лесу несколько доменов, где каждый домен представлен шагом. Hello доменное имя можно найти под заголовком hello **секции**. В разделе **статистики синхронизации**, можно найти дополнительные сведения о hello число изменений, которые были обработаны. Можно щелкнуть tooget ссылки hello список объектов hello изменен. Если у вас есть объекты с ошибкой, они отображаются в разделе **Synchronization Errors**(Ошибки синхронизации).

Дополнительные сведения см. в разделе [Устранение неполадок синхронизации объекта с Azure AD](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
