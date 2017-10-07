---
title: "aaaAzure Linux виртуальной машины DotNet Core учебник 1 | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e6f047197336de1e93c50413b6eabb718230bc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toolinux-virtual-machines"></a>Автоматизация развертывания приложения tooLinux виртуальные машины 

Эта серия из четырех статей подробно описывает развертывание и настройку ресурсов и приложений Azure с помощью шаблонов Azure Resource Manager. В этой серии образец шаблона развертывается и Здравствуйте проверяются шаблон развертывания. Цель этой серии Hello — tooeducate hello связи между ресурсами Azure и tooprovide практические навыки работы развертывание полностью интегрированной шаблонов диспетчера ресурсов Azure. Предполагается, что у читателя есть базовый уровень знаний об Azure Resource Manager. Прежде чем работать с этим руководством, предлагаем вам ознакомиться с основными понятиями Azure Resource Manager. 

## <a name="music-store-application"></a>Приложение музыкального магазина
Hello образец, использованный в этой серии представляет .net имитация Music Store, покупок качества основное приложение. Это приложение может быть развернутой tooeither Windows или Linux виртуальной системы, пример, который были созданы для обоих развертываний. приложение Hello включает веб-приложения и базы данных SQL. Перед прочтением hello статьи в этой серии, развертывание приложения hello, с помощью кнопки развертывания hello найдено на этой странице. Если полностью развернут hello архитектуры приложения / Azure выглядит как hello следующие схемы. 

шаблон диспетчера ресурсов хранилища музыка Hello можно найти здесь, [шаблона Linux музыка хранилища](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![Приложение музыкального магазина](./media/dotnet-core-1-landing/music-store.png)

Каждый из этих компонентов, включая hello связать шаблон JSON, рассматриваются в следующих четырех статей hello.

* [**Архитектура приложения** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — компоненты приложения, такие как веб-сайты и базы данных должны toobe, размещенной на компьютере Azure ресурсы, такие как виртуальные машины и базы данных Azure SQL. В этом документе рассматриваются необходимость сопоставления вычислений, tooAzure ресурсов и развертывания ресурсов с помощью шаблона диспетчера ресурсов Azure. 
* [**Доступ и безопасность** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — при размещении приложения в Azure, это tooconsider необходимые процедуры осуществляется приложения hello, и разные компоненты приложения обращаются друг к другу. В этом документе описаны предоставление и обеспечения безопасности веб-приложение tooan доступ и доступ между компонентами приложения.
* [**Высокой доступности и масштабируемости** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — высокой доступности и масштабируемости ссылаться toohello приложений возможность toostay во время простой инфраструктуры и tooscale возможность hello вычислений ресурсов toomeet приложения запросу. Этот документ сведения hello компонентов требуется toodeploy с балансировкой нагрузки и высокой доступности приложения.
* [**Развертывание приложения** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — при развертывании приложений на виртуальных машинах Azure, метод hello, по которой hello двоичные файлы приложения устанавливаются на hello виртуальной машины необходимо учитывать. В этом документе описаны возможности по автоматизации установки приложений, которые предоставляют расширения пользовательских сценариев для виртуальных машин Azure.

Задача Hello при разработке шаблоны Azure Resource Manager — tooautomate hello развертывание инфраструктуры Azure и установки hello и настройку любого приложения, размещенные на этом инфраструктуры Azure. Ознакомившись с этими статьями, вы научитесь решать эти задачи.

## <a name="deploy-hello-music-store-application"></a>Развернуть приложение из магазина музыка hello
Hello Music Store приложения могут развертываться с помощью этой кнопки.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

шаблон диспетчера ресурсов Azure Hello требует hello следующие значения параметров.

| Имя параметра | Описание |
| --- | --- |
| SSHKEYDATA |Данные ключа SSH используется toohello toosecure доступа виртуальной машины. Дополнительные сведения о создании пар ключей SSH см. в статье [Создание ключей SSH для виртуальных машин Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). |
| ADMINUSERNAME |Имя пользователя администратора, который используется на виртуальной машине hello и hello базы данных SQL Azure. |
| SQLADMINPASSWORD |Пароль, используемый на hello базы данных SQL Azure. |
| NUMBEROFINSTANCES |число Hello создан toobe виртуальных машин. Каждая из этих виртуальных машин узла hello Music Store веб-приложения, а также весь трафик будет осуществляться Балансировка между ними. |
| PUBLICIPADDRESSDNSNAME |Глобальное уникальное имя DNS, связанный с hello общедоступный IP-адрес. |

После завершения развертывания шаблона hello, Обзор toohello открытый IP-адресов с помощью Интернет-браузер. Hello .net откроется сайта основные музыки.

## <a name="next-steps"></a>Дальнейшие действия
<hr>

[Шаг 1. Архитектура приложений с использованием шаблонов Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Шаг 2. Доступ и безопасность в шаблонах Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Шаг 3. Доступность и масштабирование в шаблонах Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Шаг 4. Развертывание приложений с использованием шаблонов Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

