---
title: "aaaAzure шифрование службы хранилища с помощью клиента управляемого ключей в хранилище ключей Azure | Документы Microsoft"
description: "Используйте tooencrypt функции hello шифрование службы хранилища Azure хранилище BLOB-объектов Azure на стороне службы hello при сохранении данных hello и расшифровать его при получение данных hello, с помощью клиента управляемый ключей."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Шифрование службы хранилища с помощью управляемых клиентом ключей в Azure Key Vault

Microsoft Azure — прилагает все усилия toohelping защиты и защиты вашего toomeet данных организации безопасности и соответствия обязательства.  Можно защитить данные хранятся в том toouse шифрование службы хранилища (SSE), автоматически шифрует данные при записи его toostorage, которое расшифровывает данные при его получении. Здравствуйте, шифрования и расшифровки происходит автоматически и полностью прозрачно и 256 бит используется [шифрование AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), один блок сильные hello шифры доступны.

Можно использовать ключи шифрования с SSE, управляемые корпорацией Майкрософт, или собственные ключи шифрования. В этой статье поговорим о hello последний. Дополнительные сведения об использовании ключей, управляемых корпорацией Майкрософт, и о SSE в целом см. в разделе [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](storage-service-encryption.md).

возможность hello tooprovide toouse свои собственные ключи шифрования, SSE для хранилища BLOB-объектов интегрирован с хранилищем ключей Azure (AKV). Можно создавать свои собственные ключи шифрования и сохранения их в хранилищем ключей AZURE, или можно использовать ключи шифрования toogenerate хранилищем ключей AZURE API-интерфейсы. Не только позволяют toomanage хранилищем ключей AZURE и управления ключи, также позволяет вам tooaudit использование вашего ключа. 

Зачем toocreate собственные разделы? Обеспечивает большую гибкость, включая возможность toocreate hello, поворот, отключить и определение элементов управления доступом и шифрования ключей, используемых tooaudit hello tooprotect данных.

## <a name="sse-with-customer-managed-keys-preview"></a>Предварительная версия SSE для управляемых клиентом ключей

Эта функция в настоящее время находится на стадии предварительной версии. toouse эту возможность, необходимо toocreate новой учетной записи хранения. Можно создать новое Key Vault и ключ или использовать существующие. Учетная запись хранения Hello и хранилища ключей hello должны находиться в hello же регионе, но они могут находиться в разных подписках.

обратитесь в службу tooparticipate в режиме предварительного просмотра hello [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Корпорация Майкрософт предоставляет tooparticipate специальной ссылкой в предварительной версии hello.

toolearn более, можно найти toohello [часто задаваемые вопросы о](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Необходимо зарегистрироваться для hello предыдущих toofollowing hello шаги в этой статье. Без доступа к предварительной версии, то не сможете быть может tooenable эту функцию в портал hello.

## <a name="getting-started"></a>Приступая к работе
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Этап 1. [Создание учетной записи хранения](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Этап 2. Включение шифрования
Можно включить для hello учетной записи хранилища с помощью hello SSE [портал Azure](https://portal.azure.com). В колонке параметров hello для учетной записи хранения hello найдите hello раздел BLOB-объектов, как показано на рисунке ниже и нажмите кнопку шифрования.

![Снимок экрана портала с параметром шифрования](./media/storage-service-encryption/image1.png)
<br/>*Включение SSE для службы BLOB-объектов*

Если требуется tooprogrammatically включить или отключить hello шифрование службы хранилища в учетной записи хранения, можно использовать hello [API REST поставщика ресурсов хранилища Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [клиентской библиотеки поставщика ресурсов хранилища для .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), или hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

На этом экране Если не отображается флажок «использовать свой собственный ключ» hello, вы не были утверждены для предварительного просмотра hello. Отправьте сообщение электронной почты слишком[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) и запросить утверждение.

![Снимок экрана портала с окном предварительной версии SSE](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

По умолчанию SSE будет использовать ключи, управляемые корпорацией Майкрософт. toouse собственные разделы, установите флажок "hello". Затем можно либо указать свой ключ URI, или выберите ключ и хранилищем ключей из палитры hello.

## <a name="step-3-select-your-key"></a>Шаг 3. Выбор ключа

![Снимок экрана портала с окном SSE, в котором выбрано использование собственного ключа](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Снимок экрана портала с окном SSE, в котором выбрано указание универсального кода ресурса (URI) ключа](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Если учетной записи хранилища hello не имеет доступа toohello хранилище ключей, можно запустить следующие hello команду с помощью Azure Powershell toogrant доступа toohello учетных записей хранения toohello требуется хранилище ключей.

![Снимок экрана портала, показывающий отказ в доступе к Key Vault](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Вы можете также предоставлять доступ через портал Azure hello toohello хранилище ключей Azure в hello портал Azure и предоставление доступа к учетной записи хранилища toohello.

## <a name="step-4-copy-data-toostorage-account"></a>Шаг 4: Копирование учетной записи toostorage данных
Если вы хотите tootransfer данных в новую учетную запись хранения, чтобы он зашифрован, можно найти слишком[шаг 3 из Приступая к работе с шифрование службы хранилища для статических данных](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Шаг 5: Состояние запроса hello hello зашифрованных данных
состояние hello tooquery hello шифрование данных можно найти слишком[шаг 4 из Приступая к работе с шифрование службы хранилища для статических данных](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Часто задаваемые вопросы о шифровании службы хранилища для неактивных данных
**Вопрос. Я использую хранилище уровня "Премиум". Могу ли я использовать функцию SSE с управляемыми клиентом ключами?**

Ответ. Да, функцию SSE можно использовать с ключами, управляемыми корпорацией Майкрософт, и управляемыми клиентом ключами в хранилищах уровня "Стандартный" и "Премиум". 

**Вопрос. Можно ли создавать учетные записи хранения с включенной функцией SSE, используя управляемые клиентом ключи, с помощью Azure PowerShell и Azure CLI?**

Ответ. Да.

**Вопрос. Насколько дороже обходится служба хранилища Azure с включенной функцией SSE, использующей управляемые клиентом ключи?**

Ответ. Вы платите за использование Azure Key Vault. Дополнительные сведения см. на [странице цен на Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). За использование SSE дополнительная плата не требуется.

**Вопрос. можно ли отзывать ключи шифрования toohello доступа?**

Ответ. Да, вы можете отменить доступ в любое время. Существует несколько способов toorevoke доступа tooyour ключей. См. слишком[хранилище ключей Azure PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) и [хранилище ключей Azure CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) для получения дополнительных сведений. Отмена доступа фактически блокируют доступ tooall BLOB-объектов в учетной записи хранения hello, что hello учетной записи ключ шифрования недоступен службой хранилища Azure.

**Вопрос. Могу ли я создать учетную запись хранения и ключ в разных регионах?**

Ответ нет, hello учетной записи хранилища и ключа хранилища и ключа toobe потребность в hello одного региона. 

**Вопрос. можно включить SSE с ключами управляется пользователем при создании учетной записи хранилища hello?**

О. Нет. При включении SSE при создании учетной записи хранилища hello, можно использовать только ключи Майкрософт для управляемого кода. При желании ключи управляется пользователем toouse потребуется свойства учетной записи хранения tooupdate hello. Можно использовать REST или один из tooprogrammatically библиотеки клиента хранения hello обновления учетной записи хранилища или обновить с помощью портала Azure hello после создания учетной записи hello свойства учетной записи хранения hello.

**Вопрос. Могу ли я отключить шифрование при использовании функции SSE с управляемыми клиентом ключами?**

Ответ. Нет, при использовании функции SSE с управляемыми клиентом ключами отключить шифрование невозможно. toodisable шифрования, необходимо будет tooswitch toousing Майкрософт для управляемого кода ключей. Это можно сделать с помощью портала Azure hello или PowerShell.

**Вопрос. Включается ли SSE по умолчанию при создании учетной записи хранения?**

Ответ SSE не включена по умолчанию. можно использовать hello Azure портала tooenable его. Можно также программно включить этот компонент с помощью API-интерфейса REST поставщика ресурсов хранилища hello. 

**Вопрос. Не удается включить шифрование для учетной записи хранения.**

Ответ. Это учетная запись Resource Manager? Классические учетные записи хранения не поддерживаются. Кроме того, функцию SE с управляемыми клиентом ключами можно включить только для созданных новых учетных записей хранения Resource Manager.

**Вопрос. Функция SSE с управляемыми клиентом ключами доступна только в определенных регионах?**

Ответ. Функция SSE доступна только в определенных регионах для хранилища BLOB-объектов в рамках этой предварительной версии. Отправьте письмо на адрес [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck для обеспечения доступности и сведения о предварительной версии. 

**Вопрос. как связаться кого-либо если я все проблемы, так и tooprovide отзыв?**

Ответ обратитесь в службу [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) для проблем, связанных tooStorage шифрования службы. 

## <a name="next-steps"></a>Дальнейшие действия

*   Дополнительные сведения о hello полный набор безопасности возможности, позволяющие разработчикам создавать безопасные приложения, см. hello [руководство по безопасности хранилища](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Общие сведения о Azure Key Vault см. в статье [Что такое хранилище ключей Azure?](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)
*   О том, как приступить к работе с Azure Key Vault, рассказывается в разделе [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).
