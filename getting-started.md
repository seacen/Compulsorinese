# Getting Started

Getting started with Compulsorinese is incredibly easy. We will begin by showing you an example of Compulsorinese actually in use and demonstrate its syntaxes from there.

## 4 Simple Fields

Say we have a financial API that enables you to buy shares from stock markets. In order to place a buy order in the market, you will of course need to specify the stock _Symbol_ you want to buy, the _Exchange_ this stock belongs to, the _Quantity_ you want to buy and on what _Price_ you want to buy it for. Easy-peasy. Now the API we design have little choices but to expose the following 4 fields:

| Field Name | Required | Description |
| :--- | :--- | :--- |
| Symbol | `Yes` | Symbol of the stock you want to buy |
| Exchange | `Yes` | Exchange the symbol belongs to |
| Quantity | `No` | Amount of shares you want to buy. If omitted, default to 50. |
| Price | `Yes` | Price of the stock you are willing to pay |

Notice the _Required_ column in the above table, it contains values in Compulsorinese. `Yes` and `No` are both built in words in Compulsorinese that convey meanings in exactly what they mean in English: `Yes` is required and `No` is optional \(not required\). Now you have seen the simplest form of the language.

## Spicing Up

Now we want to make the API more powerful and user friendly by introducing 3 new fields: _OrderClass_, _SymbolExchange_ and _Code_.

What is an order class? Well, we don't want to limit ourselves with just trading equities, we want to expand our business with trading capabilities of warrants, managed funds, options and more. Thus we need a field to tell the API which type of financial instruments are we trading with. 

What is a _SymbolExchange_? From the above table we can draw a conclusion that _Symbol_ and _Exchange_ are interrelated. Thus to make the life easier for API developers, a joint field of the two can be made available so that users can attach both information in one string and assign it to the field. 

The new _Code_ field is simply a substitute of _Symbol_. Some people prefer to use the word "symbol" while others prefer "code". It's OK, we support both. So now the documentation for API fields should look something like this:

| Field Name | Required | Description |
| :--- | :--- | :--- |
| SymbolExchange | `Yes >> (Symbol & Exchange)` | Symbol of the stock you want to buy and the exchange it belongs to. Should be in format `Symbol.Exchange`. If omitted, both _Symbol_ and _Exchange_ have to be specified |
| Symbol | `Yes << SymbolExchange` | Symbol of the stock you want to buy |
| Exchange | `Yes << SymbolExchange` | Exchange the symbol belongs to |
| Quantity | `No` | Amount of shares you want to buy. If omitted, default to 50. |
| OrderClass | `Yes` | The class of the order. One of the following: <br/>**Equity**<br/>**Option**<br/>**ManagedFund** |
| Price | `Yes if OrderClass="Equity"` | Price of the stock you are willing to pay |
