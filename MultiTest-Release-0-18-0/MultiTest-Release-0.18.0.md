# CosmWasm MultiTest 0.18 released 

![pieces](sigmund-unsplash.jpg)
Photo by <a href="https://unsplash.com/@sigmund?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Sigmund</a>
on <a href="https://unsplash.com/photos/brown-and-black-jigsaw-puzzle-B-x4VaIriRc?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>

This week we have released a new version of **CosmWasm MultiTest**.
We are excited to share some details about recent updates to **CosmWasm MultiTest**
and would like you to try them out for yourself!

The new major enhancements in version **0.18.0** of **CosmWasm MultiTest** include:

- Handling `WasmMsg::Instantiate2` message
- Support for `WasmQuery::CodeInfo` message
- Custom checksum generator
- Improved custom address generator
- Extended `Wasm` trait
- Contract code duplication


## Handling `WasmMsg::Instantiate2` message

Link to article of Simon:
[Dev Note #3: Limitations of Instantiate2 and how to deal with them](https://medium.com/cosmwasm/dev-note-3-limitations-of-instantiate2-and-how-to-deal-with-them-a3f946874230)

## Support for `WasmQuery::CodeInfo` message

## Custom checksum generator

## Improved custom address generator

Example with `Bech32`

## Extended `Wasm` trait

## Contract code duplication

We added the possibility to easily duplicate contract code during testing.
Now, the `App` provides a function `duplicate_code` that creates a copy of the contract code.
Having the identifier of the copy of the contract code, new contracts may be instantiated
and used exactly as the original. The behaviour of instantiated contracts will be exactly the same.
An example of using `duplicate_code` function is shown below.

```rust
// example contract implementation
mod echo {

  // entry points are not shown here
  
  pub fn contract() -> Box<dyn Contract<Empty>> {
    // this function should return an example contract
  }
}

// create the app
let mut app = App::default();

// store an example contract that will be duplicated later
let code_id = app.store_code(echo::contract());

// duplicate contract code
let new_code_id = app.duplicate_code(code_id).unwrap();

// instantiate contract using new_code_id
```
