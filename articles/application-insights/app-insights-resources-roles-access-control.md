---
title: "aaaResources, ролей и управление доступом в Azure Application Insights | Документы Microsoft"
description: "Владельцы, участники и читатели Insights вашей организации."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Ресурсы, роли и контроль доступа в Application Insights
Можно управлять, чтение и обновление данных tooyour доступа в Azure [Application Insights][start], с помощью [управление доступом на основе ролей в Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Назначить доступ toousers в hello **группу ресурсов или подписку** toowhich - не в сам ресурс hello принадлежит ресурс приложения. Назначить hello **участника компонента Application Insights** роли. Это обеспечивает универсальный элемент управления доступа tooweb тестов и оповещения вместе с приложением ресурс. [Подробнее](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Ресурсы, группы и подписки
Сначала рассмотрим некоторые определения:

* **Ресурс** — это экземпляр службы Microsoft Azure. Ресурс Application Insights собирает и анализирует отображает hello данные телеметрии, отправленные из приложения.  Другие типы ресурсов Azure включают в себя веб-приложения, базы данных и виртуальные машины.
  
    toosee ресурсов, откройте hello [портала Azure][portal], войдите и выберите все ресурсы. toofind ресурса, тип часть его имени в поле фильтра hello.
  
    ![Список ресурсов Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Группа ресурсов** ] [ group] -каждый ресурс принадлежит tooone группы. Группа не является удобным способом toomanage связанных ресурсов, особенно для управления доступом. Например в один ресурс группы, можно поместить веб-приложения, приложения hello toomonitor ресурса Application Insights и tookeep ресурсов хранения экспортированных данных.

    ![Выберите «Обзор», «Группы ресурсов», а затем выберите группу](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Подписки** ](https://manage.windowsazure.com) -toouse Application Insights или другим ресурсам Azure, вход tooan подписки Azure. Каждая группа ресурсов принадлежит tooone подписки Azure, где выберите пакет цены, если подписка на организации, выберите hello членов и разрешений доступа.
* [**Учетная запись Майкрософт** ] [ account] -hello имени пользователя и пароля, используемых в tooMicrosoft Azure toosign подписок, XBox Live, Outlook.com и другие службы Майкрософт.

## <a name="access"></a>Управление доступом в группе ресурсов hello
Это важные toounderstand, что в сложения toohello созданный ресурс для приложения, существует также разделения скрытые ресурсы для оповещений и веб-тестов. Они являются вложенного toohello же [группы ресурсов](#resource-group) с приложением. В нее также можно поместить другие службы Azure, такие как веб-сайты или службы хранилища.

![Ресурсы в Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

ресурсы toothese toocontrol доступа, поэтому рекомендуется для:

* Управление доступом на hello **группу ресурсов или подписку** уровне.
* Назначить hello **участника компонента аналитики приложений** toousers роли. Это позволяет им tooedit веб-тесты, оповещения и ресурсы Application Insights, без предоставления доступа tooany другие службы в группе hello.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide доступа tooanother пользователей
Необходимо иметь подписку toohello права владельца или группа ресурсов hello.

Hello пользователь должен иметь [учетную запись Майкрософт][account], или доступ к tootheir [учетная запись организации Microsoft](../active-directory/sign-up-organization.md). Чтобы обеспечить доступ tooindividuals и toouser группы, определенные в Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Перейдите в группу ресурсов toohello
Добавьте hello пользователя существует.

![В колонке ресурсов приложения откройте Essentials, откройте группу ресурсов hello и существует выберите параметры и пользователей. Нажмите Добавить.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Или можно перейти вверх другого уровня и добавить пользователя hello toohello подписки.

#### <a name="select-a-role"></a>Выбор роли
![Выберите роль для нового пользователя hello](./media/app-insights-resources-roles-access-control/03-role.png)

| Роль | В группе ресурсов hello |
| --- | --- |
| Владелец |Можно менять любые параметры, в том числе права доступа пользователей |
| Участник |Можно изменять любое содержимое, в том числе любые ресурсы |
| участника компонента Application Insights |Можно изменять ресурсы, веб-тесты и оповещения Application Insights |
| Читатель |Можно просматривать содержимое, но нельзя ничего изменять |

«Изменение» включает в себя создание, удаление и обновление:

* Ресурсы
* Веб-тесты
* Оповещения
* непрерывный экспорт.

#### <a name="select-hello-user"></a>Выберите пользователя hello

Если hello пользователя отсутствует в каталоге hello, вы можете пригласить любой пользователь с учетной записью Майкрософт.
(если он использует такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у него есть учетная запись Майкрософт).

## <a name="related-content"></a>Связанная информация

* [Управление доступом на основе ролей в Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
