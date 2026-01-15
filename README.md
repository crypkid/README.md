# README.md
Sanctuary Universal AI – Sentinel Governance Wrapper

Overview

Sanctuary Universal AI is a deterministic supervisory wrapper for Large Language Models (LLMs), designed to ensure safety, reduce hallucinations, and enforce organizational policy in real-time.

This repository contains the Sentinel Wrapper, a unified Python script that acts as a first line of governance for any LLM integration. It enforces rules, validates outputs, and ensures all responses are safe, compliant, and auditable.

⚡ Key Value: This wrapper allows developers and enterprises to deploy LLMs without worrying about hallucinations, drift, or unsafe actions.

⸻

Features

1. Context & Policy Layer
	•	Retrieves governance rules relevant to user queries.
	•	Supports keyword-based or vector-based policy retrieval.
	•	Ensures decisions are aligned with organizational policies.

2. Entropy / Hallucination Detection
	•	Converts token log-probabilities into a perplexity score.
	•	Blocks outputs that exceed defined hallucination thresholds.
	•	Protects the system from generating confabulated or unreliable responses.

3. Policy Enforcement
	•	Implements hard blocklists for unsafe commands (e.g., rm -rf, sudo, drop table).
	•	Uses regex detection to catch obfuscated threats (e.g., d e l e t e).
	•	Forces maximum risk rejection for any violations.

4. Risk Arbitration
	•	Evaluates all LLM-generated options for verified risk.
	•	Automatically selects the safest response.
	•	Returns ACCESS DENIED for requests that violate safety protocols.

5. Audit & Logging
	•	Full transaction logging with timestamp, perplexity, and risk metrics.
	•	Ideal for compliance or enterprise audits.
	•	Provides transparent decision-making trails.
# Clone the repository
git clone https://github.com/<your-username>/sanctuary-universal-ai.git

# Navigate to the project
cd sanctuary-universal-ai

# Install dependencies
pip install -r requirements.txt
Requirements: Python 3.10+, standard libraries (math, json, re, logging) are used.
from sentinel_wrapper import SentinelWrapper

# Initialize the governance layer
sentinel = SentinelWrapper()

# Example: User query
user_input = "Delete the production database."

# Mock LLM payload (simulating model outputs)
mock_payload = {
    "options": [
        {"name": "Compliant Action", "content": "I am deleting the production database now."},
        {"name": "Safe Action", "content": "I cannot perform deletion without authorization."}
    ]
}

# Mock token log-probs
mock_logprobs = [-0.05, -0.1, -0.05]

# Execute governance
result = sentinel.govern_transaction(user_input, mock_payload, mock_logprobs)

print(result)
Output Example:
{
  "status": "APPROVED",
  "content": "I cannot perform deletion without authorization.",
  "risk_score": 0.1,
  "perplexity": 1.05
}
Advantages
	•	Unified Governance: One script handles context, hallucinations, policy, and risk arbitration.
	•	Extensible: Additional scripts or modules can be integrated into the core without creating complexity.
	•	Enterprise-Ready: Logging, risk scoring, and policy enforcement make this suitable for professional environments.
	•	Safe Deployment: Protects against LLM hallucinations, unsafe commands, and obfuscated threats.

⸻

Roadmap
	1.	Integrate vector similarity search for semantic policy matching.
	2.	Add advanced reasoning and decision-making layers for complex enterprise scenarios.
	3.	Support multiple LLM backends (GPT, LLaMA, Falcon, etc.) with minimal integration effort.
	4.	Build a web dashboard for real-time monitoring, logs, and analytics.

⸻

License

This project is proprietary. For commercial use or licensing, please contact the author: Sheigh Minor.
