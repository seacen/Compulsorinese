# Getting Started

Getting started with Compulsorinese is incredibly easy. We will begin by showing you an example of Compulsorinese actually in use and demonstrate its syntaxes from there.

## 4 Simple Fields

Say we have a financial API that enable you to buy shares from stock markets, in order to place a buy order in the market, you will of course need to specify the stock _Symbol_ you want to buy, the _Exchange_ this stock belongs to, the _Quantity_ you want to buy and on what _Price_ you want to buy it for. Easy-peasy. Now the API we design have little choices but to expose the following 4 fields:

| Field Name | Required | Description |
| :--- | :--- | :--- |
| Symbol | `Yes` | Symbol of the stock you want to buy |
| Exchange | `Yes` | Exchange the symbol belongs to |
| Quantity | `Yes` | Amount of shares you want to buy |
| Price | `No` | Price of the stock you are willing to pay |

Notice the Required column

