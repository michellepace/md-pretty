# md-pretty
Vibe coding experiment — A responsive markdown editor web app with live preview, version control, AI assistance, and sharing capabilities. 

This app was created combining approaches from:
- Blog Post: [My LLM codegen workflow atm](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/)
- Maven course: [AI Prototyping for Product Managers](https://maven.com/tech-for-product/ai-prototyping-for-product-managers)

## Iterate on idea to make `spec.md`

**VERSION 1** — in a Claude chat, I started with:

```
Ask me one question at a time so we can develop a thorough, step-by-step spec for this idea. Each question should build on my previous answers, and our end goal is to have a detailed specification I can hand off to a developer. Let’s do this iteratively and dig into every relevant detail. Remember, only one question at a time.

Here’s the idea:

# IDEA -  “MD Pal” web app
A markdown editor with live preview and AI editing assistance. A clean design, optimised for simplicity and user experience. Mobile-first responsive design.

## Foundational Tech Stack
* Platform: Web application
* Frontend: Next.js, TypeScript, Tailwind CSS, shadcn/UI, Lucide Icons
* Backend & Storage: Supabase for database, authentication (with Clerk via Supabase), and storage

## User Functionality
### Basic
* Homepage with ability to Sign in (sign up) with Google Account only
* User dashboard showing MD docs, with ability to create new, edit, delete
* New: Markdown editor with live preview, I can save or cancel

### Version Control
* Simple version control with the ability to compare versions. When in Markdown editor I can “save as version X” or “save” (current)

### Sharing
* Share a link to the document which renders beautifully: can download markdown document OR “Edit” where person is prompted to sign in (sign up) and the document is available now in their dashboard 

### AI Assistance
#### 1. Editing Assistance
In markdown editor view can click “Ask AI”, and prompt for document enhancements (e.g., Fix my syntax; suggest a better structure; fix grammar and spelling mistakes; write it more directly and clearly). 

I can compare my version against the AI edited version side-by-side, and click “save” or “save as version X”.

#### 2. Being your own API key
Bring your own LLM API key for AI assistance. Limited to predefined companies and models (e.g, Anthropic, API key, select model to use: where only Sonnet 3.5 or Sonnet 3.7 are allowed).
```

At the natural conclusion, Claude produced `Spec.md (version 1)`

**VERSION 2** — Manual edit to (version 1) to align to more of what I wanted.