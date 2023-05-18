# AWS Key Managed Service
- create and manage cryptographic keys
- control use of keys
- **FIPS 140-2** (**L2**) valid
- used for [[EBS]] encryption
- integrated with iam for auth
- Can audit use of keys via CloudTrail
- 3 cent per 10000 api calls.
- by default scoped **per region**
	- single region key: keys are isolated to a region & never leave
	- multi region key: allow key to be replicated in other regions
- 2 types of keys: AWS owned & customer owned
- for customer owned keys => aws Managed or Customer Managed Keys
- **Customer managed** keys are more configurable
- **KMS Keys** support **rotation**
	- aws owned keys => auto rotation every 1 year - **can't be disabled**
	- customer keys => auto rotation  every 1 year
		- enabled by default
		- but can't be disabled.
-  **Backing Key** *and **previous*** backing keys - as a key is **rotated** data encrypted with old versions **can** **still** be **decrypted**.
- key aliases are scoped to region

## Cost
- cost & levels where throttling occurs - 5500 or 10 k or 50k p/s across regions.


## Key Policies
- similar to resource policies 
- controll access to kms
- default = no one in this account can use the key
- use for cross account

## Key Types

### Symetric
- AES256 keys
- single key to encrypt and decrypt
- AWS services which use KMS use this
- you can only get this key via api call

### Asymetric
- public key (encrypt)
- private key (decrypt)
- can download public key
- private key only api
- use case: encryption outside of aws which access to api

### Free
- aws managed
### KMS Keys or (old naming) Customer Manged Key (CMK)
use case:
	- work on small bits of data
	- generate other keys
- 1 dollar a month
- keys never leave the KMS service
- kms keys are **logical** - Id , date, policy desc & state
- backed by **physical** key material
- generated or imported
- kms keys can be used for up to **encrypt or decrypt** **4kb of data**


## Data Encryption Keys - DEKs
- GenerateDataKey - works on > 4kb


## Key Rotation

### AWS Manged key
- automatic every 1 year

### CMK
- must be enabled
- automatic very uear
- if importet only manual rotation with use of alias



## Multi Region Keys
- keys are replicated with same id into diffrent region
- encrypt and decypt in other keys
- use case to encrypt global services (auroa global, dynamo global tables)