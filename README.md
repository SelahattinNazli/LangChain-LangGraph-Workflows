# LangChain & LangGraph Workflows

This project aims to **recreate and experiment with agent workflows** inspired by Anthropic's *"Building Effective Agents"* article, using the **LangChain** and **LangGraph** frameworks in combination with **Ollama models**.

The goal is to explore how structured reasoning and workflow-based LLM designs can improve controllability, interpretability, and reliability of AI agents.

---

## Project Structure

Each workflow in this repository corresponds to a different **agentic reasoning pattern** (e.g., single-step inference, multi-step reasoning, planning, reflection, etc.).  
Every workflow is implemented as an independent `.py` file for clarity and modularity.

---

## Workflow 1: Single-Step Sentiment Analysis

**File:** `single_step_workflow.py`  
**Model:** `qwen3:1.7b` via Ollama  
**Frameworks:** LangChain + Pydantic  

This first workflow demonstrates a **simple, single-step LLM process**, where the model:
1. Receives a product review text,  
2. Analyzes its sentiment,  
3. Returns a structured output (`positive`, `negative`, or `neutral`) defined by a Pydantic schema.

This workflow serves as the foundation for more complex, multi-step pipelines that will follow.

---

### Workflow Diagram

Below is a simplified diagram of the first workflow:

<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/08001314-1889-4cc2-a3c2-cd561796b989" />


*(The diagram illustrates the prompt → model → structured output flow.)*

---
## Requirements

Install dependencies from `requirements.txt`:

```bash
pip install -r requirements.txt
```
Ensure Ollama is running locally and the model qwen3:1.7b is available:

```bash
ollama pull qwen3:1.7b
```
Running the Workflow
```bash
python single_step_workflow.py
```
Expected output:
```bash
Single Step LLM Workflow Response: positive
```
------------------------------------------------------------------------------
## Workflow 2: Marketing Copy Generation & Translation

**File:** `prompt_chaining_workflow.py`

**Model:** `qwen3:1.7b via Ollama`

**Frameworks:** LangChain + Pydantic

This workflow demonstrates a two-step LLM process:

## Marketing Copy Generation

The model generates a sales-focused marketing copy based on a given product name.

The output is structured into headline, body, and call-to-action.

Outputs are validated using a Pydantic schema.

## Translation

The validated marketing copy is translated into the target language.

Translation preserves marketing tone and cultural appropriateness.

This workflow serves as a foundation for more complex, multi-step LLM pipelines.

## Workflow Diagram

Below is a simplified diagram of the workflow:

<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/47a2917c-48b9-41a9-8f84-fc973efe0c48" />

## Requirements

Install dependencies from requirements.txt:
```bash
pip install -r requirements.txt
```
Ensure Ollama is running locally and the model qwen3:1.7b is available:
```bash
ollama pull qwen3:1.7b
```
Running the Workflow
```bash
python marketing_translation_workflow.py
```

## Expected output (example):

✅ Gate PASSED: Marketing copy approved

📢 Translated Headline: Cámara de Seguridad Inteligente para Hogar

📄 Translated Body: Esta cámara de seguridad para el hogar es increíble...

📣 Translated Call to Action: ¡Compra ahora y protege tu hogar!

---------------------------------------------------------------------------
## Workflow 3: Customer Query Classification & Routing

**File:** `routing_workflow.py`

**Model:** `qwen3:1.7b via Ollama1`

**Frameworks:** LangChain + Pydantic

This workflow demonstrates agentic reasoning with routing:

Classify customer queries into categories (technical, billing, general, refund) with confidence and complexity scores.

Route the query to the appropriate handler based on the classification:

Technical Support → step-by-step troubleshooting

Billing → explanation and next steps

General → helpful answers with links

Refund → ticket creation and estimated response time

## Workflow Diagram

<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/3e18797d-850d-473e-aed8-90b70152ebfa" />



## Expected output:

🔍 Query Category: billing (Confidence: 0.92)

🛠️ Handler: handle_billing

📄 Response: {'handler': 'Billing Department', 'explanation': '...', 'next_action': '...', 'response_type': 'billing'}

## Requirements

Install dependencies for all workflows from a single requirements.txt:
```bash
pip install -r requirements.txt
```

Ensure Ollama is running locally and the qwen3:1.7b model is available:
```bash
ollama pull qwen3:1.7b
```
----------------------------------------------------------------------------
## Workflow 4: Parallel Security Review Voting

**File:** `parallelization_workflow.py`

**Model:** `qwen3:1.7b via Ollama`

**Frameworks:** LangChain + Pydantic

This workflow demonstrates parallelized LLM evaluation for security code review, where multiple specialized experts assess the same piece of code simultaneously.

The workflow introduces parallel execution through RunnableMap and performs majority voting to reach a consensus on whether the code is vulnerable or safe.

## Workflow Overview

### Expert Prompts:
Three security experts are simulated:

SQL Injection Expert

Authentication Expert

General Security Expert

### Parallel Execution:
Each expert runs in parallel using RunnableMap, producing structured evaluations via Pydantic schemas.

### Majority Voting:
The system aggregates all expert responses to determine if the overall code is vulnerable or safe, based on majority consensus.

### Pydantic Schema

The model outputs structured data in the following format:
```bash
class SecurityAssessment(BaseModel):
    has_vulnerability: bool
    issue_type: str
    confidence: float
```
## Workflow Diagram

Below is a simplified diagram of the parallel security voting process:

<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/510410a9-422c-47d2-9dc9-2805fd09b027" />


(The diagram illustrates how each expert runs in parallel → produces structured outputs → aggregates for majority voting.)

## Requirements

Install dependencies from requirements.txt:
```bash
pip install -r requirements.txt
```

Ensure Ollama is running locally and the model qwen3:1.7b is available:
```bash
ollama pull qwen3:1.7b
```
Running the Workflow
```bash
python parallelization_workflow.py
```
Example Output
```bash
Total Reviewers: 3
Vulnerability Votes: 2
Majority Vulnerability: True
Findings: [
  'sql_expert: VULN - SQL Injection Risk',
  'auth_expert: SAFE - No issues found',
  'general_expert: VULN - Input Sanitization Missing'
]
Consensus: VULNERABLE
```
### Key Learning

This workflow introduces parallelization and consensus mechanisms for AI-driven decision making.
It is particularly useful in domains like security auditing, compliance validation, or multi-agent reasoning, where diverse expert perspectives must be evaluated efficiently.

----------------------------------------------------------------------------
## Workflow 5: Iterative Code Evaluation & Optimization

**File:** `evaluator_optimizer_workflow.py`

**Model:** `qwen3:1.7b via Ollama`

**Frameworks:** LangChain + Pydantic

This workflow introduces a multi-iteration evaluation and optimization pipeline, where an LLM acts as both a code generator and a reviewer, continuously improving the generated code until it becomes production-ready or reaches a defined iteration limit.

It demonstrates a self-improving agentic workflow, simulating real-world software development loops of generation → review → optimization → re-evaluation.

## Workflow Overview

### Code Generation
The model generates initial working code for a given task.
It provides explanations, language type, and estimated complexity.

### Code Review
A second LLM reviews the generated code on multiple dimensions:

Functionality

Quality & readability

Performance & efficiency

Best practice compliance

The review outputs structured scores and concrete improvement suggestions.

### Code Optimization
The original code is optimized based on review feedback.
Improvements are tracked with their expected performance impact.

### Iterative Loop
This process repeats up to max_iterations or until the reviewer flags the code as production-ready.

### Pydantic Schemas
```bash
CodeGeneration
class CodeGeneration(BaseModel):
    code: str
    explanation: str
    language: str
    complexity: str  # low, medium, high

CodeReview
class CodeReview(BaseModel):
    functionality_score: int
    quality_score: int
    performance_score: int
    issues: list[str]
    suggestions: list[str]
    is_production_ready: bool

CodeOptimization
class CodeOptimization(BaseModel):
    optimized_code: str
    improvements_made: list[str]
    performance_impact: str
```
## Workflow Diagram

Below is a simplified diagram of the iterative LLM evaluation loop:

<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/0dd4516d-3de6-48e2-87b4-eb095981350a" />


(The diagram illustrates the cyclic flow: code generation → review → optimization → re-evaluation.)

## Requirements

Install dependencies from requirements.txt:
```bash
pip install -r requirements.txt
```

Ensure Ollama is running locally and the model qwen3:1.7b is available:
```bash
ollama pull qwen3:1.7b
```
Running the Workflow
```bash
python evaluator_optimizer_workflow.py
```
Example Output

### EVALUATOR & OPTIMIZER WORKFLOW RESULTS
============================================================
```bash
Task: Write a Python function to calculate Fibonacci numbers up to n
Initial Code:
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        print(a)
        a, b = b, a + b

Explanation: This function prints Fibonacci numbers up to n.
Language: Python
Complexity: low

Iteration 1 - REVIEW
Functionality Score: 7/10
Quality Score: 8/10
Performance Score: 7/10
Issues Found:
  - Function prints values instead of returning them
  - No input validation
Suggestions:
  - Return a list of Fibonacci numbers instead of printing
  - Add input type checking
Production Ready: No

Optimized Code:
def fibonacci(n):
    if not isinstance(n, int) or n < 0:
        raise ValueError("n must be a non-negative integer")
    seq = [0, 1]
    for _ in range(2, n):
        seq.append(seq[-1] + seq[-2])
    return seq[:n]

Improvements Made:
  - Added input validation
  - Changed print to return
Performance Impact: Minor improvement due to reduced I/O
============================================================
```
## Key Learning

This workflow demonstrates how LLM-driven evaluation loops can automatically refine outputs over multiple iterations — a foundational concept in agentic AI systems.

It simulates a self-improving code assistant, capable of generating, reviewing, and optimizing its own outputs until they reach production quality.

-----------------------------------------------------------------------------
## Reference
Based on concepts from Anthropic’s research:
“Building Effective Agents”, Anthropic, 2024.
(https://www.anthropic.com/research/building-effective-agents)



