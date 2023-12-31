## Scrape.do C# Example

<p align="center">
    <img style="background-color:white;" src="https://scrape.do/images/scrape-logo.svg" alt="scrape.do" width="200">
</p>

### Web Scraper API

- Best Rotating Proxy & [Scraping API](https://scrape.do) Alternative.
- ⚠ Please read the [documents](https://docs.scrape.do) first.

#### You can send request to any webpages with proxy gateway & web api provided by scrape.do. As you can see from the example, this takes only few lines of code

### You can see in example ([Program.cs](/Program.cs))

```C#
private static string CreateRequestUrl(string targetUrl) {
	if (string.IsNullOrEmpty(_apiToken)) throw new Exception("API_TOKEN cannot be empty!");

	string url = $ "http://api.scrape.do?token={_apiToken}";

	if (_jsRender) url += "&render=true";
	if (_superProxy) url += "&super=true";
	if (!string.IsNullOrEmpty(_geoCode)) url += $ "&geoCode={_geoCode}";
	if (!string.IsNullOrEmpty(_session)) url += $ "&session={_session}";

	return $ "{url}&url={targetUrl}";
}
```

```C#
static void Main(string[] args) {

	HttpClientHandler handler = new HttpClientHandler() {
		AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate
	};

	var client = new HttpClient(handler);

	string requestUrl = CreateRequestUrl("https://example.com");
	var response = client.GetAsync(requestUrl).Result;

	Console.WriteLine("Status Code : {0} ", response.StatusCode);
	Console.WriteLine("HTML : \n{0}", response.Content.ReadAsStringAsync().Result);
}
```
