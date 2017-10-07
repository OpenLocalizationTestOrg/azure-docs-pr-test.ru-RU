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
# <a name="develop-u-sql-user-defined-operators-udos"></a>Разработка определяемых пользователем операторов U-SQLU (UDO)
Узнайте, как toodevelop определяемые пользователем операторы tooprocess данных в задание U-SQL.

Инструкции по разработке сборок общего назначения для U-SQL см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Определение и использование определяемых пользователем операторов в U-SQL
**toocreate и отправить задание U-SQL**

1. Hello Visual Studio выберите **файл > Создать > проект > проект U-SQL**.
2. Нажмите кнопку **ОК**. Visual Studio создаст решение с помощью файла Script.usql.
3. В **обозревателе решений** разверните узел Script.usql и дважды щелкните файл **Script.usql.cs**.
4. Вставьте следующий код в файл hello hello:

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
6. Откройте **Script.usql**, и hello вставьте следующий скрипт U-SQL:

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
7. Укажите учетную запись аналитики Озера данных hello, базы данных и схемы.
8. В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Создать сценарий**.
9. В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Отправить сценарий**.
10. Если вы еще не подключены tooyour подписки Azure, будет иметь tooenter запрашиваемые учетные данные учетной записи Azure.
11. Нажмите кнопку **Submit**(Отправить). Отправка результатов и ссылку на задание доступны в окне "Результаты" hello после завершения отправки hello.
12. Щелкните hello **обновление** кнопку toosee hello последние задания состояния и обновить hello экрана.

**выходные данные toosee hello**

1. Из **обозревателя серверов**, разверните **Azure**, разверните **аналитики Озера данных**разверните учетной записи аналитики Озера данных, разверните **учетных записей хранилища**, щелкните правой кнопкой мыши hello хранилища по умолчанию и нажмите кнопку **Explorer**.
2. Разверните узлы «Примеры» и «Выходные данные», а затем дважды щелкните **Drivers.csv**.

## <a name="see-also"></a>Дополнительные материалы
* [Приступая к работе с аналитикой озера данных с помощью PowerShell](data-lake-analytics-get-started-powershell.md)
* [Приступая к работе с hello портал Azure с помощью аналитики Озера данных](data-lake-analytics-get-started-portal.md)
* [Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
