---
title: "секреты хранилище ключей Azure стека tooretrieve приложения aaaAllow | Документы Microsoft"
description: "Использование образца приложения toowork с хранилищем ключей Azure стека"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a><span data-ttu-id="17120-103">Запустить образец приложения hello для хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="17120-103">Run hello sample application for Key Vault</span></span>

<span data-ttu-id="17120-104">В этом руководстве используется образец приложения tooretrieve секреты и пароли из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="17120-104">In this guide, you'll use a sample application tooretrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-hello-samples-and-prepare"></a><span data-ttu-id="17120-105">Загрузка образцов hello и подготовка</span><span class="sxs-lookup"><span data-stu-id="17120-105">Download hello samples and prepare</span></span>
<span data-ttu-id="17120-106">Загрузка образцов клиента хранилища ключей Azure hello из hello [странице примеров из хранилища ключей Azure клиента](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="17120-106">Download hello Azure Key Vault client samples from hello [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="17120-107">Извлеките содержимое hello локального компьютера файл .zip tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="17120-107">Extract hello contents of hello .zip file tooyour local computer.</span></span>

<span data-ttu-id="17120-108">Чтение hello **README.md** файла (это текстовый файл), а затем выполните инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="17120-108">Read hello **README.md** file (this is a text file), and then follow hello instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="17120-109">Запуск образца #1 — HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="17120-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="17120-110">HelloKeyVault представляет собой консольное приложение, которое проведет вас через hello основные сценарии, которые поддерживаются хранилищем ключей:</span><span class="sxs-lookup"><span data-stu-id="17120-110">HelloKeyVault is a console application that walks through hello key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="17120-111">Создание и импорта ключа (ключ HSM или программного обеспечения)</span><span class="sxs-lookup"><span data-stu-id="17120-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="17120-112">Зашифровать секретный код, с помощью ключа контента</span><span class="sxs-lookup"><span data-stu-id="17120-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="17120-113">Перенос с помощью ключа хранилища ключей ключ содержимого hello</span><span class="sxs-lookup"><span data-stu-id="17120-113">Wrap hello content key using a Key Vault key</span></span>
4. <span data-ttu-id="17120-114">Извлечение из оболочки hello ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="17120-114">Unwrap hello content key</span></span>
5. <span data-ttu-id="17120-115">Расшифровать секретный код hello</span><span class="sxs-lookup"><span data-stu-id="17120-115">Decrypt hello secret</span></span>
6. <span data-ttu-id="17120-116">Значение секрета</span><span class="sxs-lookup"><span data-stu-id="17120-116">Set a secret</span></span>

<span data-ttu-id="17120-117">Что запуска консольного приложения следует без изменений, за исключением того, будут обновлены hello подходящие параметры конфигурации в файл App.Config toohello, выполните действия в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="17120-117">That console application should run with no changes, except that hello appropriate configuration settings in App.Config will be updated according toohello following steps:</span></span>

1. <span data-ttu-id="17120-118">Обновите параметры конфигурации приложения hello в HelloKeyVault\App.config с URL-адрес хранилища, основной идентификатор приложения и секрет.</span><span class="sxs-lookup"><span data-stu-id="17120-118">Update hello app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="17120-119">сведения о Hello при необходимости можно создавать с помощью **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="17120-119">hello information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="17120-120">Обновление значений hello hello обязательной переменные в GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="17120-120">Update hello values of hello mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="17120-121">Откройте окно Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="17120-121">Launch hello Windows PowerShell window.</span></span>
4. <span data-ttu-id="17120-122">Запустите сценарий GetAppConfigSettings.ps1 hello в окне PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="17120-122">Run hello GetAppConfigSettings.ps1 script within hello PowerShell window.</span></span>
5. <span data-ttu-id="17120-123">Копирование результатов hello hello сценария toohello HelloKeyVault\App.config файла.</span><span class="sxs-lookup"><span data-stu-id="17120-123">Copy hello results of hello script toohello HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17120-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17120-124">Next steps</span></span>
[<span data-ttu-id="17120-125">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="17120-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="17120-126">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="17120-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

