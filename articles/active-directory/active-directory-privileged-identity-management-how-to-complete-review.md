---
title: "aaaHow toocomplete доступе | Документы Microsoft"
description: "После запуска проверки доступа в Azure AD Privileged Identity Management, узнайте, как toocomplete его и просмотрите hello результатов"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Как toocomplete доступа просмотрите в Azure AD Privileged Identity Management
После [запуска функции проверки безопасности](active-directory-privileged-identity-management-how-to-start-security-review.md)администраторы привилегированных ролей могут проверить привилегированный доступ. Azure AD Privileged Identity Management (PIM) автоматически отправляет сообщение электронной почты, запросы пользователей tooreview свой доступ. Если пользователь не получает сообщение электронной почты, можно отправить им инструкции hello [как tooperform безопасности просмотрите](active-directory-privileged-identity-management-how-to-perform-security-review.md).

После период проверки безопасности hello, или все пользователи hello закончена, просмотрите их самостоятельно, выполните действия hello в этой статье toomanage hello проверки и просмотреть результаты hello.

## <a name="manage-security-reviews"></a>Управление проверкой безопасности
1. Go toohello [портал Azure](https://portal.azure.com/) и выберите hello **Azure AD Privileged Identity Management** приложения в панели мониторинга.
2. Выберите hello **проверки доступа к** hello панели мониторинга.
3. Выберите требуемый toomanage hello доступе.

В колонке сведений проверки доступа hello существует число параметров для управления этой проверки.

![Кнопки проверки доступа PIM — снимок экрана][1]

### <a name="remind"></a>Напомнить
При доступе настройки, чтобы просмотреть hello пользователи сами hello **напоминать** кнопка отправляет уведомление. 

### <a name="stop"></a>Остановить
Все отзывы доступ имеют срок действия, но можно использовать hello **остановить** toofinish кнопку раньше его. Если к этому времени еще не были проверены все пользователи, они не будет возможности tooafter остановить проверку hello. Нельзя перезапустить проверку после ее остановки.

### <a name="apply"></a>Применить
После завершения проверки доступа, либо из-за достижения Дата окончания hello или остановить его вручную, hello **применить** реализовывать hello результат проверки hello. Если при проверке hello запрещен доступ пользователя, это hello, приведет к удалению назначения ролей.  

### <a name="export"></a>экспорт.
Если требуется tooapply hello результатов проверки безопасности hello вручную, можно экспортировать hello проверки. Hello **Экспорт** кнопку начнется загрузка CSV-файла. Вы можете управлять hello результаты в Excel или другие программы, откройте CSV-файлы.

### <a name="delete"></a>Удалить
Если вы не заинтересованы в hello просматривать любые дополнительные, удалите его. Hello **удалить** кнопка удаляет hello проверки из hello PIM приложения.

> [!IMPORTANT]
> Будет не появляется предупреждение, прежде чем произойдет удаление, поэтому убедитесь, что требуется toodelete, просмотрите. 

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
