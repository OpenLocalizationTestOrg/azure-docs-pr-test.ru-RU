---
title: "Azure AD Connect: поддерживаемые топологии | Документация Майкрософт"
description: "В этой статье подробно описываются поддерживаемые и неподдерживаемые топологии Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Топологии Azure AD Connect.
Эта статья описывает различные локальные и топологии Active Directory Azure (Azure AD), которые используется синхронизация Azure AD Connect в качестве решения интеграции hello. Здесь описываются и поддерживаемые, и неподдерживаемые конфигурации.

Вот hello условные обозначения для изображения в статье hello.

| Описание | Знак |
| --- | --- |
| Локальный лес Active Directory |![Локальный лес Active Directory](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Локальная служба Active Directory с фильтрацией импорта |![Active Directory с фильтрацией импорта](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Сервер синхронизации Azure AD Connect |![Сервер синхронизации Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Промежуточный режим сервера синхронизации Azure AD Connect |![Промежуточный режим сервера синхронизации Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync с Forefront Identity Manager (FIM) 2010 или Microsoft Identity Manager (MIM) 2016 |![GALSync с FIM 2010 или MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Сервер синхронизации Azure AD Connect, подробно |![Сервер синхронизации Azure AD Connect, подробно](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Неподдерживаемый сценарий |![Неподдерживаемый сценарий](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Один лес, один клиент Azure AD
![Топология для одного леса и одного клиента](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

наиболее распространенные топология Hello — один локальный лес с одним или несколькими доменами и один Azure AD для клиента. Для проверки подлинности Azure AD используется синхронизация паролей. экспресс-установки Hello из Azure AD Connect поддерживает только этой топологии.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Один лес, нескольких клиентов Azure AD tooone серверов синхронизации
![Неподдерживаемая отфильтрованная топология для одного леса](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Наличие нескольких серверов синхронизации Azure AD Connect, подключенных toohello же Azure AD клиента не поддерживается, кроме [тестового сервера](#staging-server). Он содержит неподдерживаемую, даже если эти серверы, настроенные toosynchronize с взаимно исключающих набора объектов. Можно считать в этой топологии не могут получить доступ всех доменов в лесу hello с одного сервера или если требуется toodistribute загрузки между несколькими серверами.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Несколько лесов, один клиент Azure AD
![Топология для нескольких лесов и одного клиента](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Во многих организациях есть среды, которые включают несколько локальных лесов Active Directory. Есть разные причины существования нескольких локальных лесов Active Directory. Типичными примерами являются проекты с помощью ресурсов учетной записи леса и hello результат слияния или приобретения.

Если у вас есть несколько лесов, все они должны быть доступными для одного сервера синхронизации Azure AD Connect. У вас нет домена tooa toojoin hello сервера. При необходимости tooreach всех лесах hello server можно разместить в сети периметра (также известный как DMZ, демилитаризованная зона и промежуточной подсетью).

Мастер установки Hello Azure AD Connect предлагает несколько пользователей tooconsolidate параметры, которые представлены в нескольких лесах. Hello предназначена только один раз представлены пользователя в Azure AD. Существуют некоторые общие топологии, которые можно настроить в hello пользовательский путь установки в мастере установки hello. На hello **уникальное определение пользователей** страницы приветствия выберите соответствующий параметр, представляющий топологии. Консолидация Hello настроен только для пользователей. Повторяющиеся группы не объединяются с конфигурацией по умолчанию hello.

Общие топологии описаны в разделах hello о [отдельные топологии](#multiple-forests-separate-topologies), [полной сетки](#multiple-forests-full-mesh-with-optional-galsync), и [hello топологии ресурсов учетной записи](#multiple-forests-account-resource-forest).

Конфигурация по умолчанию Hello в Azure AD Connect sync предполагает:

* Каждый пользователь имеет только одну включенную учетную запись и hello лесу, где находится эта учетная запись является используется tooauthenticate hello пользователем. Это предположение относится как к синхронизации паролей, так и к федерации. Параметры UserPrincipalName и sourceAnchor/immutableID поступают из этого леса.
* У каждого пользователя есть только один почтовый ящик.
* Hello леса, на котором размещен почтовый ящик пользователя hello имеет hello наилучшее качество данных для атрибутов, которые отображаются в глобальном списке адресов (GAL) Exchange hello. Если нет ни одного почтового ящика для пользователя hello, любого леса можно использовать toocontribute значений этих атрибутов.
* Если у пользователя есть связанный почтовый ящик, то есть и другая учетная запись в другом лесу, которая используется для входа.

Если вашей среде, не соответствует предположений, hello выполняются следующие действия.

* Если имеется более одной активной учетной записи или более одного почтового ящика, модуль синхронизации hello выбирает один и игнорирует hello других.
* Связанный почтовый ящик с нет других активной учетной записи не экспортированного tooAzure AD. Учетная запись пользователя Hello не представлены в виде элемента в любую группу. В DirSync связанный почтовый ящик всегда будет представлен как обычный почтовый ящик. Это изменение предназначено специально сценарии несколькими лесами поддержки toobetter по-разному.

Дополнительные сведения в [основные сведения о настройке по умолчанию hello](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Несколько лесов, нескольких клиентов Azure AD tooone серверов синхронизации
![Неподдерживаемая топология для нескольких лесов и нескольких серверов синхронизации](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Наличие tooa подключен сервер синхронизации для нескольких Azure AD Connect единственный клиент Azure AD не поддерживается. Hello исключением является использование hello [тестового сервера](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Несколько лесов, отдельные топологии
![Параметр для представления пользователей во всех каталогах только один раз](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Изображение нескольких лесов и отдельных топологий](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

В этой среде все локальные леса рассматриваются как отдельные сущности. В любых других лесах пользователи отсутствуют. Каждый лес имеет свою собственную организацию Exchange, и между лесами hello отсутствует. В этой топологии может быть hello ситуации после слияний и поглощений или в организации, где каждого филиала работают независимо друг от друга. Эти леса принадлежат hello одной организации в Azure AD и отображаются вместе с унифицированной GAL. В предшествующих рисунок hello каждый объект в каждом лесу представляется в метавселенной hello и статистические вычисления в hello целевом клиенте Azure AD.

### <a name="multiple-forests-match-users"></a>Несколько лесов: сопоставление пользователей
Общие tooall этих сценариев —, распространения и группы безопасности могут содержать пользователей, контактов и участников внешней безопасности (FSP). FSP используются в доменных службах Active Directory (AD DS) toorepresent члены из других лесов, входящих в группу безопасности. Все FSP являются реальным объектом toohello разрешить в Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Несколько лесов: полная сетка с дополнительным решением GALSync
![Для с помощью атрибута mail hello для сопоставления при удостоверения пользователей существуют в нескольких каталогах](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Топология полной сетки для нескольких лесов](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Топология полной сетки позволяет пользователям и toobe ресурсы, расположенные в любом лесу. Как правило существуют двусторонние отношения доверия между лесами hello.

Если Exchange присутствует в нескольких лесах, может быть доступным дополнительное локальное решение GALSync. Каждый пользователь будет представлен во всех остальных лесах как контакт. GALSync часто реализуется через FIM 2010 или MIM 2016. Azure AD Connect нельзя использовать в локальном решении GALSync.

В этом сценарии объекты удостоверений соединены через атрибут mail hello. Пользователь с почтовым ящиком в одном лесу соединяется с контактами hello в hello других лесах.

### <a name="multiple-forests-account-resource-forest"></a>Несколько лесов: лес ресурсов учетной записи
![Вариант использования атрибутов ObjectSID и msExchMasterAccountSID hello для сопоставления при удостоверения существуют в нескольких каталогах](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Топология леса ресурсов учетной записи для нескольких лесов](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

В топологии леса ресурсов учетной записи есть один или несколько лесов *учетных записей* с активными учетными записями пользователей. Может также существовать один (или несколько) лес *ресурсов* с отключенными учетными записями.

В этом сценарии один (или несколько) лес ресурсов доверяет всем лесам учетных записей. Лес ресурсов Hello обычно имеет расширенную схему Active Directory с Exchange и Lync. Все службы Exchange и Lync, а также другие общие службы находятся в этом лесу. Пользователи имеют отключенной учетной записи пользователя в этом лесу, и связанных почтовых ящиков hello toohello учетной записи леса.

## <a name="office-365-and-topology-considerations"></a>Аспекты топологии в Office 365.
Некоторые рабочие нагрузки Office 365 налагают ряд ограничений на поддерживаемые топологии.

| Рабочая нагрузка | Ограничения |
--------- | ---------
| Exchange Online | Если имеется более одной локальной организации Exchange (то есть Exchange была развернутой toomore чем одном лесе), необходимо использовать Exchange 2013 с пакетом обновления 1 или более поздней версии. Дополнительные сведения см. в статье [Гибридные развертывания в нескольких лесах Active Directory](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype для бизнеса | При использовании нескольких локальных лесов поддерживается только топологии леса ресурсов учетной записи hello. Дополнительные сведения см. в статье [Требования к среде Skype для бизнеса Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>промежуточного сервера
![Промежуточный сервер в топологии](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect поддерживает установку второго сервера в *промежуточном режиме*. Считывает данные из всех подключенных каталогах сервера в этом режиме, но ничего не записывают tooconnected каталоги. Он использует цикл синхронизации обычный hello и поэтому имеет обновленную копию hello учетных данных.

После аварии, где происходит сбой сервера-источника hello можно выполнить переход toohello тестового сервера. Для этого в мастере Azure AD Connect hello. Этот второй сервер может располагаться в другом центре обработки данных, так как без инфраструктуры с основным сервером hello. Изменения конфигурации, внесенные на втором сервере hello сервера-источника toohello необходимо скопировать вручную.

Можно использовать промежуточный tootest server новых пользовательских hello и Настройка эффектов, оно повлияет на данные. Можно просмотреть изменения hello и настроить параметры конфигурации hello. Если вы довольны hello новую конфигурацию, можно внести hello промежуточного сервера hello активного сервера и режим hello старого активного сервера toostaging.

Можно также использовать этот метод tooreplace hello active sync сервера. Подготовка нового сервера hello и задать для него режим toostaging. Убедитесь, что он находится в рабочем состоянии, отключите промежуточный режим (сделать его активным) и завершите работу hello текущего активного сервера.

Это возможно toohave больше, чем один промежуточный сервер при необходимости toohave нескольких резервных копий в разных центрах обработки данных.

## <a name="multiple-azure-ad-tenants"></a>Множество клиентов Azure AD
Мы рекомендуем использовать один клиент в Azure AD для всей организации.
При планировании toouse нескольких клиентов Azure AD, см. статье hello [Управление административными единицами в Azure AD](../active-directory-administrative-units-management.md). В ней описываются стандартные сценарии, в которых можно использовать один клиент.

![Топология для нескольких лесов и нескольких клиентов](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Между сервером синхронизации Azure AD Connect и клиентом Azure AD устанавливается отношение 1:1. Для каждого клиента Azure AD потребуется установить отдельный сервер синхронизации Azure AD Connect. экземпляры клиента Azure AD Hello, изолируются конструктора. То есть пользователи в один клиент не могли видеть пользователей в hello другим клиентом. Если вам необходимо это разделение, это поддерживаемая конфигурация. В противном случае следует использовать hello одной модели клиента Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Каждый объект, повторяющийся только один раз в клиенте Azure AD
![Отфильтрованная топология для одного леса](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

В этой топологии один сервер синхронизации Azure AD Connect — клиента подключенных tooeach Azure AD. Hello Azure AD Connect sync серверы должны быть настроены для фильтрации, так что каждая содержит набор взаимно исключают друг друга объекты toooperate. Можно например, определить область каждого сервера tooa конкретный домен или подразделение.

Домен DNS может быть зарегистрирован только в одном клиенте Azure AD. Hello UPN пользователей hello в hello локальным экземпляром Active Directory необходимо также использовать отдельные пространства имен. Например, в предшествующих рисунок hello, три отдельном суффиксов UPN регистрируются в hello локальным экземпляром Active Directory: contoso.com и fabrikam.com, wingtiptoys.com. Hello пользователей в каждом домене Active Directory в локальной среде используйте другое пространство имен.

Нет отсутствует между hello экземпляры клиента Azure AD. Здравствуйте адресной книге в Exchange Online и Скайп Business показаны только для пользователей в hello того же клиента.

В данной топологии есть hello следующие ограничения, в противном случае — Поддерживаемые сценарии:

* Только один из клиентов hello Azure AD могут предоставлять гибридный Exchange hello локальным экземпляром Active Directory.
* устройство под управлением Windows 10 можно связать только с одним клиентом Azure AD;
* Hello единого входа (SSO) параметр для синхронизации и сквозной проверки подлинности пароль может использоваться только один клиенте Azure AD.

требование Hello взаимно исключающих набора объектов также применяется toowriteback. Эта топология не будет поддерживать некоторые функции обратной записи, так как они предполагают наличие одной локальной конфигурации. Эти функции включают в себя следующие:

* групповая обратная запись в конфигурации по умолчанию;
* обратная запись устройств.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Каждый объект, повторяющийся несколько раз в клиенте Azure AD
![Неподдерживаемая топология для одного леса и нескольких клиентов](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Неподдерживаемая топология для одного леса и нескольких соединителей](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Следующие задачи не поддерживаются:

* Синхронизация hello же клиентам toomultiple Azure AD пользователя.
* изменение конфигурации таким образом, чтобы пользователи одного клиента Azure AD отображались в другом клиенте Azure AD как контакты;
* Изменение данных клиента Azure AD toomultiple tooconnect синхронизации Azure AD Connect.

### <a name="galsync-by-using-writeback"></a>Синхронизация GALSync с помощью обратной записи
![Неподдерживаемая топология для нескольких лесов и нескольких каталогов с синхронизацией GALSync, сфокусированной на Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Неподдерживаемая топология для нескольких лесов и нескольких каталогов с синхронизацией GALSync, сфокусированной на локальном каталоге Active Directory](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Клиенты Azure AD являются изолированными по своей природе. Следующие задачи не поддерживаются:

* Изменение конфигурации hello Azure AD Connect sync tooread данных из другого клиента Azure AD.
* Экспортируйте пользователей как в локальной среде Active Directory контактов tooanother экземпляр с помощью синхронизации Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>Синхронизация GALSync с локальным сервером синхронизации
![Синхронизация GALSync в топологии для нескольких лесов и нескольких каталогов](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Можно использовать FIM 2010 или MIM 2016 локальных toosync пользователей (с помощью GALSync) между двумя организациями Exchange. Hello пользователям в одной организации отображаются как внешние пользователи и контакты в hello другой организации. Затем эти локальные экземпляры Active Directory можно синхронизировать с их собственными клиентами Azure AD.

## <a name="next-steps"></a>Дальнейшие действия
tooinstall Azure AD Connect для этих сценариев. в статье toolearn [выборочной установки из Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Дополнительные сведения об интеграции локальных удостоверений см. в статье [Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md).
