Discussion on the design of NIP-93: decentralized lists
-----

To gain acceptance by the nostr community, NIP-93 will need to be as simple and straightforward as possible to achieve the stated goal. What the nostr community does not necessarily need to know at this point is that this NIP is also designed to form the basis of what will gradually morph into the basis for the Concept Graph. Here I will discuss the the impact this has on NIP-93.

The Concept Graph is a personalized date repository that breaks down information into small chunks called words, with each word mapping to a single node in a graph. Each word belongs to one or more `word types`, and there is a one to one mapping between a `concept` and a `word type`. Many word types are expected to be widely used by the members of any given community; other word types may have limited penetrance, potentially existing only within a single Brainstorm. There are in theory an unlimited number of word types, and the community may or may not agree on the list of all word types. Therefore, nostr cannot use a different event kind for each word type. Instead, NIP-93 will define only a single new event kind: 9999, and will introduce only a single required one-letter tag, the z tag, to specify the word type(s) of any given word.

It is not necessary to introduce the notions of concept graph, words, and word types into NIP-93. We need only to specify how to create ("declare") a list and how to add (declare) an item on a list. We will use kind 9999 for both purposes [1]. To make a new list, we will use the z-tag to specify list as the word type: `["z", "list"]`. To add an item to a list we will use the z-tag to point to the list's event id: `["z", "specific_list_event_id"]`.

Note that NIP-93 supports a second, less formal way to add an item to a list: skip the list declaration step; simply give the list a human readable name, and replace specific_list_event_id with the list name in the z-tag. So for example: to add Alice to the list of Nostr Developers, we would need only a single event with two tags: `["z", "nostr developer"]` and `["p", "<pk_Alice>"]`. To add Fido to the list of dogs, we would need two tags: `["z", "dog"]` and `["t", "Fido"]`. Each of these list item declarations is an informal method to declare the list of nostr developers or the list of dogs. The process of formalized list declaration has the advantages that we can spell out in greater detail what the list means. We may discover that for any given list of interest, the community may be using multiple list declarations, in which case we have the option to combine the ones we like using a filter like this: `"#z", "dog", <dog_event_id1>, <dog_event_id1>]`.

## Future evolution (short term)

In the future, we will want a method for members of my grapevine to object to any given item being on any given list. Multiple ways to do this. We may or may not want to create lists specific to the Concept Graph (below) first.

## lists specific to the Concept Graph 

There are a handful of lists that we will want to curate that will help us to build out the basic infrastructure of the Concept Graph. Two in particular: the list of relationship types (more on tha later) and the list of word types. For starters, we will declare the list of word types, and add the following items: 
- wordType
- relationshipType
- list
- concept
- set
- subset

You read that right: wordType is an item on the list of wordTypes. The mind boggles with remembrances of Cantor set theory. Can a set be an element of itself? This is the kind of question that we will avoid entirely with NIP-93, but which we will want to have thought about ahead of time. The answer is yes, the formalism of the Concept Graph allows word type to be an element of itself. Trust me that this will not set us up to hit a wall; rather, this is how we avoid hitting any walls.

Note: actually Concept Graph theory resolves this issue in set theory by declaration two word types within a concept: we saparate wordType nodes from superset nodes. Words of word type: wordType are elements of a node of wordType: superset, all within the word type concept.

The great thing is that we won't necessarily need a NIP to declare word types. We can propose them, but our grapevines will help us to curate these lists!

## Notes

[1] Or maybe two event kinds: 9999 or 39999, which opens up the option that any given word may be editable by the word author or uneditable.
