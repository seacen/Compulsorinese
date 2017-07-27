# Getting Started

Getting started with Compulsorinese is incredibly easy. We will begin by showing you an example of Compulsorinese in use and demonstrate its syntaxes from there.

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

Now we want to make the API more powerful and user friendly by introducing 2 new fields: _OrderClass_ and _SymbolExchange_.

What is an order class? Well, we don't want to limit ourselves with just trading equities, we want to expand our business with trading capabilities of warrants, managed funds, options and more. Thus we need a field to tell the API which type of financial instruments we are trading with. 

What is a _SymbolExchange_? From the above table we can draw a conclusion that _Symbol_ and _Exchange_ are interrelated. Thus to make the life easier for API developers, a joint field of the two can be made available so that users can attach both information in one string and assign it to the field. 

So now the documentation for API fields should look something like this:

| Field Name | Required | Description |
| :--- | :--- | :--- |
| SymbolExchange | `Yes >> (Symbol & Exchange)` | Symbol of the stock you want to buy and the exchange it belongs to. Should be in format `Symbol.Exchange`. If omitted, both _Symbol_ and _Exchange_ have to be specified |
| Symbol | `Yes << SymbolExchange` | Symbol of the stock you want to buy |
| Exchange | `Yes << SymbolExchange` | Exchange the symbol belongs to |
| Quantity | `No` | Amount of shares you want to buy. If omitted, default to 50. |
| OrderClass | `Yes` | The class of the order. One of the following: <br/>**Equity**<br/>**Option**<br/>**ManagedFund** |
| Price | `Yes if OrderClass="Equity"` | Price of the stock you are willing to pay |

Hope the new syntaxes make sense by itself already! If not, well, let's dig into it one by one. 

### `>>` and `<<`

This are what in Compulsorinese called priority symbols. `>>` is a _Higher Priority Symbol_ and `<<` is a _Lower Priority Symbol_. 

They convey one meaning in common, that is the field which has got one of these symbols in _Required_ column is required in an API request, but can be optional if the fields on the symbol's right are present. 

The major difference between them, can be seen from their names, is the priority relationship they indicate. A field with `>>` has a higher priority than the symbol's right-hand fields. Thus if both the field itself and right-hand fields are present, the field itself will be used by the API service. `<<` on the other hand indicates that the field is of lower priority than the symbol's right-hand fields.

In most cases, the right-hand fields should be substitutes of the field with a priority symbol.