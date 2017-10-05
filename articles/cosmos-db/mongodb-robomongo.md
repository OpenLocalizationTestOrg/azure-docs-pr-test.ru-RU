---
title: "Использование Robomongo с Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как использовать Robomongo с учетной записью API для MongoDB в Azure Cosmos DB."
keywords: Robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="1d45c-104">Использование Robomongo с учетной записью API для MongoDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1d45c-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="1d45c-105">Чтобы подключиться к учетной записи API для MongoDB в Azure Cosmos DB с помощью Robomongo, необходимо:</span><span class="sxs-lookup"><span data-stu-id="1d45c-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="1d45c-106">скачать и установить [Robomongo](https://robomongo.org/);</span><span class="sxs-lookup"><span data-stu-id="1d45c-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="1d45c-107">Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1d45c-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="1d45c-108">Подключение с использованием Robomongo</span><span class="sxs-lookup"><span data-stu-id="1d45c-108">Connect using Robomongo</span></span>
<span data-ttu-id="1d45c-109">Чтобы добавить к подключениям Robomongo MongoDB учетную запись API для MongoDB в Azure Cosmos DB, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1d45c-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="1d45c-110">Извлеките сведения о подключении учетной записи API для MongoDB в Azure Cosmos DB. Ознакомьтесь с инструкциями [здесь](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="1d45c-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Снимок экрана, колонка строки подключения](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="1d45c-112">Запустите *Robomongo.exe*.</span><span class="sxs-lookup"><span data-stu-id="1d45c-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="1d45c-113">Нажмите кнопку подключения под меню **File** (Файл) для управления подключениями.</span><span class="sxs-lookup"><span data-stu-id="1d45c-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="1d45c-114">Щелкните **Create** (Создать) в окне **MongoDB Connections** (Подключения MongoDB). Откроется окно **Connection Settings** (Параметры подключения).</span><span class="sxs-lookup"><span data-stu-id="1d45c-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="1d45c-115">В окне **Connection Settings** (Параметры подключения) выберите имя.</span><span class="sxs-lookup"><span data-stu-id="1d45c-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="1d45c-116">Затем найдите **узел** и **порт**, указанные в сведениях о подключении, полученных на шаге 1, и введите их в полях **Address** (Адрес) и **Port** (Порт) соответственно.</span><span class="sxs-lookup"><span data-stu-id="1d45c-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Снимок экрана окна управления подключениями Robomongo](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="1d45c-118">На вкладке **Authentication** (Аутентификация) установите флажок **Perform authentication** (Выполнять аутентификацию).</span><span class="sxs-lookup"><span data-stu-id="1d45c-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="1d45c-119">Затем введите базу данных (по умолчанию — *Admin*), **имя пользователя** и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1d45c-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="1d45c-120">**Имя пользователя** и **пароль** можно найти в данных подключения, полученных на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1d45c-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Снимок экрана вкладки аутентификации Robomongo](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="1d45c-122">На вкладке **SSL** установите флажок **Use SSL protocol** (Использовать протокол SSL), затем измените значение параметра **Authentication Method** (Метод аутентификации) на **Self-signed Certificate** (Самозаверяющий сертификат).</span><span class="sxs-lookup"><span data-stu-id="1d45c-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Снимок экрана вкладки SSL Robomongo](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="1d45c-124">Наконец, нажмите кнопку **Test** (Проверить), чтобы проверить возможность подключения, затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="1d45c-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d45c-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d45c-125">Next steps</span></span>
* <span data-ttu-id="1d45c-126">Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1d45c-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
