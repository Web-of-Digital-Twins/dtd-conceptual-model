# DTD Abstract Conceptual Model
This document contains the *Abstract Conceputal Model* of the **Digital Twin Description (DTD)**. \
It serves as the conceptual basis for the processing of Digital Twin Descriptions and their serialization, indipendent from any technology or implementation.

## Root

|Element                         |Mandatory |Value Type                           | Description |
|:-------------------------------|:---------|:------------------------------------|:------------|
|**Version**                     |yes       |string                               |The version of the Digital Twin Description.|
|**DT URI**                      |yes       |URI                                  |The URI of the HWoDT Digital Twin.|
|**PA Identifier**               |yes       |string                               |The ID of the associated Physical Asset.|
|**DT type**                     |yes       |URI                                  |The type -- in the domain ontology -- that represents the Digital Twin (e.g., `ontology:Car`).|
|**DTKG link**                   |yes       |URL                                  |The direct URL to the DTKG of the HWoDT DT.|
|**Memento TimeGate**            |no        |URL                                  |The Memento TimeGate HTTP URL. The HWoDT DT use it to expose the *Memorization* service.|
|**WoDT Platforms**              |yes       |List of URL                          |The WoDT Platforms where the HWoDT DT is present. The list is empty when it is not registered to any platform.|
|**Observation affordance**      |yes       |List of **Form**                     |The affordance to observe the HWoDT DTKG. Different protocols can be specified.|
|**Properties**                  |yes       |List of **Property**                 |The properties of the HWoDT DT.|
|**Events**                      |yes       |List of **Event**                    |The events of the HWoDT DT.|
|**Relationships**               |yes       |List of **Relationship**             |The relationships of the HWoDT DT.|
|**Actions**                     |yes       |List of **Action**                   |The actions of the HWoDT DT.|

In the following the detailed description of the **referenced** elements.
### Property
Structure of a **Property** in the *Digital Twin Description*.
|Element                         |Mandatory |Value Type                           | Description |
|:-------------------------------|:---------|:------------------------------------|:------------|
|**Name**                        |yes       |string                               |The name of the property. E.g., *Temperature*.|
|**Domain Tag**                  |yes       |URI                                  |The URI that identifies the domain ontology resource (e.g., class, predicate, individual) used to describe the property in the DTKG.|
|**Is Augmented**                |no        |boolean                              |It states if the property is an augmented or not. If not it means that is mirrored directly from the PA.|
|**Read affordance**             |no        |List of **Form**                     |The affordance to read the current value of the property. Different protocols can be specified.|
|**Observation affordance**      |no        |List of **Form**                     |The affordance to observe the evolution of the value of the property. Different protocols can be specified.|

### Event
Structure of an **Event** in the *Digital Twin Description*.
|Element                         |Mandatory |Value Type                           | Description |
|:-------------------------------|:---------|:------------------------------------|:------------|
|**Name**                        |yes       |string                               |The name of the event.|
|**Domain Tag**                  |yes       |URI                                  |The URI that identifies the domain ontology resource (e.g., class, predicate, individual) used to describe the event type.|
|**Is Augmented**                |no        |boolean                              |It states if the event is an augmented or not. If not it means that is mirrored directly from the PA.|
|**Observation affordance**      |yes        |List of **Form**                    |The affordance to observe the event. Different protocols can be specified.|

### Relationship
Structure of a **Relationship** in the *Digital Twin Description*.
|Element                         |Mandatory |Value Type                           | Description |
|:-------------------------------|:---------|:------------------------------------|:------------|
|**Name**                        |yes       |string                               |The name of the relationship.|
|**Domain Tag**                  |yes       |URI                                  |The URI that identifies the domain ontology resource (e.g., class, predicate, individual) used to describe the relationship in the DTKG.|
|**Read affordance**             |no        |List of **Form**                     |The affordance to read the active intances of the relationship. Different protocols can be specified.|
|**Observation affordance**      |no        |List of **Form**                     |The affordance to observe the evolution of the instances of the relationship. Different protocols can be specified.|

### Action
Structure of an **Action** in the *Digital Twin Description*.
|Element                         |Mandatory |Value Type                           | Description |
|:-------------------------------|:---------|:------------------------------------|:------------|
|**Action ID**                   |yes       |string                               |The ID used to identify the action.|
|**Domain Tag**                  |yes       |URI                                  |The URI that identifies the domain ontology resource (e.g., class, predicate, individual) used to describe the action type (e.g., `ontology:SwitchCommand`).|
|**Is Augmented**                |no        |boolean                              |It states if the action is an augmented or not. If not it means that is mirrored directly from the PA.|
|**Required Input**              |no        |**Data Schema**                      |The input data structure that the action takes as input.|
|**Action invocation affordance**|yes       |List of **Form**                     |The affordance to invoke the action. Different protocols can be specified.|


### Data Schema
It describes the structure of the data being sent. Its serialization depends on the specific implementation.

### Form
It contains all the protocol information necessary for automatic processing -- without *out-of-band* data.