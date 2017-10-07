---
title: "Синхронизация Azure AD Connect: рабочие задачи и рекомендации | Документация Майкрософт"
description: "В этом разделе описываются рабочие задачи в Azure AD Connect sync и как tooprepare для работы этого компонента."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Службы синхронизации Azure AD Connect: рабочие задачи и рекомендации
Hello цель этого раздела — toodescribe рабочие задачи синхронизации Azure AD Connect.

## <a name="staging-mode"></a>Промежуточный режим
Промежуточный режим может использоваться в нескольких ситуациях, например:

* обеспечение высокой доступности;
* тестирование и развертывание новых изменений в конфигурации;
* Ввести новый сервер и списать старый hello.

С сервером в промежуточный режим можно изменять toohello изменения конфигурации и предварительного просмотра hello прежде чем вносить active hello server. Оно также позволяет toorun полный импорт и полную синхронизацию tooverify ожидается все изменения, прежде чем использовать эти изменения в рабочую среду.

Во время установки можно выбрать toobe сервера hello в **промежуточный режим**. Это действие hello сервер становится активной для импорта и синхронизации, но не выполняется никаким экспортам. Сервер в промежуточном режиме не выполняет синхронизацию и обратную запись паролей, даже если эти функции активированы при установке. Если отключить промежуточный режим hello server начинается экспорт, включает синхронизацию паролей и включает обратную запись паролей.

Экспорт по-прежнему можно принудительно с помощью диспетчера службы синхронизации hello.

На сервере в режиме промежуточного по-прежнему tooreceive изменения из Active Directory и Azure AD. Он всегда имеет копию hello последних изменений и может очень быстро примите через обязанности hello другого сервера. При внесении изменения конфигурации: tooyour основной сервер, это toomake вашей обязанностью hello того же сервера toohello изменения в промежуточный режим.

Для тех, кто с использованием сведений из старых технологий синхронизации hello промежуточный режим отличается, так как сервер hello имеет собственную базу данных SQL. Такая архитектура позволяет hello промежуточных toobe режим сервера, расположенный в другом центре обработки данных.

### <a name="verify-hello-configuration-of-a-server"></a>Проверка конфигурации hello сервера
tooapply этот метод, выполните следующие действия:

1. [Подготовка](#prepare)
2. [Конфигурация](#configuration)
3. [Импорт и синхронизация](#import-and-synchronize)
4. [Проверка](#verify)
5. [Переключение активного сервера](#switch-active-server)

#### <a name="prepare"></a>Подготовка.
1. Установить Azure AD Connect, выберите **промежуточный режим**и отмените выделение **начать синхронизацию** на последней странице приветствия мастера установки hello. Этот режим позволяет подсистема синхронизации hello toorun вручную.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Знак off/входа и выберите в меню Пуск hello **служба синхронизации**.

#### <a name="configuration"></a>Конфигурация
Если были внесены пользовательские изменения toohello основного сервера и конфигурации hello toocompare выполнялись с тестового сервера hello, используйте [Архивариус конфигурации Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Импорт и синхронизация
1. Выберите **соединители**, и выберите hello первый соединитель с типом hello **доменных служб Active Directory**. Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**. Проделайте это для всех соединителей данного типа.
2. Выберите hello соединитель с типом **Azure Active Directory (Майкрософт)**. Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**.
3. Убедитесь, что по-прежнему выбрана вкладка hello соединители. Для каждого соединителя типа **Доменные службы Active Directory** щелкните **Запуск**, выберите **Синхронизация изменений** и нажмите кнопку **ОК**.
4. Выберите hello соединитель с типом **Azure Active Directory (Майкрософт)**. Щелкните **Запуск**, выберите**Синхронизация изменений**) и нажмите кнопку **ОК**.

У вас теперь промежуточные экспорта изменяет tooAzure AD и локальной AD (при использовании гибридного развертывания Exchange). Дальнейшие действия Hello разрешить tooinspect, что такое о toochange перед запуском hello Экспорт toohello каталогов.

#### <a name="verify"></a>Проверка.
1. Запустите командную строку и перейдите в слишком`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Запуск: `csexport "Name of Connector" %temp%\export.xml /f:x` имя hello hello соединителя можно найти в службе синхронизации. Она имеет аналогичные too"contoso.com имя — AAD» для Azure AD.
3. Скопируйте сценарий PowerShell hello из раздела hello [CSAnalyzer](#appendix-csanalyzer) tooa файл с именем `csanalyzer.ps1`.
4. Откройте окно PowerShell и найдите папку toohello, где создан сценарий PowerShell hello.
5. Выполните команду `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Теперь у вас есть файл **processedusers1.csv**, который можно просмотреть в Microsoft Excel. В этом файле находятся tooAzure toobe экспортировать все промежуточные изменения AD.
7. Внесите необходимые изменения toohello данные или конфигурация и выполните эти шаги еще раз (импорта и синхронизации и проверьте) пока ожидаются изменения, которые будут экспортированы toobe приветствия.

#### <a name="switch-active-server"></a>Переключение активного сервера
1. На сервере активной hello Выключите сервер hello (DirSync/FIM/Azure AD Sync), поэтому он не выполняет экспорт tooAzure AD или установите его в промежуточный режим (Azure AD Connect).
2. Запустите мастер установки hello на сервере hello в **промежуточный режим** и отключить **промежуточный режим**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Аварийное восстановление
Реализация конструктора hello входит tooplan для какой toodo в случае аварии где потерять hello сервера синхронизации. Существуют различные модели toouse и какие один toouse зависит от нескольких факторов, включая:

* Что такое допустимым не может делать изменений tooobjects в Azure AD во время простоя hello
* При использовании синхронизации паролей пользователей hello принимаете наличие toouse Здравствуй, старый пароль в Azure AD в случае, если они изменяются в локальной среде?
* Зависите ли вы от выполняемых в реальном времени операций, таких как обратная запись паролей?

В зависимости от hello ответы toothese вопросы и политике вашей организации можно реализовать одним из следующих стратегий hello:

* Восстановление при необходимости.
* Наличие запасного резервного сервера ( **промежуточный режим**).
* Использование виртуальных машин.

Если hello встроенной базы данных SQL Express не используется, то следует также просмотреть hello [высокого уровня доступности SQL](#sql-high-availability) раздела.

### <a name="rebuild-when-needed"></a>Восстановление при необходимости
Стратегии реальную — tooplan для перестроения сервера, при необходимости. Как правило установке hello подсистема синхронизации и hello первоначального импорта и синхронизации можно выполнить в течение нескольких часов. Если запасной сервер недоступен, это возможных tootemporarily использовать механизм синхронизации toohost hello домена контроллера.

сервер подсистемы синхронизации Hello не хранят любое состояние, об объектах hello, hello базы данных можно восстановить из данных hello в Active Directory и Azure AD. Hello **sourceAnchor** атрибута является используемым toojoin hello объекты из локальной и облачной hello. При повторном построении сервера hello с существующие объекты в локальной и hello облака, а затем hello синхронизирует engine совпадения этих объектов в повторной установки еще раз. Hello требуется toodocument и сохранить обстоятельства hello общий доступ к изменениям конфигурации сервера toohello, такие как правила фильтрации и синхронизации. Эти пользовательские конфигурации необходимо применить повторно перед началом синхронизации.

### <a name="have-a-spare-standby-server---staging-mode"></a>Наличие запасного резервного сервера (промежуточный режим)
В более сложной среде рекомендуется использовать один или несколько резервных серверов. Во время установки, можно включить сервер toobe в **промежуточный режим**.

Дополнительные сведения см. в разделе [Промежуточный режим](#staging-mode).

### <a name="use-virtual-machines"></a>Использование виртуальных машин
Общие и поддерживаемый метод — подсистема синхронизации hello toorun на виртуальной машине. В случае узла hello имеется проблема, hello изображения с сервера ядра СУБД hello синхронизации может быть перенесенных tooanother сервер.

### <a name="sql-high-availability"></a>Высокий уровень доступности сервера SQL
Высокий уровень доступности для SQL Server следует также рассматривать, если не используется SQL Server Express, входящий в состав Azure AD Connect hello. решения высокого уровня доступности Hello поддерживается включают кластеры SQL и AOA (группы доступности AlwaysOn). Такие решения, как зеркальное отображение, не поддерживаются.

Поддержка SQL AOA была добавлена tooAzure AD Connect версии 1.1.524.0. Перед установкой Azure AD Connect включите функцию SQL AOA. Во время установки Azure AD Connect определяет, включен ли указанный экземпляр SQL hello для SQL AOA. При включении SQL AOA дальнейшей Azure AD Connect определяет, является ли SQL AOA настроенных toouse Синхронная репликация или асинхронная репликация. При настройке прослушивателя группы доступности hello, рекомендуется установить свойство too0 hello RegisterAllProvidersIP. Это так, как Azure AD Connect в настоящее время использует собственный клиент SQL tooconnect tooSQL и собственный клиент SQL не поддерживает использование hello MultiSubNetFailover свойства.

## <a name="appendix-csanalyzer"></a>Приложение CSAnalyzer
В разделе hello [проверить](#verify) о том, как toouse этот сценарий.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**  

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)  
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)  
