---
title: "aaaVulnerabilities, обнаруживаемые службой защиты идентификации Active Directory Azure | Документы Microsoft"
description: "Обзор hello уязвимостей, обнаруживаемые службой защиты идентификации Active Directory Azure."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory
Уязвимости — это слабые стороны среды, которыми могут воспользоваться злоумышленники. Корпорация Майкрософт рекомендует устранить эти уязвимости tooimprove hello уровня безопасности вашей организации и предотвратить их использование злоумышленниками.


![уязвимости](./media/active-directory-identityprotection-vulnerabilities/101.png "уязвимости")



Hello следующие разделы предоставляют обзор hello уязвимостей, сообщаемые защиту учетных данных.

## <a name="multi-factor-authentication-registration-not-configured"></a>Регистрация с многофакторной проверкой подлинности не настроена
Эта уязвимость позволяет контролировать развертывание hello многофакторной проверки подлинности Azure в вашей организации. 

Azure Multi-factor authentication предоставляет второго уровня проверки подлинности, toouser. Помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему. Служба обеспечивает строгую проверку подлинности с помощью простых способов проверки — телефонного звонка, текстового сообщения, уведомления в мобильном приложении, кода подтверждения или OATH-токенов третьей стороны.

Мы рекомендуем настроить обязательную проверку Azure Multi-Factor Authentication при входе пользователей. Multi-Factor Authentication играет основную роль в основанных на рисках политиках условного доступа в защите идентификации.

Дополнительные сведения см. в статье [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Неуправляемые облачные приложения
Благодаря этой уязвимости можно выявить неуправляемые облачные приложения в организации.

На современных предприятиях ИТ-отделы часто не уведомлены о всех hello облачных приложений, пользователи в организации используется toodo свою работу. Это легко toosee, почему Администраторы бы обеспокоены toocorporate несанкционированного доступа к данным, возможными утечками данных и других угроз безопасности. 

Рекомендуется организации развертывание Cloud App Discovery toodiscover неуправляемого облачных приложений и toomanage эти приложения с помощью Azure Active Directory.

Дополнительные сведения см. в статье [Поиск неуправляемых облачных приложений с помощью Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Оповещения системы безопасности в рамках управления привилегированными пользователями
Эта уязвимость способствует обнаружению и устранению оповещений о привилегированных удостоверениях в организации.  

toocarry пользователи tooenable привилегированных операций, организациям необходимы временным или постоянным привилегированным доступом в Azure AD пользователи toogrant ресурсы Azure или Office 365 или другими приложениями SaaS. Каждый из этих привилегированных пользователей увеличивается hello возможных направлений атак вашей организации. Эта уязвимость позволяет идентифицировать пользователей с ненужные уровнем доступа и принимать соответствующие меры tooreduce или избежать hello, они могут представлять. 

Корпорация Майкрософт рекомендует, чтобы ваша организация использует toomanage Azure AD Privileged Identity Management, управления и монитор привилегированных удостоверений и их tooresources доступа в Azure AD, а также другие Microsoft online services, например Office 365 или Microsoft Intune.

Дополнительные сведения см. в статье [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Дополнительные материалы
* [Защита идентификации Azure Active Directory.](active-directory-identityprotection.md)

