# An very simple example: A Lamp
The following example illustrates the DTD and the DTKG of a digital twin of a lamp.

The model of this lamp is the following one:
- *Properties*:
    - `luminosity`: the luminosity of the lamp
- *Relationships*:
    - `isInRoom`: the relationship with the room where the lamp is
- *Actions*:
    - `switch`: action to switch the current status of the lamp
- *Events*: empty

*N.B. `onto` is an example domain ontology. The remaining part is modeled with real-world ontologies such as SAREF, REC, and BRICK.*

## DTD
```json
{
    "@context": [
        "https://www.w3.org/2022/wot/td/v1.1",
        {
            "wodt": "https://purl.org/wodt/",
            "saref": "https://saref.etsi.org/core/",
            "rec": "https://w3id.org/rec/",
            "brick": "https://brickschema.org/schema/Brick#",
            "onto": "https://purl.org/onto/"
        }
    ],
    "@type": ["saref:Actuator", "rec:Lamp"],
    "title": "Lamp DT",
    "version": {"instance": "1.0.0", "model": "0.1.0"},
    "id": "http://localhost:3000",
    "wodt:physicalAssetId": "lamp",
    "securityDefinitions": {
        "nosec_sc": {
        "scheme": "nosec"
        }
    },
    "security": "nosec_sc",
    "properties": {
        "luminosity": {
            "wodt:domainTag": "onto:LuminousFlux",
            "wodt:augmentedInteraction": false,
            "readOnly": true
        },
        "isInRoom": {
            "wodt:domainTag": "brick:hasLocation",
            "readOnly": true
        },
        "availableActions": {
            "@type": "wodt:AvailableActions",
            "title": "Available actions",
            "description": "This property is external to the Digital Twin model and allows the DT to describe the currently active actions that can be correctly executed on the Thing.",
            "readOnly": true
        }
    },
    "actions": {
        "switch": {
            "wodt:domainTag": "onto:SwitchCommand",
            "wodt:augmentedInteraction": false,
            "forms": [{
                "href": "http://localhost:3000/action/switch",
                "op": ["invokeaction"]
            }]
        }
    },
    "links": [
        {
            "rel": "wodt:dtkg",
            "href": "http://localhost:3000/dtkg"
        },
        {
            "rel": "type",
            "href": "https://raw.githubusercontent.com/Web-of-Digital-Twins/dtd-conceptual-model/refs/heads/main/implementations/wot/dtd-thing-model.tm.jsonld?token=GHSAT0AAAAAACQZ4J4LLNN7PYFBIRVLIJZYZX2TU2A",
            "type": "application/tm+json"
        }
    ],
    "forms": [{
        "op": "observeallproperties",
        "href": "ws://localhost:3000/dtkg",
        "subprotocol": "websocket"
    }]
}
```

## DTKG
```
@prefix saref: <https://saref.etsi.org/core/> .
@prefix brick: <https://brickschema.org/schema/Brick#> .
@prefix rec: <https://w3id.org/rec> .
@prefix onto: <https://purl.org/onto/> .

<http://localhost:3000> a saref:Actuator, rec:Lamp ;
	saref:hasProperty onto:LuminousFlux ;
	saref:hasPropertyValue _:LuminousFluxValue ;
	brick:hasLocation <http://localhost:3001> ;
	wodt:availableActionId "switch" .

_:LuminousFluxValue a saref:PropertyValue ;
	saref:hasValue 0.20 ;
	saref:isMeasuredIn <https://qudt.org/2.1/vocab/unit/LM> ;
	saref:isValueOfProperty _:LuminousFlux .
```
