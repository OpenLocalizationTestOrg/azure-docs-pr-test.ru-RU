---
title: "aaaConfigure вашей службе управления API, с помощью Git - Azure | Документы Microsoft"
description: "Узнайте, как toosave и настройки конфигурации службы управления API, с помощью Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Как toosave и настройки конфигурации службы управления API, с помощью Git
> 
> 

Каждый экземпляр службы управления API поддерживает базу данных конфигурации, содержащий сведения о конфигурации hello и метаданных для экземпляра службы hello. Изменения могут выполняться экземпляр службы toohello, изменив параметр в портал издателя hello, с помощью командлета PowerShell или сделав вызова интерфейса API REST. В дополнение к этому toothese методов, можно также управлять конфигурацию экземпляра службы с помощью Git, такие как Включение сценариев управления службы:

* Управление версиями конфигурации — скачивание и хранение различных версий конфигурации службы.
* Массового изменения конфигурации — вносить изменения в ваш локальный репозиторий в toomultiple части конфигурации службы и интеграции сервера задней toohello hello изменения с одной операцией
* Знакомых инструментов Git и рабочий процесс — использовать инструментарий Git hello и рабочие процессы, которые вы уже знакомы с

Следующая схема Hello приведен обзор способов tooconfigure hello вашего экземпляра службы управления API.

![Настройка с помощью Git][api-management-git-configure]

При внесении изменений с помощью портала издателя hello, командлеты PowerShell или hello REST API службы tooyour вы управляете база данных конфигурации службы с помощью hello `https://{name}.management.azure-api.net` конечной точки, как показано hello правой части схемы hello. Hello слева hello диаграммы показано, как можно управлять конфигурации службы с помощью Git и репозитория Git в службе, расположенный `https://{name}.scm.azure-api.net`.

следующие шаги Hello предоставляют Обзор управления вашего экземпляра службы управления API, с помощью Git.

1. Доступ к конфигурации Git в службе
2. Сохранить репозиторий Git tooyour базы данных конфигурации службы
3. Клонирование hello репозитория Git tooyour локального компьютера
4. По запросу hello последнюю репозитория вниз tooyour локального компьютера и фиксации и принудительного занесения репозитория задней tooyour изменения
5. Развертывание изменений hello из вашего репозитория в базу данных конфигурации службы

В этой статье описывается как tooenable и использовать Git toomanage конфигурации службы и ссылки для hello файлов и папок в репозитории hello.

## <a name="access-git-configuration-in-your-service"></a>Доступ к конфигурации Git в службе
Можно быстро просмотреть состояние hello конфигурации Git, просмотрев hello Git значок в правом верхнем углу hello hello портала издателя. В этом примере сообщение о состоянии hello указывает на наличие toohello репозитория несохраненных изменений. Это так, как база данных конфигурации службы управления API hello еще не были сохранены toohello репозитория.

![Состояние Git][api-management-git-icon-enable]

tooview и настроить параметры конфигурации Git, можно щелкнуть значок Git hello, или щелкните hello **безопасности** меню и перейдите toohello **репозиторий конфигураций** вкладки.

![Включение доступа к GIT][api-management-enable-git]

> [!IMPORTANT]
> Все секреты, которые не определены как свойства сохраняются в репозитории hello и будет оставаться в журнал только после отключения и повторного включения доступа Git. Свойства предоставляют toomanage надежном месте постоянные строковые значения, включая секретные данные, для всех API конфигурации и политики, поэтому не нужно toostore их непосредственно в инструкциях политики. Дополнительные сведения см. в разделе [как toouse свойств политики управления API Azure](api-management-howto-properties.md).
> 
> 

Сведения по включению и отключению Git доступ с помощью hello REST API см. в разделе [разрешить или запретить доступ Git с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>репозиторий Git toohello конфигурации службы toosave hello
Первым шагом Hello перед клонированием репозитория hello является toosave hello текущее состояние конфигурации toohello hello службы хранилища. Нажмите кнопку **сохранить toorepository конфигурации**.

![Сохранение конфигурации][api-management-save-configuration]

Внесите необходимые изменения на экране подтверждения hello и нажмите кнопку **ОК** toosave.

![Сохранение конфигурации][api-management-save-configuration-confirm]

Через несколько секунд hello конфигурация сохраняется и отображается состояние конфигурации hello hello репозитория, в том числе hello дату и время последнего изменения конфигурации hello и hello последней синхронизации конфигурации службы hello и hello репозиторий.

![Состояние конфигурации][api-management-configuration-status]

После сохранения конфигурации hello toohello репозиторий можно клонировать.

Дополнительные сведения о выполнении этой операции с помощью API-интерфейса REST hello. в разделе [конфигурации фиксации моментальных снимков с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>tooclone hello tooyour хранилище локального компьютера
tooclone репозитория, необходимо репозитория tooyour hello URL-адрес, имя пользователя и пароль. Hello имя пользователя и URL-адреса отображаются вверху hello hello **репозиторий конфигураций** вкладки.

![Клонирование репозитория Git][api-management-configuration-git-clone]

пароль Hello создается внизу hello hello **репозиторий конфигураций** вкладки.

![Создание пароля][api-management-generate-password]

toogenerate пароль, сначала убедитесь, что hello **срока действия** toohello требуемого Дата окончания срока действия и время, а затем нажмите кнопку **создать токен**.

![Пароль][api-management-password]

> [!IMPORTANT]
> Запомните этот пароль. После закрытия этого пароля страницы приветствия больше не будет отображаться.
> 
> 

Следующие примеры использования hello Git Bash Hello средства из [Git для Windows](http://www.git-scm.com/downloads) , но можно использовать любое средство Git, вам знакомы.

Откройте ваш инструмент Git в нужной папке hello и запустите hello следующая команда tooclone hello git репозитория tooyour локального компьютера, с помощью команды hello, предоставляемые hello портала издателя.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Укажите имя пользователя hello и пароль при появлении запроса.

При появлении ошибки, попробуйте изменить ваш `git clone` команды tooinclude hello пользователя имя и пароль, как показано в следующий пример hello.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Если это обеспечивает ошибку, попробуйте hello пароль часть команды hello кодирование URL-адресов. Один toodo быстро это tooopen Visual Studio, и проблема hello следующие команды в hello **окна интерпретации**. tooopen hello **окна интерпретации**, открыть все решение или проект в Visual Studio (или создайте новый пустой консольное приложение) и выберите **Windows**, **Интерпретация** из Hello **отладки** меню.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Используйте пароль в кодировке hello вместе с пользователем имя и репозитория расположение tooconstruct hello git команду.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

После клонирования репозитория hello можно просматривать и работать с ними в локальной файловой системе. Дополнительные сведения см. в разделе [Справочные сведения по структуре файлов и папок локального репозитория Git](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate ваш локальный репозиторий с hello последнюю конфигурацию экземпляра службы
При внесении экземпляра службы управления API tooyour изменений в портал издателя hello или с помощью API-интерфейса REST hello репозитория toohello эти изменения необходимо сохранить перед обновлением ваш локальный репозиторий с последними изменениями hello. toodo, нажмите кнопку **сохранить конфигурации toorepository** на hello **репозиторий конфигураций** в портал издателя hello, а затем выполните следующую команду в ваш локальный репозиторий hello.

```
git pull
```

Перед запуском `git pull` убедитесь, что вы находитесь в папке hello ваш локальный репозиторий. Если Вы завершили hello `git clone` команды, то необходимо изменить, выполнив команду следующего вида hello hello каталог tooyour репозитория.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>изменения toopush из вашего репозитория сервера toohello локального репозитория
изменяет toopush из репозитория сервера toohello локального репозитория, необходимо сохранить изменения и отправить их toohello серверный репозиторий. toocommit изменения, откройте ваш Git средство командной строки, коммутатор toohello каталог локального репозитория, а проблема hello, следующие команды.

```
git add --all
git commit -m "Description of your changes"
```

toopush все hello фиксирует toohello сервером, выполните следующую команду hello.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy любой службы конфигурации изменения toohello экземпляра службы управления API
После фиксации и внедренные toohello серверный репозиторий, локальных изменений их можно развернуть tooyour экземпляра службы управления API.

![Развернуть][api-management-configuration-deploy]

Дополнительные сведения о выполнении этой операции с помощью API-интерфейса REST hello. в разделе [Git развернуть изменения tooconfiguration базы данных с помощью API-интерфейса REST hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Справочные сведения по структуре файлов и папок локального репозитория Git
Hello файлов и папок в локальном репозитории hello содержат hello конфигурации сведения о hello экземпляра службы.

| Элемент | Описание |
| --- | --- |
| Корневая папка api-management |Содержит конфигурации верхнего уровня для экземпляра службы hello |
| Папка apis |Содержит настройки hello hello API-интерфейсы в экземпляре службы hello |
| Папка groups |Содержит hello конфигурацию для группы hello в экземпляре службы hello |
| Папка policies |Содержит политики hello в экземпляре службы hello |
| Папка portalStyles |Содержит hello конфигурации для настройки портала разработчиков hello в экземпляре службы hello |
| Папка products |Содержит настройки hello hello продуктов в экземпляре службы hello |
| Папка templates |Содержит настройки hello hello шаблонов сообщений электронной почты в экземпляре службы hello |

В каждой папке может находиться один или несколько файлов и в некоторых случаях одна или несколько папок, например папка для каждого API, продукта или группы. Hello файлов в каждой папке характерные для типа сущности hello, описываемого hello имя папки.

| Тип файла | Назначение |
| --- | --- |
| json |Сведения о соответствующей сущности hello конфигурации |
| html |Описание сущности hello, часто отображается на портале разработчиков hello |
| xml |Правила политики |
| css |Таблицы стилей для настройки портала разработчика |

Эти файлы можно создать, удалить, изменить и управляются на локальной файловой системе, и изменения hello развернуты задней toohello вашего экземпляра службы управления API.

> [!NOTE]
> Hello следующие сущности не хранятся в репозитории hello и не может быть настроен с использованием Git.
> 
> * Пользователи
> * Подписки
> * Свойства
> * Сущности портала разработчика, отличные от стилей
> 
> 

### <a name="root-api-management-folder"></a>Корневая папка api-management
корневой Hello `api-management` папка содержит `configuration.json` файл со сведениями о hello экземпляру службы в кодировке hello верхнего уровня.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Здравствуйте первых четырех параметров (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, и `UserRegistrationTermsConsentRequired`) сопоставить следующие параметры на hello toohello **удостоверения** hello на вкладке **безопасности** раздела.

| Параметр удостоверения | Сопоставляет слишком|
| --- | --- |
| RegistrationEnabled |**Анонимные пользователи в toosign страницы перенаправления** флажок |
| UserRegistrationTerms |**Условия использования при регистрации пользователя**  |
| UserRegistrationTermsEnabled |**Показывать условия использования на странице регистрации**  |
| UserRegistrationTermsConsentRequired |**Требовать согласия**  |

![Параметры удостоверений][api-management-identity-settings]

Здравствуйте следующие четыре параметры (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, и `DelegationValidationKey`) сопоставить следующие параметры на hello toohello **делегирования** hello на вкладке **безопасности** раздела.

| Параметр делегирования | Сопоставляет слишком|
| --- | --- |
| DelegationEnabled |Флажок **Делегировать вход и регистрацию** |
| DelegationUrl |**URL-адрес конечной точки делегирования**  |
| DelegatedSubscriptionEnabled |**Делегировать подписку на продукт**  |
| DelegationValidationKey |**Делегировать ключ проверки**  |

![Параметры делегирования][api-management-delegation-settings]

Здравствуйте, Окончательная настройка `$ref-policy`, сопоставляет файл инструкций toohello глобальную политику для экземпляра службы hello.

### <a name="apis-folder"></a>Папка apis
Hello `apis` содержит папку для каждого API в экземпляре службы hello, содержащий hello следующих элементов.

* `apis\<api name>\configuration.json`-Это hello конфигурация для hello API и содержит сведения об операции hello и URL-адрес службы hello серверной части. Это hello же данные, что будет возвращено, если были toocall [получить определенный API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) с `export=true` в `application/json` формате.
* `apis\<api name>\api.description.html`— Это описание hello hello API, соответствует toohello `description` свойство hello [сущность API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Эта папка содержит `<operation name>.description.html` файлы, которые toohello операции сопоставления в hello API. Каждый файл содержит описание hello одной операции в hello API, который сопоставляет toohello `description` свойство hello [сущности операции](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) в hello REST API.

### <a name="groups-folder"></a>Папка groups
Hello `groups` содержит папку для каждой группы, определенные в экземпляре службы hello.

* `groups\<group name>\configuration.json`-Это hello конфигурацию для группы hello. Это hello же данные, что будет возвращено, если были toocall hello [получить имя конкретной группы](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) операции.
* `groups\<group name>\description.html`— Это описание hello группы hello и соответствует toohello `description` свойство hello [группы сущности](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>Папка policies
Hello `policies` папка содержит операторы политики hello для вашего экземпляра службы.

* `policies\global.xml` содержит политики, определенные в глобальной области для экземпляра службы.
* `policies\apis\<api name>\` — если в области API определены какие-либо политики, они содержатся в этой папке.
* `policies\apis\<api name>\<operation name>\`Папка — Если у вас есть какие-либо политики, определенные в области операции, они содержатся в этой папке в `<operation name>.xml` файлы сопоставления toohello инструкций политики для каждой операции.
* `policies\products\`— Если у вас есть какие-либо политики, определенные в области продукта, они содержатся в этой папке, которая содержит `<product name>.xml` файлы сопоставления toohello инструкций политики для каждого продукта.

### <a name="portalstyles-folder"></a>Папка portalStyles
Hello `portalStyles` папка содержит конфигурацию и стиля таблицы для настройки портала разработчиков для экземпляра службы hello.

* `portalStyles\configuration.json`-содержит имена hello hello таблиц стилей, используемых портал разработчиков hello
* `portalStyles\<style name>.css`-каждого `<style name>.css` файл содержит стили для портала разработчиков hello (`Preview.css` и `Production.css` по умолчанию).

### <a name="products-folder"></a>Папка products
Hello `products` содержит папку для каждого продукта, определенных в экземпляре службы hello.

* `products\<product name>\configuration.json`-Это конфигурация hello hello продукта. Это hello же данные, что будет возвращено, если были toocall hello [получить определенный продукт](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) операции.
* `products\<product name>\product.description.html`— Это описание hello hello продукта и соответствует toohello `description` свойство hello [сущности «Продукт»](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) в hello REST API.

### <a name="templates"></a>шаблоны
Hello `templates` папка содержит конфигурацию для hello [шаблоны электронной почты](api-management-howto-configure-notifications.md) hello экземпляра службы.

* `<template name>\configuration.json`-Это конфигурация hello для шаблона сообщения электронной почты hello.
* `<template name>\body.html`— Это текст hello hello шаблона сообщения электронной почты.

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других способах toomanage вашего экземпляра службы. в разделе:

* Управление Вашего экземпляра службы с помощью hello следующие командлеты PowerShell
  * [Справочник по командлетам PowerShell для развертывания службы](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Справочник по командлетам PowerShell для управления службами](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Управление экземпляр службы в портал издателя hello
  * [Управление вашим первым API](api-management-get-started.md)
* Управление Вашего экземпляра службы с помощью API-интерфейса REST hello
  * [Справочник по REST API для управления API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Просмотр видеообзора
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




