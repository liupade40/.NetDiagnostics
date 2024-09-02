# C#调用第三方软件及交互

最近有一个功能pdf转epub，网上找到一个解决方案[pdf2epubEX](https://github.com/dodeeric/pdf2epubEX "pdf2epubEX")，Windows环境只能以docker方式安装，手动执行docker命令是可以的，如下图:
![image](https://github.com/user-attachments/assets/bbf6bbd1-07a3-4047-8d0f-4043486cc620)

由于pdf数量过多，全部手动转肯定不行，想通过C#调用docker命令，但是这种方法会报错"the input device is not a TTY. If you are using mintty, try prefixing the command with ‘winpty’
"，网上查了一下是Windows和docker的交互有关系。后面选择了在Linux上面直接安装软件，然后用C#调用软件并且提供交互。
需要与软件进行交互要用异步，不然streamReader.ReadLine()当输出完以后，有交互的话会卡在这里，一开始这里也琢磨了好久，这也是为什么要写这篇文章的原因吧。

以下是相关代码：
```csharp
static async Task Main(string[] args)
{
    string folderPath = Path.Combine("pdf");
    string[] pdfFiles = Directory.GetFiles(folderPath, "*.pdf");
    foreach (var item in pdfFiles)
    {
        try
        {
            ProcessStartInfo startInfo = new ProcessStartInfo
            {
                FileName = "pdf2epubEX",
                Arguments = item,
                RedirectStandardInput = true,
                RedirectStandardOutput = true,
                RedirectStandardError = true,
                UseShellExecute = false,
                CreateNoWindow = true
            };
            var filename = Path.GetFileName(item);
            Console.WriteLine($"开始处理:{filename}");
            using (var process = new Process { StartInfo = startInfo })
            {
                process.Start();

                // 处理标准输出流
                var outputTask = ReadOutputAsync(process.StandardOutput);
                // 处理标准错误流
                var errorTask = ReadOutputAsync(process.StandardError);

                // 写入标准输入流
                await WriteInputAsync(process.StandardInput);

                // 等待进程完成
                await process.WaitForExitAsync();

                // 等待输出和错误任务完成
                await Task.WhenAll(outputTask, errorTask);

            }
        }
        catch (Exception ex)
        {
            
        }
        finally
        {

        }

    }
    
}

static async Task WriteInputAsync(StreamWriter standardInput)
{
    using (var writer = standardInput)
    {
        // 与软件进行交互， 这里可以发送多个输入
        await writer.WriteLineAsync("n");
        await writer.WriteLineAsync("svg");
        await writer.WriteLineAsync();//这里类似于直接敲回车，但是对于默认的参数不加这句好像也可以
        // 结束输入流
        writer.Close();
    }
}

static async Task ReadOutputAsync(StreamReader reader)
{
    using (var streamReader = reader)
    {
        string line;
        while ((line = await streamReader.ReadLineAsync()) != null)
        {
            Console.WriteLine("Output: " + line);
        }
    }
}
```
