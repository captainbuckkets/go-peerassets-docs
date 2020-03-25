<div class="welcome-card">
  <div class="title">Welcome to Go-PeerAssets Documentation</div>
  <img src="img/welcome.svg" width="458">
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
    <deck_id string>: {
		version: <version int>, 
		name: <name string>, 
		number_of_decimals: <number of decimals int>, 
		issue_mode: <issue_mode int>,
                asset_specific_data: <asset_specific_data string>
    },
    <deck_id string>: { ... },
    <deck_id string>: { ... }
}
```
### Attributes
**deck_id**
 The transaction ID of the deck spawn.
* **name**
 The name of the deck.
* **version**
 The version of the deck.
* **number_of_decimals**
 The granularity as defined by the deck spawn owner. 
* **issue_mode**
 The issue mode of the deck. 
* **asset_specific_data**
 Returns asset information stored in the transaction, similar to OP_RETURN.  

### Parameters
**Example:**```/v1/assets?page=1&limit=25```

* **Page**
Returns the assets on a given page. Note, returns ten assets per page unless the limit parameter is included.

* **Limit**
Limits page response to a given number of results.

---

## Transactions

`GET /v1/transactions/`

Gets information about assets tied to a given address.  Returns a JSON object with with the "Decks" Id or "Cards" as the key, and the asset information as a dictionary. 

**Example:**

```
{
    "cards": {
        <card_id string>:{
            version: <version int>, 
            amount: <name int>, 
            number_of_decimals: <number of decimals int>, 
            asset_specific_data: <asset_specific_data string>
               }, ...}
    "decks": {
        <deck_id string>: {
            version: <version int>, 
            name: <name string>, 
            number_of_decimals: <number of decimals int>, 
            issue_mode: <issue_mode int>,
            asset_specific_data: <asset_specific_data string>
        }, ...}
    
}
```
### Attributes
**card_id**
The transaction ID of the card.
* **version**
The version the card was generated under.
* **amount**
The amount of cards of a given deck held by the address
* **number_of_decimals**
The granularity as defined by the deck spawn owner. 
* **asset_specific_data**
Returns asset information stored in the transaction, similar to OP_RETURN.

**deck_id**
 The transaction ID of the deck spawn.
* **name**
 The name of the deck.
* **version**
 The version of the deck.
* **number_of_decimals**
 The granularity as defined by the deck spawn owner. 
* **issue_mode**
 The issue mode of the deck. 
* **asset_specific_data**
 Returns asset information stored in the transaction, similar to OP_RETURN.  

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