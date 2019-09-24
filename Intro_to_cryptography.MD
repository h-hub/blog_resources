# Introduction to Cryptography

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

Symmetric-Key Encryption: Try every key within the full algorithm until the right key is found.
Public-Key Encryption: 










https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/Introduction_to_Public_Key_Cryptography.html
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto/s-crypto-pdf.pdf
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto2/s-crypto2-pdf.pdf
https://www.ibm.com/developerworks/tivoli/tutorials/s-crypto3/s-crypto3-pdf.pdf
https://docs.oracle.com/cd/E13214_01/wli/docs70/b2bsecur/nonrep.htm
https://access.redhat.com/documentation/en-US/Red_Hat_Certificate_System/8.1/html/Deploy_and_Install_Guide/Introduction_to_Public_Key_Cryptography-Certificates_and_Authentication.html
