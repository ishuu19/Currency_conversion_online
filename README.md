# Exchange Rate API

## Description

This Python script fetches the exchange rate between two currencies using the Exchange Rate API. The API takes parameters such as the amount to convert, the source currency, and the target currency to determine the exchange rate.

## Functionality

- The `get_exchange_rate` function takes the following parameters:
  - `amount`: The amount to be converted.
  - `from_currency`: The source currency code.
  - `to_currency`: The target currency code.
- It sends a GET request to the Exchange Rate API with the specified parameters.
- The response contains the latest exchange rates for various currencies against the USD.
- The function calculates the total amount after converting from the source currency to USD and then to the target currency.
- The total amount after conversion is returned.

## Requirements

- Python 3.x
- requests library

## Usage

- Ensure Python and the requests library are installed.
- Call the `get_exchange_rate` function with the required parameters (amount, from_currency, to_currency) to fetch the exchange rate.

## Code
```python
def get_exchange_rate(amount, from_currency, to_currency):
    
    url = "https://exchangerate-api.p.rapidapi.com/rapid/latest/USD"

    headers = {
        "X-RapidAPI-Key": "2cb11a79eemsh3e02386a94e7969p129c47jsn2dce33b3a5d7",
        "X-RapidAPI-Host": "exchangerate-api.p.rapidapi.com"
    }

    response = requests.get(url, headers=headers)
    data = response.json()
    rates = data['rates']
    converted_to_USD = 1/rates[from_currency]
    converted_to_req_currency = rates[to_currency] * converted_to_USD
    
    total_amount = amount * converted_to_req_currency
    
    return total_amount

print(get_exchange_rate(10_000,"HKD","USD"))  # should give roughly 1278
print(get_exchange_rate(1_000_000,"JPY","HKD"))  # should give roughly 52000    
```

## Example

```python
print(get_exchange_rate(10_000, "HKD", "USD"))   # should give roughly 1278
print(get_exchange_rate(1_000_000, "JPY", "HKD"))   # should give roughly 52000
```

## Output
```
For the first example, the output is approximately 1278.1244903478594, indicating the converted amount from HKD to USD.
For the second example, the output is approximately 52122.92507633472, indicating the converted amount from JPY to HKD.
```

## Author Name
Anayed Hossain Eshan
