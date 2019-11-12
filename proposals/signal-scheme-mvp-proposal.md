# Signal Scheme MVP Proposal
# Abstract
We are proposing the initial step toward the implementation of a method to drive soft consensus, referred to as "Signal Scheme" in this document. It allows DAOs to agree on arbitrary information without creating any action on the blockchain (except being marked as accepted by the DAO or not).

This information can then be interpreted in various ways on the client side allowing many versatile use cases.

This is important because various different use cases (that are outside of the scope of this proposal) can be build upon it. Future use cases include (but are not limited to):

- Curating a list of resources - onboarding guides, website, social groups, etc
- Agreeing on norms - rep for onboarding, prices,
- Building a home page for the DAO
- Managing a shared calendar

# Proposal

This proposal focuses on the minimum viable implementation of a single use:  "Curation of the DAO Header". Passed proposals on the signal scheme will result in updating information visible to Alchemy's DAO home screen (overview of schemes) above the headline "All Schemes".
The Attributes that are visinle and can be updated include:

- icon (as url / base64 / ipfs?)
- name
- headline
- mission statement / abstract
- banner image (as url / ipfs?)
 
Furthermore the header will display the holdings of the DAO (ETH / GEN / DAI etc.)

A initial version of the scheme contract is already written (https://github.com/daostack/arc/blob/master/contracts/schemes/SignalScheme.sol). Part of the proposal is changing the contract and reviewing it to meet the requirements of the use case.

# Example of envisioned DAO header functionality
![](https://i.imgur.com/xJOkl6N.jpg)


# High-level mechanism
A signal scheme’s only property is its interpretation instructions. Its passed proposals produce a series of agreed-upon data objects. The subgraph interprets the signals and constructs the final state.

# Specs Contracts
## Registering a signal scheme
On registering a signal scheme the "interpretation directions" will be specified  as a param in the param hash. Either the interpretation direction tells that the scheme will be about a list of objects or one individual object. The underlying data structure will always be a list so interpretation direction can be changed later on without having to transform the data structure.

## Signal proposal
The signal proposal includes a description hash (only). This will include the usual proposal properties (Title, description and url), but will also include a new <signal> property. As such, if passed, the proposal has no effect on the state of the blockchain, it just marks this data as either approved by the DAO or not.

### Interpretation specs
In addition to the usual title, description and URL the signal proposals will have a signal field.

The signal field will include two fields:

- signalType
- signalData


# Signal type: DSSignal-object-0.1

## Abstract

The object signal 

## Signal types:

### set_properties

This will overwrite the supplied properties in the object with the new values provided.

#### Validation

The data needs to be an object.
If a property doesn’t exist, it will add it.
If a property is set to null, it will delete it.

#### Example:

The object before the proposal:

```
{
   Name: “dao name”
   Description: “dao description”
}
```

Proposal:

```
{
   Name: “change the dao name”
   Description: “I want to change the dao name”
   Signal: {
      Signal_type: “set_properties”
      Signal_data: {
         Name: “new dao name”
      }
   }
}
```

Object after the proposal:

```
{
   Name: “new dao name”
   Description: “dao description”
}
```

#### Set_object

Setting the object simply replaces the existing object with the data of the signal

##### Validation

The data needs to be an object.

# Specs - Caching
The subgraph needs to parse each passed proposal and construct the latest state of the data managed by the scheme.

# Specs - Alchemy
Alchemy simply asks for the latest state, and presents it.

# Milestones & Tasks
Development will take place between 11.11.2019 - 31.01.2020
Following outcome can be expected in the end of the specified due date:
- Signal Scheme Contract meets requirements and is reviewed and tested
- Subgraph contract tracker for Signal Scheme
- DAO Header implemented in Alchemy 
- create proposal screen for changing header properties

In order to follow our progress, the code will be pushed through the following repository:
https://github.com/apeunit/Ecosystem

# Costs
- 45 ETH
- 250 REP
- 1500 GEN

# Link to proposal in GenesisDAO
[https://alchemy.daostack.io/dao/0x294f999356ed03347c7a23bcbcf8d33fa41dc830/proposal/0x369e0cf75dc46e2defa2963f5ac7dfd162eec886c5404fc946db85c49afd8956](https://alchemy.daostack.io/dao/0x294f999356ed03347c7a23bcbcf8d33fa41dc830/proposal/0x369e0cf75dc46e2defa2963f5ac7dfd162eec886c5404fc946db85c49afd8956)
