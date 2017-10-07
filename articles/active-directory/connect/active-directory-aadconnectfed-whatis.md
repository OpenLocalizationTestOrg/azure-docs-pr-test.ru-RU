---
title: "aaaAzure AD Connect и федерации | Документы Microsoft"
description: "Данная страница является hello центрального расположения для всей документации об операциях службы федерации Active Directory, использующих Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect и федерация
Azure Active Directory (Azure AD) Connect позволяет настроить федерацию с локальными службами федерации Active Directory (AD FS) и Azure AD. Федерации входа в систему можно включить toosign пользователей в службах AD под управлением tooAzure со своими локальными паролями — и, в корпоративной сети hello, без необходимости tooenter свои пароли еще раз. С помощью параметра hello федерации с AD FS, можно развернуть новую установку AD FS, или можно указать существующую установку в ферме Windows Server 2012 R2.

В этом разделе — hello домашней сведения о функциями федерации для Azure AD Connect. Он содержит список tooall связанные разделы. Для ссылки tooAzure AD Connect, в разделе [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Статьи об Azure AD Connect и федерации
| Раздел | Она охватывает и когда tooread его |
|:--- |:--- |
| **Параметры входа в Azure AD Connect** | |
| [Параметры входа в Azure AD Connect](active-directory-aadconnect-user-signin.md) |Дополнительные сведения о различных параметров вход пользователя и их влияние на взаимодействие с пользователем hello Azure вход. |
| **Установка AD FS с помощью Azure AD Connect** | |
| [Предварительные требования](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |См. предварительные требования hello для успешной установки службы федерации Active Directory через Azure AD Connect. |
| [Настройка федерации с AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Установка новой фермы AD FS с помощью Azure AD Connect. |
| [Федерация с Azure AD с помощью альтернативного имени пользователя](active-directory-aadconnect-federation-management.md#alternateid) | Настройка федерации с использованием альтернативного имени пользователя.  |
| **Изменение конфигурации hello AD FS** | |
| [Восстановите доверие hello](active-directory-aadconnect-federation-management.md#repairthetrust) |Восстановление hello текущей доверия между локальной AD FS и Office 365 или Azure. |
| [Добавление сервера AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Добавление к ферме AD FS дополнительных серверов AD FS после начальной установки. |
| [Добавление прокси-сервера веб-приложения AD FS](active-directory-aadconnect-federation-management.md#addwapserver) |Добавление к ферме AD FS дополнительного сервера прокси-службы веб-приложения (WAP) после начальной установки. |
| [Добавление нового федеративного домена](active-directory-aadconnect-federation-management.md#addfeddomain) |Добавьте другой toobe домена в федерацию с Azure AD. |
| [Обновить сертификат SSL hello](active-directory-aadconnectfed-ssl-update.md)| Обновите hello SSL-сертификат для фермы AD FS. |
| **Другая конфигурация федерации** | |
| [Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Федерация нескольких экземпляров Azure AD с одной фермой AD FS.| 
| [Добавление настраиваемого логотипа компании или иллюстрации](active-directory-aadconnect-federation-management.md#customlogo) |Измените hello входа в систему, указав hello логотип, отображаемый на hello AD FS на странице входа. |
| [Добавление описания входа в систему](active-directory-aadconnect-federation-management.md#addsignindescription) |Изменить hello описание на страницу входа AD FS hello. |
| [Изменение правил утверждений служб федерации Active Directory](active-directory-aadconnect-federation-management.md#modclaims) |Изменение или добавление правил для утверждений в AD FS, которые соответствуют конфигурация синхронизации tooAzure AD Connect. |


## <a name="additional-resources"></a>Дополнительные ресурсы
* [Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Развертывание AD FS в Azure](active-directory-aadconnect-azure-adfs.md)
* [Развертывание AD FS высокого уровня доступности в нескольких регионах Azure с помощью диспетчера трафика Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
