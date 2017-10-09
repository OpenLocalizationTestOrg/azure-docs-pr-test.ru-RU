---
title: "Установка расширения браузера панели доступа приложения hello aaaProblem | Документы Microsoft"
description: "Как toofix распространенных ошибок при установке расширения браузера панели доступа hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Проблема при установке расширения браузера панели доступа приложения hello

Hello панель доступа является Интернет-порталом, который дает возможность пользователя, имеющего рабочей или учебной учетной записи в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, администратор hello Azure AD предоставил им доступ к. Пользователь, имеющий выпуски Azure AD можно также использовать группы самообслуживания и возможности управления приложениями через панель доступа hello. Панель доступа Hello отделен от hello портал Azure и не требует toohave пользователей подписки Azure.

toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello. Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Соответствующие требования к браузеру для hello панели доступа

Hello панели доступа требуется браузер, поддерживающий JavaScript и CSS включена. toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello. Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.

Для единого входа по паролю может быть браузеров hello конечных пользователей:

-   Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);

-   Edge в Windows 10 Anniversary Edition или более поздней версии; 

-   Chrome (начиная с Windows 7 и Mac OS X);

-   Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Как tooinstall hello расширение обозревателя панели доступа

hello tooinstall расширение обозревателя панели доступа, следуйте инструкциям hello:

1.  Откройте hello [панели доступа](https://myapps.microsoft.com) в одном hello поддерживаемых браузеров и входа в качестве **пользователя** в Azure AD.

2.  Нажмите кнопку **SSO на ОСНОВЕ пароля приложения** в hello панели доступа.

3.  В hello запрос запросом tooinstall hello программного обеспечения, выберите **установить сейчас**.

4.  На основе браузера можно направленной toohello ссылку для скачивания. **Добавить** браузер tooyour расширений hello.

5.  Если браузер запрашивает, выберите tooeither **включить** или **Разрешить** hello расширения.

6.  После установки **перезапустите** сеанс браузера.

7.  Войдите в панель доступа hello и разделе, если вы можете **запуска** приложения SSO на ОСНОВЕ пароля

Можно также загрузить расширения hello для Chrome и границей из hello прямые ссылки ниже:

-   [Расширение "Панель доступа" для Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Расширение "Панель доступа" для Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Настройка групповой политики для Internet Explorer

Вы можете настроить групповой политики, которые позволяют вам tooremotely установки hello расширение для Internet Explorer на компьютерах пользователей.

Предварительные требования Hello включают следующие:

-   Вы настроили [доменных служб Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), и вы присоединились к домену tooyour машин пользователей.

-   Необходимо иметь hello «Изменить параметры» разрешение tooedit hello объекта групповой политики (GPO). По умолчанию это разрешение имеют члены элемента hello следующие группы безопасности: Администраторы домена "," Администраторы предприятия "и" Владельцы-создатели групповой политики. [Подробнее](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Выполните действия из учебника hello [как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md) пошаговые инструкции по как tooconfigure hello групповую политику и развернуть ее toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Устранение неполадок hello панели доступа в Internet Explorer

Выполните hello [Устранение hello расширение панели доступа для Internet Explorer](active-directory-saas-ie-troubleshooting.md) руководстве доступ средства диагностики и пошаговые инструкции по настройке расширения hello для IE.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Если эти шаги по устранению неполадок не решат проблему hello

Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:

-   идентификатор ошибки корреляции;

-   имя участника-пользователя (адрес электронной почты пользователя);

-   идентификатор клиента;

-   тип браузера;

-   часовой пояс и время или отрезок времени возникновения ошибки;

-   трассировки Fiddler.

## <a name="next-steps"></a>Дальнейшие действия
[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
