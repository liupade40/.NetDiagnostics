用selenium的SendKeys上传文件时，第二次上传文件老是把第一次上传的文件一起上传了，感觉很奇怪；界面上有清空按钮，手动操作是没问题的，但是通过selenium操作就是有问题，刚好有两个上传控件，一个有问题，一个没问题，对比了两个控件发现，有问题的控件多了一个multiple属性，该属性说明支持多文件上传，这说明上传完后并没有清空内容。
``` csharp
// 定位文件上传元素
IWebElement fileInput = driver.FindElement(By.Id("file-upload-input"));

// 第一次上传文件
fileInput.SendKeys(@"C:\path\to\file1.txt");
```

后面想了一个办法就是第一次上传完刷新页面再上传，发现可行；还有一种方法就是通过调用js清空控件内容。代码如下：

方法1：
``` csharp
driver.Navigate().Refresh();
```
方法2：
``` csharp
IJavaScriptExecutor js = (IJavaScriptExecutor)driver;
js.ExecuteScript("arguments[0].value = '';", fileInput);
```
