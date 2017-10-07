---
title: "заметки о выпуске aaaMicrosoft обозреватель хранилища Azure (Предварительная версия) | Документы Microsoft"
description: "Заметки о выпуске обозревателя службы хранилища Microsoft Azure (предварительная версия)."
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="cf041-103">Заметки о выпуске обозревателя службы хранилища Microsoft Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cf041-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="cf041-104">Эта статья содержит выпуска hello выпуске заметки обозреватель хранилищ Azure 0.8.16 (Предварительная версия), а также заметки о выпуске для предыдущих версий.</span><span class="sxs-lookup"><span data-stu-id="cf041-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="cf041-105">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](./vs-azure-tools-storage-manage-with-storage-explorer.md) имеет отдельное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="cf041-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="cf041-106">Версия 0.8.16 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cf041-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="cf041-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="cf041-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="cf041-108">Скачивание обозревателя службы хранилища Azure 0.8.16 (предварительная версия):</span><span class="sxs-lookup"><span data-stu-id="cf041-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- <span data-ttu-id="cf041-109">[Обозреватель службы хранилища Azure 0.8.16 (предварительная версия) для Windows](https://go.microsoft.com/fwlink/?LinkId=708343).</span><span class="sxs-lookup"><span data-stu-id="cf041-109">[Azure Storage Explorer 0.8.16 (Preview) for Windows](https://go.microsoft.com/fwlink/?LinkId=708343)</span></span>
- <span data-ttu-id="cf041-110">[Обозреватель служб хранилища Azure 0.8.16 (предварительная версия) для Mac](https://go.microsoft.com/fwlink/?LinkId=708342).</span><span class="sxs-lookup"><span data-stu-id="cf041-110">[Azure Storage Explorer 0.8.16 (Preview) for Mac](https://go.microsoft.com/fwlink/?LinkId=708342)</span></span>
- <span data-ttu-id="cf041-111">[Обозреватель служб хранилища Azure 0.8.16 (предварительная версия) для Linux](https://go.microsoft.com/fwlink/?LinkId=722418).</span><span class="sxs-lookup"><span data-stu-id="cf041-111">[Azure Storage Explorer 0.8.16 (Preview) for Linux](https://go.microsoft.com/fwlink/?LinkId=722418)</span></span>

### <a name="new"></a><span data-ttu-id="cf041-112">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-112">New</span></span>
* <span data-ttu-id="cf041-113">При открытии большого двоичного объекта, обозреватель хранилищ предложит tooupload hello загружен файл обнаружения изменения</span><span class="sxs-lookup"><span data-stu-id="cf041-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="cf041-114">Улучшена процедура входа в Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="cf041-115">Hello Улучшенная производительность передаче или загрузке множество небольших файлы hello же времени</span><span class="sxs-lookup"><span data-stu-id="cf041-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="cf041-116">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-116">Fixes</span></span>
* <span data-ttu-id="cf041-117">Для некоторых типов больших двоичных объектов выбор слишком «replace» при возникновении конфликта передачи иногда приведет передачи hello в процессе перезапуска.</span><span class="sxs-lookup"><span data-stu-id="cf041-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="cf041-118">В версии 0.8.15 процесс передачи мог остановиться на 99 %.</span><span class="sxs-lookup"><span data-stu-id="cf041-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="cf041-119">При передаче файлов tooa общую папку, если вы выбрали tooupload tooa каталог, который еще не существует, произойдет сбой передачи.</span><span class="sxs-lookup"><span data-stu-id="cf041-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="cf041-120">Обозреватель хранилищ неправильно создавал метки времени для подписанных URL-адресов и запросов к таблицам.</span><span class="sxs-lookup"><span data-stu-id="cf041-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="cf041-121">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-121">Known Issues</span></span>
* <span data-ttu-id="cf041-122">В настоящее время строка подключения с использованием имени и ключа не работает.</span><span class="sxs-lookup"><span data-stu-id="cf041-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="cf041-123">Он будет исправлена в следующем выпуске hello.</span><span class="sxs-lookup"><span data-stu-id="cf041-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="cf041-124">До этого времени вы можете использовать подключение с именем и ключом.</span><span class="sxs-lookup"><span data-stu-id="cf041-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="cf041-125">При попытке tooopen файла с недопустимым именем файла Windows, файл не найден Ошибка приведет к hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="cf041-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="cf041-126">После нажатия кнопки «Отмена» для задачи, она может занять некоторое время для этой задачи toocancel.</span><span class="sxs-lookup"><span data-stu-id="cf041-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="cf041-127">Это ограничение библиотеки hello узел хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cf041-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="cf041-128">После завершения передачи больших двоичных объектов, вкладку hello, инициированное hello передачи обновляются.</span><span class="sxs-lookup"><span data-stu-id="cf041-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="cf041-129">Это отличается от предыдущего поведения, а также вызовет вы toobe toohello корневого контейнера hello, находясь в выполнен переход.</span><span class="sxs-lookup"><span data-stu-id="cf041-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="cf041-130">При выборе hello не тот сертификат ПИН-кода или смарт-карты, то необходимо будет toorestart в порядке toohave обозреватель хранилищ забудете это решение.</span><span class="sxs-lookup"><span data-stu-id="cf041-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="cf041-131">Панель параметров Hello учетной записи может отображаться необходимые подписки toofilter tooreenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="cf041-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="cf041-132">При переименовании больших двоичных объектов (по отдельности или в переименованном контейнере больших двоичных объектов) не сохраняются моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="cf041-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="cf041-133">Все прочие свойства и метаданные больших двоичных объектов, файлов и сущностей при переименовании сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cf041-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="cf041-134">Несмотря на то, что сейчас Azure Stack не поддерживает общие файловые ресурсы, соответствующий узел все равно отображается под подключенной учетной записью хранения Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="cf041-135">Для пользователей на Ubuntu 14.04 потребуется tooensure GCC работает toodate – это можно сделать, запустив hello следующие команды, а затем перезапуск компьютера:</span><span class="sxs-lookup"><span data-stu-id="cf041-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="cf041-136">Для пользователей на Ubuntu 17.04 потребуется tooinstall GConf – это можно сделать hello следующие команды, а затем перезапуск компьютера под управлением:</span><span class="sxs-lookup"><span data-stu-id="cf041-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="cf041-137">Версия 0.8.14 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cf041-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="cf041-138">22.06.2017</span><span class="sxs-lookup"><span data-stu-id="cf041-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="cf041-139">Скачивание обозревателя службы хранилища Azure 0.8.14 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cf041-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="cf041-140">Скачивание обозревателя службы хранилища Azure 0.8.14 (предварительная версия) для Windows</span><span class="sxs-lookup"><span data-stu-id="cf041-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="cf041-141">Скачивание обозревателя службы хранилища Azure 0.8.14 (предварительная версия) для Mac</span><span class="sxs-lookup"><span data-stu-id="cf041-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="cf041-142">Скачивание обозревателя службы хранилища Azure 0.8.14 (предварительная версия) для Linux</span><span class="sxs-lookup"><span data-stu-id="cf041-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="cf041-143">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-143">New</span></span>

* <span data-ttu-id="cf041-144">Обновленный too1.7.2 электронные версии в порядке tootake преимуществами несколько критических обновлений</span><span class="sxs-lookup"><span data-stu-id="cf041-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="cf041-145">Теперь вы можете быстро просматривать электронного руководства по устранению неполадок hello из меню "Справка" hello</span><span class="sxs-lookup"><span data-stu-id="cf041-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="cf041-146">[Руководство][2] по устранению неполадок в обозревателе хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="cf041-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="cf041-147">[Инструкции] [ 3] о подключении подписки tooan стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf041-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="cf041-148">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-148">Known Issues</span></span>

* <span data-ttu-id="cf041-149">В диалоговом окне для подтверждения папку delete hello не регистрируют щелчками мыши hello в Linux.</span><span class="sxs-lookup"><span data-stu-id="cf041-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="cf041-150">Решение — клавишу ВВОД toouse hello</span><span class="sxs-lookup"><span data-stu-id="cf041-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="cf041-151">При выборе hello не тот сертификат ПИН-кода или смарт-карты, то необходимо будет toorestart в порядке toohave обозреватель хранилищ забудете hello принятия решений</span><span class="sxs-lookup"><span data-stu-id="cf041-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="cf041-152">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам</span><span class="sxs-lookup"><span data-stu-id="cf041-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="cf041-153">Панель параметров Hello учетной записи может отображать, необходимо иметь учетные данные tooreenter в порядке toofilter подписки</span><span class="sxs-lookup"><span data-stu-id="cf041-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="cf041-154">При переименовании больших двоичных объектов (по отдельности или в переименованном контейнере больших двоичных объектов) не сохраняются моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="cf041-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="cf041-155">Все прочие свойства и метаданные больших двоичных объектов, файлов и сущностей при переименовании сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cf041-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="cf041-156">Несмотря на то, что сейчас Azure Stack не поддерживает общие файловые ресурсы, соответствующий узел все равно отображается под подключенной учетной записью хранения Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="cf041-157">Ubuntu 14.04 потребности установки версии gcc обновления или обновления — tooupgrade действия приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="cf041-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="cf041-158">Предыдущие выпуски</span><span class="sxs-lookup"><span data-stu-id="cf041-158">Previous releases</span></span>

* [<span data-ttu-id="cf041-159">Версия 0.8.13</span><span class="sxs-lookup"><span data-stu-id="cf041-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="cf041-160">Версия 0.8.12, 0.8.11, 0.8.10</span><span class="sxs-lookup"><span data-stu-id="cf041-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="cf041-161">Версия 0.8.9, 0.8.8</span><span class="sxs-lookup"><span data-stu-id="cf041-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="cf041-162">Версия 0.8.7</span><span class="sxs-lookup"><span data-stu-id="cf041-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="cf041-163">Версия 0.8.6</span><span class="sxs-lookup"><span data-stu-id="cf041-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="cf041-164">Версия 0.8.5</span><span class="sxs-lookup"><span data-stu-id="cf041-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="cf041-165">Версия 0.8.4</span><span class="sxs-lookup"><span data-stu-id="cf041-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="cf041-166">Версия 0.8.3</span><span class="sxs-lookup"><span data-stu-id="cf041-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="cf041-167">Версия 0.8.2</span><span class="sxs-lookup"><span data-stu-id="cf041-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="cf041-168">Версия 0.8.0</span><span class="sxs-lookup"><span data-stu-id="cf041-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="cf041-169">Версия 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="cf041-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="cf041-170">Версия 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="cf041-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="cf041-171">Версия 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="cf041-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="cf041-172">Версия 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="cf041-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="cf041-173">Версия 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="cf041-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="cf041-174">Версия 0.8.13</span><span class="sxs-lookup"><span data-stu-id="cf041-174">Version 0.8.13</span></span>
<span data-ttu-id="cf041-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="cf041-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-176">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-176">New</span></span>

* <span data-ttu-id="cf041-177">[Руководство][2] по устранению неполадок в обозревателе хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="cf041-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="cf041-178">[Инструкции] [ 3] о подключении подписки tooan стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf041-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-179">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-179">Fixes</span></span>

* <span data-ttu-id="cf041-180">Исправлено: при отправке файлов с высокой вероятностью могла произойти ошибка нехватки памяти.</span><span class="sxs-lookup"><span data-stu-id="cf041-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="cf041-181">Исправлено: теперь можно входить с использованием ПИН-кода или смарт-карты.</span><span class="sxs-lookup"><span data-stu-id="cf041-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="cf041-182">Исправлено: функция "Открыть на портале" теперь работает в Azure для Китая, Германии, для государственных организаций США и в Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="cf041-183">Исправлена: При отправке BLOB-контейнере tooa папку, «Недопустимая операция» иногда возникнет ошибка</span><span class="sxs-lookup"><span data-stu-id="cf041-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="cf041-184">Исправлено: функция "Выбрать все" отключалась при управлении моментальными снимками.</span><span class="sxs-lookup"><span data-stu-id="cf041-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="cf041-185">Исправлена ошибка: hello метаданные базового BLOB-объекта hello могут получить перезаписаны после просмотра свойств hello моментальные снимки</span><span class="sxs-lookup"><span data-stu-id="cf041-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-186">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-186">Known Issues</span></span>

* <span data-ttu-id="cf041-187">При выборе hello не тот сертификат ПИН-кода или смарт-карты, то необходимо будет toorestart в порядке toohave обозреватель хранилищ забудете hello принятия решений</span><span class="sxs-lookup"><span data-stu-id="cf041-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="cf041-188">При увеличении in или out, уровень масштаба hello моментально может привести к сбросу toohello уровень по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cf041-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="cf041-189">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам</span><span class="sxs-lookup"><span data-stu-id="cf041-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="cf041-190">Панель параметров Hello учетной записи может отображать, необходимо иметь учетные данные tooreenter в порядке toofilter подписки</span><span class="sxs-lookup"><span data-stu-id="cf041-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="cf041-191">При переименовании больших двоичных объектов (по отдельности или в переименованном контейнере больших двоичных объектов) не сохраняются моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="cf041-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="cf041-192">Все прочие свойства и метаданные больших двоичных объектов, файлов и сущностей при переименовании сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cf041-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="cf041-193">Несмотря на то, что сейчас Azure Stack не поддерживает общие файловые ресурсы, соответствующий узел все равно отображается под подключенной учетной записью хранения Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="cf041-194">Ubuntu 14.04 потребности установки версии gcc обновления или обновления — tooupgrade действия приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="cf041-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="cf041-195">Версия 0.8.12, 0.8.11, 0.8.10</span><span class="sxs-lookup"><span data-stu-id="cf041-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="cf041-196">07.04.2017</span><span class="sxs-lookup"><span data-stu-id="cf041-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-197">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-197">New</span></span>

* <span data-ttu-id="cf041-198">Обозреватель хранилищ автоматически завершается при установке обновления с уведомлением об обновлении hello</span><span class="sxs-lookup"><span data-stu-id="cf041-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="cf041-199">Быстрый доступ обеспечивает дополнительные возможности для работы с часто используемыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="cf041-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="cf041-200">В редакторе контейнер больших двоичных объектов hello теперь можно увидеть арендованного BLOB-объекта принадлежит виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cf041-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="cf041-201">Теперь можно свернуть hello левой панели</span><span class="sxs-lookup"><span data-stu-id="cf041-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="cf041-202">Обнаружение теперь запускается на hello же время загрузки</span><span class="sxs-lookup"><span data-stu-id="cf041-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="cf041-203">Использовать статистику в контейнер больших двоичных объектов, общей папки и таблица редакторы toosee hello размер ресурса или выбор hello</span><span class="sxs-lookup"><span data-stu-id="cf041-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="cf041-204">Теперь можно tooAzure входа в Active Directory (AAD) на основе учетных записей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="cf041-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="cf041-205">После этого можно архив передачи файлов учетных записей хранилища для более чем 32 МБ tooPremium</span><span class="sxs-lookup"><span data-stu-id="cf041-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="cf041-206">Улучшена поддержка специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="cf041-206">Improved accessibility support</span></span>
* <span data-ttu-id="cf041-207">Теперь можно добавить надежных Base-64 SSL-сертификатов X.509 в кодировке с переходом tooEdit -&gt; сертификаты SSL -&gt; импорта сертификатов</span><span class="sxs-lookup"><span data-stu-id="cf041-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-208">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-208">Fixes</span></span>

* <span data-ttu-id="cf041-209">Исправлена ошибка: после обновления учетных данных учетной записи, представление в виде дерева hello бы иногда не обновляется автоматически</span><span class="sxs-lookup"><span data-stu-id="cf041-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="cf041-210">Исправлено: при создании SAS для очередей и таблиц эмулятора приводило к тому, что URL-адрес становился недопустимым.</span><span class="sxs-lookup"><span data-stu-id="cf041-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="cf041-211">Исправлено: учетные записи хранения уровня Premium можно развернуть, пока включен прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="cf041-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="cf041-212">Исправлена: hello "Применить" на учетные записи hello, страница управления не будет работать, если был выбран 1 или 0 учетных записей</span><span class="sxs-lookup"><span data-stu-id="cf041-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="cf041-213">Исправлено (в версии 0.8.11): происходил сбой при отправке больших двоичных объектов, требующих разрешения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="cf041-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="cf041-214">Исправлено (в версии 0.8.12): отправка отзывов не работала в версии 0.8.11.</span><span class="sxs-lookup"><span data-stu-id="cf041-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="cf041-215">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-215">Known Issues</span></span>

* <span data-ttu-id="cf041-216">После обновления too0.8.10, необходимо будет toorefresh все свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="cf041-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="cf041-217">При увеличении in или out, уровень масштаба hello моментально может привести к сбросу toohello уровень по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf041-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="cf041-218">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="cf041-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="cf041-219">Панель параметров Hello учетной записи может отображать, необходимо иметь учетные данные tooreenter в порядке toofilter подписки.</span><span class="sxs-lookup"><span data-stu-id="cf041-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="cf041-220">При переименовании больших двоичных объектов (по отдельности или в переименованном контейнере больших двоичных объектов) не сохраняются моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="cf041-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="cf041-221">Все прочие свойства и метаданные больших двоичных объектов, файлов и сущностей при переименовании сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cf041-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="cf041-222">Несмотря на то, что сейчас Azure Stack не поддерживает общие файловые ресурсы, соответствующий узел все равно отображается под подключенной учетной записью хранения Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cf041-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="cf041-223">Ubuntu 14.04 потребности установки версии gcc обновления или обновления — tooupgrade действия приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="cf041-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="cf041-224">Версия 0.8.9, 0.8.8</span><span class="sxs-lookup"><span data-stu-id="cf041-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="cf041-225">23.02.2017</span><span class="sxs-lookup"><span data-stu-id="cf041-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="cf041-226">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-226">New</span></span>

* <span data-ttu-id="cf041-227">Обозреватель хранилищ 0.8.9 автоматически загрузит hello последнюю версию обновления.</span><span class="sxs-lookup"><span data-stu-id="cf041-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="cf041-228">Исправление: с помощью портала создан tooattach универсальный код Ресурса SAS, учетной записи хранилища приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="cf041-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="cf041-229">Теперь можно создавать и повышать уровень моментальные снимков больших двоичных объектов, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="cf041-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="cf041-230">Теперь вы можете войти в учетные записи tooAzure Китая, Германия Azure и правительства США.</span><span class="sxs-lookup"><span data-stu-id="cf041-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="cf041-231">Теперь можно изменить уровень масштаба hello.</span><span class="sxs-lookup"><span data-stu-id="cf041-231">You can now change hello zoom level.</span></span> <span data-ttu-id="cf041-232">Используйте параметры hello tooZoom меню представления hello в уменьшить масштаб и сбросить масштаб.</span><span class="sxs-lookup"><span data-stu-id="cf041-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="cf041-233">Символы Юникода поддерживаются в метаданных пользователя для больших двоичных объектов и файлов.</span><span class="sxs-lookup"><span data-stu-id="cf041-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="cf041-234">Улучшены специальные возможности.</span><span class="sxs-lookup"><span data-stu-id="cf041-234">Accessibility improvements.</span></span>
* <span data-ttu-id="cf041-235">заметки о выпуске следующей версии Hello можно просмотреть в уведомление об обновлении hello.</span><span class="sxs-lookup"><span data-stu-id="cf041-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="cf041-236">Можно также просмотреть hello заметки о текущем выпуске из меню "Справка" hello.</span><span class="sxs-lookup"><span data-stu-id="cf041-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-237">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-237">Fixes</span></span>

* <span data-ttu-id="cf041-238">Исправлена ошибка: номер версии hello теперь правильно отображается на панели управления в Windows</span><span class="sxs-lookup"><span data-stu-id="cf041-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="cf041-239">Исправлена: поиска больше не является ограниченной too50, 000 узлов</span><span class="sxs-lookup"><span data-stu-id="cf041-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="cf041-240">Исправлена ошибка: Отправка tooa общей папки выполнения навсегда. Если hello целевой каталог еще не существует</span><span class="sxs-lookup"><span data-stu-id="cf041-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="cf041-241">Исправлено: повышена стабильность при длительной передаче и скачивании.</span><span class="sxs-lookup"><span data-stu-id="cf041-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-242">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-242">Known Issues</span></span>

* <span data-ttu-id="cf041-243">При увеличении in или out, уровень масштаба hello моментально может привести к сбросу toohello уровень по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf041-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="cf041-244">Быстрый доступ работает только с элементами подписки.</span><span class="sxs-lookup"><span data-stu-id="cf041-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="cf041-245">В этом выпуске не поддерживаются локальные ресурсы или ресурсы, подключенные с помощью ключа или маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="cf041-246">Может потребоваться несколько секунд toonavigate toohello целевой ресурс, в зависимости от количества ресурсов, у вас есть быстрый доступ.</span><span class="sxs-lookup"><span data-stu-id="cf041-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="cf041-247">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="cf041-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="cf041-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="cf041-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="cf041-249">Версия 0.8.7</span><span class="sxs-lookup"><span data-stu-id="cf041-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="cf041-250">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-250">New</span></span>

* <span data-ttu-id="cf041-251">Можно выбрать как конфликты tooresolve hello начала операции обновления, загрузите или скопируйте сеанса в окне действия hello</span><span class="sxs-lookup"><span data-stu-id="cf041-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="cf041-252">Наведите указатель мыши на вкладку toosee hello полный путь к ресурсу хранилища hello</span><span class="sxs-lookup"><span data-stu-id="cf041-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="cf041-253">При нажатии кнопки на вкладке, выполняет синхронизацию с расположением в левой части панели навигации hello</span><span class="sxs-lookup"><span data-stu-id="cf041-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-254">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-254">Fixes</span></span>

* <span data-ttu-id="cf041-255">Исправлено: обозреватель хранилищ теперь относится к доверенным приложениям в Mac.</span><span class="sxs-lookup"><span data-stu-id="cf041-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="cf041-256">Исправлено: ОС Ubuntu 14.04 снова поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cf041-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="cf041-257">Исправлена ошибка: Иногда hello добавьте учетную запись, пользовательский Интерфейс отображается при загрузке подписок</span><span class="sxs-lookup"><span data-stu-id="cf041-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="cf041-258">Исправлена ошибка: Иногда не все ресурсы хранения перечисленные в левой части панели навигации hello</span><span class="sxs-lookup"><span data-stu-id="cf041-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="cf041-259">Исправлена ошибка: hello области действий в некоторых случаях отображаются пустые действия</span><span class="sxs-lookup"><span data-stu-id="cf041-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="cf041-260">Исправлена ошибка: размер окна hello из сеанса hello закрыт в последний раз теперь сохраняется</span><span class="sxs-lookup"><span data-stu-id="cf041-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="cf041-261">Исправлена: Можно открыть несколько вкладок для hello одного ресурса, с помощью контекстного меню hello</span><span class="sxs-lookup"><span data-stu-id="cf041-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-262">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-262">Known Issues</span></span>

* <span data-ttu-id="cf041-263">Быстрый доступ работает только с элементами подписки.</span><span class="sxs-lookup"><span data-stu-id="cf041-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="cf041-264">В этом выпуске не поддерживаются локальные ресурсы или ресурсы, подключенные с помощью ключа или маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="cf041-265">Быстрый доступ может занять несколько секунд toonavigate toohello целевой ресурс, в зависимости от количества ресурсов, у вас есть</span><span class="sxs-lookup"><span data-stu-id="cf041-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="cf041-266">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам</span><span class="sxs-lookup"><span data-stu-id="cf041-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="cf041-267">Служба поиска обрабатывает поисковые запросы приблизительно по 50 000 узлам. После достижения этого порога может снизиться производительность или могут возникать необработанные исключения.</span><span class="sxs-lookup"><span data-stu-id="cf041-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="cf041-268">Для hello первый раз, используя hello обозреватель хранилищ на macOS, может появиться несколько запросов, запрашивает разрешение пользователя tooaccess-цепочке ключей.</span><span class="sxs-lookup"><span data-stu-id="cf041-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="cf041-269">Мы рекомендуем выбрать всегда разрешать, строка hello не будет отображаться еще раз</span><span class="sxs-lookup"><span data-stu-id="cf041-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="cf041-270">18.11.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="cf041-271">Версия 0.8.6</span><span class="sxs-lookup"><span data-stu-id="cf041-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-272">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-272">New</span></span>

* <span data-ttu-id="cf041-273">После этого можно ПИН-код чаще всего используются службы toohello быстрого доступа для упрощения перемещения</span><span class="sxs-lookup"><span data-stu-id="cf041-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="cf041-274">Теперь можно открыть несколько редакторов на разных вкладках.</span><span class="sxs-lookup"><span data-stu-id="cf041-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="cf041-275">Одним щелчком tooopen временные вкладки. Дважды щелкните tooopen постоянные вкладки. Можно также щелкнуть на toomake временные вкладку hello его постоянные вкладки</span><span class="sxs-lookup"><span data-stu-id="cf041-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="cf041-276">Значительное улучшение производительности и стабильности при передаче и скачивании, особенно заметное для больших файлов на быстрых компьютерах.</span><span class="sxs-lookup"><span data-stu-id="cf041-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="cf041-277">Теперь в контейнерах больших двоичных объектов можно создавать пустые "виртуальные" папки.</span><span class="sxs-lookup"><span data-stu-id="cf041-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="cf041-278">Мы повторно представляем поиск в заданных областях с расширенным поиском в подстроках. Теперь у вас есть два варианта поиска:</span><span class="sxs-lookup"><span data-stu-id="cf041-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="cf041-279">Глобальный поиск - просто введите условие поиска в текстовое поле поиска hello</span><span class="sxs-lookup"><span data-stu-id="cf041-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="cf041-280">Области поиска - щелкните hello лупы значок Далее tooa узел, сложите поиска термина toohello конец hello пути, или щелкните правой кнопкой мыши и выберите «Поиска из сюда»</span><span class="sxs-lookup"><span data-stu-id="cf041-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="cf041-281">Мы добавили различные темы: "Светлая" (по умолчанию), "Темная", "Высокая контрастность черного" и "Высокая контрастность белого".</span><span class="sxs-lookup"><span data-stu-id="cf041-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="cf041-282">Go tooEdit -&gt; toochange темы предпочтения использования тем</span><span class="sxs-lookup"><span data-stu-id="cf041-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="cf041-283">Вы можете изменять свойства больших двоичных объектов и файлов.</span><span class="sxs-lookup"><span data-stu-id="cf041-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="cf041-284">Добавлена поддержка кодированных (base64) и не кодированных сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="cf041-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="cf041-285">В среде Linux теперь является обязательной 64-разрядная операционная система.</span><span class="sxs-lookup"><span data-stu-id="cf041-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="cf041-286">Для этого выпуска поддерживается только 64-разрядная Ubuntu 16.04.1 LTS.</span><span class="sxs-lookup"><span data-stu-id="cf041-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="cf041-287">Мы обновили наш логотип!</span><span class="sxs-lookup"><span data-stu-id="cf041-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-288">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-288">Fixes</span></span>

* <span data-ttu-id="cf041-289">Исправлено. Проблема с блокированием экрана.</span><span class="sxs-lookup"><span data-stu-id="cf041-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="cf041-290">Исправлен. Усилена безопасность.</span><span class="sxs-lookup"><span data-stu-id="cf041-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="cf041-291">Исправлено: иногда возникали повторяющиеся подключенные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="cf041-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="cf041-292">Исправлено: большой двоичный объект с содержимым неопределенного типа мог создать исключение.</span><span class="sxs-lookup"><span data-stu-id="cf041-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="cf041-293">Исправлена ошибка: Hello открытия панели запроса для пустой таблицы не удалось</span><span class="sxs-lookup"><span data-stu-id="cf041-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="cf041-294">Исправлено: различные ошибок в поиске.</span><span class="sxs-lookup"><span data-stu-id="cf041-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="cf041-295">Исправлена ошибка: Увеличение hello количество ресурсов, загруженного из 50 too100 при нажатии кнопки «Более нагрузки»</span><span class="sxs-lookup"><span data-stu-id="cf041-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="cf041-296">Исправлено: если при первом запуске выполнен вход в учетную запись, выбираются все подписки для этой учетной записи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf041-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="cf041-297">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-297">Known Issues</span></span>

* <span data-ttu-id="cf041-298">Этот выпуск hello обозреватель хранилища не может быть запущена Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="cf041-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="cf041-299">tooopen несколько вкладок для одного ресурса, а не непрерывно щелкните hello hello того же ресурса.</span><span class="sxs-lookup"><span data-stu-id="cf041-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="cf041-300">Щелкните на другой ресурс и затем вернитесь на исходный ресурс tooopen hello повторно щелкните его на другой вкладке</span><span class="sxs-lookup"><span data-stu-id="cf041-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="cf041-301">Быстрый доступ работает только с элементами подписки.</span><span class="sxs-lookup"><span data-stu-id="cf041-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="cf041-302">В этом выпуске не поддерживаются локальные ресурсы или ресурсы, подключенные с помощью ключа или маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="cf041-303">Быстрый доступ может занять несколько секунд toonavigate toohello целевой ресурс, в зависимости от количества ресурсов, у вас есть</span><span class="sxs-lookup"><span data-stu-id="cf041-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="cf041-304">Более 3 групп BLOB-объектов или файлов, отправка в hello же время может привести к ошибкам</span><span class="sxs-lookup"><span data-stu-id="cf041-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="cf041-305">Служба поиска обрабатывает поисковые запросы приблизительно по 50 000 узлам. После достижения этого порога может снизиться производительность или могут возникать необработанные исключения.</span><span class="sxs-lookup"><span data-stu-id="cf041-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="cf041-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="cf041-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="cf041-307">Версия 0.8.5</span><span class="sxs-lookup"><span data-stu-id="cf041-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-308">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-308">New</span></span>

* <span data-ttu-id="cf041-309">Могут теперь использовать SAS создается портал ключей tooattach tooStorage учетных записей и ресурсов</span><span class="sxs-lookup"><span data-stu-id="cf041-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-310">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-310">Fixes</span></span>

* <span data-ttu-id="cf041-311">Исправлена: состязания во время поиска иногда вызвал-расширяемый toobecome узлов</span><span class="sxs-lookup"><span data-stu-id="cf041-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="cf041-312">Исправлена ошибка: «Использовать HTTP» не работает при подключении tooStorage учетных записей имя учетной записи и ключа</span><span class="sxs-lookup"><span data-stu-id="cf041-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="cf041-313">Исправлено: ключи SAS (созданные на портале) возвращали ошибку с сообщением о косой черте в конце.</span><span class="sxs-lookup"><span data-stu-id="cf041-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="cf041-314">Исправлено: ошибки импорта таблиц.</span><span class="sxs-lookup"><span data-stu-id="cf041-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="cf041-315">Иногда ключ раздела и строки стояли в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="cf041-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="cf041-316">Не удается tooread ключи разделов «null»</span><span class="sxs-lookup"><span data-stu-id="cf041-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-317">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-317">Known Issues</span></span>

* <span data-ttu-id="cf041-318">Служба поиска обрабатывает поисковые запросы приблизительно по 50 000 узлам. После достижения этого порога может снизиться производительность.</span><span class="sxs-lookup"><span data-stu-id="cf041-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="cf041-319">Стек Azure сейчас не поддерживает файлы, поэтому попытка tooexpand файлов выводится сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="cf041-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="cf041-320">12.09.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="cf041-321">Версия 0.8.4</span><span class="sxs-lookup"><span data-stu-id="cf041-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="cf041-322">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-322">New</span></span>

* <span data-ttu-id="cf041-323">Создание учетных записей toostorage прямых ссылок, контейнеры, очереди, таблицы или общие папки для общего доступа и простой доступ к ресурсам tooyour - Windows и Mac OS поддерживают</span><span class="sxs-lookup"><span data-stu-id="cf041-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="cf041-324">Поиск контейнеров больших двоичных объектов, таблиц, очередей, общих папок или учетных записей хранения в поле поиска hello</span><span class="sxs-lookup"><span data-stu-id="cf041-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="cf041-325">Теперь можно группировать предложения в построителе запросов hello таблицы</span><span class="sxs-lookup"><span data-stu-id="cf041-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="cf041-326">Переименовывайте, копируйте и вставляйте контейнеры и папки больших двоичных объектов, общие файловые ресурсы, таблицы, большие двоичные объекты, файлы и каталоги из учетных записей и контейнеров, подключенных с использованием SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="cf041-327">Теперь при переименовывании и копировании контейнеров больших двоичных объектов и общих файловых ресурсов сохраняются свойства и метаданные.</span><span class="sxs-lookup"><span data-stu-id="cf041-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-328">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-328">Fixes</span></span>

* <span data-ttu-id="cf041-329">Исправлено: отсутствовала возможность изменения сущностей таблицы с логическими или двоичными свойствами.</span><span class="sxs-lookup"><span data-stu-id="cf041-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-330">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-330">Known Issues</span></span>

* <span data-ttu-id="cf041-331">Служба поиска обрабатывает поисковые запросы приблизительно по 50 000 узлам. После достижения этого порога может снизиться производительность.</span><span class="sxs-lookup"><span data-stu-id="cf041-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="cf041-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="cf041-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="cf041-333">Версия 0.8.3</span><span class="sxs-lookup"><span data-stu-id="cf041-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="cf041-334">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-334">New</span></span>

* <span data-ttu-id="cf041-335">Переименование контейнеров, таблиц, файловых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cf041-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="cf041-336">Улучшена работа с конструктором запросов.</span><span class="sxs-lookup"><span data-stu-id="cf041-336">Improved Query builder experience</span></span>
* <span data-ttu-id="cf041-337">Возможность toosave и загрузка запросов</span><span class="sxs-lookup"><span data-stu-id="cf041-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="cf041-338">Прямой ссылки toostorage учетных записей или контейнеры, очередей, таблиц, также к общим папкам для обмена данными и легко доступ к ресурсам (только для Windows - macOS поддерживают ожидается в ближайшее время!)</span><span class="sxs-lookup"><span data-stu-id="cf041-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="cf041-339">Возможность toomanage и настройка правил CORS</span><span class="sxs-lookup"><span data-stu-id="cf041-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-340">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-340">Fixes</span></span>

* <span data-ttu-id="cf041-341">Исправлено: учетные записи Майкрософт требуют повторной аутентификации каждые 8–12 часов.</span><span class="sxs-lookup"><span data-stu-id="cf041-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-342">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-342">Known Issues</span></span>

* <span data-ttu-id="cf041-343">Иногда hello пользовательского интерфейса может казаться зависшим — максимальное увеличение окна hello помогает устранить эту проблему</span><span class="sxs-lookup"><span data-stu-id="cf041-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="cf041-344">Для установки macOS может потребоваться повышенный уровень разрешений.</span><span class="sxs-lookup"><span data-stu-id="cf041-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="cf041-345">Панель параметров учетной записи может показать, что вам необходимы учетные данные tooreenter в порядке toofilter подписки</span><span class="sxs-lookup"><span data-stu-id="cf041-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="cf041-346">Переименование файловых ресурсов, контейнеров больших двоичных объектов и таблиц не сохраняет метаданные или другие свойства в контейнере hello, такие как квоты для общей папки, общего доступа на уровне или политики доступа</span><span class="sxs-lookup"><span data-stu-id="cf041-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="cf041-347">При переименовании больших двоичных объектов (по отдельности или в переименованном контейнере больших двоичных объектов) не сохраняются моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="cf041-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="cf041-348">Все прочие свойства и метаданные больших двоичных объектов, файлов и сущностей при переименовании сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cf041-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="cf041-349">Копирование и переименование ресурсов не работает в учетных записях, подключенных с использованием SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="cf041-350">07.07.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="cf041-351">Версия 0.8.2</span><span class="sxs-lookup"><span data-stu-id="cf041-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="cf041-352">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-352">New</span></span>

* <span data-ttu-id="cf041-353">Учетные записи хранения группируются по подпискам. Хранилище разработки и ресурсы, подключенные с использованием ключа или SAS, отображаются в узле (локальном и подключенном).</span><span class="sxs-lookup"><span data-stu-id="cf041-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="cf041-354">Выход из учетных записей осуществляется на панели Azure Account Settings (Параметры учетной записи Azure).</span><span class="sxs-lookup"><span data-stu-id="cf041-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="cf041-355">Настройка tooenable параметры прокси-сервера и управление вход</span><span class="sxs-lookup"><span data-stu-id="cf041-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="cf041-356">Создавайте и прерывайте аренду большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="cf041-356">Create and break blob leases</span></span>
* <span data-ttu-id="cf041-357">Открывайте контейнеры больших двоичных объектов, очереди, таблицы и файлы одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="cf041-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-358">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-358">Fixes</span></span>

* <span data-ttu-id="cf041-359">Исправлено: декодировка (base64) сообщений очереди, вставленных с помощью библиотек .NET или Java, выполнялась неправильно.</span><span class="sxs-lookup"><span data-stu-id="cf041-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="cf041-360">Исправлено: таблицы $metrics не отображались для учетных записей хранения больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf041-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="cf041-361">Исправлено: узел таблицы не работает в локальном хранилище (разработка).</span><span class="sxs-lookup"><span data-stu-id="cf041-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-362">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-362">Known Issues</span></span>

* <span data-ttu-id="cf041-363">Для установки macOS может потребоваться повышенный уровень разрешений.</span><span class="sxs-lookup"><span data-stu-id="cf041-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="cf041-364">15.06.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="cf041-365">Версия 0.8.0</span><span class="sxs-lookup"><span data-stu-id="cf041-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="cf041-366">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-366">New</span></span>

* <span data-ttu-id="cf041-367">Поддержка общих файловых ресурсов: просмотр, передача, скачивание, копирование файлов, каталогов и URI SAS (создание и подключение).</span><span class="sxs-lookup"><span data-stu-id="cf041-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="cf041-368">Улучшенное взаимодействие с пользователями для подключения tooStorage с SAS URI или ключи учетной записи</span><span class="sxs-lookup"><span data-stu-id="cf041-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="cf041-369">Экспорт результатов запросов таблицы.</span><span class="sxs-lookup"><span data-stu-id="cf041-369">Export table query results</span></span>
* <span data-ttu-id="cf041-370">Изменение порядка и настройка столбцов таблицы.</span><span class="sxs-lookup"><span data-stu-id="cf041-370">Table column reordering and customization</span></span>
* <span data-ttu-id="cf041-371">Просмотр контейнеров больших двоичных объектов $logs и таблиц $metrics для учетных записей хранения с включенными метриками.</span><span class="sxs-lookup"><span data-stu-id="cf041-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="cf041-372">Улучшен экспорт и импорт (теперь включает тип значения свойства).</span><span class="sxs-lookup"><span data-stu-id="cf041-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-373">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-373">Fixes</span></span>

* <span data-ttu-id="cf041-374">Исправлено: передаются или скачиваются не все большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="cf041-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="cf041-375">Исправлена ошибка: изменения, добавив или импортировав сущности со значением числовую строку («1») преобразует его toodouble</span><span class="sxs-lookup"><span data-stu-id="cf041-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="cf041-376">Исправлена ошибка: Не удается tooexpand hello узла таблицы hello локальной среде разработки</span><span class="sxs-lookup"><span data-stu-id="cf041-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-377">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-377">Known Issues</span></span>

* <span data-ttu-id="cf041-378">Таблицы $metrics не отображаются для учетных записей хранения больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf041-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="cf041-379">Программно добавлены в очередь сообщения могут неправильно отображаться Если hello сообщения должны кодироваться с использованием кодировки Base64</span><span class="sxs-lookup"><span data-stu-id="cf041-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="cf041-380">17.05.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="cf041-381">Версия 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="cf041-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-382">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-382">New</span></span>

* <span data-ttu-id="cf041-383">Улучшена обработка ошибок при сбое приложения.</span><span class="sxs-lookup"><span data-stu-id="cf041-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-384">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-384">Fixes</span></span>

* <span data-ttu-id="cf041-385">Исправлена ошибка, при возникновении которой иногда при запросе учетных данных для входа на информационной панели не появляются сообщения.</span><span class="sxs-lookup"><span data-stu-id="cf041-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-386">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-386">Known Issues</span></span>

* <span data-ttu-id="cf041-387">Таблицы: Добавление, изменение, или импорт сущность имеет свойство с неоднозначно числовое значение, например «1» или «1.0», и hello toosend пользователь пытается его как `Edm.String`, hello станет через клиент hello API как Edm.Double</span><span class="sxs-lookup"><span data-stu-id="cf041-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="cf041-388">31.03.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="cf041-389">Версия 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="cf041-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="cf041-390">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-390">New</span></span>

* <span data-ttu-id="cf041-391">Поддержка таблиц: просмотр, поиск, экспорт, импорт и выполнение операций CRUD для сущностей.</span><span class="sxs-lookup"><span data-stu-id="cf041-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="cf041-392">Поддержка очередей: просмотр, добавление, вывод сообщений из очереди.</span><span class="sxs-lookup"><span data-stu-id="cf041-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="cf041-393">Создание URI SAS для учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="cf041-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="cf041-394">Соединение tooStorage учетных записей с URI SAS</span><span class="sxs-lookup"><span data-stu-id="cf041-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="cf041-395">Уведомления об обновлениях для будущих обновлений tooStorage обозревателя</span><span class="sxs-lookup"><span data-stu-id="cf041-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="cf041-396">Обновленный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="cf041-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-397">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-397">Fixes</span></span>

* <span data-ttu-id="cf041-398">Улучшения производительности и надежности.</span><span class="sxs-lookup"><span data-stu-id="cf041-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="cf041-399">Известные проблемы и способы их устранения</span><span class="sxs-lookup"><span data-stu-id="cf041-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="cf041-400">Скачивание больших файлов большого двоичного объекта выполняется неправильно. Мы рекомендуем использовать AzCopy, пока мы не устраним эту проблему.</span><span class="sxs-lookup"><span data-stu-id="cf041-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="cf041-401">Учетные данные учетной записи будет не получены или если домашняя папка hello не найден или не может быть записан в кэше</span><span class="sxs-lookup"><span data-stu-id="cf041-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="cf041-402">Если мы Добавление, изменение и импорт сущность имеет свойство с неоднозначно числовое значение, например «1» или «1.0», и пользователь hello пытается toosend его как `Edm.String`, hello станет через клиент hello API как Edm.Double</span><span class="sxs-lookup"><span data-stu-id="cf041-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="cf041-403">При импорте CSV-файлы с многострочных записей, может получить жесткому hello данных или шифрованных</span><span class="sxs-lookup"><span data-stu-id="cf041-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="cf041-404">03.02.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="cf041-405">Версия 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="cf041-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-406">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-406">Fixes</span></span>

* <span data-ttu-id="cf041-407">Улучшена производительность при передаче, скачивании и копировании больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf041-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="cf041-408">14.01.2016</span><span class="sxs-lookup"><span data-stu-id="cf041-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="cf041-409">Версия 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="cf041-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-410">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-410">New</span></span>

* <span data-ttu-id="cf041-411">Поддержка Linux (tooOSX функции четности)</span><span class="sxs-lookup"><span data-stu-id="cf041-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="cf041-412">Добавление контейнеров больших двоичных объектов с использованием подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="cf041-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="cf041-413">Добавление учетных записей хранения в Azure для Китая.</span><span class="sxs-lookup"><span data-stu-id="cf041-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="cf041-414">Добавление учетные записей хранения с применением пользовательских конечных точек.</span><span class="sxs-lookup"><span data-stu-id="cf041-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="cf041-415">Открыть и просмотреть hello содержимое текста и рисунка больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cf041-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="cf041-416">Просмотр и изменение свойств и метаданных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf041-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="cf041-417">Исправления</span><span class="sxs-lookup"><span data-stu-id="cf041-417">Fixes</span></span>

* <span data-ttu-id="cf041-418">Исправлена: отправка или загрузка большое количество больших двоичных объектов (500 +) может иногда вызвать toohave приложения hello белый экран</span><span class="sxs-lookup"><span data-stu-id="cf041-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="cf041-419">Исправлена ошибка: при задании уровня общего доступа контейнера больших двоичных объектов, новое значение hello не обновляется только если повторно задать фокус hello в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="cf041-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="cf041-420">Кроме того, диалоговое окно приветствия всегда по умолчанию слишком «получить доступ ни один public», а не hello фактическое текущее значение.</span><span class="sxs-lookup"><span data-stu-id="cf041-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="cf041-421">Улучшена работа с клавиатурой, специальные возможности и поддержка пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cf041-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="cf041-422">Длинный текст журнала строки навигации переносится с помощью пробела.</span><span class="sxs-lookup"><span data-stu-id="cf041-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="cf041-423">Диалоговое окно SAS поддерживает проверку входных данных.</span><span class="sxs-lookup"><span data-stu-id="cf041-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="cf041-424">Локальное хранилище toobe доступных продолжается, даже если истек срок действия учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="cf041-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="cf041-425">При удалении контейнера открытых больших двоичных объектов, обозревателя blob hello hello правой стороны закрыт</span><span class="sxs-lookup"><span data-stu-id="cf041-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-426">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-426">Known Issues</span></span>

* <span data-ttu-id="cf041-427">Потребности установки Linux версии gcc обновления или обновления — tooupgrade действия приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="cf041-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="cf041-428">18.11.2015</span><span class="sxs-lookup"><span data-stu-id="cf041-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="cf041-429">Версия 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="cf041-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="cf041-430">Создать</span><span class="sxs-lookup"><span data-stu-id="cf041-430">New</span></span>

* <span data-ttu-id="cf041-431">Версии macOS и Windows.</span><span class="sxs-lookup"><span data-stu-id="cf041-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="cf041-432">Войдите в tooview учетные записи хранения — используется учетная запись организации, учетная запись Майкрософт, 2FA, и т. д.</span><span class="sxs-lookup"><span data-stu-id="cf041-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="cf041-433">Локальное хранилище для разработки (используйте эмулятор хранения, только Windows).</span><span class="sxs-lookup"><span data-stu-id="cf041-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="cf041-434">Поддержка ресурсов Azure Resource Manager и классического хранилища.</span><span class="sxs-lookup"><span data-stu-id="cf041-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="cf041-435">Создавайте и удаляйте большие двоичные объекты, очереди и таблицы.</span><span class="sxs-lookup"><span data-stu-id="cf041-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="cf041-436">Ищите конкретные большие двоичные объекты, очереди и таблицы.</span><span class="sxs-lookup"><span data-stu-id="cf041-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="cf041-437">Исследуйте hello содержимое контейнеров BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="cf041-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="cf041-438">Просматривайте каталоги и перемещайтесь по ним.</span><span class="sxs-lookup"><span data-stu-id="cf041-438">View and navigate through directories</span></span>
* <span data-ttu-id="cf041-439">Передавайте, скачивайте и удаляйте большие двоичные объекты и папки.</span><span class="sxs-lookup"><span data-stu-id="cf041-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="cf041-440">Просмотр и изменение свойств и метаданных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf041-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="cf041-441">Создавайте ключи SAS.</span><span class="sxs-lookup"><span data-stu-id="cf041-441">Generate SAS keys</span></span>
* <span data-ttu-id="cf041-442">Создавайте хранимые политики доступа (SAP) и управляйте ими.</span><span class="sxs-lookup"><span data-stu-id="cf041-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="cf041-443">Поиск больших двоичных объектов по префиксу.</span><span class="sxs-lookup"><span data-stu-id="cf041-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="cf041-444">Перетащите 'n drop tooupload файлы или загрузки</span><span class="sxs-lookup"><span data-stu-id="cf041-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="cf041-445">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cf041-445">Known Issues</span></span>

* <span data-ttu-id="cf041-446">При задании уровня общего доступа контейнера больших двоичных объектов, новое значение hello не обновляется, пока не будет повторно задан hello фокус на контейнер hello</span><span class="sxs-lookup"><span data-stu-id="cf041-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="cf041-447">При открытии диалогового окна tooset hello hello-уровень общего доступа, он всегда будет отображаться «Нет общего доступа» как по умолчанию hello и не hello фактическое текущее значение</span><span class="sxs-lookup"><span data-stu-id="cf041-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="cf041-448">Не удается переименовать скачанные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="cf041-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="cf041-449">Состояние записи в журнале активности будет иногда могут «зависнуть» в выполняющееся при возникновении ошибки и hello ошибки не отображаются</span><span class="sxs-lookup"><span data-stu-id="cf041-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="cf041-450">Иногда сбоев и включение полностью белому при попытке tooupload или загружать большое количество больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cf041-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="cf041-451">Иногда отмена операции копирования не работает.</span><span class="sxs-lookup"><span data-stu-id="cf041-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="cf041-452">При создании контейнера (больших двоичных объектов или очереди или таблицы), если недопустимое имя входных данных и продолжить toocreate другой под другой контейнер типа нельзя задать фокус на новый тип hello</span><span class="sxs-lookup"><span data-stu-id="cf041-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="cf041-453">Не удается создать или переименовать папку.</span><span class="sxs-lookup"><span data-stu-id="cf041-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md