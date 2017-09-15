### <a name="install-via-composer"></a><span data-ttu-id="f8be6-101">Установка через компоновщик</span><span class="sxs-lookup"><span data-stu-id="f8be6-101">Install via Composer</span></span>
1. <span data-ttu-id="f8be6-102">[Установите Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="f8be6-102">[Install Git][install-git].</span></span> <span data-ttu-id="f8be6-103">Обратите внимание, что в Windows необходимо также добавить исполняемый файл Git в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="f8be6-103">Note that on Windows, you must also add the Git executable to your PATH environment variable.</span></span> 
2. <span data-ttu-id="f8be6-104">Создайте файл с именем **composer.json** в корневой папке проекта и добавьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="f8be6-104">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="f8be6-105">Скачайте **[composer.phar][composer-phar]** в корневой каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="f8be6-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="f8be6-106">Откройте командную строку и выполните следующую команду в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="f8be6-106">Open a command prompt and execute the following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
