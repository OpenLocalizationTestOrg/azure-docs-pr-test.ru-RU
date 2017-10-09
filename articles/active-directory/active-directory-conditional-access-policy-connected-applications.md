---
title: "политики условного доступа на основе устройств Azure Active Directory aaaConfigure | Документы Microsoft"
description: "Узнайте, как политики tooconfigure Azure Active Directory на основе устройств условного доступа."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Настройка политик условного доступа на основе устройств для Azure Active Directory

Благодаря [условному доступу Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md) можно настроить доступ авторизованных пользователей к вашим ресурсам. Например вы ограничиваете hello доступа toocertain ресурсов tootrusted устройств. Политика условного доступа, требующая доверенного устройства, также называется политикой условного доступа на основе устройств.

Этот раздел предоставляет сведения в как условное устройства под управлением tooconfigure политик доступа для приложения Azure AD подключен. 


## <a name="before-you-begin"></a>Перед началом работы

Условный доступ на основе устройств объединяет **условный доступ Azure AD** и **управление устройствами Azure AD**. Если вы еще не знакомы с одной из этих областей, следует прочитать следующие разделы, сначала hello:

- **[Условный доступ в Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -в этом разделе содержится с концептуальный обзор условного доступа и hello связанной терминологии.

- **[Управление toodevice введение в Azure Active Directory](device-management-introduction.md)**  -в этом разделе дается обзор hello различных параметров у вас есть tooconnect устройствами с помощью Azure AD. 


## <a name="trusted-devices"></a>Доверенные устройства

В мире mobile сначала, облачный Azure Active Directory позволяет-toodevices приложений и служб из любого места. Для некоторых ресурсов в вашей среде, предоставление доступа toohello пользователи не вполне достаточно. В дополнение к этому toohello пользователи, вы может также потребоваться toobe доверенного устройства используемых tooaccess ресурса. В вашей среде, можно определить, какие доверенное устройство, основываясь на hello следующие компоненты:

- Hello [платформ устройств](active-directory-conditional-access-azure-portal.md#device-platforms) на устройстве
- Является ли устройство совместимым.
- Подключено ли устройство к домену. 

Hello [платформ устройств](active-directory-conditional-access-azure-portal.md#device-platforms) характеризуется hello операционной системы, на котором работает на вашем устройстве. В политике условного доступа на основе устройств можно ограничить доступ toocertain ресурсов toospecific платформах.



В политике условного доступа на основе устройств может потребоваться toobe доверенных устройств, помеченные как соответствующие требованиям.

![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Устройства могут быть помечены как совместимые в каталоге hello по:

- Intune 
- Сторонней системы управления мобильными устройствами, интегрируемой с Azure AD.  

Только устройства, подключенного tooAzure AD может быть помечен как соответствующий. tooconnect устройства tooAzure Active Directory, у вас есть hello следующие параметры: 

- регистрация в Azure AD;
- присоединение к Azure AD;
- присоединение к Azure AD (гибридные устройства).

    ![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Если у вас есть локально занимаемое место Active Directory (AD), может потребоваться устройства, не подключенного tooAzure AD, но доверенных toobe tooyour присоединены к домену AD.

![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Дальнейшие действия

Перед настройкой политики условного доступа на основе устройств в вашей среде, следует рассмотреть hello [советы и рекомендации для условного доступа в Azure Active Directory](active-directory-conditional-access-best-practices.md).

