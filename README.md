# gpt-bridge-chrome-extension
JavaScript bridge connection point between any page and OpenAI GPTs. It provides a way to create other extensions or use BridgeGPT library to interact with GPTs.

![BridgeGPT-logo](https://github.com/maZahaca/BridgeGpt-chrome-extension/assets/1290067/a413f55d-7a27-4fa5-b2d8-8977a5750517)

## Concept
1. Any page is a **consumer** of GPT, and another page contains a page with opened Chat-GPT where questions are asked.
2. Using the JavaScript library (`BridgeGPT`) injected into any page by Chrome Extension, it can use the method `BridgeGPT.ask()` to communicate with another page with GPT.
3. For the end user provided a JavaScript accessible method `BridgeGPT.ask()`
4. Communication between tabs happens in one of the following [ways](https://twitter.com/AndrewRedUK/status/1746142202466627910).
5. When asking GPT, optionally you can define a response schema which should be followed by GPT to form a response.

Spec of **BridgeGPT**
```javascript
class BridgeGPT {
   construct (gptUrl: string, responseSchema?: Object);
   async ask<T>(question: string): Promise<T>;
}
```

Example of usage:
```javascript
const responseSchema = {
   "kpis": ["KPI 1", "KPI 2"],
};
const gpt = new BridgeGPT('https://chat.openai.com/g/g-bLDsE3HsD-goal-planner'); // or just https://chat.openai.com
const answer = gpt.ask('Grow on Twitter to 10k in 12 months');
```

Example of programmatical message in chat GPT:
```javascript
const askGPT = (input) => {
  const inputElement = document.querySelector('#prompt-textarea');
  const inputEvent = new Event('input', { bubbles: true });
  inputElement.value = \`${input}\`; // must be escaped backticks to support multiline
  inputElement.dispatchEvent(inputEvent);
      
  const btn = document.querySelector('button[data-testid="send-button"]');
  btn.focus();
  btn.disabled = false;
  btn.click();

  // How to wait for the response finalization and capture it?
};
```

## Tech
- TypeScript
- [Chrome extension template](https://github.com/chibat/chrome-extension-typescript-starter)
- GitHub Actions for CI/CD pipelines.

## Features
- injected into the page BridgeGPT allows to interact from the page with desired GPT

## Resources
- [How to programmatically interact with chat gpt](https://github.com/smol-ai/GodMode/blob/8ac3ffde96ab72d992b5d5cf1743673e610cb07b/src/providers/openai.js#L13)
