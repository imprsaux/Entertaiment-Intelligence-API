# ⚠️ REPOSITORY-SPECIFIC INSTRUCTION
**This document contains the complete Africa Intelligence MVP for all 9 APIs.**
However, this repository is **ONLY** for:
---

## 🎯 THIS REPO: [Entertaiment-Intelligence-API
]

| Property | Value |
|----------|-------|
| **Repository** | `[FILL: api-name]-api` *(derived from API Name)* |
| **API Name** | [FILL: API Name] |
| **Port Block** | *(auto-derived from table below)* |
| **Dev Port** | *(auto-derived from table below)* |
| **Primary Endpoint** | *(auto-derived from table below)* |
| **Data Sources** | *(auto-derived from table below)* |

---

## 📌 INSTRUCTIONS FOR AI MODELS

**When reading this document, you MUST:**

1. **Look at the API Name** at the top of this document — this is the ONLY API you will build
2. **Find this API in the "API Master Table" below** to get: Port Block, Dev Port, Primary Endpoint, and Data Sources
3. **Ignore all other APIs** in the master table and in the full MVP document below
4. **Build only the endpoints** listed for this API in the master table
5. **Use the port** listed for this API in the master table

**If you are unsure about any instruction, prioritize this repo's API Name above all else.**

---

## 🔴 STOP — CONFIRM BEFORE PROCEEDING

Before implementing any code, confirm:

- [ ] I have read the API Name: **[FILL: API Name]**
- [ ] I have found this API in the Master Table below
- [ ] I will use the port listed in the Master Table
- [ ] I will build ONLY the endpoints listed for this API
- [ ] I will ignore all other APIs
---
## 📊 API MASTER TABLE (Auto-Reference)
| # | API Name | GitHub Repo | Port Block | Dev Port | Prod Port | Primary Endpoint | Data Sources |
|---|----------|-------------|------------|----------|-----------|------------------|--------------|
| 1 | Mobile Carrier Intelligence | `carrier-intel-api` | 7400-7499 | 7400 | 7401 | `/v1/carrier/lookup` | MNC/MCC databases, carrier APIs |
| 2 | Email Intelligence | `email-intel-api` | 7500-7599 | 7500 | 7501 | `/v1/email/validate` | Domain reputation, breach databases |
| 3 | Phone Number Risk | `phone-risk-api` | 7600-7699 | 7600 | 7601 | `/v1/phone/risk` | Phone databases, SIM swap registries |
| 4 | KYC Helper | `kyc-helper-api` | 7700-7799 | 7700 | 7701 | `/v1/kyc/verify` | National ID, sanctions lists |
| 5 | Fraud Velocity | `fraud-velocity-api` | 7800-7899 | 7800 | 7801 | `/v1/velocity/track` | In-memory/Redis event tracking |
| 6 | Streaming Geo-Restriction | `streaming-geo-api` | 7900-7999 | 7900 | 7901 | `/v1/streaming/geo` | MaxMind, VPN/proxy lists |
| 7 | Payment Fraud Helper | `payment-fraud-api` | 8000-8099 | 8000 | 8001 | `/v1/payment/check` | BIN databases, transaction history |
| 8 | SMS Delivery Intelligence | `sms-intel-api` | 8100-8199 | 8100 | 8101 | `/v1/sms/route` | Carrier databases, gateway logs |
| 9 | Device Fingerprint | `device-fingerprint-api` | 8200-8299 | 8200 | 8201 | `/v1/fingerprint/generate` | Browser signatures, device databases |
---
## 📋 FULL MVP DOCUMENTATION STARTS BELOW

(Sections below this line are the complete MVP document for reference)

---
[PASTE FULL MVP DOCUMENT HERE]

AFRICA INTELLIGENCE APIs — FINAL MVP DOCUMENT
Version: 2.0
Owner: Makinde.O
Market Focus: Nigeria + Emerging Markets + Global
Status: READY FOR IMPLEMENTATION

🤖 MODEL COLLABORATION & HANDOFF PROTOCOL
This MVP is to be implemented by multiple AI models working together, primarily:

DeepSeek Coder (DSC) — Implements code exactly as specified, writes Python scripts, FastAPI endpoints, tests, Dockerfiles, and infra configs. Follows instructions from V4P and does not change architecture on its own.

DeepSeek V4 Pro (V4P) — Designs architecture, data flows, risk-scoring logic, pipeline sequencing, and documentation. Reviews DSC's work and issues precise next steps.

DeepSeek V4 Flash (V4F) — Used mainly for fast autocomplete and small edits; does not own architecture.

Handoff Rules
When a model starts work, it must:

Read this MVP document.

Summarize in 3–5 bullet points what its current task is.

State which previous model it is continuing from (if any).

When a model finishes a task, it must:

Summarize what was done (files created/modified, scripts implemented, endpoints added).

List any TODOs or open questions.

Explicitly say which model should take over next and for what purpose.

Output a short "handoff block" that can be pasted into the next model's context.

Handoff Block Format
The model must output a block like:

text
[HANDOFF] From: DeepSeek Coder To: DeepSeek V4 Pro

Context:
- Implemented scripts: 01_prepare_env.py, 02_load_config.py, 03_fetch_data.py
- All scripts accept --context and --dry-run, update state/checkpoints.json, and print JSON to stdout.
- No risk-scoring logic implemented yet.

Next Tasks for V4P:
- Design detailed risk-scoring rules for 09_run_risk_scoring.py
- Define reason codes and scoring thresholds for each API's specific use case
- Create unified response schema across all 9 APIs
[/HANDOFF]
The next model must:

Read the [HANDOFF] block.

Confirm understanding.

Continue from there without redoing completed work.

The human operator may switch models at any time and will paste the latest [HANDOFF] block into the new model's context.

📋 PROBLEM STATEMENT
Nigeria and many emerging markets face high levels of online fraud, identity spoofing, account takeover attempts, SIM-swap fraud, and cross-border cybercrime. Banks, fintechs, telcos, and digital service providers require reliable, low-latency intelligence APIs to:

Detect suspicious logins and transactions

Identify impossible-travel events

Flag high-risk entities (IPs, emails, phones, devices)

Enforce geo-based compliance rules

Improve fraud scoring models

Support investigations

Market Gap: Existing global intelligence APIs often fail in African markets due to:

Poor carrier/ISP coverage

Inaccurate ASN mapping

Outdated phone/email databases

Slow latency from non-regional servers

Lack of fraud-specific intelligence

There is a clear opportunity to build a region-optimized, fraud-aware, intelligence API suite for the African market.

🎯 TARGET USERS
Primary:

Banks and fintechs

Payment processors

Digital lending platforms

Fraud detection teams

Cybersecurity SOC teams

SRE and NOC teams

Identity verification platforms

Secondary:

E-commerce platforms

Ride-hailing and logistics apps

Government digital services

Law enforcement (with proper legal process)

Telecom operators

Global companies needing accurate African intelligence

🏗️ CORE MVP FEATURES (9 APIs)
#	API	Core Endpoints	Key Features
1	Mobile Carrier Intelligence	/v1/carrier/lookup, /v1/carrier/batch	Carrier detection (MTN, Airtel, Vodafone), network type (2G-5G), roaming status
2	Email Intelligence	/v1/email/validate, /v1/email/batch	Format validation, domain reputation, disposable detection, breach detection
3	Phone Number Risk	/v1/phone/risk, /v1/phone/batch	Format validation, country detection, SIM swap history, ported status
4	KYC Helper	/v1/kyc/verify, /v1/kyc/document	Identity verification, document validation, sanctions/PEP screening
5	Fraud Velocity	/v1/velocity/track, /v1/velocity/check	Event frequency tracking, rate anomaly detection, configurable time windows
6	Streaming Geo-Restriction	/v1/streaming/geo, /v1/streaming/batch	IP geolocation, VPN/proxy detection, streaming service compatibility
7	Payment Fraud Helper	/v1/payment/check, /v1/payment/bin	Payment velocity, geo-mismatch, device mismatch, BIN analysis
8	SMS Delivery Intelligence	/v1/sms/route, /v1/sms/predict	Carrier detection, route optimization, delivery prediction, cost estimation
9	Device Fingerprint	/v1/fingerprint/generate, /v1/fingerprint/check	Browser fingerprinting, device detection, bot detection, session consistency
🔧 TECHNICAL ARCHITECTURE (Universal Template)
Data Sources
MaxMind GeoLite2 / commercial GeoIP2 databases

AFRINIC delegated-stats (ASN → country)

Public threat feeds (TOR exit nodes, known bad IPs)

Carrier MNC/MCC databases (for carrier intelligence)

Email domain reputation databases

Phone number databases (SIM swap, porting registries)

BIN databases (for payment fraud)

Device fingerprint databases

Core Components
1. Offline Data Pipeline — 14 modular Python scripts (see Appendix A)

Refresh data sources (GeoDB, ASN, threat feeds, carrier DBs, etc.)

Build indices (JSON / SQLite / Redis)

Enrich sample/batch queries with intelligence

Publish versioned artifacts

Health gates, validation, tests, recovery

2. API Service — FastAPI (Python 3.11+)

Synchronous endpoints per API

In-memory lookups from pre-built indices

Unified error handling and response format

3. Caching Layer — Redis (optional for MVP, can be skipped with direct file reads)

4. Observability — Prometheus + Grafana (metrics), Uvicorn access logs

5. Security — API key authentication (planned post-MVP; MVP uses no auth or simple static key)

Performance Targets
p95 latency < 150 ms (including disk lookup)

99.9% uptime for the API service

Pipeline scalability: 10k requests/sec (horizontal scaling via multiple API replicas)

🌍 MARKET FIT — NIGERIA & EMERGING MARKETS
Nigeria is an ideal initial market due to:

High fintech adoption

High fraud pressure

Mobile-first traffic

Dynamic IP pools

Frequent VPN usage

SIM-swap challenges

Key Nigerian use cases:

Detect login attempts from unexpected regions

Flag IPs from known fraud hotspots

Identify VPN/proxy usage during onboarding

Validate that a user's IPAFRICA INTELLIGENCE APIs — FINAL MVP DOCUMENT
Version: 2.0
Owner: Makinde.O
Market Focus: Nigeria + Emerging Markets + Global
Status: READY FOR IMPLEMENTATION

🤖 MODEL COLLABORATION & HANDOFF PROTOCOL
This MVP is to be implemented by multiple AI models working together, primarily:

DeepSeek Coder (DSC) — Implements code exactly as specified, writes Python scripts, FastAPI endpoints, tests, Dockerfiles, and infra configs. Follows instructions from V4P and does not change architecture on its own.

DeepSeek V4 Pro (V4P) — Designs architecture, data flows, risk-scoring logic, pipeline sequencing, and documentation. Reviews DSC's work and issues precise next steps.

DeepSeek V4 Flash (V4F) — Used mainly for fast autocomplete and small edits; does not own architecture.

Handoff Rules
When a model starts work, it must:

Read this MVP document.

Summarize in 3–5 bullet points what its current task is.

State which previous model it is continuing from (if any).

When a model finishes a task, it must:

Summarize what was done (files created/modified, scripts implemented, endpoints added).

List any TODOs or open questions.

Explicitly say which model should take over next and for what purpose.

Output a short "handoff block" that can be pasted into the next model's context.

Handoff Block Format
The model must output a block like:

text
[HANDOFF] From: DeepSeek Coder To: DeepSeek V4 Pro

Context:
- Implemented scripts: 01_prepare_env.py, 02_load_config.py, 03_fetch_data.py
- All scripts accept --context and --dry-run, update state/checkpoints.json, and print JSON to stdout.
- No risk-scoring logic implemented yet.

Next Tasks for V4P:
- Design detailed risk-scoring rules for 09_run_risk_scoring.py
- Define reason codes and scoring thresholds for each API's specific use case
- Create unified response schema across all 9 APIs
[/HANDOFF]
The next model must:

Read the [HANDOFF] block.

Confirm understanding.

Continue from there without redoing completed work.

The human operator may switch models at any time and will paste the latest [HANDOFF] block into the new model's context.

📋 PROBLEM STATEMENT
Nigeria and many emerging markets face high levels of online fraud, identity spoofing, account takeover attempts, SIM-swap fraud, and cross-border cybercrime. Banks, fintechs, telcos, and digital service providers require reliable, low-latency intelligence APIs to:

Detect suspicious logins and transactions

Identify impossible-travel events

Flag high-risk entities (IPs, emails, phones, devices)

Enforce geo-based compliance rules

Improve fraud scoring models

Support investigations

Market Gap: Existing global intelligence APIs often fail in African markets due to:

Poor carrier/ISP coverage

Inaccurate ASN mapping

Outdated phone/email databases

Slow latency from non-regional servers

Lack of fraud-specific intelligence

There is a clear opportunity to build a region-optimized, fraud-aware, intelligence API suite for the African market.

🎯 TARGET USERS
Primary:

Banks and fintechs

Payment processors

Digital lending platforms

Fraud detection teams

Cybersecurity SOC teams

SRE and NOC teams

Identity verification platforms

Secondary:

E-commerce platforms

Ride-hailing and logistics apps

Government digital services

Law enforcement (with proper legal process)

Telecom operators

Global companies needing accurate African intelligence

🏗️ CORE MVP FEATURES (9 APIs)
#	API	Core Endpoints	Key Features
1	Mobile Carrier Intelligence	/v1/carrier/lookup, /v1/carrier/batch	Carrier detection (MTN, Airtel, Vodafone), network type (2G-5G), roaming status
2	Email Intelligence	/v1/email/validate, /v1/email/batch	Format validation, domain reputation, disposable detection, breach detection
3	Phone Number Risk	/v1/phone/risk, /v1/phone/batch	Format validation, country detection, SIM swap history, ported status
4	KYC Helper	/v1/kyc/verify, /v1/kyc/document	Identity verification, document validation, sanctions/PEP screening
5	Fraud Velocity	/v1/velocity/track, /v1/velocity/check	Event frequency tracking, rate anomaly detection, configurable time windows
6	Streaming Geo-Restriction	/v1/streaming/geo, /v1/streaming/batch	IP geolocation, VPN/proxy detection, streaming service compatibility
7	Payment Fraud Helper	/v1/payment/check, /v1/payment/bin	Payment velocity, geo-mismatch, device mismatch, BIN analysis
8	SMS Delivery Intelligence	/v1/sms/route, /v1/sms/predict	Carrier detection, route optimization, delivery prediction, cost estimation
9	Device Fingerprint	/v1/fingerprint/generate, /v1/fingerprint/check	Browser fingerprinting, device detection, bot detection, session consistency
🔧 TECHNICAL ARCHITECTURE (Universal Template)
Data Sources
MaxMind GeoLite2 / commercial GeoIP2 databases

AFRINIC delegated-stats (ASN → country)

Public threat feeds (TOR exit nodes, known bad IPs)

Carrier MNC/MCC databases (for carrier intelligence)

Email domain reputation databases

Phone number databases (SIM swap, porting registries)

BIN databases (for payment fraud)

Device fingerprint databases

Core Components
1. Offline Data Pipeline — 14 modular Python scripts (see Appendix A)

Refresh data sources (GeoDB, ASN, threat feeds, carrier DBs, etc.)

Build indices (JSON / SQLite / Redis)

Enrich sample/batch queries with intelligence

Publish versioned artifacts

Health gates, validation, tests, recovery

2. API Service — FastAPI (Python 3.11+)

Synchronous endpoints per API

In-memory lookups from pre-built indices

Unified error handling and response format

3. Caching Layer — Redis (optional for MVP, can be skipped with direct file reads)

4. Observability — Prometheus + Grafana (metrics), Uvicorn access logs

5. Security — API key authentication (planned post-MVP; MVP uses no auth or simple static key)

Performance Targets
p95 latency < 150 ms (including disk lookup)

99.9% uptime for the API service

Pipeline scalability: 10k requests/sec (horizontal scaling via multiple API replicas)

🌍 MARKET FIT — NIGERIA & EMERGING MARKETS
Nigeria is an ideal initial market due to:

High fintech adoption

High fraud pressure

Mobile-first traffic

Dynamic IP pools

Frequent VPN usage

SIM-swap challenges

Key Nigerian use cases:

Detect login attempts from unexpected regions

Flag IPs from known fraud hotspots

Identify VPN/proxy usage during onboarding

Validate that a user's IP/phone matches their claimed carrier

Support AML/CFT compliance checks

Assist SOC teams in incident investigations

Other similar markets: Kenya, Ghana, South Africa, India, Brazil, Indonesia, Philippines.

💰 VALUE PROPOSITION
For Banks & Fintechs:

Reduce fraud losses

Improve KYC/AML checks

Strengthen login security

Enhance risk scoring models

For Telcos:

Optimize SMS delivery

Detect SIM-swap fraud

Improve network intelligence

For Streaming Services:

Enforce geo-restrictions

Detect VPN/proxy violations

Improve content delivery

📁 GITHUB REPOSITORY NAMING CONVENTION
All repositories follow this naming pattern:

text
{api-name}-api
#	API	GitHub Repo Name	Port Block
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499
2	Email Intelligence	email-intel-api	7500-7599
3	Phone Number Risk	phone-risk-api	7600-7699
4	KYC Helper	kyc-helper-api	7700-7799
5	Fraud Velocity	fraud-velocity-api	7800-7899
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999
7	Payment Fraud Helper	payment-fraud-api	8000-8099
8	SMS Delivery Intelligence	sms-intel-api	8100-8199
9	Device Fingerprint	device-fingerprint-api	8200-8299
Environment Variables per Repo
Each repo will have a .env file with:

bash
# API Configuration
API_NAME={api-name}
API_VERSION=v1
PORT={dev_port}

# Database Paths
DATA_DIR=./data
ARTIFACTS_DIR=./artifacts
STATE_DIR=./state

# Logging
LOG_LEVEL=INFO
LOG_FILE=./logs/api.log

# Security (post-MVP)
API_KEY_REQUIRED=false
RATE_LIMIT_ENABLED=false

# Pipeline
PIPELINE_LOCK_FILE=./state/pipeline.lock
CHECKPOINT_FILE=./state/checkpoints.json
CONTEXT_FILE=./state/context.json
AUDIT_LOG=./state/audit.log
🔨 IMPLEMENTATION WORKFLOW — PER API
Step 1: Create GitHub Repository
Action: Human operator creates repository on GitHub

bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api (e.g., carrier-intel-api)
# 3. Description: "Mobile Carrier Intelligence API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Step 2: Clone Repository to Hostnode
Action: Human operator clones the repo to the hostnode (AS-1015A-MT server)

bash
# On hostnode (Ubuntu 24.04)
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Step 3: Scaffold Directory Structure
Action: Run the universal directory creation script

bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Step 4: Copy Universal Files
Action: Copy files from reference repository (gin)

bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Step 5: Customize API-Specific Files
Action: Edit files for this specific API

bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set:
#   REPO_NAME: {api-name}-api
#   PORT_BLOCK: {port_block}
#   PRIMARY_APP: {api-name}

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set:
#   REPO_NAME={api-name}-api
#   REPO_ALLOW_PORTS={ports}

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set:
#   app title: "{API Name} API"
#   app description: "..."
#   import routers from v1

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.py
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set:
#   API_NAME={api-name}
#   PORT={dev_port}
Step 6: Implement Automation Pipeline
Action: Build the 14 automation scripts

bash
# For each script, implement based on API-specific data sources
# Scripts:
# 01_prepare_env.py - Set up environment
# 02_load_config.py - Load configuration
# 03_fetch_data.py - Fetch raw data
# 04_parse_data.py - Parse data
# 05_enrich_data.py - Enrich with intelligence
# 06_validate_data.py - Validate data
# 07_build_index.py - Build JSON index
# 08_test_index.py - Test index
# 09_run_risk_scoring.py - Apply risk scoring
# 10_publish_outputs.py - Publish artifacts
# 11_health_gate.py - Health checks
# 12_verify_validate.py - Verification
# 13_test_suite.py - Run tests
# 14_recovery_reset.py - Recovery
# driver.py - Orchestrator
Step 7: Test Locally
Action: Run pipeline and start API

bash
# Create Python virtual environment
python3.11 -m venv env
source env/bin/activate
pip install -r requirements.txt

# Run pipeline
python automation/driver.py --dry-run
python automation/driver.py

# Start API
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}

# Test endpoints
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Step 8: Push to GitHub
Action: Commit and push to sync with GitHub

bash
# Stage all files
git add .

# Commit with message
git commit -m "Initial scaffold for {api-name}-api

- Directory structure created
- Universal files copied from gin
- Customized AGENT_MANIFEST.md
- Customized firewall config
- Created API models and endpoints
- Implemented automation pipeline
"

# Push to GitHub
git push origin main
Step 9: Verify Sync
Action: Confirm files are on GitHub

bash
# Check GitHub repository
# Navigate to https://github.com/your-org/{api-name}-api
# Verify all files are present
Step 10: Clean Cache and Proceed to Next API
Action: Prepare for next API implementation

bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"
# Or: rm -rf ~/.config/Code/CachedData/*

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Navigate to parent directory
cd ~/projects/

# Proceed to next API (repeat from Step 1)
📋 STEP-BY-STEP CHECKLIST FOR EACH API
For each API, complete this checklist:

Pre-Implementation (Human Operator)
Create GitHub repository {api-name}-api

Clone to hostnode ~/projects/{api-name}-api

Note port block from allocation table

Set environment variables in .env

Implementation (DeepSeek Coder)
Scaffold directory structure (Step 3)

Copy universal files (Step 4)

Customize API-specific files (Step 5)

AGENT_MANIFEST.md

peer_allow_profile.conf

apply-rules.sh

api/main.py

api/models/request.py

api/models/response.py

api/v1/lookup.py

api/v1/batch.py

.env

Data Pipeline (DeepSeek Coder)
Implement 14 automation scripts

01_prepare_env.py

02_load_config.py

03_fetch_data.py

04_parse_data.py

05_enrich_data.py

06_validate_data.py

07_build_index.py

08_test_index.py

09_run_risk_scoring.py

10_publish_outputs.py

11_health_gate.py

12_verify_validate.py

13_test_suite.py

14_recovery_reset.py

driver.py

Testing (DeepSeek Coder)
Run pipeline python automation/driver.py

Start API uvicorn api.main:app

Test endpoints curl

Run test suite python -m pytest tests/

Deployment (Human Operator)
Commit changes git add . && git commit -m "..." && git push

Verify GitHub sync (check repository online)

Clean caches (Continue, VS Code)

Proceed to next API

📊 PORT BLOCK ALLOCATION (Bulletin 001)
#	API	GitHub Repo	Block	Dev Port	Prod Port
0	IP Risk API	ip-risk-api	7200-7299	7200	7201
0	Gin (Reference)	gin	7300-7399	7300	7301
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499	7400	7401
2	Email Intelligence	email-intel-api	7500-7599	7500	7501
3	Phone Number Risk	phone-risk-api	7600-7699	7600	7601
4	KYC Helper	kyc-helper-api	7700-7799	7700	7701
5	Fraud Velocity	fraud-velocity-api	7800-7899	7800	7801
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999	7900	7901
7	Payment Fraud Helper	payment-fraud-api	8000-8099	8000	8001
8	SMS Delivery Intelligence	sms-intel-api	8100-8199	8100	8101
9	Device Fingerprint	device-fingerprint-api	8200-8299	8200	8201
Shared Ports: 9090 (Prometheus), 3000 (Grafana)

🔌 API ENDPOINTS (MVP)
Unified Response Format
All APIs share a common response structure:

json
{
  "success": true,
  "data": {
    // API-specific data
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z",
    "version": "v1",
    "api": "api-name"
  }
}
Error Response Format
json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z"
  }
}
API-Specific Endpoints
#	API	Method	Path	Description
1	Carrier	GET	/v1/carrier/lookup?phone={phone}	Lookup carrier by phone number
1	Carrier	POST	/v1/carrier/batch	Batch carrier lookup
2	Email	GET	/v1/email/validate?email={email}	Validate and analyze email
2	Email	POST	/v1/email/batch	Batch email validation
3	Phone Risk	GET	/v1/phone/risk?phone={phone}	Assess phone number risk
3	Phone Risk	POST	/v1/phone/batch	Batch phone risk assessment
4	KYC	POST	/v1/kyc/verify	Verify identity
4	KYC	POST	/v1/kyc/document	Validate document
5	Velocity	POST	/v1/velocity/track	Track an event
5	Velocity	GET	/v1/velocity/check?entity={id}	Check velocity
6	Streaming	GET	/v1/streaming/geo?ip={ip}	Geo-restriction lookup
6	Streaming	POST	/v1/streaming/batch	Batch geo-restriction lookup
7	Payment	POST	/v1/payment/check	Check payment fraud
7	Payment	GET	/v1/payment/bin/{bin}	BIN lookup
8	SMS	GET	/v1/sms/route?phone={phone}	Best SMS route
8	SMS	POST	/v1/sms/predict	Delivery prediction
9	Device	POST	/v1/fingerprint/generate	Generate device fingerprint
9	Device	GET	/v1/fingerprint/check/{id}	Check fingerprint
All	All	GET	/v1/health	Service health status
🏗️ OFFLINE PIPELINE — 14 SCRIPTS (DeepSeek Coder Ready)
All scripts live in automation/. A driver.py orchestrates them, passing a shared context.json. Each script supports --dry-run and --resume. A lock file prevents concurrent runs. Checkpoints are saved in state/checkpoints.json.

Script List (14)
#	Script	Purpose
1	01_prepare_env.py	Set up environment, verify dependencies
2	02_load_config.py	Load configuration from env/config files
3	03_fetch_data.py	Fetch/refresh raw data from sources
4	04_parse_data.py	Parse raw data into structured format
5	05_enrich_data.py	Enrich with additional intelligence
6	06_validate_data.py	Validate data quality and completeness
7	07_build_index.py	Build JSON indices from processed data
8	08_test_index.py	Test index performance and accuracy
9	09_run_risk_scoring.py	Apply risk scoring to data
10	10_publish_outputs.py	Publish versioned artifacts
11	11_health_gate.py	Check health gates for deployment
12	12_verify_validate.py	Verify data meets requirements
13	13_test_suite.py	Run comprehensive test suite
14	14_recovery_reset.py	Reset state for recovery
Script Contract
Each script must:

Accept --context (path to context.json) and --dry-run flags

Update state/checkpoints.json with completion status

Print JSON output to stdout (status, metrics, errors)

Handle errors gracefully and exit with appropriate code

🔨 BUILD RUNBOOK (MVP → DEV BUILD)
Environment
OS: Ubuntu 24.04

Python: 3.11+

Tools: git, docker (optional), systemd (for production)

Phase 0 – Prerequisites
bash
sudo apt update && sudo apt install -y python3.11 python3.11-venv git wget
mkdir -p ~/projects/ && cd ~/projects/
Phase 1 – Create GitHub Repository
bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api
# 3. Description: "{API Name} API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Phase 2 – Clone to Hostnode
bash
# On hostnode
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Phase 3 – Scaffold Directory Structure
bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Phase 4 – Copy Universal Files
bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Phase 5 – Customize API-Specific Files
bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set: REPO_NAME, PORT_BLOCK, PRIMARY_APP

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set: REPO_NAME, REPO_ALLOW_PORTS

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set: port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set: app title, description, import routers

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.pyAFRICA INTELLIGENCE APIs — FINAL MVP DOCUMENT
Version: 2.0
Owner: Makinde.O
Market Focus: Nigeria + Emerging Markets + Global
Status: READY FOR IMPLEMENTATION

🤖 MODEL COLLABORATION & HANDOFF PROTOCOL
This MVP is to be implemented by multiple AI models working together, primarily:

DeepSeek Coder (DSC) — Implements code exactly as specified, writes Python scripts, FastAPI endpoints, tests, Dockerfiles, and infra configs. Follows instructions from V4P and does not change architecture on its own.

DeepSeek V4 Pro (V4P) — Designs architecture, data flows, risk-scoring logic, pipeline sequencing, and documentation. Reviews DSC's work and issues precise next steps.

DeepSeek V4 Flash (V4F) — Used mainly for fast autocomplete and small edits; does not own architecture.

Handoff Rules
When a model starts work, it must:

Read this MVP document.

Summarize in 3–5 bullet points what its current task is.

State which previous model it is continuing from (if any).

When a model finishes a task, it must:

Summarize what was done (files created/modified, scripts implemented, endpoints added).

List any TODOs or open questions.

Explicitly say which model should take over next and for what purpose.

Output a short "handoff block" that can be pasted into the next model's context.

Handoff Block Format
The model must output a block like:

text
[HANDOFF] From: DeepSeek Coder To: DeepSeek V4 Pro

Context:
- Implemented scripts: 01_prepare_env.py, 02_load_config.py, 03_fetch_data.py
- All scripts accept --context and --dry-run, update state/checkpoints.json, and print JSON to stdout.
- No risk-scoring logic implemented yet.

Next Tasks for V4P:
- Design detailed risk-scoring rules for 09_run_risk_scoring.py
- Define reason codes and scoring thresholds for each API's specific use case
- Create unified response schema across all 9 APIs
[/HANDOFF]
The next model must:

Read the [HANDOFF] block.

Confirm understanding.

Continue from there without redoing completed work.

The human operator may switch models at any time and will paste the latest [HANDOFF] block into the new model's context.

📋 PROBLEM STATEMENT
Nigeria and many emerging markets face high levels of online fraud, identity spoofing, account takeover attempts, SIM-swap fraud, and cross-border cybercrime. Banks, fintechs, telcos, and digital service providers require reliable, low-latency intelligence APIs to:

Detect suspicious logins and transactions

Identify impossible-travel events

Flag high-risk entities (IPs, emails, phones, devices)

Enforce geo-based compliance rules

Improve fraud scoring models

Support investigations

Market Gap: Existing global intelligence APIs often fail in African markets due to:

Poor carrier/ISP coverage

Inaccurate ASN mapping

Outdated phone/email databases

Slow latency from non-regional servers

Lack of fraud-specific intelligence

There is a clear opportunity to build a region-optimized, fraud-aware, intelligence API suite for the African market.

🎯 TARGET USERS
Primary:

Banks and fintechs

Payment processors

Digital lending platforms

Fraud detection teams

Cybersecurity SOC teams

SRE and NOC teams

Identity verification platforms

Secondary:

E-commerce platforms

Ride-hailing and logistics apps

Government digital services

Law enforcement (with proper legal process)

Telecom operators

Global companies needing accurate African intelligence

🏗️ CORE MVP FEATURES (9 APIs)
#	API	Core Endpoints	Key Features
1	Mobile Carrier Intelligence	/v1/carrier/lookup, /v1/carrier/batch	Carrier detection (MTN, Airtel, Vodafone), network type (2G-5G), roaming status
2	Email Intelligence	/v1/email/validate, /v1/email/batch	Format validation, domain reputation, disposable detection, breach detection
3	Phone Number Risk	/v1/phone/risk, /v1/phone/batch	Format validation, country detection, SIM swap history, ported status
4	KYC Helper	/v1/kyc/verify, /v1/kyc/document	Identity verification, document validation, sanctions/PEP screening
5	Fraud Velocity	/v1/velocity/track, /v1/velocity/check	Event frequency tracking, rate anomaly detection, configurable time windows
6	Streaming Geo-Restriction	/v1/streaming/geo, /v1/streaming/batch	IP geolocation, VPN/proxy detection, streaming service compatibility
7	Payment Fraud Helper	/v1/payment/check, /v1/payment/bin	Payment velocity, geo-mismatch, device mismatch, BIN analysis
8	SMS Delivery Intelligence	/v1/sms/route, /v1/sms/predict	Carrier detection, route optimization, delivery prediction, cost estimation
9	Device Fingerprint	/v1/fingerprint/generate, /v1/fingerprint/check	Browser fingerprinting, device detection, bot detection, session consistency
🔧 TECHNICAL ARCHITECTURE (Universal Template)
Data Sources
MaxMind GeoLite2 / commercial GeoIP2 databases

AFRINIC delegated-stats (ASN → country)

Public threat feeds (TOR exit nodes, known bad IPs)

Carrier MNC/MCC databases (for carrier intelligence)

Email domain reputation databases

Phone number databases (SIM swap, porting registries)

BIN databases (for payment fraud)

Device fingerprint databases

Core Components
1. Offline Data Pipeline — 14 modular Python scripts (see Appendix A)

Refresh data sources (GeoDB, ASN, threat feeds, carrier DBs, etc.)

Build indices (JSON / SQLite / Redis)

Enrich sample/batch queries with intelligence

Publish versioned artifacts

Health gates, validation, tests, recovery

2. API Service — FastAPI (Python 3.11+)

Synchronous endpoints per API

In-memory lookups from pre-built indices

Unified error handling and response format

3. Caching Layer — Redis (optional for MVP, can be skipped with direct file reads)

4. Observability — Prometheus + Grafana (metrics), Uvicorn access logs

5. Security — API key authentication (planned post-MVP; MVP uses no auth or simple static key)

Performance Targets
p95 latency < 150 ms (including disk lookup)

99.9% uptime for the API service

Pipeline scalability: 10k requests/sec (horizontal scaling via multiple API replicas)

🌍 MARKET FIT — NIGERIA & EMERGING MARKETS
Nigeria is an ideal initial market due to:

High fintech adoption

High fraud pressure

Mobile-first traffic

Dynamic IP pools

Frequent VPN usage

SIM-swap challenges

Key Nigerian use cases:

Detect login attempts from unexpected regions

Flag IPs from known fraud hotspots

Identify VPN/proxy usage during onboarding

Validate that a user's IP/phone matches their claimed carrier

Support AML/CFT compliance checks

Assist SOC teams in incident investigations

Other similar markets: Kenya, Ghana, South Africa, India, Brazil, Indonesia, Philippines.

💰 VALUE PROPOSITION
For Banks & Fintechs:

Reduce fraud losses

Improve KYC/AML checks

Strengthen login security

Enhance risk scoring models

For Telcos:

Optimize SMS delivery

Detect SIM-swap fraud

Improve network intelligence

For Streaming Services:

Enforce geo-restrictions

Detect VPN/proxy violations

Improve content delivery

📁 GITHUB REPOSITORY NAMING CONVENTION
All repositories follow this naming pattern:

text
{api-name}-api
#	API	GitHub Repo Name	Port Block
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499
2	Email Intelligence	email-intel-api	7500-7599
3	Phone Number Risk	phone-risk-api	7600-7699
4	KYC Helper	kyc-helper-api	7700-7799
5	Fraud Velocity	fraud-velocity-api	7800-7899
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999
7	Payment Fraud Helper	payment-fraud-api	8000-8099
8	SMS Delivery Intelligence	sms-intel-api	8100-8199
9	Device Fingerprint	device-fingerprint-api	8200-8299
Environment Variables per Repo
Each repo will have a .env file with:

bash
# API Configuration
API_NAME={api-name}
API_VERSION=v1
PORT={dev_port}

# Database Paths
DATA_DIR=./data
ARTIFACTS_DIR=./artifacts
STATE_DIR=./state

# Logging
LOG_LEVEL=INFO
LOG_FILE=./logs/api.log

# Security (post-MVP)
API_KEY_REQUIRED=false
RATE_LIMIT_ENABLED=false

# Pipeline
PIPELINE_LOCK_FILE=./state/pipeline.lock
CHECKPOINT_FILE=./state/checkpoints.json
CONTEXT_FILE=./state/context.json
AUDIT_LOG=./state/audit.log
🔨 IMPLEMENTATION WORKFLOW — PER API
Step 1: Create GitHub Repository
Action: Human operator creates repository on GitHub

bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api (e.g., carrier-intel-api)
# 3. Description: "Mobile Carrier Intelligence API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Step 2: Clone Repository to Hostnode
Action: Human operator clones the repo to the hostnode (AS-1015A-MT server)

bash
# On hostnode (Ubuntu 24.04)
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Step 3: Scaffold Directory Structure
Action: Run the universal directory creation script

bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Step 4: Copy Universal Files
Action: Copy files from reference repository (gin)

bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Step 5: Customize API-Specific Files
Action: Edit files for this specific API

bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set:
#   REPO_NAME: {api-name}-api
#   PORT_BLOCK: {port_block}
#   PRIMARY_APP: {api-name}

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set:
#   REPO_NAME={api-name}-api
#   REPO_ALLOW_PORTS={ports}

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set:
#   app title: "{API Name} API"
#   app description: "..."
#   import routers from v1

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.py
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set:
#   API_NAME={api-name}
#   PORT={dev_port}
Step 6: Implement Automation Pipeline
Action: Build the 14 automation scripts

bash
# For each script, implement based on API-specific data sources
# Scripts:
# 01_prepare_env.py - Set up environment
# 02_load_config.py - Load configuration
# 03_fetch_data.py - Fetch raw data
# 04_parse_data.py - Parse data
# 05_enrich_data.py - Enrich with intelligence
# 06_validate_data.py - Validate data
# 07_build_index.py - Build JSON index
# 08_test_index.py - Test index
# 09_run_risk_scoring.py - Apply risk scoring
# 10_publish_outputs.py - Publish artifacts
# 11_health_gate.py - Health checks
# 12_verify_validate.py - Verification
# 13_test_suite.py - Run tests
# 14_recovery_reset.py - Recovery
# driver.py - Orchestrator
Step 7: Test Locally
Action: Run pipeline and start API

bash
# Create Python virtual environment
python3.11 -m venv env
source env/bin/activate
pip install -r requirements.txt

# Run pipeline
python automation/driver.py --dry-run
python automation/driver.py

# Start API
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}

# Test endpoints
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Step 8: Push to GitHub
Action: Commit and push to sync with GitHub

bash
# Stage all files
git add .

# Commit with message
git commit -m "Initial scaffold for {api-name}-api

- Directory structure created
- Universal files copied from gin
- Customized AGENT_MANIFEST.md
- Customized firewall config
- Created API models and endpoints
- Implemented automation pipeline
"

# Push to GitHub
git push origin main
Step 9: Verify Sync
Action: Confirm files are on GitHub

bash
# Check GitHub repository
# Navigate to https://github.com/your-org/{api-name}-api
# Verify all files are present
Step 10: Clean Cache and Proceed to Next API
Action: Prepare for next API implementation

bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"
# Or: rm -rf ~/.config/Code/CachedData/*

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Navigate to parent directory
cd ~/projects/

# Proceed to next API (repeat from Step 1)
📋 STEP-BY-STEP CHECKLIST FOR EACH API
For each API, complete this checklist:

Pre-Implementation (Human Operator)
Create GitHub repository {api-name}-api

Clone to hostnode ~/projects/{api-name}-api

Note port block from allocation table

Set environment variables in .env

Implementation (DeepSeek Coder)
Scaffold directory structure (Step 3)

Copy universal files (Step 4)

Customize API-specific files (Step 5)

AGENT_MANIFEST.md

peer_allow_profile.conf

apply-rules.sh

api/main.py

api/models/request.py

api/models/response.py

api/v1/lookup.py

api/v1/batch.py

.env

Data Pipeline (DeepSeek Coder)
Implement 14 automation scripts

01_prepare_env.py

02_load_config.py

03_fetch_data.py

04_parse_data.py

05_enrich_data.py

06_validate_data.py

07_build_index.py

08_test_index.py

09_run_risk_scoring.py

10_publish_outputs.py

11_health_gate.py

12_verify_validate.py

13_test_suite.py

14_recovery_reset.py

driver.py

Testing (DeepSeek Coder)
Run pipeline python automation/driver.py

Start API uvicorn api.main:app

Test endpoints curl

Run test suite python -m pytest tests/

Deployment (Human Operator)
Commit changes git add . && git commit -m "..." && git push

Verify GitHub sync (check repository online)

Clean caches (Continue, VS Code)

Proceed to next API

📊 PORT BLOCK ALLOCATION (Bulletin 001)
#	API	GitHub Repo	Block	Dev Port	Prod Port
0	IP Risk API	ip-risk-api	7200-7299	7200	7201
0	Gin (Reference)	gin	7300-7399	7300	7301
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499	7400	7401
2	Email Intelligence	email-intel-api	7500-7599	7500	7501
3	Phone Number Risk	phone-risk-api	7600-7699	7600	7601
4	KYC Helper	kyc-helper-api	7700-7799	7700	7701
5	Fraud Velocity	fraud-velocity-api	7800-7899	7800	7801
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999	7900	7901
7	Payment Fraud Helper	payment-fraud-api	8000-8099	8000	8001
8	SMS Delivery Intelligence	sms-intel-api	8100-8199	8100	8101
9	Device Fingerprint	device-fingerprint-api	8200-8299	8200	8201
Shared Ports: 9090 (Prometheus), 3000 (Grafana)

🔌 API ENDPOINTS (MVP)
Unified Response Format
All APIs share a common response structure:

json
{
  "success": true,
  "data": {
    // API-specific data
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z",
    "version": "v1",
    "api": "api-name"
  }
}
Error Response Format
json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z"
  }
}
API-Specific Endpoints
#	API	Method	Path	Description
1	Carrier	GET	/v1/carrier/lookup?phone={phone}	Lookup carrier by phone number
1	Carrier	POST	/v1/carrier/batch	Batch carrier lookup
2	Email	GET	/v1/email/validate?email={email}	Validate and analyze email
2	Email	POST	/v1/email/batch	Batch email validation
3	Phone Risk	GET	/v1/phone/risk?phone={phone}	Assess phone number risk
3	Phone Risk	POST	/v1/phone/batch	Batch phone risk assessment
4	KYC	POST	/v1/kyc/verify	Verify identity
4	KYC	POST	/v1/kyc/document	Validate document
5	Velocity	POST	/v1/velocity/track	Track an event
5	Velocity	GET	/v1/velocity/check?entity={id}	Check velocity
6	Streaming	GET	/v1/streaming/geo?ip={ip}	Geo-restriction lookup
6	Streaming	POST	/v1/streaming/batch	Batch geo-restriction lookup
7	Payment	POST	/v1/payment/check	Check payment fraud
7	Payment	GET	/v1/payment/bin/{bin}	BIN lookup
8	SMS	GET	/v1/sms/route?phone={phone}	Best SMS route
8	SMS	POST	/v1/sms/predict	Delivery prediction
9	Device	POST	/v1/fingerprint/generate	Generate device fingerprint
9	Device	GET	/v1/fingerprint/check/{id}	Check fingerprint
All	All	GET	/v1/health	Service health status
🏗️ OFFLINE PIPELINE — 14 SCRIPTS (DeepSeek Coder Ready)
All scripts live in automation/. A driver.py orchestrates them, passing a shared context.json. Each script supports --dry-run and --resume. A lock file prevents concurrent runs. Checkpoints are saved in state/checkpoints.json.

Script List (14)
#	Script	Purpose
1	01_prepare_env.py	Set up environment, verify dependencies
2	02_load_config.py	Load configuration from env/config files
3	03_fetch_data.py	Fetch/refresh raw data from sources
4	04_parse_data.py	Parse raw data into structured format
5	05_enrich_data.py	Enrich with additional intelligence
6	06_validate_data.py	Validate data quality and completeness
7	07_build_index.py	Build JSON indices from processed data
8	08_test_index.py	Test index performance and accuracy
9	09_run_risk_scoring.py	Apply risk scoring to data
10	10_publish_outputs.py	Publish versioned artifacts
11	11_health_gate.py	Check health gates for deployment
12	12_verify_validate.py	Verify data meets requirements
13	13_test_suite.py	Run comprehensive test suite
14	14_recovery_reset.py	Reset state for recovery
Script Contract
Each script must:

Accept --context (path to context.json) and --dry-run flags

Update state/checkpoints.json with completion status

Print JSON output to stdout (status, metrics, errors)

Handle errors gracefully and exit with appropriate code

🔨 BUILD RUNBOOK (MVP → DEV BUILD)
Environment
OS: Ubuntu 24.04

Python: 3.11+

Tools: git, docker (optional), systemd (for production)

Phase 0 – Prerequisites
bash
sudo apt update && sudo apt install -y python3.11 python3.11-venv git wget
mkdir -p ~/projects/ && cd ~/projects/
Phase 1 – Create GitHub Repository
bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api
# 3. Description: "{API Name} API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Phase 2 – Clone to Hostnode
bash
# On hostnode
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Phase 3 – Scaffold Directory Structure
bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Phase 4 – Copy Universal Files
bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Phase 5 – Customize API-Specific Files
bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set: REPO_NAME, PORT_BLOCK, PRIMARY_APP

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set: REPO_NAME, REPO_ALLOW_PORTS

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set: port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set: app title, description, import routers

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.py
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set: API_NAME, PORT
Phase 6 – Implement 14 Pipeline Scripts
bash
# For each script, implement based on API-specific data sources
# Refer to Appendix A for script contracts
Phase 7 – Run Pipeline
bash
python automation/driver.py --dry-run
python automation/driver.py
Phase 8 – Start API
bash
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}
Phase 9 – Test API
bash
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Phase 10 – Docker Deployment
bash
docker build -f infra/docker/Dockerfile -t {api-name}:latest .
docker run -d --name {api-name} -p {dev_port}:8000 {api-name}:latest
Phase 11 – Push to GitHub
bash
git add .
git commit -m "Initial implementation for {api-name}-api"
git push origin main
Phase 12 – Clean Cache and Proceed
bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Proceed to next API
cd ~/projects/
📈 REVENUE PROJECTIONS
#	API	Low End (Mo)	High End (Mo)	Annual Potential
1	Mobile Carrier Intelligence	$49	$299	$588 - $3,588
2	Email Intelligence	$19	$199	$228 - $2,388
3	Phone Number Risk	$29	$299	$348 - $3,588
4	KYC Helper	$49	$199	$588 - $2,388
5	Fraud Velocity	$29	$149	$348 - $1,788
6	Streaming Geo-Restriction	$99	$999	$1,188 - $11,988
7	Payment Fraud Helper	$49	$299	$588 - $3,588
8	SMS Delivery Intelligence	$19	$99	$228 - $1,188
9	Device Fingerprint	$49	$399	$588 - $4,788
TOTAL		$391	$2,941	$4,692 - $35,292
🎯 PHASE 1 PRIORITY (High-Value, Low-Complexity)
Order	API	GitHub Repo	Port	Reason
1	Email Intelligence	email-intel-api	7500	Simplest, fastest to market
2	Fraud Velocity	fraud-velocity-api	7800	Reuses existing velocity engine
3	Mobile Carrier Intelligence	carrier-intel-api	7400	High demand in Africa
🔒 SECURITY & COMPLIANCE
No raw PII logs beyond 30 days

Pipeline audit logs in state/audit.log

API key authentication (planned post-MVP)

Rate limiting per tenant (planned post-MVP)

📝 SUCCESS METRICS
API uptime: ≥ 99.9%

p95 latency: < 150ms

Pipeline completion: < 30 minutes

Data accuracy: ≥ 95% (verified against ground truth)

Customer adoption: ≥ 10 paying customers in first 6 months

🗺️ ROADMAP (POST-MVP)
Phase 2: UI dashboard, webhooks, API key authentication
Phase 3: Telco CAMARA integration, regional POPs
Phase 4: Enterprise SLA, multi-region failover

⚠️ RISKS & MITIGATIONS
Risk	Mitigation
Data source unavailability	Multiple fallback data sources
Pipeline failure	14_recovery_reset.py for state recovery
Slow performance	In-memory indices, Redis caching
Security breach	Audit logging, encrypted data, firewall rules
Low adoption	Target anchor customers in Phase 1
📄 APPENDIX A — 14-SCRIPT PIPELINE CONTRACTS
Each script in automation/ must implement:

python
#!/usr/bin/env python3
"""
Script: XX_script_name.py
Purpose: [Brief description]
Input: --context (path to context.json), --dry-run (optional)
Output: JSON to stdout with keys: status, metrics, errors
Checkpoints: Updates state/checkpoints.json
"""

import json
import sys
import argparse
from pathlib import Path
from datetime import datetime

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--context', required=True, help='Path to context.json')
    parser.add_argument('--dry-run', action='store_true', help='Dry run mode')
    args = parser.parse_args()
    
    # Load context
    with open(args.context) as f:
        context = json.load(f)
    
    # ... script logic here ...
    
    # Update checkpoint
    checkpoint = {
        'script': 'XX_script_name',
        'status': 'completed',
        'timestamp': datetime.now().isoformat(),
        'metrics': {'records_processed': 1000}
    }
    
    # Print JSON output
    print(json.dumps({
        'status': 'success',
        'metrics': checkpoint['metrics'],
        'errors': []
    }))

if __name__ == '__main__':
    main()
📄 APPENDIX B — QUICK REFERENCE COMMANDS
bash
# Initial setup
make setup

# Run pipelinemake pipeline

# Start API
make api

# Run tests
make test

# Docker build
make docker-build

# Deploy
make deploy

# Security status
sr

# Health check
hc
📄 APPENDIX C — HOSTNODE SETUP
Initial Hostnode Configuration (AS-1015A-MT)
bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install -y python3.11 python3.11-venv git wget curl docker.io docker-compose

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Create projects directory
mkdir -p ~/projects/
cd ~/projects/

# Clone reference repository (gin)
git clone https://github.com/your-org/gin.git

# Set up SSH keys for GitHub (optional but recommended)
ssh-keygen -t ed25519 -C "your.email@example.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub: Settings -> SSH and GPG keys
📄 APPENDIX D — VS CODE & CONTINUE CACHE CLEANUP
Clean VS Code Cache
bash
# Option 1: Through VS Code
# Command Palette -> "Developer: Reload Window"

# Option 2: Manual (Linux)
rm -rf ~/.config/Code/CachedData/*
rm -rf ~/.config/Code/Cache/*
Clean Continue Cache
bash
# Continue cache location
rm -rf ~/.continue/cache/*
rm -rf ~/.continue/index/*
Verify Clean
bash
# Check that caches are cleared
ls -la ~/.config/Code/CachedData/  # Should be empty
ls -la ~/.continue/cache/          # Should be empty
✅ IMPLEMENTATION TRACKER
#	API	GitHub Repo	Port	Status	Handoff
1	Email Intelligence	email-intel-api	7500	⬜ Not Started	-
2	Fraud Velocity	fraud-velocity-api	7800	⬜ Not Started	-
3	Mobile Carrier Intelligence	carrier-intel-api	7400	⬜ Not Started	-
4	Phone Number Risk	phone-risk-api	7600	⬜ Not Started	-
5	KYC Helper	kyc-helper-api	7700	⬜ Not Started	-
6	Streaming Geo-Restriction	streaming-geo-api	7900	⬜ Not Started	-
7	Payment Fraud Helper	payment-fraud-api	8000	⬜ Not Started	-
8	SMS Delivery Intelligence	sms-intel-api	8100	⬜ Not Started	-
9	Device Fingerprint	device-fingerprint-api	8200	⬜ Not Started	-
© 2024 Africa Intelligence APIs. All rights reserved.

🚀 READY TO START
This document is now complete and ready for implementation.

Next Step: Begin with Phase 1, API #1 — Email Intelligence API (email-intel-api)

The human operator should:

Create GitHub repository email-intel-api

Clone to hostnode ~/projects/email-intel-api

Open in VS Code with Continue

Paste this MVP document into the chat

Start with [V4P] to design the architecture

First Handoff Block:

text
[HANDOFF] From: Human Operator To: DeepSeek V4 Pro

Context:
- We are starting implementation of the Email Intelligence API (email-intel-api)
- GitHub repository exists: https://github.com/your-org/email-intel-api
- Repository cloned to: ~/projects/email-intel-api
- Port block: 7500-7599 (dev port: 7500)
- Reference repository (gin) is at: ~/Documents/gin

Next Tasks for V4P:
- Review MVP document sections specific to Email Intelligence API
- Design the request/response models
- Design the risk scoring logic for emails
- Issue precise next steps for DeepSeek Coder
- Specify which data sources to use (domain reputation, breach databases, etc.)
[/HANDOFF]
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set: API_NAME, PORT
Phase 6 – Implement 14 Pipeline Scripts
bash
# For each script, implement based on API-specific data sources
# Refer to Appendix A for script contracts
Phase 7 – Run Pipeline
bash
python automation/driver.py --dry-run
python automation/driver.py
Phase 8 – Start API
bash
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}
Phase 9 – Test API
bash
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Phase 10 – Docker Deployment
bash
docker build -f infra/docker/Dockerfile -t {api-name}:latest .
docker run -d --name {api-name} -p {dev_port}:8000 {api-name}:latest
Phase 11 – Push to GitHub
bash
git add .
git commit -m "Initial implementation for {api-name}-api"
git push origin main
Phase 12 – Clean Cache and Proceed
bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Proceed to next API
cd ~/projects/
📈 REVENUE PROJECTIONS
#	API	Low End (Mo)	High End (Mo)	Annual Potential
1	Mobile Carrier Intelligence	$49	$299	$588 - $3,588
2	Email Intelligence	$19	$199	$228 - $2,388
3	Phone Number Risk	$29	$299	$348 - $3,588
4	KYC Helper	$49	$199	$588 - $2,388
5	Fraud Velocity	$29	$149	$348 - $1,788
6	Streaming Geo-Restriction	$99	$999	$1,188 - $11,988
7	Payment Fraud Helper	$49	$299	$588 - $3,588
8	SMS Delivery Intelligence	$19	$99	$228 - $1,188
9	Device Fingerprint	$49	$399	$588 - $4,788
TOTAL		$391	$2,941	$4,692 - $35,292
🎯 PHASE 1 PRIORITY (High-Value, Low-Complexity)
Order	API	GitHub Repo	Port	Reason
1	Email Intelligence	email-intel-api	7500	Simplest, fastest to market
2	Fraud Velocity	fraud-velocity-api	7800	Reuses existing velocity engine
3	Mobile Carrier Intelligence	carrier-intel-api	7400	High demand in Africa
🔒 SECURITY & COMPLIANCE
No raw PII logs beyond 30 days

Pipeline audit logs in state/audit.log

API key authentication (planned post-MVP)

Rate limiting per tenant (planned post-MVP)

📝 SUCCESS METRICS
API uptime: ≥ 99.9%

p95 latency: < 150ms

Pipeline completion: < 30 minutes

Data accuracy: ≥ 95% (verified against ground truth)

Customer adoption: ≥ 10 paying customers in first 6 months

🗺️ ROADMAP (POST-MVP)
Phase 2: UI dashboard, webhooks, API key authentication
Phase 3: Telco CAMARA integration, regional POPs
Phase 4: Enterprise SLA, multi-region failover

⚠️ RISKS & MITIGATIONS
Risk	Mitigation
Data source unavailability	Multiple fallback data sources
Pipeline failure	14_recovery_reset.py for state recovery
Slow performance	In-memory indices, Redis caching
Security breach	Audit logging, encrypted data, firewall rules
Low adoption	Target anchor customers in Phase 1
📄 APPENDIX A — 14-SCRIPT PIPELINE CONTRACTS
Each script in automation/ must implement:

python
#!/usr/bin/env python3
"""
Script: XX_script_name.py
Purpose: [Brief description]
Input: --context (path to context.json), --dry-run (optional)
Output: JSON to stdout with keys: status, metrics, errors
Checkpoints: Updates state/checkpoints.json
"""

import json
import sys
import argparse
from pathlib import Path
from datetime import datetime

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--context', required=True, help='Path to context.json')
    parser.add_argument('--dry-run', action='store_true', help='Dry run mode')
    args = parser.parse_args()
    
    # Load context
    with open(args.context) as f:
        context = json.load(f)
    
    # ... script logic here ...
    
    # Update checkpoint
    checkpoint = {
        'script': 'XX_script_name',
        'status': 'completed',
        'timestamp': datetime.now().isoformat(),
        'metrics': {'records_processed': 1000}
    }
    
    # Print JSON output
    print(json.dumps({
        'status': 'success',
        'metrics': checkpoint['metrics'],
        'errors': []
    }))

if __name__ == '__main__':
    main()
📄 APPENDIX B — QUICK REFERENCE COMMANDS
bash
# Initial setup
make setup

# Run pipelinemake pipeline

# Start API
make api

# Run tests
make test

# Docker build
make docker-build

# Deploy
make deploy

# Security status
sr

# Health check
hc
📄 APPENDIX C — HOSTNODE SETUP
Initial Hostnode Configuration (AS-1015A-MT)
bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install -y python3.11 python3.11-venv git wget curl docker.io docker-compose

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Create projects directory
mkdir -p ~/projects/
cd ~/projects/

# Clone reference repository (gin)
git clone https://github.com/your-org/gin.git

# Set up SSH keys for GitHub (optional but recommended)
ssh-keygen -t ed25519 -C "your.email@example.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub: Settings -> SSH and GPG keys
📄 APPENDIX D — VS CODE & CONTINUE CACHE CLEANUP
Clean VS Code Cache
bash
# Option 1: Through VS Code
# Command Palette -> "Developer: Reload Window"

# Option 2: Manual (Linux)
rm -rf ~/.config/Code/CachedData/*
rm -rf ~/.config/Code/Cache/*
Clean Continue Cache
bash
# Continue cache location
rm -rf ~/.continue/cache/*
rm -rf ~/.continue/index/*
Verify Clean
bash
# Check that caches are cleared
ls -la ~/.config/Code/CachedData/  # Should be empty
ls -la ~/.continue/cache/          # Should be empty
✅ IMPLEMENTATION TRACKER
#	API	GitHub Repo	Port	Status	Handoff
1	Email Intelligence	email-intel-api	7500	⬜ Not Started	-
2	Fraud Velocity	fraud-velocity-api	7800	⬜ Not Started	-
3	Mobile Carrier Intelligence	carrier-intel-api	7400	⬜ Not Started	-
4	Phone Number Risk	phone-risk-api	7600	⬜ Not Started	-
5	KYC Helper	kyc-helper-api	7700	⬜ Not Started	-
6	Streaming Geo-Restriction	streaming-geo-api	7900	⬜ Not Started	-
7	Payment Fraud Helper	payment-fraud-api	8000	⬜ Not Started	-
8	SMS Delivery Intelligence	sms-intel-api	8100	⬜ Not Started	-
9	Device Fingerprint	device-fingerprint-api	8200	⬜ Not Started	-
© 2024 Africa Intelligence APIs. All rights reserved.

🚀 READY TO START
This document is now complete and ready for implementation.

Next Step: Begin with Phase 1, API #1 — Email Intelligence API (email-intel-api)

The human operator should:

Create GitHub repository email-intel-api

Clone to hostnode ~/projects/email-intel-api

Open in VS Code with Continue

Paste this MVP document into the chat

Start with [V4P] to design the architecture

First Handoff Block:

text
[HANDOFF] From: Human Operator To: DeepSeek V4 Pro

Context:
- We are starting implementation of the Email Intelligence API (email-intel-api)
- GitHub repository exists: https://github.com/your-org/email-intel-api
- Repository cloned to: ~/projects/email-intel-api
- Port block: 7500-7599 (dev port: 7500)
- Reference repository (gin) is at: ~/Documents/gin

Next Tasks for V4P:
- Review MVP document sections specific to Email Intelligence API
- Design the request/response models
- Design the risk scoring logic for emails
- Issue precise next steps for DeepSeek Coder
- Specify which data sources to use (domain reputation, breach databases, etc.)
[/HANDOFF]/phone matches their claimed carrier

Support AML/CFT compliance checks

Assist SOC teams in incident investigations

Other similar markets: Kenya, Ghana, South Africa, India, Brazil, Indonesia, Philippines.

💰 VALUE PROPOSITION
For Banks & Fintechs:

Reduce fraud losses

Improve KYC/AML checks

Strengthen login security

Enhance risk scoring models

For Telcos:

Optimize SMS delivery

Detect SIM-swap fraud

Improve network intelligence

For Streaming Services:

Enforce geo-restrictions

Detect VPN/proxy violations

Improve content delivery

📁 GITHUB REPOSITORY NAMING CONVENTION
All repositories follow this naming pattern:

text
{api-name}-api
#	API	GitHub Repo Name	Port Block
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499
2	Email Intelligence	email-intel-api	7500-7599
3	Phone Number Risk	phone-risk-api	7600-7699
4	KYC Helper	kyc-helper-api	7700-7799
5	Fraud Velocity	fraud-velocity-api	7800-7899
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999
7	Payment Fraud Helper	payment-fraud-api	8000-8099
8	SMS Delivery Intelligence	sms-intel-api	8100-8199
9	Device Fingerprint	device-fingerprint-api	8200-8299
Environment Variables per Repo
Each repo will have a .env file with:

bash
# API Configuration
API_NAME={api-name}
API_VERSION=v1
PORT={dev_port}

# Database Paths
DATA_DIR=./data
ARTIFACTS_DIR=./artifacts
STATE_DIR=./state

# Logging
LOG_LEVEL=INFO
LOG_FILE=./logs/api.log

# Security (post-MVP)
API_KEY_REQUIRED=false
RATE_LIMIT_ENABLED=false

# Pipeline
PIPELINE_LOCK_FILE=./state/pipeline.lock
CHECKPOINT_FILE=./state/checkpoints.json
CONTEXT_FILE=./state/context.json
AUDIT_LOG=./state/audit.log
🔨 IMPLEMENTATION WORKFLOW — PER API
Step 1: Create GitHub Repository
Action: Human operator creates repository on GitHub

bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api (e.g., carrier-intel-api)
# 3. Description: "Mobile Carrier Intelligence API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Step 2: Clone Repository to Hostnode
Action: Human operator clones the repo to the hostnode (AS-1015A-MT server)

bash
# On hostnode (Ubuntu 24.04)
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Step 3: Scaffold Directory Structure
Action: Run the universal directory creation script

bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Step 4: Copy Universal Files
Action: Copy files from reference repository (gin)

bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Step 5: Customize API-Specific Files
Action: Edit files for this specific API

bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set:
#   REPO_NAME: {api-name}-api
#   PORT_BLOCK: {port_block}
#   PRIMARY_APP: {api-name}

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set:
#   REPO_NAME={api-name}-api
#   REPO_ALLOW_PORTS={ports}

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set:
#   app title: "{API Name} API"
#   app description: "..."
#   import routers from v1

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.py
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set:
#   API_NAME={api-name}
#   PORT={dev_port}
Step 6: Implement Automation Pipeline
Action: Build the 14 automation scripts

bash
# For each script, implement based on API-specific data sources
# Scripts:
# 01_prepare_env.py - Set up environment
# 02_load_config.py - Load configuration
# 03_fetch_data.py - Fetch raw data
# 04_parse_data.py - Parse data
# 05_enrich_data.py - Enrich with intelligence
# 06_validate_data.py - Validate data
# 07_build_index.py - Build JSON index
# 08_test_index.py - Test index
# 09_run_risk_scoring.py - Apply risk scoring
# 10_publish_outputs.py - Publish artifacts
# 11_health_gate.py - Health checks
# 12_verify_validate.py - Verification
# 13_test_suite.py - Run tests
# 14_recovery_reset.py - Recovery
# driver.py - Orchestrator
Step 7: Test Locally
Action: Run pipeline and start API

bash
# Create Python virtual environment
python3.11 -m venv env
source env/bin/activate
pip install -r requirements.txt

# Run pipeline
python automation/driver.py --dry-run
python automation/driver.py

# Start API
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}

# Test endpoints
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Step 8: Push to GitHub
Action: Commit and push to sync with GitHub

bash
# Stage all files
git add .

# Commit with message
git commit -m "Initial scaffold for {api-name}-api

- Directory structure created
- Universal files copied from gin
- Customized AGENT_MANIFEST.md
- Customized firewall config
- Created API models and endpoints
- Implemented automation pipeline
"

# Push to GitHub
git push origin main
Step 9: Verify Sync
Action: Confirm files are on GitHub

bash
# Check GitHub repository
# Navigate to https://github.com/your-org/{api-name}-api
# Verify all files are present
Step 10: Clean Cache and Proceed to Next API
Action: Prepare for next API implementation

bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"
# Or: rm -rf ~/.config/Code/CachedData/*

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Navigate to parent directory
cd ~/projects/

# Proceed to next API (repeat from Step 1)
📋 STEP-BY-STEP CHECKLIST FOR EACH API
For each API, complete this checklist:

Pre-Implementation (Human Operator)
Create GitHub repository {api-name}-api

Clone to hostnode ~/projects/{api-name}-api

Note port block from allocation table

Set environment variables in .env

Implementation (DeepSeek Coder)
Scaffold directory structure (Step 3)

Copy universal files (Step 4)

Customize API-specific files (Step 5)

AGENT_MANIFEST.md

peer_allow_profile.conf

apply-rules.sh

api/main.py

api/models/request.py

api/models/response.py

api/v1/lookup.py

api/v1/batch.py

.env

Data Pipeline (DeepSeek Coder)
Implement 14 automation scripts

01_prepare_env.py

02_load_config.py

03_fetch_data.py

04_parse_data.py

05_enrich_data.py

06_validate_data.py

07_build_index.py

08_test_index.py

09_run_risk_scoring.py

10_publish_outputs.py

11_health_gate.py

12_verify_validate.py

13_test_suite.py

14_recovery_reset.py

driver.py

Testing (DeepSeek Coder)
Run pipeline python automation/driver.py

Start API uvicorn api.main:app

Test endpoints curl

Run test suite python -m pytest tests/

Deployment (Human Operator)
Commit changes git add . && git commit -m "..." && git push

Verify GitHub sync (check repository online)

Clean caches (Continue, VS Code)

Proceed to next API

📊 PORT BLOCK ALLOCATION (Bulletin 001)
#	API	GitHub Repo	Block	Dev Port	Prod Port
0	IP Risk API	ip-risk-api	7200-7299	7200	7201
0	Gin (Reference)	gin	7300-7399	7300	7301
1	Mobile Carrier Intelligence	carrier-intel-api	7400-7499	7400	7401
2	Email Intelligence	email-intel-api	7500-7599	7500	7501
3	Phone Number Risk	phone-risk-api	7600-7699	7600	7601
4	KYC Helper	kyc-helper-api	7700-7799	7700	7701
5	Fraud Velocity	fraud-velocity-api	7800-7899	7800	7801
6	Streaming Geo-Restriction	streaming-geo-api	7900-7999	7900	7901
7	Payment Fraud Helper	payment-fraud-api	8000-8099	8000	8001
8	SMS Delivery Intelligence	sms-intel-api	8100-8199	8100	8101
9	Device Fingerprint	device-fingerprint-api	8200-8299	8200	8201
Shared Ports: 9090 (Prometheus), 3000 (Grafana)

🔌 API ENDPOINTS (MVP)
Unified Response Format
All APIs share a common response structure:

json
{
  "success": true,
  "data": {
    // API-specific data
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z",
    "version": "v1",
    "api": "api-name"
  }
}
Error Response Format
json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  },
  "meta": {
    "request_id": "uuid",
    "timestamp": "2024-01-01T00:00:00Z"
  }
}
API-Specific Endpoints
#	API	Method	Path	Description
1	Carrier	GET	/v1/carrier/lookup?phone={phone}	Lookup carrier by phone number
1	Carrier	POST	/v1/carrier/batch	Batch carrier lookup
2	Email	GET	/v1/email/validate?email={email}	Validate and analyze email
2	Email	POST	/v1/email/batch	Batch email validation
3	Phone Risk	GET	/v1/phone/risk?phone={phone}	Assess phone number risk
3	Phone Risk	POST	/v1/phone/batch	Batch phone risk assessment
4	KYC	POST	/v1/kyc/verify	Verify identity
4	KYC	POST	/v1/kyc/document	Validate document
5	Velocity	POST	/v1/velocity/track	Track an event
5	Velocity	GET	/v1/velocity/check?entity={id}	Check velocity
6	Streaming	GET	/v1/streaming/geo?ip={ip}	Geo-restriction lookup
6	Streaming	POST	/v1/streaming/batch	Batch geo-restriction lookup
7	Payment	POST	/v1/payment/check	Check payment fraud
7	Payment	GET	/v1/payment/bin/{bin}	BIN lookup
8	SMS	GET	/v1/sms/route?phone={phone}	Best SMS route
8	SMS	POST	/v1/sms/predict	Delivery prediction
9	Device	POST	/v1/fingerprint/generate	Generate device fingerprint
9	Device	GET	/v1/fingerprint/check/{id}	Check fingerprint
All	All	GET	/v1/health	Service health status
🏗️ OFFLINE PIPELINE — 14 SCRIPTS (DeepSeek Coder Ready)
All scripts live in automation/. A driver.py orchestrates them, passing a shared context.json. Each script supports --dry-run and --resume. A lock file prevents concurrent runs. Checkpoints are saved in state/checkpoints.json.

Script List (14)
#	Script	Purpose
1	01_prepare_env.py	Set up environment, verify dependencies
2	02_load_config.py	Load configuration from env/config files
3	03_fetch_data.py	Fetch/refresh raw data from sources
4	04_parse_data.py	Parse raw data into structured format
5	05_enrich_data.py	Enrich with additional intelligence
6	06_validate_data.py	Validate data quality and completeness
7	07_build_index.py	Build JSON indices from processed data
8	08_test_index.py	Test index performance and accuracy
9	09_run_risk_scoring.py	Apply risk scoring to data
10	10_publish_outputs.py	Publish versioned artifacts
11	11_health_gate.py	Check health gates for deployment
12	12_verify_validate.py	Verify data meets requirements
13	13_test_suite.py	Run comprehensive test suite
14	14_recovery_reset.py	Reset state for recovery
Script Contract
Each script must:

Accept --context (path to context.json) and --dry-run flags

Update state/checkpoints.json with completion status

Print JSON output to stdout (status, metrics, errors)

Handle errors gracefully and exit with appropriate code

🔨 BUILD RUNBOOK (MVP → DEV BUILD)
Environment
OS: Ubuntu 24.04

Python: 3.11+

Tools: git, docker (optional), systemd (for production)

Phase 0 – Prerequisites
bash
sudo apt update && sudo apt install -y python3.11 python3.11-venv git wget
mkdir -p ~/projects/ && cd ~/projects/
Phase 1 – Create GitHub Repository
bash
# On GitHub.com
# 1. Click "New Repository"
# 2. Repository name: {api-name}-api
# 3. Description: "{API Name} API for Africa"
# 4. Public/Private: Private (for now)
# 5. Initialize with README: Yes
# 6. Click "Create Repository"
Phase 2 – Clone to Hostnode
bash
# On hostnode
cd ~/projects/
git clone https://github.com/your-org/{api-name}-api.git
cd {api-name}-api
Phase 3 – Scaffold Directory Structure
bash
# Create all directories
mkdir -p api/{v1,models,utils,extras}
mkdir -p automation
mkdir -p scripts/cli/commands
mkdir -p scripts/security/{evidence,verification,incident,ml_agent,firewall}
mkdir -p infra/{docker,prometheus,grafana,traefik}
mkdir -p tests
mkdir -p docs/security
mkdir -p data/{source1,source2,threatfeeds}
mkdir -p artifacts/current
mkdir -p state
mkdir -p .github/{copilot,workflows}
mkdir -p logs
Phase 4 – Copy Universal Files
bash
REF=/home/versey/Documents/gin

# API core
cp $REF/api/utils/*.py api/utils/
cp $REF/api/models/__init__.py api/models/
cp $REF/api/v1/__init__.py api/v1/
cp $REF/api/v1/health.py api/v1/
cp $REF/api/__init__.py api/
cp $REF/api/extras/__init__.py api/extras/
cp $REF/api/extras/velocity.py api/extras/

# Security & CLI
cp -r $REF/scripts/security/* scripts/security/
cp -r $REF/scripts/cli/* scripts/cli/
cp -r $REF/docs/security/* docs/security/
cp $REF/.github/copilot/AGENT_MANIFEST.md .github/copilot/

# Infrastructure
cp $REF/infra/docker/Dockerfile infra/docker/
cp $REF/infra/prometheus/prometheus.yml infra/prometheus/

# Pipeline & config
cp $REF/requirements.txt .
cp $REF/.env.example .env
cp $REF/.gitignore .
cp $REF/Makefile .
cp $REF/state/context.json state/
cp $REF/state/checkpoints.json state/

# Make scripts executable
chmod +x scripts/security/*/*.sh scripts/cli/aliases.sh scripts/cli/commands/*.sh
chmod +x automation/*.py 2>/dev/null || true

# Create empty automation scripts
for i in {01..14}; do
    touch automation/${i}_*.py
done
touch automation/driver.py
chmod +x automation/*.py
Phase 5 – Customize API-Specific Files
bash
# 1. Edit AGENT_MANIFEST.md
vim .github/copilot/AGENT_MANIFEST.md
# Set: REPO_NAME, PORT_BLOCK, PRIMARY_APP

# 2. Edit firewall configuration
vim scripts/security/firewall/peer_allow_profile.conf
# Set: REPO_NAME, REPO_ALLOW_PORTS

# 3. Edit firewall apply-rules.sh
vim scripts/security/firewall/apply-rules.sh
# Set: port block in nftables

# 4. Edit api/main.py
vim api/main.py
# Set: app title, description, import routers

# 5. Create API models
vim api/models/request.py
vim api/models/response.py

# 6. Create API endpoints
vim api/v1/lookup.py
vim api/v1/batch.py

# 7. Edit .env file
vim .env
# Set: API_NAME, PORT
Phase 6 – Implement 14 Pipeline Scripts
bash
# For each script, implement based on API-specific data sources
# Refer to Appendix A for script contracts
Phase 7 – Run Pipeline
bash
python automation/driver.py --dry-run
python automation/driver.py
Phase 8 – Start API
bash
uvicorn api.main:app --reload --host 0.0.0.0 --port {dev_port}
Phase 9 – Test API
bash
curl http://localhost:{dev_port}/v1/health
curl http://localhost:{dev_port}/v1/lookup?param=value
Phase 10 – Docker Deployment
bash
docker build -f infra/docker/Dockerfile -t {api-name}:latest .
docker run -d --name {api-name} -p {dev_port}:8000 {api-name}:latest
Phase 11 – Push to GitHub
bash
git add .
git commit -m "Initial implementation for {api-name}-api"
git push origin main
Phase 12 – Clean Cache and Proceed
bash
# Deactivate virtual environment
deactivate

# Clean VS Code cache
# In VS Code: Command Palette -> "Developer: Reload Window"

# Clean Continue cache
# rm -rf ~/.continue/cache/*

# Proceed to next API
cd ~/projects/
📈 REVENUE PROJECTIONS
#	API	Low End (Mo)	High End (Mo)	Annual Potential
1	Mobile Carrier Intelligence	$49	$299	$588 - $3,588
2	Email Intelligence	$19	$199	$228 - $2,388
3	Phone Number Risk	$29	$299	$348 - $3,588
4	KYC Helper	$49	$199	$588 - $2,388
5	Fraud Velocity	$29	$149	$348 - $1,788
6	Streaming Geo-Restriction	$99	$999	$1,188 - $11,988
7	Payment Fraud Helper	$49	$299	$588 - $3,588
8	SMS Delivery Intelligence	$19	$99	$228 - $1,188
9	Device Fingerprint	$49	$399	$588 - $4,788
TOTAL		$391	$2,941	$4,692 - $35,292
🎯 PHASE 1 PRIORITY (High-Value, Low-Complexity)
Order	API	GitHub Repo	Port	Reason
1	Email Intelligence	email-intel-api	7500	Simplest, fastest to market
2	Fraud Velocity	fraud-velocity-api	7800	Reuses existing velocity engine
3	Mobile Carrier Intelligence	carrier-intel-api	7400	High demand in Africa
🔒 SECURITY & COMPLIANCE
No raw PII logs beyond 30 days

Pipeline audit logs in state/audit.log

API key authentication (planned post-MVP)

Rate limiting per tenant (planned post-MVP)

📝 SUCCESS METRICS
API uptime: ≥ 99.9%

p95 latency: < 150ms

Pipeline completion: < 30 minutes

Data accuracy: ≥ 95% (verified against ground truth)

Customer adoption: ≥ 10 paying customers in first 6 months

🗺️ ROADMAP (POST-MVP)
Phase 2: UI dashboard, webhooks, API key authentication
Phase 3: Telco CAMARA integration, regional POPs
Phase 4: Enterprise SLA, multi-region failover

⚠️ RISKS & MITIGATIONS
Risk	Mitigation
Data source unavailability	Multiple fallback data sources
Pipeline failure	14_recovery_reset.py for state recovery
Slow performance	In-memory indices, Redis caching
Security breach	Audit logging, encrypted data, firewall rules
Low adoption	Target anchor customers in Phase 1
📄 APPENDIX A — 14-SCRIPT PIPELINE CONTRACTS
Each script in automation/ must implement:

python
#!/usr/bin/env python3
"""
Script: XX_script_name.py
Purpose: [Brief description]
Input: --context (path to context.json), --dry-run (optional)
Output: JSON to stdout with keys: status, metrics, errors
Checkpoints: Updates state/checkpoints.json
"""

import json
import sys
import argparse
from pathlib import Path
from datetime import datetime

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--context', required=True, help='Path to context.json')
    parser.add_argument('--dry-run', action='store_true', help='Dry run mode')
    args = parser.parse_args()
    
    # Load context
    with open(args.context) as f:
        context = json.load(f)
    
    # ... script logic here ...
    
    # Update checkpoint
    checkpoint = {
        'script': 'XX_script_name',
        'status': 'completed',
        'timestamp': datetime.now().isoformat(),
        'metrics': {'records_processed': 1000}
    }
    
    # Print JSON output
    print(json.dumps({
        'status': 'success',
        'metrics': checkpoint['metrics'],
        'errors': []
    }))

if __name__ == '__main__':
    main()
📄 APPENDIX B — QUICK REFERENCE COMMANDS
bash
# Initial setup
make setup

# Run pipelinemake pipeline

# Start API
make api

# Run tests
make test

# Docker build
make docker-build

# Deploy
make deploy

# Security status
sr

# Health check
hc
📄 APPENDIX C — HOSTNODE SETUP
Initial Hostnode Configuration (AS-1015A-MT)
bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install -y python3.11 python3.11-venv git wget curl docker.io docker-compose

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Create projects directory
mkdir -p ~/projects/
cd ~/projects/

# Clone reference repository (gin)
git clone https://github.com/your-org/gin.git

# Set up SSH keys for GitHub (optional but recommended)
ssh-keygen -t ed25519 -C "your.email@example.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub: Settings -> SSH and GPG keys
📄 APPENDIX D — VS CODE & CONTINUE CACHE CLEANUP
Clean VS Code Cache
bash
# Option 1: Through VS Code
# Command Palette -> "Developer: Reload Window"

# Option 2: Manual (Linux)
rm -rf ~/.config/Code/CachedData/*
rm -rf ~/.config/Code/Cache/*
Clean Continue Cache
bash
# Continue cache location
rm -rf ~/.continue/cache/*
rm -rf ~/.continue/index/*
Verify Clean
bash
# Check that caches are cleared
ls -la ~/.config/Code/CachedData/  # Should be empty
ls -la ~/.continue/cache/          # Should be empty
✅ IMPLEMENTATION TRACKER
#	API	GitHub Repo	Port	Status	Handoff
1	Email Intelligence	email-intel-api	7500	⬜ Not Started	-
2	Fraud Velocity	fraud-velocity-api	7800	⬜ Not Started	-
3	Mobile Carrier Intelligence	carrier-intel-api	7400	⬜ Not Started	-
4	Phone Number Risk	phone-risk-api	7600	⬜ Not Started	-
5	KYC Helper	kyc-helper-api	7700	⬜ Not Started	-
6	Streaming Geo-Restriction	streaming-geo-api	7900	⬜ Not Started	-
7	Payment Fraud Helper	payment-fraud-api	8000	⬜ Not Started	-
8	SMS Delivery Intelligence	sms-intel-api	8100	⬜ Not Started	-
9	Device Fingerprint	device-fingerprint-api	8200	⬜ Not Started	-
© 2024 Africa Intelligence APIs. All rights reserved.

🚀 READY TO START
This document is now complete and ready for implementation.

Next Step: Begin with Phase 1, API #1 — Email Intelligence API (email-intel-api)

The human operator should:

Create GitHub repository email-intel-api

Clone to hostnode ~/projects/email-intel-api

Open in VS Code with Continue

Paste this MVP document into the chat

Start with [V4P] to design the architecture

First Handoff Block:

text
[HANDOFF] From: Human Operator To: DeepSeek V4 Pro

Context:
- We are starting implementation of the Email Intelligence API (email-intel-api)
- GitHub repository exists: https://github.com/your-org/email-intel-api
- Repository cloned to: ~/projects/email-intel-api
- Port block: 7500-7599 (dev port: 7500)
- Reference repository (gin) is at: ~/Documents/gin

Next Tasks for V4P:
- Review MVP document sections specific to Email Intelligence API
- Design the request/response models
- Design the risk scoring logic for emails
- Issue precise next steps for DeepSeek Coder
- Specify which data sources to use (domain reputation, breach databases, etc.)
[/HANDOFF]
