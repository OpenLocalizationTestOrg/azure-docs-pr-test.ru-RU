Теперь Azure поддерживает две функции отладки. Виртуальные машины Azure, созданные на основе модели развертывания с помощью Resource Manager, поддерживают выходные данные и снимки экрана консоли. 

При повторном подключении tooAzure собственного образа или даже загрузки одного из образов платформы hello, может быть несколько причин, почему Возвращает виртуальную машину в состояние не является загрузочным. Эти функции позволяют вам tooeasily Диагностика и восстановление сбоев загрузки виртуальных машин.

Для виртуальных машин Linux можно легко просмотреть hello выходные данные журналов консоли из hello портала:

![Портал Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Тем не менее для Windows и Linux виртуальных машин Azure также позволяет toosee снимок экрана приветствия виртуальных Машин из низкоуровневой оболочки hello:

![Ошибка](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Обе эти функции доступны на виртуальных машинах Azure во всех регионах. Обратите внимание, снимки экрана и выходных данных может занять tooappear минут too10 вашей учетной записи хранилища.

## <a name="common-boot-errors"></a>Распространенные ошибки загрузки

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Операционная система не найдена](https://support.microsoft.com/help/4010142)
- [Сбой при загрузке или INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Включение диагностики на новой виртуальной машине
1. При создании новой виртуальной машины из hello предварительной версии портала выберите hello **диспетчера ресурсов Azure** из раскрывающегося списка модели развертывания hello:
 
    ![Диспетчер ресурсов](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Настройте hello мониторинг параметр tooselect hello учетной записи хранилища куда tooplace эти файлы диагностики.
 
    ![Создание виртуальной машины](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. При развертывании на основе шаблона Azure Resource Manager перейдите tooyour ресурса виртуальной машины и добавить профиль раздел hello диагностики. Не забывайте заголовок версии API «2015-06-15» hello toouse.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Hello диагностического профиля позволяет учетной записи хранилища hello tooselect место tooput эти журналы.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy образец виртуальной машины с включена, диагностика загрузки извлечение здесь нашей репозитория.

## <a name="update-an-existing-virtual-machine"></a>Обновление имеющейся виртуальной машины ##

Диагностика загрузки tooenable через hello портала, можно также обновить существующую виртуальную машину через портал hello. Выберите hello Диагностика загрузки и сохранить. Перезапустите эффект tootake hello виртуальной Машины.

![Обновление имеющейся виртуальной машины](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

