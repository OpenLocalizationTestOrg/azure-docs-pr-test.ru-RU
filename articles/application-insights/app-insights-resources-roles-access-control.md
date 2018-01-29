---
title: "Ресурсы, роли и контроль доступа в Azure Application Insights | Документация Майкрософт"
description: "Владельцы, участники и читатели Insights вашей организации."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: mbullwin
ms.openlocfilehash: 6e811c9b427469fa781cf1f5b7c7deff3a8e6eb3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Ресурсы, роли и контроль доступа в Application Insights
Вы можете управлять доступом на чтение и обновлять права доступа к данным в Azure [Application Insights][start], используя [Управление доступом на основе ролей в Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Вы также можете предоставлять доступ пользователям в **группе ресурсов или подписке** , к которым относится ресурс приложения, а не в самом ресурсе. Назначьте им роль **участника компонента Application Insights** . Это обеспечит универсальный контроль доступа к веб-тестам и оповещениям с помощью ресурса приложения. [Подробнее](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Ресурсы, группы и подписки
Сначала рассмотрим некоторые определения:

* **Ресурс** — это экземпляр службы Microsoft Azure. Ресурс Application Insights собирает, анализирует и отображает данные телеметрии, отправленные приложением.  Другие типы ресурсов Azure включают в себя веб-приложения, базы данных и виртуальные машины.
  
    Чтобы просмотреть свои ресурсы, откройте [портал Azure][portal], выполните вход и щелкните "Все ресурсы". Чтобы найти ресурс, введите часть его имени в поле фильтра.
  
    ![Список ресурсов Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Группа ресурсов**][group] — каждый ресурс принадлежит одной группе. Создание группы — это удобный способ управления связанными ресурсами, особенно для контроля доступа. Например, в одну группу ресурсов можно поместить веб-приложение и ресурс Application Insights для мониторинга приложения, а также ресурс хранилища для хранения экспортированных данных.

    ![Выберите «Обзор», «Группы ресурсов», а затем выберите группу](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Подписка**](https://portal.azure.com). Чтобы использовать Application Insights или другие ресурсы Azure, войдите в подписку Azure. Каждая группа ресурсов относится к одной подписке Azure, где вы выбираете пакет по цене и, при использовании подписки для организации, выбираете участников и права доступа для них.
* [**Учетная запись Майкрософт**][account] — имя пользователя и пароль, используемые для входа в подписки Microsoft Azure, Xbox Live, Outlook.com и другие службы Майкрософт.

## <a name="access"></a> Контроль доступа в группе ресурсов
Важно понимать, что кроме ресурса, созданного для приложения, существуют также отдельные скрытые ресурсы для оповещений и веб-тестов. Они вложены в ту же [группу ресурсов](#resource-group) , что и ваше приложение. В нее также можно поместить другие службы Azure, такие как веб-сайты или службы хранилища.

![Ресурсы в Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

Поэтому для контроля доступа к этим ресурсам рекомендуем:

* осуществлять контроль доступа на уровне **группы ресурсов или подписки** ;
* назначать пользователям роль **участника компонента Application Insights** . Это позволяет изменять веб-тесты, оповещения и ресурсы Application Insights, не предоставляя доступ к другим службам в группе.

## <a name="to-provide-access-to-another-user"></a>Предоставление доступа другому пользователю
Для этого у вас должны быть права владельца подписки или группы ресурсов.

У пользователя должна быть [учетная запись Майкрософт][account] или доступ к [корпоративной учетной записи Майкрософт](../active-directory/sign-up-organization.md). Вы можете предоставлять доступ отдельным пользователям и группам пользователей, определенным в Azure Active Directory.

#### <a name="navigate-to-the-resource-group"></a>Переход к группе ресурсов
Добавьте в нее пользователя.

![В колонке ресурсов приложения откройте «Основные компоненты», откройте группу ресурсов и выберите параметры или пользователей. Нажмите Добавить.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Вы также можете перейти на уровень выше и добавить пользователя в подписку.

#### <a name="select-a-role"></a>Выбор роли
![Выберите роль для нового пользователя](./media/app-insights-resources-roles-access-control/03-role.png)

| Роль | В группе ресурсов |
| --- | --- |
| Владелец. |Можно менять любые параметры, в том числе права доступа пользователей |
| участник; |Можно изменять любое содержимое, в том числе любые ресурсы |
| участника компонента Application Insights |Можно изменять ресурсы, веб-тесты и оповещения Application Insights |
| Читатель |Можно просматривать содержимое, но нельзя ничего изменять |

«Изменение» включает в себя создание, удаление и обновление:

* Ресурсы
* Веб-тесты
* Оповещения
* непрерывный экспорт.

#### <a name="select-the-user"></a>Выбор пользователя

Если в каталоге нет необходимого пользователя, вы можете пригласить любого пользователя с учетной записью Майкрософт
(если он использует такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у него есть учетная запись Майкрософт).

## <a name="related-content"></a>Связанная информация

* [Управление доступом на основе ролей в Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
