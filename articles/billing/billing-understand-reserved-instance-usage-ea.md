---
title: "Общие сведения об использовании зарезервированных экземпляров Azure с соглашением о регистрации Enterprise | Документация Майкрософт"
description: "Узнайте, как читать данные об использовании, чтобы понимать применение зарезервированного экземпляра для соглашения о регистрации Enterprise."
services: billing
documentationcenter: 
author: manish-shukla01
manager: manshuk
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/03/2017
ms.author: manshuk
ms.openlocfilehash: 7ef601033b36ee968cb766d40a0a6b05afa9a1a4
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/16/2017
---
# <a name="understand--reserved-instance-usage-for-your-enterprise-enrollment"></a>Общие сведения об использовании зарезервированных экземпляров с соглашением о регистрации Enterprise
Научитесь понимать данные об использовании зарезервированного экземпляра с помощью ReservationId со [страницы резервирования](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade ) и использовать файл с [портала EA](https://ea.azure.com). Вы можете также просмотреть данные об использовании резервирования в разделе сводки на [портале EA](https://ea.azure.com).

>[!NOTE]
>Если вы приобрели резервирование в контексте выставления счетов с оплатой по мере использования, обратитесь к разделу [Understand Reserved Instance usage for your Pay-As-You-Go subscription](billing-understand-reserved-instance-usage.md) (Общие сведения об использовании зарезервированного экземпляра для подписки с оплатой по мере использования).

В следующем разделе предполагается, что запущена виртуальная машина Windows Standard_D1_v2 в регионе "Восточная часть США"А, и данные резервирования имеют вид, как в приведенной ниже таблице.

| Поле | Значение |
|---| --- |
|ReservationId |8f82d880-d33e-4e0d-bcb5-6bcb5de0c719|
|Количество |1|
|SKU | Standard_D1|
|Регион | eastus |

## <a name="reservation-application"></a>Приложения в резервировании

Аппаратная часть виртуальной машины рассматривается, так как развертываемая виртуальная машина соответствует атрибутам резервирования. Чтобы узнать, какое программное обеспечение Windows не входит в состав зарезервированного экземпляра, перейдите к разделу [Windows software costs not included with Reserved Instances](billing-reserved-instance-windows-software-costs.md) (Затраты на программное обеспечение Windows, не входящее в состав зарезервированных экземпляров).


### <a name="reservation-usage-in-csv"></a>Данные о резервировании в формате CSV
Можно скачать CSV-файл данных об использовании EA с портала EA. В скачанном CSV-файле отфильтруйте дополнительные сведения и введите свой идентификатор резервирования. На следующем снимке экрана показаны поля, связанные с резервированием.

![CSV-файл EA для зарезервированного экземпляра](./media/billing-understand-reserved-instance-usage-ea/billing-ea-reserved-instance-csv.png)

1. ReservationId в поле "Дополнительные сведения" представляет резервирование, которое было использовано для применения преимущества к виртуальной машине.
2. ConsumptionMeter представляет собой значение MeterId виртуальной машины.
3. Это ReservationMeter без затрат, так как затраты на выполнение виртуальной машины уже оплачены при резервировании. 
4. Виртуальная машина Standard_D1 имеет один виртуальный ЦП и развертывается без использования преимущества гибридного использования Azure. Таким образом данная единица измерения включает в себя дополнительную плату за программное обеспечение Windows. Ознакомьтесь с разделом [Windows software costs not included with Reserved Instances](billing-reserved-instance-windows-software-costs.md) (Затраты на программное обеспечение Windows в зарезервированных экземплярах виртуальных машин Azure). В нем вы найдете единицу измерения для 1-ядерной виртуальной машины серии D. В случае применения преимущества гибридного использования Azure эта дополнительная плата не будет взиматься.

### <a name="reservation-usage-in-usage-summary-page-in-ea-portal"></a>Данные об использовании резервирования на странице сводки по использованию на портале EA

Данные об использовании зарезервированного экземпляра также отображаются в разделе сводки по использованию на портале EA: ![Сводка по использованию EA](./media/billing-understand-reserved-instance-usage-ea/billing-ea-reserved-instance-usagesummary.png).

1. Плата за аппаратный компонент виртуальной машины не взимается, так как она входит в стоимость зарезервированного экземпляра. 
2. Взимается плата за программное обеспечение Windows, так как преимущество гибридного использования Azure не применяется. 

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.

Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.