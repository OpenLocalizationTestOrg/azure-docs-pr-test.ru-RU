### <a name="install-via-composer"></a><span data-ttu-id="769b7-101">Установка через компоновщик</span><span class="sxs-lookup"><span data-stu-id="769b7-101">Install via Composer</span></span>
1. <span data-ttu-id="769b7-102">[Установите Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="769b7-102">[Install Git][install-git].</span></span> <span data-ttu-id="769b7-103">Обратите внимание, что в Windows, необходимо также добавить переменную среды PATH исполняемый tooyour Git hello.</span><span class="sxs-lookup"><span data-stu-id="769b7-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="769b7-104">Создайте файл с именем **composer.json** в hello корень проекта и добавьте следующий код tooit hello:</span><span class="sxs-lookup"><span data-stu-id="769b7-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="769b7-105">Скачайте **[composer.phar][composer-phar]** в корневой каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="769b7-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="769b7-106">Откройте командную строку и выполните следующую команду в корневом каталоге проекта hello</span><span class="sxs-lookup"><span data-stu-id="769b7-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
