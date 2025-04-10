# Simplified version(s) for `spec.md`

The below options are more aligned to the examples seen on Bolt, Replit, etc., as they are simplier and more concise. At the heart of it, the app is this: ***A modern markdown editor with real-time preview, version history, AI-powered enhancements, and seamless sharing.***

Below are the responses of asking for a simplification on `spec.md`. As I am just concentrating on a prototype first, I think I'll use [Option 3: UI/UX only](#option-3-uiux-only) and hope that Bolt/Replit doesn't use up my credits for building the database, authentication, etc.

## Grok3

### Option 1: initial
```
Create a modern web app, MD Pretty, a clean markdown editor with live preview and AI vibes. Keep it minimal, mobile-friendly. Features: markdown editing with live preview, simple document saving, ‘Ask AI’ button (Anthropic API, user’s key). Use Next.js and a DB like Supabase, but riff if something cooler fits. Surprise me with vibe’y twists!
```

### Option 2: (force word count)
```
# MD Pretty Web App

## Purpose
Develop a web application, MD Pretty, designed as a clean, user-friendly markdown editor with live preview and AI assistance. The intent is to offer a straightforward tool for creating, managing, and enhancing markdown documents in an intuitive interface. The app must prioritize simplicity, usability, and mobile responsiveness, ensuring a seamless experience across devices.

## Core Features

### Markdown Editor
- Implement a markdown editor with real-time live preview.
- Support standard markdown syntax (incl. code blocks, links)
- Provide a minimal, distraction-free design for focused editing

### Document Dashboard
A dashboard to manage all documents
- Options to create, edit, delete, rename and share documents
- Meta data for each document (e.g., created, last modified)
- Store documents securely, tied to the user’s account.

### AI Assistance
- Add an "Ask AI" button on the editor page for user-initiated help.
- Process:
  1. User clicks "Ask AI" and enters a prompt (e.g., "Improve my structure").
  2. Send the current markdown content and prompt to the Anthropic API (user provides their API key).
  3. Display the original and AI-edited versions side-by-side.
  4. Allow users to save the AI-edited version as the current document.
- Include a simple interface to input and store the user’s API key.

### Mobile Responsiveness
- Ensure the app adapts to mobile devices:
  - Use a tabbed interface (e.g., "Edit" and "Preview" tabs) on smaller screens.
  - Maintain usability with touch-friendly controls and readable text.

## Technical Requirements
- Build as a web app using Next.js for the frontend.
- Use a database (e.g., Supabase) to store users, documents, and API keys.
- Integrate Clerk for user authentication (sign-up, sign-in flows).
- Leverage existing libraries (e.g., react-markdown) for markdown rendering, but suggest alternatives if more efficient.

## Additional Guidance
- Focus on a clean, professional aesthetic with intuitive navigation.
- Optimize for performance, especially on mobile devices.
- Propose creative enhancements (e.g., UI layouts, feature tweaks) that align with the app’s purpose, justifying your choices.

Start with this foundation and deliver a functional prototype, prioritizing usability and core functionality.
```

### Option 3: UI/UX only

(ThinkMode): *You provided an option which is similar to the below. As I am concentrating on building a working prototype first in a vibe coding tool, I don’t want the AI to yet worry about any technical requirements. Hence I have left these details out as it will “self determine” this. I have left out specifications about the UI itself so that the AI will use creativity. **Q1.** Considering my original spec, is this description well aligned? **Q.2** Can you please improve it?*

> *MD Pretty—a clean markdown editor with live preview and AI vibes. Keep it minimal, mobile-friendly. Features: markdown editing with live preview, ‘Ask AI’ button (which previews  a re-write of the document for replacement), easy share (a public link to the rendered document with ability to download markdown file), version control, and document dashboard.*

Response:
```
MD Pretty: A mobile-responsive markdown editor with live preview and user-initiated AI assistance. Features include:
- Markdown editing with real-time preview
- A dashboard to manage saved documents
- Simple version control to save and compare document versions
- Sharing via public links to view rendered documents and download markdown files
- An 'Ask AI' button where users can input a prompt to receive a rewritten version of the document, which they can preview and optionally replace the current content with
```

## Sonnet 3.7

### Option 4
```
# MD Pretty - Initial Specification

## Project Vision
MD Pretty is a web application that provides a clean, intuitive markdown editor with live preview and AI editing assistance. The application combines simplicity with powerful features for technical writers who want to create, manage, and share markdown documents. At its core, MD Pretty solves the problem of having markdown documents scattered across different platforms by providing a central repository with editing, versioning, and sharing capabilities.

I'm looking to build something that feels delightful to use - clean design with thoughtful interactions that make writing markdown enjoyable rather than just functional.

## Target Users & Key Use Cases
- **Technical writers** creating documentation who need a simple, dedicated solution
- **Product managers** drafting PRDs who want to improve documents with AI assistance
- **Content creators** who use markdown regularly and need version history to track document evolution
- **Professionals** who want to share beautifully rendered markdown documents with colleagues

## Core Technical Stack
- **Frontend**: Next.js with TypeScript, Tailwind CSS for styling, shadcn/UI for components
- **Backend**: Supabase for database and storage
- **Authentication**: Google Sign-in only (via Clerk integrated with Supabase)
- **Markdown**: react-markdown combined with @uiw/react-md-editor or equivalent
- **AI Integration**: Support for Anthropic's Claude models (bring your own API key)

## Key Features

### 1. Markdown Editor with Live Preview
A clean, responsive editor with side-by-side editing and preview on desktop, and a tabbed interface on mobile. Support for core markdown features including headings, lists, links, tables, and code blocks with syntax highlighting.

### 2. Document Management & Dashboard
A simple dashboard showing user's documents with creation and last edited dates. Each document can be opened for editing, shared via link, or deleted. New documents can be created from the dashboard.

### 3. Version History
The ability to save named versions of documents and compare different versions side-by-side. Users can view version history, compare versions, and copy content from previous versions into the current document.

### 4. Document Sharing
Generate shareable links that allow recipients to view beautifully rendered markdown, download as a markdown file, or open a copy in their own MD Pretty account.

### 5. AI Assistance
Request AI help with document improvements via user-initiated prompts. AI can suggest enhancements to structure, grammar, clarity, or other aspects based on user requests. Users can review AI suggestions side-by-side with their original and choose what to incorporate.

## Initial Implementation Approach
Let's start with the core editing experience and build out from there:

1. Create a beautiful, responsive markdown editor with live preview
2. Implement basic document saving and management
3. Add user authentication to enable personal document storage
4. Develop version history comparison capability 
5. Add document sharing functionality

For the first iteration, focus on making the core writing experience exceptional before expanding to additional features.

## Creative Direction
I've outlined the core features I need, but I'm actively seeking your creative input on implementation. Please suggest UI patterns, interactions, animations, or approaches that could make this app feel special and delightful to use.

Some areas where I'd especially value your creativity:
- How to make the editor feel responsive and pleasant to type in
- Thoughtful transitions between views
- Elegant ways to present version history
- Making the AI assistance feel seamlessly integrated
- Any "surprise and delight" features that could elevate the experience

The primary goal is to create an application that makes markdown editing feel joyful rather than utilitarian, while keeping the interface clean and intuitive.
```

### Option 5
```
# MD Pretty - Streamlined Specification

## Project Overview
MD Pretty is a clean, user-friendly markdown editor web application with live preview and AI editing assistance. Designed with a mobile-first responsive approach, MD Pretty prioritizes simplicity and excellent user experience. The target users are anyone who wants to create, manage, and share markdown documents beautifully.

I'm seeking your creative input on implementation while adhering to the core functionality and technology constraints.

## Technology Stack
- **Platform**: Web application
- **Frontend**: 
  - Next.js
  - TypeScript
  - Tailwind CSS 
  - shadcn/UI components
  - Recommended: react-markdown and @uiw/react-md-editor
- **Backend & Storage**: 
  - Supabase for database and storage
  - Authentication via Clerk integrated with Supabase

## Core Structure

### Main Pages
1. **Home Page**
   - Public landing page with feature highlights
   - "See it in action" demo access

2. **Dashboard Page** (authenticated)
   - Document management interface
   - Toggle between list and card views
   - Document actions (open, share, delete)

3. **Document Page** (authenticated)
   - Markdown editor with live preview
   - Document actions (save, version, share)

### Basic Components
- **Header**: Logo, authentication/navigation buttons, user profile
- **Footer**: Minimal with copyright information

## Key Functionality

### 1. Markdown Editor/Preview
- Clean, responsive interface
- Side-by-side editing and preview on desktop
- Tab-based switching between edit/preview on mobile
- Support for core markdown syntax
- Sync scroll option (toggleable)

### 2. Document Management
- Create, save, and delete documents
- Simple version history with comparison view
- Document sharing via links

### 3. AI Assistance
- User-prompted markdown enhancement
- Compare original and AI-edited versions
- "Bring your own API key" for Anthropic models
- Save AI suggestions as current version or new version

## Data Concepts
Key entities to store:
- Users (from Clerk authentication)
- Documents (with user ownership)
- Document versions (with content and metadata)
- Shared documents
- API keys (for AI assistance)

## Implementation Considerations
Priority features in approximate order:
1. Core markdown editor and preview
2. Basic document management
3. User authentication
4. Document sharing
5. Version comparison
6. AI assistance

Feel free to suggest creative approaches to these features and alternative user experiences that might better achieve the application's goals while maintaining simplicity and usability.
```