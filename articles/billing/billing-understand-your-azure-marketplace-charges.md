---
title: "aaaUnderstand Azure взимает плату внешней службы | Документы Microsoft"
description: "Узнайте больше о выставлении счетов за использование внешних служб, ранее известных как Marketplace, в Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>Основные сведения о выставлении счетов за использование внешних служб в Azure
Внешние службы используется toobe вызывается Azure Marketplace. Обычно это службы, публикуемые сторонними поставщиками для использования в Azure, но при этом они полностью интегрируются в Azure. Например, ClearDB и SendGrid — это внешние службы, которые можно приобрести в Azure, но которые не опубликованы корпорацией Майкрософт.

При подготовке новой внешней службы или ресурса отображается предупреждение.

![Предупреждение о покупке Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> Внешние службы публикуются компаниями, не принадлежащими корпорации Майкрософт, но иногда продукты Майкрософт также относят к внешним службам.
> 
> 

## <a name="how-external-services-are-billed"></a>Как выставляются счета за внешние службы
- Счета за внешние службы выставляются отдельно. Они обрабатываются как отдельные заказы в подписке Azure. Hello расчетного периода для каждой службы задается при покупке hello службы. Не toobe путать с hello расчетного периода подписки hello, под которой он был приобретен. Вы будете получать отдельные счета, плата за которые будет отдельно взиматься с кредитной карты.
- У каждой внешней службы своя модель выставления счетов. Одни службы используют модель с оплатой по мере использования, другие — модель с ежемесячными платежами. Для оплаты внешних служб Azure нужна кредитная карта, их нельзя приобрести посредством оплаты счета.
- Для оплаты внешних служб невозможно использовать бесплатные кредитные средства. Если вы используете подписка Azure, которая включает [освободить кредиты](https://azure.microsoft.com/pricing/spending-limits/), они не может быть применен tooexternal службы спецификаций. С помощью внешних служб toopurchase кредитной карты.


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>Просмотр расходов внешней службы и журналом hello портал Azure
Можно просмотреть список hello внешних служб, которые находятся на каждой подписки в hello [портал Azure](https://portal.azure.com/): 

1. Войдите в toohello [портал Azure](https://portal.azure.com/) от имени учетной записи администратора hello.
2. В главном меню hello, выберите **подписки**.
   
    ![Выберите в главном меню hello подписки](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. В hello **подписки** колонки, выберите hello подписки требуется tooview, а затем выберите **внешних служб**.
   
    ![Выберите подписку, в колонке выставления счетов hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. Необходимо просмотреть заказы внешней службы, имя издателя hello, уровня службы, которые вы приобрели, названием ресурса hello и текущее состояние заказа hello. toosee за счета, установите внешней службы.
   
    ![Выберите внешнюю службу.](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. Здесь можно просмотреть за суммы счета, включая декомпозиции налога hello.
   
    ![Просмотрите журнал выставленных счетов за внешние службы.](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>Просмотр расходов на внешние службы для клиентов с соглашением Enterprise (EA)
EA клиенты могут увидеть тратит внешнюю службу и загрузить отчет в портале EA hello. В разделе [Azure Marketplace для клиентов EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget работы.

## <a name="manage-payment-methods-for-external-service-orders"></a>Управление способами оплаты заказов внешних служб
Обновление методов оплаты для внешней службы заказами hello [центр учетных записей](https://account.windowsazure.com/).

> [!NOTE]
> Если вы приобрели подписку с помощью учетной записи рабочего или учебного заведения, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake изменяет способ оплаты tooyour.
> 
> 

1. Войдите в toohello [центр учетных записей](https://account.windowsazure.com/) и [перехода toohello **marketplace** вкладка](https://account.windowsazure.com/Store)
   
    ![Выберите marketplace в центре учетных записей hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. Выберите внешнюю службу hello требуется toomanage
   
    ![Выберите внешнюю службу hello требуется toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. Нажмите кнопку **изменить метод оплаты** hello правой части страницы приветствия. Эта ссылка переводит вы tooa различных портала toomanage метод оплаты.
   
    ![Сводка заказов](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. Нажмите кнопку **изменить сведения о** и следуйте инструкциям tooupdate платежную информацию.
   
    ![Выберите "Изменить информацию".](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>Отмена заказа внешней службы
Toocancel ваш заказ внешней службы, удалить ресурс hello в hello [портал Azure](https://portal.azure.com).

![Удалите ресурс.](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если у вас есть вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.

