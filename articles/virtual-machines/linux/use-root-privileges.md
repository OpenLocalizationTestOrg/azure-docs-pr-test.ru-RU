---
title: "aaaUse корневой права на виртуальных машинах Linux | Документы Microsoft"
description: "Узнайте, как корневой toouse права доступа на виртуальной машине Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="b3dc0-103">Использование прав корневой учетной записи на виртуальных машинах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="b3dc0-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b3dc0-104">По умолчанию hello `root` пользователь отключен на виртуальных машинах Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="b3dc0-105">Пользователи могут запускать команды с повышенными привилегиями, используя hello `sudo` команды.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="b3dc0-106">Тем не менее в зависимости от того, как была создана система hello зависит hello качества.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="b3dc0-107">**SSH-ключ и пароль или пароль только** -hello виртуальной машины была создана с сертификатом (`.CER` файл) или ключ SSH, а также пароль, или только имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="b3dc0-108">В этом случае `sudo` предложит ввести пароль пользователя hello перед выполнением команды hello.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="b3dc0-109">**SSH-ключ только** -hello виртуальной машины, была создана с помощью сертификата (`.cer`, `.pem`, или `.pub` файл) или ключа SSH, но без пароля.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="b3dc0-110">В этом случае `sudo` **не будет** запрашивать hello пароль перед выполнением команды hello.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="b3dc0-111">Ключ и пароль или только пароль SSH</span><span class="sxs-lookup"><span data-stu-id="b3dc0-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="b3dc0-112">Войдите на виртуальную машину Linux hello, с помощью ключа или пароля для проверки подлинности SSH, а затем выполните команды с помощью `sudo`, например:</span><span class="sxs-lookup"><span data-stu-id="b3dc0-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="b3dc0-113">В этом случае пользователь hello предложит ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="b3dc0-114">После ввода пароля hello `sudo` будет выполнена команда hello с `root` права.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="b3dc0-115">Можно также включить passwordless sudo, изменив hello `/etc/sudoers.d/waagent` файла, например:</span><span class="sxs-lookup"><span data-stu-id="b3dc0-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="b3dc0-116">Это изменение позволит passwordless sudo пользователем hello «azureuser».</span><span class="sxs-lookup"><span data-stu-id="b3dc0-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="b3dc0-117">Только ключ SSH</span><span class="sxs-lookup"><span data-stu-id="b3dc0-117">SSH Key Only</span></span>
<span data-ttu-id="b3dc0-118">Войдите на виртуальной машине Linux hello, с помощью проверки подлинности SSH с ключом, а затем выполните команды с помощью `sudo`, например:</span><span class="sxs-lookup"><span data-stu-id="b3dc0-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="b3dc0-119">В этом случае будет hello пользователя **не** предложено ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="b3dc0-120">После нажатия `<enter>`, `sudo` будет выполнена команда hello с `root` права.</span><span class="sxs-lookup"><span data-stu-id="b3dc0-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

