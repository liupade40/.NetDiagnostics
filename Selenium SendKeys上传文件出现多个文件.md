用selenium的SendKeys上传文件时，第二次上传文件老是把第一次上传的文件一起上传了，感觉很奇怪；界面上有清空按钮，手动操作是没问题的，但是通过selenium操作就是有问题，刚好有两个上传控件，一个有问题，一个没问题，对比了两个控件发现，有问题了多了一个multiple属性，说明支持多文件上传，这说明上传完后并没有清空；
后面想了一个办法就是刷新页面第二次重新上传，发现可行。


        // 定位文件上传元素
        IWebElement fileInput = driver.FindElement(By.Id("file-upload-input"));

        // 第一次上传文件
        fileInput.SendKeys(@"C:\path\to\file1.txt");
        // 提交上传（视具体情况）
        // driver.FindElement(By.Id("submit-button")).Click();

        // 清空文件输入框（通过 JavaScript）
        IJavaScriptExecutor js = (IJavaScriptExecutor)driver;
        js.ExecuteScript("arguments[0].value = '';", fileInput);
