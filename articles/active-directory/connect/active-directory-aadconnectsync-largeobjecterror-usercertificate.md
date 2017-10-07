---
title: "Синхронизация Azure AD Connect: обработка ошибок LargeObject, вызванных атрибутом userCertificate | Документация Майкрософт"
description: "В этом разделе шаги hello исправления для LargeObject ошибки, вызванные userCertificate атрибута."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Синхронизация Azure AD Connect: обработка ошибок LargeObject, вызванных атрибутом userCertificate

Azure AD обеспечивает максимальное количество **15** сертификатов значения на hello **userCertificate** атрибута. Если Azure AD Connect экспортирует объект с более чем на 15 tooAzure значения AD, Azure AD возвращает **LargeObject** ошибка с сообщением:

>*«hello подготовленный объект слишком велик. Trim hello число значений атрибутов для этого объекта. Hello операция будет повторена в hello следующего цикла синхронизации...»*

Hello LargeObject ошибки может быть вызвано другими атрибутами AD. на самом деле она вызвана hello userCertificate атрибут tooconfirm, необходимо tooverify для hello объекта в локальном AD или в hello [поиска метавселенной диспетчера службы синхронизации](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

tooobtain hello список объектов в клиенте с ошибками LargeObject, используйте один из следующих методов hello:

 * Если включена вашего клиента Azure AD Connect Health для синхронизации, можно обратиться toohello [отчет об ошибках синхронизации](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) предоставлен.
 
 * Hello уведомление по электронной почте для ошибок синхронизации каталогов, отправляемый в конце каждого цикла синхронизации в hello имеет hello список объектов с ошибками LargeObject. 
 * Hello [вкладку Диспетчер службы синхронизации операции](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) отображает hello список объектов с ошибками LargeObject, если щелкнуть hello последней операции экспорта tooAzure AD.
 
## <a name="mitigation-options"></a>Варианты устранения ошибок
Пока не будет устранена ошибка LargeObject hello, другие toohello изменения атрибутов одного объекта не может быть экспортирован tooAzure AD. Ошибка tooresolve hello, рассмотрим hello следующие параметры:

 * Обновление Azure AD Connect toobuild 1.1.524.0 или после. В Azure AD Connect сборки 1.1.524.0, правила синхронизации out-of-box hello были userCertificate атрибуты экспорта обновленные toonot и userSMIMECertificate у более чем на 15 значения атрибутов hello. Дополнительные сведения о том, как tooupgrade Azure AD Connect см. tooarticle [Azure AD Connect: обновление с предыдущей версии toohello последней](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Реализуйте **правило исходящей синхронизации** в Azure AD Connect, которая экспортирует **значение вместо фактических значений для объектов с более чем на 15 значения сертификата hello null**. Этот параметр подходит, если любой из hello сертификата значения toobe экспортировать tooAzure AD не требуется для объектов с более чем на 15 значения. Дополнительные сведения о том, как правило этой синхронизации, см. раздел toonext tooimplement [реализация экспорта toolimit правила синхронизации userCertificate атрибута](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Сократите число hello значений сертификат на hello локального объекта AD (15 или меньше), удаляя значения, которые больше не используются в организации. Это подходит, если атрибут Раздувание hello вызвана сертификаты с истекшим сроком действия или не используется. Можно использовать hello [доступные здесь сценарий PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) найти toohelp резервной копии, а также удалять просроченные сертификаты в локальном AD. Прежде чем удалять сертификаты hello, рекомендуется проверить с открытым ключом инфраструктурных администраторами hello в вашей организации.

 * Настройка Azure AD Connect tooexclude hello userCertificate атрибута не экспортированы tooAzure AD. В общем случае не рекомендуется этот параметр, так как атрибут hello может использоваться Microsoft Online Services tooenable конкретных сценариев. например:
    * атрибут userCertificate Hello hello объекта пользователя используется с Exchange Online и клиенты Outlook для подписывания и шифрования сообщений. toolearn больше об этой функции см. tooarticle [S/MIME для подписывания и шифрования сообщений](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * атрибут userCertificate Hello hello объекта-компьютера используется tooconnect устройств, присоединенных к домену tooAzure AD Azure AD tooallow Windows 10 в локальной среде. toolearn больше об этой функции см. tooarticle [подключения tooAzure устройств, присоединенных к домену AD, для Windows 10 возникает](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Реализация экспорта toolimit правила синхронизации userCertificate атрибута
LargeObject hello tooresolve ошибка вызвана hello userCertificate атрибута, можно реализовать правило исходящей синхронизации в Azure AD Connect, которая экспортирует **значение вместо фактических значений для объектов с более чем на 15 значения сертификатаhellonull**. В этом разделе описываются правила hello действия требуется tooimplement hello синхронизации для **пользователя** объектов. Hello действия может быть адаптирован для **контакт** и **компьютера** объектов.

> [!IMPORTANT]
> Экспорт значение null Удаляет сертификат, что значения ранее успешно экспортирован tooAzure AD.

Hello действия можно вкратце описать следующим образом:

1. Отключите планировщик синхронизации и убедитесь, что синхронизация не выполняется.
3. Найти существующее правило исходящей синхронизации hello userCertificate атрибута.
4. Создание правила исходящей синхронизации hello требуется.
5. Проверьте hello новое правило синхронизации на основе существующего объекта с ошибкой LargeObject.
6. Примените hello новый синхронизации правило tooremaining объекты с ошибкой LargeObject.
7. Проверьте, нет ли Непредвиденная изменений, требующих tooAzure toobe экспортировать AD.
8. Экспорт tooAzure изменения hello AD.
9. Повторно включите планировщик синхронизации.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Шаг 1. Отключите планировщик синхронизации и убедитесь, что синхронизация не выполняется
Убедитесь, синхронизация не выполняется, пока вы находитесь в середине hello реализации синхронизацию правило tooavoid непреднамеренного изменения срока экспортировать tooAzure AD. Планировщик синхронизации встроенных hello toodisable:
1. Запустите сеанс PowerShell на сервере hello Azure AD Connect.

2. Отключите плановую синхронизацию, выполнив командлет: `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hello описанные выше шаги являются только применимые toonewer версии (1.1.xxx.x) Azure AD Connect с помощью встроенного планировщика hello. Если вы используете более старых версий Azure AD Connect, который использует планировщик заданий Windows (1.0.xxx.x) или вы используете собственный пользовательский планировщик (как правило, не) tootrigger периодической синхронизации, необходимо toodisable их соответствующим образом.

3. Запуск hello **диспетчер службы синхронизации** с переходом → tooSTART службы синхронизации.

4. Go toohello **операции** вкладку и подтвердите нет операции с состоянием *в состоянии «выполняется».*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Шаг 2. Поиск атрибута userCertificate hello существующее правило исходящей синхронизации
Должно быть существующее правило синхронизации, включения и настройки атрибутов userCertificate tooexport для tooAzure объектов пользователя AD. Найдите это toofind правило синхронизации out его **приоритет** и **фильтр области** конфигурации:

1. Запуск hello **редактор правил синхронизации** с переходом → tooSTART синхронизации правила редактора.

2. Настройте фильтры поиска hello hello следующие значения:

    | Атрибут | Значение |
    | --- | --- |
    | Направление |**Outbound** |
    | Тип объекта метавселенной |**Person** |
    | Соединитель |*Имя вашего клиента Azure AD* |
    | Тип объекта соединителя |**user** |
    | Атрибуты метавселенной |**userCertificate** |

3. Если вы используете OOB (out-of-box) tooAzure AD правила синхронизации соединителя атрибут userCertficiate tooexport для пользовательских объектов, вы должны получить обратно hello *«ожидания tooAAD — ExchangeOnline пользователя»* правило.
4. Запишите hello **приоритет** значение данного правила синхронизации.
5. Выберите правило синхронизации hello и нажмите кнопку **изменить**.
6. В hello *«Изменить зарезервированный правило подтверждения»* всплывающем диалоговом окне щелкните **нет**. (Не беспокойтесь, мы не будем toomake любое правило синхронизации toothis изменений).
7. На экране приветствия редактирования выберите hello **фильтр области** вкладки.
8. Запишите hello области конфигурации фильтра. При использовании правил синхронизации OOB hello точно следует **одной области фильтра группа, содержащая два предложения**, в том числе:

    | Атрибут | Оператор | Значение |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Пользователь |
    | cloudMastered | NOTEQUAL | Да |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Шаг 3. Создание правила исходящей синхронизации hello требуется
Hello новое правило синхронизации должна иметь hello же **фильтр области** и **более высокий приоритет** чем hello существующее правило синхронизации. Это гарантирует, что новое правило синхронизации hello относятся toohello же набор объектов как hello существующее правило синхронизации и переопределений hello существующего синхронизации правила для атрибута userCertificate hello. правило синхронизации hello toocreate:
1. В hello редактор правил синхронизации, щелкните hello **добавить новое правило** кнопки.
2. В разделе hello **вкладка "Описание"**, предоставляют hello следующая конфигурация:

    | Атрибут | Значение | Сведения |
    | --- | --- | --- |
    | Имя | *Укажите имя* | Например *«Out tooAAD — настраиваемый переопределение для userCertificate»* |
    | Описание | *Укажите описание* | Например, *если атрибут userCertificate содержит более 15 значений, экспортировать NULL.* |
    | Подключенная система | *Выберите hello соединителя Azure AD* |
    | Тип объекта подключенной системы | **user** | |
    | Тип объекта метавселенной | **person** | |
    | Тип связи | **Join** | |
    | Приоритет | *Выберите число от 1 до 99* | Hello число_выбранных не должны использоваться любое существующее правило синхронизации и имеет меньшее значение (и, следовательно, более высокий приоритет), чем hello существующее правило синхронизации. |

3. Go toohello **фильтр области** вкладку и реализовать hello, используя же области фильтра hello существующих правило синхронизации.
4. Пропустить hello **правила присоединения** вкладки.
5. Go toohello **преобразования** вкладке tooadd новую преобразование, используя следующие конфигурации:

    | Атрибут | Значение |
    | --- | --- |
    | Тип потока |**Expression** |
    | Целевой атрибут |**userCertificate** |
    | Исходный атрибут |*Следующее выражение hello используйте*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Нажмите кнопку hello **добавить** правило синхронизации hello toocreate кнопки.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Шаг 4. Проверьте hello новое правило синхронизации на основе существующего объекта с ошибкой LargeObject
Это tooverify, hello синхронизации правило создано работает правильно на основе существующего объекта AD с ошибкой LargeObject применить tooother объектов:
1. Go toohello **операции** hello Synchronization Service Manager на вкладке.
2. Hello последней операции экспорта tooAzure AD и щелкните один из объектов hello LargeObject ошибок.
3.  В новое окно hello свойства объекта пространства соединителя, щелкните hello **предварительного просмотра** кнопки.
4. В новое окно предварительного просмотра hello, выберите **полная синхронизация** и нажмите кнопку **зафиксировать Preview**.
5. Закройте окно Предварительный просмотр экран приветствия и свойства объекта пространства соединителя экран приветствия.
6. Go toohello **соединители** hello Synchronization Service Manager на вкладке.
7. Щелкните правой кнопкой мыши на hello **Azure AD** соединитель и выберите **запуска...**
8. Во всплывающем запуска соединителя hello, выберите **Экспорт** шаг и щелкните **ОК**.
9. Дождитесь toocomplete tooAzure AD экспорта и убедиться, что ошибка не дополнительные LargeObject на данном объекте.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Шаг 5. Применить hello новых синхронизации правило tooremaining объектов с ошибкой LargeObject
После добавления правила синхронизации hello требуется toorun шага полную синхронизацию в hello соединителя AD:
1. Go toohello **соединители** hello Synchronization Service Manager на вкладке.
2. Щелкните правой кнопкой мыши на hello **AD** соединитель и выберите **запуска...**
3. Во всплывающем запуска соединителя hello, выберите **полная синхронизация** шаг и щелкните **ОК**.
4. Дождитесь toocomplete шаг hello полную синхронизацию.
5. Повторите hello выше шаги для hello оставшийся соединители AD, если у вас есть несколько соединителей AD. Как правило, для нескольких локальных каталогов требуется несколько соединителей.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Шаг 6. Проверьте, нет Непредвиденная изменений, требующих tooAzure toobe экспортировать AD
1. Go toohello **соединители** hello Synchronization Service Manager на вкладке.
2. Щелкните правой кнопкой мыши на hello **Azure AD** соединитель и выберите **поиска пространства соединителя**.
3. Во всплывающем hello поиска пространства соединителя:
    1. Настройка области слишком**ожидающие экспорта**.
    2. Установите все 3 флажка, в том числе **Добавить**, **Изменить** и **Удалить**.
    3. Нажмите кнопку **поиска** кнопку tooreturn все объекты с изменений, требующих tooAzure toobe экспортировать AD.
    4. Убедитесь, что непредвиденные изменения отсутствуют. Дважды щелкните hello объекта tooexamine hello изменения для данного объекта.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Шаг 7. Экспорт tooAzure изменения hello AD
изменения tooAzure hello tooexport AD:
1. Go toohello **соединители** hello Synchronization Service Manager на вкладке.
2. Щелкните правой кнопкой мыши на hello **Azure AD** соединитель и выберите **запуска...**
4. Во всплывающем запуска соединителя hello, выберите **Экспорт** шаг и щелкните **ОК**.
5. Дождитесь toocomplete tooAzure AD экспорта и убедиться, что отсутствуют дополнительные ошибки LargeObject.

### <a name="step-8-re-enable-sync-scheduler"></a>Шаг 8. Повторно включите планировщик синхронизации
Теперь, когда hello проблема будет устранена, повторно включите планировщика hello встроенных синхронизации:
1. Запустите сеанс PowerShell.
2. Повторно включите плановую синхронизацию, выполнив командлет: `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hello описанные выше шаги являются только применимые toonewer версии (1.1.xxx.x) Azure AD Connect с помощью встроенного планировщика hello. Если вы используете более старых версий Azure AD Connect, который использует планировщик заданий Windows (1.0.xxx.x) или вы используете собственный пользовательский планировщик (как правило, не) tootrigger периодической синхронизации, необходимо toodisable их соответствующим образом.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

