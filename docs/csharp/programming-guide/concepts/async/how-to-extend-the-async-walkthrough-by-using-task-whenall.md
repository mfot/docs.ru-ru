---
title: "Практическое руководство. Расширение пошагового руководства по асинхронным процедурам с использованием метода Task.WhenAll (C#)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
ms.assetid: f6927ef2-dc6c-43f8-bc82-bbeac42de423
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: e074874a539d1dd52901ff6a5841b5a501b5b5af
ms.sourcegitcommit: cec0525b2121c36198379525e69aa5388266db5b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-c"></a>Практическое руководство. Расширение пошагового руководства по асинхронным процедурам с использованием метода Task.WhenAll (C#)
Можно повысить производительность асинхронного решения, которое описывается в [пошаговом руководстве по получению доступа к Интернету с помощью модификатора Async и оператора Await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md), с помощью метода <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>. Этот метод асинхронно ожидает несколько асинхронных операций, которые представлены в виде коллекции задач.  
  
 Как вы могли заметить в этом пошаговом руководстве, веб-сайты загружаются с разной скоростью. Иногда один из веб-сайтов работает слишком медленно, что задерживает все остальные загрузки. Во время работы асинхронных программ, созданных в этом пошаговом руководстве, программу можно с легкостью завершить, если нет необходимости в ожидании, но было бы лучше начать все загрузки одновременно и дать возможность более быстрым загрузкам продолжаться без ожидания более медленных.  
  
 Метод `Task.WhenAll` можно применить к коллекции задач. Метод `WhenAll`, примененный к коллекции, возвращает одну задачу, которая остается незавершенной до тех пор, пока не будет выполнена каждая задача из коллекции. Как видим, задачи выполняются параллельно, однако дополнительные потоки не создаются. Задачи могут выполняться в любом порядке.  
  
> [!IMPORTANT]
>  Следующие процедуры описывают расширения для асинхронных приложений, разработка которых описывается в статье [Пошаговое руководство. Получение доступа к Интернету с помощью модификатора Async и оператора Await](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). Вы можете разработать приложения, выполнив пошаговое руководство или скачав код на странице [Примеры кода от разработчиков](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f).  
>   
>  Для выполнения этого примера на компьютере должна быть установлена среда Visual Studio 2012 или более поздней версии.  
  
### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a>Добавление метода Task.WhenAll в решение GetURLContentsAsync  
  
1.  Добавьте метод `ProcessURLAsync` в первое приложение, которое разрабатывается в статье [Пошаговое руководство. Получение доступа к Интернету с помощью модификатора Async и оператора Await](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Если вы скачали код со страницы [Примеры кода от разработчиков](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f), откройте проект AsyncWalkthrough, а затем добавьте `ProcessURLAsync` в файл MainWindow.xaml.cs.  
  
    -   Если вы разработали код, выполнив пошаговое руководство, добавьте `ProcessURLAsync` в приложение, которое включает метод `GetURLContentsAsync`. Файл MainWindow.xaml.cs для этого приложения — это первый пример в разделе "Полный код примеров из пошагового руководства".  
  
     Метод `ProcessURLAsync` объединяет действия в теле цикла `foreach` в `SumPageSizesAsync` в исходном пошаговом руководстве. Метод асинхронно скачивает содержимое указанного веб-сайта в виде массива байтов и затем отображает и возвращает длину массива байтов.  
  
    ```csharp  
    private async Task<int> ProcessURLAsync(string url)  
    {  
        var byteArray = await GetURLContentsAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  Закомментируйте или удалите цикл `foreach` в `SumPageSizesAsync`, как показано в следующем коде.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    byte[] urlContents = await GetURLContentsAsync(url);  
  
    //    // The previous line abbreviates the following two assignment statements.  
    //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
    //    //byte[] urlContents = await getContentsTask;  
  
    //    DisplayResults(url, urlContents);  
  
    //    // Update the total.            
    //    total += urlContents.Length;  
    //}  
    ```  
  
3.  Создайте коллекцию задач. Следующий код определяет [запрос](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d), который при выполнении метода <xref:System.Linq.Enumerable.ToArray%2A> создает коллекцию задач, скачивающих содержимое каждого веб-сайта. Задачи запускаются при вычислении запроса.  
  
     Добавьте следующий код в метод `SumPageSizesAsync` после объявления `urlList`.  
  
    ```csharp  
    // Create a query.   
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURLAsync(url);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  Примените `Task.WhenAll` к коллекции задач, `downloadTasks`. `Task.WhenAll` возвращает одну задачу, которая завершается после завершения всех задач в коллекции задач.  
  
     В следующем примере выражение `await` ожидает завершения одной задачи, возвращаемой `WhenAll`. Результат этого выражения – массив целых чисел, каждое из которых – размер загруженного веб-сайта. Добавьте следующий код в `SumPageSizesAsync` сразу после кода, добавленного на предыдущем шаге.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  И, наконец, используйте метод <xref:System.Linq.Enumerable.Sum%2A> для вычисления суммы длин всех веб-сайтов. Добавьте следующую строку в `SumPageSizesAsync`.  
  
    ```csharp  
    int total = lengths.Sum();  
    ```  
  
### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a>Добавление метода Task.WhenAll в решение HttpClient.GetByteArrayAsync  
  
1.  Добавьте следующую версию метода `ProcessURLAsync` во второе приложение, которое разрабатывается в статье [Пошаговое руководство. Получение доступа к Интернету с помощью модификатора Async и оператора Await](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Если вы скачали код со страницы [Примеры кода от разработчиков](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f), откройте проект AsyncWalkthrough_HttpClient, а затем добавьте `ProcessURLAsync` в файл MainWindow.xaml.cs.  
  
    -   Если вы разработали код, выполнив пошаговое руководство, добавьте `ProcessURLAsync` в приложение, которое использует метод `HttpClient.GetByteArrayAsync`. Файл MainWindow.xaml.cs для этого приложения  — это второй пример в разделе "Полный код примеров из пошагового руководства".  
  
     Метод `ProcessURLAsync` объединяет действия в теле цикла `foreach` в `SumPageSizesAsync` в исходном пошаговом руководстве. Метод асинхронно скачивает содержимое указанного веб-сайта в виде массива байтов и затем отображает и возвращает длину массива байтов.  
  
     Единственное отличие от метода `ProcessURLAsync` из предыдущей процедуры заключается в использовании экземпляра <xref:System.Net.Http.HttpClient>, `client`.  
  
    ```csharp  
    async Task<int> ProcessURL(string url, HttpClient client)  
    {  
        byte[] byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  Закомментируйте или удалите цикл `For Each` или `foreach` в `SumPageSizesAsync`, как показано в следующем коде.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
    //    // The previous line abbreviates the following two assignment  
    //    // statements.  
    //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
    //    byte[] urlContent = await getContentTask;  
  
    //    DisplayResults(url, urlContent);  
  
    //    // Update the total.  
    //    total += urlContent.Length;  
    //}  
    ```  
  
3.  Определите [запрос](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d), который при выполнении метода <xref:System.Linq.Enumerable.ToArray%2A> создает коллекцию задач, скачивающих содержимое каждого веб-сайта. Задачи запускаются при вычислении запроса.  
  
     Добавьте следующий код в метод `SumPageSizesAsync` после объявления `client` и `urlList`.  
  
    ```csharp  
    // Create a query.  
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURL(url, client);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  Затем примените `Task.WhenAll` к коллекции задач, `downloadTasks`. `Task.WhenAll` возвращает одну задачу, которая завершается после завершения всех задач в коллекции задач.  
  
     В следующем примере выражение `await` ожидает завершения одной задачи, возвращаемой `WhenAll`. Результат выражения `await` — массив целых чисел, каждое из которых представляет размер скачанного веб-сайта. Добавьте следующий код в `SumPageSizesAsync` сразу после кода, добавленного на предыдущем шаге.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  И, наконец, используйте метод <xref:System.Linq.Enumerable.Sum%2A> для получения суммы длин всех веб-сайтов. Добавьте следующую строку в `SumPageSizesAsync`.  
  
    ```csharp  
    int total = lengths.Sum();
    ```  
  
### <a name="to-test-the-taskwhenall-solutions"></a>Тестирование решений Task.WhenAll  
  
-   Для любого из решений нажмите клавишу F5, чтобы запустить программу, а затем нажмите кнопку **Запуск**. Полученный вывод должен напоминать вывод из асинхронных решений в статье [Пошаговое руководство. Получение доступа к Интернету с помощью модификатора Async и оператора Await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). Тем не менее обратите внимание, что веб-сайты каждый раз отображаются в другом порядке.  
  
## <a name="example"></a>Пример  
 В следующем коде показано расширение для проекта, использующее метод `GetURLContentsAsync` для скачивания содержимого из Интернета.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // Two-step async call.  
            Task sumTask = SumPageSizesAsync();  
            await sumTask;  
  
            // One-step async call.  
            //await SumPageSizesAsync();  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Create a query.   
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURLAsync(url);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    byte[] urlContents = await GetURLContentsAsync(url);  
  
            //    // The previous line abbreviates the following two assignment statements.  
            //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
            //    //byte[] urlContents = await getContentsTask;  
  
            //    DisplayResults(url, urlContents);  
  
            //    // Update the total.            
            //    total += urlContents.Length;  
            //}  
  
            // Display the total count for all of the websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        private async Task<int> ProcessURLAsync(string url)  
        {  
            var byteArray = await GetURLContentsAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private async Task<byte[]> GetURLContentsAsync(string url)  
        {  
            // The downloaded resource ends up in the variable named content.  
            var content = new MemoryStream();  
  
            // Initialize an HttpWebRequest for the current URL.  
            var webReq = (HttpWebRequest)WebRequest.Create(url);  
  
            // Send the request to the Internet resource and wait for  
            // the response.  
            using (WebResponse response = await webReq.GetResponseAsync())  
            {  
                // Get the data stream that is associated with the specified url.  
                using (Stream responseStream = response.GetResponseStream())  
                {  
                    await responseStream.CopyToAsync(content);  
                }  
            }  
  
            // Return the result as a byte array.  
            return content.ToArray();  
  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
  
        }  
    }  
}  
```  
  
## <a name="example"></a>Пример  
 В следующем коде показано расширение для проекта, использующее метод `HttpClient.GetByteArrayAsync` для скачивания содержимого из Интернета.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_HttpClient_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // One-step async call.  
            await SumPageSizesAsync();  
  
            // Two-step async call.  
            //Task sumTask = SumPageSizesAsync();  
            //await sumTask;  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Declare an HttpClient object and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client = new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create a query.  
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURL(url, client);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
            //    // The previous line abbreviates the following two assignment  
            //    // statements.  
            //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
            //    byte[] urlContent = await getContentTask;  
  
            //    DisplayResults(url, urlContent);  
  
            //    // Update the total.  
            //    total += urlContent.Length;  
            //}  
  
            // Display the total count for all of the web addresses.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        async Task<int> ProcessURL(string url, HttpClient client)  
        {  
            byte[] byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each web site. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>  
 [Walkthrough: Accessing the Web by Using async and await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) (Пошаговое руководство. Обращение к веб-сайтам с помощью async и await в C#)
