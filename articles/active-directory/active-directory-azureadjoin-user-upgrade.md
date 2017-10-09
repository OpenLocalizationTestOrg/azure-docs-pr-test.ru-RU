---
title: "aaaSet устройства Windows 10 с Azure AD из параметров | Документы Microsoft"
description: "Объясняет, как пользователи могут присоединять tooAzure AD через меню \"настройки\" hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Настройка устройства с Windows 10 для работы с Azure AD с помощью меню «Параметры»
Если вы уже использование Windows 7 или Windows 8 и этот компьютер или устройство было обновленного tooWindows 10, вы можете присоединиться к tooAzure Active Directory (Azure AD) через меню "настройки" hello.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>tooAzure toojoin AD из меню параметров hello
1. Из hello **запустить** меню, щелкните hello **параметры** чудо-кнопку.
2. В разделе **Параметры** выберите **Система**->**About** (О системе)->**Присоединиться к Azure AD**.
   
   <center>
   ![Присоединение Azure AD из меню параметров hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Нажмите кнопку **Продолжить** в окне сообщения hello-присоединения Azure AD.
   
   <center>
   ![Окно сообщения о присоединении к Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. Введите учетные данные для входа. Это входа в систему будет включать все hello шаги, необходимые toocomplete проверки подлинности. Если вы являетесь частью федеративного клиента, администратору будет предоставления возможностей федерации hello, размещенному в вашей организации.
   <center>
   ![Ввод учетных данных для входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. Если ваша организация настроил многофакторной проверки подлинности Azure для присоединения tooAzure AD, предоставляют hello второй фактор, прежде чем продолжить.
6. Нажмите кнопку **Accept** на hello **разрешить этот toobe устройства управляемых** экрана.
7. Должно появиться сообщение hello, «устройство теперь не присоединены к домену tooyour организации в Azure AD».

## <a name="additional-information"></a>Дополнительная информация
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)
* [Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport](active-directory-azureadjoin-passport.md)

