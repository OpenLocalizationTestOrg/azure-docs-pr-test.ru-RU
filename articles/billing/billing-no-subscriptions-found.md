---
title: "подписки aaaNo найдены ошибки при повторите toosign на портале tooAzure или в центре учетных записей Azure | Документы Microsoft"
description: "Предлагается решение hello подписки не найдены возникает ошибка проблемы при входе в портал tooAzure или центр учетных записей Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Ошибка "Подписки не найдены" на портале Azure или в Центре управления учетной записью Azure
Может появиться сообщение об ошибке «Подписки не найден» при попытке toosign в toohello [портал Azure](https://portal.azure.com/) или hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions). В этой статье предлагается решение указанной проблемы.

## <a name="symptom"></a>Симптом

При попытке toosign в toohello [портал Azure](https://portal.azure.com/) или hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions), появляется сообщение об ошибке после hello: «Подписки не найдены».

## <a name="cause"></a>Причина:

Эта проблема возникает, если учетная запись не предоставляет необходимых разрешений. 

## <a name="solution"></a>Решение

Убедитесь, что войдите как администратор правильный hello. Администратор учетной записи может получить доступ только hello центр учетных записей. Администраторы служб (SA) и Соадминистраторами (CA) имеют только toohello разрешение доступа к порталу Azure, или hello классический портал Azure.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Сценарий 1: Получено сообщение об ошибке в hello [портал Azure](https://portal.azure.com)

toofix этой проблемы:

* Убедитесь, что правильных Azure directory выбран, щелкнув вашей учетной записи в правом верхнем углу hello hello.

  ![Выберите hello каталогов в hello верхнему правому углу hello портал Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Если hello справа Azure directory выбран, но по-прежнему сообщение hello, [свою учетную запись, добавляемого в качестве владельца](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Сценарий 2: Получено сообщение об ошибке в hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions)

Проверка hello учетной записью, используемой hello учетной записи администратора. tooverify кто Здравствуйте, администратор учетной записи, выполните следующие действия:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите меню концентратора hello **подписки**.
3. Выберите подписку hello требуется toocheck, а затем выберите **параметры**.
4. Выберите **Свойства**. Здравствуйте, администратор учетной записи подписки hello отображается в hello **администратор учетной записи** поле.

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget быстро устранить проблему. 
