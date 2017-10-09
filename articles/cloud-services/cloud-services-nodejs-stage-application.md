---
title: "aaaStage развертывания облачной службы (Node.js) | Документы Microsoft"
description: "Узнайте, как toodeploy tooa вашего приложения Azure, в промежуточной среде, затем развернуть tooa рабочей среде, с помощью переключения виртуального IP-адресов (VIP)."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Развертывание приложения в промежуточной среде Azure
Упакованные приложения могут быть развернутой toohello промежуточной среды в Azure toobe тестирования перед перемещением его toohello рабочей среды, в которых hello приложение доступно hello Internet. Промежуточной среды — так же, как hello рабочей среде, за исключением того, вы можете только доступ hello промежуточное приложение скрытый URL-адрес, который формируется Azure. После проверки работы приложения может быть развернутой toohello рабочую среду, выполнив переключение виртуального IP-адресов (VIP).

> [!NOTE]
> Hello действия в этой статье, относятся только toonode приложений, размещенных в виде облачной службы Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Шаг 1. Развертывание приложения в промежуточной среде.
Эта задача рассматривается как hello toostage приложения с помощью **Microsoft Azure PowerShell**.

1. При публикации службы, просто передайте hello **-слот** параметр hello **AzureServiceProject публикации** командлета.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Войдите на toohello [классический портал Azure] и выберите **облачные службы**. Создается после hello облачной службы и hello **промежуточной** состояние столбца обновлялось слишком**под управлением**, щелкните имя службы hello.
   
   ![портал, на котором отображается выполняющаяся служба][cloud-service]
3. Выберите hello **панели мониторинга**, а затем выберите **промежуточной**.
   
   ![панель мониторинга облачной службы][cloud-service-dashboard]
4. Запомните значение hello в hello **URL-адрес сайта** toohello правом записи. имя DNS Hello — скрытый внутренний идентификатор, созданный Azure.
   
    ![URL-адрес сайта][cloud-service-staging-url]

Теперь можно проверить правильность работы приложения hello в промежуточной среде, используя URL-адрес сайта размещения hello hello.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Шаг 2. Обновление приложения в рабочей среде путем переключения виртуальных IP-адресов
После проверки hello обновленной версии приложения в промежуточной среде, можно быстро облегчить доступен в рабочей среде путем замены hello виртуальных IP-адресов (VIP) hello промежуточной и производственной средах.

> [!NOTE]
> Предполагается, что уже развертывания приложения tooproduction и промежуточное hello обновленной версии приложения.
> 
> 

1. Войти в hello [классический портал Azure], нажмите кнопку **облачные службы** и выберите имя службы hello.
2. Из hello **мониторинга**выберите **промежуточной**и нажмите кнопку **замены** hello нижней части страницы приветствия. При этом откроется hello диалогового окна переключения виртуального IP-адреса.
   
   ![диалоговое окно переключения виртуального IP-адреса][vip-swap-dialog]
3. Просмотрите сведения hello и нажмите кнопку **ОК**. два развертывания Hello начать обновление как промежуточного развертывания коммутаторы tooproduction и hello производственного развертывания коммутаторы toostaging hello.

Вы успешно промежуточное развертывание и обновление развертывания в рабочей среде путем перестановки VIP по развертыванию hello в промежуточной.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Как tooDeploy tooProduction на обновление службы, требуется поменять местами виртуальные IP-адреса в Azure]

[классический портал Azure]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Как tooDeploy tooProduction на обновление службы, требуется поменять местами виртуальные IP-адреса в Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
