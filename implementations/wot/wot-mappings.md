# DTD Implementation: Web of Things Thing Description
This document contains the mappings between the **[DTD Abstract Conceptual Model](https://github.com/Web-of-Digital-Twins/dtd-conceptual-model/blob/main/abstract-conceptual-model.md)** and the **[WoT Thing Description](https://www.w3.org/TR/2023/REC-wot-thing-description11-20231205/)** model to implement the DTD with the WoT Thing Description. \
The Thing Description does not have the whole semantics needed to represent the concepts of the **DTD Abstract Conceptual Model**. The **[WoDT vocabulary](https://github.com/Web-of-Digital-Twins/wodt-vocabulary)** fills this gap and it is used as a *[WoT TD Context Extension](https://www.w3.org/TR/2023/REC-wot-thing-description11-20231205/#sec-context-extensions)*.

It is possible to note that the **WoT Thing Description**, appropriately **supported** by the **WoDT vocabulary**, can **implement** a **Digital Twin Description** offering at the same time a compatibility layer towards the *Web of Things*. \
A HWoDT Digital Twin described by a Digital Twin Description implemented with a Thing Description can also be used by a Consumer as a WoT Thing.

***N.B: To ease the creation of a HWoDT-compliant DTD with the WoT Thing Description a WoT Thing Model is provided [here](https://github.com/Web-of-Digital-Twins/dtd-conceptual-model/blob/main/implementations/wot/dtd-thing-model.tm.jsonld).*** 

## Root
|Element                         | Description |
|:-------------------------------|:------------|
|**Version**                     |Use the TD's `version` key with a `VersionInfo` value.|
|**DT URI**                      |Set as the ID of the Thing, using the `id` field.|
|**PA Identifier**               |Set via context extension, using a new key-value pair, with the `physicalAssetId` property (from *WoDT vocabulary*).|
|**DT type**                     |Set via the `@type` field at the Thing level.|
|**DTKG link**                   |Defined through a link (TD's *Link*) in `links`, with `dtkg` as relation type (from *WoDT vocabulary*).|
|**Memento TimeGate**            |Defined through a link (TD's *Link*) in `links`, with `timegate` as relation type, following the *Memento* protocol.|
|**WoDT Platforms**              |Each platform is defined through a link (TD's *Link*) in `links`, with `registeredToPlatform` as relation type (from *WoDT vocabulary*).|
|**Observation affordance**      |*Thing level Form** with `"op": "observeallproperties"` |
|**Properties**                  |Set using the TD *Property* Interaction affordance of the TD. Each property has the `readOnly` field set to `true`.|
|**Events**                      |Set using the TD *Event* Interaction affordance of the TD.|
|**Relationships**               |TD does not provide a way to observe or add metadata to *Links*. So, each relationship must be modeled through a *TD Property* in the TD. Each property has the `readOnly` field set to `true`.|
|**Actions**                     |Set using the TD *Action* Interaction affordance of the TD.|

In addition, a new TD Property `availableActions` with `@type` assigned to `AvailableActions` (from *WoDT vocabulary*) and `"readOnly": true`, must be added to describe the *availableActions* returned within the observation Thing level Form.

In the following the detailed description and mappings of the **referenced** elements.

### Property
Mapping of a DT Property in a TD Property.
|Element                         | Description |
|:-------------------------------|:------------|
|**Name**                        |Set as the name of the TD Property.|
|**Domain Tag**                  |Set via context extension, using a new key-value pair, with the `domainTag` property (from *WoDT vocabulary*).|
|**Is Augmented**                |Set via context extension, using a new key-value pair, with the `augmentedInteraction` property (from *WoDT vocabulary*).|
|**Read affordance**             |Set as a TD *Form* instance specified with the `"op": "readproperty"` field.|
|**Observation affordance**      |Set as a TD *Form* instance specified with the `"op": "observeproperty"` field.|

### Event
Mapping of a DT Event in a TD Event.
|Element                         | Description |
|:-------------------------------|:------------|
|**Name**                        |Set as the name of the TD Event.|
|**Domain Tag**                  |Set via context extension, using a new key-value pair, with the `domainTag` property (from *WoDT vocabulary*).|
|**Is Augmented**                |Set via context extension, using a new key-value pair, with the `augmentedInteraction` property (from *WoDT vocabulary*).|
|**Observation affordance**      |Set as a TD *Form* instance specified with the `"op": "subscribeevent"` field.|

### Relationship
Mapping of a DT Relationship in a TD Property.
|Element                         | Description |
|:-------------------------------|:------------|
|**Name**                        |Set as the name of the TD Property.|
|**Domain Tag**                  |Set via context extension, using a new key-value pair, with the `domainTag` property (from *WoDT vocabulary*).|
|**Read affordance**             |Set as a TD *Form* instance specified with the `"op": "readproperty"` field.|
|**Observation affordance**      |Set as a TD *Form* instance specified with the `"op": "observeproperty"` field.|

### Action
Mapping of a DT Action in a TD Action.
|Element                         | Description |
|:-------------------------------|:------------|
|**Action ID**                   |Set as the name of the TD Action.|
|**Domain Tag**                  |Set via context extension, using a new key-value pair, with the `domainTag` property (from *WoDT vocabulary*).|
|**Is Augmented**                |Set via context extension, using a new key-value pair, with the `augmentedInteraction` property (from *WoDT vocabulary*).|
|**Required Input**              |Set with the `input` field of the TD *Action* using the WoT *Data Schema*.|
|**Action invocation affordance**|Set as a TD *Form* instance specified with the `"op: "invokeaction"` field.|

### Data Schema & Form
The *Data Schema* and the *Form* specified in the Abstract conceptual model are mapped respectively to the `DataSchema` and the `Form` concept in the **Thing Description model**.