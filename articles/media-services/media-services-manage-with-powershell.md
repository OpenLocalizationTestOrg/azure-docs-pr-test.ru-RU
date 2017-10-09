---
title: "aaaManage учетные записи служб мультимедиа Azure с помощью PowerShell"
description: "Узнайте, как учетные записи служб мультимедиа Azure toomanage с помощью командлетов PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Управление учетными записями служб мультимедиа Azure с помощью PowerShell
> [!div class="op_single_selector"]
> * [Портал](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocreate toobe доступ учетной записи служб мультимедиа Azure, необходимо иметь учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Бесплатная пробная версия Azure</a>.
> 
> 

## <a name="overview"></a>Обзор
В этой статье перечислены hello командлетов Azure PowerShell для служб мультимедиа Azure (AMS) в framework hello диспетчера ресурсов Azure. Существуют командлеты Hello в hello **Microsoft.Azure.Commands.Media** пространства имен.

## <a name="versions"></a>Версии
**ApiVersion**: от 01.10.2015.

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Создает службу мультимедиа.

### <a name="syntax"></a>Синтаксис
Набор параметров: StorageAccountIdParamSet.

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Набор параметров: StorageAccountsParamSet.

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Name (Имя) |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

**-Location &lt;String&gt;**

Указывает расположение ресурса hello hello службы мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |2 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-StorageAccountId &lt;String&gt;**

Указывает учетную запись основного хранилища, связанный с hello службы мультимедиа.

* Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.
* Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |3 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Имя набора параметров |StorageAccountIdParamSet |
| Принимает подстановочные знаки? |нет |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Задает учетные записи хранения, связанный с hello службы мультимедиа.

* Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.
* Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.
* Можно указать только одну основную учетную запись хранения.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |3 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Имя набора параметров |StorageAccountsParamSet |
| Принимает подстановочные знаки? |нет |

**-Tags &lt;Hashtable&gt;**

Указывает хэш-таблицу hello теги, связанные с hello службы мультимедиа.

* Пример: @{«tag1 «=» значение1»;» tag2» =: значение2»}

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция? |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Обновляет службу мультимедиа.

### <a name="syntax"></a>Синтаксис
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Name (Имя) |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |Ложь |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Задает учетные записи хранения, связанный с hello службы мультимедиа.

* Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.
* Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.
* Можно указать только одну основную учетную запись хранения.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция? |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Имя набора параметров |StorageAccountsParamSet |
| Принимает подстановочные знаки? |нет |

**-Tags &lt;Hashtable&gt;**

Указывает хэш-таблицу hello теги, связанные с этой службы мультимедиа.

* значение, указанное клиентом hello заменяются Hello теги, связанные с hello службы мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция? |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Удаляет службу мультимедиа.

### <a name="syntax"></a>Синтаксис
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |2 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |Ложь |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Получает все службы мультимедиа в группе ресурсов или службу мультимедиа с заданным именем.

### <a name="syntax"></a>Синтаксис
Набор параметров: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

Набор параметров: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Имя набора параметров |ResourceGroupParameterSet, AccountNameParameterSet |

Принимает подстановочные знаки?   нет

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Имя набора параметров |AccountNameParameterSet |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Возвращает ключи службы мультимедиа.

### <a name="syntax"></a>Синтаксис
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Повторно создает первичный или вторичный ключ службы мультимедиа.

### <a name="syntax"></a>Синтаксис
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-KeyType &lt;KeyType&gt;**

Задает тип ключа hello hello службы мультимедиа.

* Первичный или вторичный

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |2 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toothe.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Синхронизация ключей учетной записи хранения для учетной записи хранения, связанный с hello службы мультимедиа.

### <a name="syntax"></a>Синтаксис
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Параметры
**-ResourceGroupName &lt;String&gt;**

Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |0 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-AccountName &lt;String&gt;**

Указывает имя службы мультимедиа hello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция? |1 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**-StorageAccountId &lt;String&gt;**

Указывает учетную запись хранилища hello, связанные с hello службы мультимедиа.

| Псевдонимы | Идентификатор |
| --- | --- |
| Обязательный? |Да |
| Позиция? |2 |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |true(ByPropertyName) |
| Принимает подстановочные знаки? |нет |

**&lt;CommandParameters&gt;**

Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.

### <a name="inputs"></a>Входные данные
Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.

### <a name="outputs"></a>outputs
Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.

## <a name="next-step"></a>Дальнейшие действия
Изучите схемы обучения для служб мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

