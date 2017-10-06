---
title: "Общие сведения о состоянии aaaEnterprise перемещаемые | Документы Microsoft"
description: "Здесь содержится информация о параметрах Enterprise State Roaming для устройств Windows. Enterprise State Roaming пользователям предоставляются унифицированного интерфейса на своих устройствах Windows и снижает hello время, необходимое для настройки нового устройства."
services: active-directory
keywords: "что такое Enterprise State Roaming, корпоративная синхронизация, облако Windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Обзор службы Enterprise State Roaming
С Windows 10 [Azure Active Directory (Azure AD)](active-directory-whatis.md) hello возможности пользователей рост toosecurely синхронизировать их параметров пользователя и облако toohello данных параметров приложения. Enterprise State Roaming пользователям предоставляются унифицированного интерфейса на своих устройствах Windows и снижает hello время, необходимое для настройки нового устройства. Enterprise State Roaming работает аналогично standard toohello [синхронизация параметров потребителя](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) , впервые появившийся в Windows 8. Кроме того, Enterprise State Roaming обеспечивает следующее:

* **Разделение корпоративных и потребительских данных**. Организации управляют своими данными, поэтому корпоративные данные не попадают в облачную учетную запись потребителя, а данные потребителя — в корпоративную облачную учетную запись.
* **Усиленная безопасность** — данные автоматически шифруются перед выходом из устройства Windows 10 hello пользователя с помощью Azure Rights Management (Azure RMS), и данные остаются шифруются в неактивном состоянии в облаке hello. Все содержимое остается зашифрованным, хранящихся в облаке hello, за исключением hello пространства имен, такие как имена параметров и имена приложений Windows.  
* **Более высокий уровень управления и мониторинга** — обеспечивает возможность управления и просмотра, синхронизируется параметры в вашей организации и на каких устройствах через интеграцию с портала Azure AD hello. 

Служба Enterprise State Roaming доступна в различных регионах Azure. Можно найти hello обновить список доступных регионов на hello [служб Azure в регионах](https://azure.microsoft.com/regions/#services) страницы в Azure Active Directory.

| Статья | Описание |
| --- | --- |
| [Включение службы Enterprise State Roaming в Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md) |Enterprise State Roaming — доступные tooany организация с подпиской Premium Azure Active Directory (Azure AD). Дополнительные сведения о том, как tooget подписка на Azure AD, в разделе hello [продукта Azure AD](https://azure.microsoft.com/services/active-directory) страницы. |
| [Часто задаваемые вопросы о перемещении параметров и данных](active-directory-windows-enterprise-state-roaming-faqs.md) |В этой статье содержится информация о синхронизации параметров и данных приложений, которая может быть полезной для ИТ-администраторов. |
| [Group policy and MDM settings for settings sync (Параметры групповой политики и управления мобильными устройствами)](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 предоставляет групповой политики и синхронизация параметров toolimit параметры политики мобильных устройств management (MDM). |
| [Справочник по перемещаемым параметрам в Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |Hello ниже приведен полный список всех параметров hello, которые будут иметь перемещаться и (или) резервных копий в Windows 10. |
| [Устранение неполадок](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |В этом разделе представлены основные инструкции по устранению неполадок, а также список известных проблем. |

