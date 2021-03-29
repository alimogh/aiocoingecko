# AIOCoinGecko
<p align="center">
<img src="https://user-images.githubusercontent.com/64792903/112778422-2bffd480-904d-11eb-83ee-edecd6599f1f.png">
	💲💲💲 Asynchronous wrapper for the CoinGecko API written in Python 3.7 with asyncio and aiohttp.
</p>


## 💿 Installation

```
💲 pip install coingecko
```

## 💻 How use?
```python3
from coingecko import CoinGeckoAPI
import asyncio


async def main():
    cg_client = CoinGeckoAPI()
    eth_price = await cg_client.get_price(ids='bitcoin')
    print(eth_price)
    await cg_client.close()

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

>>> {'bitcoin': {'usd': 55250}}
```
#### More examples...
```python3
>>> eth_price = await cg_client.get_price(ids='bitcoin')
{'bitcoin': {'usd': 55402}}
>>> more_tokens_price = await cg_client.get_price(ids='venus,pancakeswap-token,bakerytoken', vs_currencies='usd,rub')
{'pancakeswap-token': {'usd': 16.21, 'rub': 1228.86}, 'bakerytoken': {'usd': 1.1, 'rub': 83.09}, 'venus': {'usd': 47.72, 'rub': 3616.73}}
>>> uniswap_price = await cg_client.get_token_price(contract_addresses='0x1f9840a85d5af5bf1d1762f925bdaddc4201f984')
{'0x1f9840a85d5af5bf1d1762f925bdaddc4201f984': {'usd': 27.99}}
>>> btc_markets = await cg_client.get_coins_markets(ids='bitcoin', price_change_percentage='1h,24h,7d,30d')
[{'id': 'bitcoin', 'symbol': 'btc', 'name': 'Bitcoin', 'image': 'https://assets.coingecko.com/coins/images/1/large/bitcoin.png?1547033579', 'current_price': 55521, 'market_cap': 1034211314094, 'market_cap_rank': 1, 'fully_diluted_valuation': 1163441273807, 'total_volume': 49131259246, 'high_24h': 56498, 'low_24h': 54719, 'price_change_24h': -324.07620506, 'price_change_percentage_24h': -0.58032, 'market_cap_change_24h': -8829421386.302612, 'market_cap_change_percentage_24h': -0.84651, 'circulating_supply': 18667412.0, 'total_supply': 21000000.0, 'max_supply': 21000000.0, 'ath': 61712, 'ath_change_percentage': -10.29018, 'ath_date': '2021-03-13T20:49:26.606Z', 'atl': 67.81, 'atl_change_percentage': 81543.45636, 'atl_date': '2013-07-06T00:00:00.000Z', 'roi': None, 'last_updated': '2021-03-29T02:34:57.498Z', 'price_change_percentage_1h_in_currency': 0.8134387798896393, 'price_change_percentage_24h_in_currency': -0.5803176209294367, 'price_change_percentage_30d_in_currency': 19.266972573440928, 'price_change_percentage_7d_in_currency': -3.565856062894675}]

```

### API documentation
https://www.coingecko.com/api/docs/v3

### Endpoints included
> :warning: **Endpoints documentation**: To make sure that your are using properly each endpoint you should check the [API documentation](https://www.coingecko.com/api/docs/v3). Return behaviour and parameters of the endpoints, such as *pagination*, might have changed. <br> Any **optional parameters** defined in CoinGecko API doc can be passed as function parameters using same parameters names with the API *(see Examples above)*.
- *ping*
- **/ping** (Check API server status)
```python 
cg.ping()
```
- *simple*
- **/simple/price** (Get the current price of any cryptocurrencies in any other supported currencies that you need)
```python 
cg.get_price()
```
- **/simple/token_price/{id}** (Get current price of tokens (using contract addresses) for a given platform in any other currency that you need)
```python 
cg.get_token_price()
```  
- **/simple/supported_vs_currencies** (Get list of supported_vs_currencies)
```python 
cg.get_supported_vs_currencies()
```
- *coins*
- **/coins/list** (List all supported coins id, name and symbol (no pagination required))
```python 
cg.get_coins_list()
```
- **/coins/markets** (List all supported coins price, market cap, volume, and market related data)
```python 
cg.get_coins_markets()
```
- **/coins/{id}** (Get current data (name, price, market, ... including exchange tickers) for a coin)
```python 
cg.get_coin_by_id()
```
- **/coins/{id}/tickers** (Get coin tickers (paginated to 100 items))
```python 
cg.get_coin_ticker_by_id()
```
- **/coins/{id}/history** (Get historical data (name, price, market, stats) at a given date for a coin)
```python 
cg.get_coin_history_by_id()
```
- **/coins/{id}/market_chart** (Get historical market data include price, market cap, and 24h volume (granularity auto))
```python 
cg.get_coin_market_chart_by_id()
```
- **/coins/{id}/market_chart/range** (Get historical market data include price, market cap, and 24h volume within a range of timestamp (granularity auto))
```python 
cg.get_coin_market_chart_range_by_id()
```
- **/coins/{id}/status_updates** (Get status updates for a given coin (beta))
```python
cg.get_coin_status_updates_by_id()
```
- **/coins/{id}/ohlc** (Get coin's OHLC (beta))
```python
cg.get_coin_ohlc_by_id()
```
- *contract*
- **/coins/{id}/contract/{contract_address}** (Get coin info from contract address)
```python
cg.get_coin_info_from_contract_address_by_id()
```
- **/coins/{id}/contract/{contract_address}/market_chart/** (Get historical market data include price, market cap, and 24h volume (granularity auto) from a contract address)
```python
cg.get_coin_market_chart_from_contract_address_by_id()
```
- **/coins/{id}/contract/{contract_address}/market_chart/range** (Get historical market data include price, market cap, and 24h volume within a range of timestamp (granularity auto) from a contract address)
```python
cg.get_coin_market_chart_range_from_contract_address_by_id()
```
- *exchanges (beta)*
- **/exchanges** (List all exchanges)
```python
cg.get_exchanges_list()
```
- **/exchanges/list** (List all supported markets id and name (no pagination required))
```python
cg.get_exchanges_id_name_list()
```
- **/exchanges/{id}** (Get exchange volume in BTC and top 100 tickers only)
```python
cg.get_exchanges_by_id()
```
- **/exchanges/{id}/tickers** (Get exchange tickers (paginated, 100 tickers per page))
```python
cg.get_exchanges_tickers_by_id()
```
- **/exchanges/{id}/status_updates** (Get status updates for a given exchange (beta))
```python
cg.get_exchanges_status_updates_by_id()
```
- **/exchanges/{id}/volume_chart** (Get volume_chart data for a given exchange (beta))
```python
cg.get_exchanges_volume_chart_by_id()
```
- *finance (beta)*
- **/finance_platforms** (List all finance platforms)
```python
cg.get_finance_platforms()
```
- **/finance_products** (List all finance products)
```python
cg.get_finance_products()
```
- *indexes (beta)*
- **/indexes** (List all market indexes)
```python
cg.get_indexes()
```
- **/indexes/{id}** (Get market index by id)
```python
cg.get_indexes_by_id()
```
- **/indexes/list** (List market indexes id and name)
```python
cg.get_indexes_list()
```
- *derivatives (beta)*
- **/derivatives** (List all derivative tickers)
```python
cg.get_derivatives()
```
- **/derivatives/exchanges** (List all derivative exchanges)
```python
cg.get_derivatives_exchanges()
```
- **/derivatives/exchanges/{id}** (Show derivative exchange data)
```python
cg.get_derivatives_exchanges_by_id()
```
- **/derivatives/exchanges/list** (List all derivative exchanges name and identifier)
```python
cg.get_derivatives_exchanges_list()
```
- status_updates (beta)
- **/status_updates** (List all status_updates with data (description, category, created_at, user, user_title and pin))
```python
cg.get_status_updates()
```
- *events*
- **/events** (Get events, paginated by 100)
```python
cg.get_events()
```
- **/events/countries** (Get list of event countries)
```python
cg.get_events_countries()
```
- **/events/types** (Get list of events types)
```python
cg.get_events_types()
```
- *exchange_rates*
- **/exchange_rates** (Get BTC-to-Currency exchange rates)
```python
cg.get_exchange_rates()
```
- *trending*
- **/search/trending** (Get trending search coins (Top-7) on CoinGecko in the last 24 hours)
```python
cg.get_search_trending()
```
- *global*
- **/global** (Get cryptocurrency global data)
```python
cg.get_global()
```
- **/global/decentralized_finance_defi** (Get cryptocurrency global decentralized finance(defi) data)
```python
cg.get_global_decentralized_finance_defi()
```
