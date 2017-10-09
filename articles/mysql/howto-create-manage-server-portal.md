---
title: "aaaCreate и управления базой данных Azure для сервера MySQL с помощью портала Azure | Документы Microsoft"
description: "В этой статье описываются можно быстро создать новую базу данных Azure для MySQL server и управлять ими с помощью портала Azure hello server hello."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="8c26d-103">Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8c26d-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="8c26d-104">В этой статье описываются можно быстро создать новую базу данных Azure для MySQL server и управлять ими с помощью портала Azure hello server hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="8c26d-105">Управление сервером включает просмотр сведения о сервере и баз данных, сброс пароля и удаления сервера hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="8c26d-106">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8c26d-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="8c26d-107">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c26d-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="8c26d-108">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="8c26d-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="8c26d-109">Выполните эти шаги toocreate базы данных Azure для сервера MySQL с именем «mysqlserver4demo»</span><span class="sxs-lookup"><span data-stu-id="8c26d-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="8c26d-110">1-click **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c26d-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="8c26d-111">Выберите 2 **баз данных** из hello новую страницу и выберите **базы данных Azure для MySQL** со страницы приветствия баз данных.</span><span class="sxs-lookup"><span data-stu-id="8c26d-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="8c26d-112">Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8c26d-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="8c26d-113">Hello базы данных создается в группе ресурсов Azure и в базе данных для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="8c26d-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="8c26d-115">3 - заполните hello базы данных Azure для MySQL формы с hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="8c26d-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="8c26d-116">**Поле формы**</span><span class="sxs-lookup"><span data-stu-id="8c26d-116">**Form Field**</span></span> | <span data-ttu-id="8c26d-117">**Описание поля**</span><span class="sxs-lookup"><span data-stu-id="8c26d-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="8c26d-118">*Server name* (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="8c26d-118">*Server name*</span></span> | <span data-ttu-id="8c26d-119">azure-mysql (глобально уникальное имя сервера).</span><span class="sxs-lookup"><span data-stu-id="8c26d-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="8c26d-120">*Подписка*</span><span class="sxs-lookup"><span data-stu-id="8c26d-120">*Subscription*</span></span> | <span data-ttu-id="8c26d-121">MySQLaaS (выберите из раскрывающегося списка).</span><span class="sxs-lookup"><span data-stu-id="8c26d-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="8c26d-122">*Группа ресурсов*</span><span class="sxs-lookup"><span data-stu-id="8c26d-122">*Resource group*</span></span> | <span data-ttu-id="8c26d-123">myresource (создайте новую группу ресурсов или используйте существующую).</span><span class="sxs-lookup"><span data-stu-id="8c26d-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="8c26d-124">*Имя для входа администратора сервера*</span><span class="sxs-lookup"><span data-stu-id="8c26d-124">*Server admin login*</span></span> | <span data-ttu-id="8c26d-125">myadmin (укажите имя учетной записи администратора)</span><span class="sxs-lookup"><span data-stu-id="8c26d-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="8c26d-126">*Пароль*</span><span class="sxs-lookup"><span data-stu-id="8c26d-126">*Password*</span></span> | <span data-ttu-id="8c26d-127">Задайте пароль учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="8c26d-127">setup admin account password</span></span> |
| <span data-ttu-id="8c26d-128">*Подтверждение пароля.*</span><span class="sxs-lookup"><span data-stu-id="8c26d-128">*Confirm password*</span></span> | <span data-ttu-id="8c26d-129">Подтвердите пароль учетной записи администратора</span><span class="sxs-lookup"><span data-stu-id="8c26d-129">confirm admin account password</span></span> |
| <span data-ttu-id="8c26d-130">*Расположение*</span><span class="sxs-lookup"><span data-stu-id="8c26d-130">*Location*</span></span> | <span data-ttu-id="8c26d-131">Северная Европа (выберите регион "Северная Европа" или "Западная часть США").</span><span class="sxs-lookup"><span data-stu-id="8c26d-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="8c26d-132">*Версия*</span><span class="sxs-lookup"><span data-stu-id="8c26d-132">*Version*</span></span> | <span data-ttu-id="8c26d-133">5.6 (выберите версию сервера базы данных Azure для MySQL).</span><span class="sxs-lookup"><span data-stu-id="8c26d-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="8c26d-134">Нажмите кнопку 4 **Ценовая категория** toospecify hello службы уровня и уровня производительности для нового сервера.</span><span class="sxs-lookup"><span data-stu-id="8c26d-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="8c26d-135">Для уровня "Базовый" можно настроить от 50 до 100 единиц вычислений, для уровня "Стандартный" — от 100 до 200 единиц вычислений. Емкость хранилища можно добавлять в пределах допустимого объема.</span><span class="sxs-lookup"><span data-stu-id="8c26d-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="8c26d-136">В рамках этого практического руководства выберите 50 единиц вычислений и хранилище емкостью в 50 ГБ.</span><span class="sxs-lookup"><span data-stu-id="8c26d-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="8c26d-137">Нажмите кнопку **ОК** toosave ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="8c26d-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="8c26d-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="8c26d-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="8c26d-139">Нажмите кнопку 5 **создать** tooprovision hello server.</span><span class="sxs-lookup"><span data-stu-id="8c26d-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="8c26d-140">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8c26d-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="8c26d-141">Проверьте hello **toodashboard ПИН-код** параметр tooallow легко отслеживания развертываний.</span><span class="sxs-lookup"><span data-stu-id="8c26d-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="8c26d-142">Несмотря на то, что too1000GB в базовый уровень и 10000 ГБ в стандартном уровня будет поддерживаться для хранения, для общедоступной предварительной версии hello максимальный объем хранилища — по-прежнему ограничено too1000GB временно.</span><span class="sxs-lookup"><span data-stu-id="8c26d-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="8c26d-143">Обновление сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="8c26d-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="8c26d-144">После подготовки нового сервера пользователь имеет 2 tooedit параметры существующего сервера: сброс пароля администратора или масштаб для увеличения или уменьшения hello server путем изменения hello вычислений — единицы.</span><span class="sxs-lookup"><span data-stu-id="8c26d-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="8c26d-145">Смена пароля пользователя администратора hello</span><span class="sxs-lookup"><span data-stu-id="8c26d-145">Change hello administrator user password</span></span>
<span data-ttu-id="8c26d-146">1 — на сервере hello **Обзор** колонка, щелкните **сброс пароля** toopopulate окна ввод и подтверждение пароля.</span><span class="sxs-lookup"><span data-stu-id="8c26d-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="8c26d-147">2 - введите новый пароль и подтверждение пароля hello в окне приветствия, как показано ниже: ![сброса пароля](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="8c26d-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="8c26d-148">Нажмите кнопку 3 **ОК** toosave hello новый пароль.</span><span class="sxs-lookup"><span data-stu-id="8c26d-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="8c26d-149">Масштабирование с помощью изменения количества единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="8c26d-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="8c26d-150">1 — в колонке сервера hello в разделе **параметры**, нажмите кнопку **Ценовая категория** tooopen цены hello уровня колонке hello базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="8c26d-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="8c26d-151">Выполните 2 шага 4 в **создания базы данных Azure для сервера MySQL** toochange вычислений единицы в hello же ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="8c26d-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="8c26d-152">Удаление сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="8c26d-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="8c26d-153">1 — на сервере hello **Обзор** колонке нажмите кнопку **удалить** команда кнопки tooopen hello удаление подтверждения колонку.</span><span class="sxs-lookup"><span data-stu-id="8c26d-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="8c26d-154">Тип 2 hello правильное имя сервера в поле ввода колонка hello двойные подтверждения.</span><span class="sxs-lookup"><span data-stu-id="8c26d-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="8c26d-155">Нажмите кнопку 3 **удалить** еще раз кнопку tooconfirm удаление действия и дождитесь всплывающее окно «Удаление успех» на панель уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="8c26d-156">Список hello базы данных Azure для баз данных MySQL</span><span class="sxs-lookup"><span data-stu-id="8c26d-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="8c26d-157">На сервере hello **Обзор** колонки, прокрутите вниз до базы данных hello плитку на нижней hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="8c26d-158">Все базы данных hello отображаются в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="8c26d-159">Нажмите кнопку **удалить** команда кнопки tooopen hello удаление подтверждения колонку.</span><span class="sxs-lookup"><span data-stu-id="8c26d-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="8c26d-161">Отображение сведений о сервере базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="8c26d-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="8c26d-162">Нажмите кнопку **свойства** под **параметры** на сервере hello колонке откроется hello **свойства** колонку.</span><span class="sxs-lookup"><span data-stu-id="8c26d-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="8c26d-163">Затем можно просмотреть все подробные сведения о сервере hello.</span><span class="sxs-lookup"><span data-stu-id="8c26d-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c26d-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c26d-164">Next steps</span></span>

[<span data-ttu-id="8c26d-165">Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8c26d-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
