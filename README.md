# CoinspotAPI-CSharp
I've been tinkering around with the Coinspot (Australian Crypto Exchange) API lately and became frustrated with the lack of C# documentation or implementations.. By rabidly googling I eventually came up with my own implementation that seems to work for *MOST* of the Queries..

## Usage 
- Include the .cs in your project
- Examples of usage below
- All responses are in JSON as per the API docs here: https://www.coinspot.com.au/api

##### I believe Coinspot truncates any decimal places that exceed their limits.. ie if you put 1.0000001 and they limit to 6 decimal places, you are putting an order for 1.0

#### Custom URL query
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.APIQuery(apiKey, apiSecret, "/ro/my/balances"));`

#### Custom URL query2
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.APIQuery(apiKey, apiSecret, "/ro/my/transactions"));`

#### List open orders - if you don't include a coin type it will get all open orders
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListOpenOrders(apiKey, apiSecret, "BTC"));`

#### List Deposit/Receive Address for specified coins
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.MyDepositAddress(apiKey, apiSecret, "BTC"));`

#### Quickbuy/QuickSell **THESE DO NOT SEEM TO WORK AS INTENDED**
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.QuickBuyQuote(apiKey, apiSecret, "BTC",5));`

#### List Account Balances
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListMyBalances(apiKey, apiSecret));`

#### List Market Orders
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListMyOrders(apiKey, apiSecret));`

#### Place market buy order -- example interpretation following..
`var response = await CoinspotAPI.CoinspotAPI.PlaceBuyOrder(apiKey, apiSecret, "XRP", 5, 2.00000001f);
Debug.WriteLine(response);
dynamic data = JObject.Parse(response);
 data.id = id`

#### Place Sell order
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.PlaceSellOrder(apiKey, apiSecret,"XRP", 4.30603262, 2.650000));`

#### Cancel Sell order, using data.id from above.
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.CancelBuyOrder(apiKey, apiSecret, data.id));`

#### List Transaction History (all)
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListTransactionHistory(apiKey, apiSecret));`

#### List Transaction History (specific Coin)
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListTransactionHistory(apiKey, apiSecret, "DOGE"));`
  
#### Below, self explanitory.
`Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListMyReferralPayments(apiKey, apiSecret));
Debug.WriteLine(await CoinspotAPI.CoinspotAPI.SendReceiveTransactions(apiKey, apiSecret));
Debug.WriteLine(await CoinspotAPI.CoinspotAPI.ListMyAffiliatePayments(apiKey, apiSecret));`
