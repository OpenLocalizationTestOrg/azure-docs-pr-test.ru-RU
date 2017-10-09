---
title: "aaaEncrypt виртуальной машине Azure | Документы Microsoft"
description: "Этот документ поможет вам tooencrypt виртуальной машине Azure после получения оповещения центра обеспечения безопасности Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Шифрование виртуальной машины Azure
Если у вас есть незашифрованные виртуальные машины, центр безопасности Azure оповестит вас. Эти предупреждения будут показаны как высокого уровня серьезности и hello рекомендация является tooencrypt эти виртуальные машины.

![Рекомендации по шифрованию дисков](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> Hello сведения в этом документе относятся tooencrypting виртуальных машин без использования шифрования ключа (который обязателен для резервного копирования виртуальных машин с помощью резервного копирования Azure). См. в разделе статьи hello [Azure диск шифрования для Windows и виртуальных машин Linux Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) сведения о том, как toouse toosupport ключа шифрования для зашифрованного виртуальных машин Azure служба архивации Azure.
>
>

tooencrypt виртуальных машинах Azure, которые идентифицируются центра безопасности Azure, указывающая шифрования, мы рекомендуем hello следующие шаги:

* Установите и настройте Azure PowerShell. Это позволит toorun hello PowerShell команды требуется tooset копирование tooencrypt необходимые предварительные требования hello виртуальных машинах Azure.
* Получение и запустите сценарий hello предварительные требования шифрования диска Azure, Azure PowerShell
* Зашифруйте свои виртуальные машины.

Hello цель данного документа — tooenable вы tooencrypt виртуальные машины, даже при наличии очень низкая или отсутствует в Azure PowerShell.
В этом документе предполагается, что вы используете Windows 10 как hello клиентского компьютера, с которого вы настроите шифрование диска Azure.

Существует множество подходов, которые могут быть предварительные условия используется toosetup hello и tooconfigure шифрования для виртуальных машин Azure. Если вы уже хорошо versed в Azure PowerShell или Azure CLI, то лучше toouse альтернативные подходы.

> [!NOTE]
> toolearn Дополнительные сведения о шифрования tooconfiguring альтернативные подходы для виртуальных машин Azure, см. в разделе [Azure диск шифрования для Windows и виртуальных машин Linux Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Установка и настройка Azure PowerShell
На компьютере необходимо установить Azure PowerShell 1.2.1 или более поздней версии. статья Hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) содержит все hello шаги, которые tooprovision toowork ваш компьютер с помощью Azure PowerShell. наиболее простой подход Hello подход toouse hello Web PI установки упоминаемые в этой статье. Даже если у вас уже есть Azure PowerShell установлен, установить повторно с использованием подхода hello Web PI, чтобы получить последнюю версию Azure PowerShell hello.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Получение и выполните необходимые условия для шифрования диска Azure hello скрипт конфигурации
Hello сценарий настройки необходимых компонентов шифрования диска Azure устанавливаются все hello, необходимых для шифрования виртуальные машины Azure.

1. Страница GitHub перейдите toohello hello [Azure диск шифрования необходимых компонентов установки скрипт](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. На странице приветствия GibHub щелкните hello **Raw** кнопки.
3. Используйте **CTRL + A** tooselect все hello текста на странице приветствия, а затем используйте **CTRL-C** toocopy все hello текст в буфере обмена toohello страницы приветствия.
4. Откройте **Блокнот** и вставьте текст hello копируются в Блокнот.
5. Создайте на диске C: новую папку с именем **AzureADEScript**.
6. Сохраните файл в блокноте hello, нажав **файл**, нажмите кнопку **Сохранить как**. Введите в текстовое поле имя файла hello **«ADEPrereqScript.ps1»** и нажмите кнопку **Сохранить**. (Убедитесь, что кавычки hello hello имя, в противном случае он hello-файл будет сохранен с расширением .txt).

Теперь, когда содержимое сценария hello сохраняется, откройте скрипт hello hello интегрированной среды Сценариев PowerShell.

1. В hello меню "Пуск", щелкните **Cortana**. Попросите **Cortana** «PowerShell», введя **PowerShell** в Cortana hello поиска.
2. Щелкните правой кнопкой мыши **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.
3. В hello **администратор: Windows PowerShell ISE** окно, нажмите кнопку **представление** и нажмите кнопку **Показать область сценариев**.
4. Если вы видите hello **команды** панели hello правой части окна приветствия щелкните hello **«x»** в hello правом верхнем углу панели tooclose hello его. Если текст hello слишком мал для вас toosee, используйте **CTRL + добавить** («Добавить» — hello «знак "+"»). Если текст hello слишком велико, используйте **CTRL + Subtract** (Subtract — hello»-«входа).
5. Щелкните **Файл** и выберите пункт **Открыть**. Перейдите toohello **C:\AzureADEScript** папки и hello дважды щелкнуть hello **ADEPrereqScript**.
6. Hello **ADEPrereqScript** содержимое должен появиться в интегрированной среде Сценариев PowerShell hello и имеет цветовую маркировку toohelp более легко получить различные компоненты, такие как команды, параметры и переменные.

Вы увидите нечто похожее на следующем рисунке hello.

![Окно PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

hello нижней области — ссылка tooas hello «консоли» Hello верхней панели — hello tooas ссылка «"панель сценарий» Мы будем использовать эти термины далее в этой статье.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Выполните команду PowerShell предварительные требования шифрования диска Azure hello
Предварительные требования для шифрования диска Azure скрипт Hello запросит следующую информацию, после запуска сценария hello hello:

* **Имя группы ресурсов** — имя для группы ресурсов, которые должны tooput hello hello хранилище ключей в.  Если его не существует уже с таким именем создан создается новую группу ресурсов с именем Привет вводимых вами. При наличии группы ресурсов, которые должны toouse в эту подписку, затем введите имя hello данной группы ресурсов.
* **Имя хранилища ключей** -имя хранилища ключей hello, в какие шифрования, ключи toobe разместить. Будет создано хранилище ключей с таким именем (если оно еще не создано). Если уже имеется хранилище ключей, которые должны toouse, введите имя hello hello существующие хранилища ключей.
* **Расположение** -расположение hello хранилища ключей. Убедитесь, что hello хранилище ключей и виртуальные машины toobe зашифрованы в hello местоположения. Если вам не известно расположение hello, далее в этой статье, будет показано, как будут действия toofind out.
* **Имя приложения с Azure Active Directory** -имя hello приложений Azure Active Directory, используемые toowrite секреты toohello хранилища ключей. Будет создано приложение с таким именем (если оно еще не создано). Если уже имеется приложение Azure Active Directory, что требуется toouse, введите имя hello этого приложения Azure Active Directory.

> [!NOTE]
> Если интересно как toowhy необходимо toocreate приложения Azure Active Directory, см. в разделе *зарегистрировать приложение в Azure Active Directory* hello статьи [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).
>
>

Выполните следующие шаги tooencrypt виртуальной машине Azure hello.

1. Если закрыто hello интегрированной среды Сценариев PowerShell, откройте экземпляр hello интегрированной среды Сценариев PowerShell с повышенными привилегиями. Следуйте инструкциям hello ранее в этой статье, если открыть интегрированной среды Сценариев PowerShell еще не приветствия. При закрытии скрипт hello откройте hello **ADEPrereqScript.ps1** щелкнув **файл**, затем **откройте** и выбрав команду сценария hello hello **c:\ AzureADEScript** папки. Если в этой статье были выполнены с начала hello, просто переместите на следующем шаге toohello.
2. В консоли hello hello интегрированной среды Сценариев PowerShell (hello нижней части интегрированной среды Сценариев PowerShell hello), изменить локальной toohello фокус hello hello сценария, введя **cd c:\AzureADEScript** и нажмите клавишу **ввод**.
3. Задайте политику выполнения hello на компьютере, чтобы обеспечить возможность выполнения скрипта hello. Тип **Set-ExecutionPolicy Unrestricted** в hello консоли и нажмите клавишу ВВОД. Если отображается диалоговое окно, сообщение о эффекты hello hello изменение tooexecution политики, щелкните **Да tooall** или **Да** (Если вы видите **Да tooall**, выберите соответствующий параметр – если Вы не видите **Да tooall**, нажмите кнопку **Да**).
4. Войдите в свою учетную запись Azure. Можно ввести в консоли hello **входа AzureRmAccount** и нажмите клавишу **ввод**. Диалоговое окно будет отображаться, в котором можно ввести учетные данные (Убедитесь, что у вас есть права toochange hello виртуальных машин — Если нет прав, не будет возможности tooencrypt их. (Убедитесь, что у вас есть права на изменение виртуальных машин, иначе вы не сможете зашифровать виртуальные машины. Вы должны увидеть сведения о **среде**, **учетной записи**, а также **TenantId**, **SubscriptionId** и **CurrentStorageAccount**. Копировать hello **SubscriptionId** tooNotepad. Он потребуется toouse на шаге #6.
5. Найти какие подписки виртуальный компьютер принадлежит tooand его расположение. Go слишком[https://portal.azure.com](ttps://portal.azure.com) и войдите в систему.  Щелкните hello левая сторона страницы приветствия, **виртуальные машины**. Вы увидите список виртуальных машин и hello подписки, которым они принадлежат.

   ![Виртуальные машины](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Возвращает toohello интегрированной среды Сценариев PowerShell. Задать контекст hello подписки, в которой будет выполняться скрипт hello. Можно ввести в консоли hello **Select AzureRmSubscription — SubscriptionId < your_subscription_Id >** (Замените **< your_subscription_Id >** своим Идентификатором подписки фактическое) и нажмите клавишу  **Введите**. Вы увидите сведения о среде, hello **учетной записи**, **TenantId**, **SubscriptionId** и **CurrentStorageAccount**.
7. Теперь вы находитесь готов toorun hello скрипта. Нажмите кнопку hello **выполнить сценарий** или клавишу **F5** на клавиатуре hello.

   ![Выполнение скрипта PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. запрашивает Hello сценарий **resourceGroupName:** -введите имя hello *группы ресурсов* требуется toouse, нажмите клавишу **ввод**. Если у вас его нет, введите имя для нового требуется toouse. Если у вас уже есть *группы ресурсов* требуется toouse (например, «hello один виртуальный компьютер, находящийся в), введите имя hello hello существующие группы ресурсов.
9. запрашивает Hello сценарий **keyVaultName:** -введите имя hello hello *хранилище ключей* toouse и нажмите клавишу ВВОД. Если у вас его нет, введите имя для нового требуется toouse. При наличии нужных toouse хранилище ключей, введите имя hello hello существующих *хранилище ключей*.
10. запрашивает Hello сценарий **расположение:** — введите имя hello hello расположения, в какие hello находится требуется tooencrypt виртуальной Машины, а затем нажмите клавишу **ввод**. Если вы не помните hello расположение, вы можете вернуться toostep #5.
11. запрашивает Hello сценарий **aadAppName:** -введите имя hello hello *Azure Active Directory* приложение, требуется toouse, затем нажмите клавишу **ввод**. Если у вас его нет, введите имя для нового требуется toouse. Если у вас уже есть *приложения Azure Active Directory* требуется toouse, введите имя hello hello существующих *приложения Azure Active Directory*.
12. Появится диалоговое окно входа. Укажите свои учетные данные (Да, необходимо войти в один раз, но теперь требуется toodo его еще раз).
13. сценарий Hello выполняется, а по завершении он запросит значения hello toocopy hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**и **keyVaultResourceId**. Каждый из этих значений toohello буфера копирования и вставьте их в Блокнот.
14. Вернуть toohello интегрированной среды Сценариев PowerShell и поместите курсор hello в конце hello последнюю строку hello и нажмите клавишу **ввод**.

Вывод Hello hello скрипта должен выглядеть примерно экран приветствия, показанный ниже:

![Вывод PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Шифрование hello виртуальной машины Azure
Вы являются tooencrypt теперь готовы к виртуальной машине. Если виртуальная машина находится в hello же группе ресурсов вашего хранилища ключей, можно переместить на разделе действий toohello шифрования. Тем не менее если виртуальная машина не находится в hello же группа ресурсов как вашего хранилища ключей, вы должны будете tooenter следующие hello в hello консоли в интегрированной среде Сценариев PowerShell hello:

**$resourceGroupName = <’Virtual_Machine_RG’>**

Замените **< Virtual_Machine_RG >** с именем hello hello группы ресурсов, в котором содержатся виртуальные машины, заключенных в одинарные кавычки. Нажмите клавишу **ВВОД**.
tooconfirm, Здравствуйте правильных введено имя группы ресурсов, введите ниже hello в hello консоли интегрированной среды Сценариев PowerShell:

**$resourceGroupName**

Нажмите клавишу **ВВОД**. Вы увидите hello имя группы ресурсов, виртуальные машины находятся в. Например:

![Вывод PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Шаги шифрования
Во-первых, необходимо имя hello PowerShell tootell hello виртуальной машины требуется tooencrypt. В консоли hello введите:

**$vmName = <’your_vm_name’>**

Замените **< your_vm_name >** с именем hello вашей виртуальной машины (Убедитесь, что имя hello, заключенных в одинарные кавычки) и нажмите клавишу **ввод**.

tooconfirm, Здравствуйте правильных введено имя виртуальной Машины, введите:

**$vmName**

Нажмите клавишу **ВВОД**. Вы увидите имя hello hello виртуальной машины требуется tooencrypt. Например:

![Вывод PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Существует два методы toorun hello шифрования команда tooencrypt все диски на виртуальной машине hello. Первый метод Hello является hello tootype следующую команду в консоли PowerShell ISE hello:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Введя эту команду, нажмите клавишу **ВВОД**.

Второй метод Hello — tooclick в области сценариев hello (hello верхней панели hello интегрированной среды Сценариев PowerShell) и прокрутите вниз toohello конец скрипта hello. Выделите команду hello, перечисленных выше и затем щелкните правой кнопкой мыши его и нажмите кнопку **выполнить выделенный фрагмент** или нажмите клавишу **F8** на клавиатуре hello.

![Интегрированная среда сценариев PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Независимо от метода hello используется, диалоговое окно будет отображаться информирующее 10 – 15 минут для операции toocomplete hello. Щелкните **Да**.

Во время процесса шифрования hello, можно возвращать toohello портала Azure и просмотреть состояние hello hello виртуальной машины. На hello левая сторона страницы приветствия, нажмите кнопку **виртуальные машины**, затем в hello **виртуальные машины** колонка, щелкните имя виртуальной машины hello, шифрование hello. В колонке hello, которое отображается, вы заметите, что hello **состояние** говорит, что это **обновление**. которое свидетельствует о выполнении шифрования.

![Дополнительные сведения о hello виртуальной Машины](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Возвращает toohello интегрированной среды Сценариев PowerShell. После завершения скрипта hello, вы увидите, что будет отображаться в приведенном ниже рисунке hello.

![Вывод PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

Теперь шифруется toodemonstrate, hello виртуальной машины, возвращают toohello портала Azure и нажмите кнопку **виртуальные машины** на hello левая сторона страницы приветствия. Щелкните имя hello hello виртуальной машины, которые были зашифрованы. В hello **параметры** колонка, щелкните **дисков**.

![Параметры](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

На hello **дисков** колонку, вы увидите, что **шифрования** — **включено**.

![Свойства дисков](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Дальнейшие действия
В этом документе вы узнали, каким образом tooencrypt виртуальной машине Azure. toolearn Дополнительные сведения о центра безопасности Azure, см. ниже hello:

* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) -Узнайте, как предупреждения toosecurity toomanage и ответ
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности Azure и соответствию требованиям.
