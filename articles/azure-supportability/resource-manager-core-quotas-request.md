---
title: "Запросы на увеличение квоты ядер Azure Resource Manager | Документация Майкрософт"
description: "Запросы на увеличение квоты ядер Azure Resource Manager."
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a>Запросы на увеличение квоты ядер Resource Manager

Квоты ядер Resource Manager применяются на уровне региона и семейства SKU.
Дополнительные сведения о применении квот доступны на странице [Подписка Azure, границы, квоты и ограничения службы](http://aka.ms/quotalimits).
Чтобы узнать больше о семействах SKU, вы можете сравнить затраты и производительность на странице [Цены на виртуальные машины Windows](http://aka.ms/pricingcompute).

Чтобы запросить увеличение квоты ядер, отправьте соответствующее обращение в службу поддержки на портале Azure: [https://portal.azure.com](https://portal.azure.com).

> [!NOTE]
> Узнайте, как [создать запрос на поддержку](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) на портале Azure.

1. На странице создания запроса на поддержку выберите тип проблемы "Квота" и тип квоты как "Ядра".

    ![Колонка "Основные" для квоты](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. Выберите модель развертывания "Resource Manager" и укажите расположение.

    ![Колонка "Проблема" для квоты](./media/resource-manager-core-quotas-request/Problem-step.png)

3. Выберите семейства SKU, которые требуют увеличения квоты.

    ![Выбранные семейства SKU](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. Введите желаемые ограничения для подписки.

    ![Новый запрос квоты для SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- Чтобы удалить строку, снимите флажок SKU в раскрывающемся списке семейства SKU или щелкните значок отмены "x".
После ввода требуемой квоты для каждого семейства SKU нажмите кнопку "Далее" на странице "Проблема", чтобы продолжить создание запроса на поддержку.
