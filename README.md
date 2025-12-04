# MedAI-Agent

A research prototype that creates specialized LLM-based AI agents to analyze complex medical cases. This system runs multiple specialist agents in parallel, integrates their insights, and produces a consolidated assessment with suggested directions for further evaluation and management.

⚠️ IMPORTANT DISCLAIMER
This project is for research and educational purposes only. It is not intended for clinical use, medical decision making, or patient care. Do NOT use this tool as a substitute for professional medical judgment.

---

## Features
- Runs multiple specialist AI agents (currently: Cardiologist, Psychologist, Pulmonologist)
- Agents operate in parallel and return structured findings
- Combines and summarizes outputs into prioritized possible diagnoses and suggested next steps
- Simple file-based input/output: put medical reports in `Medical Reports/` and check `Results/` for outputs
- Extensible architecture for adding more specialists or local LLM backends

---

## Repository Structure
- `Medical Reports/` — Synthetic sample medical report files for testing
- `Results/` — Generated outputs from the agents
- `main.py` — Entry point for running the system
- `agents/` — Agent implementations and orchestration logic
- `requirements.txt` — Python dependencies
- `.gitignore`, `LICENSE`, `apikey.env` (local)

---

## Quickstart

1. Clone the repo
   - git clone https://github.com/Avinash3570/MedAI-Agent.git
   - cd MedAI-Agent

2. Create and activate a virtual environment
   - macOS / Linux:
     - python -m venv venv
     - source venv/bin/activate
   - Windows (PowerShell):
     - python -m venv venv
     - .\venv\Scripts\Activate.ps1

3. Install dependencies
   - pip install -r requirements.txt

4. Provide your LLM API key
   - Create a file at the project root named `apikey.env`
   - Add the following line:
     - OPENAI_API_KEY=your_api_key_here
   - (If you use another provider, update the project config/adapter accordingly.)

5. Run the system
   - python main.py
   - Input reports placed in `Medical Reports/` will be processed and outputs written to `Results/`.

---

## Running with Example Reports
- Drop a `.txt` or supported report file in the `Medical Reports/` directory.
- Each run will spawn the specialist agents in parallel, generate agent-specific findings, and create a combined summary (saved in `Results/`).
- Example filename conventions: `case-001.txt`, `sample-report.txt`.

---

## Agents & Responsibilities
- Cardiologist Agent
  - Focus: Detect cardiac issues (arrhythmias, structural abnormalities, ischemia patterns).
  - Outputs: Suggested tests (ECG, echocardiogram, cardiac enzymes), monitoring recommendations.
- Psychologist Agent
  - Focus: Identify psychological or behavioral contributors (anxiety, panic, depression).
  - Outputs: Therapy suggestions, screening tools, medication considerations.
- Pulmonologist Agent
  - Focus: Assess respiratory causes (asthma, COPD, sleep/disordered breathing).
  - Outputs: Lung function tests, imaging recommendations, breathing management.

The system aggregates their findings and summarizes the top 2–3 likely issues with reasoning and suggested next steps.

---

## Configuration & Extensibility
- Model selection and API endpoints are configurable in the code (search for `MODEL`, `API`, or `provider` settings).
- To add a new specialist:
  - Create a new agent module under `agents/`
  - Implement the agent interface used by the orchestrator (input parsing, prompt template, output parsing)
  - Register the agent with the orchestrator

Planned: adapters for local LLMs (Ollama, vLLM, llama.cpp) and function-calling style outputs with strict JSON schemas.

---

## Safety, Ethics & Limitations
- Not validated for clinical performance — do not use for diagnosis or treatment decisions.
- LLM outputs may hallucinate or omit key details. Always verify findings against primary data and clinical expertise.
- Do not include patient identifiers or protected health information (PHI) when using public or untrusted models/APIs.
- Consider adding logging, audit trails, and differential privacy before handling real clinical data.

---

## Testing & CI Suggestions
- Add unit tests that mock LLM responses to validate parsing and aggregation logic.
- Create smoke tests that verify end-to-end flows using deterministic/mocked models.
- Use environment-specific configuration for CI that does not contain real API keys.

---

## Contributing
Contributions are welcome (features, bug fixes, extra agents). When opening PRs:
- Describe the change and rationale
- Add tests for new behavior where possible
- Keep changes modular (one agent or feature per PR)

Please follow the existing code style and add documentation for new components.

---

## Future Enhancements (Planned)
- Specialist Expansion: Neurology, Endocrinology, Immunology, etc.
- Local LLM Support: Ollama, vLLM, llama.cpp
- Vision Capabilities: Radiology image analysis and multimodal fusion
- Live Data Tools: Real-time queries to structured medical datasets
- Advanced Parsing: Strict JSON schema outputs, schema validation
- Automated Testing: Mocked LLM calls, reproducible CI

---

## License
This project is released under the MIT License. See the `LICENSE` file for details.

---
