---
title: "Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory | Документация Майкрософт"
description: "Предоставляет список сообщений об ошибках из hello Azure Active Directory действия содержимого пакета и шаги toofix их."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory 


При работе с hello пакет содержимого Power BI для предварительной версии Azure Active Directory, возможно, возникли следующие ошибки hello: 

- [Сбой обновления](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Не удалось tooupdate учетные данные источника данных](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Importing of data is taking too long](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) (Импорт данных занимает слишком много времени) 
 
Этот раздел содержит сведения о возможных причинах hello и как toofix эти ошибки.
 
## <a name="refresh-failed"></a>"Сбой обновления" 
 
**Как эта ошибка будет отображена**: электронной почты из Power BI или состояние ошибки в журнал обновления hello. 


| Причина: | Как toofix |
| ---   | ---        |
| Обновите сбоя, которые могут возникать ошибки при hello учетные данные пользователей hello подключении пакет содержимого toohello были сброса, но не обновляются в параметры подключения, hello hello hello содержимого пакета. | В Power BI найдите соответствующий toohello hello набора данных мониторинга журналы действие Azure Active Directory (Azure Active Directory действия журналы), выберите расписание обновления и затем введите учетные данные Azure AD. |
| Обновление может завершиться ошибкой из-за проблемы toodata в базовый пакет содержимого hello. | Отправьте запрос в службу поддержки. Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Не удалось tooupdate учетные данные источника данных 
 
**Как эта ошибка будет отображена**: В Power BI, можно использовать при подключении пакет содержимого журналов (Предварительная версия) Azure Active Directory действия toohello. 

| Причина: | Как toofix |
| ---   | ---        |
| Hello подключающегося пользователя является глобальным администратором, ни чтения безопасности или является администратором безопасности. | Эта учетная запись глобального администратора или чтения безопасности или безопасность admin tooaccess hello пакеты содержимого. |
| Клиент не имеет лицензии Premium или по крайней мере одного пользователя с файлом лицензии Premium. | Отправьте запрос в службу поддержки. Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>"Importing of data is taking too long" (Импорт данных занимает слишком много времени) 
 
**Как эта ошибка будет отображена**: В Power BI, после подключения ваш пакет содержимого hello данных процесс импорта начинается tooprepare панели мониторинга для Azure Active Directory журналом. Вы видите приветственное сообщение: «*Импорт данных...* »  

| Причина: | Как toofix |
| ---   | ---        |
| В зависимости от размера вашего клиента hello этот шаг может занять от нескольких минут too30 мин.. | Просто подождите. Если сообщение hello не изменяет tooshowing панели мониторинга в течение часа, отправьте запрос в службу поддержки. Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Дальнейшие действия

Щелкните tooinstall hello пакет содержимого Power BI в Azure Active Directory предварительной версии [здесь](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


