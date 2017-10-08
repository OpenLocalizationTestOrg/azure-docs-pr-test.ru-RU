---
title: "aaaUsing tooSaaS доступа toomanage группы приложений | Документы Microsoft"
description: "Как toouse группы в Azure Active Directory Premium или Basic tooassign доступ к tooSaaS приложения, интегрированные с Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>С помощью приложения tooSaaS для доступа к toomanage группы
С помощью Azure Active Directory (Azure AD) с лицензией Azure AD Premium или Azure AD Basic, можно использовать группы tooassign доступа tooa приложению SaaS, которое интегрировано с Azure AD. Например если вы хотите получить доступ tooassign для hello маркетинговый отдел toouse пяти разным приложениям SaaS, можно создать группу, содержащую пользователей hello в отделе маркетинга hello и назначьте этой группе toothese пять приложений SaaS, которые являются требуемые hello отдела маркетинга. Таким образом можно сэкономить время, управление членством hello объекта hello маркетинг отдела в одном месте. Пользователи затем назначаются toohello приложения во время их добавления в качестве членов группы marketing hello и назначениях удалены из приложения hello после их удаления из маркетингового hello.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. 

Эту возможность можно использовать с сотнями приложений, которые можно добавить из в hello коллекции приложений Azure AD.

**tooassign доступ для группы tooa приложения SaaS**

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory** на панели навигации hello hello левой стороны.
2. Выберите hello **каталога** вкладку и откройте hello каталог, в котором нужно tooassign доступ для группы tooa приложения SaaS.
3. Выберите hello **приложений** вкладки. Выберите приложение, которое вы добавили из коллекции приложений hello и нажмите кнопку hello **пользователей и групп** вкладки.
4. На hello **пользователей и групп** hello на вкладке **начиная с** введите имя hello hello группы toowhich нужно tooassign доступ, а затем выберите hello флажок в правом верхнем углу hello. Требуется только tootype hello первую часть имени группы.
5. Выберите группу hello, а затем выберите hello **назначать доступ к** кнопки. Выберите **Да** при появлении сообщения о подтверждении hello. В данный момент вложенных группах не поддерживаются для tooapplications назначения на основе группы.
6. Также вы увидите, какие пользователи назначаются приложения toohello напрямую или через членство в группе. toodo это, измените hello **показывать раскрывающийся список с «Группы»** слишком**«Все пользователи»**. Hello список пользователей в каталоге hello и ли каждому пользователю назначается toohello приложения. Hello также перечислены ли hello назначенных пользователей, назначенных toohello приложению напрямую (тип Inherited «Direct»), или посредством членства в группе (тип Inherited «Inherited.»)

> [!NOTE]
> Вы увидите hello пользователей и группы только после включения Azure AD Premium или Azure AD Basic.
>
>

### <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Настройка параметров групп с помощью командлетов Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Что такое Microsoft Azure Active Directory](active-directory-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
