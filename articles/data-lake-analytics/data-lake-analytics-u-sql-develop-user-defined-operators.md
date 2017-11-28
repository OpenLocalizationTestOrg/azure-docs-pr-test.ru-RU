---
title: "определяемые пользователем операторы aaaDevelop U-SQL (определяемые пользователем операторы) | Документы Microsoft"
description: "Узнайте, как использовать toobe toodevelop определяемые пользователем операторы и повторно использовать в аналитике Озера данных задания. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="4e9fd-103">Разработка определяемых пользователем операторов U-SQLU (UDO)</span><span class="sxs-lookup"><span data-stu-id="4e9fd-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="4e9fd-104">Узнайте, как toodevelop определяемые пользователем операторы tooprocess данных в задание U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="4e9fd-105">Инструкции по разработке сборок общего назначения для U-SQL см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="4e9fd-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="4e9fd-106">Определение и использование определяемых пользователем операторов в U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e9fd-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="4e9fd-107">**toocreate и отправить задание U-SQL**</span><span class="sxs-lookup"><span data-stu-id="4e9fd-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="4e9fd-108">Hello Visual Studio выберите **файл > Создать > проект > проект U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="4e9fd-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-109">Click **OK**.</span></span> <span data-ttu-id="4e9fd-110">Visual Studio создаст решение с помощью файла Script.usql.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="4e9fd-111">В **обозревателе решений** разверните узел Script.usql и дважды щелкните файл **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="4e9fd-112">Вставьте следующий код в файл hello hello:</span><span class="sxs-lookup"><span data-stu-id="4e9fd-112">Paste hello following code into hello file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="4e9fd-113">Откройте **Script.usql**, и hello вставьте следующий скрипт U-SQL:</span><span class="sxs-lookup"><span data-stu-id="4e9fd-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="4e9fd-114">Укажите учетную запись аналитики Озера данных hello, базы данных и схемы.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="4e9fd-115">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Создать сценарий**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="4e9fd-116">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Отправить сценарий**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="4e9fd-117">Если вы еще не подключены tooyour подписки Azure, будет иметь tooenter запрашиваемые учетные данные учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="4e9fd-118">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="4e9fd-118">Click **Submit**.</span></span> <span data-ttu-id="4e9fd-119">Отправка результатов и ссылку на задание доступны в окне "Результаты" hello после завершения отправки hello.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="4e9fd-120">Щелкните hello **обновление** кнопку toosee hello последние задания состояния и обновить hello экрана.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="4e9fd-121">**выходные данные toosee hello**</span><span class="sxs-lookup"><span data-stu-id="4e9fd-121">**toosee hello output**</span></span>

1. <span data-ttu-id="4e9fd-122">Из **обозревателя серверов**, разверните **Azure**, разверните **аналитики Озера данных**разверните учетной записи аналитики Озера данных, разверните **учетных записей хранилища**, щелкните правой кнопкой мыши hello хранилища по умолчанию и нажмите кнопку **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="4e9fd-123">Разверните узлы «Примеры» и «Выходные данные», а затем дважды щелкните **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="4e9fd-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e9fd-124">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4e9fd-124">See also</span></span>
* [<span data-ttu-id="4e9fd-125">Приступая к работе с аналитикой озера данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e9fd-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="4e9fd-126">Приступая к работе с hello портал Azure с помощью аналитики Озера данных</span><span class="sxs-lookup"><span data-stu-id="4e9fd-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4e9fd-127">Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e9fd-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
