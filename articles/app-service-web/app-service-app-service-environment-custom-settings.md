---
title: "Параметры aaaCustom для среды службы приложений"
description: "Настраиваемые параметры конфигурации для сред службы приложений"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Настраиваемые параметры конфигурации для сред службы приложений
## <a name="overview"></a>Обзор
Поскольку среды службы приложений теперь изолированной tooa одного клиента, есть определенные параметры конфигурации, которые могут быть применены только tooApp среды службы. В данной статье описывается hello различные отдельные настройки, доступные для среды службы приложения.

Если у вас среды службы приложений, см. раздел [как tooCreate среды службы приложений](app-service-web-how-to-create-an-app-service-environment.md).

Можно сохранить настройки среды службы приложений с помощью нового массива hello **clusterSettings** атрибута. Этот атрибут находится в словарь «Свойства» hello hello *hostingEnvironments* сущности диспетчера ресурсов Azure.

Hello следующий сокращенный диспетчера ресурсов шаблона фрагмент показывает hello **clusterSettings** атрибута:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Hello **clusterSettings** атрибута может быть включено в hello tooupdate шаблона диспетчера ресурсов среды службы приложений.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Использование обозревателя ресурсов Azure tooupdate среды службы приложений
Кроме того, можно обновить hello среды службы приложений с помощью [обозревателя ресурсов Azure](https://resources.azure.com).  

1. В обозревателе ресурсов, перейдите в узел toohello для hello среды службы приложений (**подписки** > **resourceGroups** > **поставщики**  >  **Microsoft.Web** > **hostingEnvironments**). Нажмите кнопку hello определенной среды службы приложений, которые должны tooupdate.
2. Hello правой панели щелкните **чтения и записи** в tooallow верхней панели инструментов hello интерактивного редактирования в обозревателе ресурсов.  
3. Щелкните голубой hello **изменить** кнопку toomake hello шаблона диспетчера ресурсов для редактирования.
4. Прокрутите toohello нижней правой области hello. Hello **clusterSettings** атрибут находится в самом низу hello, где можно ввести или обновить его значение.
5. Тип (или копировать и вставить) hello массив значений параметров конфигурации в hello **clusterSettings** атрибута.  
6. Щелкните зеленый hello **ПОМЕСТИТЬ** кнопку, который находится вверху hello toohello hello правой панели toocommit hello изменение среды службы приложений.

Однако при отправке изменений hello, занимает приблизительно 30 минут, умноженное на количество hello интерфейсы в hello среды службы приложений для hello изменение tootake эффекта.
Например если среды службы приложений имеет четыре интерфейсных, он займет приблизительно два часа для toofinish обновления конфигурации hello. При изменении конфигурации hello разворачивается, никакие другие операции масштабирования или операций изменения конфигурации могут иметь место в hello среды службы приложений.

## <a name="disable-tls-10"></a>Отключение TLS 1.0
Повторяющиеся вопрос от клиентов, особенно пользователи сталкиваются со соответствие стандартам PCI событий аудита, является то, каким образом tooexplicitly отключить TLS 1.0 для своих приложений.

Протокол TLS 1.0 можно отключить с помощью следующих hello **clusterSettings** входа:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Порядок изменения комплекта шифров TLS 
Другой вопрос от клиентов — Если hello список шифров согласовывается путем их сервер могут быть изменены, и это можно сделать, изменив hello **clusterSettings** как показано ниже. Список доступных комплектов шифров Hello можно получить из [в этой статье MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Если для hello комплекты шифров SChannel не понимают заданы неверные значения, все сервера tooyour TLS связи могут перестать работать. В этом случае вам потребуется tooremove hello *FrontEndSSLCipherSuiteOrder* запись из **clusterSettings** и отправьте hello обновления диспетчера ресурсов шаблона toorevert toohello назад по умолчанию шифров набор параметров.  Используйте эту возможность с осторожностью.
> 
> 

## <a name="get-started"></a>Начало работы
Hello сайта шаблона диспетчера ресурсов Azure краткое руководство предоставляет шаблон с hello базовое определение для [создание среды службы приложений](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
