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
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure
В этой статье описываются можно быстро создать новую базу данных Azure для MySQL server и управлять ими с помощью портала Azure hello server hello. Управление сервером включает просмотр сведения о сервере и баз данных, сброс пароля и удаления сервера hello.

## <a name="log-in-toohello-azure-portal"></a>Войдите в toohello портал Azure
Войдите в toohello [портал Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Создание сервера базы данных Azure для MySQL
Выполните эти шаги toocreate базы данных Azure для сервера MySQL с именем «mysqlserver4demo»

1-click **New** кнопка найдена в верхнем левом углу hello hello портал Azure.

Выберите 2 **баз данных** из hello новую страницу и выберите **базы данных Azure для MySQL** со страницы приветствия баз данных.

> Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md). Hello базы данных создается в группе ресурсов Azure и в базе данных для сервера MySQL.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - заполните hello базы данных Azure для MySQL формы с hello следующую информацию:

| **Поле формы** | **Описание поля** |
|----------------|-----------------------|
| *Server name* (Имя сервера) | azure-mysql (глобально уникальное имя сервера). |
| *Подписка* | MySQLaaS (выберите из раскрывающегося списка). |
| *Группа ресурсов* | myresource (создайте новую группу ресурсов или используйте существующую). |
| *Имя для входа администратора сервера* | myadmin (укажите имя учетной записи администратора) |
| *Пароль* | Задайте пароль учетной записи администратора. |
| *Подтверждение пароля.* | Подтвердите пароль учетной записи администратора |
| *Расположение* | Северная Европа (выберите регион "Северная Европа" или "Западная часть США"). |
| *Версия* | 5.6 (выберите версию сервера базы данных Azure для MySQL). |

Нажмите кнопку 4 **Ценовая категория** toospecify hello службы уровня и уровня производительности для нового сервера. Для уровня "Базовый" можно настроить от 50 до 100 единиц вычислений, для уровня "Стандартный" — от 100 до 200 единиц вычислений. Емкость хранилища можно добавлять в пределах допустимого объема. В рамках этого практического руководства выберите 50 единиц вычислений и хранилище емкостью в 50 ГБ. Нажмите кнопку **ОК** toosave ваш выбор.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Нажмите кнопку 5 **создать** tooprovision hello server. Подготовка занимает несколько минут.

> Проверьте hello **toodashboard ПИН-код** параметр tooallow легко отслеживания развертываний.
> [!NOTE]
> Несмотря на то, что too1000GB в базовый уровень и 10000 ГБ в стандартном уровня будет поддерживаться для хранения, для общедоступной предварительной версии hello максимальный объем хранилища — по-прежнему ограничено too1000GB временно. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Обновление сервера базы данных Azure для MySQL
После подготовки нового сервера пользователь имеет 2 tooedit параметры существующего сервера: сброс пароля администратора или масштаб для увеличения или уменьшения hello server путем изменения hello вычислений — единицы.

### <a name="change-hello-administrator-user-password"></a>Смена пароля пользователя администратора hello
1 — на сервере hello **Обзор** колонка, щелкните **сброс пароля** toopopulate окна ввод и подтверждение пароля.

2 - введите новый пароль и подтверждение пароля hello в окне приветствия, как показано ниже: ![сброса пароля](./media/howto-create-manage-server-portal/reset-password.png)

Нажмите кнопку 3 **ОК** toosave hello новый пароль.

### <a name="scale-updown-by-changing-compute-units"></a>Масштабирование с помощью изменения количества единиц вычислений

1 — в колонке сервера hello в разделе **параметры**, нажмите кнопку **Ценовая категория** tooopen цены hello уровня колонке hello базы данных Azure для сервера MySQL.

Выполните 2 шага 4 в **создания базы данных Azure для сервера MySQL** toochange вычислений единицы в hello же ценовой категории.

## <a name="delete-an-azure-database-for-mysql-server"></a>Удаление сервера базы данных Azure для MySQL

1 — на сервере hello **Обзор** колонке нажмите кнопку **удалить** команда кнопки tooopen hello удаление подтверждения колонку.

Тип 2 hello правильное имя сервера в поле ввода колонка hello двойные подтверждения.

Нажмите кнопку 3 **удалить** еще раз кнопку tooconfirm удаление действия и дождитесь всплывающее окно «Удаление успех» на панель уведомлений hello.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Список hello базы данных Azure для баз данных MySQL
На сервере hello **Обзор** колонки, прокрутите вниз до базы данных hello плитку на нижней hello. Все базы данных hello отображаются в таблице hello. Нажмите кнопку **удалить** команда кнопки tooopen hello удаление подтверждения колонку.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Отображение сведений о сервере базы данных Azure для MySQL
Нажмите кнопку **свойства** под **параметры** на сервере hello колонке откроется hello **свойства** колонку. Затем можно просмотреть все подробные сведения о сервере hello.

## <a name="next-steps"></a>Дальнейшие действия

[Создание сервера базы данных Azure для MySQL и управление им с помощью портала Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
