# � Aythena AI - Advanced Browser-Based AI Assistant

**Live Demo:** [https://athena-ai-weld.vercel.app/](https://athena-ai-weld.vercel.app/)

A sophisticated, browser-based AI assistant that combines intelligent conversation with powerful tool integration. Built with vanilla JavaScript and modern web technologies, Athena AI provides a seamless chat experience with real-time capabilities and extensive customization options.

## ✨ Features

### 🤖 Intelligent Agent System
- **Multi-turn conversations** with context awareness
- **Tool integration** for enhanced capabilities
- **Agent loop** that continues working until tasks are complete
- **OpenAI-compatible function calling** for tool execution

### 🌐 Multi-Provider AI Support
- **AI Pipe Proxy** - Access multiple models through one API
- **OpenAI GPT** - GPT-3.5, GPT-4, and latest models
- **Google Gemini** - Gemini Pro and advanced models
- **Anthropic Claude** - Claude 3 and family
- **Dynamic model switching** without page reload

### 🛠️ Integrated Tools
- **Web Search** - Real-time information retrieval
- **Code Execution** - Safe JavaScript sandbox
- **File Processing** - Analyze uploaded documents
- **Data Visualization** - Create charts and graphs

### 💎 Modern Interface
- **Responsive design** that works on all devices
- **Dark/light theme** with system preference detection
- **Conversation management** with persistent history
- **Voice input/output** support
- **File drag & drop** for easy uploads
- **Real-time typing indicators**

### ⚙️ Advanced Configuration
- **Comprehensive settings** for all aspects
- **Export/import** configuration
- **Performance monitoring** with real-time metrics
- **Accessibility features** and keyboard shortcuts

## 🚀 Quick Start

### Prerequisites
- Modern web browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- API key from one of the supported providers

### Installation
1. **Clone the repository**
   ```bash
   git clone https://github.com/AchalStark/Athena-AI
   cd Athena-AI
   ```

2. **Open in browser**
   ```bash
   # Simply open index.html in your browser
   # No build process or server required!
   open index.html
   ```

3. **Configure your API**
   - Click the settings gear icon (⚙️)
   - Select your preferred AI provider
   - Enter your API key
   - Choose your model
   - Start chatting!

## 🏗️ Architecture

### Core Components

**Agent Engine** (`agent.js`)
- Manages conversation state and message flow
- Handles multi-provider API integration
- Executes tool calls and processes responses
- Implements the agent reasoning loop

**User Interface** (`index.html`)
- Modern, responsive chat interface
- Comprehensive settings modal
- File upload and drag-drop support
- Voice input/output controls

**Styling** (`styles.css`)
- CSS custom properties for theming
- Responsive grid layout
- Smooth animations and transitions
- Accessibility-compliant design

### Agent Loop Flow

```javascript
async function agentLoop(conversationId) {
  while (maxTurns-- > 0) {
    // 1. Send conversation to LLM
    const response = await callLLM(conversation);
    
    // 2. Display AI response
    addMessage('assistant', response.content);
    
    // 3. Check for tool calls
    if (response.tool_calls) {
      // 4. Execute tools
      const results = await executeTools(response.tool_calls);
      
      // 5. Add tool results to conversation
      addToolResults(results);
      
      // 6. Continue loop for AI to process results
    } else {
      // 7. No tools needed, conversation complete
      break;
    }
  }
}
```

### Tool System

Tools are defined with OpenAI-compatible schemas:

```javascript
{
  type: "function",
  function: {
    name: "web_search",
    description: "Search the web for current information",
    parameters: {
      type: "object",
      properties: {
        query: { type: "string" },
        results: { type: "integer", default: 5 }
      },
      required: ["query"]
    }
  }
}
```

## 🔧 Configuration

### API Providers

| Provider | Endpoint | Models | Features |
|----------|----------|--------|----------|
| AI Pipe | `aipipe.org/openrouter/v1/` | 50+ models | Proxy, cost-effective |
| OpenAI | `api.openai.com/v1/` | GPT-3.5, GPT-4 | Function calling, streaming |
| Google | `generativelanguage.googleapis.com/` | Gemini Pro | Multimodal, fast |
| Anthropic | Direct API | Claude 3 | Long context, reasoning |

### Settings Categories

**API Configuration**
- Provider selection and API keys
- Model selection and parameters
- Token limits and temperature control

**Interface Preferences**
- Theme selection (auto/light/dark)
- Animation and sound settings
- Font size and accessibility options

**Voice Features**
- Speech recognition for input
- Text-to-speech for responses
- Language and rate configuration

**Advanced Options**
- Conversation history limits
- Auto-save preferences
- Performance monitoring
- Data management

## � Usnage Examples

### Research Assistant
```
User: "Research the latest developments in quantum computing and summarize the key breakthroughs"

Athena: [Searches web] → [Analyzes results] → [Provides comprehensive summary with sources]
```

### Code Development
```
User: "Create a function to calculate fibonacci numbers and test it"

Athena: [Writes JavaScript code] → [Executes in sandbox] → [Shows results and explains]
```

### Data Analysis
```
User: "Analyze this CSV file and create a visualization"

Athena: [Processes uploaded file] → [Analyzes data] → [Creates chart] → [Explains insights]
```

### Creative Writing
```
User: "Help me write a short story about AI"

Athena: [Asks clarifying questions] → [Develops plot] → [Writes story] → [Refines based on feedback]
```

## 🛠️ Development

### Project Structure
```
├── index.html          # Main application interface
├── agent.js           # Core AI agent and tool system
├── styles.css         # Modern CSS with custom properties
├── LICENSE           # MIT license
└── README.md         # This documentation
```

### Key Classes and Functions

**AthenaAI Class**
- Main application controller
- Manages state, UI, and API interactions
- Handles conversation flow and tool execution

**Core Methods**
- `sendMessage()` - Processes user input
- `agentLoop()` - Manages AI reasoning cycle
- `callLLM()` - Handles API communication
- `executeTool()` - Runs tool functions

### Adding Custom Tools

```javascript
// 1. Define tool schema
const customTool = {
  type: "function",
  function: {
    name: "my_custom_tool",
    description: "Description of what the tool does",
    parameters: {
      type: "object",
      properties: {
        param1: { type: "string", description: "Parameter description" }
      },
      required: ["param1"]
    }
  }
};

// 2. Add to tools array
this.tools.push(customTool);

// 3. Implement execution logic
async executeMyCustomTool({ param1 }) {
  // Your tool logic here
  return { result: "Tool output" };
}

// 4. Add to executeTool switch statement
case 'my_custom_tool': 
  return await this.executeMyCustomTool(args);
```

### Extending API Providers

```javascript
// Add new provider in callLLM method
case 'my_provider':
  apiUrl = 'https://api.myprovider.com/v1/chat';
  headers.Authorization = `Bearer ${apiKey}`;
  body = {
    model,
    messages: messagesForApi,
    max_tokens: maxTokens,
    temperature
  };
  break;
```

## 🎨 Customization

### Theming
The application uses CSS custom properties for easy theming:

```css
:root {
  --primary: #6366f1;
  --background: #ffffff;
  --text-primary: #0f172a;
  /* ... more variables */
}

[data-theme="dark"] {
  --background: #0f172a;
  --text-primary: #f8fafc;
  /* ... dark theme overrides */
}
```

### UI Components
All UI components are built with vanilla JavaScript and can be easily customized:

- Message bubbles with markdown support
- Settings modal with tabbed interface
- Toast notifications for feedback
- Context menus for message actions

## 📱 Mobile Support

- **Responsive design** that adapts to all screen sizes
- **Touch-friendly** interface with appropriate tap targets
- **Mobile-optimized** sidebar that slides in/out
- **Voice input** support on mobile browsers
- **File upload** via camera or gallery

## 🔒 Security & Privacy

- **Client-side only** - no data sent to third parties except chosen AI provider
- **API keys** stored locally in browser storage
- **Sandboxed code execution** for safety
- **No tracking** or analytics by default
- **HTTPS required** for voice features

## 🚀 Performance

- **Lazy loading** of components and features
- **Memory monitoring** with automatic cleanup
- **Response caching** for repeated queries
- **Optimized rendering** with virtual scrolling
- **Bundle size**: ~50KB minified

## 🧪 Testing

The application includes built-in testing capabilities:

- **Demo mode** works without API keys
- **Tool simulation** for development
- **Error handling** with graceful degradation
- **Performance metrics** displayed in real-time


## 📊 Browser Compatibility

| Browser | Version | Status |
|---------|---------|--------|
| Chrome | 90+ | ✅ Full support |
| Firefox | 88+ | ✅ Full support |
| Safari | 14+ | ✅ Full support |
| Edge | 90+ | ✅ Full support |
| Mobile Safari | 14+ | ✅ Full support |
| Chrome Mobile | 90+ | ✅ Full support |

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
