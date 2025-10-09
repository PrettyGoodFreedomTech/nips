NIP-93
=====
decentralized lists
-----

`draft` `optional`

This NIP defines lists of things that users can create and that anyone can add to. It provides an alternative to NIP-51 for list formation. The distinction is that each NIP-51 list is maintained by the list author, whereas this NIP, the list is maintained by the community.

We introduce a single event kind: `9999`, which is used either to create a new list or to add an item to a list. A list can be an item on another list, in which case we can refer to their relationship as parent-child (alternatively: hypernym-hyponym).

## tags

The `z` tag defines the category or categories to which the kind `9999` note belongs. It must be a string, and can be either human readable or an event id. There can be multiple z-tags. There is a special `z` tag: `*`, which defines a new list. 

The `allowed` and `disallowed` tags are optional and specify which data types ("p", "e", "t", "a") are (dis)allowed in child notes.  

Required: `z`

Optional: `name`, `name_singular`, `name_plural`, `description`, `title`, `comments`

### Example 1: a list of AI-controlled profiles (pubkeys)

List creation:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "AI bots"],
    ["title", "AI Bots"],
    ["description", "This is a list of nostr accounts that are automated and controlled by some sort of AI bot"],
    ["allowed", "p"]
  ],
  "id": "id_ai_bots"
}
```

Add a pubkey as an item on the list of AI bots:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "id_ai_bots"],
    ["name", "AI News"],
    ["p", "5c741f41bc40146c8a75c5842b9166275541503ac5d6633a0e785d41702e2f91"]
  ]
}
```

### Example 2: a list of long form articles on hyperinflation:

List creation:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "long form articles on hyperinflation"],
    ["description", "This is a list of long form content events on the topic of hyperinflation"],
    ["allowed", "a"]
  ],
  "id": "id_hyperinflation"
}
```

Add an naddr address as an item to the above list:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "id_hyperinflation"],
    ["a", "naddr1qvzqqqr4gupzq4rqjpyzsnf2z5wgma397sxr382z8mg90l80jf7m3z2k628z9wsrqythwumn8ghj7cnfw33k76twv4ezuum0vd5kzmp0qythwumn8ghj7ct5d3shxtnwdaehgu3wd3skuep0qq3kv6tpwskkxatjwfjkucme946xsefdwd5kcetwwskhg6tdv5khg6rfv4nqnxv6fx"],
    ["title", "Fiat Currency: The Silent Time Thief"]
  ]
}
```

### Example 3: a list of dog names:

List creation:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "dog names"],
    ["description", "This is a list of dog names"],
    ["allowed", "t"]
  ],
  "id": "id_dog_names"
}
```

Add a piece of text as an item to the above list:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "id_dog_names"],
    ["t", "Fido"]
  ]
}
```

### Example 4: A single item on multiple lists

Create a list of dogs and a list of animals:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "dogs"],
    ["description", "This is a list (by name) of individual dogs"],
    ["allowed", "t"]
  ],
  "id": "id_dogs"
}
```

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "animals"],
    ["description", "This is a list of animals"],
    ["allowed", "t"]
  ],
  "id": "id_animals"
}
```

Now add Fido to both of the above lists.

```json
{
  "kind": 9999,
  "tags": [
    ["z", "id_dogs", "id_animals"],
    ["t", "Fido"]
  ]
}
```

An alternate and equivalent way to add Fido to these two lists is to provide each list `name` in place of the list id:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "dogs", "animals"],
    ["t", "Fido"]
  ]
}
```

However, it is encouraged to use the list id if an appropriate one is known and available.
