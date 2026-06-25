[update-readmes]   Mode: rewrite — migrating to template structure...
# ccxt

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/ccxt)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install


The easiest way to install the CCXT library is to use a package manager:

- [ccxt in **NPM**](https://www.npmjs.com/package/ccxt) (JavaScript / Node v7.6+)
- [ccxt in **PyPI**](https://pypi.python.org/pypi/ccxt) (Python 3.7.0+)
- [ccxt in **Packagist/Composer**](https://packagist.org/packages/ccxt/ccxt) (PHP 8.1+)
- [ccxt in **Nuget**](https://www.nuget.org/packages/ccxt) (netstandard 2.0)
- [ccxt in **GO**](https://pkg.go.dev/github.com/ccxt/ccxt/go/v4)
- [ccxt in **Java**](https://central.sonatype.com/artifact/io.github.ccxt/ccxt) (Java 21+, Gradle)

This library is shipped as an all-in-one module implementation with minimalistic dependencies and requirements:

- [js/](https://github.com/ccxt/ccxt/blob/master/js/) in JavaScript
- [python/](https://github.com/ccxt/ccxt/blob/master/python/) in Python (generated from TS)
- [php/](https://github.com/ccxt/ccxt/blob/master/php/) in PHP (generated from TS)
- [cs/](https://github.com/ccxt/ccxt/blob/master/cs/)  in C# (generated from TS)
- [go/](https://github.com/ccxt/ccxt/blob/master/go/)  in Go (generated from TS)
- [java/](https://github.com/ccxt/ccxt/blob/master/java/) in Java (generated from TS)

You can also clone it into your project directory from [ccxt GitHub repository](https://github.com/ccxt/ccxt):

```shell
git clone https://github.com/ccxt/ccxt.git  # including 1GB of commit history

# or

git clone https://github.com/ccxt/ccxt.git --depth 1  # avoid downloading 1GB of commit history
```

### JavaScript (NPM)

JavaScript version of CCXT works in both Node and web browsers. Requires ES6 and `async/await` syntax support (Node 7.6.0+). When compiling with Rspack (or Webpack) and Babel, make sure it is [not excluded](https://github.com/ccxt/ccxt/issues/225#issuecomment-331905178) in your `babel-loader` config.

[ccxt in **NPM**](https://www.npmjs.com/package/ccxt)

```shell
npm install ccxt
```

```JavaScript
//cjs
var ccxt = require ('ccxt')
console.log (ccxt.exchanges) // print all available exchanges
```
```Javascript
//esm
import {version, exchanges} from 'ccxt';
console.log(version, Object.keys(exchanges));
```

### JavaScript (for use with the `<script>` tag):

All-in-one browser bundle (dependencies included), served from a CDN of your choice:

* jsDelivr: https://cdn.jsdelivr.net/npm/ccxt@4.5.59/dist/ccxt.browser.min.js
* unpkg: https://unpkg.com/ccxt@4.5.59/dist/ccxt.browser.min.js

CDNs are not updated in real-time and may have delays. Defaulting to the most recent version without specifying the version number is not recommended. Please, keep in mind that we are not responsible for the correct operation of those CDN servers.

```HTML
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/ccxt@4.5.59/dist/ccxt.browser.min.js"></script>
```

Creates a global `ccxt` object:

```JavaScript
console.log (ccxt.exchanges) // print all available exchanges
```

### Python

[ccxt in **PyPI**](https://pypi.python.org/pypi/ccxt)

```shell
pip install ccxt
```

```Python
import ccxt
print(ccxt.exchanges) # print a list of all available exchange classes
```

The library supports concurrent asynchronous mode with asyncio and async/await in Python 3.7.0+

```Python
import ccxt.async_support as ccxt # link against the asynchronous version of ccxt
```

#### orjson support

CCXT also supports `orjson` for parsing JSON since it is much faster than the builtin library. This is especially important when using websockets because some exchanges return big messages that need to be parsed and dispatched as quickly as possible.

However, `orjson` is not enabled by default because it is not supported by every python interpreter. If you want to opt-in, you just need to install it (`pip install orjson`) on your local environment. CCXT will detect the installion and pick it up automatically.

#### ECDSA Support

Some exchanges, such as Hyperliquid, Binance, and Paradex use **ECDSA** for request signing.
By default, CCXT includes a pure Python ECDSA implementation that ensures compatibility across all environments. However, this implementation may not meet the performance requirements of latency-sensitive applications.

To address this, CCXT also supports the Coincurve library, which dramatically reduces signing time from approximately 45 ms to under 0.05 ms.

For optimal performance, we recommend installing Coincurve via:

```
pip install coincurve
```

Once installed, CCXT will automatically detect and use it.

### PHP

[ccxt in PHP with **Packagist/Composer**](https://packagist.org/packages/ccxt/ccxt) (PHP 8.1+)

It requires common PHP modules:

- cURL
- mbstring (using UTF-8 is highly recommended)
- PCRE
- iconv
- gmp

```PHP
include "ccxt.php";
var_dump (\ccxt\Exchange::$exchanges); // print a list of all available exchange classes
```

The library supports concurrent asynchronous mode using tools from [ReactPHP](https://reactphp.org/) in PHP 8.1+. Read the [Manual](https://github.com/ccxt/ccxt/wiki/) for more details.

### .net/C#

[ccxt in C# with **Nuget**](https://www.nuget.org/packages/ccxt) (netstandard 2.0 and netstandard 2.1)
```c#
using ccxt;
Console.WriteLine(ccxt.Exchanges) // check this later
```

### Go

[ccxt in GO with **PKG**](https://pkg.go.dev/github.com/ccxt/ccxt/go/v4)

```shell
go install github.com/ccxt/ccxt/go/v4@latest
```

```Go
import "ccxt"
fmt.Println(ccxt.Exchanges)
```

### Java

Java version of CCXT requires Java 21+ and uses Gradle as its build system.

Add the CCXT library as a local dependency in your `build.gradle.kts`:

```kotlin
dependencies {
    implementation("io.github.ccxt:ccxt:4.5.52")
}
```

Or clone and build from source:

```shell
git clone https://github.com/ccxt/ccxt.git --depth 1
cd ccxt/java
./gradlew :lib:build
```

```Java
import io.github.ccxt.exchanges.Binance;
import io.github.ccxt.types.Ticker;

Binance exchange = new Binance();
exchange.loadMarkets(false);

Ticker ticker = exchange.fetchTicker("BTC/USDT");
System.out.println(ticker.symbol + " " + ticker.last);
```

Each exchange has its own typed subclass with strongly-typed return values. Every typed method ships both a blocking sync and a non-blocking `CompletableFuture`-returning async overload — pick the idiom that fits your call site:

```Java
// Sync — blocks until the response arrives
Ticker ticker = exchange.fetchTicker("BTC/USDT");

// Async — returns immediately, completes when the response arrives
CompletableFuture<Ticker> future = exchange.fetchTickerAsync("BTC/USDT", null);
future.thenAccept(t -> System.out.println(t.last));
```

WebSocket support is available via the pro exchange classes, with the same sync/async symmetry — `watchTicker` blocks for one update; `watchTickerAsync` returns a `CompletableFuture<Ticker>` you can compose:

```Java
import io.github.ccxt.exchanges.pro.Binance;

var exchange = new Binance();
exchange.loadMarkets(false);

// Sync — blocks for one update
Ticker tick = exchange.watchTicker("BTC/USDT");

// Async — returns a typed CompletableFuture (composable with allOf, anyOf, etc.)
CompletableFuture<Ticker> future = exchange.watchTickerAsync("BTC/USDT", null);
```

See [java/examples/](https://github.com/ccxt/ccxt/tree/master/java/examples) for more usage examples.

### Docker

You can get CCXT installed in a container along with all the supported languages and dependencies. This may be useful if you want to contribute to CCXT (e.g. run the build scripts and tests — please see the [Contributing](https://github.com/ccxt/ccxt/blob/master/CONTRIBUTING.md) document for the details on that).

Using `docker-compose` (in the cloned CCXT repository):

```shell
docker-compose run --rm ccxt
```

You don't need the Docker image if you're not going to develop CCXT. If you just want to use CCXT – just install it as a regular package into your project.

---

## Usage


### Intro

The CCXT library consists of a public part and a private part. Anyone can use the public part immediately after installation. Public APIs provide unrestricted access to public information for all exchange markets without the need to register a user account or have an API key.

Public APIs include the following:

- market data
- instruments/trading pairs
- price feeds (exchange rates)
- order books
- trade history
- tickers
- OHLC(V) for charting
- other public endpoints

In order to trade with private APIs you need to obtain API keys from an exchange's website. It usually means signing up to the exchange and creating API keys for your account. Some exchanges require personal info or identification. Sometimes verification may be necessary as well. In this case you will need to register yourself, this library will not create accounts or API keys for you. Some exchanges expose API endpoints for registering an account, but most exchanges don't. You will have to sign up and create API keys on their websites.

Private APIs allow the following:

- manage personal account info
- query account balances
- trade by making market and limit orders
- deposit and withdraw fiat and crypto funds
- query personal orders
- get ledger history
- transfer funds between accounts
- use merchant services

This library implements full public and private REST and WebSocket APIs for all exchanges in TypeScript, JavaScript, PHP and Python.

The CCXT library supports both camelcase notation (preferred in TypeScript and JavaScript) and underscore notation (preferred in Python and PHP), therefore all methods can be called in either notation or coding style in any language.

```JavaScript
// both of these notations work in JavaScript/Python/PHP
exchange.methodName ()  // camelcase pseudocode
exchange.method_name () // underscore pseudocode
```

Read the [Manual](https://github.com/ccxt/ccxt/wiki/) and see [examples](https://github.com/ccxt/ccxt/tree/master/examples) for more details.

### JavaScript

**CCXT now supports ESM and CJS modules**

#### CJS

```JavaScript
// cjs example
'use strict';
const ccxt = require ('ccxt');

(async function () {
    let kraken    = new ccxt.kraken ()
    let bitfinex  = new ccxt.bitfinex ({ verbose: true })
    let huobipro  = new ccxt.huobipro ()
    let okcoinusd = new ccxt.okcoin ({
        apiKey: 'YOUR_PUBLIC_API_KEY',
        secret: 'YOUR_SECRET_PRIVATE_KEY',
    })

    const exchangeId = 'binance'
        , exchangeClass = ccxt[exchangeId]
        , exchange = new exchangeClass ({
            'apiKey': 'YOUR_API_KEY',
            'secret': 'YOUR_SECRET',
        })

    console.log (kraken.id,    await kraken.loadMarkets ())
    console.log (bitfinex.id,  await bitfinex.loadMarkets  ())
    console.log (huobipro.id,  await huobipro.loadMarkets ())

    console.log (kraken.id,    await kraken.fetchOrderBook (kraken.symbols[0]))
    console.log (bitfinex.id,  await bitfinex.fetchTicker ('BTC/USD'))
    console.log (huobipro.id,  await huobipro.fetchTrades ('ETH/USDT'))

    console.log (okcoinusd.id, await okcoinusd.fetchBalance ())

    // sell 1 BTC/USD for market price, sell a bitcoin for dollars immediately
    console.log (okcoinusd.id, await okcoinusd.createMarketSellOrder ('BTC/USD', 1))

    // buy 1 BTC/USD for $2500, you pay $2500 and receive ฿1 when the order is closed
    console.log (okcoinusd.id, await okcoinusd.createLimitBuyOrder ('BTC/USD', 1, 2500.00))

    // pass/redefine custom exchange-specific order params: type, amount, price or whatever
    // use a custom order type
    bitfinex.createLimitSellOrder ('BTC/USD', 1, 10, { 'type': 'trailing-stop' })

}) ();
```
#### ESM

```Javascript
//esm example
import {version, binance} from 'ccxt';

console.log(version);
const exchange = new binance();
const ticker = await exchange.fetchTicker('BTC/USDT');
console.log(ticker);
```

### Python

```Python
# coding=utf-8

import ccxt

hitbtc   = ccxt.hitbtc({'verbose': True})
bitmex   = ccxt.bitmex()
huobipro = ccxt.huobipro()
exmo     = ccxt.exmo({
    'apiKey': 'YOUR_PUBLIC_API_KEY',
    'secret': 'YOUR_SECRET_PRIVATE_KEY',
})
kraken = ccxt.kraken({
    'apiKey': 'YOUR_PUBLIC_API_KEY',
    'secret': 'YOUR_SECRET_PRIVATE_KEY',
})

exchange_id = 'binance'
exchange_class = getattr(ccxt, exchange_id)
exchange = exchange_class({
    'apiKey': 'YOUR_API_KEY',
    'secret': 'YOUR_SECRET',
})

hitbtc_markets = hitbtc.load_markets()

print(hitbtc.id, hitbtc_markets)
print(bitmex.id, bitmex.load_markets())
print(huobipro.id, huobipro.load_markets())

print(hitbtc.fetch_order_book(hitbtc.symbols[0]))
print(bitmex.fetch_ticker('BTC/USD'))
print(huobipro.fetch_trades('LTC/USDT'))

print(exmo.fetch_balance())

# sell one ฿ for market price and receive $ right now
print(exmo.id, exmo.create_market_sell_order('BTC/USD', 1))

# limit buy BTC/EUR, you pay €2500 and receive ฿1  when the order is closed
print(exmo.id, exmo.create_limit_buy_order('BTC/EUR', 1, 2500.00))

# pass/redefine custom exchange-specific order params: type, amount, price, flags, etc...
kraken.create_market_buy_order('BTC/USD', 1, {'trading_agreement': 'agree'})
```

### PHP

```PHP
include 'ccxt.php';

$poloniex = new \ccxt\poloniex ();
$bittrex  = new \ccxt\bittrex  (array ('verbose' => true));
$quoinex  = new \ccxt\quoinex   ();
$zaif     = new \ccxt\zaif     (array (
    'apiKey' => 'YOUR_PUBLIC_API_KEY',
    'secret' => 'YOUR_SECRET_PRIVATE_KEY',
));
$hitbtc   = new \ccxt\hitbtc   (array (
    'apiKey' => 'YOUR_PUBLIC_API_KEY',
    'secret' => 'YOUR_SECRET_PRIVATE_KEY',
));

$exchange_id = 'binance';
$exchange_class = "\\ccxt\\$exchange_id";
$exchange = new $exchange_class (array (
    'apiKey' => 'YOUR_API_KEY',
    'secret' => 'YOUR_SECRET',
));

$poloniex_markets = $poloniex->load_markets ();

var_dump ($poloniex_markets);
var_dump ($bittrex->load_markets ());
var_dump ($quoinex->load_markets ());

var_dump ($poloniex->fetch_order_book ($poloniex->symbols[0]));
var_dump ($bittrex->fetch_trades ('BTC/USD'));
var_dump ($quoinex->fetch_ticker ('ETH/EUR'));
var_dump ($zaif->fetch_ticker ('BTC/JPY'));

var_dump ($zaif->fetch_balance ());

// sell 1 BTC/JPY for market price, you pay ¥ and receive ฿ immediately
var_dump ($zaif->id, $zaif->create_market_sell_order ('BTC/JPY', 1));

// buy BTC/JPY, you receive ฿1 for ¥285000 when the order closes
var_dump ($zaif->id, $zaif->create_limit_buy_order ('BTC/JPY', 1, 285000));

// set a custom user-defined id to your order
$hitbtc->create_order ('BTC/USD', 'limit', 'buy', 1, 3000, array ('clientOrderId' => '123'));
```

### .net/C#

```C#
using ccxt; // importing ccxt
namespace Project;
class Project {
    public async static Task CreateOrder() {
        var exchange = new Binance();
        exchange.apiKey = "my api key";
        exchange.secret = "my secret";
        // always use the capitalized method (CreateOrder instead of createOrder)
        var order = await exchange.CreateOrder("BTC/USDT", "limit", "buy", 1, 50);
        Console.WriteLine("Placed Order, order id: " + order.id);
    }
}
```

### Go

```Go
package main
import (
	"github.com/ccxt/ccxt/go/v4/go"
	"fmt"
)

func main() {
	exchange := ccxt.NewBinance(map[string]interface{}{
		"apiKey": "MY KEY",
		"secret": "MY SECRET",
	})
	orderParams := map[string]interface{}{
		"clientOrderId": "myOrderId68768678",
	}

    exchange.LoadMarkets()

	order, err := exchange.CreateOrder("BTC/USDT", "limit", "buy", 0.001, ccxt.WithCreateOrderPrice(6000), ccxt.WithCreateOrderParams(orderParams))
	if err != nil {
		if ccxtError, ok := err.(*ccxt.Error); ok {
			if ccxtError.Type == "InvalidOrder" {
				fmt.Println("Invalid order")
			} else {
				fmt.Println("Some other error")
			}
		}
	} else {
		fmt.Println(*order.Id)
	}


    // fetching OHLCV
	ohlcv, err := exchange.FetchOHLCV("BTC/USDT", ccxt.WithFetchOHLCVTimeframe("5m"), ccxt.WithFetchOHLCVLimit(100))

	if err != nil {
		fmt.Println("Error: ", err)
	} else {
		fmt.Println("Got OHLCV!")
	}
}
```

#### Optional parameters

Unlike Javascript/Python/PHP/C# Go does not support "traditional" optional parameters like `function a(optional = false)`. However, the CCXT language and structure have some methods with optional params, and since the Go language is transpiled from the Typescript source, we had to find a way of representing them.

We have decided to "go" (pun intended) with Option structs and the `WithX` methods.

For example, this function `FetchMyTrades` supports 4 different "optional" parameters, symbol, since, limit, and params.

```Golang
func (this *Binance) FetchMyTrades(options ...FetchMyTradesOptions) ([]Trade, error)
```

And we can provide them by doing

```Golang
trades, error := exchange.FetchMyTrades(ccxt.withFetchMyTradesSymbol("BTC/USDT"), ccxt.WithFetchOHLCVLimit(5), ccxt.WithFetchMyTradesParams(orderParams))
```

Lastly, just because the signature dictates that some argument like `symbol` is optional, it will depend from exchange to exchange and you might need to provide it to avoid getting a `SymbolRequired` error.

You can check different examples in the `examples/go` folder.

### Java

```Java
import io.github.ccxt.exchanges.Kraken;
import io.github.ccxt.exchanges.Bitfinex;
import io.github.ccxt.exchanges.Binance;
import io.github.ccxt.types.*;

import java.util.HashMap;
import java.util.Map;

public class Example {
    public static void main(String[] args) {
        // Create exchange instances
        Kraken kraken = new Kraken();
        Bitfinex bitfinex = new Bitfinex();

        Map<String, Object> config = new HashMap<>();
        config.put("apiKey", "YOUR_API_KEY");
        config.put("secret", "YOUR_SECRET");
        Binance binance = new Binance(config);

        // Load markets
        kraken.loadMarkets(false);
        binance.loadMarkets(false);

        // Public API
        OrderBook orderBook = kraken.fetchOrderBook("BTC/USDT");
        Ticker ticker = bitfinex.fetchTicker("BTC/USD");
        System.out.println(ticker.symbol + " last=" + ticker.last);

        // Fetch OHLCV
        var candles = binance.fetchOHLCV("BTC/USDT", "1h", null, 10L, null);
        System.out.println("Got " + candles.size() + " candles");

        // Private API (requires API keys)
        Balances balance = binance.fetchBalance();
        System.out.println("BTC free: " + balance.free.get("BTC"));

        // Place a limit buy order
        Order order = binance.createLimitBuyOrder("BTC/USDT", 0.001, 50000.0);
        System.out.println("Order id: " + order.id + " status: " + order.status);

        // Cancel it
        binance.cancelOrder(order.id, "BTC/USDT", null);
    }
}
```

#### Async

All methods are also available as async variants returning `CompletableFuture`:

```Java
import java.util.concurrent.CompletableFuture;

// Fire multiple requests concurrently
CompletableFuture<Ticker> btc = binance.fetchTickerAsync("BTC/USDT", null);
CompletableFuture<Ticker> eth = binance.fetchTickerAsync("ETH/USDT", null);
CompletableFuture.allOf(btc, eth).join();
System.out.println("BTC: " + btc.get().last + " ETH: " + eth.get().last);
```

#### Error handling

Typed sync methods throw the underlying ccxt error directly — no `CompletionException`
unwrap needed. Catch exceptions in standard JDK order (most-specific first), like you
would with any other Java library:

```Java
import io.github.ccxt.errors.*;
import io.github.ccxt.exchanges.Binance;
import io.github.ccxt.types.Order;

Binance binance = new Binance(Map.of("apiKey", "...", "secret", "..."));
try {
    Order order = binance.createOrder("BTC/USDT", "limit", "buy", 0.001, 50000.0);
} catch (InsufficientFunds e) {
    // user error — show balance, don't retry
} catch (InvalidOrder e) {                        // covers OrderNotFound, DuplicateOrderId, …
    // user error — fix params
} catch (AuthenticationError e) {                 // covers PermissionDenied, AccountSuspended
    // refresh credentials
} catch (RateLimitExceeded | DDoSProtection e) {  // multi-catch (Java 7+)
    Thread.sleep(30_000);
} catch (NetworkError e) {                        // RequestTimeout, ExchangeNotAvailable, …
    Thread.sleep(2_000);                          // transient — retry
} catch (ExchangeError e) {                       // any other exchange-side error
    // exchange refused
} catch (BaseError e) {                           // ccxt catch-all
    // unknown ccxt error
}
```

For async methods, `CompletableFuture` wraps thrown errors in `CompletionException`
(JDK behaviour). Use `Helpers.unwrap()` inside `.exceptionally(...)` to peel the wrap
and pattern-match the real cause:

```Java
import io.github.ccxt.Helpers;

binance.createOrderAsync("BTC/USDT", "limit", "buy", 0.001, 50000.0)
    .thenAccept(order -> log.info("placed " + order.id))
    .exceptionally(throwable -> {
        Throwable cause = Helpers.unwrap(throwable);
        return switch (cause) {
            case InsufficientFunds    e -> { notifyUser(e); yield null; }
            case AuthenticationError  e -> { refreshCreds(); yield null; }
            case RateLimitExceeded    e -> { scheduleRetry(); yield null; }
            case NetworkError         e -> { scheduleRetry(); yield null; }
            case BaseError            e -> { log.error("ccxt", e); yield null; }
            default -> throw new java.util.concurrent.CompletionException(cause);
        };
    });
```

The full hierarchy lives under `io.github.ccxt.errors` — see the [Error Handling
section of the Manual](https://github.com/ccxt/ccxt/wiki/Manual#error-handling)
for the complete tree (NetworkError vs ExchangeError, retry-safe vs user-error
categories, etc.).

#### WebSocket

WebSocket support is available via the pro exchange classes:

```Java
import io.github.ccxt.Exchange;
import io.github.ccxt.exchanges.pro.Binance;

import java.util.concurrent.TimeUnit;

Exchange exchange = new Binance();
exchange.loadMarkets().join();

// Stream live ticker updates
for (int i = 0; i < 10; i++) {
    Object ticker = exchange.watchTicker("BTC/USDT").get(30, TimeUnit.SECONDS);
    System.out.println(ticker);
}
```

You can check different examples in the `java/examples` folder.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/ccxt`](https://github.com/Interested-Deving-1896/ccxt) and mirrored through:

```
Interested-Deving-1896/ccxt  ──►  OpenOS-Project-OSP/ccxt  ──►  OpenOS-Project-Ecosystem-OOC/ccxt
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
<!-- License not detected — add a LICENSE file to this repo. -->
<!-- AI:end:license -->
