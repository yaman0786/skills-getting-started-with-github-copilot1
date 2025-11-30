# GitHub Copilot Instructions

## Project: J.A.R.V.I.S Clone - AI Assistant iOS Application

You are a Senior iOS Engineer and Software Architect. When generating code for this project, follow these guidelines:

### Project Overview
- **Project Name**: J.A.R.V.I.S Clone
- **Architecture**: MVVM (Model-View-ViewModel)
- **Language**: Swift 5+ with async/await concurrency
- **Framework**: SwiftUI (native iOS frameworks only)

### Core Features & Requirements

#### 1. The Brain (OpenAI API)
- Integrate OpenAI API using the GPT-4o model
- Implement Function Calling (Tool Use) capability
- The AI must intelligently decide when to use tools based on user queries
  - Use search for real-time data queries (e.g., "What is the weather in Istanbul?")
  - Do not use search for conversational queries (e.g., "Tell me a joke")
- System Prompt: "You are a helpful, witty Turkish-speaking assistant. Use the 'search_internet' tool for real-time data."

#### 2. Live Data (Serper.dev API)
- Create a `searchGoogle(query: String)` function using the Serper.dev API
- This function should be called via the OpenAI "Tool Call" mechanism
- Parse JSON responses to extract organic search snippets

#### 3. Hearing (Speech-to-Text)
- Use `SFSpeechRecognizer` for real-time audio-to-text conversion
- Handle all required permissions (`SFSpeechRecognizer`, `AVAudioSession`)
- Implement a "Listen" button that toggles recording state

#### 4. Speaking (Text-to-Speech)
- Use `AVSpeechSynthesizer` to vocalize AI responses
- Configure audio session correctly (`.playback` mode) for adequate volume

#### 5. User Interface (UI)
- Create a futuristic, dark-themed UI (Cyberpunk style)
- Use dark background color: `Color(hex: "0f0f12")`
- Use Cyan/Blue accent colors
- Display scrolling chat history with distinct bubbles for User and Assistant
- Add pulsing animation to the Microphone button when listening
- Show status text indicators: "Listening...", "Thinking...", "Speaking..."

### Code Structure

```
├── Config.swift           // API Keys configuration struct
├── AIService.swift        // Network logic (OpenAI + Serper)
├── AssistantViewModel.swift  // @MainActor - Speech, Audio, UI State
└── ContentView.swift      // SwiftUI UI components
```

### Coding Standards

#### Error Handling
- Code must be robust and handle all errors gracefully
- Never crash on network failures
- Provide user-friendly error messages

#### Networking
- Use native `URLSession` for all network requests
- Do not use external libraries - only native iOS frameworks
- Implement proper async/await patterns

#### Documentation
- Write clear comments explaining complex logic
- Especially document the Function Calling mechanism
- Use Swift documentation comments (`///`) for public APIs

#### SwiftUI Best Practices
- Use `@MainActor` for view models
- Implement proper state management with `@StateObject`, `@Published`
- Follow SwiftUI lifecycle conventions

### API Integration Notes

#### OpenAI API Structure
```swift
// Function definition for tool calling
let searchFunction = [
    "type": "function",
    "function": [
        "name": "search_internet",
        "description": "Search the internet for real-time information",
        "parameters": [
            "type": "object",
            "properties": [
                "query": [
                    "type": "string",
                    "description": "The search query"
                ]
            ],
            "required": ["query"]
        ]
    ]
]
```

#### Serper.dev API
- Endpoint: `https://google.serper.dev/search`
- Method: POST with JSON body
- Headers: `X-API-KEY`, `Content-Type: application/json`

### UI Color Palette
- Background: `#0f0f12`
- Primary Accent: Cyan (`#00FFFF`)
- Secondary Accent: Blue (`#0080FF`)
- User Message: Dark blue tint
- Assistant Message: Dark cyan tint
- Text: White/Light gray
