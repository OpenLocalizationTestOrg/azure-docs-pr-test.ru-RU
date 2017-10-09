---
title: "Повторным запуском мастера установки hello Azure AD Connect | Документы Microsoft"
description: "Объясняет, как мастер установки hello работает hello во второй раз при запуске."
keywords: "Мастер установки Hello Azure AD Connect позволяет настраивать параметры hello обслуживания второй раз при запуске"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Синхронизация Azure AD Connect: запуск мастера установки hello еще раз
Hello первом запуске мастера установки hello Azure AD Connect, оно описано, как tooconfigure установки. При запуске мастера установки hello, он предлагает варианты для обслуживания.

Приветствия мастера установки можно найти в меню "Пуск" hello с именем **Azure AD Connect**.

![Меню "Пуск"](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

При запуске мастера установки hello, отображается страница с этими параметрами.

![Страница со списком дополнительных задач](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Если вы установили службы AD FS с Azure AD Connect, вам будет доступно еще больше возможностей. Здравствуйте, дополнительные параметры, у вас есть по ADFS описаны в [управления ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Выберите одну из задач hello и нажмите кнопку **Далее** toocontinue.

> [!IMPORTANT]
> При наличии откройте мастер установки hello приостанавливаются все операции в модуль синхронизации hello. Убедитесь, что сразу после завершения изменения конфигурации, закройте мастер установки hello.
>
>

## <a name="view-current-configuration"></a>Просмотр текущей конфигурации
Этот параметр позволяет быстро просмотреть текущие настройки параметров.

![Страница со списком всех параметров и их состоянием](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Нажмите кнопку **Назад** toogo назад. При выборе **выхода**, закройте мастер установки hello.

## <a name="customize-synchronization-options"></a>Настройка параметров синхронизации
Этот параметр является toohello синхронизации используется toomake изменения конфигурации. Вы увидите подмножество параметров hello пути установки пользовательской конфигурации. Они отобразятся, даже если изначально использовались параметры экспресс-установки.

* [Добавить дополнительные каталоги](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Сведения об удалении каталога см. [здесь](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Изменить фильтрацию доменов и подразделений](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Удалить групповую фильтрацию.
* [Изменить дополнительные возможности](active-directory-aadconnect-get-started-custom.md#optional-features).

Hello другие параметры из первоначальной установки hello не может быть изменено и не доступны. Доступны следующие параметры:

* Изменить toouse hello атрибут userPrincipalName и sourceAnchor.
* Изменить hello присоединение метод для объектов из другого леса.
* Включить фильтрацию на основе группы.

## <a name="refresh-directory-schema"></a>Обновление схемы каталога
Этот параметр используется при изменении схемы hello в одном из локальных лесов AD DS. Например мог установить Exchange или обновления схемы tooa Windows Server 2012 с объектами устройства. В этом случае требуется tooinstruct Azure AD Connect tooread hello схемы из AD DS и обновляет свой кэш. Это действие также выполняется повторное создание правила синхронизации hello. При добавлении схемы Exchange hello, например hello правила синхронизации для Exchange добавляются toohello конфигурации.

При выборе этого параметра отображаются все каталоги hello в конфигурации. Можно сохранить значение по умолчанию hello и обновление всех лесах или отменить выбор некоторых из них.

![Страница со списком всех каталогов в среде hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Настройка промежуточного режима
Этот параметр позволяет вам tooenable и отключить промежуточный режим на сервере hello. Дополнительные сведения о промежуточном режиме и его использовании см. [здесь](active-directory-aadconnectsync-operations.md#staging-mode).

При выборе параметра Hello отображаются, если промежуточной включено или отключено:  
![Параметр, который отображается текущее состояние промежуточного режима hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Здравствуйте состояния, выберите этот параметр и выберите или отмените выбор hello флажок.  
![Параметр, который отображается текущее состояние промежуточного режима hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Изменение параметров входа пользователя
Этот параметр позволяет toochange из toofederation синхронизации пароля или наоборот hello. Невозможно изменить слишком**не задан**.

Дополнительные сведения о входе пользователя см. [здесь](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о модели конфигурации hello, используемой службой Azure AD Connect sync в [декларативной подготовки основные сведения о](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
