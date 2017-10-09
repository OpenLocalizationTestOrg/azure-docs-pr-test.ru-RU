---
title: "Общие сведения о разработке приложений aaaDatabase для базы данных Azure для MySQL | Документы Microsoft"
description: "Появились вопросы проектирования, разработчику необходимо следовать при написании приложения код tooconnect tooAzure базы данных для MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="57b23-103">Обзор разработки приложений для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="57b23-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="57b23-104">В этой статье рассматриваются вопросы проектирования, разработчику необходимо следовать при написании приложения код tooconnect tooAzure базы данных для MySQL</span><span class="sxs-lookup"><span data-stu-id="57b23-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="57b23-105">Учебник отображение вы toocreate server, создать брандмауэр на основе сервера, просмотр свойств сервера, создание базы данных, подключение и запрос с использованием рабочей среды и mysql.exe см [проектирование первой базы данных MySQL в Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="57b23-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="57b23-106">Язык и платформа</span><span class="sxs-lookup"><span data-stu-id="57b23-106">Language and platform</span></span>
<span data-ttu-id="57b23-107">Доступны примеры кода на разных языках программирования и для разных платформ.</span><span class="sxs-lookup"><span data-stu-id="57b23-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="57b23-108">Toohello образцов кода можно найти следующие ссылки: [библиотек подключений используется tooconnect tooAzure базы данных для MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="57b23-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="57b23-109">Средства</span><span class="sxs-lookup"><span data-stu-id="57b23-109">Tools</span></span>
<span data-ttu-id="57b23-110">База данных Azure для MySQL использует hello MySQL community версии, совместимой с MySQL стандартные инструменты управления, таких как Workbench или MySQL служебные программы, например mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)и др.</span><span class="sxs-lookup"><span data-stu-id="57b23-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="57b23-111">Также можно использовать hello портал Azure, Azure CLI и toointeract API-интерфейс REST со службой hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="57b23-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="57b23-112">Ограничения ресурсов</span><span class="sxs-lookup"><span data-stu-id="57b23-112">Resource limitations</span></span>
<span data-ttu-id="57b23-113">База данных MySQL в Azure управляет hello ресурсы доступны tooa сервера с помощью двух разных механизмов:</span><span class="sxs-lookup"><span data-stu-id="57b23-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="57b23-114">управление ресурсами;</span><span class="sxs-lookup"><span data-stu-id="57b23-114">Resources Governance</span></span> 
- <span data-ttu-id="57b23-115">принудительное применение ограничений.</span><span class="sxs-lookup"><span data-stu-id="57b23-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="57b23-116">Безопасность</span><span class="sxs-lookup"><span data-stu-id="57b23-116">Security</span></span>
<span data-ttu-id="57b23-117">База данных Azure MySQL предоставляет ресурсы для ограничения доступа, защиты данных, настройки пользователей и ролей и мониторинга действий в базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="57b23-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="57b23-118">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="57b23-118">Authentication</span></span>
<span data-ttu-id="57b23-119">База данных Azure MySQL поддерживает аутентификацию пользователей и имен входа на сервере.</span><span class="sxs-lookup"><span data-stu-id="57b23-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="57b23-120">Устойчивость</span><span class="sxs-lookup"><span data-stu-id="57b23-120">Resiliency</span></span>
<span data-ttu-id="57b23-121">В случае временная ошибка при подключении базы данных tooMySQL кода следует повторить вызов hello.</span><span class="sxs-lookup"><span data-stu-id="57b23-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="57b23-122">Используйте логику повторных попыток hello отхода логику, рекомендуется, чтобы он не перегрузки hello базы данных SQL с повтором одновременно несколькими клиентами.</span><span class="sxs-lookup"><span data-stu-id="57b23-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="57b23-123">Примеры кода: образцы кода, иллюстрирующие логику повторных попыток, в разделе примеров для hello язык в: [библиотек подключений используется tooconnect tooAzure базы данных для MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="57b23-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="57b23-124">Управление подключениями</span><span class="sxs-lookup"><span data-stu-id="57b23-124">Managing Connections</span></span>
<span data-ttu-id="57b23-125">Подключения к базе данных являются ограниченным ресурсом, поэтому рекомендуется получить понятное использования подключений при доступе к базе данных MySQL tooachieve более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="57b23-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="57b23-126">База данных Access hello с использованием пулов соединений или постоянные подключения.</span><span class="sxs-lookup"><span data-stu-id="57b23-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="57b23-127">База данных hello доступ с помощью коротких подключения срока действия.</span><span class="sxs-lookup"><span data-stu-id="57b23-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="57b23-128">Используйте логику повторных попыток в приложении в момент hello попытки подключения hello, toocatch сбоев из-за tooconcurrent подключений достигли hello максимально допустимое.</span><span class="sxs-lookup"><span data-stu-id="57b23-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="57b23-129">В hello логику повторных попыток, задайте небольшую задержку и дождитесь случайное время до попытки hello дополнительные подключения.</span><span class="sxs-lookup"><span data-stu-id="57b23-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
