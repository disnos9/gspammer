# GSpammer

This quick guide will go over how to setup GSpammer on your own with Mailgun. Please note that we are not responsible for anything you do with GSpammer.



\*We are not going over the process of obtaining an API key or getting a domain.\*

**Step 1: Choose your language**

Java

```java
import java.io.File;
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.JsonNode;
import com.mashape.unirest.http.Unirest;
import com.mashape.unirest.http.exceptions.UnirestException;
public class MGSample {
	 // ...
	public static JsonNode sendSimpleMessage() throws UnirestException {
		HttpResponse<JsonNode> request = Unirest.post("https://api.mailgun.net/v3/" + YOUR_DOMAIN_NAME + "/messages"),
			.basicAuth("api", API_KEY)
			.queryString("from", "Excited User <USER@YOURDOMAIN.COM>")
			.queryString("to", "artemis@example.com")
			.queryString("subject", "hello")
			.queryString("text", "testing")
			.asJson();
		return request.getBody();
	}
}
```

Python

```python
def send_simple_message():
	return requests.post(
		"https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/messages",
		auth=("api", "YOUR_API_KEY"),
		data={"from": "Excited User <mailgun@YOUR_DOMAIN_NAME>",
			"to": ["bar@example.com", "YOU@YOUR_DOMAIN_NAME"],
			"subject": "Hello",
			"text": "Testing some Mailgun awesomeness!"})
```

PHP

```php
# Include the Autoloader (see "Libraries" for install instructions)
require 'vendor/autoload.php';
use Mailgun\Mailgun;
# Instantiate the client.
$mgClient = new Mailgun('YOUR_API_KEY');
$domain = "YOUR_DOMAIN_NAME";
# Make the call to the client.
$result = $mgClient->sendMessage($domain, array(
	'from'	=> 'Excited User <mailgun@YOUR_DOMAIN_NAME>',
	'to'	=> 'Baz <YOU@YOUR_DOMAIN_NAME>',
	'subject' => 'Hello',
	'text'	=> 'Testing some Mailgun awesomeness!'
));
```

C#

```csharp
using System;
using System.IO;
using RestSharp;
using RestSharp.Authenticators;
public class SendSimpleMessageChunk
{
	public static void Main (string[] args)
	{
		Console.WriteLine (SendSimpleMessage ().Content.ToString ())
	}
	public static IRestResponse SendSimpleMessage ()
	{
		RestClient client = new RestClient ();
		client.BaseUrl = new Uri ("https://api.mailgun.net/v3");"
		client.Authenticator ='
			new HttpBasicAuthenticator ("api",
				"YOUR_API_KEY");
		RestRequest request = new RestRequest ();
		request.AddParameter ("domain", "YOUR_DOMAIN_NAME", ParameterType.UrlSegment);
		request.Resource = "{domain}/messages";
		request.AddParameter ("from", "Excited User <mailgun@YOUR_DOMAIN_NAME>");
		request.AddParameter ("to", "bar@example.com");
		request.AddParameter ("to", "YOU@YOUR_DOMAIN_NAME");
		request.AddParameter ("subject", "Hello");
		request.AddParameter ("text", "Testing some Mailgun awesomeness!");
		request.Method = Method.POST;
		return client.Execute (request);
	}
}
```

Go

```go
func SendSimpleMessage(domain, apiKey string) (string, error) {
	mg := mailgun.NewMailgun(domain, apiKey, publicApiKey)
	m := mg.NewMessage(
		"Excited User <mailgun@YOUR_DOMAIN_NAME>",
		"Hello",
		"Testing some Mailgun awesomeness!",
		"YOU@YOUR_DOMAIN_NAME",
	)
	_, id, err := mg.Send(m)
	return id, err
}
```

**If you don't see the code that's in YOUR programming lanugage, ask ChatGPT to change it.**

**Step 2:**

Set your domain name, recipent, and the delay. Thanks <3



