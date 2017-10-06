---
title: "aaaHow tooLink tooAzure подписки Azure AD B2C | Документы Microsoft"
description: "Пошаговое руководство по tooenable выставления счетов для клиента Azure AD B2C в подписку Azure."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Связывание toopay клиента подписки Azure tooan Azure B2C для использования расходов

Текущее использование для Azure Active Directory B2C (или Azure AD B2C) взимается по документу tooan подписки Azure. Это необходимо для клиента hello Azure AD B2C tooan подписки Azure, после создания клиента hello B2C сам hello клиента администратора tooexplicitly ссылку.  Эта ссылка достигается путем создания Azure AD «Клиента B2C» ресурса в целевом hello подписки Azure. Множество B2C клиентов может быть одной подписки Azure связанного tooa вместе с другими ресурсами Azure (например, виртуальных машин, хранилища данных, LogicApps)


> [!IMPORTANT]
> последние сведения об использовании выставления счетов и ценах на странице приветствия для B2C Hello: [ценообразования Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Шаг 1. Создание клиента Azure AD B2C
Сначала нужно создать клиент B2C. Пропустите этот шаг, если вы уже создали целевого клиента B2C. [Начало работы с Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Шаг 2 - откройте портал Azure на приветствия клиента Azure AD, который показывает подписки Azure
Перейдите toohello [портал Azure](https://portal.azure.com). Переключение toohello клиента Azure AD, который показывает hello хотелось бы toouse подписки Azure. Этот клиент Azure AD, отличается от клиента B2C hello. В рамках hello портал Azure щелкните имя учетной записи hello hello верхней правой части hello мониторинга tooselect hello клиента Azure AD. Подписка Azure имеет необходимые tooproceed. [Оформление подписки Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Переключение tooyour клиента Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Шаг 3. Создание ресурса "Клиент B2C" в Azure Marketplace
Откройте Marketplace, щелкнув значок Marketplace hello, или выбрав hello зеленого «+» в верхний левый угол hello hello панели мониторинга.  Найдите и выберите Azure Active Directory B2C. Нажмите кнопку Создать.

![Выбор плитки Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Поиск AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Hello ресурсов Azure AD B2C создать диалоговое окно hello обложки, следующие параметры:

1. Клиент Azure AD B2C — выберите клиент Azure AD B2c раскрывающемся hello.  Отображаются только допустимые клиенты Azure AD B2C.  Подходящих клиентов B2C удовлетворяют этим условиям: hello глобальный администратор клиента hello B2C и hello B2C клиента не является в настоящее время связаны tooan подписки Azure

2. Azure AD B2C ресурс - называется предустановленные toomatch hello доменное имя клиента B2C hello

3. "Подписка". Активная подписка Azure, в которой вы являетесь администратором или соадминистратором.  Несколько клиентов Azure AD B2C могут быть добавлены tooone подписки Azure

4. "Группа ресурсов" и "Расположение группы ресурсов". Эти параметры позволяют создать несколько ресурсов Azure.  Этот выбор не оказывает влияния на расположение, производительность или выставление счетов за клиент B2C.

5. Закрепить toodashboard для простой tooyour B2C доступа клиента, выставление счетов информацию и hello параметры клиента B2C ![Создание ресурса B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Шаг 4. Управление ресурсами клиента B2C (необязательно)
После завершения развертывания новый ресурс «Клиента B2C» создается в целевой группы ресурсов hello и связанных с подпиской Azure.  В списке ресурсов Azure отобразится новый ресурс типа "Клиент B2C".

![Создание ресурса B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Нажимая кнопку hello B2C ресурсов клиента, есть ли возможность
- Выберите данные для выставления счетов tooreview подписки имя. См. раздел "Выставление счетов и использование".
- Нажмите кнопку Параметры Azure AD B2C tooopen новую вкладку браузера непосредственно в клиенте tooyour B2C колонку параметров
- Отправить запрос на техническую поддержку.
- Перемещение вашей tooanother ресурсов клиента B2C tooanother группы ресурсов или подписки Azure.  Плата за использование будет начисляться в подписке Azure, куда перемещен ресурс.

![Параметры ресурсов B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Известные проблемы
- Удаление клиента B2C. При создании клиента B2C удален и создан повторно с hello таким же именем домена, также удалите и повторно создать ресурс «Компоновка» hello с hello таким же именем домена.  Вы увидите это «Привязка» ресурса в разделе «Всех ресурсов» в hello подписки клиента с помощью портала Azure hello.
- Самоназначенные ограничения на региональное расположение ресурсов.  В редких случаях пользователь может установить региональное ограничение на создания ресурсов Azure.  Это ограничение может препятствовать hello Создание hello связь между подпиской Azure и клиента B2C. toomitigate, можно опускать это ограничение.

## <a name="next-steps"></a>Дальнейшие действия
После того как вы выполните эти шаги для каждого клиента B2C, счета за подписку Azure будут выставляться в соответствии с вашим соглашением Azure Direct или Enterprise.
- Просмотр сведений об использовании и выставлении счетов в выбранной подписке Azure
- Просмотрите подробные сведения об использовании день отчетов, с помощью hello [Reporting API использования](active-directory-b2c-reference-usage-reporting-api.md)
