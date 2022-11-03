# **DID:SCID Method Specification**

## **Introduction**

StraitsChain is the first blockchain infrastructure in China to strengthen and promote cross-strait economy, business trade and cultural exchanges. StraitsChain is the new generation of blockchain technology service platform. Relying on advanced blockchain infrastructure technology, StraitsChain serves developers, enterprises and organizations across Taiwan strait, Chinese mainland and all over the world. In accordance with China’s policies and regulations, StraitsChain combined mature Consortium Blockchain and Public Blockchain technology with its core technology accumulated over the years.

StraitsChain Decentralized Identity(SCID) is based on blockchain，provide infrastructure for trusted digital identity and data exchange services across systems and organizations. SCID allows users to provide distributed identities for individuals, enterprises, devices, and digital objects, building a distributed, data-secure, privacy-protected identity system that addresses trusted connections between individuals, enterprises, devices, and digital objects.

## **Status of this document**

This is a draft document and will be updated based on W3C.

## **Method Specific Identifier**

```
straitchain-did = "did:scid:" specific-id
specific-id = base58(version+type+straitchain-address)
version = 2*HEXDIG
type = 2*HEXDIG
```

- "version" is the SCIC version number, the current version is 01
- "type" is the identity of the DID certified on StraitsChain platform
- "straitchain-address" is the public key address of the identity on StraitsChain 

### **Example**

```
did:scid:6GFxvNrooGoh2te8kukKYWuyu4UqqMn5TuN9DuWGxjkz2FatSJCcjb28pAZnx3Y
```

## **DID Document**

### **Example**

```
{  
   "@context":"https://w3id.org/did/v1",
   "id":"did:scid:6GFxvNrooGoh2te8kukKYWuyu4UqqMn5TuN9DuWGxjkz2FatSJCcjb28pAZnx3Y",
   "sc-index":"36621783fbaa4d498797f8aff54b15de",
   "agent":{
       "id":"did:scid:6GFyFAMCpSVwsCLmW6MpPxVEKSQz5kr9QdPVMLobVZHLEpDDdLt9wDfg6CGnBvu#agent",
       "type":"Secp256k1VerificationKey2018"
   },
   "publicKeys":[  
      {  
         "id":"did:scid:5HDx7jPsiED6n47eNfERrBBRHZb59jVW6UMZZMTSBpikzvhX#owner",
         "type":"Secp256k1VerificationKey2018"
      }
   ],
   "authentication":[
      {  
         "type":"Secp256k1SignatureAuthentication2018",
         "publicKey":"did:scid:6GFxvNrooGoh2te8kukKYWuyu4UqqMn5TuN9DuWGxjkz2FatSJCcjb28pAZnx3Y#owner",
      }
   ],
   "updated":"2022-03-03T06:41:39.723Z"
}
```

- sc-index is the search id of user on StraitsChain, and StraitsChain allows user to hold multiple DID (optional)
- agent is the agent user of the DID, and StraitsChain allows users to designate a platform to process business (optional)

## **CRUD Operations**

### **Create (Register)**

Contract Method

```
function addKey(string calldata did, bytes calldata newPubKey, string[] calldata pubKeyController,
        bytes calldata singer) external;
```

SCID Service Method

```
Result new(CreateDocument doc)
```

### **Read (Resolve)**

SCID Service Method

```
Result get(String scid)
Result get(String scIndex)
```

### **Update**

SCID Service Method

```
Result update(String scid, UpdateDoc doc)
```

### **Delete (Deactivate)**

Contract Method

```
function deactivateID(string calldata did, bytes calldata singer) external;
```

SCID Service Method

```
Result deactivate(String scid)
```

## **Security Considerations**

To protect user privacy, SCID stores user data in the user's local client. SCID uses secp256k1 based signature algorithm to protect data privacy.

All operations of the user are verified by the signature of the on-chain contract to ensure the security of the user's operations.

The private key (used for signing operations) should be kept confidential. If the key is compromised, the user needs to immediately deactivate (revoke) any existing DID. Proxies can be used to reduce the risk of private key exposure.

## **Privacy Considerations**

Following the DID core specification requirements, the documents in the SCID method do not contain any data that may expose the user's privacy, only the user's public key data is saved, and some of the platform fields are user-selectable and do not contain the user's information data, and the DID entity cannot be identified from the DID document.

Users keep private data through verifiable credentials issued by the DID service provided by StraitsChain. The protection of user privacy depends on the security of VC.

## **References**

**[1]** https://w3c-ccg.github.io/did-core/

**[2]** [ethereum/EIPs#1056](https://github.com/ethereum/EIPs/issues/1056)