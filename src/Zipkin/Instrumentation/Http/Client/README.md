# Zipkin instrumentation for PSR18 HTTP Client

This component contains the instrumentation for the standard [PSR18 HTTP clients](https://www.php-fig.org/psr/psr-18/).

## Getting started

Before using this library, make sure the interfaces for PSR18 HTTP client are installed:

```bash
composer require psr/http-client
```

## Usage

In this example we use Guzzle 7 but any HTTP client supporting PSR18 clients will work.

```php
use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;
use Zipkin\Instrumentation\Http\Client\Client as ZipkinClient;
use Zipkin\Instrumentation\Http\Client\ClientTracing;

$tracing = TracingBuilder::create()
            ->havingLocalServiceName('my_service')
            ->build();

$httpClientTracing = new ClientTracing($tracing);
...

$httpClient = new ZipkinClient(new Client, $httpClientTracing);
$request = new Request('POST', 'http://myurl.test');
$response = $httpClient->sendRequest($request);
```
