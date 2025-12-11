## Introducing Cryptography Concepts

Cryptography uses mathematical concepts to protect data.

| Concept | Description | Security Goal(s) Provided | Core Mechanism |
| :--- | :--- | :--- | :--- |
| **Integrity** | Provides assurance that data has **not been modified**. | Integrity | **Hashing** (A **hash** is a fixed-length alphanumeric string derived from data. Comparison verifies integrity). |
| **Confidentiality** | Ensures data is only viewable by **authorized users**. | Confidentiality | **Encryption** (Scrambles data to make it unreadable; requires an **algorithm** and a **key**). |
| **Authentication** | Validates an **identity**. | Authentication | Digital Certificates, Passwords, Biometrics (covered in detail elsewhere). |
| **Non-repudiation** | Prevents a party from successfully **disputing** having performed an action (e.g., sending an email). | Non-repudiation | **Digital Signatures**. |

### 1. Hashing

* A hash is a fixed-length string created by applying a mathematical function (hashing algorithm) to data (message, file, etc.).
* It is a **one-way function**; the hash cannot be reversed to re-create the original data.
* **Common Algorithm:** Secure Hash Algorithm 3 (**SHA-3**).

### 2. Encryption Types 

| Type | Key Usage | Cipher Type | How it Works |
| :--- | :--- | :--- | :--- |
| **Symmetric Encryption** | Uses the **same key** to encrypt and decrypt data. | **Block Cipher** (encrypts data in blocks) or **Stream Cipher** (encrypts data 1 bit at a time). | Faster and more efficient for bulk data encryption. |
| **Asymmetric Encryption** | Uses two mathematically linked keys: a **public key** and a matching **private key**. | Requires a **Public Key Infrastructure (PKI)** to issue certificates. | Data encrypted with the **public key** can *only* be decrypted with the matching **private key**. Conversely, data encrypted with the **private key** can *only* be decrypted with the matching **public key**. |

### 3. Steganography and Digital Signatures

* **Steganography:** Provides confidentiality by **hiding data within other files** (e.g., embedding data in the white space of a picture file).
* **Digital Signature:** Provides **Authentication**, **Non-repudiation**, and **Integrity** in a single mechanism.
    * It is created by taking a **hash** of the message and encrypting that hash using the sender's **private key**.
    * The recipient uses the sender's **public key** to decrypt the digital signature and reveal the hash, which confirms the hash was created by the owner of the private key (authentication and non-repudiation). The recipient then compares this hash to a hash of the received message (integrity).

## Providing Integrity with Hashing

**Hashing** is a mathematical algorithm that creates a fixed-length hexadecimal string (the **hash**) from data (file, message, password). It is used to verify that data has maintained **integrity** (has not been modified).

### 1. Hash vs. Checksum

| Feature | Hash | Checksum |
| :--- | :--- | :--- |
| **Length** | Much longer (e.g., 128-bit, 256-bit). | Typically small (e.g., 1 or 2 bits, or a single check digit). |
| **Purpose** | Strong cryptographic integrity and identity verification. | Quick, non-cryptographic integrity check (e.g., RAID parity, credit card validation). |
| **Security** | Designed to be cryptographically secure (e.g., SHA-3). | Not intended to be cryptographically secure. |

### 2. Hashing Algorithms

A hash is a **one-way function**; it cannot be reversed to re-create the original data. 

| Algorithm | Hash Size | Security Status | Use Case |
| :--- | :--- | :--- | :--- |
| **MD5** (Message Digest 5) | 128 bits (32 hex characters) | **Cracked/Vulnerable** (Susceptible to collision attacks). | **Discouraged** for cryptographic use; sometimes used for quick file integrity checks (checksums). |
| **SHA-1** (Secure Hash Algorithm 1) | 160 bits | **Vulnerable** (No longer approved for most cryptographic uses). | Legacy integrity checks. |
| **SHA-2** | 224, **256**, 384, **512** bits | **Strong/Current** | Cryptographic hashing, digital signatures, password storage. |
| **SHA-3** (Keccak) | 224, **256**, 384, **512** bits | **Strong/Current** (Alternative to SHA-2). | Cryptographic hashing, digital signatures, password storage. |

### 3. Hash-based Message Authentication Code (HMAC)

An **HMAC** is a hashing algorithm (like HMAC-MD5 or HMAC-SHA256) that uses a **shared secret integrity key** in the calculation.

* **Benefit:** Provides both **integrity** (via the hash comparison) and **authenticity** (since only the sender and receiver know the secret key).
* **Mitigation of SPOF:** HMAC prevents an attacker from modifying a message *and* calculating a new hash to cover the change, because the attacker lacks the secret key needed to create a valid HMAC hash.
* **Usage:** Used in protocols such as IPsec and TLS.

### 4. Hash Collisions and Password Security

* **Hash Collision:** Occurs when a hashing algorithm creates the **same hash** for two different inputs.
    * This is highly undesirable in cryptography as it allows an attacker to use a different input (e.g., a different password) that generates the same stored hash to gain unauthorized access. MD5 is highly susceptible to this.
* **Hashing Passwords:** Systems store a hash of the password, not the password itself.
    * When a user attempts to log in, the system hashes the entered password and compares it to the stored hash.
    * Only **strong hashing algorithms** (like SHA-3) should be used for password storage. Passwords are also often **salted** (extra characters added) before hashing to increase security.

## Understanding Password Attacks

Password attacks attempt to discover or bypass passwords used for authentication.

| Attack Type | Target | Description | Indicators / Mitigation |
| :--- | :--- | :--- | :--- |
| **Online Attack** | Live authentication system (e.g., login portal). | Repeatedly guessing username/password combinations against an active service (e.g., using `ncrack`). | System logs show repeated **Event ID 4625** (failed logon attempts). Mitigated by **Account Lockout Policies** (**Event ID 4740**). |
| **Offline Attack** | Captured database or password file (e.g., during a data breach). | Attempts to discover the original password from the stored password **hash** without interacting with the live system. | Mitigated by strong hashing algorithms (SHA-3) and **Key Stretching**. |
| **Dictionary Attack** | Online or Offline. | Uses a pre-compiled list of common words, passwords, and character combinations (a "dictionary"). | Mitigated by **Complex Passwords** that are not found in common wordlists. |
| **Brute Force Attack** | Online or Offline. | Attempts to guess **all possible character combinations** (uppercase, lowercase, numbers, special characters). | Mitigated by **Longer, Complex Passwords** and **Key Stretching**. |
| **Password Spraying** | Online (large list of accounts). | Tries **one password** against a **large list of accounts** before trying the next password, designed to bypass time-based **Account Lockout Policies**. | Logs show many **Event ID 4625** entries spread out over time for different accounts. |
| **Pass the Hash (PtH) Attack** | Network Authentication Protocol (e.g., NTLM, Kerberos). | Attacker steals the user's password **hash** and uses the hash itself to authenticate to another system without ever needing to decrypt the actual password. | Windows logs show **Event ID 4624** with **NTLMSSP** as the Logon Process or **NTLM** as the Authentication Package. |
| **Birthday Attack** | Hashing Algorithm. | Exploits the mathematical concept of a **hash collision** (two different inputs producing the same hash). Attacker only needs to find one input that produces the target hash. | Mitigated by using strong, long-bit hashing algorithms (e.g., SHA-3 512-bit) that are resistant to collisions. |
| **Rainbow Table Attack** | Password Hash Database (Offline). | Uses a huge **precomputed database** (rainbow table) of plaintext passwords and their corresponding hashes to quickly look up and discover passwords from stolen hashes. | Thwarted by **Salting Passwords** and **Key Stretching**. |

### 5. Password Protection Techniques

These techniques make offline attacks (especially rainbow table and brute-force attacks) computationally expensive or impossible.

#### Salting

* **Mechanism:** A **salt** (a set of random data/characters) is added to a user's password *before* it is hashed.
* **Result:** A unique hash is created, even for identical passwords used by different users.
* **Mitigation:** Thwarts **Rainbow Table Attacks** because the precomputed hashes in the table will not match the salted hashes.

#### Key Stretching

Key stretching is an advanced technique that repeatedly applies a cryptographic algorithm to a password and salt. This consumes more time and computing resources, frustrating attackers.

| Technique | Based On | Key Features | Mitigation |
| :--- | :--- | :--- | :--- |
| **Bcrypt** | Blowfish block cipher. | Adds salt, encrypts the password, and can repeat the process multiple times (iterations). Creates a 60-character string. | Highly resistant to brute-force attacks due to computational overhead. |
| **PBKDF2** (Password-Based Key Derivation Function 2) | Pseudo-random functions (e.g., HMAC). | Uses salts of at least 64 bits and can iterate the hashing process up to 1,000,000 times. | Used in WPA2 and some mobile OSs; computational cost makes brute force difficult. |
| **Argon2** | PHC winner (2015). | Optimized for modern processors, uses parallel processing. Designed to use configurable amounts of CPU time and RAM. | Considered a strong alternative to bcrypt and PBKDF2 for password storage. |

## Providing Confidentiality with Encryption

**Encryption** provides **confidentiality** by scrambling human-readable **plaintext** into unreadable **ciphertext** using an **algorithm** (mathematical calculations) and a **key** (a number providing variability).

| Data State | Description | Common Protection Method |
| :--- | :--- | :--- |
| **Data at Rest** | Data stored on media (databases, files, disks). | Full disk encryption, file/folder encryption, database field encryption. |
| **Data in Transit (Motion)** | Data sent over a network. | TLS/SSL (e.g., HTTPS sessions). |
| **Data in Use** | Data being actively processed by a computer (decrypted and stored in memory). | Memory purging after processing sensitive data. |

### 1. Symmetric Encryption

**Symmetric encryption** uses the **same key** to encrypt and decrypt data. It is also called **secret-key** or **session-key** encryption. 

* **Substitution Cipher:** A simple symmetric cipher (e.g., ROT13) that replaces plaintext with ciphertext using a fixed key (e.g., rotating letters by 13 places). ROT13 is an **obfuscation** method, not true encryption.
* **Key Strength:** Directly corresponds to the **key length** (more bits = stronger key). Symmetric keys should be changed frequently and not reused.

#### Block Ciphers vs. Stream Ciphers

| Cipher Type | Mechanism | Efficiency | Example Use |
| :--- | :--- | :--- | :--- |
| **Block Cipher** | Encrypts data in **fixed-size blocks** (e.g., 64-bit or 128-bit blocks). | Efficient when the data size is known (e.g., encrypting a file or database field). | AES, 3DES. |
| **Stream Cipher** | Encrypts data as a continuous **stream of bits or bytes**. | More efficient when data size is unknown or continuous (e.g., streaming audio/video over a network). | Requires keys to never be reused to maintain security. |

#### Common Symmetric Algorithms

| Algorithm | Key Size (Bits) | Block Size (Bits) | Description |
| :--- | :--- | :--- | :--- |
| **AES** (Advanced Encryption Standard) | **128, 192, 256** | **128** | Strong, fast, and efficient successor to DES. The current NIST standard. |
| **3DES** (Triple DES) | 112 or **168** | **64** | Encrypts data using the DES algorithm in three separate passes with multiple keys. Resource intensive compared to AES. |
| **Blowfish** | 32 to 448 | **64** | Strong, general-purpose algorithm; faster than AES-256 in some instances. |
| **Twofish** | 128, 192, 256 | **128** | Related to Blowfish; a finalist in the AES competition. |

### 2. Asymmetric Encryption

**Asymmetric encryption** uses a matched pair of two keys: a **public key** and a **private key**. 

* **Confidentiality:** If the **public key** encrypts information, **only the matching private key** can decrypt it. Public keys are freely shared (via certificates); private keys are kept secret.
* **Authentication/Non-repudiation:** If the **private key** encrypts information (e.g., a digital signature), **only the matching public key** can decrypt it.
* **Performance:** Asymmetric encryption is **resource intensive**. It is primarily used for **key exchange** (sharing a symmetric key) rather than bulk data encryption.

#### Key Concepts

* **Key Exchange:** The process of using asymmetric encryption to securely share a symmetric key. The subsequent data transfer uses the faster symmetric encryption.
* **Digital Certificate:** A digital document issued by a **Certificate Authority (CA)** that includes the owner's **public key** and identifying information. Used for sharing public keys and verifying identity.
    * **Certificate Elements:** Serial number, Issuer (CA), Validity Dates, Subject (owner), Public Key, Key Usage.
    * **Distinguished Name Attributes:** CN (Common Name/FQDN), O (Organization), L (Locality), S (State), C (Country).
* **Ephemeral Keys:** Keys created for a single session and then discarded (short lifetime). They support **Perfect Forward Secrecy**, which ensures that the compromise of a key does not compromise any past keys.
* **Elliptic Curve Cryptography (ECC):** A method that requires less processing power than others. It allows for much smaller keys (e.g., 256-bit ECC provides the same security as a 3072-bit DSA key). Often used in low-power devices.
    * **ECDSA** (Elliptic Curve Digital Signature Algorithm) is used for digital signatures.
* **Key Length (Asymmetric):** Recommended minimum key length for algorithms like RSA is **2048 bits**.

### 3. Obfuscation Techniques

**Obfuscation** is the act of deliberately making something unclear or difficult to understand, often to hide information.

| Technique | Description | Use Case | Detection Method |
| :--- | :--- | :--- | :--- |
| **Steganography** | Hides data (message, file) **inside other data** (audio, image, video files) in a way that is not readily apparent. | Hiding a message in an image by altering the least significant bit (LSB) or using white space. | **Steganalysis** (detecting changes by comparing file **hashes**). |
| **Tokenization** | Replaces sensitive data (e.g., credit card number) with non-sensitive **placeholders (tokens)**. The original data is stored securely in a separate vault. | Payment processing and protecting PII; reduces the scope of a data breach. | N/A (Non-sensitive data is stored). |
| **Masking** | Partially or fully **conceals** sensitive data with characters or symbols (e.g., displaying only the last four digits of an account number: `123*****1208`). | Displaying sensitive data on-screen, sharing data for development/testing, or password fields. | N/A (Data is concealed but still functional for processing). |

## Using Cryptographic Protocols

Cryptographic protocols combine asymmetric and symmetric encryption and hashing to achieve multiple security goals.

| Protocol Goal | Key Used for **Encryption** (Signing) | Key Used for **Decryption** (Verification) | Security Goals Provided |
| :--- | :--- | :--- | :--- |
| **Email Digital Signature** | Sender's **Private Key** (encrypts the hash) | Sender's **Public Key** | Authentication, Non-repudiation, Integrity |
| **Email Encryption (Confidentiality)** | Recipient's **Public Key** (encrypts the symmetric key) | Recipient's **Private Key** | Confidentiality |
| **Website Encryption (Key Exchange)** | Website's **Public Key** (encrypts the symmetric session key) | Website's **Private Key** | Key Exchange for Confidentiality |

### 1. Protecting Email

Email uses **S/MIME** (Secure/Multipurpose Internet Mail Extensions) standards, which combine asymmetric and symmetric encryption.

#### A. Digital Signatures

* **Process:** The sender's email application **hashes** the message. The hash is then encrypted using the sender's **private key** to create the digital signature. 
* **Verification:** The recipient uses the sender's **public key** (from the sender's certificate) to decrypt the signature and reveal the hash. The recipient then calculates a hash on the received message and compares the two hashes.
* **Results:** If hashes match, it proves:
    * **Authentication:** Only the sender has the private key.
    * **Non-repudiation:** The sender cannot deny having sent the message.
    * **Integrity:** The message has not been modified.

#### B. Email Encryption

* **Process (Hybrid):** Uses asymmetric encryption for efficiency. 
    1.  Sender creates a random **Symmetric Session Key** (e.g., AES key).
    2.  Sender encrypts the email contents with the **Symmetric Session Key**.
    3.  Sender encrypts the **Symmetric Session Key** using the **Recipient's Public Key**.
    4.  Recipient uses their **Private Key** to decrypt the Symmetric Session Key.
    5.  Recipient uses the decrypted **Symmetric Session Key** to decrypt the email contents.

* **S/MIME Ports (TLS/SSL):**
    * POP3-over-TLS: Port 995
    * SMTP-over-TLS: Port 587
    * IMAP-over-TLS: Port 993

### 2. HTTPS Transport Encryption (TLS Handshake)

**TLS** (Transport Layer Security, the successor to SSL) encrypts HTTPS traffic using a **hybrid approach** to ensure confidentiality. TLS requires **certificates** issued by a **Certificate Authority (CA)**. 

| Step | Asymmetric / Symmetric / Other | Action |
| :--- | :--- | :--- |
| 1. Client Hello | Other | Client requests an HTTPS session. |
| 2. Server Hello | Asymmetric | Server sends its **Certificate** (containing the **Public Key**). |
| 3. Key Exchange | Asymmetric | Client creates a **Symmetric Session Key** and encrypts it using the server's **Public Key**. |
| 4. Key Delivery | Asymmetric | Client sends the encrypted Session Key to the server. |
| 5. Key Decryption | Asymmetric | Server uses its **Private Key** to decrypt the Session Key. (Client and Server now know the symmetric key). |
| 6. Data Transfer | Symmetric | All subsequent session data is encrypted and decrypted using the **Symmetric Session Key**. |

#### Downgrade Attacks

* An attack that forces a system to use a weaker, deprecated protocol or cipher suite (e.g., forcing a server to use vulnerable SSL instead of TLS).
* **Mitigation:** Administrators must **disable weak protocols** (like SSL) and vulnerable cipher suites on the server.

### 3. Blockchain

A **blockchain** is a distributed, decentralized, public ledger.

* **Block Components:** Transaction information, parties involved (using **digital signatures**), and a **unique hash** for the block.
* **Chain Mechanism:** Each new block includes the **hash of the immediately preceding block**, linking them cryptographically and ensuring integrity.
* **Cryptocurrency:** Bitcoin uses blockchain; transactions are verified and recorded by network computers (**miners**).

### 4. Cryptographic Limitations

When choosing algorithms, organizations must balance **security constraints** with **resource availability**.

| Limitation Factor | Description / Consideration |
| :--- | :--- |
| **Resources** | Encryption increases data size (storage) and consumes processing time/power (CPU/memory overhead). |
| **Speed/Time** | Encryption algorithms should be quick. Password hashing algorithms (like bcrypt) should be intentionally **slow** to thwart brute-force attacks. |
| **Size/Overhead** | Computational and memory requirements. Lightweight cryptography is needed for low-power devices. |
| **Entropy** | The level of **randomness** in an algorithm. Higher entropy = higher security. Lack of entropy (predictability) leads to weaker keys. |
| **Weak Keys** | Short keys (e.g., 1024-bit RSA keys) or reused symmetric keys (especially in stream ciphers) make even strong algorithms vulnerable. |
| **Longevity** | How long an algorithm remains secure against projected increases in processing power (e.g., DES was deprecated due to short key length). |
| **Key Reuse** | Symmetric keys should never be reused, particularly in stream ciphers (e.g., WEP failure). |
| **Plaintext Attacks** | **Known-plaintext** (attacker has some plaintext and corresponding ciphertext) and **Chosen-plaintext** attacks are often successful and can compromise the encryption method. |

## Exploring PKI Components

A **Public Key Infrastructure (PKI)** is a group of technologies used to request, create, manage, store, distribute, and revoke digital certificates. It enables secure communication between entities that do not know each other.

### 1. Certificate Authority (CA) and Trust

* **Certificate Authority (CA):** Issues, manages, validates, and revokes digital certificates. CAs can be public (e.g., DigiCert) or private (internal).
* **Root of Trust:** The foundation of trust in a PKI. The CA's authority is established by placing its **Root Certificate** into an operating system's or web browser's **Trusted Root Certificate Store**.
* **Hierarchical Trust Model:** The most common model.
    * **Root CA (Trust Anchor):** The self-signed first CA, typically kept **offline** for security.
    * **Intermediate CAs:** Created by the Root CA to issue **leaf certificates** to end-entities (users, servers). They act as a buffer to protect the Root CA.
    * **Certificate Chaining:** Combines all certificates from the Root CA down to the end-entity certificate. 

### 2. Registration and Issuance

* **Registration Authority (RA):** An entity that assists the CA by collecting and verifying registration information from users. The RA **never issues** certificates.
* **Certificate Signing Request (CSR):** A digitally formatted file (**PKCS #10** specification) sent to the CA to request a certificate.
    * The requestor first creates an RSA-based **public/private key pair**.
    * The CSR contains the **public key** and information about the requestor and the certificate's purpose.
    * The **private key** is **never** sent to the CA.
* **Online vs. Offline CAs:**
    * **Online CA:** Accessible over the network; can automate CSR submissions.
    * **Offline CA:** Not accessible over the network; only accepts manual submissions (often used for the highly protected **Root CA**).

### 3. Certificate Status and Revocation

CAs can revoke a certificate before its expiration for several reasons (e.g., private key compromise, CA compromise, change of affiliation).

| Mechanism | Description | Response Type | Benefit / Use Case |
| :--- | :--- | :--- | :--- |
| **Certificate Revocation List (CRL)** | A publicly available version 2 certificate containing a list of **serial numbers** for all revoked certificates. Clients download and cache this list. | List of serial numbers. | Standard method for verifying revocation status. Caching reduces network traffic to the CA. |
| **Online Certificate Status Protocol (OCSP)** | A protocol where the client queries the CA in **real-time** with a certificate's serial number. | "good," "revoked," or "unknown." | Low latency, immediate revocation updates. (Generates high CA traffic). |
| **OCSP Stapling** (Certificate Stapling) | The server (certificate presenter) obtains a signed, timestamped OCSP response from the CA and **appends (staples) it** to the certificate during the TLS handshake. | Timestamped "good" status. | Reduces the real-time OCSP traffic load on the CA. |

* **Validation Checks:** When a client receives a certificate, it checks if it is: **Not Expired**, issued by a **Trusted CA** (checking the Trusted Root Store), and **Not Revoked** (checking CRL or OCSP).

### 4. Advanced PKI Concepts

* **Certificate Pinning:** A mechanism where a website provides clients with a list of **hashes** of its valid public keys (or keys in the chain) via an extra HTTP header. Clients store these hashes and compare them on subsequent connections to prevent impersonation via fraudulent certificates.
* **Key Escrow:** The process of placing a copy of a **private key** in a safe environment for **recovery** purposes if the original key is lost or inaccessible.
    * A **Key Recovery Agent (KRA)** is a designated individual authorized to recover or restore cryptographic keys (e.g., using a separate recovery key for full disk encryption).
* **Key Management System (KMS):** A centralized service for the secure management of the entire key lifecycle: **Generation, Storage (e.g., HSMs), Distribution, Rotation, Revocation, and Destruction**.

### 5. Comparing Certificate Types

| Certificate Type | Usage | Key Feature |
| :--- | :--- | :--- |
| **Machine/User** | Identifies a device or an end-user for authentication and encryption (e.g., EFS). | Standard identity-based certificates. |
| **Code Signing** | Used by developers to digitally sign applications/scripts. | Verifies the authenticity of the code and that it has not been modified. |
| **Self-Signed** | Not issued by a trusted public CA (often created by a private, internal CA). | Not trusted by default; must be manually or automatically added to the trusted store. |
| **Wildcard** | Used for multiple subdomains under the same root domain (e.g., `*.google.com`). | Reduces administrative burden. |
| **Subject Alternative Name (SAN)** | Used for multiple distinct domain names owned by the same entity (e.g., `google.com` and `google.net`). | Consolidates multiple domain names into one certificate. |
| **Domain Validation (DV)** | CA verifies that the requestor controls the DNS domain (low bar). | Basic level of trust. |
| **Extended Validation (EV)** | Requires additional verification steps beyond DV (use is declining). | Highest level of vetting. |

### 6. Comparing Certificate Formats

Most certificates use the **X.509 v3** standard. Formats are categorized by encoding and what they contain.

| Format/Extension | Encoding | Contains (Commonly) | Description / Use Case |
| :--- | :--- | :--- | :--- |
| **CER/DER** (Base Formats) | **CER:** ASCII (BASE64) / **DER:** Binary | Certificate/Public Key | Base encoding formats. |
| **PEM** (`.pem`, `.cer`, `.crt`, `.key`) | ASCII (BASE64) | Public Key, Private Key, CSR, CRL | Most widely used format; can contain almost any element. |
| **P7B** (PKCS #7) | ASCII (BASE64) | **Public Key**, Certificate Chain, CRL | Commonly used to share public keys or certificate chains. **Never includes the private key.** |
| **P12** (PKCS #12) / **PFX** | **Binary** | **Private Key**, Public Key, Certificate Chain | Commonly used to securely export/import certificates along with their private keys (e.g., for web servers). **Typically encrypted.** |


