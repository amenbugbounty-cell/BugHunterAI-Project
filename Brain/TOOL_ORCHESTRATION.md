# TOOL_ORCHESTRATION.md

## Tool Orchestration: Harmonizing External Security Tools

The Tool Orchestration component of BugHunterAI is responsible for the intelligent selection, configuration, execution, and output processing of a diverse array of external security tools. It transforms a collection of disparate utilities into a cohesive, automated arsenal, ensuring that the right tool is applied at the right time with optimal parameters, and that its results are seamlessly integrated into the overall research process.

### Purpose

The primary purpose of Tool Orchestration is to:

1.  **Standardize Tool Interaction**: Provide a unified interface for invoking any external tool, abstracting away tool-specific command-line arguments, input formats, and output parsing.
2.  **Optimize Tool Usage**: Select the most appropriate tool(s) for a given task based on context, target characteristics, and historical performance data.
3.  **Manage Tool Dependencies**: Ensure that all prerequisites (e.g., environment variables, configuration files, upstream data) for a tool's execution are met.
4.  **Automate Output Processing**: Parse raw tool outputs into structured, machine-readable formats that can be consumed by other agents (e.g., Reasoning Engine, Memory System).
5.  **Implement Resilience**: Handle tool failures, timeouts, and unexpected behaviors gracefully, including retries and fallback mechanisms.
6.  **Maintain Tool Inventory**: Keep an up-to-date catalog of available tools, their capabilities, limitations, and usage guidelines.

### Architecture

The Tool Orchestration system is built around a flexible, adapter-based architecture:

-   **Tool Registry**: A centralized database or configuration store containing metadata for each integrated tool:
    -   `tool_name`: Unique identifier (e.g., `subfinder`, `nuclei`, `httpx`).
    -   `description`: Brief explanation of the tool's function.
    -   `capabilities`: What the tool can achieve (e.g., `subdomain_enumeration`, `port_scanning`, `vulnerability_scanning`).
    -   `input_schema`: Expected input parameters and their types.
    -   `output_schema`: Structure of the tool's output.
    -   `command_template`: Template for generating the shell command or API call.
    -   `parser_script`: Script or module responsible for parsing raw output.
    -   `performance_metrics`: Historical data on execution time, success rate, and resource consumption.
    -   `dependencies`: External libraries or other tools required.

-   **Tool Selector**: A module that, given a task and context, queries the Tool Registry to identify the most suitable tool(s) based on capabilities, efficiency, and past success rates.

-   **Tool Adapters**: Each tool has a dedicated adapter responsible for:
    -   **Command Generation**: Translating generic task parameters into specific command-line arguments or API request bodies.
    -   **Execution Wrapper**: Invoking the tool (typically via the Execution Engine's Terminal Automation Module) and capturing its raw output.
    -   **Output Parser**: Transforming the raw, often unstructured, output into a standardized `Observation` object according to the `output_schema`.
    -   **Error Translator**: Mapping tool-specific error codes or messages into a common error format for the Execution Engine.

-   **Input/Output Validators**: Ensure that inputs provided to tools and outputs received from them conform to their defined schemas, preventing malformed data from propagating through the system.

### Orchestration Flow

1.  **Task Reception**: The Tool Orchestration receives a `ToolInvocationTask` from the Execution Engine, specifying the desired capability (e.g., `enumerate_subdomains`) and target information.

2.  **Tool Selection**: The Tool Selector consults the Tool Registry and, potentially, the Knowledge System (for best practices) to choose the optimal tool (e.g., `subfinder` or `amass`).

3.  **Parameter Generation**: The selected Tool Adapter generates the precise command-line arguments or API request parameters based on the task's input and the tool's `command_template`.

4.  **Execution**: The generated command is passed to the Execution Engine for actual invocation. The Execution Engine handles the process management, resource allocation, and raw output capture.

5.  **Output Parsing**: Once the Execution Engine returns the raw output, the Tool Adapter's `parser_script` processes it, extracting relevant data points and structuring them into an `Observation` object.

6.  **Observation Transmission**: The structured `Observation` is then sent back to the Execution Engine, which in turn forwards it to the Memory System and Reasoning Engine for further analysis and storage.

### Resilience and Optimization

-   **Dynamic Tool Selection**: If a preferred tool consistently fails or performs poorly, the Tool Selector can dynamically switch to alternative tools with similar capabilities.
-   **Rate Limiting and Throttling**: Integrates with the Resource Manager to ensure tools do not overwhelm target systems or exceed API rate limits.
-   **Caching**: Caches frequently accessed tool outputs or intermediate results to reduce redundant executions.
-   **Tool Health Monitoring**: Continuously monitors the operational status and performance of integrated tools, flagging any issues to the Self-Improvement Engine.

### Integration with Other Components

-   **Execution Engine**: The primary consumer and provider of execution context for Tool Orchestration.
-   **Memory System**: Stores tool outputs, performance metrics, and configuration details.
-   **Knowledge System**: Provides tool documentation, usage guidelines, and vulnerability patterns that inform tool selection and configuration.
-   **Planning Engine**: Receives high-level capabilities requests and uses tool performance data for more accurate planning.
-   **Self-Improvement Engine**: Learns from tool successes and failures to refine tool selection algorithms and adapter logic.

By centralizing and intelligently managing external tools, the Tool Orchestration component ensures that BugHunterAI can leverage the vast ecosystem of security utilities effectively, consistently delivering high-quality, actionable results while minimizing operational overhead.
