---
title: "aaaAzure условного доступа к Active Directory часто задаваемые вопросы | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о условного доступа в Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Условный доступ к Azure Active Directory: часто задаваемые вопросы

## <a name="which-applications-work-with-conditional-access-policies"></a>Какие приложения работают с политиками условного доступа?

Дополнительные сведения о приложениях, которые работают с политиками условного доступа, см. в статье [Приложения и браузеры, использующие правила условного доступа в Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>Являются ли политики условного доступа обязательными для службы совместной работы B2B и гостевых пользователей?

Политики применяются для пользователей службы совместной работы B2B. Однако в некоторых случаях пользователь может быть требованиям политики может toosatisfy hello. Например, организация гостевого пользователя может не поддерживать многофакторную проверку подлинности. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Политика SharePoint Online также применять tooOneDrive для бизнеса?

Да. Политика SharePoint Online также применяется tooOneDrive для бизнеса.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Почему не удается задать политику для клиентских приложений, таких как Word или Outlook?

Политика условного доступа устанавливает требования для доступа к службе. Происходит при возникновении toothat службы проверки подлинности. не задана политика Hello непосредственно в клиентском приложении. Вместо этого она применяется, когда клиент вызывает службу. Например установленная на сервере SharePoint политика применяется tooclients вызов SharePoint. Установленная на сервере Exchange политика применяется tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Политики условного доступа применяется tooservice учетные записи?

Политики условного доступа применяются tooall учетных записей пользователей. Это относится и к учетным записям пользователей, которые используются как учетные записи служб. Часто учетная запись службы, которая выполняется автоматически не может удовлетворить требования hello политики условного доступа. Например, может потребоваться многофакторная проверка подлинности. Учетные записи служб можно исключить из политики с помощью параметров управления политикой условного доступа. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Доступны ли API Graph для настройки политики условного доступа?

В настоящее время нет. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Какова политика исключения по умолчанию hello для неподдерживаемых платформ?

В настоящее время политики условного доступа применяются избирательно к пользователям устройств iOS и Android. На других платформах по умолчанию не влияет на приложения hello политику условного доступа для устройств iOS и Android. Администратор клиента можно выбрать toousers toooverride hello глобальной политики toodisallow доступ на платформах, которые не поддерживаются.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Как работают политики условного доступа для Microsoft Teams?  

Microsoft Teams в значительной степени зависит от Exchange Online и SharePoint Online в основных сценариях производительности, таких как собрания, календари и совместное использование файлов. Политики условного доступа, заданные для этих облачных приложений применяются tooMicrosoft команды при входе в систему пользователя.

Microsoft Teams также поддерживается отдельно в качестве облачного приложения в политиках условного доступа Azure Active Directory. Политики центр сертификатов, установленных для облачного приложения применяются tooMicrosoft команды при входе в систему пользователя.

Клиенты рабочего стола Microsoft Teams для Windows и Mac поддерживают современные методы проверки подлинности. Современная проверка подлинности использует вход на основе hello Azure Active Directory Authentication библиотеки (ADAL) tooMicrosoft Office клиентских приложений на платформах. 
