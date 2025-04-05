# cloud

## key vault
key vault is a way to manage secrets and keys with HSM security, and it could contains
- secret ( to be read and write)
- key (gen/import and actions)
- cert (lifecycle and distribution)

### there are 2 ways to access the keys
1. access policy
2. Role based access control - better, could control who to read/write what

### how does app access the key
App has a managed identity, which we could give permission to this identity to access the key vault to get the secret to the DB.

<img width="909" alt="Screenshot 2025-04-05 at 3 39 35 PM" src="https://github.com/user-attachments/assets/0f49cc8f-b6a4-41fd-a224-67e5f06264de" />

A **Key Vault** (like Azure Key Vault, AWS Secrets Manager, or HashiCorp Vault) is a **secure, centralized service for managing secrets** such as passwords, API keys, certificates, and cryptographic keys.

### 🔐 What's the Use of a Key Vault?

1. **Secure Secret Storage**  
   Stores secrets in an encrypted form, often backed by hardware security modules (HSMs) for strong protection.

2. **Centralized Management**  
   A single place to store and access secrets, instead of scattering them across config files, environment variables, code, or spreadsheets.

3. **Access Control**  
   Fine-grained access via role-based access control (RBAC), ensuring only authorized users/apps can access specific secrets.

4. **Audit and Monitoring**  
   Tracks when and by whom secrets are accessed or modified, helping with compliance and security audits.

5. **Automatic Secret Rotation**  
   Some vaults can automatically rotate secrets (e.g., regenerate passwords or keys) on a schedule to improve security.

6. **Integration with Cloud and DevOps Tools**  
   Easily integrates with cloud services (e.g., Azure, AWS) and CI/CD pipelines to securely retrieve secrets during deployments.

---

### 🆚 Why It's Better Than Traditionally Managed Passwords

| Feature                     | Traditional (Env Vars / Files / Hardcoded) | Key Vault                                          |
|----------------------------|---------------------------------------------|----------------------------------------------------|
| **Security**               | Often stored in plain text, risky           | Encrypted, HSM-backed                              |
| **Access Control**         | Limited control, often shared access        | Role-based, app-specific access                    |
| **Audit Logging**          | Manual or non-existent                      | Automatic logging of all access and changes        |
| **Secret Rotation**        | Manual and error-prone                      | Automated (in some systems)                        |
| **Centralized Management** | Scattered across servers/files              | Centralized and consistent                         |
| **Human Error Risk**       | High (e.g., commit secrets to Git)          | Lower (managed access and vault policies)          |

---

### ✅ Real-World Example

Instead of this:

```js
const dbPassword = "my-plaintext-password"; // Hardcoded secret 😬
```

You do this:

```js
const dbPassword = getSecretFromVault("db-password"); // Pulled securely at runtime ✔️
```

And the app has only permission to that one secret, not all.
