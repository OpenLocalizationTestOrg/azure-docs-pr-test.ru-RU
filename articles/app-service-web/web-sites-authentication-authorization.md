---
title: "aaaAuthenticate с локальной Active Directory в приложении Azure | Документы Microsoft"
description: "Дополнительные сведения о различных параметрах hello для бизнес приложений в службе приложений Azure tooauthenticate с локальной Active Directory"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Проверка подлинности в приложении Azure с помощью локального каталога Active Directory
В этой статье показано, как tooauthenticate с локальной Active Directory (AD) в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md). Приложения Azure размещается в облаке hello, но существуют способы tooauthenticate локальных пользователей AD безопасно. 

## <a name="authenticate-through-azure-active-directory"></a>Проверка подлинности с помощью Azure Active Directory
Клиент Azure Active Directory можно синхронизировать с локальным каталогом AD. Такой подход дает пользователям доступ к вашему приложению из AD hello Интернета и пройти проверку подлинности с использованием учетных данных в локальной среде. Кроме того, служба приложений Azure предоставляет [готовое решение для этого метода](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Нажав несколько кнопок, вы можете включить проверку подлинности для приложения Azure с помощью клиента, синхронизированного с каталогом. Такой подход имеет следующие преимущества hello.

* Не требуется код проверки подлинности в приложении. Разрешить службы приложения hello за проверку подлинности и тратить время на предоставление функциональных возможностей в приложении.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) обеспечивает доступ к данным toodirectory из приложения Azure.
* Предоставляет SSO слишком[всех приложений, совместимых с Azure Active Directory](/marketplace/active-directory/), включая Office 365, Dynamics CRM Online, Microsoft Intune и тысячам сторонних облачных приложений. 
* Azure Active Directory поддерживает управление доступом на основе ролей. Можно использовать шаблон hello [Authorize(Roles="X")] с минимальными изменениями кода tooyour.

toowrite бизнес приложения Azure, выполняющий проверку подлинности в Azure Active Directory. в статье toosee [Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Проверка подлинности с помощью локальной службы маркеров безопасности
При наличии локальной службой маркеров безопасности (STS) как службы федерации Active Directory (AD FS), что проверка подлинности toofederate можно использовать для приложения Azure. Этот метод лучше всего подходит, если политика компании запрещает хранить данные AD в Azure. Тем не менее Обратите внимание hello следующее:

* Топологию службы маркеров безопасности необходимо развертывать локально с учетом затрат и расходов на управление.
* Только администраторы AD FS можно настроить [проверяющей стороны отношения доверия и правила утверждений](http://technet.microsoft.com/library/dd807108.aspx), которой может привести к ограничению параметров разработчика hello. На hello другой стороны, его возможных toomanage и настраивать [утверждений](http://technet.microsoft.com/library/ee913571.aspx) отдельно для каждого приложения.
* Доступ к локальной tooon AD данных требуется отдельное решение через корпоративный брандмауэр hello.

статье toowrite бизнес-приложения Azure, который выполняет проверку подлинности с локальным STS, toosee [Создание бизнес-приложения Azure с проверкой подлинности AD FS](web-sites-dotnet-lob-application-adfs.md).

