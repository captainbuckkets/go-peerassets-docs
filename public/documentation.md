<div class="welcome-card">
  <div class="title">Welcome to Go-PeerAssets Documentation</div>
  <img src="img/go-peerassets.png" width="auto">
  <div class="call-to-action">Feel free to navigate through any section of interest.</div>

</div>

---

# Introduction to Go-PeerAssets

Go-PeerAssets (gPA) is an implementation of PeerAssets in Go, originally ported from python.    

## PeerAssets

PeerAssets was originally proposed in a 2016 whitepaper by Peercoin Foundation President, Peerchemist.  You can read the [whitepaper here](http://peerassets.github.io/WhitePaper/).

[Peercoin university](https://university.peercoin.net/) is a community project aimed at less technical members of the community to grasp and understand the complex topic of public blockchain.

---


# API

## Assets

`GET /v1/assets/`

Gets all valid and registered assets on the given network. Returns a JSON object with the Deck Id as the key, and the asset information as a dictionary. Note you are not guaranteed to get all fields, as it depends on what the asset was created with.  

**Example:**
```
{
    <key>: {
        data : <data string>,
        decimals: <decimals int>,
        fee: <fee int>,
        mode: <mode string>,
        name: <name string>,
        txid: <txid string>,
        version: <version int>,
    },
    <deck_id string>: { ... },
    <deck_id string>: { ... }
}
```
### Attributes
* **data**
    Returns asset information stored in the transaction, similar to OP_RETURN.
* **decimals** 
    The granularity as defined by the deck spawn owner.
* **fee**
    The transactions fee.
* **mode**
    The mode the issue mode defined by the deck spawn owner.
* **name**
    The name of the deck as defined by the deck spawn owner.
* **txid** 
    The transaction id of the deck when it was spawned.
* **version**
    The version the deck was spawn under.

### Parameters
**Example:**```/v1/assets?page=1&limit=25```

* **Page**
Returns the assets on a given page. Note, returns ten assets per page unless the limit parameter is included.

* **Limit**
Limits page response to a given number of results.

---

## Transactions

`GET /v1/transactions/`

Gets information about assets tied to a given address.  Returns a card or deck JSON object with the asset information as a dictionary. 

**Example:**

```
{
    "card": {
        <key>:{
            amount: <amount int>,
            block_height: <block_height int>,
            card_id: <card_id string>,
            card_index: <card_index int>,
            data: <data string>,
            deck_id: <deck_id string>,
            receiver: <receiver string>,
            sender: <sender string>,
            tx_index: <tx_index int>,
            type: <type string>,
            }, ...}
    "deck": {
        <key> : {
            data : <data string>,
            decimals: <decimals int>,
            fee: <fee int>,
            mode: <mode string>,
            name: <name string>,
            txid: <txid string>,
            version: <version int>,
        }, ...}
    
}
```
### Attributes
#### Card
* **amount**
    Amount of a given card held.
* **block_height**
    The height at which the transaciton took place.
* **card_id**
    The id of the card.  Same as the transaction ID.
* **data**
    Returns asset information stored in the transaction, similar to OP_RETURN.
* **deck_id**
    The id of the deck.
* **receiver**
    Receiver address of the transaction.
* **sender**
    Sender address of the transaction.
* **tx_index**
    Transaction location in the block.
* **type**
    Describes whether the transaction was sent or received.  Returns "send" or "receive".

#### Deck
* **data**
    Returns asset information stored in the transaction, similar to OP_RETURN.
* **decimals** 
    The granularity as defined by the deck spawn owner.
* **fee**
    The transactions fee.
* **mode**
    The mode the issue mode defined by the deck spawn owner.
* **name**
    The name of the deck as defined by the deck spawn owner.
* **txid** 
    The transaction id of the deck when it was spawned.
* **version**
    The version the deck was spawn under.

### Parameters
**Example:** ```/v1/transactions?address=<address>&type=<card|deck>&page=1&limit=25```

* **Address (Required)**
    The public network address being queried.  Required parameter.

* **Type (Required)**
    Accepts either a 'card' or 'deck' parameter.  Returns cards or decks associated with a given address.

* **Page**
    Returns the assets on a given page. Note, returns ten assets per page unless the limit parameter is included.

* **Limit**
    Limits page response to a given number of results.

---

## Balances

`GET /v1/balances/`

Gets information about assets held in balance by the given address.  Returns a JSON object with the asset information and amount. 

**Example:**

```
{
    "balances": {
        <tx_id string>:{
            amount: <amount int>
            }, ...}    
}
```
### Attributes

* **amount**
    Amount of a given card held.

---

