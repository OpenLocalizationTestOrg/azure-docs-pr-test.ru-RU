---
title: "Azure AD Connect: обновление до последней версии | Документация Майкрософт"
description: "Описание hello различные методы tooupgrade toohello последний выпуск Azure Active Directory Connect, включая обновление на месте и ходу миграции."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: Обновление с предыдущей версии toohello последняя версия
В этом разделе описываются hello различные методы, которые можно использовать tooupgrade вашей установки подключение Azure Active Directory (Azure AD) toohello последний выпуск. Мы рекомендуем оставить самостоятельно текущего с выпусками hello Azure AD Connect. Вы также использовать действия hello hello [Вращающаяся миграции](#swing-migration) статьи при внесении значительное изменение конфигурации.

Tooupgrade от DirSync см [обновить средство синхронизации Azure AD (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) вместо него.

Существует несколько различных стратегий, которые можно использовать tooupgrade Azure AD Connect.

| Метод | Описание |
| --- | --- |
| [Автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) |Это самый простой метод hello для клиентов с экспресс-установки. |
| [Обновление «на месте»](#in-place-upgrade) |При наличии одного сервера, вы можете обновить hello установки на месте на сервере hello. |
| [Обновление со сменой сервера](#swing-migration) |С двумя серверами можно подготовить один из серверов hello с новым выпуском hello или конфигурации и изменить hello активного сервера, когда вы будете готовы. |

Разрешения подробнее hello [разрешения, необходимые для обновления](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> После включения ваш новый Azure AD Connect server toostart синхронизации изменений tooAzure AD, вы должны не откат toousing DirSync или Azure AD Sync. Понижении от клиентов toolegacy Azure AD Connect, включая DirSync и Azure AD Sync не поддерживается и может привести tooissues, такие как потеря данных в Azure AD.

## <a name="in-place-upgrade"></a>Обновление «на месте»
Обновление на месте подходит для обновления Azure AD Sync или Azure AD Connect. Оно не подходит для перехода с DirSync или для решения на основе Forefront Identity Manager (FIM) и соединителя Azure AD.

Мы советуем использовать этот вариант, если у вас есть один сервер и меньше 100 000 объектов. Если имеются изменения правила синхронизации out-of-box toohello, полный импорт и полную синхронизацию возникать после обновления hello. Этот метод гарантирует, что новая конфигурация этого hello — примененных tooall существующие объекты в системе hello. Этот запуск может занять несколько часов в зависимости от числа объектов, которые находятся в области действия подсистемы синхронизации hello в hello. Планировщик синхронизации обычный дельта Hello (который по умолчанию выполняет синхронизацию каждые 30 минут) приостанавливается, но по-прежнему синхронизации паролей. Может выполнить обновление на месте hello выходные дни. Если отсутствуют изменения настройки out-of-box toohello с выпуском hello новый Azure AD Connect, затем обычный дельта импорта или синхронизации запускает вместо.  
![Обновление «на месте»](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Если вы внесли изменения toohello синхронизации out-of-box правила, затем такие правила установлены обратно toohello конфигурация по умолчанию при обновлении. toomake поддерживает конфигурацию между обновления, убедитесь в том, внести изменения, как они описаны в [советы и рекомендации по изменению конфигурации по умолчанию hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Во время обновления на месте, возможно, представленные изменения, которые требуют определенных синхронизации действий (в том числе шаге полный импорт и полную синхронизацию) toobe выполняется после завершения обновления. toodefer такие операции ссылаться toosection [как toodefer полная синхронизация после обновления](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Обновление со сменой сервера
При наличии комплексного развертывания или нескольких объектов, бывает нецелесообразным toodo обновление на месте в действующей системе hello. У некоторых клиентов процесс может занять несколько дней, в течение которых никакие изменения синхронизироваться не будут. Этот метод также можно использовать при планировании конфигурации tooyour toomake существенные изменения, которые будут tootry их ожидания перед их работе отправить toohello облака.

Привет, рекомендуется использовать метод для этих сценариев — toouse миграции ходу. Вам потребуется по крайней мере два сервера — активный и промежуточный. Hello активного сервера (показана с сплошными синими линиями в hello следующий рисунок) отвечает за hello активной рабочей нагрузки. Hello тестового сервера (показана с пунктирных линий фиолетовый) подготовлен с новым выпуском hello или конфигурации. После завершения подготовки к использованию он становится активным сервером. Hello предыдущей active сервер, который теперь имеет старую версию hello или установленную конфигурацию, внесенные в промежуточном сервере hello и обновляется.

два сервера Hello можно использовать разные версии. Например hello активного сервера планирования toodecommission можно использовать Azure AD Sync, и hello новый промежуточный сервер можно использовать Azure AD Connect. При использовании toodevelop миграции ходу новой конфигурации, его toohave смысл hello такие же версии на hello двух серверов.  
![Промежуточный сервер.](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Некоторые пользователи предпочитают toohave трех или четырех серверов для данного сценария. При обновлении hello тестового сервера, у вас нет резервной копии сервера для [аварийного восстановления](active-directory-aadconnectsync-operations.md#disaster-recovery). С тремя или четырьмя серверами можно подготовить одного набора серверов основной или резервной hello новой версии, который гарантирует, что всегда промежуточного сервера, готовы tootake через.

Эти действия могут быть использованы toomove из Azure AD Sync или решение с FIM + соединитель Azure AD. Эти шаги не работают для DirSync, но hello же ходу метод миграции (также называемые параллельного развертывания) с шагами по DirSync в [обновления Azure Active Directory sync (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Использовать tooupgrade ходу миграции
1. При использовании Azure AD Connect на серверах и сделать план tooonly изменения конфигурации, убедитесь, что активного сервера и промежуточного серверов заданы оба с помощью одной версии "hello". Это позволяет упростить различия toocompare позже. При обновлении Azure AD Sync эти серверы имеют разные версии. При обновлении с более старой версии Azure AD Connect, это рекомендуется toostart с hello двух серверов, с помощью одной версии "hello", но это не обязательно.
2. Если вы внесли пользовательской конфигурации и промежуточном сервере нет, выполните действия hello под [перемещение пользовательской конфигурации с тестового сервера toohello активного сервера hello](#move-custom-configuration-from-active-to-staging-server).
3. При обновлении от более раннего выпуска Azure AD Connect, обновите hello промежуточного сервера toohello последнюю версию. При перемещении из Azure AD Sync установите Azure AD Connect на промежуточном сервере.
4. Разрешить hello синхронизации engine работают полный импорт и полную синхронизацию на промежуточном сервере.
5. Проверить новую конфигурацию, hello не вызваны любые непредвиденные изменения с помощью hello шаги в разделе «Проверить» в [hello Проверьте конфигурацию сервера](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Если что-то не как ожидаемый, верно, запустите hello импорта и синхронизации и убедитесь hello данных пока выглядит неплохо, выполнив указанные ниже действия hello.
6. Переключение hello промежуточного сервера toobe hello активного сервера. Это последний шаг hello «Коммутатора active server» в [hello Проверьте конфигурацию сервера](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. При обновлении Azure AD Connect, обновите сервер hello, теперь в промежуточного режима toohello последний выпуск. Выполните шаги таким же как и прежде tooget hello данных и обновления конфигурации hello. При обновлении Azure AD Sync на этом этапе можно отключить и списать старый сервер.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Переместить пользовательской конфигурации с промежуточного сервера hello активного сервера toohello
При внесении сервер active toohello изменения конфигурации необходимо toomake убедитесь, что, hello же изменения, примененные toohello тестового сервера. переместить toohelp с этим, можно использовать hello [Архивариус конфигурации Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

Можно перемещать пользовательские синхронизации hello правил, что вы создали с помощью PowerShell. Необходимо применить другие изменения hello так же, как систем, и вам не удается выполнить миграцию hello изменения. Hello [Архивариус конфигурации](https://github.com/Microsoft/AADConnectConfigDocumenter) может помочь сравнение hello двух систем toomake убедиться, что они совпадают. также может помочь Hello средство автоматизации hello шаги, представленные в этом разделе.

Требуются следующие hello tooconfigure вещей hello таким же образом на обоих серверах:

* Подключение toohello того же леса
* Фильтрацию доменов и подразделений.
* Здравствуйте, же дополнительных компонентов, таких как синхронизация паролей и обратная запись паролей

**Перемещение пользовательских правил синхронизации**  
toomove пользовательские правила синхронизации, hello следующие:

1. Откройте **редактор правил синхронизации** на активном сервере.
2. Выберите пользовательское правило. Щелкните **Экспорт**. Откроется окно Блокнота. Сохранение hello временного файла с расширением PS1. он станет скриптом PowerShell. Скопируйте файл hello PS1 toohello с тестового сервера.  
   ![Экспорт правил синхронизации](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hello GUID соединителя отличается на промежуточном сервере hello и необходимо изменить его. Запуск tooget hello GUID, **редактор правил синхронизации**, выберите одно из правил out-of-box hello, представляют Привет же соединение системы, а затем нажмите кнопку **Экспорт**. Замените hello GUID из тестового сервера hello hello GUID в PS1-файл.
4. В командной строке PowerShell запустите файл hello PS1. При этом создается правило синхронизации hello на промежуточном сервере hello.
5. Повторите эти действия для всех пользовательских правил.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Как toodefer полная синхронизация после обновления
Во время обновления на месте, возможно, вносимые, требующих синхронизации определенных действий (в том числе шаге полный импорт и полную синхронизацию) toobe выполнена. Например, изменения схемы соединителя требуют **полный импорт** шаг и out-of-box изменения правила синхронизации требуют **полная синхронизация** шаг toobe выполнена на затронутых соединители. Во время обновления Azure AD Connect определяет действия синхронизации, которые необходимо выполнить, и записывает их в виде *переопределений*. В следующий цикл синхронизации hello Планировщик синхронизации hello собирают эти переопределения и выполняет их. После успешного выполнения переопределения оно удаляется.

Могут возникнуть ситуации, где требуется поместить tootake эти переопределения сразу же после обновления. Например имеется множество Синхронизируемые объекты и необходимо по окончании рабочего дня эти toooccur действия синхронизации. tooremove эти переопределения:

1. Во время обновления **снимите** hello параметр **запуск процесса синхронизации hello после завершения конфигурации**. Это отключит Планировщик синхронизации hello и предотвращает цикл синхронизации осуществляются автоматически до удаления hello переопределения.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. После завершения обновления выполните следующие toofind командлет out добавили какие переопределения hello:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > переопределения Hello связаны с конкретной соединителя. В hello в примере, действия полный импорт и полную синхронизацию были добавлены tooboth hello локального соединителя AD и соединителя Azure AD.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Запишите hello существующие переопределения, которые были добавлены.
   
4. полный импорт и полную синхронизацию на произвольный соединитель, запустите следующий командлет hello переопределяет tooremove hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   переопределения hello tooremove на все соединители, выполните следующий сценарий PowerShell hello:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume планировщик hello, запустите следующий командлет hello:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Не забывайте действия синхронизации tooexecute hello необходимые по своему усмотрению раннее. Можно либо вручную выполните следующие действия с помощью диспетчера службы синхронизации hello или добавить обратно с помощью командлета Set-ADSyncSchedulerConnectorOverride hello переопределения hello.

полный импорт и полную синхронизацию на произвольный соединитель, запустите следующий командлет hello переопределяет tooadd hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об интеграции локальных удостоверений см. в статье [Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md).
