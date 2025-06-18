
# Fragments by E2B

Fragments is an open-source platform inspired by apps like Anthropic's Claude Artifacts, Vercel v0, and GPT Engineer. It leverages the powerful E2B SDK to securely execute AI-generated code with streaming UI support and flexible stack and LLM provider integrations.

---

## Features

- Built on **Next.js 14** (App Router, Server Actions), **shadcn/ui**, **TailwindCSS**, and **Vercel AI SDK**.
- Secure code execution powered by the **E2B SDK**.
- Streaming output in the user interface.
- Supports installing and using any npm or pip packages.
- Multiple supported stacks (with ability to add your own):
  - Python interpreter
  - Next.js
  - Vue.js
  - Streamlit
  - Gradio
- Supported LLM providers (expandable):
  - OpenAI
  - Anthropic
  - Google AI
  - Mistral
  - Groq
  - Fireworks
  - Together AI
  - Ollama

---

## Getting Started

### Prerequisites

- Git
- Recent version of Node.js and npm
- E2B API Key
- LLM Provider API Key (e.g., OpenAI, Anthropic, etc.)

### Installation

1. Clone the repository:

   ```
   git clone https://github.com/e2b-dev/fragments.git
   cd fragments
   ```

2. Install dependencies:

   ```
   npm install
   ```

3. Create a `.env.local` file and add your environment variables:

   ```
   E2B_API_KEY="your-e2b-api-key"
   OPENAI_API_KEY=
   ANTHROPIC_API_KEY=
   GROQ_API_KEY=
   FIREWORKS_API_KEY=
   TOGETHER_API_KEY=
   GOOGLE_AI_API_KEY=
   GOOGLE_VERTEX_CREDENTIALS=
   MISTRAL_API_KEY=
   XAI_API_KEY=

   # Optional environment variables
   NEXT_PUBLIC_SITE_URL=
   NEXT_PUBLIC_NO_API_KEY_INPUT=
   NEXT_PUBLIC_NO_BASE_URL_INPUT=
   RATE_LIMIT_MAX_REQUESTS=
   RATE_LIMIT_WINDOW=
   KV_REST_API_URL=
   KV_REST_API_TOKEN=
   SUPABASE_URL=
   SUPABASE_ANON_KEY=
   NEXT_PUBLIC_POSTHOG_KEY=
   NEXT_PUBLIC_POSTHOG_HOST=
   ```

4. Start the development server:

   ```
   npm run dev
   ```

5. To build the app for production:

   ```
   npm run build
   ```

---

## Customization

### Adding Custom Personas (Sandbox Templates)

1. Ensure you have the [E2B CLI](https://e2b.dev/) installed and logged in.
2. Create a new folder under `sandbox-templates/`.
3. Initialize a new template:

   ```
   e2b template init
   ```

   This creates an `e2b.Dockerfile` which you can customize. For example, a Streamlit template:

   ```
   FROM python:3.19-slim
   RUN pip3 install --no-cache-dir streamlit pandas numpy matplotlib requests seaborn plotly
   WORKDIR /home/user
   COPY . /home/user
   ```

4. Define a custom start command in `e2b.toml`:

   ```
   start_cmd = "cd /home/user && streamlit run app.py"
   ```

5. Build the template:

   ```
   e2b template build --name 
   ```

6. Add your template to `lib/templates.json` with details like dependencies, entrypoint, and port.

7. Optionally, add a logo under `public/thirdparty/templates`.

---

### Adding Custom LLM Models

- Edit `lib/models.json` and add your model:

  ```
  {
    "id": "mistral-large",
    "name": "Mistral Large",
    "provider": "Ollama",
    "providerId": "ollama"
  }
  ```

---

### Adding Custom LLM Providers

- Edit `lib/models.ts` and add your provider configuration. Example for Fireworks:

  ```
  fireworks: () => createOpenAI({
    apiKey: apiKey || process.env.FIREWORKS_API_KEY,
    baseURL: baseURL || 'https://api.fireworks.ai/inference/v1'
  })(modelNameString),
  ```

- Optionally adjust the default output mode in `getDefaultMode()`.

- Add provider logos under `public/thirdparty/logos`.

---

## Contributing

Contributions are welcome! Please open issues or submit pull requests for bugs, improvements, or new features.

---

## License

This project is open-source. Please check the LICENSE file for details.

---
