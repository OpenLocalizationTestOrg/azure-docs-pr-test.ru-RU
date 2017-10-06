---
title: "aaaSecurity функций, которые могут использоваться со службой хранилища Azure | Документы Microsoft"
description: " В этой статье Обзор функций hello основных компонентов Azure безопасности, которые можно использовать со службой хранилища Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Общие сведения о безопасности при использовании службы хранилища Azure
Хранилище Azure — hello решение облачного хранилища для современных приложений, которые зависят от надежности, доступности и toomeet hello масштабируемостью с клиентами. Служба хранилища Azure предусматривает много разных средств обеспечения безопасности.

* Hello учетной записи хранения могут быть защищены с помощью управления доступом на основе ролей и Azure Active Directory.
* Защитить данные, передаваемые между приложением и Azure, можно с помощью шифрования на стороне клиента, HTTPS или SMB 3.0.
* Данные могут быть определены toobe автоматически шифруются при записи tooAzure хранилища с помощью шифрование службы хранилища.
* Диски операционной системы и данных, используемым виртуальными машинами можно задать toobe, зашифрованных с помощью шифрования диска Azure.
* Объекты данных toohello делегированный доступ в хранилище Azure можно предоставить с помощью подписей общего доступа.
* Hello метод проверки подлинности, используемый другим при доступе к хранилища можно отслеживать с помощью аналитики хранилища.

Более подробное рассмотрение безопасности в службе хранилища Azure в разделе hello [руководство по безопасности хранилища Azure](../storage/common/storage-security-guide.md). Это руководство содержит глубокое погружение в средства безопасности hello хранилища Azure как ключи учетной записи хранения, шифрование данных во время передачи, а также в rest и аналитики хранилища.

В этой статье содержатся общие сведения о функциях безопасности Azure, которые можно использовать в службе хранилища Azure. Предоставляются tooarticles, предоставляют подробные сведения о каждой функции, дополнительные ссылки.

Ниже приведены hello основные функции toobe, описанный в этой статье.

* Управление доступом на основе ролей
* Делегированный доступ toostorage объектов
* Шифрование при передаче
* Шифрование при хранении (шифрование службы хранилища)
* Дисковое шифрование Azure
* Хранилище ключей Azure

## <a name="role-based-access-control-rbac"></a>Управление доступа на основе ролей
Вы можете защитить учетную запись хранения с помощью управления доступом на основе ролей (RBAC). Ограничение доступа на основании hello [требуется tooknow](https://en.wikipedia.org/wiki/Need_to_know) и [наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege) принципы безопасности важно для организаций, которые планируют tooenforce политики безопасности для доступа к данным. Эти права доступа предоставляются путем назначения hello соответствующие RBAC роли toogroups и приложения в определенной области. Можно использовать [встроенные роли RBAC](../active-directory/role-based-access-built-in-roles.md), например участника учетной записи хранилища, tooassign привилегии toousers.

Подробнее.

* [Контроль доступа на основе ролей Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Делегированный доступ toostorage объектов
Подписанный URL-адрес (SAS) предоставляет tooresources делегированный доступ в вашей учетной записи хранилища. Hello SAS означает предоставить клиент ограниченную tooobjects разрешения вашей учетной записи хранилища в течение заданного времени, используя указанный набор разрешений. Можно предоставить эти ограниченные разрешения без необходимости tooshare ключей доступа к учетной записи. Hello SAS является URI, который охватывает все hello сведения, необходимые для доступа с проверкой подлинности ресурса хранилища tooa параметрами запроса. tooaccess ресурсов хранения в hello SAS, hello клиент должен только tooprovide hello SAS toohello соответствующего конструктора или метода.

Подробнее.

* [Основные сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Шифрование при передаче
Шифрование при передаче — это механизм защиты данных, передаваемых по сетям. Служба хранилища Azure позволяет применять для защиты данных:

* [шифрование транспортного уровня](../storage/common/storage-security-guide.md#encryption-in-transit), например протокол HTTPS, при передаче данных в службу хранилища Azure или из нее;
* [шифрование подключения](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), например шифрование SMB 3.0 для файловых ресурсов Azure;
* [Шифрование на стороне клиента](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello данных перед передачей в хранилище и toodecrypt hello данные после передачи за пределами хранилища.

Дополнительные сведения о шифровании на стороне клиента.

* [Client-Side Encryption for Microsoft Azure Storage (Шифрование на стороне клиента для службы хранилища Microsoft Azure)](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud security controls series: Encrypting Data in Transit (Серия статей об управлении безопасностью в облаке: защита данных при передаче)](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Шифрование при хранении
Для многих организаций [шифрование неактивных данных](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) является обязательным шагом для защиты данных, соблюдения стандартов и обеспечения конфиденциальности данных. В Azure есть три функции, обеспечивающие шифрование неактивных данных.

* [Шифрование службы хранилища](../storage/common/storage-security-guide.md#encryption-at-rest) позволяет toorequest, что службы хранилища hello автоматически шифровать данные при записи tooAzure хранилища.
* [Шифрование на стороне клиента](../storage/common/storage-security-guide.md#client-side-encryption) также обеспечивает возможность hello шифрования при хранении.
* [Azure шифрование диска](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) позволяет tooencrypt hello ОС дисков и дисков данных, используемый виртуальной машиной IaaS.

Дополнительные сведения о шифровании службы хранилища.

* [Шифрование службы хранилища Azure](https://azure.microsoft.com/services/storage/) доступно для [хранилища BLOB-объектов Azure](https://azure.microsoft.com/services/storage/blobs/). Сведения о других типах хранилища Azure см. в описании хранилищ [файлов](https://azure.microsoft.com/services/storage/files/), [дисков (хранилище класса Premium)](https://azure.microsoft.com/services/storage/premium-storage/), [таблиц](https://azure.microsoft.com/services/storage/tables/) и [очередей](https://azure.microsoft.com/services/storage/queues/).
* [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Дисковое шифрование Azure
Шифрование дисков Azure для виртуальных машин помогает соблюдать требования (включая корпоративные требования к безопасности). Эта служба выполняет шифрование дисков виртуальных машин (загрузочных дисков и дисков данных) с использованием ключей и политик, которыми вы управляете в [хранилище ключей Azure](https://azure.microsoft.com/services/key-vault/).

Шифрование дисков для виртуальных машин используется для операционных систем Linux и Windows. Она также использует хранилище ключей toohelp защиты, управление и аудит использования ключей шифрования диска. Все данные hello в дисков виртуальной Машины находится в зашифрованном виде с помощью технологии шифрования стандартных учетных записей хранилища Azure. Шифрование диска решения для Windows Hello основан на [программы шифрования диска BitLocker](https://technet.microsoft.com/library/cc732774.aspx), hello Linux решения на основе [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Подробнее.

* [Шифрование дисков Azure для виртуальных машин IaaS с ОС Windows и Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Хранилище ключей Azure
Использует Azure шифрование диска [хранилище ключей Azure](https://azure.microsoft.com/services/key-vault/) toohelp вы для управления ключами шифрования диска и секретные данные в вашей подписке хранилища ключей, обеспечивая шифровать все данные в hello диски виртуальной машины при хранении в Azure Хранилище. Следует использовать хранилище ключей tooaudit ключей и использование политик.

Подробнее.

* [Что такое хранилище ключей Azure?](../key-vault/key-vault-whatis.md)
* [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md)
