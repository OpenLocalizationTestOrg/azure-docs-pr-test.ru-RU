---
title: "Разрешить приложению получать секреты в хранилище ключей Azure стек | Документы Microsoft"
description: "Использование примера приложения для работы с хранилищем ключей Azure стека"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a><span data-ttu-id="7fd29-103">Запустить образец приложения для хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="7fd29-103">Run the sample application for Key Vault</span></span>

<span data-ttu-id="7fd29-104">В этом руководстве используется образец приложения для получения секреты и пароли из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="7fd29-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-the-samples-and-prepare"></a><span data-ttu-id="7fd29-105">Загрузка образцов и подготовка</span><span class="sxs-lookup"><span data-stu-id="7fd29-105">Download the samples and prepare</span></span>
<span data-ttu-id="7fd29-106">Загрузка образцов клиента хранилища ключей Azure из [странице примеров из хранилища ключей Azure клиента](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="7fd29-106">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="7fd29-107">Извлеките содержимое ZIP-файл на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="7fd29-107">Extract the contents of the .zip file to your local computer.</span></span>

<span data-ttu-id="7fd29-108">Чтение **README.md** файла (это текстовый файл), а затем следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="7fd29-108">Read the **README.md** file (this is a text file), and then follow the instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="7fd29-109">Запуск образца #1 — HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="7fd29-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="7fd29-110">HelloKeyVault представляет собой консольное приложение, которое проведет вас через основные сценарии, которые поддерживаются хранилищем ключей:</span><span class="sxs-lookup"><span data-stu-id="7fd29-110">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="7fd29-111">Создание и импорта ключа (ключ HSM или программного обеспечения)</span><span class="sxs-lookup"><span data-stu-id="7fd29-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="7fd29-112">Зашифровать секретный код, с помощью ключа контента</span><span class="sxs-lookup"><span data-stu-id="7fd29-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="7fd29-113">Ключ содержимого с помощью ключа хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="7fd29-113">Wrap the content key using a Key Vault key</span></span>
4. <span data-ttu-id="7fd29-114">Извлечение из оболочки ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="7fd29-114">Unwrap the content key</span></span>
5. <span data-ttu-id="7fd29-115">Расшифровать секретный код</span><span class="sxs-lookup"><span data-stu-id="7fd29-115">Decrypt the secret</span></span>
6. <span data-ttu-id="7fd29-116">Значение секрета</span><span class="sxs-lookup"><span data-stu-id="7fd29-116">Set a secret</span></span>

<span data-ttu-id="7fd29-117">Что запуска консольного приложения следует без изменений, за исключением того, что соответствующие настройки в файле App.Config обновляется с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="7fd29-117">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span></span>

1. <span data-ttu-id="7fd29-118">Обновите параметры конфигурации приложения в HelloKeyVault\App.config с URL-адрес хранилища, основной идентификатор приложения и секрет.</span><span class="sxs-lookup"><span data-stu-id="7fd29-118">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="7fd29-119">Эти сведения можно при необходимости создаются с помощью **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="7fd29-119">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="7fd29-120">Обновление значений обязательной переменные в GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="7fd29-120">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="7fd29-121">Откройте окно Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fd29-121">Launch the Windows PowerShell window.</span></span>
4. <span data-ttu-id="7fd29-122">Запустите сценарий GetAppConfigSettings.ps1 в окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fd29-122">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span></span>
5. <span data-ttu-id="7fd29-123">Скопируйте файл HelloKeyVault\App.config результаты работы скрипта.</span><span class="sxs-lookup"><span data-stu-id="7fd29-123">Copy the results of the script to the HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd29-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fd29-124">Next steps</span></span>
[<span data-ttu-id="7fd29-125">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="7fd29-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="7fd29-126">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="7fd29-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

