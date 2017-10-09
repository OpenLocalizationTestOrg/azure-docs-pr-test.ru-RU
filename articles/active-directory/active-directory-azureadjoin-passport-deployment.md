---
title: "aaaEnable Microsoft Windows Hello для бизнеса в вашей организации | Документы Microsoft"
description: "Развертывание инструкции tooenable Microsoft Passport в вашей организации."
services: active-directory
documentationcenter: 
keywords: "настройка Microsoft Passport, развертывание Microsoft Windows Hello для бизнеса"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Включение Microsoft Windows Hello для бизнеса в организации
После [подключение устройств, присоединенных к домену Windows 10 с Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), hello следующие tooenable Microsoft Windows Hello для бизнеса в вашей организации:

1. Развертывание System Center Configuration Manager  
2. Настройка параметров политики
3. Настройка профиля сертификата hello  

## <a name="deploy-system-center-configuration-manager"></a>Развертывание System Center Configuration Manager
toodeploy пользователя сертификаты на основе Windows Hello для бизнес-ключи, необходимы следующие hello.

* **Текущей ветви System Center Configuration Manager** -требуется tooinstall версии 1606 или более поздней. Дополнительные сведения см. в разделе hello [документации для System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) и [блог группы System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Инфраструктуры открытых ключей (PKI)** -tooenable Microsoft Windows Hello для бизнеса с помощью пользовательских сертификатов, необходимо иметь PKI на месте. Если у вас его нет, или вы не хотите toouse его для сертификатов пользователей, можно развернуть новый контроллер домена с Windows Server 2016 построения 10551 (или выше) установлен. Выполните действия hello слишком[Установка реплики контроллера домена в существующем домене](https://technet.microsoft.com/library/jj574134.aspx) или слишком[Установка нового леса Active Directory, если вы создаете новую среду](https://technet.microsoft.com/library/jj574166). (hello образы ISO доступны для загрузки на [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Настройка параметров политики
hello tooconfigure Microsoft Windows Hello для бизнеса параметров политики можно использовать два варианта:

* групповая политика в Active Directory; 
* Hello System Center Configuration Manager 

Благодаря использованию групповой политики в Active Directory — hello, рекомендуется использовать метод tooconfigure Microsoft Windows Hello для бизнеса параметров политики. 

С помощью System Center Configuration Manager — hello предпочтительный метод, можно также использовать сертификаты toodeploy. Данный сценарий:

* Обеспечивает совместимость с более новые сценарии развертывания hello
* Требуется на стороне клиента hello Windows 10 версии 1607 или выше.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Настройка Microsoft Windows Hello для бизнеса с помощью групповой политики в Active Directory
**Шаги**:

1. Откройте диспетчер сервера и перейдите слишком**средства** > **Управление групповой политикой**.
2. Управление групповой политикой перейдите toohello узел домена, соответствующий toohello домен, в котором нужно tooenable присоединения Azure AD.
3. Щелкните правой кнопкой мыши **Объекты групповой политики** и выберите **Создать**. Укажите имя объекта групповой политики, например "Включение Windows Hello для бизнеса". Нажмите кнопку **ОК**.
4. Щелкните правой кнопкой мыши новый объект групповой политики и выберите пункт **Изменить**.
5. Перейдите в слишком**Конфигурация компьютера** > **политики** > **административные шаблоны** > **Windows Компоненты** > **Windows Hello для бизнеса**.
6. Щелкните правой кнопкой мыши **Enable Windows Hello for Business** (Включить Windows Hello для бизнеса), а затем выберите пункт **Изменить**.
7. Выберите hello **включено** переключатель, а затем нажмите кнопку **применить**. Нажмите кнопку **ОК**.
8. Теперь можно связать hello объекта групповой политики tooa местом по своему усмотрению. tooenable эту политику для всех hello присоединенных к домену устройств Windows 10 в вашей организации toohello групповой политики домена для связи hello. Например:
   * с определенным подразделением в Active Directory, в котором будут размещаться компьютеры Windows 10, присоединенные к домену;
   * с определенной группой безопасности, содержащей присоединенные к домену компьютеры Windows 10, для которых будет выполняться автоматическая регистрация в Azure AD.

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Настройка Windows Hello для бизнеса с помощью System Center Configuration Manager
**Шаги**:

1. Откройте hello **System Center Configuration Manager**и перейдите слишком**активы и соответствие нормативным требованиям > Параметры соответствия > доступ к ресурсам компании > Windows Hello для бизнес-профили**.
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Щелкните hello панели инструментов в верхней части hello **создать Windows Hello для бизнеса профиль**.
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. На hello **Общие** диалоговое окно, выполните следующие шаги hello:
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    а. В hello **имя** текстовом поле введите имя для своего профиля, например, **Мой профиль WHfB**.
   
    b. Щелкните **Далее**.
4. На hello **поддерживаемые платформы** диалоговое окно, выберите hello платформы, будет использован этот Windows Hello для бизнес-профиль и нажмите кнопку **Далее**.
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. На hello **параметры** диалоговое окно, выполните следующие шаги hello:
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    а. Для параметра **Настройка Windows Hello для бизнеса** выберите значение **Включено**.
   
    b. Для параметра **Использовать доверенный платформенный модуль (TPM)** выберите **Требуется**. 
   
    c. Для параметра **Способ проверки подлинности** выберите значение **На основе сертификата**.
   
    d. Щелкните **Далее**.
6. На hello **Сводка** диалоговое окно, нажмите кнопку **Далее**.
7. На hello **завершения** диалоговое окно, нажмите кнопку **закрыть**.
8. Щелкните hello панели инструментов в верхней части hello **развернуть**.
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Настройка профиля сертификата hello
При использовании проверки подлинности на основе сертификатов для проверки подлинности в локальной среде требуется tooconfigure и развертывание профиля сертификата. Эта задача требует tooset NDES-сервер, и роли сайта точки регистрации сертификатов в System Center Configuration Manager hello. Дополнительные сведения см. в разделе hello [необходимые условия для профилей сертификатов в Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Привет открыть **System Center Configuration Manager**, а затем переходить слишком**активы и соответствие нормативным требованиям > параметров соответствия требованиям > доступ к ресурсам компании > профилей сертификатов**.
2. Выберите шаблон с EKU входа со смарт-картой.

На hello **регистрация SCEP** страницы приветствия профиль сертификата, вы должны toochoose **tooPassport для работы в противном случае сбой установки** как hello **поставщик хранилища ключей**.

## <a name="next-steps"></a>Дальнейшие действия
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

