# go-alpha-vantage
A comprehensive Alpha Vantage client written in Go.
## Usage
Instructions on how to get the most of the client.
### API-Key
In order to use the client you need a valid Alpha-Vantage API-Key, which you can get on their website.

Once you have an API-Key, store it in the environment-variable `ALPHA_VANTAGE_API_KEY`. If the key is not set, no request will be possible

### Connection
Before you can send a request you need to create an `AlphaVantageConnection` by calling the `NewAlphaVantageConnection` factory from the `connection` package.

### Request
Once you have a `connection` you can create an `AlphaVantageRequest` and send it with `connection.Request`. For each Alpha-Vantage function there exists one preconfigured implementation of the `AlphaVantageRequest` interface.

In order to send a request for daily timeseries data you may do the following:
```Go
con := connection.NewAlphaVantageConnection()
request := DailyAdjustedRequest{
    Symbol:     "IBM",
    OutputSize: FULL,
}
resp, err := connection.Request(&request)
if err != nil {
    t.Error(err)
    return
}
dailyAdjResp := resp.(*DailyAdjustedResponse)
for time, ohlcv := range dailyAdjResp.Timeseries {
    //Access the candles
}
```

For more examples you may also take a look at the tests