---
title: "aaaDownload hello Azure SDK для PHP"
description: "Узнайте, как toodownload и установите hello Azure SDK для PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>Скачать hello Azure SDK для PHP
## <a name="overview"></a>Обзор
компоненты, позволяющие toodevelop включает Hello Azure SDK для PHP, развертывания и управления приложений PHP для Azure. В частности hello Azure SDK для PHP содержит hello следующее:

* **Здравствуйте, клиентские библиотеки PHP для Azure**. Эти библиотеки классов предоставляют интерфейс для доступа к функциям Azure, таким как службы управления данными и облачные службы.  
* **Интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI) Hello**. Это набор команд для развертывания и управления службами Azure, например веб-сайтами Azure и виртуальными машинами Azure. Hello Azure CLI работы на любой платформе, включая Mac, Linux и Windows.
* **Azure PowerShell (только для Windows)**. Это набор командлетов PowerShell для развертывания служб Azure, таких как облачные службы и виртуальные машины, и управления ими.
* **Привет эмуляторы Azure (только Windows)**. Привет эмуляторы вычислений и хранения являются локальными эмуляторами облачных служб и служб управления данными, позволяющие tootest приложения локально. Привет эмуляторы Azure работают только в Windows.

Hello разделах описываются hello как toodownload и установите компоненты, описанные выше.

Hello инструкции в этом разделе предполагается, что вы [PHP] [ install-php] установлен.

> [!NOTE]
> Необходимо иметь PHP 5.5 или более поздней версии клиентских библиотек toouse hello PHP для Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Клиентские библиотеки PHP для Azure
Hello PHP клиентские библиотеки для Azure предоставляют интерфейс для доступа к Azure возможностей, таких как службы управления данными и облачным службам из любой операционной системы. Эти библиотеки могут устанавливаться через hello редактор.

Сведения о как toouse hello клиентские библиотеки PHP для Azure см. в разделе [как tooUse hello службы BLOB-объектов][blob-service], [как tooUse hello службы таблиц] [ table-service] и [как tooUse hello службы очередей][queue-service].

### <a name="install-via-composer"></a>Установка через компоновщик
1. [Установите Git][install-git].

    > [AZURE.NOTE] В Windows необходимо также tooadd hello Git исполняемый tooyour в переменную среды PATH.

1. Создайте файл с именем **composer.json** в hello корень проекта и добавьте следующий код tooit hello:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Скачайте **[composer.phar][composer-phar]** в корневой каталог проекта.
3. Откройте командную строку и выполните эту команду в корневом каталоге проекта.
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell и эмуляторы Azure
Azure PowerShell — это набор командлетов PowerShell для развертывания служб Azure и управления ими, например облачных служб и виртуальных машин. Привет эмуляторы Azure — это эмуляторы облачных служб и служб управления данными, позволяющие tootest приложения локально. Эти компоненты поддерживаются только в Windows.

Здравствуйте, рекомендуемым способом tooinstall Azure PowerShell и Привет эмуляторы Azure — toouse hello [Microsoft Web Platform Installer][download-wpi]. Обратите внимание, что можно также выбрать tooinstall другими компонентами разработки, такие как PHP, SQL Server, hello драйверы Майкрософт для SQL Server для PHP и WebMatrix.

Сведения о разделе toouse Azure PowerShell, [как tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Инфраструктура CLI Azure
Hello Azure CLI — это набор команд для развертывания и управления службами Azure, такие как веб-сайтов Azure и виртуальных машинах Azure. Сведения об установке Azure CLI см. в разделе [Install hello Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
