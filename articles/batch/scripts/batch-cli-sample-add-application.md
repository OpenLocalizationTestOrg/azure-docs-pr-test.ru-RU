---
title: "Пример сценария Azure CLI для добавления приложения в пакетную службу | Документация Майкрософт"
description: "Пример сценария Azure CLI для добавления приложения в пакетную службу."
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="5dfa9-103">Добавление приложений в пакетную службу Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5dfa9-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="5dfa9-104">Этот сценарий демонстрирует настройку приложения для использования в пуле или задаче пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="5dfa9-105">Чтобы настроить приложение, упакуйте его исполняемый файл и зависимые компоненты в ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="5dfa9-106">В этом примере ZIP-файл с исполняемым файлом называется my-приложения-exe.zip.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dfa9-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5dfa9-107">Prerequisites</span></span>

- <span data-ttu-id="5dfa9-108">Установите Azure CLI с помощью инструкций, приведенных в [руководстве по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="5dfa9-109">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="5dfa9-110">Пример скрипта создания учетной записи см. в статье [Создание учетной записи пакетной службы с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="5dfa9-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5dfa9-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5dfa9-111">Sample script</span></span>

<span data-ttu-id="5dfa9-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Добавление приложения")]</span><span class="sxs-lookup"><span data-stu-id="5dfa9-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="5dfa9-113">Очистка приложения</span><span class="sxs-lookup"><span data-stu-id="5dfa9-113">Clean up application</span></span>

<span data-ttu-id="5dfa9-114">После запуска приведенного выше примера сценария выполните следующие команды, чтобы удалить приложение и все его переданные пакеты приложения.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5dfa9-115">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5dfa9-115">Script explanation</span></span>

<span data-ttu-id="5dfa9-116">Этот сценарий использует приведенные ниже команды для создания приложения и передачи пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="5dfa9-117">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5dfa9-118">Команда</span><span class="sxs-lookup"><span data-stu-id="5dfa9-118">Command</span></span> | <span data-ttu-id="5dfa9-119">Примечания</span><span class="sxs-lookup"><span data-stu-id="5dfa9-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5dfa9-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="5dfa9-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="5dfa9-121">Создает приложение.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-121">Creates an application.</span></span>  |
| [<span data-ttu-id="5dfa9-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="5dfa9-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="5dfa9-123">Обновляет свойства приложения.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="5dfa9-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="5dfa9-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="5dfa9-125">Добавляет пакет приложения в указанное приложение.</span><span class="sxs-lookup"><span data-stu-id="5dfa9-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="5dfa9-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dfa9-126">Next steps</span></span>

<span data-ttu-id="5dfa9-127">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5dfa9-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5dfa9-128">Дополнительные примеры скриптов для интерфейса командной строки пакетной службы см. в [документации по интерфейсу командной строки пакетной службы Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5dfa9-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
