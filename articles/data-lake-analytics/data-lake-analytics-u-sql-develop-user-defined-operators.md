---
title: "Разработка определяемых пользователем операторов U-SQLU (UDO) | Документы Майкрософт"
description: "Узнайте, как разрабатывать определяемые пользователем операторы (с возможностью повторного использования) для заданий Data Lake Analytics. "
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
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="38b47-103">Разработка определяемых пользователем операторов U-SQLU (UDO)</span><span class="sxs-lookup"><span data-stu-id="38b47-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="38b47-104">Узнайте, как разрабатывать определяемые пользователем операторы для обработки данных в задании U-SQL.</span><span class="sxs-lookup"><span data-stu-id="38b47-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="38b47-105">Инструкции по разработке сборок общего назначения для U-SQL см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="38b47-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="38b47-106">Определение и использование определяемых пользователем операторов в U-SQL</span><span class="sxs-lookup"><span data-stu-id="38b47-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="38b47-107">**Создание и отправка задания U-SQL**</span><span class="sxs-lookup"><span data-stu-id="38b47-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="38b47-108">В Visual Studio выберите **Файл > Создать > Проект > Проект U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="38b47-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="38b47-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="38b47-109">Click **OK**.</span></span> <span data-ttu-id="38b47-110">Visual Studio создаст решение с помощью файла Script.usql.</span><span class="sxs-lookup"><span data-stu-id="38b47-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="38b47-111">В **обозревателе решений** разверните узел Script.usql и дважды щелкните файл **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="38b47-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="38b47-112">Скопируйте приведенный ниже код и вставьте его в файл.</span><span class="sxs-lookup"><span data-stu-id="38b47-112">Paste the following code into the file:</span></span>

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
6. <span data-ttu-id="38b47-113">Откройте файл **Script.usql** и вставьте следующий сценарий U-SQL:</span><span class="sxs-lookup"><span data-stu-id="38b47-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

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
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="38b47-114">Укажите учетную запись аналитики озера данных, базу данных и схему.</span><span class="sxs-lookup"><span data-stu-id="38b47-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="38b47-115">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Создать сценарий**.</span><span class="sxs-lookup"><span data-stu-id="38b47-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="38b47-116">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Отправить сценарий**.</span><span class="sxs-lookup"><span data-stu-id="38b47-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="38b47-117">Если вы еще не подключились к своей подписке Azure, вам будет предложено ввести учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="38b47-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="38b47-118">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="38b47-118">Click **Submit**.</span></span> <span data-ttu-id="38b47-119">Итоги отправки и ссылка на задание появятся в окне результатов, когда операция отправки будет завершена.</span><span class="sxs-lookup"><span data-stu-id="38b47-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="38b47-120">Чтобы увидеть последнее состояние задания, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="38b47-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="38b47-121">**Просмотр выходных данных**</span><span class="sxs-lookup"><span data-stu-id="38b47-121">**To see the output**</span></span>

1. <span data-ttu-id="38b47-122">В **обозревателе сервера** разверните узлы **Azure**, **Data Lake Analytics**, а также учетную запись Data Lake Analytics. Затем разверните узел **Учетные записи хранения**, щелкните хранилище по умолчанию правой кнопкой мыши и выберите **Обозреватель**.</span><span class="sxs-lookup"><span data-stu-id="38b47-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="38b47-123">Разверните узлы «Примеры» и «Выходные данные», а затем дважды щелкните **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="38b47-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="38b47-124">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="38b47-124">See also</span></span>
* [<span data-ttu-id="38b47-125">Приступая к работе с аналитикой озера данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b47-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="38b47-126">Приступая к работе с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="38b47-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="38b47-127">Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL</span><span class="sxs-lookup"><span data-stu-id="38b47-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
