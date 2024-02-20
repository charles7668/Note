# HttpClient 問題記錄

這裡記錄了一些使用 `HttpClient` 的可能遇到的問題

- [HttpClient 問題記錄](#httpclient-問題記錄)
- [請求無回應](#請求無回應)
- [參考](#參考)

# 請求無回應

在測試 `HttpClient` 進行請求時 , 可能會簡單像這樣使用

```C#
using var client = new HttpClient();
var content = await client.GetStringAsync("http://example.com");

Console.WriteLine(content);
```

在很多網站上確實不會遇到問題, 但某些網站可能會發現遲遲無法獲得回應(但在瀏覽器上瀏覽網址正常) , 最終導致 timeout

會發生這樣問題的主要原因是缺失了某些請求 Header , 如下範例 , 而且這些 Header 有時缺一不可 , 即時刪掉任何一段都可能會導致 timeout

```C#
client.DefaultRequestHeaders.Add("User-Agent",
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36");
client.DefaultRequestHeaders.Add("Accept", "*/*");
client.DefaultRequestHeaders.Add("Accept-Encoding", "gzip, deflate, br");
client.DefaultRequestHeaders.Add("Accept-Language", "zh-TW,zh;q=0.8,en-US;q=0.5,en;q=0.3");
```

另外比較重要的是 `User-Agent` 的部分 , 對於某些特定的 `User-Agent` 可以不需要其它`Header` , 但對於某些`User-Agent` 卻需要完整的`Header` , 具體使用上可能需要根據網站來進行個別處理

# 參考

- [http - Why can the C# HttpClient not call this URL (always times out)? - Stack Overflow](https://stackoverflow.com/questions/48790438/why-can-the-c-sharp-httpclient-not-call-this-url-always-times-out)
