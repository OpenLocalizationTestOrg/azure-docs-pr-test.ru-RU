---
title: "aaaCreate пользовательские роли для управления доступом на основе ролей и назначения toointernal и внешних пользователей в Azure | Документы Microsoft"
description: "Назначение настраиваемых ролей RBAC, созданных с помощью PowerShell и интерфейса командной строки, внутренним и внешним пользователям."
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Общие сведения об управлении доступом на основе ролей

Управление доступом на основе ролей функция Azure портала только разрешение hello владельцев подписки tooassign детализированных ролей tooother пользователи могут управлять областей определенного ресурса в своей среде.

RBAC позволяет более эффективного управления безопасности для крупных организаций, а также для SMB, работе с внешними участниками, поставщикам или freelancers, которым требуется доступ к ресурсам toospecific в вашей среде, но не обязательно toohello всей инфраструктуры или любой области действия, связанные с выставления счетов. RBAC обеспечивает гибкость hello владельцам одной подписки Azure под управлением учетной записи администратора hello (роль администратора служб на уровне подписки) и имеют несколько пользователей, которые приглашены toowork под hello но без одной подписке любое администратора права для него. Для управления и выставления счетов функция RBAC hello доказывает toobe эффективный параметр времени и управления для использования Azure в различных сценариях.

## <a name="prerequisites"></a>Предварительные требования
С помощью RBAC в среде Azure hello требуются:

* Наличие автономного подписки Azure назначенный пользователь toohello имени владельца (роль подписка)
* Роль владельца hello объекта hello подписки Azure
* Имеет доступ toohello [портал Azure](https://portal.azure.com)
* Убедитесь, что следующие поставщики ресурсов hello toohave зарегистрирован для подписки пользователя hello: **Microsoft.Authorization**. Дополнительные сведения о как tooregister hello поставщиков ресурсов см. в разделе [поставщиков диспетчеров ресурсов, регионы, версии API и схем](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Подписки Office 365 или лицензии Azure Active Directory (например: доступ к Active Directory tooAzure) подготовленного портал не качества с помощью RBAC hello Office 365.

## <a name="how-can-rbac-be-used"></a>Как можно использовать RBAC
RBAC можно применять в трех различных областях в Azure. Из hello наибольший области toohello значением снизу к ним относится следующее:

* подписка (самый высокий уровень доступа);
* Группа ресурсов
* Область ресурсов (hello низкий уровень доступа предложения целевой разрешения tooan области отдельных ресурсов Azure)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Назначение ролей RBAC в области видимости hello подписки
Существует два распространенных примера использования RBAC (но это еще не все):

* Внешние пользователи из организаций hello (не является частью пользователя admin hello клиента Azure Active Directory) приглашены toomanage определенные ресурсы или всей подписки hello
* Работа с пользователями внутри организации hello (они являются частью hello Azure Active Directory клиента пользователя), но входит разными командами или группы, которым требуется детального доступа либо toohello всей подписки или toocertain группы ресурсов или ресурсов областей в hello Среда

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Предоставление доступа на уровне подписки внешним пользователям Azure Active Directory
RBAC роли могут быть предоставлены только в выпуске **владельцев** подписки hello таким образом hello admin пользователь должен быть подключен с именем пользователя, в которой это предварительно назначенной ролью или создал hello подписки Azure.

Из hello портал Azure по окончании вход как администратор, выберите «Подписки» и выбрать hello требуемого один.
![колонке подписки на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) по умолчанию, если администратор hello приобрела hello подписки Azure hello пользователя будет показываться как **администратор учетной записи**, то выполняется роль hello подписки. Дополнительные сведения о роли hello подписки Azure см. в разделе [добавить или изменить роли Администратор Azure, управлять hello подписки или службы](/billing/billing-add-change-azure-subscription-administrator.md).

В этом примере hello пользователя «alflanigan@outlook.com» — hello **владельца** из hello «Бесплатной пробной версии» подписки в hello AAD клиента «По умолчанию клиента Azure». Так как этот пользователь является создателем hello hello подписки Azure с hello начальной учетной записи Майкрософт «Outlook» (учетная запись Майкрософт = Outlook Live и т.д.) hello имя домена по умолчанию для всех пользователей, добавленные в этот клиент будет **«@alflaniganuoutlook.onmicrosoft.com»**. Намеренно, синтаксис hello hello нового домена образуется путем объединения имя пользователя и домен hello hello пользователя, создавшего клиент hello и Добавление расширения hello **«. onmicrosoft.com»**.
Кроме того пользователи могут войти, используя имени пользовательского домена в клиенте hello после добавления и проверки его для нового клиента hello. Дополнительные сведения о tooverify имени пользовательского домена в клиенте Azure Active Directory. в статье [добавить каталог tooyour имя пользовательского домена](/active-directory/active-directory-add-domain).

В этом примере каталог hello» по умолчанию клиента Azure» содержит только пользователи с доменным именем hello «@alflanigan.onmicrosoft.com».

После выбора hello подписки, необходимо нажать кнопку hello пользователя с правами администратора **управления доступа (IAM)** и затем **добавить новую роль**.





![Функция "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Параметр "Добавить новую роль" в области "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

Hello следующим шагом является tooselect hello роли toobe назначенный и hello пользователя, которому будет назначен роли RBAC hello. В hello **роли** раскрывающегося меню hello admin пользователь видит только hello встроенных RBAC ролей, доступных в Azure. Подробное описание каждой роли и их назначаемых областей см. в статье [Встроенные роли для управления доступом на основе ролей в Azure](/active-directory/role-based-access-built-in-roles.md).

Hello пользователя с правами администратора, то требуется адрес электронной почты tooadd hello hello внешнего пользователя. Hello ожидается, что поведение для hello внешнего пользователя toonot отображались в hello существующего клиента. После приглашен hello внешнего пользователя, он будут отображаться в списке **подписки > управления доступа (IAM)** со всех hello текущих пользователей, назначенных в данный момент роли RBAC hello область подписки.





![Добавьте роль RBAC toonew разрешения](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Список ролей RBAC на уровне подписки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

пользователь Hello»chessercarlton@gmail.com» было приглашенных toobe **владельца** для подписки «Бесплатной пробной версии» hello. После отправки приглашения hello, hello внешнего пользователя будет отправлено сообщение электронной почты со ссылкой активации.
![Приглашение по электронной почте стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Возможности использования внешних toohello организации, hello новый пользователь не имеет существующие атрибуты в каталоге «По умолчанию клиента Azure» hello. Они будут созданы после hello внешний пользователь предоставил согласие toobe записывается в каталог hello, связанный с подпиской hello, которой он назначен роли.





![Сообщение с приглашением стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

Hello внешнего пользователя отображаются в hello клиента Azure Active Directory теперь как внешнего пользователя, с его можно просмотреть в hello портал Azure и hello классического портала.





![Колонка пользователя Azure Active Directory на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Колонка пользователя Azure Active Directory на классическом портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

В hello **пользователей** распознаваться представления в обоих порталов hello внешних пользователей:

* Тип Hello другой значок в hello портал Azure
* разные источники точки в классическом портале hello Hello

Однако предоставление **владельца** или **участника** tooan доступ внешних пользователей в hello **подписки** области, не допускает каталога toohello администратора hello доступа пользователей Если hello **глобального администратора** допускает это. В свойства пользователя hello, hello **тип пользователя** содержит два общих параметра — **член** и **гостевой** можно определить. Элемент — это пользователь, который регистрируется в каталоге hello, пока гостя является каталогом toohello пригласить пользователя из внешнего источника. Дополнительные сведения см. в статье [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Убедитесь в том, что после ввода учетных данных hello в портале hello, hello внешнего пользователя выбирает hello правильный каталог toosign на. Hello одного пользователя может иметь доступа к каталогам toomultiple выберите один из них, щелкнув имя пользователя hello в верхнем правом углу hello в hello портал Azure и hello в раскрывающемся списке выберите нужный каталог hello.

Без значительной гостя в каталоге hello, hello внешнего пользователя можно осуществлять управление всеми ресурсами для hello подписки Azure, но не может получить доступ к каталогу hello.





![доступ к порталу Azure active directory ограниченных tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory и подписка Azure не имеют дочерних и родительских отношений, в отличие от других ресурсов Azure (например, виртуальные машины, виртуальные сети, веб-приложения, хранилище и т. д.), которые связаны с подпиской Azure. Все hello последний создан, управление и выставлен счет по подписке Azure, пока tooan доступа используется toomanage hello Azure directory подписки Azure. Дополнительные сведения см. в разделе [подписка Azure — это связанные tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Из всех hello встроенных RBAC ролей **владельца** и **участника** предоставляют доступ полное управление tooall ресурсов в среде hello, hello различие, который участник не может создать и удалить новый RBAC роли. Hello другие встроенные роли, например **участника виртуальной машины** обеспечивают полное управление доступ только имя hello, независимо от того, hello ресурсы toohello **группы ресурсов** они созданы в.

Назначение hello встроенных RBAC роль **участника виртуальной машины** на уровне подписки, означает этой роли hello hello, пользователь:

* Можно просмотреть все виртуальные машины независимо от их развертывания даты и hello групп ресурсов, они являются частью
* Имеет полный доступ toohello виртуальных машин управления в подписке hello
* Не удается просмотреть любые другие типы ресурсов в подписке hello
* не может изменять параметры выставления счетов.

> [!NOTE]
> RBAC выполняется Azure портала единственный компонент не предоставляет доступа toohello классического портала.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Назначение встроенных RBAC роли tooan внешних пользователей
Для разных сценариев в этом тесте hello внешнего пользователя «alflanigan@gmail.com» добавляется в качестве **участника виртуальной машины**.




![Встроенная роль "Участник виртуальных машин"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

Hello обычное поведение для данного внешнего пользователя с этой ролью встроенных — toosee и управление ими только виртуальные машины и их смежные диспетчера ресурсов только ресурсы, необходимые во время развертывания. Изначально эти ограниченные роли предоставляют доступ только ресурсы корреспондент tootheir, созданные в hello портал Azure, независимо от некоторых можно будет развернуть hello классическом портале, а также (например: виртуальные машины).





![Обзор роли "Участник виртуальных машин" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Предоставление доступа на уровне подписки для пользователя в hello таким же каталога
поток процесса Hello — идентичные tooadding внешнего пользователя, как hello перспективы предоставление hello RBAC ролью "Администратор", а также hello пользователя, которому предоставляется роль toohello доступа. различие Hello является hello пригласить пользователя не будет получать любые по электронной почте приглашения всех областей hello ресурсов в рамках подписки hello, будут доступны на панели мониторинга hello после входа в систему.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Назначение ролей RBAC в области группы ресурсов hello
Назначение роли RBAC в **группы ресурсов** области имеется идентичные процесс для назначения hello роли на уровне подписки hello, для обоих типов пользователей - либо внешних или внутренних (частью hello один каталог). Hello пользователей, назначенных роли RBAC hello: toosee в своей среде только группы ресурсов hello им была назначена доступ из hello **групп ресурсов** значок в hello портал Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Назначение ролей RBAC в области видимости ресурса hello
Назначение роли RBAC в области ресурсов в Azure имеется идентичные процесс для назначения hello роли на уровне подписки hello, или на уровне группы ресурсов hello, следующие hello же рабочего процесса для обоих сценариев. Опять же, hello, назначенных роли RBAC hello пользователям только элементы hello, что они были назначены доступ, либо в hello **все ресурсы** вкладка или непосредственно в их мониторинга.

Важный аспект для RBAC и в области группы ресурсов или ресурсов области — для hello пользователей toomake toohello убедитесь, что toosign в правильный каталог.





![Вход в каталог на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Назначение ролей RBAC группе Azure Active Directory
Все сценарии hello, с помощью RBAC в трех различных областях hello в привилегии hello предложение Azure управление, развертывание и администрирование различные ресурсы как назначенный пользователь без hello потребность в управлении личные подписки. Для подписки, группы ресурсов или ресурсов области назначена роль RBAC hello независимо от того, все ресурсы hello, созданные далее в пользователями hello назначенный оплачиваются под hello одной подписки Azure где hello пользователи имеют доступ к. Таким образом, hello пользователи, имеющие разрешения администратора для всей подписки Azure выставления счетов имеет полный обзор потребление hello, независимо от того, который управляет hello ресурсы.

Для более крупных организациях могут применяться роли RBAC в hello одинаково для группы Azure Active Directory, учитывая hello перспективы этого пользователя admin hello планирует toogrant hello детального доступа для группы или всей отделами, а не по отдельности для каждого пользователя, таким образом Учитывая его как очень времени и управления эффективный параметр. tooillustrate этот пример, hello **участника** роли был добавлен tooone hello групп в клиенте hello на уровне подписки hello.





![Добавление роли RBAC группе AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Подготовка этих групп безопасности и управление ими выполняется только в Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Создайте пользовательскую поддержку tooopen роли RBAC запросов с помощью PowerShell
Hello встроенных RBAC ролей, которые доступны в Azure гарантировать определенные уровни разрешений, исходя из доступных ресурсов hello в среде hello. Однако если эти роли соответствуют требованиям пользователя admin hello, есть еще больше, создав пользовательские роли RBAC доступа toolimit параметр hello.

Создание пользовательских ролей RBAC требует tootake одной встроенные роли, измените его, затем импортировать обратно в среду hello. Hello загрузки и передачи роли hello управляются с помощью PowerShell или интерфейс командной строки.

Это важные toounderstand hello предварительные условия создания пользовательской роли, которые можно предоставлять детального доступа на уровне подписки hello и также обеспечивают гибкость hello hello пригласить пользователя по открытию запросов на получение поддержки.

Для этого примера hello встроенные роли **чтения** разрешающее tooview доступ для пользователей всех ресурсов hello областей, но не tooedit их или создавать новые был настроен tooallow hello пользователя hello можно открыть запросов поддержки.

Здравствуйте, первое действие экспорта hello **чтения** запускали toobe потребностей роль завершена в PowerShell с повышенными разрешениями от имени администратора.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Снимок экрана PowerShell с ролью RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Затем необходимо tooextract шаблона JSON hello hello роли.





![Шаблон JSON настраиваемой роли RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Типичная роль RBAC состоит из трех основных разделов: **Actions**, **NotActions** и **AssignableScopes**.

В hello **действия** разделе перечислены все hello разрешенных операций для этой роли. Это важные toounderstand, назначенный каждого действия из поставщика ресурсов. В этом случае для создания поддержки билеты hello **Microsoft.Support** должна быть в списке поставщика ресурсов.

возможности toosee toobe все Здравствуйте поставщиков ресурсов доступна и зарегистрирована в вашей подписке, можно использовать PowerShell.
```
Get-AzureRMResourceProvider

```
Кроме того можно искать hello всех hello доступных PowerShell командлеты toomanage hello поставщиков ресурсов.
    ![Снимок экрана PowerShell для управления поставщиком ресурсов](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

Здравствуйте, все действия для определенной роли RBAC ресурсов, перечисленных в разделе "hello" Поставщики toorestrict **NotActions**.
И, наконец является обязательным, этой роли RBAC hello содержит явной подписки hello идентификаторов, где он используется. Hello идентификаторы подписки отображаются в категории hello **AssignableScopes**, в противном случае вы не разрешаются tooimport hello роли в вашей подписке.

После создания и настройки роли RBAC hello, ему toobe импортированных назад hello среды.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

В этом примере hello пользовательское имя для этой роли RBAC является «Чтения поддержки билеты уровнем доступа «допускающей hello пользователя tooview все данные в hello подписки, а также запросов поддержки tooopen.

> [!NOTE]
> Hello только два встроенных ролей RBAC, позволяя действие hello открывающие поддержки запросов, **владельца** и **участника**. Для поддержки запросов может tooopen toobe пользователя он должна быть назначена RBAC только в области hello подписки, так как все запросы на поддержку создается подписка Azure.

Новой пользовательской роли назначен пользователь tooan из hello один каталог.





![Снимок экрана пользовательской роли RBAC импортирована в hello портал Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Снимок экрана: назначение пользовательских импортированных toouser роли RBAC в hello один каталог](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Снимок экрана с разрешениями импортированной настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

пример Hello был дополнительные ограничения hello подробные tooemphasize пользовательской роли RBAC следующим образом:
* может создавать запросы в службу поддержки;
* не может создавать области действия ресурсов (например, виртуальная машина);
* не может создавать группы ресурсов.





![Снимок экрана настраиваемой роли RBAC, используемой для создания запросов в службу поддержки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Снимок экрана пользовательской роли RBAC не удается toocreate виртуальные машины](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Снимок экрана пользовательской роли RBAC не удается toocreate нового RGs.](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Создайте пользовательскую поддержку tooopen роли RBAC запросов с помощью Azure CLI
Запущен на компьютере Mac, а также без необходимости доступа к tooPowerShell, Azure CLI — toogo способом hello.

toocreate действия Hello пользовательской роли являются одинаковыми, с единственным исключением hello, с использованием интерфейса CLI hello роли не могут быть загружены в шаблон JSON, но его можно просмотреть в hello CLI приветствия.

В этом примере я выбрали hello встроенные роли **чтения резервного копирования**.

```

azure role show "backup reader" --json

```





![Снимок экрана интерфейса командной строки с ролью Backup Reader (Читатель резервных копий)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Изменение роли hello в Visual Studio после копирования hello свойства в шаблоне JSON, hello **Microsoft.Support** поставщика ресурсов был добавлен в hello **действия** разделах, чтобы этот пользователь может открыть запросы на поддержку продолжая toobe чтения для hello резервными хранилищами. Еще раз это идентификатор подписки hello необходимые tooadd которых эта роль будет использоваться в hello **AssignableScopes** раздела.

```

azure role create --inputfile <path>

```





![Снимок экрана интерфейса командной строки во время импорта настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

Новая роль Hello теперь доступен в hello портал Azure и процесса любые имена hello hello же, как в предыдущих примерах hello.





![Снимок экрана портала Azure с настраиваемой ролью RBAC, созданной с помощью CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

Начиная с hello последней сборки 2017 г., hello оболочки облако Azure общедоступна. Azure облачной оболочки — это дополнение tooIDE и hello портала Azure. Эта служба предоставляет браузерную оболочку, проходящую аутентификацию и размещенную в Azure. Ее можно установить на компьютере вместо интерфейса командной строки.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
