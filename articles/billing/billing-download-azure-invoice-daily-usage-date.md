---
title: "aaaDownload выставления счета и ежедневно использования данных Azure | Документы Microsoft"
description: "Описывает, как toodownload или представления Azure расчетной счета и данных ежедневного использования."
keywords: "счет на оплату,скачать счет,счет azure,использование azure"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Скачивание или просмотр счета на оплату и данных о ежедневном использовании в Azure
Можно загрузить счет hello [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) или отправить по электронной почте его. toodownload ваше ежедневном использовании, последовательно выберите toohello [центр учетных записей Azure](https://account.windowsazure.com). Только определенные роли имеют разрешение tooget счета и использования сведения, например hello учетной записи администратора выставления счетов. в разделе toolearn Дополнительные сведения о получении доступа к данным toobilling, [tooAzure управление доступом, выставления счетов с помощью ролей](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Получение счета по электронной почте (в формате PDF)
Можно включить и настроить tooreceive дополнительных получателей счета Azure по электронной почте. Эта функция может быть недоступна для определенных подписок, например для предложений о планах поддержки, соглашений Enterprise или Azure с открытой лицензией.

1. Выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Необходимо выбрать все свои подписки. Щелкните **Invoices** (Счета), а затем — **Email my invoice** (Отправить счет по электронной почте). 

    ![Снимок экрана, показывающий hello участие в поток](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Нажмите кнопку **согласие** и примите условия hello.

    ![Снимок экрана, показывающий hello участие в поток](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Принятие соглашения hello формат, можно настроить дополнительных получателей.

    ![Снимок экрана, показывающий hello участие в поток](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Если не электронное сообщение после выполнения шагов hello, проверьте правильность адреса электронной почты в hello [получать сообщения от Майкрософт в вашем профиле](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Скачивание счета с портала Azure (в формате PDF)

1. Выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) в портал управления Azure как [это пользователь, обладающий доступом tooinvoices](billing-manage-access.md).

2. Выберите **Счета**. 

    ![Снимок экрана, показывающий hello выставления счетов и использования параметра](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Нажмите кнопку **загрузить счет** tooview копию счет PDF. Если отображается надпись **недоступно**, в разделе [почему я не вижу счета для hello последнего периода выставления счетов?](#noinvoice)

    ![Снимок экрана, показывающий циклов выставления счетов, параметр загрузки hello и общие затраты для каждого периода выставления счетов](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. Можно также просмотреть ежедневного использования нажав hello расчетного периода. 

Дополнительные сведения о счете см. в статье [Расшифровка счета за использование Microsoft Azure](billing-understand-your-bill.md). Справочные материалы по управлению затратами см. в статье [Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Загрузить сведения об использовании из hello центр учетных записей (.csv)

1. Вход в hello [центр учетных записей Azure](https://account.windowsazure.com/subscriptions) как Здравствуйте, администратор учетной записи.

2. Выберите подписку hello, для которого требуется hello счета и использования информации.

3. Щелкните **ЖУРНАЛ ВЫСТАВЛЕННЫХ СЧЕТОВ**. 

    ![Снимок экрана, на котором показан вариант "Журнал выставленных счетов"](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Можно увидеть ваши отчеты для hello последних шести периода выставления счетов и текущий период неоплаченным hello. 

    ![Снимок экрана, показывающий циклов выставления счетов, параметры toodownload счета и ежедневном использовании и общие затраты для каждого периода выставления счетов](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Выберите **просмотреть текущую выписку** toosee оценку ваших расходов на Оценка hello времени hello был создан. Эти сведения обновляются только один раз в день, поэтому в ней могут отображаться не все данные об использовании. Ежемесячный счет может отличаться от предварительного.

    ![Снимок экрана, показывающий hello параметр просмотреть текущую выписку](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Снимок экрана, показывающий hello оценку текущие расходы](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Выберите **скачать сведения об использовании** toodownload hello данных о ежедневном использовании в CSV-файл. Если вы видите две доступные версии, скачайте вторую.

    ![Снимок экрана, показывающий hello скачать сведения об использовании параметра](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Только администратор учетной записи hello могут обращаться к hello центр учетных записей Azure. Другие Администраторы выставления счетов, например владельца, можно получить сведения об использовании с помощью hello [выставления счетов API-интерфейсы](billing-usage-rate-card-overview.md).

Дополнительные сведения о данных о ежедневном использовании см. в статье [Расшифровка счета за использование Microsoft Azure](billing-understand-your-bill.md). Справочные материалы по управлению затратами см. в статье [Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure](billing-getting-started.md).

## <a name="noinvoice"></a>Почему я не вижу счета для hello последнего периода выставления счетов?

Это может происходить по нескольким причинам:

- В вашей подписке назначен ежемесячный кредит, не использованный полностью, или вы используете бесплатную пробную версию. Счет создается, только если вы должны что-то оплатить.

- Это менее 30 дней после даты hello подписана tooAzure.

- еще не создана накладная Hello. Подождите, пока конец hello hello расчетного периода.

- Если вы не являетесь hello учетной записи администратора, старые счета не может быть tooyou доступных.

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.

