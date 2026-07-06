# Secure Off-Chain Medical Records Access Platform

An enterprise-grade decoupled application architecture utilizing a frontend user bus interface (Vue 2), a secure backend routing API engine (Express.js), and two distinct high-performance off-chain caching schemas (Redis) to separate and manage User-to-Document and Document-to-User permissions.

---

## 🏗️ Folder Tree Map
```text
medical-blockchain-project/
├── package.json                   # Root Frontend configuration (patched with regenerator-runtime)
├── run-application.sh             # Gateway installation automation script
├── server/                        # Backend Processing Engine
│   ├── app.js
│   └── config.json                # Redis connection parameters
└── src/                           # Vue Client Engine code
    ├── main.js
    ├── components/                # Stakeholder portals (Admin, Doctor, Patient)
    └── secrets/
        └── config.json            # Base system routing map

```

---

## 🚀 How to Run the Project Locally

### 1. Boot up the Off-Chain Target Databases

The platform caches dual-directional authorization logs inside two isolated database container processes. Spin them up sequentially using your terminal terminal:

```bash
# Database 1: User-to-Document Permissions Mapping Node
docker run -d --name redis-user-to-doc -p 6379:6379 redis:alpine

# Database 2: Document-to-User Permissions Mapping Node
docker run -d --name redis-doc-to-user -p 6380:6379 redis:alpine

```

### 2. Verify Database Connection Configs

Ensure your local config mappings point exactly to your environment target bounds.

* **Backend Matrix Config (`./server/config.json`):**

```json
{
  "services": {
    "databases-for-redis": [
      { "credentials": { "db_type": "redis", "uri": "redis://host.docker.internal:6379" } },
      { "credentials": { "db_type": "redis", "uri": "redis://host.docker.internal:6380" } }
    ]
  }
}

```

* **Frontend Route Map (`./src/secrets/config.json`):**

```json
{
  "iss": "http://localhost:8081",
  "blockchain_channel": "medrec-channel"
}

```

### 3. Clear macOS Quarantine Restrictions & Launch App Stack

Strip downloaded file security restrictions from the deployment script, assign full execution modes, and launch the docker platform orchestration script:

```bash
# Bypass gatekeeper quarantine attributes
xattr -d com.apple.quarantine run-application.sh

# Elevate script execution permissions
chmod +x run-application.sh

# Execute deployment automation pipeline
./run-application.sh

```

Once the compilation terminal logs settle and print `Application running...`, view your apps live in your web browser layout engine:

* **Interactive Client Web Interface Layout:** `http://localhost:8080`
* **API Gateway Microservice Node Server:** `http://localhost:8081`

---

## 🔐 Simulating Role Login Identity Tokens

Production deployments utilize secure signed web tokens to evaluate permissions. To bypass external identity authenticators while developing locally, execute this terminal command to output a mock cryptographic string payload:

```bash
node -e "const payload={sid:'sol-admin-cluster',uid:'admin-dev',oid:'org-master',name:'Solution Admin'}; const b=o=>Buffer.from(JSON.stringify(o)).toString('base64url'); console.log(b({alg:'none',typ:'JWT'})+'.'+b(payload)+'.signature')"

```

Copy the JWT-shaped output from your terminal and paste it into the **Solution Admin** login box token field at `http://localhost:8080` to authenticate and unlock permission workflows!

---

## 🛑 Safely Stop the Application

To drop the microservice bindings and turn off all background databases to clear system memory, run:

```bash
docker stop medrec-vue medrec-server redis-user-to-doc redis-doc-to-user

```

```

```
