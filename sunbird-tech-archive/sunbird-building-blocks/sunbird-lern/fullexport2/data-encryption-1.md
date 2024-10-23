---
icon: elementor
---

# Data Encryption

### [Problem Statement:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-ProblemStatement%3A)[Solution for point 1:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-Solutionforpoint1%3A)[Solution for point 2: ](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-Solutionforpoint2%3A)[Solution for point 3: ](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-Solutionforpoint3%3A)[Solution for point 4: ](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-Solutionforpoint4%3A)[Approach 2:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1059651703/Data+Encryption#DataEncryption-Approach2%3A)Background  <a href="#dataencryption-background" id="dataencryption-background"></a>

In sunbird all user private data are stored as encrypted.  Currently sunbird is using **Salt**  based encryption service and there is only one salt is used for data encryption and decryption.

### Problem Statement: <a href="#dataencryption-problemstatement" id="dataencryption-problemstatement"></a>

New encryption service is using multi key based encryption. So now user private data can be encrypted with different-2 key value. This will lead following problems:

1. &#x20;User search using email , phone and userName or get user by email, phone
2. Get user by externalid, idType and provider
3. Providing user search response with decrypted attribute.
4. Checking user phone and email uniqueness

### Solution for point 1: <a href="#dataencryption-solutionforpoint1" id="dataencryption-solutionforpoint1"></a>

&#x20; User data will be encrypted with different keys and store inside elasticsearch. During search by phone,email or userName , incoming value will be encrypted with all existing keys and list will be provided to ES for match.

&#x20;Because email,phone or userName are unique in system , so either one or zero record will match. Same record can be pass to user.

&#x20;Note:

&#x20; 1\. For any user we are always showing masked email, masked phone , so no need to decrypt it , only decryption need to perform for username.

&#x20; 2\. Search with email,phone and username will have some performance impact.

\


### Solution for point 2:  <a href="#dataencryption-solutionforpoint2" id="dataencryption-solutionforpoint2"></a>

&#x20;As requested by Rahul , no need to store user external id as encrypted , so there is no issue of encryption and decryption here.

### Solution for point 3:  <a href="#dataencryption-solutionforpoint3" id="dataencryption-solutionforpoint3"></a>

&#x20;As of now in user search we are doing decryption of username only , other fields email and phone are coming as masked value. In System user name is not mandatory and during login as well we are not asking user to use user name, instead we are asking for phone or email based login. Due to system generated user name it's difficult for user to remember it. Other user also can't identify user based on username.

Example: I created a user with first name as Amit and another person also created user with firstName as Amit, So user name can be amit2134 and amit3245.

\


### Solution for point 4:  <a href="#dataencryption-solutionforpoint4" id="dataencryption-solutionforpoint4"></a>

&#x20;Phone and email uniqueness can be done as suggested in Point 1.

\


### Approach 2: <a href="#dataencryption-approach2" id="dataencryption-approach2"></a>

&#x20;Define salt value for each tenant and one for default(custodian). in that way we can use multi key to encrypt data and each tenant data will be encrypted with same key always.

| Pros                                                        | Cons​​                                                                                                               |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| <ol><li>User search can be done with private data</li></ol> | <ol><li>Search response time will increase</li><li>Still we can't perform phone and email uniqueness check</li></ol> |
