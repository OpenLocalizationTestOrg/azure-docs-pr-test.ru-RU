---
title: "aaaAzure защитить личные данные хранятся с шифрованием | Документы Microsoft"
description: "В этой статье входит в серию, помогая использование Azure tooprotect личных данных"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Технологии шифрования Azure. Защита неактивных персональных данных с помощью шифрования

Эта статья поможет вам освоить и использовать данные toosecure технологии Azure шифрование при хранении.

Шифрование статических данных очень важно как лучший подход tooprotect конфиденциальных или личных данных, а также соответствие toomeet и требования к конфиденциальности данных.
Шифрование неактивных — спроектированный tooprevent hello злоумышленником доступа к данным, hello без шифрования, гарантируя hello, данные шифруются при на диске.

## <a name="scenario"></a>Сценарий 

Большой прогулка по организации, штаб-квартира компании в США, hello развернут расписаниям toooffer его операций в hello морская, балтийские компании seas, а также hello Британские острова. toosupport эти усилия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания

Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello. Это может включать сотрудников и/или сведения о заказчике такие как:

- адреса;
- номера телефонов;
- идентификационные номера налогоплательщиков;
- медицинские сведения
- данные кредитной карты.

Hello компании должны защищать конфиденциальность hello данных сотрудников и клиентов во время внесения данных доступны toothose отделов, которым она необходима. (например, отделах заработной платы и бронирования).

Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы, содержат персональные данные tootrack связи с клиентами, текущие и прошлые.

### <a name="problem-statement"></a>Проблема

Hello компании должны защищать hello конфиденциальность личных данных сотрудников и клиентов во время внесения данных доступны toothose отделов, в которых он нужен (например, отделы заработной платы и резервирования). Эти личные данные хранятся вне центра обработки данных, управляемых корпоративной hello, а не в физический контроль hello компании.

### <a name="company-goal"></a>Цель компании

Как часть стратегии безопасности многоуровневый глубокой обороны это tooensure цель компании, что все источники данных, которые содержат персональные данные зашифрованы, включая находящиеся в Облачное хранилище. Если несанкционированный лиц прибыль доступа toohello личных данных, ее необходимо в форме, которая сделает его может быть прочитан. Шифрование должно быть простым или прозрачным для пользователей и администраторов.

## <a name="solutions"></a>Решения

Службы Azure предоставляют несколько средств и технологий toohelp защиты личных данных неактивные путем его шифрования.

### <a name="azure-key-vault"></a>Хранилище ключей Azure

[Хранилище ключей Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) обеспечивает безопасное хранение для hello ключей используется tooencrypt данные хранятся на служб Azure и hello рекомендуется ключа хранилища и управления ими. Управление ключами шифрования — это основные toosecuring хранимые данные.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Как использовать хранилище ключей Azure tooprotect ключи шифрования персональные данные?

toouse хранилище ключей Azure, вы должны подписки tooan учетная запись Azure. Кроме того, необходимо установить Azure PowerShell. Шаги включают использование следующих hello toodo командлеты PowerShell.

1. Подключение tooyour подписки

2. Создайте хранилище ключей.

3. Добавление ключа или секрета toohello хранилища ключей

4. Регистрация приложения, которые будет использовать хранилище ключей hello в Azure Active Directory

5. Авторизовать hello приложений toouse hello ключа или секрета

toocreate хранилища ключей, используйте командлет PowerShell New-AzureRmKeyVault hello. Вы присвоите имя хранилища, имя группы ресурсов и географическое местоположение. Имя хранилища hello будет использоваться при управлении ключами через другие командлеты. Приложения, использующие хранилище hello через API-Интерфейс REST hello будет использовать хранилище hello URI.

Azure Key Vault предоставляет ключ с программной защитой. Вы также можете импортировать ключ, имеющийся в PFX-файле. Можно также хранить секреты (пароли) в хранилище hello.

Можно также создать ключ в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello.

Подробные инструкции по использованию хранилища ключей Azure, выполните шаги hello [Приступая к работе с хранилищем ключей Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Сведения о списке командлетов PowerShell, используемых с Azure Key Vault, см. в статье [Azure​RM.​Key​Vault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Шифрование дисков Azure для Windows

[Шифрование дисков Azure для виртуальных машин IaaS под управлением Windows и Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) позволяет защитить неактивные персональные данные на виртуальных машинах Azure. Эта возможность интегрируется с Azure Key Vault. Использует Azure шифрование диска [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) в Windows и [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) в Linux tooencrypt оба hello ОС и hello диски с данными. Шифрование дисков Azure поддерживается в Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, а также клиентах Windows 8 и Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Как использовать шифрование диска Azure tooprotect персональные данные?

toouse шифрование диска Azure требуется подписка tooan учетная запись Azure. tooenable Azure диск шифрования для Windows и виртуальных машин Linux hello следующие:

1. Укажите hello шаблона диспетчера ресурсов шифрования диска Azure, PowerShell или шифрование диска tooenable hello командной строки (CLI) и конфигурации шифрования. 

2. Предоставление доступа toohello основы платформы Azure tooread hello шифрования из хранилища ключей.

3. Укажите Azure Active Directory (AAD) приложение удостоверения toowrite hello шифрования ключа материала tooyour хранилища ключей.

Azure будет обновить hello виртуальных Машин и хранилища ключей конфигурации hello и настройка зашифрованных ВМ.

При настройке toosupport вашего хранилища ключей шифрования диска Azure можно добавить ключ ключа шифрования (ключ обмена Ключами) для повышения безопасности и резервного копирования toosupport зашифрованные виртуальных машин.

![](media/protect-personal-data-at-rest/create-key.png)

Подробные инструкции для определенных сценариев развертывания и взаимодействия с пользователем см. в статье [Дисковое шифрование Azure для виртуальных машин IaaS под управлением Windows и Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption).

### <a name="azure-storage-service-encryption"></a>Шифрование службы хранилища Azure

[Azure хранилища службы шифрования (SSE) для статических данных](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) помогает защитить и защиты вашего toomeet данных организации свои обязательства по безопасности и соответствия требованиям. Хранилище Azure автоматически шифрует данные с помощью toostorage предыдущих toopersisting шифрования AES 256-разрядный и расшифровывает его предыдущего tooretrieval. Эта служба доступна для файлов и больших двоичных объектов Azure.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Как использовать шифрование службы хранилища tooprotect персональные данные?

Шифрование службы хранилища, tooenable hello следующие:

1. Войдите на hello портал Azure.

2. Выберите учетную запись хранения.

3. В параметрах в разделе "hello" BLOB-объектов, выберите шифрования.

4. Установите шифрования hello раздела службы файлов.

После щелчка шифрования приветствия, можно включить или отключить шифрование службы хранилища.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Новые данные будут зашифрованы. Данные в имеющихся файлах этой учетной записи хранения останутся незашифрованными.

После включения шифрования, скопируйте данные учетной записи хранилища toohello с помощью одного из следующих методов hello:

1. Копирование больших двоичных объектов или файлов с hello [служебной программы командной строки AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Подключить общей папки SMB с помощью](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , можно использовать программу, например файлы toocopy Robocopy.

3. Скопируйте большой двоичный объект или файл данных tooand из хранилища BLOB-объектов или между хранилища учетных записей с помощью [клиентских библиотек хранилища, такие как .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Используйте [обозреватель хранилищ](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload BLOB-объектов учетной записи хранилища tooyour с включенным шифрованием.

### <a name="transparent-data-encryption"></a>Прозрачное шифрование данных

Прозрачное шифрование данных (TDE) является компонентом в SQL Azure, с помощью которого можно шифровать данные на обоих уровнях hello базы данных и сервера. Эта функция теперь включена по умолчанию во всех новых базах данных. Прозрачное шифрование данных выполняет в реальном времени ввода-вывода шифрование и дешифрование файлов данных и журналов hello.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Использование прозрачного шифрования данных tooprotect персональные данные

Прозрачное шифрование данных можно настроить через hello портал Azure с помощью API-интерфейса REST hello, или с помощью PowerShell. tooenable прозрачное шифрование данных на существующей базы данных с помощью портала Azure hello hello следующие:

1. Посетите hello Azure портала в <https://portal.azure.com> и войдите с учетной записью администратора или участника Azure.

2. В hello слева щелкните tooBROWSE и выберите базы данных SQL.

3. С базами данных SQL, выбранной в левой области hello выберите пользовательскую базу данных.

4. В колонке базы данных hello выберите все параметры.

5. В колонке параметров hello щелкните прозрачное шифрование часть tooopen hello прозрачное шифрование колонку.

6. В колонке шифрования данных hello переместить tooOn кнопка шифрования данных hello и нажмите кнопку Сохранить (в начале hello страницы приветствия) tooapply приветствия. состояние шифрования Hello будет отображаться приблизительный ход выполнения hello hello прозрачное шифрование данных.

![Включение шифрования данных](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Инструкции по обнаружение tooenable прозрачного шифрования данных и сведения о расшифровке базы данных с защитой TDE и многое другое в статье hello [прозрачное шифрование данных с базой данных SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Сводка

Hello компании можно выполнить его задача шифрования персональные данные, хранящиеся в облаке Azure hello. Это можно сделать с помощью шифрования диска Azure слишком защитить всего тома. Это может включать hello системные файлы и файлы данных, которые содержат персональные данные и другие конфиденциальные данные. Azure шифрование службы хранилища может быть используется tooprotect персональные данные, хранящиеся в файлах и больших двоичных объектов. К персональным данным, хранящимся в базе данных SQL Azure, можно применить прозрачное шифрование, которое обеспечивает защиту от несанкционированного доступа.

ключи hello tooprotect, используемые tooencrypt данные в Azure, hello компании можно использовать хранилище ключей Azure. Это упрощает процесс управления ключами hello и включает hello компании toomaintain управление ключами, которые обращаются к и шифрования личных данных.

## <a name="next-steps"></a>Дальнейшие действия

- [Руководство по устранению неполадок шифрования дисков Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Шифрование виртуальной машины Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Шифрование данных в Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Шифрование неактивных данных базы данных в Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
