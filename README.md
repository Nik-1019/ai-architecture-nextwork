# AI Question Answering Service

## Architecture

```mermaid
%%{init: {"c4": {"c4ShapeMargin": 110, "c4ShapeInRow": 3}}}%%
C4Container
    title C4 Level 2 - AI Question Answering Service

    Person(user, "User", "Sends questions via HTTP")
    System_Ext(gemini, "Google Gemini API", "External LLM service")

    System_Boundary(system, "AI Question Answering Service") {
        Container(api, "API Container", "FastAPI", "Receives HTTP requests and returns responses")
        Container(orchestrator, "Prompt Orchestrator", "Python module", "Builds prompts from user input and system context")
        Container(provider, "Model Provider", "Python module", "Sends prompts to the LLM and returns generated text")
    }

    Rel(user, api, "POST /ask", "HTTPS")
    Rel(api, orchestrator, "User question")
    Rel(orchestrator, provider, "LLM prompt")
    Rel(provider, gemini, "generate_content()", "HTTPS")

    UpdateRelStyle(user, api, $offsetX="-45", $offsetY="-30")
    UpdateRelStyle(api, orchestrator, $offsetX="-40", $offsetY="-10")
    UpdateRelStyle(orchestrator, provider, $offsetX="-35", $offsetY="-10")
    UpdateRelStyle(provider, gemini, $offsetX="10")
```
