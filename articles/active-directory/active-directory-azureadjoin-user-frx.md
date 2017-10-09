---
title: "aaaSet новые устройства в Azure AD во время установки | Документы Microsoft"
description: "В этом разделе объясняется, как пользователи могут настроить присоединение к Azure AD в процессе запуска при первом включении компьютера."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Настройка нового устройства под управлением Windows 10 для работы с Azure AD
В Windows 10 пользователей можно соединить их устройства tooAzure Active Directory (Azure AD) в hello при первом запуске (FRX). Это позволяет организациям toodistribute упакованной со сжатием устройств tootheir сотрудников или студентов или позволить им Выбор свои собственные устройства (CYOD).
Если выпусков Windows 10 Профессиональная или Windows 10 Корпоративная установлено на устройстве, hello возникновение процесс установки toohello значения по умолчанию для устройств, принадлежащих компании.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin устройства tooAzure AD
1. Если включить новое устройство и запустить процесс установки hello, вы увидите hello **Подготовка** сообщения. Выполните tooset приглашения hello вашего устройства.
2. Для начала выберите свой регион и язык. Затем примите условия лицензии программного обеспечения Microsoft hello.
   ![Настройка для вашего региона](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Выберите сеть hello требуется toouse для подключения toohello Интернета.
4. Укажите, является ли ваше устройство личным или корпоративным. Если это принадлежащие компании, выберите **это устройство принадлежит организации toomy**. Это запускает процесс присоединения AD Azure hello. В ОС Windows 10 Профессиональная экран будет выглядеть так:
   <center>
   ![Владелец экрана ПК](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Введите учетные данные hello, предоставленные tooyou вашей организацией.
   <center>
   ![Экран входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. После ввода имени пользователя в Azure AD выполняется поиск соответствующего клиента. Если вы находитесь в федеративный домен, можно перенаправленный tooyour локального сервера службы маркеров безопасности (STS) — например, Active Directory службы федерации (AD FS).
7. Если вы являетесь пользователем в домене, не относящихся к федерации, введите свои учетные данные непосредственно в Azure AD размещенной страницы приветствия. Если была настроена фирменная символика, вы также увидите логотип компании и сопроводительный текст.
8. Появится окно многофакторной проверки подлинности. Его настраивает ИТ-администратор.
9. Azure AD проверит, требуется ли регистрация пользователя или устройства в рамках политики управления мобильными устройствами.
10. Windows регистрирует hello устройства в каталоге организации hello в Azure AD и регистрирует в управление мобильными устройствами, если это необходимо.
11. Если управляемых пользователей Windows имеет desktop toohello hello автоматического входа в процессе.
12. Если федеративные пользователи направляются toohello входа в Windows экране tooenter учетные данные.

> [!NOTE]
> Присоединением к домену Windows Server Active Directory в локальной среде в hello Windows out-of-box experience не поддерживается. Таким образом, если планируется toojoin tooa домен компьютера, следует выбрать ссылку hello **настроить Windows с учетной записью** вместо него. Затем можно соединить hello домена из параметров hello на компьютере, как вы сделали перед.
> 
> 

## <a name="additional-information"></a>Дополнительная информация
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

