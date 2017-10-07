---
title: "aaaGet к работе с хранилищем ключей Azure | Документы Microsoft"
description: "Использовать этот учебник toohelp, вы получаете работы с хранилищем ключей Azure toocreate жесткой контейнера в Azure, toostore и управлять ими, криптографические ключи и секретные данные в Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Приступая к работе с хранилищем ключей Azure
Хранилище ключей Azure доступно в большинстве регионов. Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Введение
Использовать этот учебник toohelp, вы получаете работы с хранилищем ключей Azure toocreate жесткой контейнера (хранилище) в Azure, toostore и управлять ими, криптографические ключи и секретные данные в Azure. Помогает выполнить процесс с помощью Azure PowerShell toocreate hello хранилище, в котором содержится ключ или пароль, который затем можно использовать вместе с приложением Azure. В нем также показано, как приложение может использовать этот ключ или пароль.

**Предполагаемое время toocomplete:** 20 минут

> [!NOTE]
> Этот учебник не содержит инструкций для как toowrite hello Azure приложения, которое содержит один из шагов hello, а именно как tooauthorize приложения toouse ключа или секрета в ключе hello хранилище.
>
> В этом руководстве используется Azure PowerShell. Инструкции по кроссплатформенному интерфейсу командной строки см. в [этом руководстве](key-vault-manage-with-cli2.md).
>
>

Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника необходимо иметь следующие hello:

* TooMicrosoft подписки Azure. Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной учетной записи](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell, **начиная с версии 1.1.0**. tooinstall Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Если вы уже установили Azure PowerShell и вы не знаете версии hello из консоли Azure PowerShell hello, введите `(Get-Module azure -ListAvailable).Version`. Если у вас установлено средство Azure PowerShell версий 0.9.1–0.9.8, вы можете использовать это руководство с некоторыми незначительными поправками. Например, необходимо использовать hello `Switch-AzureMode AzureResourceManager` команды и команд hello хранилище ключей Azure были изменены. Список hello командлетам хранилища ключей для версий 0.9.1 через 0.9.8, в разделе [командлетам](/powershell/module/azurerm.keyvault/#key_vault).
* Приложение, настроенное toouse hello ключ или пароль, который создан в этом учебнике. Образец приложения доступно из hello [центра загрузки Майкрософт](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Инструкции см. в файле Readme, сопровождающие hello.

Этот учебник предназначен для начинающих Azure PowerShell, но предполагается, что вы понимаете базовые понятия hello, например модули, командлеты и сеансов. Дополнительные сведения см. в статье [Начало работы с Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

tooget подробную справку для любого командлета, которое будет отображаться в этом учебнике используйте hello **Get-Help** командлета.

    Get-Help <cmdlet-name> -Detailed

Например, tooget справку для hello **AzureRmAccount входа** командлета введите:

    Get-Help Login-AzureRmAccount -Detailed

Можно также прочитать hello следующие учебники tooget знакомы с диспетчером ресурсов Azure в Azure PowerShell.

* [Как tooinstall и настройка Azure PowerShell](/powershell/azure/overview)
* [Использование Azure PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Подключение tooyour подписки
Запустите сеанс Azure PowerShell и войдите в tooyour учетная запись Azure с hello следующую команду:  

    Login-AzureRmAccount

Обратите внимание, что при использовании определенного экземпляра Azure, например, Azure для государственных, используйте hello - параметр среды с помощью этой команды. Например: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль. Azure PowerShell возвращает все подписки hello, которые связаны с этой учетной записью, а также по умолчанию, использует hello первое.

Если есть несколько подписок и требуется toospecify конкретных один toouse для хранилища ключей Azure, введите hello, следуя toosee hello подписки для учетной записи:

    Get-AzureRmSubscription

Затем toospecify hello подписки toouse, тип:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Дополнительные сведения о настройке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Создание новой группы ресурсов
При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов. Для примера мы создадим новую группу ресурсов с именем **ContosoResourceGroup** :

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Создание хранилища ключей
Используйте hello [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) toocreate командлет хранилища ключей. Этот командлет имеет три обязательных параметра: **имя группы ресурсов**, **имя хранилища ключей**и hello **географическое расположение**.

Например, если вы используете хранилище hello с именем **ContosoKeyVault**, hello группу ресурсов с именем **ContosoResourceGroup**и расположение hello **Восточная Азия**, тип:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

выходные данные командлета Hello приведены свойства ключа хранилища hello, которое вы только что создали. Hello двух наиболее важных свойств:

* **Имя хранилища**: В примере hello это **ContosoKeyVault**. Вы будете использовать это имя для выполнения других командлетов хранилища ключей;
* **Код URI хранилища**: пример hello это https://contosokeyvault.vault.azure.net/. Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.

Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище. Пока что это недоступно для других учетных записей.

> [!NOTE]
> При возникновении ошибки hello **hello подписки не зарегистрированного toouse пространством имен «Microsoft.KeyVault»** при обращении toocreate новое хранилище ключей, выполните `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` и затем снова запустите команду New-AzureRmKeyVault. Дополнительные сведения см. в статье [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Добавление ключа или секрета toohello хранилища ключей
Хранилище ключей Azure toocreate программно защищенного ключа для вас, используйте hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) командлет и введите hello ниже:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Тем не менее если имеется существующий программно защищенного ключа. Файл сохранен PFX tooyour C:\ диск в файл с именем, которые должны tooupload tooAzure хранилище ключей, тип hello следующая переменная hello tooset softkey.pfx **securepfxpwd** пароль **123** для hello. PFX-файла:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Затем введите следующую tooimport hello ключ из hello hello. PFX-файл, который защищает hello с помощью программного обеспечения в hello службы хранилища ключей:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Теперь можно ссылаться на этот ключ, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес. Используйте **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways получения текущей версии hello и **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget этой конкретной версии.  

hello toodisplay URI для этого ключа типа:

    $Key.key.kid

tooadd хранилище toohello секретный пароль, с именем SQLPassword и имеют значение hello Pa$ $w0rd tooAzure хранилище ключей, сначала преобразуйте значение hello Pa$ $w0rd tooa защищенной строки, введя следующее hello:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Затем введите hello следующее:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Теперь можно ссылаться на этот пароль добавили tooAzure хранилище ключей с помощью URI-адрес. Используйте **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways получения текущей версии hello и **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget этой конкретной версии.

hello toodisplay URI для этот секрет типа:

    $secret.Id

Позволяет просмотреть hello ключа или секрета, который вы только что создали:

* tooview вашей, введите:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview в тайне, тип:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Теперь хранилища ключей и ключа или секрета готова для toouse приложений. Toouse приложений необходимо авторизовать их.  

## <a id="register"></a>Регистрация приложения в Azure Active Directory
Обычно этот шаг выполняет разработчик на отдельном компьютере. Он не tooAzure конкретного хранилища ключей, но указан для полноты.

> [!IMPORTANT]
> Учебник toocomplete hello, учетная запись, хранилище hello и приложения hello, которое будет зарегистрирован на этом шаге необходимо в hello один каталог Azure.
>
>

Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory. toodo, hello владелец приложения hello сначала необходимо зарегистрировать приложение hello в своем Azure Active Directory. В конце hello регистрации владелец приложения hello возвращает hello следующие значения:

* **Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет hello). приложение Hello необходимо представить оба этих значения tooAzure Active Directory, tooget маркер. Как приложение hello настраивается toodo это зависит от приложения hello. Для hello образец приложения хранилища ключей владелец приложения hello устанавливает эти значения в файле app.config hello.

приложение hello tooregister в Azure Active Directory:

1. Войдите в систему toohello классический портал Azure.
2. В левой части экрана приветствия щелкните **Active Directory**и выберите каталог hello, в котором будет зарегистрировать приложение. <br> <br> **Примечание:** hello необходимо выбрать каталог, содержащий hello подписки Azure, в которой для создания хранилища ключей. Если вы не знаете, какой каталог это, нажмите кнопку **параметры**идентификации hello подписки, в которой для создания хранилища ключей и Примечание hello hello directory название hello последнего столбца.
3. Щелкните **ПРИЛОЖЕНИЯ**. Если приложения не были добавлены tooyour каталог, на этой странице отображаются только hello **добавить приложение** ссылку. Щелкните ссылку hello, или в качестве альтернативы можно щелкнуть **добавить** на панели команд hello.
4. В hello **добавить приложение** мастера hello **что вам требуется toodo?** щелкните **добавить приложение, разрабатываемое моей организацией**.
5. На hello **Расскажите о своем приложении** страницы, укажите имя для приложения и выберите **веб-приложение и/или WEB API** (по умолчанию hello). Нажмите кнопку hello **Далее** значок.
6. На hello **свойства приложения** укажите hello **URL-адрес входа** и **URI идентификатора приложения** для веб-приложения. Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях). Неважно, существуют ли эти сайты. Важно то, что URI идентификатора приложения hello для каждого приложения отличается для каждого приложения в каталоге. каталог Hello используется этой строки tooidentify приложений.
7. Нажмите кнопку hello **завершить** toosave значок изменения в мастере hello.
8. На hello **быстрый запуск** щелкните **Настройка**.
9. Прокрутите toohello **ключей** выберите длительность hello и нажмите кнопку **Сохранить**. Страница приветствия обновляется и теперь отображается значение ключа. Необходимо настроить приложение с таким значением ключа и hello **идентификатор КЛИЕНТА** значение. (указания по этой конфигурации зависят от конкретного приложения).
10. На этой странице, который будет использоваться в hello следующий шаг tooset разрешения на ваше хранилище, скопируйте значение идентификатора клиента hello.

## <a id="authorize"></a>Авторизовать hello приложения toouse hello ключа или секрета
tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) командлета.

Например, если имя хранилища — **ContosoKeyVault** и tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и вы хотите toodecrypt приложения hello tooauthorize входа с ключами в приложение hello хранилище, выполните следующие hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Если требуется, чтобы toouse аппаратный модуль безопасности (HSM)
Для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello. Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки. Если это требование не распространяется tooyou, пропустите этот раздел и перейдите слишком[удалить hello хранилища ключей и связанные ключи и секретные данные](#delete).

toocreate этих ключей, защищенных HSM, необходимо использовать hello [хранилище ключей Azure Premium службы ключей, защищенных HSM toosupport уровня](https://azure.microsoft.com/pricing/free-trial/). Обратите внимание, эта функция недоступна для Китая.

При создании хранилища ключей hello добавить hello **- SKU** параметр:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Можно добавить программно защищенных ключей (как показано выше) и хранилища ключей toothis ключей, защищенных HSM. toocreate Перенос аппаратно защищенного ключа набора hello **-назначения** too'HSM параметр ":

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Можно использовать следующие команды tooimport hello ключа из. PFX-файл на компьютере. Эта команда импортирует ключ hello в аппаратные модули безопасности в hello службы хранилища ключей:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


Hello следующая команда импортирует «принеси свой собственный ключ» (BYOK) пакета. Этот сценарий позволяет создание ключа в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Более подробные инструкции о том, как toogenerate этот пакет BYOK разделе [как toogenerate и передача ключей, защищенных HSM для хранилища ключей Azure](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Удаление хранилища ключей hello и связанные ключи и секретные данные
Если вы больше не нужна hello хранилища ключей и hello ключа или секрета, который его содержит, можно удалить hello хранилища ключей с помощью hello [AzureRmKeyVault удаление](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) командлета:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Или можно удалить группы весь ресурс Azure, которая включает в себя хранилище ключей hello и другие ресурсы, которые включены в эту группу:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Другие командлеты Azure PowerShell
Другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'` — эта команда отображает все ключи и выбранные свойства в виде таблицы;
* `$Keys[0]`: Эта команда отображает полный список свойств для указанного ключа hello
* `Get-AzureKeyVaultSecret` — эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы;
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Пример как tooremove определенного ключа.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Пример как tooremove конкретных секрета.

## <a id="next"></a>Дальнейшие действия
Подробное руководство по использованию хранилища ключей Azure в веб-приложении см. в [этой статье](key-vault-use-from-web-application.md).

toosee используется хранилище ключей в статье [ведение журнала хранилища ключей Azure](key-vault-logging.md).

Список hello новые командлеты Azure PowerShell для хранилища ключей Azure см. в разделе [командлетам](/powershell/module/azurerm.keyvault/#key_vault).

Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).
