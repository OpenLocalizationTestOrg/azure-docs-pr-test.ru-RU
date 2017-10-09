---
title: "aaaTroubleshoot Azure проблемы с регистрацией | Документы Microsoft"
description: "Описывает, как tootroubleshoot некоторые распространенные Azure Зарегистрируйтесь проблемы."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Устранение неполадок при регистрации в Azure
Если вы не можете зарегистрироваться для Azure, следуйте советам hello в этой статье tootroubleshoot распространенных проблем. При возникновении проблем с кредитной картой во время регистрации см. статью [Банковская или кредитная карта отклонена при регистрации в Azure](billing-credit-card-fails-during-azure-sign-up.md). Если есть учетная запись Azure, но не удается выполнить вход, см. раздел [не удается войти в toomanage Моя подписка Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>Индикатор выполнения зависает в разделе "Проверка личности с помощью карты"

Проверка подлинности hello toocomplete картой, сторонние файлы cookie должен быть разрешен для браузера.

![Снимок экрана: hello проверка подлинности по разделам карты висячей во время регистрации](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Используйте следующие шаги tooupdate hello параметры файлов cookie в браузере.

1. При использовании Chrome go слишком**параметры** > **Показывать дополнительные параметры** > **конфиденциальности** > **содержимого Параметры**. Снимите флажок **Блокировать данные и файлы cookie сторонних сайтов**.
2. При использовании Edge go слишком**параметры** > **Просмотр расширенных параметров** > **файлы cookie**. Выберите **Не блокировать файлы "cookie"**.
3. Обновите hello Azure "Регистрация" и проверьте, устранена ли проблема hello.
4. Если обновление hello не решило проблему hello, закройте и перезапустите браузер и повторите попытку.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Форма кредитной карты не поддерживает мой адрес для выставления счетов
Адрес для выставления счета требуется toobe в стране hello, выбранного в hello **о вас** раздела. Убедитесь, что вы выбрали правильную страну hello.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Отсутствие текстовых сообщений или вызовов при проверке учетной записи во время регистрации
Хотя обычно гораздо быстрее, может занять toofour минут для проверки кода toobe доставки. номер телефона Hello, которое вводится для проверки не хранятся как номер контакта для учетной записи hello.

Ниже приведены некоторые дополнительные советы:
* Номер телефона VOIP не может использоваться для проверки процесса hello телефона.
* Проверьте hello номер телефона, который вводится, включая код страны hello, выбранный в раскрывающемся меню hello.
* Если ваш телефон не получает текстовых сообщений (SMS), попробуйте hello **Позвонить** параметр.
* Убедитесь, что ваш телефон может получать звонки или SMS-сообщения с номера в США.

Получив текстовое сообщение hello или телефонный звонок, введите код, который появляется в текстовом поле hello.

## <a name="credit-card-declined-or-not-accepted"></a>Кредитная карта отклонена или не принята
Оплата с использованием таких карт не поддерживается для подписок Azure. разделе toosee, что еще может привести к toobe карта отклонена, [отклонено дебетовой картой или кредитная карта, в Azure регистрации](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"Бесплатная пробная версия недоступна"
Вы использовали подписки Azure в прошлом hello? Hello Azure условия использования соглашение ограничивает свободного активации пробной версии только для пользователя, который является новой tooAzure. Если у вас уже была подписка Azure любого типа, вы не сможете активировать бесплатную пробную версию. Попробуйте зарегистрироваться, чтобы использовать [подписку с оплатой по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>В учетной записи бесплатной пробной версии появился платеж
Может появиться небольшая проверки хранения в вашей учетной записи кредитной карты после регистрации, которая удаляется в течение трех дней too5. Если вы беспокоитесь об управлении расходами, узнайте больше о [предотвращении непредвиденных затрат](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Не удается активировать льготный план Azure, например MSDN, BizSpark, BizSparkPlus или MPN
Убедитесь, что вы используете hello правый вход учетные данные. Затем проверьте hello преимущество программы toomake убедиться, что дает право. 

* MSDN
  * Проверьте свой статус соответствия требованиям на своей [странице учетной записи MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Если не удается проверить свое состояние, обратитесь в службу hello [центры обслуживания пользователей подписки MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Войдите в toohello [BizSpark портала](https://www.microsoft.com/bizspark/default.aspx#start-two) и проверьте состояние проверки допустимости для BizSpark и BizSpark плюс.
  * Если не удается проверить свое состояние, вы можете [помощь на форумах hello BizSpark](http://aka.ms/bzforums).
* MPN
  * Войдите в toohello [портала MPN](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) и проверьте состояние проверки допустимости. Если у вас есть соответствующие hello [облачной платформы компетенции](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), могут оказаться пригодными для дополнительные преимущества.
  * Если вам не удается проверить свой статус, обратитесь в [службу поддержки MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Не удается активировать новую подписку Azure с открытой лицензией
toocreate подписку Azure в Open, необходимо иметь допустимый ключ документации службы активации (OSA) с по крайней мере один Azure в Open маркера tooit связанные. Если у вас нет ключа OSA, свяжитесь с любым из партнеров корпорации Майкрософт, которые перечислены на странице [Партнеры Майкрософт](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
