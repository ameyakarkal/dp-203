
## Auditing | Encryption

References : 
- [Implement Data Auditing with Azure Data Lake](https://app.pluralsight.com/library/courses/implement-data-auditing-azure-data-lake/table-of-contents)

- Azure SQL DB 
    - Dynamic Data Masking.
    - setup masking per column of table

## Encryption

- Types of encryption algorithms
    - Type of Key used
        - Symmetric
            - encryption key encrypts
            - decryption key decrypts 
            - encryption key = decryption key
            - performant
        - Asymmetric
            - entryption key encrypts
            - decryption key decrypts 
            - encryption key != decryption key
            - not performant
    - Behavior of Encrypted output
        - Deterministic
            - same encrypted output for same input
            - can be used for lookups / joins
        - Randomized / Indeterministic
            - opposite of deterministic
    - Column Encryption Key
        - used to encrypt specific columns
        - 
    - Column Encryption Master Key
        - metadata object in database
        - stored externally 
        - used to encrypt ALL column encryption keys
- Types of encryption
    - at rest
        - storage is encrypted
    - in transit
    - in use / generated

### Storage Account
- Encryption Tab
    - key is managed by azure
    - key is managed by user

### Azure SQL Server
- Transparent Data Encrpytion Tab
    - enabled by default
### Azure SQL Database
- Transparent Data Encrpytion Tab
    - key managed by azure
    - key managed by user



## Secure Endpoint Security
- service endpoint allow access azure services 
- service enables IP addresses