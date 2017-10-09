---
title: "решения aaaUse API-интерфейсов для пакета Azure и средств toodevelop крупномасштабных параллельной обработки | Документы Microsoft"
description: "Дополнительные сведения о hello API-интерфейсы и инструменты для разработки решений с hello пакетной службы Azure."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Общие сведения об API-интерфейсах и средствах пакетной службы

Обработка параллельных рабочих нагрузок с помощью пакетной службы Azure обычно выполняется программным образом с помощью одного из hello [API-интерфейсы пакета](#batch-development-apis). Клиентское приложение или служба можно использовать API-интерфейсы пакета toocommunicate hello с hello пакетной службы. С hello API-интерфейсы пакета, можно создавать и управлять пулами вычислительных узлов виртуальных машин или облачных служб. Можно запланировать выполнение заданий и задач, toorun на этих узлах. 

Можно эффективно обработать крупномасштабных рабочих нагрузок для вашей организации или предоставления службы интерфейса tooyour клиентов, чтобы их выполнения заданий и задач, — по требованию или по расписанию — на один, сотнями или даже тысячами узлов. Кроме того, пакетную службу Azure можно использовать как часть более крупного рабочего процесса под управлением таких средств, как [фабрика данных Azure](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Когда вы будете готовы toodig в toohello пакета API для более подробное представление о hello содержащая его предоставляет, ознакомьтесь с hello [пакета Обзор возможностей для разработчиков](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Учетные записи Azure для разработки с помощью пакетной службы
При разработке пакета решений, вы будете использовать hello следующие учетные записи в Microsoft Azure.

* **Учетная запись и подписка Azure.** Если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN][msdn_benefits] или зарегистрироваться для получения [бесплатной учетной записи Azure][free_account]. При создании учетной записи автоматически создается подписка по умолчанию.
* **Учетная запись пакетной службы** — это ресурсы пакетной службы Azure, в том числе пулы, вычислительные узлы, задания и задачи, связанные с учетной записью пакетной службы Azure. Когда приложение выполняет запрос к hello пакетной службы, проверяет подлинность запроса hello, используя имя учетной записи пакетной службы Azure hello, URL-адрес hello hello учетной записи и ключ доступа. Вы можете [создать учетную запись пакетной](batch-account-create-portal.md) в hello портал Azure.
* **Учетная запись хранения.** В пакетную службу встроена поддержка работы с файлами в [службе хранилища Azure][azure_storage]. Практически во всех пакетного сценария использует хранилище больших двоичных объектов Azure для промежуточных hello программы, которые запускаются задачами и hello данные, которые они обрабатывают, а также для хранения hello выходных данных, они создают. toocreate учетной записи хранения в разделе [учетных записей хранилища Azure о](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>API-интерфейсы пакетной службы

Вашим приложениям и службам может выдавать прямые вызовы API-интерфейса REST или использовать один или несколько следующих клиентских библиотек toorun hello и управлять рабочих нагрузок пакетной службы Azure.

| API | Справочник по API | Загрузить | Учебник | Примеры кода | Подробнее |
| --- | --- | --- | --- | --- | --- |
| **Пакетная служба (REST)** |[MSDN][batch_rest] |Недоступно |- |- | [Поддерживаемые версии](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Пакетная служба (.NET)** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Руководство](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Заметки о выпуске](http://aka.ms/batch-net-dataplane-changelog) |
| **Пакетная служба Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Руководство](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Файл сведений](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Node.js для пакетной службы** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Файл сведений](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Java для пакетной службы** |[github.io][api_java] |[Maven][api_java_jar] |- |[Файл сведений][api_sample_java] | [Файл сведений](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>API-интерфейсы для управления пакетной службой

Hello API диспетчера ресурсов Azure для пакета предоставляют программный доступ tooBatch учетные записи. С помощью этих API можно программно управлять учетными записями, квотами и пакетами приложений.  

| API | Справочник по API | Загрузить | Учебник | Примеры кода |
| --- | --- | --- | --- | --- |
| **REST диспетчера ресурсов пакетной службы** |[docs.microsoft.com][api_rest_mgmt] |Недоступно |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **.NET диспетчера ресурсов пакетной службы** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Руководство](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Программы командной строки пакетной службы

Эти средства командной строки представляют Привет же функциональные возможности, как hello пакетная служба и API-интерфейсов для пакета управления: 

* [Командлеты PowerShell пакета][batch_ps]: hello командлеты пакетной службы Azure в hello [Azure PowerShell](/powershell/azure/overview) модуль включить toomanage пакетными ресурсами с помощью PowerShell.
* [Azure CLI](/cli/azure/overview): hello Azure командной строки (CLI Azure) — это набор средств кросс платформенных, предоставляющий команды оболочки для взаимодействия с многие службы Azure, включая hello пакетной службы и службы управления пакета. В разделе [пакетное управление ресурсами с помощью Azure CLI](batch-cli-get-started.md) Дополнительные сведения об использовании hello Azure CLI с использованием пакета.

## <a name="other-tools-for-application-development"></a>Другие средства для разработки приложений

Ниже приведены дополнительные средства, которые можно использовать для создания и отладки приложений и служб пакетной службы.

* [Портал Azure][portal]: создание, мониторинг и удалить пулы, заданий и задач в hello Azure пакета портала пакета колонок. Можно просмотреть сведения о состоянии hello для этих и других ресурсов во время выполнения заданий и даже загружать файлы из hello вычислительных узлов в пулов. Например, при устранении неполадок можно скачать файл `stderr.txt` задачи, завершившейся сбоем. Можно также загрузить файлы удаленного рабочего стола (RDP), можно использовать toolog в toocompute узлов.
* [Azure обозреватель пакета][batch_explorer]: обозреватель пакета предоставляет аналогичные функциональные возможности управления ресурсами пакета как hello портал Azure, но в изолированной клиентское приложение Windows Presentation Foundation (WPF). Одно из приложений образец hello пакета .NET доступны на [GitHub][github_samples], можно построить с помощью Visual Studio 2015 или более поздней версии и использовать его toobrowse и управлять hello ресурсы в вашей учетной записи пакета во время разработки и отлаживать свои решения пакета. Просмотр заданий, пул и сведения о задаче, загрузка файлов из вычислительных узлов и toonodes удаленно подключиться с помощью удаленного рабочего стола (RDP) файлы, которые можно загрузить с помощью обозревателя пакета.
* [Обозреватель хранилищ Microsoft Azure][storage_explorer]: А не строго средство пакетной службы Azure, hello обозреватель хранилищ — другой toohave ценным инструментом, во время разработки и отладки пакета решения.

## <a name="additional-resources"></a>Дополнительные ресурсы

- toolearn о события ведения журнала из пакета приложения, в разделе [журнал событий для наблюдения за пакета решения и диагностики оценки](batch-diagnostics.md). Ссылка на события, вызванные hello пакетная служба, в разделе [пакета аналитики](batch-analytics.md).
- Сведения о переменных среды для вычислительных узлов см. в статье [Переменные среды вычислительного узла пакетной службы Azure](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Дальнейшие действия

* Чтение hello [пакета Обзор возможностей для разработчиков](batch-api-basics.md), важные сведения для тех, кто Подготовка toouse пакета. Hello статья содержит более подробные сведения о пакете службы ресурсы, такие как пулы, узлы, заданий и задач и hello множество функций API, которые можно использовать при создании пакета приложения.
* [Начало работы с библиотекой hello пакетной службы Azure для .NET](batch-dotnet-get-started.md) toolearn как toouse C# и hello tooexecute библиотеки .NET пакета простой рабочей нагрузки с помощью общих рабочего процесса пакета. В этой статье должно быть одним из вашего первого останавливается во время обучения как toouse hello пакетной службы. Имеется также [версию Python](batch-python-tutorial.md) hello учебника.
* Загрузите hello [код примеров на GitHub] [ github_samples] toosee, как C# и Python может взаимодействовать с пакета tooschedule и процесс образца рабочих нагрузок.
* Извлечение hello [план обучения пакета] [ learning_path] tooget представление о hello tooyou доступные ресурсы как можно узнать toowork с использованием пакета.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
