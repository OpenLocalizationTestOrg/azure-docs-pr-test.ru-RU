---
title: "toocreate aaaUse CLI 2.0 приложения Azure AD и настройте его tooaccess API служб мультимедиа Azure | Документы Microsoft"
description: "В этом разделе показано, как toocreate toouse CLI 2.0 приложения Azure AD и настройте его tooaccess API служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Использовать toocreate CLI 2.0 приложения AAD и настройте его tooaccess API служб мультимедиа Azure

В этом разделе показано, как toocreate toouse CLI 2.0 приложение Azure Active Directory (Azure AD) и tooaccess основной службы служб мультимедиа Azure для ресурсов. 

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Учетная запись служб мультимедиа. Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Использовать hello оболочки облако Azure

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Запустите hello оболочки облака из hello верхней панели навигации портала hello.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Дополнительные сведения см. в [обзоре Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Создание приложения Azure AD и настройка учетной записи доступа toohello мультимедиа с CLI 2.0
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Например:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

В этом примере hello **область** — hello полный путь к ресурсу для носителя hello учетная запись службы. Здравствуйте, однако **область** может быть на любом уровне.

Например оно может принимать одно из следующих уровней hello:
 
* Hello **подписки** уровне.
* Hello **группы ресурсов** уровне.
* Hello **ресурсов** уровня (например, учетная запись носителя).

Дополнительные сведения см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).

См. также [Manage Role-Based управления доступом с hello Azure интерфейс командной строки](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Дальнейшие действия

Приступая к работе с [передача файлов учетная запись tooyour](media-services-portal-upload-files.md).
