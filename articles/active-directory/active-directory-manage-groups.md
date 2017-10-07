---
title: "aaaUse группирует toomanage tooresources доступа в Azure Active Directory | Документы Microsoft"
description: "Как toouse группы в Azure Active Directory toomanage пользователя доступ к tooon локальных и облачных приложений и ресурсы."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Управление tooresources доступ с помощью групп Azure Active Directory
Azure Active Directory (Azure AD) — это комплексный удостоверениями и доступом решение управления, предоставляет широкий набор возможностей toomanage доступа tooon организациями и облачных приложений и ресурсы, включая Microsoft online services, например Office 365 и множеству приложений SaaS, отличных от Майкрософт. В этой статье содержатся общие сведения, но если требуется с помощью Azure AD toostart группирует прямо сейчас, следуйте инструкциям в разделе hello [Управление группами безопасности в Azure AD](active-directory-accessmanagement-manage-groups.md). Если требуется toosee об использовании PowerShell toomanage групп в Azure Active directory, можно прочитать подробнее в [командлеты Azure Active Directory для управления группами](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Azure Active Directory, необходима учетная запись Azure. Если у вас нет учетной записи, вы можете [зарегистрироваться для получения бесплатной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

В Azure AD одной из основных функций hello — tooresources доступа toomanage возможность hello. Эти ресурсы могут быть частью каталога hello, как hello случае разрешения toomanage объектов с помощью ролей в каталоге hello, или ресурсы, внешние toohello каталогом, таким как приложений SaaS, служб Azure и сайтов SharePoint или в локальной среде ресурсы. Существует четыре способа пользователю можно назначить ресурсов tooa права доступа:

1. Прямое назначение

    Пользователей можно назначить непосредственно tooa ресурсов hello владельцем этого ресурса.
2. Членство в группе

    Группу можно назначить ресурсов tooa владельцем ресурса hello и таким образом, предоставление hello члены этой группы доступа toohello ресурсов. Членство группы hello можно будет управляться hello владельца группы hello. По сути делегаты владельца ресурса hello hello разрешение tooassign пользователей tootheir toohello владелец ресурса группы hello.
3. На основе правила

    владелец ресурса Hello можно использовать правила tooexpress, пользователей, которым следует назначить доступ tooa ресурсов. результат Hello hello правила определяется hello атрибуты, используемые в это правило и их значения для определенных пользователей и таким образом, владелец ресурса hello фактически передает hello toomanage правом доступа tootheir ресурсов toohello Авторитетный источник для hello атрибуты, которые используются в правиле hello. владелец ресурса Hello по-прежнему управляет само правило hello и определяет, какие атрибуты и значения предоставляют доступ tootheir ресурс.
4. Внешний источник

    ресурс tooa Hello доступа является производным от внешнего источника; например группа, синхронизируемых из надежного источника, например локального каталога или приложению SaaS, таких как рабочего дня. владелец ресурса Hello назначает ресурс toohello доступа tooprovide группы hello и hello внешнего источника управляет hello члены группы hello.

   ![Обзор схемы управления доступом](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Просмотрите видео, в котором объясняется управление доступом
Видео с более подробными объяснениями:

**Azure AD: Введение toodynamic членство для групп**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Как работает управление доступом в Azure Active Directory
В hello центре hello решение по управлению доступом Azure AD является группой безопасности hello. Использование tooresources доступа toomanage группа безопасности — это распространенный, позволяющий ресурс гибкие и понятным способом доступа tooprovide tooa hello предназначен группы пользователей. владелец ресурса Hello (или администратор hello hello каталога) можно назначить tooprovide группы определенные доступа правой toohello ресурсов которыми они владеют. Hello члены группы hello будет предоставляться доступ hello и владелец ресурса hello можно делегировать правой toomanage hello hello список членов группы toosomeone, else, такие как руководитель отдела или администратор службы технической поддержки.

![Схема управления доступом Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

Hello владельцем группы можно также предоставить этой группе запросы самообслуживания. При этом конечному пользователю можно искать и hello группы и toojoin запрос эффективного поиска разрешение tooaccess hello ресурсы, которые управляются с помощью группы hello. Hello владельца hello группы можно настроить группы hello, чтобы запросы соединения утверждаются автоматически, или требуют утверждения владельцем hello hello группы. Когда пользователь создает запрос toojoin группу, hello соединения запрос перенаправляется toohello владельцев группы hello. Если один владельцев hello утверждает запрос hello, hello запрашивающий пользователь получает уведомление, и пользователь hello является группы объединенных toohello. Если один владельцев hello отклоняет запрос hello, запрашивающего пользователя hello уведомляется, но не входящих в группу toohello.

## <a name="getting-started-with-access-management"></a>Приступая к работе с управлением доступом
Tooget готова к работе? Попробуйте некоторые hello основные задачи, которые можно выполнить с группами Azure AD. Используйте специализированные tooprovide эти возможности получить доступ к toodifferent групп пользователей для разных ресурсов в вашей организации. Ниже перечислены первые основные шаги.

* [Создание простого правила tooconfigure динамическое членство в группе](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [С помощью приложения tooSaaS для доступа к toomanage группы](active-directory-accessmanagement-group-saasapps.md)
* [Включение функции самообслуживания для пользователей группы](active-directory-accessmanagement-self-service-group-management.md)
* [Идет синхронизация tooAzure локальной группы, с помощью Azure AD Connect](active-directory-aadconnect.md)
* [Управление владельцами группы](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Дальнейшие действия
Теперь понятны hello основы управления доступом здесь доступны некоторые дополнительные расширенные возможности в Azure Active Directory для управления tooyour получать доступ к приложениям и ресурсам.

* [При помощи атрибутов toocreate расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Управление группами безопасности в Azure Active Directory](active-directory-accessmanagement-manage-groups.md)
* [Настройка выделенных групп в Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md)
* [Справочник по API Graph для групп](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Настройка параметров групп с помощью командлетов Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
