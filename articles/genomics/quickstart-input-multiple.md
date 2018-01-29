---
title: "Краткое руководство: отправка рабочего процесса с помощью нескольких наборов входных данных | Документация Майкрософт"
titleSuffix: Azure
description: "В этом руководстве предполагается, что вы установили клиент msgen и успешно запустили примеры данных через службу."
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: quickstart
ms.date: 12/07/2017
ms.openlocfilehash: d410516f807b7914e15bed1fb93ee58d3e340d1e
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2017
---
# <a name="submit-a-workflow-using-multiple-inputs-from-the-same-sample"></a>Отправка рабочего процесса с помощью нескольких входных данных из одного примера

В этом руководстве показано, как отправить рабочий процесс в службу Microsoft Genomics, если входной файл включает несколько FASTQ- или BAM-файлов **из одного примера**. Однако следует помнить, что **нельзя** смешивать FASTQ- и BAM-файлы в рамках одной отправки.

В этом разделе предполагается, что вы уже установили и запустили клиент `msgen` и знаете, как использовать службу хранилища Azure. Если вы успешно отправили рабочий процесс с использованием предоставленного примера данных, можно продолжать работу с этим кратким руководством. 


## <a name="multiple-bam-files"></a>Несколько BAM-файлов

### <a name="upload-your-input-files-to-azure-storage"></a>Передача входных файлов в службу хранилища Azure
Предположим, что у вас есть несколько BAM-файлов в качестве входных данных — *reads.bam*, *additional_reads.bam* и *yet_more_reads.bam* — и вы передали их в свою учетную запись хранения *myaccount* в Azure. У вас есть URL-адрес API и ключ доступа. Вы хотите разместить выходные данные на странице **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.


### <a name="submit-your-job-to-the-msgen-client"></a>Отправка задания в клиент `msgen` 

Вы можете отправить несколько BAM-файлов, передав все их имена в аргумент --input-blob-name-1. Обратите внимание, что все файлы должны быть из одного примера, но их порядок не имеет значения. Ниже представлены примеры отправки данных из командной строки в Windows и Unix, а также с помощью файла конфигурации. Разрывы строк добавлены для ясности.


Для Windows:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


Для Unix:

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Если вы предпочитаете использовать файл конфигурации, он должен содержать следующие строки:

``` config.txt
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads.bam additional_reads.bam yet_more_reads.bam
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

Отправьте файл `config.txt` с помощью этого вызова: `msgen submit -f config.txt`


## <a name="multiple-paired-fastq-files"></a>Несколько пар FASTQ-файлов

### <a name="upload-your-input-files-to-azure-storage"></a>Передача входных файлов в службу хранилища Azure
Предположим, что у вас есть несколько пар FASTQ-файлов в качестве входных данных — *reads_1.fq.gz* и *reads_2.fq.gz*, *additional_reads_1.fq.gz* и *additional_reads_2.fq.gz*, *yet_more_reads_1.fq.gz* и *yet_more_reads_2.fq.gz*. Вы отправили их в свою учетную запись хранения *myaccount* в Azure, и у вас есть URL-адрес API и ключ доступа. Вы хотите разместить выходные данные на странице **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.


### <a name="submit-your-job-to-the-msgen-client"></a>Отправка задания в клиент `msgen` 

Пары FASTQ-файлов должны не только быть взяты из одного примера, но и обрабатываться вместе.  Порядок имен файлов имеет значение при передаче их в качестве аргументов в --input-blob-name-1 и --input-blob-name-2. 

Ниже представлены примеры отправки данных из командной строки в Windows и Unix, а также с помощью файла конфигурации. Разрывы строк добавлены для ясности.


Для Windows:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz ^
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


Для Unix:

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz \
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Если вы предпочитаете использовать файл конфигурации, он должен содержать следующие строки:

```
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads_1.fq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz
input_blob_name_2:                reads_2.fq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

Отправьте файл `config.txt` с помощью этого вызова: `msgen submit -f config.txt`

## <a name="next-steps"></a>Дальнейшие действия
Из этой статьи вы узнали, как передать несколько BAM-файлов или пар FASTQ-файлов в службу хранилища Azure и как отправить рабочий процесс в службу Microsoft Genomics через клиент Python `msgen`. Дополнительные сведения об отправке рабочего процесса и других команд, которые можно использовать в службе Microsoft Genomics, см. в разделе [часто задаваемых вопросов](frequently-asked-questions-genomics.md). 