---
title: "возникает tooAzure aaaConnect устройств, присоединенных к домену AD для Windows 10 | Документы Microsoft"
description: "Объясняет, как администраторы могут настроить групповую политику tooenable устройств toobe домену toohello корпоративной сети."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Подключитесь к домену устройства tooAzure AD для Windows 10
Присоединение к домену — организаций hello традиционным способом подключения устройств для работы по hello последние 15 лет и многое другое. Включил toosign пользователей в tootheir устройств с помощью своей работы Windows Server Active Directory (Active Directory) или учебных учетных записей и разрешенных toofully ИТ управлять этими устройствами. Организациям обычно полагаются на toousers устройств tooprovision методы создания образа и обычно используют System Center Configuration Manager (SCCM) или групповой политики toomanage их.


Присоединение к домену, в Windows 10 предоставляет следующие преимущества, после подключения устройства tooAzure Active Directory (Azure AD) hello:

* Единого входа (SSO) tooAzure AD ресурсам из любого места
* Доступ к toohello корпоративного магазина Windows с помощью рабочих или школьные учетные записи (не требуется учетная запись Майкрософт)
* перенос пользовательских параметров между устройствами, которые используют рабочую учетную запись (с соблюдением корпоративных требований; не требуется учетная запись Майкрософт);
* строгая аутентификация и удобный вход с использованием рабочих или учебных учетных записей с помощью Windows Hello для бизнеса и Windows Hello;
* Возможность toorestrict доступ только toodevices, совместимых с параметрами групповой политики организации устройства

## <a name="prerequisites"></a>Предварительные требования
Присоединение к домену продолжается toobe полезно. Однако tooget hello Azure AD преимущества единого входа, перемещаемых параметров с работать или школьные учетные записи и получить доступ к хранилищу tooWindows с рабочие или школьные учетные записи, вы должны будете hello следующие:

* Подписка Azure AD
* Azure AD Connect tooextend hello локального каталога tooAzure AD
* Политики, которое задано tooAzure tooconnect устройств, присоединенных к домену AD
* сборка Windows 10 (сборка 10551 или более поздней версии) для устройств.

tooenable Windows Hello для бизнеса и Windows Hello, необходимо также hello следующее:

- **инфраструктура открытых ключей (PKI)** для выдачи сертификатов пользователей;

- **Текущей ветви System Center Configuration Manager** -требуется tooinstall версии 1606 или более поздней.  
Дополнительные сведения можно найти в разделе  
    - [Документация по System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Блог команды разработчиков Microsoft System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Параметры Windows Hello для бизнеса с помощью System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Как альтернативный toohello требование развертывания PKI, можно сделать hello следующее:

* Несколько контроллеров домена с доменными службами Active Directory Windows Server 2016.

tooenable условного доступа, можно создать параметры групповой политики, позволяющие доступа к устройствам, присоединенным toodomain с нет дополнительные развертывания. toomanage управление доступом на основе соответствия устройства hello, вам потребуется hello следующее:

* Текущая версия System Center Configuration Manager (1606 и выше) для сценариев Windows Hello для бизнеса.

## <a name="deployment-instructions"></a>Инструкции по развертыванию

toodeploy, повторите шаги hello, перечисленных в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Дальнейшие действия
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

