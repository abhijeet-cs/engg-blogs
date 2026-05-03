🔗 Ref: https://medium.com/agoda-engineering/building-agodas-booking-form-bot-the-agentic-way-407455e50808

## 🧠Agent Workflow
1. Agent Manager
   - Receives requests from clients
   - Forwards requests to the Router Agent

2. Router Agent
   - Receives user query
   - Constructs system prompt using data science + scoring instructions
   - Sends request to OpenAI
   - Routes to appropriate response agent based on score

3. Guardrail Agent
   - Receives user query + internal allowed topics
   - Sends request to OpenAI
   - Returns label: allowed / not_allowed

4. Response Agents
   - Final agents in the chain
   - Receive user query + chat history + current booking state

