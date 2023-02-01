

//API Documentation

With our API endpoints you can upload resources, post trading signals from your own strategies, get access to data and interact with your investors.


Publish resources
A resource is any valuable piece of data, represented by a specified key-value pair data structure, that other user's could subscribe to on a time basis, in exchange for a fee or for free.
For example financial indicators, news, sentiment analyser, alpha indicators, etc...
To publish a resource you first need to create a resource app and generate your api keys.
* Anyone can upload a resource and charge fees for their use. Even uncertified financial advisors.
Create resource

[POST] Upload a resource signal
/upload_resource
Python example:

      
        import requests
        import os
        
        BASE_URL = 'https://justfor.fund/api/v1'
        API_KEY = os.environ['API_KEY']
        API_SECRET = os.environ['API_SECRET']
        HEADERS = {'API-KEY': API_KEY, 'API-SECRET': API_SECRET}
        
        def upload_resource(resource_id, resource_dict):
            url = "{}/upload_resource".format(BASE_URL)
            data = {
              'resource_id': resource_id,
              'resource_dict': resource_dict
            }
            r = requests.post(url, json=data, headers=HEADERS)
            return r
        

        if __name__ == '__main__':

            ""
            Imagine there's a resource object with a unique id with this structure:  Resource(id, title, key_value_type_pairs), where the id is an integer,
            the title is a string and the key_value_type_pairs is a dictionary of key and value type pairs for the resource {'key1': value_type1, 'key2': value_type2, ..., 'keyn': value_typen }.

            For example, lets say you've created a Resource that has the following parameters:
              Resource(id=1, title="Return stocks that are on fibonacci retracement channels in realtime.", key_value_type_pairs={'Symbol': "STRING", 'Market': "STRING", 'Retracement channels': "ARRAY"})
            
            then the code for uploading such resource would be the following:
            ""

            data_dict = {
              "Symbol": "LGND",
              "Market": "U.S. Nasdaq",
              "Retracement channels":{
                "90": {
                    "current_price": 66.51000213623047,
                    "fibonacci_levels": [
                        82.04000091552734,
                        75.13517967224121,
                        70.86355297088623,
                        67.41114234924316,
                        63.958731727600096,
                        59.04343524932861,
                        52.782283782958984
                    ],
                    "trend": "bullish"
                }
            },
            }
            upload_resource(1, data_dict)
      
    
resource_id: (Integer)
resource_dict: (e.g. : {'key1': value1, 'key2': value2, ..., 'keyn': valuen }) (Hash Table/Dictionary)


Publish algorithms
To publish trading signals from an algorithm you first need to create an app and generate your api keys.
* Mind that only certified financial advisors can have other users use their algorithms and charge fee's.
If you are not a financial advisor you can still create a algorithms, connect them to your brokerage accounts and have other users see it's performance.
Create algorithm

[POST] Create trading signal
/create_trading_signal
Python example:

      
        import requests
        import os
        
        BASE_URL = 'https://justfor.fund/api/v1'
        API_KEY = os.environ['API_KEY']
        API_SECRET = os.environ['API_SECRET']
        HEADERS = {'API-KEY': API_KEY, 'API-SECRET': API_SECRET}
        
        def create_trading_signal(algorithm_id, symbol, portfolio_ratio_investment, order_type, side, time_in_force):
            data = {
                "algorithm_id":algorithm_id,
                "ticker_symbol":symbol,
                "order_type": order_type, 
                "portfolio_ratio_investment": portfolio_ratio_investment, 
                "side":side, 
                "time_in_force":time_in_force
            }
            url = "{}/create_trading_signal".format(BASE_URL)
            r = requests.post(url, json=data, headers=HEADERS)
            return r
        
        
        if __name__ == '__main__':
            create_trading_signal(1, 'AAPL', 0.01, 'market', 'buy', 'gtc')
      
    
symbol: stock symbol (e.g. : "AAPL") (String)
percentage_of_buying_power: The percentage of the current buying power that will be spent on the stock (Float) (e.g. : 0.01 --> 1%)
order_type: Only "market" orders supported at this time (String)
side: "buy" or "sell" (String)
time_in_force: "day" (String) (Must be "day" for fractional trading)

 
Terms and conditions

Privacy policy

All rights reserved JustForFund SpA ©
