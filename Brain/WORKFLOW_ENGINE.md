# WORKFLOW_ENGINE.md

## Workflow Engine: Automating Complex Security Processes

The Workflow Engine is the component within BugHunterAI responsible for defining, executing, and managing sequences of interconnected tasks, known as workflows. It enables the automation of complex security research processes, from initial reconnaissance to vulnerability validation, by orchestrating the interaction between various agents and tools. This engine ensures consistency, repeatability, and efficiency in how BugHunterAI approaches different bug bounty scenarios.

### Purpose

The primary purpose of the Workflow Engine is to:

1.  **Define Reusable Processes**: Create standardized, repeatable sequences of actions for common security research tasks (e.g., "Subdomain Enumeration Workflow", "XSS Testing Workflow").
2.  **Orchestrate Task Sequences**: Manage the flow of execution between individual tasks, ensuring dependencies are met and actions are performed in the correct order.
3.  **Automate Decision Points**: Incorporate conditional logic to adapt workflow execution based on intermediate results or observed data.
4.  **Handle Workflow State**: Track the progress of ongoing workflows, allowing for pausing, resuming, and auditing.
5.  **Integrate Agents and Tools**: Seamlessly combine the capabilities of different specialized agents (Recon, Browser, Analysis) and external tools into coherent processes.
6.  **Provide Transparency**: Log all workflow steps, decisions, and outcomes for review, debugging, and continuous improvement.

### Architecture

The Workflow Engine is designed to be declarative and flexible, often utilizing a domain-specific language (DSL) or a visual editor for workflow definition, and a robust execution runtime:

-   **Workflow Definition Language (WDL)**: A declarative language (e.g., YAML, JSON, or a custom DSL) used to describe workflows, including:
    -   `workflow_id`: Unique identifier.
    -   `name`, `description`.
    -   `input_schema`: Expected inputs to start the workflow.
    -   `output_schema`: Expected outputs upon completion.
    -   `steps`: A sequence of tasks or sub-workflows.
    -   `conditions`: Logic for branching or looping.
    -   `error_handlers`: Strategies for dealing with task failures within the workflow.

-   **Workflow Repository**: A centralized store for all defined workflows, accessible by the Planning Engine and other components.

-   **Workflow Orchestrator**: The runtime component responsible for:
    -   **Parsing and Validation**: Loading and validating workflow definitions.
    -   **State Management**: Tracking the current step, status, and context of each running workflow instance.
    -   **Task Dispatcher**: Sending individual tasks to the Execution Engine based on the workflow logic.
    -   **Event Listener**: Monitoring `Observation` objects from the Memory System to react to task completions or new evidence.
    -   **Concurrency Manager**: Handling parallel execution of independent workflow branches.

-   **Workflow Templates**: Pre-defined, parameterized workflows for common scenarios, promoting reusability and best practices.

### Workflow Execution Flow

1.  **Workflow Initiation**: The Planning Engine (or a user) initiates a workflow by providing the `workflow_id` and necessary inputs.

2.  **Workflow Loading**: The Workflow Orchestrator loads the workflow definition from the Workflow Repository and validates its structure.

3.  **Step-by-Step Execution**: The Orchestrator processes the workflow steps sequentially or in parallel, based on the defined logic:
    -   For each step, it generates a `Task` object for the Execution Engine (or another agent).
    -   It waits for the `Observation` (result) of the task from the Memory System.
    -   It evaluates any `conditions` to determine the next step (e.g., if subdomains found, proceed to port scan; else, end recon).

4.  **Data Flow**: Outputs from one task are automatically passed as inputs to subsequent tasks within the workflow, ensuring a continuous data pipeline.

5.  **Error Handling**: If a task fails, the Workflow Engine consults its `error_handlers` to decide whether to retry, skip, or terminate the workflow.

6.  **Workflow Completion**: Once all steps are executed, the workflow generates a final `WorkflowResult` object, summarizing its outcome and key findings, which is stored in the Memory System.

### Example: Subdomain to Vulnerability Workflow

1.  **Start**: `Target Domain` (e.g., `example.com`)
2.  **Step 1: Subdomain Enumeration**:
    -   **Task**: `ExecutionEngine.run_tool(tool='subfinder', target=input.domain)`
    -   **Condition**: If `subdomains_found > 0`, proceed to Step 2.
    -   **Else**: End workflow (no subdomains).
3.  **Step 2: Alive Host Check**:
    -   **Task**: `ExecutionEngine.run_tool(tool='httpx', targets=output_from_step1.subdomains)`
    -   **Condition**: If `alive_hosts > 0`, proceed to Step 3.
    -   **Else**: End workflow.
4.  **Step 3: Port Scanning (Top Ports)**:
    -   **Task**: `ExecutionEngine.run_tool(tool='nmap', targets=output_from_step2.alive_hosts, ports='top100')`
    -   **Output**: Open ports.
5.  **Step 4: Vulnerability Scanning (Nuclei)**:
    -   **Task**: `ExecutionEngine.run_tool(tool='nuclei', targets=output_from_step2.alive_hosts, templates='critical')`
    -   **Output**: Potential vulnerabilities.
6.  **Step 5: Report Generation**:
    -   **Task**: `ReportingEngine.generate_report(findings=output_from_step4.vulnerabilities)`
7.  **End**: Workflow completed.

### Integration with Other Components

-   **Planning Engine**: Initiates workflows and receives high-level status updates.
-   **Execution Engine**: Executes individual tasks within a workflow.
-   **Memory System**: Stores workflow definitions, state, and all intermediate/final results.
-   **Knowledge System**: Provides workflow templates and best practices for designing effective workflows.
-   **Reasoning Engine**: Can analyze workflow results to identify patterns or suggest improvements.
-   **Self-Improvement Engine**: Learns from workflow successes and failures to optimize workflow definitions and execution strategies.

By providing a structured approach to automating complex security tasks, the Workflow Engine significantly enhances BugHunterAI's efficiency, consistency, and ability to tackle diverse bug bounty challenges at scale.
