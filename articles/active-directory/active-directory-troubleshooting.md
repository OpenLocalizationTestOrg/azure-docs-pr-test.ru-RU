---
title: "Устранение неполадок: Элемент «Active Directory» отсутствует или недоступен | Документы Microsoft"
description: "Какие toodo при Active Directory пункт меню не отображается в hello портала управления Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Устранение неполадок: элемент Active Directory отсутствует или недоступен
Многие hello инструкции по использованию функции Azure Active Directory и службы начинаются с «toohello портал управления Azure перейдите и выберите **Active Directory**.» Но что делать, если hello Active Directory расширения или пункта меню не появляется или если он помечен как **недоступно**? Этот раздел является спроектированный toohelp. Здесь описываются условия, при которых hello **Active Directory** отсутствует или недоступен и объясняется, как tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory отсутствует
Как правило **Active Directory** элемент появляется в меню навигации слева hello. инструкции Hello в Azure Active Directory процедуры предполагают, что этот элемент находится в представлении.

![Снимок экрана: Active Directory в Azure](./media/active-directory-troubleshooting/typical-view.png)

элемент Hello Active Directory появляется в hello левом меню навигации, когда любое из следующих условий hello. В противном случае — элемент hello не отображается.

* Hello текущий пользователь вошел с учетной записью Майкрософт (которая ранее называлась Windows Live ID).
  
    ИЛИ
* Hello клиент Windows Azure имеет каталог и hello текущая учетная запись является администратором каталога.
  
    ИЛИ
* Hello клиент Windows Azure имеет по крайней мере одно пространство имен Azure AD Access Control (ACS). Дополнительные сведения см. в статье о [пространстве имен контроля доступа](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    ИЛИ
* Hello клиент Windows Azure имеет хотя бы один поставщик многофакторной проверки подлинности Azure. Дополнительные сведения см. в статье [Администрирование поставщиков Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

пространство имен Access Control или поставщика многофакторной проверки подлинности, щелкните toocreate **+ создать** > **службы приложений** > **Active Directory**.

каталог tooa tooget права администратора, имеют администратора назначить администратора роли tooyour учетную запись. Дополнительные сведения см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory недоступен
Элемент **Active Directory** отобразится, если щелкнуть **+Создать** > **Службы приложений**. В частности элемент hello Active Directory появляется при все возможности Active Directory hello, например каталог, управление доступом или поставщик многофакторной проверки подлинности, доступные toohello текущего пользователя.

Однако во время загрузки страницы приветствия hello элемент будет недоступен и помечен **недоступно**. Это временное состояние. Если подождать несколько секунд, пункт hello станет доступным. Если hello задержка продлевается, обновление hello веб-страницы часто устраняет проблему hello.

![Снимок экрана: Active Directory недоступен](./media/active-directory-troubleshooting/not-available.png)

