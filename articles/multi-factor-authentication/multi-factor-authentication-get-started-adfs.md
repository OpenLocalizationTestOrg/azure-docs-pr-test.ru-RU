---
title: "aaaTwo шаг проверки и AD FS - многофакторной проверки Подлинности Azure | Документы Microsoft"
description: "Это страница hello Azure многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA и AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Приступая к работе со службой Azure Multi-Factor Authentication и службами федерации Active Directory
<center>![Облако](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Если в организации создана федерация локальной службы Active Directory со службой Azure Active Directory с помощью служб федерации Active Directory, доступны два варианта использования Многофакторной идентификации Azure.

* Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб федерации Active Directory
* Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication

Привет, в следующей таблице приведена сводка hello проверки взаимодействия между защищаемых ресурсов с помощью многофакторной проверки подлинности Azure и AD FS

| Проверка для браузерных приложений | Проверка для небраузерных приложений |
|:--- |:--- |:--- |
| Защита ресурсов Azure AD с помощью Azure Multi-Factor Authentication |<li>Первый шаг проверки Hello выполняется локально с помощью AD FS.</li> <li>второй шаг Hello — по телефону, выполняются с помощью проверки подлинности в облаке.</li> |
| Защита ресурсов Azure AD с помощью служб федерации Active Directory |<li>Первый шаг проверки Hello выполняется локально с помощью AD FS.</li><li>второй шаг Hello — выполняется локально путем выполнения утверждения hello.</li> |

Разъяснения касательно паролей приложений для федеративных пользователей.

* Пароли приложений проверяются с использованием облачной проверки подлинности и, следовательно, обходят федерацию. Федерация активно используется только при настройке пароля приложения.
* Параметры контроля доступа локальных клиентов не учитываются при использовании паролей приложений.
* У вас нет возможности вести журнал локальной проверки подлинности для паролей приложений.
* Отключение или удаление учетной записи может занять toothree часов для синхронизации каталогов, задержкой отключения/удаления пароли приложений в удостоверении облака hello.

## <a name="next-steps"></a>Дальнейшие действия
Сведения о настройке многофакторной проверки подлинности Azure или hello сервера Azure Multi-factor Authentication с AD FS см. следующие статьи hello:

* [Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и сервера Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
