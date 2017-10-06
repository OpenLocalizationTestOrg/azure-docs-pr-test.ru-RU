---
title: "aaaUse Robomongo для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toouse Robomongo с Azure DB Cosmos: API для MongoDB учетной записи"
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="0597f-104">Использование Robomongo с учетной записью API для MongoDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0597f-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="0597f-105">tooconnect tooan Azure Cosmos DB: API для MongoDB учетной записи, с помощью Robomongo необходимо:</span><span class="sxs-lookup"><span data-stu-id="0597f-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="0597f-106">скачать и установить [Robomongo](https://robomongo.org/);</span><span class="sxs-lookup"><span data-stu-id="0597f-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="0597f-107">Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0597f-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="0597f-108">Подключение с использованием Robomongo</span><span class="sxs-lookup"><span data-stu-id="0597f-108">Connect using Robomongo</span></span>
<span data-ttu-id="0597f-109">tooadd Cosmos базы данных Azure: API для учетной записи MongoDB toohello Robomongo MongoDB подключений, выполнения hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="0597f-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="0597f-110">Получить Cosmos базы данных Azure: API для MongoDB сведений о соединении учетной записи с помощью инструкций hello [здесь](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="0597f-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Снимок экрана: колонка строка подключения hello](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="0597f-112">Запустите *Robomongo.exe*.</span><span class="sxs-lookup"><span data-stu-id="0597f-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="0597f-113">Нажмите кнопку подключения hello под **файл** toomanage подключений.</span><span class="sxs-lookup"><span data-stu-id="0597f-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="0597f-114">Нажмите кнопку **создать** в hello **подключений MongoDB** окна, который будет открыть hello **параметры подключения** окна.</span><span class="sxs-lookup"><span data-stu-id="0597f-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="0597f-115">В hello **параметры подключения** окно, выберите имя.</span><span class="sxs-lookup"><span data-stu-id="0597f-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="0597f-116">Найдите hello **узла** и **порт** из данные подключения в шаге 1 и введите их в **адрес** и **порт**соответственно .</span><span class="sxs-lookup"><span data-stu-id="0597f-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Снимок экрана: hello Robomongo Управление соединениями](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="0597f-118">На hello **проверки подлинности** щелкните **выполнение проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="0597f-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="0597f-119">Затем введите базу данных (по умолчанию — *Admin*), **имя пользователя** и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0597f-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="0597f-120">**Имя пользователя** и **пароль** можно найти в данных подключения, полученных на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="0597f-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Снимок экрана: hello вкладку Robomongo проверки подлинности](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="0597f-122">На hello **SSL** установите флажок **протокол SSL используется**, затем измените hello **метод проверки подлинности** слишком**самозаверяющего сертификата**.</span><span class="sxs-lookup"><span data-stu-id="0597f-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Снимок экрана: hello вкладку Robomongo SSL](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="0597f-124">Наконец, нажмите кнопку **теста** tooverify, затем являются может tooconnect **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0597f-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0597f-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0597f-125">Next steps</span></span>
* <span data-ttu-id="0597f-126">Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0597f-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
