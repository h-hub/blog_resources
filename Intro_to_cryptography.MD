# Introduction to Cryptography
>"Security is not obtained through obscurity." 

With this thought in mind lets not dive, but take a swim in the Cryptography field. Because Programmers must know how Cryptography works.


> Cryptography, is the actual securing, control, and identification of digital data.

As Developers or Software Engineers it is important to know the concepts of cryptography since application security needs to implemented by the programmers. Insecure applications could jeopardize systems and as a result your clients can loose businesses.

Cryptography is being used nearly everywhere in computer system. Internet is filled with system which need to control the access and usage of computer programs or digital data and they use  cryptography for that.

We are somewhat familiar with or at least have heard about concepts such as OAuth, 2FA, JWT, IAM and SSO. And all these topics are directly connected to Cryptography. Cryptography comes under **Cryptology** and Cryptanalysis is the sister branch of Cryptography.

            Cryptology
            /       \
           /         \
    Cryptography    Cryptanalysis

> Cryptanalysis, is made up of all the attempts one might develop to undermine, circumvent, and/or break what the first part, cryptography, is attempting to accomplish.

Cryptanalysis is absolutely essential to cryptography. Cryptanalysis is a way of crash testing cryptography. If Cryptanalysis is failing that means your cryptography methods are working properly as expected. Cryptanalysis helps to find the failing points of cryptography.

## The four objectives of cryptography

1. **Confidentiality**: It is the privacy or secrecy of information. It prohibits unauthorized people from accessing the information and it is achieved by using scrambled text, cipher text, or encrypted text.

2. **Integrity**: Prove that a message has not been altered in unauthorized ways. This can be done by using a cryptographic hash.

3. **Authentication**: Prove that a message actually originates with its claimed originator. That means it provides the identification of the originator, so that receiver knows that the message was sent by an identified and verified sender(originator).

4. **Non-repudiation**: Prevent an originator from denying credit (or blame) for creating or sending a message. According to wikipedia **"Non-repudiation refers to a situation where a statement's author cannot successfully dispute its authorship or the validity of an associated contract"**. More about Non-repudiation -> https://docs.oracle.com/cd/E13214_01/wli/docs70/b2bsecur/nonrep.htm

## Protocols and algorithms
Protocols and algorithms are equaly important when it comes to cryptography. A protocol is a specification of the complete set of steps involved in carrying out a cryptographic activity.A cryptographic algorithm is a mathematical function used for encryption or decryption.. Protocols must use one or more algorithms to secure data.

## Encryption and Decryption
Encryption is the process of transforming information so it is unintelligible to anyone but the intended recipient. Decryption is the process of decoding encrypted information.

A cryptographic **algorithm**, also called a cipher, is a mathematical function used for encryption or decryption.

Modern cryptography uses a number called a **key** to keep encrypted information secret. Algorithms are widely known. The key must be used to encrypt or decrypt information. Decryption without the correct key is impossible.

There are two different categories of encryption algorithms

                        Encryption
                        /       \
                       /         \
    Symmetric-Key Encryption   Public-Key Encryption      

### 1.Symmetric-Key Encryption
The encryption key can be calculated from the decryption key and vice versa. The same key is used for both encryption and decryption.

![alt text](https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/images/05scrypt2.png)
 - This encryption can be highly efficient.
 - It provides a degree of authentication.
 - But, if somebody can discover the secret key, they not only can decrypt messages with that key, but can encrypt new messages and send.
 
This method is widely used in the SSL communication.

### 2.Public-Key Encryption (Asymmetric encryption)
This method involves a public key and a private key, associated with an entity. Each public key is published, and the corresponding private key is kept secret.

![alt text](https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/images/06pcrypt.png
)

**Data encrypted with a public key can be decrypted only with the corresponding private key.**

 - May not be feasible for encrypting and decrypting large amounts of data.
 - This method can be used to send a Symmetric-Key and use that key to secure data (SSL/TLS protocols).
 
Private-key encryption(Inverse of Public-Key Encryption) is useful because it means the private key can be used to sign data with a digital signature.

## Breaking an encryption algorithm
To break an algorithm, you need to find the key to access the encrypted data in plain text.

For Symmetric-Key Encryption: Breaking the algorithm usually means trying to determine the key used to encrypt the text.

For Public-Key Encryption: Breaking the algorithm usually means acquiring the shared secret information between two recipients.

### How to break ?

 - Symmetric-Key Encryption: Try every key within the full algorithm until the right key is found.
 - Public-Key Encryption: Private key can be derived using published, using complex, mathematical calculations.

Manually finding the key to break an algorithm is called a brute force attack. A brute force attack is trying to find the username, password or a key using a trial and error approach. Using this method, attackers are trying to guess the credentials correctly eventually.

### Strength

> The key strength of an algorithm is determined by finding the fastest method to break the algorithm and comparing it to a brute force attack.
 - Symmetric-Key Encryption: Encryption strength is often described in terms of the size or length of the keys used to perform the encryption.
   - 128-bit keys with the RC4 symmetric-key cipher supported by SSL provide significantly better cryptographic protection than 40-bit keys used with the same cipher.
   - 128-bit RC4 encryption is 3 x 1026 times stronger than 40-bit RC4 encryption.
   
 - Public-Key Encryption: Requires different key lengths to achieve the same level of encryption strength as a symmetric-key cipher.
   - RSA public-key encryption cipher must have at least 1024 bits key to be considered strong.
   {more about RSA}
 
 
An encryption key is considered full strength if the best known attack to break the key is no faster than a brute force attempt to test every key possibility.

## Digital Signatures

A digital signature is similar to a handwritten signature and is as legally binding as a handwritten signature. Most importantly digital signatures provides a high degree of nonrepudiation.One cannot deny having signed the data.

I have devided this topic into small sections for the ease of understanding.

### One-way functions
It is a lot harder to get the toothpaste back in the tube than it was to get it out. It is a lot easier to multiply together some large primes than it is to factor the product.

>One-way functions are functions that are computationally easy to compute, but computationally infeasible to reverse.

Cryptographic one-way functions are function that can perform in milliseconds on computers, but believe it would take these same computers millions of years to reverse.

### Cryptographic hashes

A hash is similar to a one-way function, but rather than being a total function (one whose inverse is also a function), a hash takes a long message and produces a comparatively short output.

Example : Errorchecking codes (ECC), such as CRC32 (32 bits)

**Cryptographic hash** is (believed to be) computationally infeasible to find a message that produces a given hash that means the content of the hashed message cannot be deduced from the hash. The out put is 128 bits or longer. The value of the hash is unique for the hashed data. Any change in the data could alter the hash.

       message/data >>>> hashing >>>>>>> hashed(message/data) >>>>> X >>>>> message/data

Other names for Cryptographic hashes : "message digests","fingerprints", "cryptographic checksums", or "message integrity checks.

### What is a Digital Signature ?

>Firstly, a one-way hash of the data is created, then uses the private key to encrypt the hash. The encrypted hash, along with other information such as the hashing algorithm, is known as a digital signature.

Below image explains it properly.


![alt text](https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/images/04digsgn.png
)


1. Original data is hashed using a hashing algorithm.
2. Hash is encrypted using a private key.
3. Data is transfered to the receiver (Digital Signature = encrypted hash + hashing algorithm).
4. Receiver uses the public key to decrypt the hash.
5. Then uses the same hashing algorithm to generate a hash.
6. Then compares the new hash against the original hash.
7. If matching, the data has not been changed.

Two hashes are matching means,receiver can confirm that public key corresponds to the private key which used during the create the digital signature. But this is not enought to identify the user. I'll dicuss this in the next section(Certificates and Authentication).

## Certificates and Authentication
>A certificate is an electronic document used to identify an individual, a server, a company, or other entity and to associate that identity with a public key.

A certificate is like passport which can be used to proove our identity.Public-key cryptography uses certificates to prohibit impersonation.













https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/Introduction_to_Public_Key_Cryptography.html
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto/s-crypto-pdf.pdf
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto2/s-crypto2-pdf.pdf
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto3/s-crypto3-pdf.pdf
https://docs.oracle.com/cd/E13214_01/wli/docs70/b2bsecur/nonrep.htm
https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/Introduction_to_Public_Key_Cryptography-Certificates_and_Authentication.html
https://www.kaspersky.com/resource-center/definitions/brute-force-attack
