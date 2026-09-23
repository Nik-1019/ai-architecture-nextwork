# AI Question Answering Service

## Architecture

```mermaid
C4Container
    title C4 Level 2 - AI Question Answering Service

    Person(user, "User", "Sends questions via HTTP")

    Container_Boundary(system, "AI Question Answering Service") {
        Container(api, "API Container", "FastAPI", "Receives HTTP requests and returns responses")
        Container(orchestrator, "Prompt Orchestrator", "Python module", "Builds prompts from user input and system context")
        Container(provider, "Model Provider", "Python module", "Sends prompts to the LLM and returns generated text")
    }

    System_Ext(gemini, "Google Gemini API", "External LLM service")

    Rel(user, api, "POST /ask", "HTTPS")
    Rel(api, orchestrator, "Passes user question")
    Rel(orchestrator, provider, "Sends formatted prompt")
    Rel(provider, gemini, "generate_content()", "HTTPS")
```
