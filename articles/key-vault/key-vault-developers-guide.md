---
title: "Руководство разработчика aaaAzure ключ хранилища"
description: "Разработчики могут использовать ключи шифрования toomanage хранилище ключей Azure в среде Microsoft Azure hello."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Руководство разработчика хранилища ключей Azure

Хранилище ключей предоставляет toosecurely доступа к конфиденциальной информации в приложениях:

- Защищенные ключи и секретные коды без необходимости кода hello toowrite самостоятельно и являются легкостью toouse их из приложений.
- Вы могли toohave собственных клиентов и управление свои собственные ключи, что позволяет сосредоточиться на предоставление hello основных программных компонентов. Таким образом приложения не будет владеть hello никакой ответственности потенциальных для ваших клиентов клиента ключи и секретные коды.
- Приложение может использовать ключи для подписывания и шифрования еще сохраняет управления ключами hello отдельно от приложения, включая toobe вашего решения может использоваться как географически распределенного приложения.
- Начиная с выпуска сентября 2016 hello хранилища ключей, приложения теперь могут использовать хранилище ключей [сертификаты](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). См. дополнительные сведения о [ключах, секретах и сертификатах](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Дополнительные сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md).

## <a name="public-previews"></a>Общедоступные предварительные версии

Периодически мы выпускаем общедоступные предварительные версии нового компонента Key Vault. Мы предлагаем вам испытать их и отправить отзыв на наш адрес электронной почты для обратной связи: azurekeyvault@microsoft.com.

### <a name="storage-account-keys---july-10-2017"></a>Ключи учетной записи хранения — 10 июля 2017 г.

>[!NOTE]
>Для этого обновления хранилища ключей Azure только hello **ключи учетной записи хранения** компонент находится в предварительной версии.

Эта предварительная версия включает новую функцию "Ключи учетной записи хранения", доступную через интерфейсы [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) или [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Дополнительные сведения о новой функции ключи учетной записи хранения hello см. в разделе [Общие сведения об учетной записи хранилища ключей хранилища ключей Azure](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Видеоролики

В этом видео показано, как toocreate свой собственный ключ в хранилище и как toouse с «Hello хранилище ключей» пример приложения hello.

- [Key Vault developer - quick start guide](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player) (Краткое руководство по началу работы для разработчиков Key Vault)

Ресурсы, используемые в этом видео:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Пример кода для хранилища ключей Azure](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Создание хранилищ ключей и управление ими

Перед началом работы с хранилищем ключей Azure в коде, можно создать и управлять хранилищами через REST, шаблоны диспетчера ресурсов, PowerShell или интерфейс командной строки, как описано в hello в следующих статьях:

- [Создание хранилищ ключей и управление ими с помощью REST](https://docs.microsoft.com/rest/api/keyvault/)
- [Создание хранилищей ключей и управление ими с помощью PowerShell](key-vault-get-started.md)
- [Создание хранилищей ключей и управление ими с помощью CLI](key-vault-manage-with-cli2.md)
- [Create a key vault and add a secret via an Azure Resource Manager template](../azure-resource-manager/resource-manager-template-keyvault.md) (Создание хранилища ключей и добавление секрета с помощью шаблона Azure Resource Manager)

> [!NOTE]
> Операции с хранилищами ключей проходят проверку подлинности в AAD и авторизуются с помощью собственной политики доступа хранилища ключей, определенной для каждого хранилища.

## <a name="coding-with-key-vault"></a>Программирование с помощью хранилища ключей

Hello хранилища ключей системы управления для программистов состоит из нескольких интерфейсов с ОСТАЛЬНОЙ как hello foundation. Через интерфейс REST hello все ресурсы хранилищ ключей доступны; ключи, секреты и сертификаты. [Справочник по REST API для Key Vault](https://docs.microsoft.com/rest/api/keyvault/) 

### <a name="supported-programming-languages"></a>Поддерживаемые языки программирования

#### <a name="net"></a>.NET

- [Справочник по API .NET для Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Дополнительные сведения о версии 2.x hello hello .NET SDK см. в разделе hello [заметки о выпуске](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Пакет Java SDK для Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

В Node.js отделены API управления хранилищем hello и хранилище hello объекта API. Управление Key Vault позволяет создавать и обновлять хранилище ключей. API операций Key Vault предназначен для работы с такими объектами хранилища, как ключи, секреты и сертификаты. 

- [Справочник по API Node.js для управления Key Vault](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Справочник по API Node.js для операций Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Быстрый запуск

- [Создание хранилища ключей](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Приступая к работе с Key Vault в Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Примеры кода

Полные примеры использования хранилища ключей с приложениями см. в следующих документах:

- [Примеры кода Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) — пример приложения .NET *HelloKeyVault* и пример веб-службы Azure. 
- [Использовать хранилище ключей Azure из веб-приложения](key-vault-use-from-web-application.md) -toohelp учебник, вы узнаете, как toouse Azure ключ хранилища из веб-приложения в Azure. 

## <a name="how-tos"></a>Инструкции

Hello следующих статей и сценарии приведены рекомендации определенных задач по работе с хранилищем ключей Azure:

- [Переместить ИД клиента хранилища ключей изменений после подписки](key-vault-subscription-move-fix.md) - при перемещении вашей подписке Azure из клиента tootenant B, они недоступны для hello субъекты (пользователи и приложения) в клиенте б. Исправьте это с помощью этого руководства в существующие хранилища ключей.
- [Доступ к хранилищу ключей за брандмауэром](key-vault-access-behind-firewall.md) -tooaccess ключ в хранилище вашего хранилища ключей клиента приложения требованиям toobe может tooaccess несколько конечных точек для различных функций.
- [Как tooGenerate и Transfer HSM-Protected ключей для хранилища ключей Azure](key-vault-hsm-protected-keys.md) -это поможет вам спланировать, создать и затем перенести собственные ключей, защищенных HSM toouse с хранилищем ключей Azure.
- [Как toopass защитить значения (например, пароли) во время развертывания](../azure-resource-manager/resource-manager-keyvault-parameter.md) — при необходимости toopass безопасное значение (например, пароля) как параметр во время развертывания, это значение можно сохранить в качестве секрета хранилища ключей Azure и ссылка значение hello в других Шаблоны диспетчера ресурсов.
- [Как toouse хранилище ключей расширенного управления ключами, с помощью SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) -hello соединителя SQL Server для хранилища ключей Azure позволяет SQL Server и SQL в ВМ tooleverage hello ключ службы хранилища Azure в качестве поставщика расширенного управления Ключами tooprotect шифрование ключей для связи приложения; Прозрачное шифрование данных, шифрование резервной копии и шифрование на уровне столбца.
- [Как toodeploy tooVMs сертификаты из хранилища ключей](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - облачного приложения ОС на виртуальной машине Azure требованиям сертификата. Как получить этот сертификат для виртуальной машины?
- [Как tooset копии хранилища ключей с конечным tooend ключа аудит и поворота](key-vault-key-rotation-log-monitoring.md) -в этом руководстве как tooset копирование аудит с хранилищем ключей Azure и смены ключей.
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) (Развертывание сертификата службы веб-приложения Azure с помощью Key Vault) — пошаговое руководство по развертыванию сертификатов, хранящихся в Key Vault, в рамках предложения [Сертификаты службы приложений](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Предоставьте разрешение toomany приложений tooaccess хранилища ключей](key-vault-group-permissions-for-apps.md) политики управления доступом в хранилище ключей поддерживает только 16 элементов. Однако вы можете создать группу безопасности Azure Active Directory. Добавьте все hello связанная группа безопасности toothis участников службы, а затем предоставьте доступ toothis безопасности группы tooKey хранилища.
- Руководство по интеграции и использованию хранилищ ключей в Azure см. в этой статье [с примерами шаблонов Azure Resource Manager для хранилища ключей от Райана Джонса (Ryan Jones)](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Как toouse хранилище ключей soft-delete с CLI](key-vault-soft-delete-cli.md) поможет использование hello и жизненным циклом хранилища ключей и различных объектов в хранилище ключей с soft-delete включено.
- [Как toouse хранилище ключей soft удаление с помощью PowerShell](key-vault-soft-delete-powershell.md) поможет использование hello и жизненным циклом хранилища ключей и различных объектов в хранилище ключей с soft-delete включено.

## <a name="integrated-with-key-vault"></a>Интеграция с хранилищем ключей

Эти статьи посвящены другим сценариям и службам, использующим Key Vault или интегрирующимся с ним.

- [Azure шифрование диска](../security/azure-security-disk-encryption.md) использует hello отраслевого стандарта [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) компонента Windows, а также hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) функции шифрования тома tooprovide Linux для hello операционной системы и данных hello диски. решение Hello интегрировано в хранилище ключей Azure toohelp управления и управление ключами шифрования диска hello и секретные данные в вашей подписке хранилища ключей, гарантируя, что в службе хранилища Azure в зашифрованном виде все данные в hello дисков виртуальной машины.
- [Хранилище Озера данных Azure](../data-lake-store/data-lake-store-get-started-portal.md) предоставляет параметр для шифрования данных, которые хранятся в учетной записи hello. Для управления ключами хранилища Озера данных предоставляет два режима для управления ключей шифрования master (MEKs), которые необходимы для расшифровки любые данные, которые хранятся в хранилище Озера данных hello. Можно либо воспользоваться хранилища Озера данных управлять hello MEKs, или выберите tooretain владения MEKs hello, с помощью учетной записи хранилища ключей Azure. Укажите режим hello управления ключами при создании учетной записи хранилища Озера данных. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) позволяет toomanager ключа клиента. Например вместо управлении ключом клиента (по умолчанию hello) корпорации Майкрософт, могут управлять toocomply собственного ключа клиента, с определенным нормам tooyour организации. Управление собственным ключом клиента также является ссылка tooas перевести собственного ключа, или BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Основные сведения о Key Vault

- [Поведение soft удаления хранилища ключей](key-vault-ovw-soft-delete.md) описывает функцию, которая позволяет восстанавливать удаленные объекты ли удаление hello было случайное или намеренное.
- [Хранилище ключей клиента регулирования](key-vault-ovw-throttling.md) рассказывается toohello основные понятия регулирования количества запросов и подход для своего приложения.
- [Общие сведения об учетной записи хранилища ключей хранилища ключей](key-vault-ovw-storage-keys.md) Описание интеграции учетных записей хранилища Azure hello хранилище ключей разделов.
- [Механизмы обеспечения безопасности хранилища ключей](key-vault-ovw-security-worlds.md) описывает hello связи между регионами и областей безопасности.

## <a name="social"></a>Социальные сети

- [Блог хранилища ключей](http://aka.ms/kvblog)
- [Форум хранилища ключей](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Поддержка библиотек

- [Библиотека ядра Key Vault Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) предоставляет интерфейсы **IKey** и **IKeyResolver** для поиска ключей по идентификаторам и выполнения операций с ключами.
- [Расширения хранилища ключей Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) предоставляют расширенные возможности для хранилища ключей Azure.


