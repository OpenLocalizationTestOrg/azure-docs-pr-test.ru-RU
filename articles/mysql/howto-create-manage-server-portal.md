---
title: "Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure | Документация Майкрософт"
description: "В этой статье описывается, как быстро создать сервер базы данных Azure для MySQL и управлять этим сервером с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="0107e-103">Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="0107e-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="0107e-104">В этой статье описывается, как быстро создать сервер базы данных Azure для MySQL и управлять этим сервером с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0107e-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="0107e-105">Управление сервером включает в себя просмотр сведений о сервере и базах данных, сброс пароля и удаление сервера.</span><span class="sxs-lookup"><span data-stu-id="0107e-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="0107e-106">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0107e-106">Log in to the Azure portal</span></span>
<span data-ttu-id="0107e-107">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0107e-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0107e-108">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0107e-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0107e-109">Чтобы создать сервер базы данных Azure для MySQL с именем mysqlserver4demo, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="0107e-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="0107e-110">1- Нажмите кнопку **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0107e-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="0107e-111">2- Выберите **Базы данных** на странице создания и щелкните **Azure Database for MySQL** (База данных Azure для MySQL) на странице "Базы данных".</span><span class="sxs-lookup"><span data-stu-id="0107e-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="0107e-112">Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0107e-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="0107e-113">База данных создается в группе ресурсов Azure и на логическом сервере базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0107e-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="0107e-115">3- Заполните форму базы данных Azure для MySQL, указав следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="0107e-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="0107e-116">**Поле формы**</span><span class="sxs-lookup"><span data-stu-id="0107e-116">**Form Field**</span></span> | <span data-ttu-id="0107e-117">**Описание поля**</span><span class="sxs-lookup"><span data-stu-id="0107e-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="0107e-118">*Server name* (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="0107e-118">*Server name*</span></span> | <span data-ttu-id="0107e-119">azure-mysql (глобально уникальное имя сервера).</span><span class="sxs-lookup"><span data-stu-id="0107e-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="0107e-120">*Подписка*</span><span class="sxs-lookup"><span data-stu-id="0107e-120">*Subscription*</span></span> | <span data-ttu-id="0107e-121">MySQLaaS (выберите из раскрывающегося списка).</span><span class="sxs-lookup"><span data-stu-id="0107e-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="0107e-122">*Группа ресурсов*</span><span class="sxs-lookup"><span data-stu-id="0107e-122">*Resource group*</span></span> | <span data-ttu-id="0107e-123">myresource (создайте новую группу ресурсов или используйте существующую).</span><span class="sxs-lookup"><span data-stu-id="0107e-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="0107e-124">*Имя для входа администратора сервера*</span><span class="sxs-lookup"><span data-stu-id="0107e-124">*Server admin login*</span></span> | <span data-ttu-id="0107e-125">myadmin (укажите имя учетной записи администратора)</span><span class="sxs-lookup"><span data-stu-id="0107e-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="0107e-126">*Пароль*</span><span class="sxs-lookup"><span data-stu-id="0107e-126">*Password*</span></span> | <span data-ttu-id="0107e-127">Задайте пароль учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="0107e-127">setup admin account password</span></span> |
| <span data-ttu-id="0107e-128">*Подтверждение пароля.*</span><span class="sxs-lookup"><span data-stu-id="0107e-128">*Confirm password*</span></span> | <span data-ttu-id="0107e-129">Подтвердите пароль учетной записи администратора</span><span class="sxs-lookup"><span data-stu-id="0107e-129">confirm admin account password</span></span> |
| <span data-ttu-id="0107e-130">*Расположение*</span><span class="sxs-lookup"><span data-stu-id="0107e-130">*Location*</span></span> | <span data-ttu-id="0107e-131">Северная Европа (выберите регион "Северная Европа" или "Западная часть США").</span><span class="sxs-lookup"><span data-stu-id="0107e-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="0107e-132">*Версия*</span><span class="sxs-lookup"><span data-stu-id="0107e-132">*Version*</span></span> | <span data-ttu-id="0107e-133">5.6 (выберите версию сервера базы данных Azure для MySQL).</span><span class="sxs-lookup"><span data-stu-id="0107e-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="0107e-134">4- Щелкните **Ценовая категория**, чтобы указать уровень производительности и уровень служб для нового сервера.</span><span class="sxs-lookup"><span data-stu-id="0107e-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="0107e-135">Для уровня "Базовый" можно настроить от 50 до 100 единиц вычислений, для уровня "Стандартный" — от 100 до 200 единиц вычислений. Емкость хранилища можно добавлять в пределах допустимого объема.</span><span class="sxs-lookup"><span data-stu-id="0107e-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="0107e-136">В рамках этого практического руководства выберите 50 единиц вычислений и хранилище емкостью в 50 ГБ.</span><span class="sxs-lookup"><span data-stu-id="0107e-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="0107e-137">Нажмите кнопку **ОК** , чтобы сохранить изменение.</span><span class="sxs-lookup"><span data-stu-id="0107e-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="0107e-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="0107e-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="0107e-139">5- Нажмите кнопку **Создать**, чтобы подготовить сервер.</span><span class="sxs-lookup"><span data-stu-id="0107e-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="0107e-140">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0107e-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="0107e-141">Установите флажок **Закрепить на панели мониторинга**, чтобы с легкостью отслеживать процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="0107e-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="0107e-142">Несмотря на то, что для уровне "Базовый" и "Стандартный" поддерживается хранилище до 1000 и 10 000 ГБ соответственно, в общедоступной предварительной версии максимальный размер хранилища временно ограничен до 1000 ГБ.</span><span class="sxs-lookup"><span data-stu-id="0107e-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="0107e-143">Обновление сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0107e-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="0107e-144">После подготовки нового сервера пользователь может изменить его двумя способами: сбросить пароль администратора или масштабировать ресурсы сервера, изменив количество единиц вычислений.</span><span class="sxs-lookup"><span data-stu-id="0107e-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="0107e-145">Изменение пароля администратора</span><span class="sxs-lookup"><span data-stu-id="0107e-145">Change the administrator user password</span></span>
<span data-ttu-id="0107e-146">1- В колонке **Обзор** сервера щелкните **Сбросить пароль**, чтобы заполнить окно ввода и подтверждения пароля.</span><span class="sxs-lookup"><span data-stu-id="0107e-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="0107e-147">2- Введите новый пароль и подтвердите его в окне, как показано ниже. ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="0107e-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="0107e-148">3- Нажмите кнопку **ОК** , чтобы сохранить новый пароль.</span><span class="sxs-lookup"><span data-stu-id="0107e-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="0107e-149">Масштабирование с помощью изменения количества единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0107e-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="0107e-150">1- В колонке сервера в разделе **Параметры** щелкните **Ценовая категория**, чтобы открыть колонку "Ценовая категория" для сервера базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0107e-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="0107e-151">2- Выполните шаг 4 из руководства **Создание сервера базы данных Azure для MySQL**, чтобы изменить число единицы вычислений в текущей ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="0107e-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="0107e-152">Удаление сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0107e-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="0107e-153">1- В колонке **Обзор** сервера нажмите кнопку **Удалить**, чтобы открыть колонку подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="0107e-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="0107e-154">2- Введите правильное имя сервера в поле ввода в колонке, чтобы еще раз подтвердить его удаление.</span><span class="sxs-lookup"><span data-stu-id="0107e-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="0107e-155">3- Нажмите кнопку **Удалить** еще раз, чтобы подтвердить действие удаления, и дождитесь появления всплывающего окна "Deleting success" (Удаление выполнено) на панели уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0107e-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="0107e-156">Вывод списка баз данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0107e-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="0107e-157">Прокрутите колонку **Обзор** сервера вниз до элемента базы данных.</span><span class="sxs-lookup"><span data-stu-id="0107e-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="0107e-158">Все базы данных будут отображены в таблице.</span><span class="sxs-lookup"><span data-stu-id="0107e-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="0107e-159">Нажмите кнопку **Удалить**, чтобы открыть колонку подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="0107e-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="0107e-161">Отображение сведений о сервере базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0107e-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="0107e-162">Щелкните **Свойства** в разделе **Параметры** в колонке сервера. Откроется колонка **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0107e-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="0107e-163">В ней можно просмотреть подробные сведения о сервере.</span><span class="sxs-lookup"><span data-stu-id="0107e-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0107e-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0107e-164">Next steps</span></span>

[<span data-ttu-id="0107e-165">Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="0107e-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
