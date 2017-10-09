---
title: "Azure AD Connect: включение обратной записи устройств | Документация Майкрософт"
description: "Это содержатся подробные сведения, как tooenable обратной записи устройства с помощью Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: включение обратной записи устройств
> [!NOTE]
> Подписки tooAzure AD Premium является обязательным для обратной записи устройства.
> 
> 

Привет, следующая документация содержит сведения о как функция обратной записи устройства tooenable hello в Azure AD Connect. Следующие сценарии hello используются обратной записи устройства.

* Включить условный доступ на основании tooADFS устройства (2012 R2 или более поздней версии) защищенных приложений (доверия с проверяющей стороной).

Это обеспечивает дополнительную безопасность и гарантию того, что доступ к tooapplications предоставляется только tootrusted устройства. Дополнительные сведения о настройке условного доступа см. в статьях [Управление рисками с помощью условного доступа](../active-directory-conditional-access.md) и [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Устройства должен быть расположен в hello же лесе hello пользователей. Поскольку устройства необходимо записать tooa одного леса, этот компонент не поддерживает развертывание с несколькими лесами пользователя в настоящее время.</li>
> <li>Объект конфигурации регистрации только одно устройство можно добавить toohello локального леса Active Directory. Эта функция не совместим с топологией где hello в локальной Active Directory является каталогов синхронизированные toomultiple Azure AD.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Часть 1. Установка Azure AD Connect
1. Установите Azure AD Connect с использованием стандартных или пользовательских параметров. Корпорация Майкрософт рекомендует toostart со всех пользователей и групп, успешно синхронизирован перед включением обратной записи устройства.

## <a name="part-2-prepare-active-directory"></a>Часть 2. Подготовка Active Directory
Используйте следующие шаги tooprepare для обратной записи устройства с помощью hello.

1. С компьютера hello, где установлен Azure AD Connect запустите PowerShell с повышенными привилегиями.
2. Если модуль Active Directory PowerShell hello не установлен, установите его с помощью hello следующую команду:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Если установлен модуль Azure Active Directory PowerShell hello, затем загрузите и установите его из [Azure Active Directory модуля для Windows PowerShell (64-разрядная версия)](http://go.microsoft.com/fwlink/p/?linkid=236297). Этот компонент имеет зависимость от hello помощника по входу, которая устанавливается с Azure AD Connect.
4. Используя учетные данные администратора предприятия запустите следующие команды hello и выйдите из PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Учетные данные администратора предприятия необходимы, так как пространство имен конфигурации toohello изменения необходимы. Администратор домена не имеет достаточных разрешений.

![Powershell для включения обратной записи устройств](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Описание:

* Если они больше не существуют, функция создает и настраивает их в разделах CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].
* Если они больше не существуют, функция создает и настраивает их в разделе CN=RegisteredDevices,[domain-dn]. Объекты устройства будут созданы в этом контейнере.
* Задает необходимые разрешения учетной записи соединителя Azure AD, hello toomanage устройств в Active Directory.
* Достаточно toorun в одном лесу, даже если Azure AD Connect установлена в нескольких лесах.

Параметры

* DomainName: домен Active Directory, в котором будут созданы объекты устройства. Примечание: все устройства для отдельно взятого леса Active Directory будут созданы в одном домене.
* AdConnectorAccount: Учетная запись Active Directory, который будет использоваться с Azure AD Connect toomanage объектов в каталоге hello. Это hello учетной записи, используемой tooAD tooconnect синхронизации Azure AD Connect. Если вы установили, используя стандартные параметры, это учетная запись hello с MSOL_ префиксом.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Часть 3. Включение обратной записи устройств в Azure AD Connect
Используйте следующие процедуры tooenable обратной записи устройств в Azure AD Connect hello.

1. Снова запустите мастер установки hello. Выберите **настроить параметры синхронизации** из дополнительных задач hello и нажмите кнопку **Далее**.
   ![Выборочная установка: настройка параметров синхронизации](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. На странице приветствия дополнительных функций обратной записи устройства будет больше не выделен серым. Обратите внимание, что если hello Azure AD Connect подготовки не выполняются действия обратной записи устройства серым цветом помещает на странице дополнительных функций hello. Hello для обратной записи устройства, выберите **Далее**. Если флажок hello по-прежнему недоступен, см. раздел hello [устранении неполадок](#the-writeback-checkbox-is-still-disabled).
   ![Выборочная установка: дополнительные компоненты обратной записи устройства](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. На странице приветствия обратной записи вы увидите домена hello указано как леса обратной записи устройства по умолчанию hello.
   ![Выборочная установка: целевой лес обратной записи устройства](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Завершить установку hello приветствия мастера без изменения настроек. Используйте слишком[выборочной установки из Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Включение условного доступа
Подробные инструкции tooenable станут доступны в этом сценарии [Настройка регистрации устройств Azure Active Directory с помощью условного доступа локальной](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Убедитесь, что устройства, синхронизированные tooActive каталога
Функция обратной записи устройств должна теперь работать правильно. Имейте в виду, что может занять too3 часов для tooAD обратная запись toobe объектов устройств.  tooverify, что устройства синхронизированные надлежащим образом, hello, следующие после выполнения правила синхронизации hello:

1. Запустите центр администрирования Active Directory.
2. Разверните RegisteredDevices, в домен, который входит в федерацию hello.
   ![Центр администрирования Active Directory: зарегистрированные устройства](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Там будут перечислены зарегистрированные в настоящий момент устройства.
   ![Центр администрирования Active Directory: список зарегистрированных устройств](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="hello-writeback-checkbox-is-still-disabled"></a>флажок Hello обратной записи по-прежнему недоступен
Если флажок hello для обратной записи устройства не включена, несмотря на то, что выполнены действия hello выше hello следующие шаги помогут вам через какие hello установки мастер проверяет прежде, чем доступно поле hello.

Начнем сначала:

* Убедитесь, что по крайней мере в одном лесу есть 2012R2 Windows Server. Тип объекта устройства Hello должен присутствовать.
* Если мастер установки hello уже выполняется, любые изменения не будут обнаружены. В этом случае завершения приветствия мастера установки и запустите его еще раз.
* Убедитесь, что hello, указываемых в сценарий инициализации hello пользователем является учетная запись фактически hello правильный используемые hello Соединитель Active Directory. tooverify это, выполните следующие действия:
  * Из меню "Пуск" Привет открыть **служба синхронизации**.
  * Откройте hello **соединители** вкладки.
  * Найти hello соединитель с типом доменных служб Active Directory и выберите его.
  * В разделе **Действия** выберите **Свойства**.
  * Go слишком**подключения леса tooActive**. Убедитесь, что hello домен и имя пользователя указано для выполнения сценария toohello соответствия hello экрана указанная учетная запись.
    ![Учетная запись соединителя в диспетчере службы синхронизации](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Проверьте конфигурацию Active Directory.

* Убедитесь, что hello службы регистрации устройств находится в расположение hello (CN DeviceRegistrationService, CN = службы регистрации устройств, CN = = Device Registration Configuration, CN = Services, CN = Configuration) в контексте именования конфигурации.

![Устранение неполадок, служба регистрации устройств в пространстве имен конфигурации](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Убедитесь, что имеется только один объект конфигурации, выполняя поиск пространство имен конфигурации hello. Если имеется более одного, удалите дубликат hello.

![Устранение неполадок, поиск дубликатов объектов hello](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Hello объекта службы регистрации устройств убедитесь, что hello атрибут msDS-DeviceLocation присутствует и имеет значение. Уточняющий запрос это расположение и убедитесь, что он присутствует с hello objectType msDS-DeviceContainer.

![Устранение неполадок, расположение устройств msDS](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Устранение неполадок, класс объекта зарегистрированных устройств](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Проверьте hello учетной записи, используемой hello Соединитель Active Directory имеет необходимые разрешения для контейнера hello зарегистрированные устройства, обнаруженные hello предыдущего шага. Это ожидалось hello разрешения для данного контейнера:

![Устранение неполадок, проверка разрешений в контейнере](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Проверьте hello учетной записи Active Directory имеет разрешения на hello CN = Device Registration Configuration, CN = Services, CN = объект конфигурации.

![Устранение неполадок, проверка разрешений в конфигурации регистрации устройства](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Дополнительная информация
* [Управление рисками с помощью условного доступа](../active-directory-conditional-access.md)
* [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

