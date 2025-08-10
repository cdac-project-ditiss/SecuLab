## SSL/TLS Certificate Generation using Root CA and Subordinate CA

This section documents the process used to generate and manage certificates for internal services:
- `mail.dexter.local`
- `fw.dexter.local`
- `web.dexter.local`
- `nagios.dexter.local`

The PKI (Public Key Infrastructure) model was implemented with a **Root Certificate Authority (Root CA)** and a **Subordinate Certificate Authority (Sub-CA)**.

---

### 1. Create Root CA
1. Generate the **Root CA private key**.
2. Create a **self-signed Root CA certificate** using the private key.
3. Store both securely — the Root CA key should never be shared.

---

### 2. Create Subordinate CA
1. Generate the **Sub-CA private key**.
2. Create a **Certificate Signing Request (CSR)** for the Sub-CA, signed with its **own private key**.
3. Submit the Sub-CA CSR to the Root CA.
4. **Root CA signs the Sub-CA CSR** and issues the Sub-CA certificate.
5. Store the Sub-CA certificate and private key securely.

---

### 3. Generate Entity Certificates (Internal Services)
For each service (`mail.dexter.local`, `fw.dexter.local`, `web.dexter.local`, `nagios.dexter.local`):

1. **Generate a key pair** (private + public key) for the entity.
2. Create a **CSR** containing:
   - Public key
   - Common Name (CN) — e.g., `mail.dexter.local`
   - Organizational details (O, OU, etc.)
   - Other required certificate attributes
3. **Digitally sign the CSR** using the entity’s **private key**.
4. Submit the CSR to the **Sub-CA**.
5. **Sub-CA verifies the CSR** by:
   - Checking the digital signature using the entity’s public key
   - Validating the provided details
6. **Sub-CA signs the CSR** with its **private key** and issues the certificate.
7. Install the issued certificate on the respective service.

---

### 4. Certificate Formats Used
During the process, certificates were generated in the following formats:

#### **.pem (Privacy Enhanced Mail)**
- **Type**: Base64 encoded text format.
- **Contains**: Certificates, certificate chains, and private keys (when applicable).
- **Usage**: Commonly used for web servers (Apache, Nginx, Fortinet Firewall, etc.).
- **Advantages**: Human-readable, easy to store and share securely.

#### **.pfx (Personal Information Exchange)**
- **Type**: Binary format.
- **Contains**: Private key, certificate, and optionally the full certificate chain — all in a single file.
- **Usage**: Typically used for importing into Windows servers, Microsoft IIS, or applications that require both the certificate and key in one file.
- **Advantages**: Convenient for transport, especially when moving between platforms.

---

### 5. Outcome
- All internal services now use **trusted certificates** issued via the internal PKI chain.
- Certificates are available in both `.pem` and `.pfx` formats, ensuring compatibility with different platforms and systems.
- Communication between devices and services is encrypted and authenticated.

---

**PKI Hierarchy Overview:**

```
Root CA
   |
   ---> Subordinate CA
           |
           ---> mail.dexter.local certificate
           ---> fw.dexter.local certificate
           ---> web.dexter.local certificate
           ---> nagios.dexter.local certificate
```
