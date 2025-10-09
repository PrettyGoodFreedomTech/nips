NIP-93
=====
decentralized lists
-----

`draft` `optional`

This NIP defines lists of things that users can create and that anyone can add to. It provides an alternative to NIP-51 for list formation. The distinction is that each NIP-51 list is maintained by the list author, whereas this NIP, the list is maintained by the community.

We introduce a single event kind: `9999`, which is used either to create a new list or to add an item to a list. A list can be an item on another list, in which case we can refer to their relationship as parent-child (alternatively: hypernym-hyponym).

## Tags

The `z` tag is required and defines the category or categories to which the kind `9999` note belongs. It must be a string, and can be either human readable or an event id. There can be multiple z-tags. There is a special `z` tag: `*`, which defines a new list. 

The `p`, `e`, `t`, and `a` tags are required, allowed, or disallowed if their parent event specifies this to be the case. For example: the declaration of the list of AI Bots specifies that child notes must have the `p` tag.

The `required`, `allowed` and `disallowed` tags are optional and specify which data types ("p", "e", "t", "a") are required, allowed, or disallowed in child notes.  

If `z` type is `*` (I would use `list` in place of `*`, but the meaning of `*` is going to morph over time into something more complicated: a `concept`; `*` is special in the sense that it can be an element of itself), then the `name` tag is required, and must have two strings: a singular form ("widget") and a plural form ("widgets"), as in the examples below. Think of the `z` tag as the "element of" operator. If the `title` tag is used, it should likewise have the singular and plural forms.

Optional: `name`, `description`, `title`, `comments`

## Examples

### Example 1: a list of AI-controlled profiles (pubkeys)

List creation:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "AI bot", "AI bots"],
    ["description", "This is a list of nostr accounts that are automated and controlled by some sort of AI bot"],
    ["required", "p", "name"]
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
    ["name", "long form article on hyperinflation", "long form articles on hyperinflation"],
    ["description", "This is a list of long form content events on the topic of hyperinflation"],
    ["required", "a", "title"]
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
    ["name", "dog name", "dog names"],
    ["description", "This is a list of dog names"],
    ["required", "t"]
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
    ["name", "dog", "dogs"],
    ["description", "This is a list (by name) of individual dogs"],
    ["required", "t"]
  ],
  "id": "id_dogs"
}
```

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "animal", "animals"],
    ["description", "This is a list of animals"],
    ["required", "t"]
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

An alternate and equivalent way to add Fido to these two lists is to provide each list `name` (singular) in place of the list id:

```json
{
  "kind": 9999,
  "tags": [
    ["z", "dog", "animal"],
    ["t", "Fido"]
  ]
}
```

The above can be translated: "Fido is a dog" and "Fido is an animal".

However, it is encouraged to use the list id if an appropriate one is known and available.

### Example 5: A list of lists

Create a list of the lists of long form articles

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*"],
    ["name", "list of long form articles", "lists of long form articles"],
    ["description", "This is a list of lists of long form articles"],
    ["required", "e"]
  ],
  "id": "id_list_of_articles"
}
```

**UNFINISHED** Not sure whether the z-tag below should include "*" (in which case it needs name, singular and plural) or not --- is it a subset of wordType or a specific instance of wordType?????
Now add an item to the above list. Note that it points to the event above. 

```json
{
  "kind": 9999,
  "tags": [
    ["z", "*", "id_list_of_articles"],
    ["e", "id_hyperinflation"],
  ],
  "id": "foo"
}
```
