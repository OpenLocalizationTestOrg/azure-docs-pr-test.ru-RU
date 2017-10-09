


## <a name="tagging-a-virtual-machine-through-templates"></a>Пометка виртуальной машины с помощью шаблонов
Для начала рассмотрим пометку с помощью шаблонов. [Этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) помещает теги hello следующие ресурсы: вычислительные (виртуальная машина), (учетной записи хранилища) хранилища и сети (общедоступный IP-адрес виртуальной сети и сетевой интерфейс). (Это шаблон для виртуальной машины Windows, но его можно приспособить для виртуальных машин Linux.)

Нажмите кнопку hello **развертывание tooAzure** кнопку hello [ссылка на шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Это произойдет переход toohello [портал Azure](https://portal.azure.com/) которого можно развернуть этот шаблон.

![Простое развертывание с тегами](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Этот шаблон включает в себя следующие теги hello: *отдел*, *приложения*, и *автор*. Вы можно добавить или изменить эти теги непосредственно в шаблоне hello при желании имена другой тег.

![Теги Azure в шаблоне](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Как видите, теги hello определяются как пар ключей и значений, разделенных двоеточием (:). Hello теги должны быть определены в следующем формате:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Сохраните файл шаблона hello после завершения изменения его с тегами hello по своему усмотрению.

Затем в hello **изменение параметров** раздел, вы сами можете заполнить hello значения тегов.

![Редактирование тегов на портале Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Нажмите кнопку **создать** toodeploy этот шаблон нужные значения тега.

## <a name="tagging-through-hello-portal"></a>Добавление тегов через портал hello
После создания ресурсов с тегами, можно просматривать, добавлять и удалять теги в портале hello.

Выберите hello теги tooview значок тегов:

![Значок тегов на портале Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Добавить новый тег через портал hello, определив собственные пара ключ-значение и сохраните его.

![Добавление тега на портале Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Ваш новый тег должен появиться в списке hello тегов для ресурса.

![Новый тег, сохраненный на портале Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

