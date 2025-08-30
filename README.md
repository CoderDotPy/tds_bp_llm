# LLM Agent POC — Browser-Based Multi-Tool Reasoning  

This repository contains a **proof-of-concept (POC)** for a **browser-based LLM-powered agent** that can reason across multiple tools.  
The agent demonstrates how modern LLMs can **loop between reasoning and tool calls**, integrating results until a task is complete.  

---

## 🚀 Features
- **Conversational LLM Agent**: Chat with an LLM in the browser.  
- **Dynamic Tool Calls** (LLM decides when to use a tool):  
  - 🔍 **Google Search API** → get snippet results.  
  - 🔗 **AI Pipe API** → flexible dataflow calls through the proxy.  
  - ⚡ **JavaScript Code Execution** → securely run JS snippets in-browser.  
- **Reasoning Loop**:  
  - Agent outputs text.  
  - If tool calls are required, it executes them and feeds results back to the LLM.  
  - Loop continues until the agent decides task is complete.  
- **Model Picker**: Users select LLM provider/model via [`bootstrap-llm-provider`](https://github.com/hwchase17/bootstrap-llm-provider).  
- **Error Handling**: Clean error messages via Bootstrap alerts.  
- **Minimal Codebase**: Simple HTML + JS, easy to hack and extend.  

---

## 🧠 Core Agent Logic  

This POC ports a **Python agent loop** into **JavaScript**:  

```python
# Python reference
def loop(llm):
    msg = [user_input()]
    while True:
        output, tool_calls = llm(msg, tools)
        print("Agent:", output)
        if tool_calls:
            msg += [handle_tool_call(tc) for tc in tool_calls]
        else:
            msg.append(user_input())
