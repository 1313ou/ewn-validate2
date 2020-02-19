#WordNet-LMF 1.1
#===

This is to equip WordNet with state-of-the-art validation schemas the way FrameNet did. This move is dictated by the following:

- DTD does not provide fine-grained control the way XSD does. The most significant difference between DTDs and XML Schema is the capability to create and use **datatypes**. XSD schemas define datatypes for elements and attributes while DTD doesn't support them. This allows for control on what sort of data (ids, content) is expected. Leveraging datatypes gets errors to bubble up that would otherwise go unnoticed.

- Incidentally the reference to  Dublin Core schema is erroneous (as mentioned [here](https://github.com/globalwordnet/schemas/issues/5) ) in that the definition of elements is mistakenly applied to attributes. Any real validation against the Dublin Core definitions would fail. Besides, Dublin Core seems superimposed and unnatural and it is doubtful it is of real use here.

####name spaces

Namespaces are left unchanged. Beyond the current namespace, the only namespace is dc:.

####modules

 The design is modular:
 
***dc.xsd*** for dc: namespace.
***(ewn-)idtypes(-relax_idrefs).xsd*** for id types (it defines ID policy).
***(ewn-)wordtypes.xsd*** for word types (it defines word form policy).
***types.xsd*** for core data types.
***types-1.1.xsd*** for 1.1 data types.
***core-1.1.xsd*** for elements and the core structure.

This allows for different levels of validation to be performed. 

This makes it possible to bring stricter constraints to bear on the same data. But it does not mean the previous level is incompatible with the next. For example the data that satisfies EWN-LMF-1.1.xsd is a subset of data validated by WN-LMF-1.1.xsd (or  WN-LMF-1.1 is a superset of EWN-LMF-1.1). 

Another use is different IDREF validation depending on whether you are attempting at validating merged files or not.

####id types

idtypes-1.1.xsd and ewn-idtypes-1.1.xsd differ in that the latter imposes extra constraints on the **well-formedness** of EWN ids.

####relaxed id types vs strict

This deals with **id reference** validation.

*(ewn-)idtypes-1.1.xsd* and *(ewn-)idtypes-1.1-relax_idrefs.xsd* differ in that the latter allows some **non-local references not to have their target in the same file**. This is necessary in the case of part-of-speech cross-references such as the ones found in derivation relations (adj derived from noun, etc...) or maybe other cases (seealso, etc). The target then resides in a different file. This is useful to validate **pre-merging lexicographer files** while the strict mode must be used **to validate the merged file**, to make sure references are not left dangling.

####some resulting combinations:

WN-LMF-1.1-relax_idrefs.xsd
WN-LMF-1.1.xsd
EWN-LMF-1.1-relax_idrefs.xsd
EWN-LMF-1.1.xsd

####EWN compatibility with 1.1. schema

The current lexicographer files satisfy both:

- WN-LMF-1.1-relax_idrefs.xsd
- EWN-LMF-1.1-relax_idrefs.xsd

The current merged file satisfies both:

- WN-LMF-1.1.xsd
- EWN-LMF-1.1.xsd