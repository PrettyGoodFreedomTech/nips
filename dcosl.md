NIP-xx
=====
decentralized lists
-----

`draft` `optional`

This NIP defines lists of things that users can create and that anyone can add to. It provides an alternative to NIP-51 for list formation. The distinction is that each NIP-51 list is maintained by the list author, whereas this NIP, the list is maintained by the community.

We introduce a single new event kind: `9903`, which can be either a new list or a new list item. The reason for using the same event kind is because any given list may itself be an item on another list. (Should we give word creators the option to use use `39903` rather than `9903` if they want it to be editable?)

## tags

The `noteType` tag defines the category to which the kind 9903 note belongs. It must be a string, and can be either human readable or an event id.

### Example 1: a list of pubkeys

List creation:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType","list"],
    ["title","Nostr Developers"],
    ["description","This is a list of nostr developers"],
    ["allowed", "p"]
  ],
  "id": "abc123"
}
```

Add a pubkey as an item on the list of Nostr Developers:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType":"abc123"],
    ["p","<pubkey1>"]
  ]
}
```

### Example 2: a list of kind 1 content events:

List creation:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType","list"],
    ["title","Whatever"],
    ["description","This is a list of kind 1 content events on the topic of whatever"],
    ["allowed", "e"]
  ],
  "id": "bcd234"
}
```

Add an item (a kind 1 event) to the above list:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType":"bcd234"],
    ["e","<event_id1>"]
  ]
}
```

### Example 3: a list of tags:

List creation:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType","list"],
    ["title","Dog names"],
    ["description","This is a list of dog names"],
    ["allowed", "t"]
  ],
  "id": "cde345"
}
```

Add an item (a kind 1 event) to the above list:

```json
{
  "kind": 9903,
  "tags": [
    ["noteType":"cde345"],
    ["t","Fido"]
  ]
}
```
