---
title: "Создание емкости Power BI Embedded на портале Azure | Документация Майкрософт"
description: "В этой статье содержится пошаговое руководство по созданию емкости Power BI Embedded в Microsoft Azure."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 09/28/2017
ms.author: asaxton
ms.openlocfilehash: 1902e5c18cd7083ceeda79e6b9e779e4baaf175a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="create-power-bi-embedded-capacity-in-the-azure-portal"></a>Создание емкости Power BI Embedded на портале Azure

В этой статье содержится пошаговое руководство по созданию емкости Power BI Embedded в Microsoft Azure. Power BI Embedded упрощает возможности Power BI, позволяя быстро добавлять привлекательные визуальные элементы, отчеты и панели мониторинга в приложения.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.

> [!VIDEO https://www.youtube.com/embed/aXrvFfg_iSk]

## <a name="before-you-begin"></a>Перед началом работы

Для работы с этим кратким руководством вам понадобится:

* **Подписка Azure**: откройте ссылку на [бесплатную пробную версию Azure](https://azure.microsoft.com/free/), чтобы создать учетную запись.
* **Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory (AAD). И ***необходимо войти в Azure с учетной записью в этом клиенте***. Учетные записи Майкрософт не поддерживаются. Дополнительные сведения см. в руководстве по аутентификации и настройке пользовательских разрешений.
* **Клиент Power BI:** по крайней мере одна учетная запись в клиенте AAD должна быть зарегистрирована в Power BI.
* **Группа ресурсов**: используйте уже имеющуюся группу ресурсов или [создайте новую](../azure-resource-manager/resource-group-overview.md).

## <a name="create-a-capacity"></a>Создание емкости

1. Войдите на [портал Azure](https://portal.azure.com/).

2. Щелкните **+ Создать** > **Данные и аналитика**.

3. В поле поиска введите *Power BI Embedded*.

4. В Power BI Embedded щелкните **Создать**.

5. Введите требуемые данные и щелкните **Создать**.

    ![Заполняемые поля для создания емкости](media/create-capacity/azure-portal-create-power-bi-embedded.png)

    |Настройка |Описание |
    |---------|---------|
    |**Имя ресурса**|Имя для идентификации емкости. Помимо портала Azure, имя ресурса отображается и на портале администрирования Power BI.|
    |**Подписка**|Подписка, в которой требуется создать емкость.|
    |**Группа ресурсов**|Группа ресурсов для создаваемой емкости. Выберите имеющуюся группу ресурсов или создайте новую. Дополнительные сведения см. в [обзоре Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).|
    |**Администратор емкости Power BI**|Администраторы емкости Power BI могут просматривать емкость на портале администрирования Power BI и предоставлять разрешения другим пользователям. По умолчанию администратором емкости является ваша учетная запись. Администратор емкости должен быть размещен в вашем клиенте Power BI.|
    |**Расположение**|Расположение Power BI для вашего клиента. Этот параметр устанавливается автоматически и не может быть изменен.|
    |**Ценовая категория**|Выберите номер SKU (число виртуальных ядер и объем памяти), соответствующий вашим потребностям.  Дополнительные сведения см. на странице с информацией о [ценах на Power BI Embedded](https://azure.microsoft.com/pricing/details/power-bi-embedded/).|

6. Нажмите кнопку **Создать**.

Создание обычно занимает меньше минуты, чаще всего несколько секунд. Если вы выбрали **Закрепить на панели мониторинга**, перейдите к своей панели мониторинга, чтобы просмотреть новую емкость. Или выберите **Больше служб** > **Power BI Embedded**, чтобы узнать, готова ли ваша емкость.

![Емкость Power BI Embedded на панели мониторинга на портале Azure](media/create-capacity/azure-portal-dashboard.png)

## <a name="next-steps"></a>Дальнейшие действия

Чтобы использовать новую емкость Power BI Embedded, перейдите на портал администрирования Power BI для назначения рабочих областей. Дополнительные сведения см. в разделе [Управление емкостью в Power BI Premium и Power BI Embedded](https://powerbi.microsoft.com/documentation/powerbi-admin-premium-manage/).

Если данная емкость не нужна, приостановите ее, чтобы остановить выставление счетов за ее использование. Дополнительные сведения см. в разделе [Приостановка и запуск емкости Power BI Embedded на портале Azure](pause-start.md).

Чтобы начать внедрение содержимого Power BI в приложение, прочитайте раздел [Внедрение панелей мониторинга, отчетов и плиток Power BI](https://powerbi.microsoft.com/documentation/powerbi-developer-embedding-content/).

У вас имеются и другие вопросы? [Попробуйте задать их в сообществе Power BI](http://community.powerbi.com/)