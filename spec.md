# IDEA - “MD Pretty” web app
A markdown editor with live preview and AI editing assistance. A clean design, optimised for simplicity and user experience. Mobile-first responsive design. MD Pretty is for anyone who wants to create, manage, and share markdown documents beautifully. 

## Foundational Tech Stack
* Platform: Web application
* Frontend: Next.js, TypeScript, Tailwind CSS, shadcn/UI
* Backend & Storage: Supabase for database, authentication (with Clerk via Superbase), and storage
* Package for markdown editor with live preview: UNKNOWN (please recommend)

## User Functionality

### Core

#### Header (with authentication)
Shared across app (simple design)
* Navigation Logo with “MD Pretty”
* “Sign in” (sign up) button if user is unauthenticated
* “Dashboard” button if user is authenticated AND on homepage
* User profile icon if user is on a protected page (ie a page requiring authentication, e.g.,  Dashboard page and children).

#### Footer
Shared across app (simple design)
* One line footer with copyright information only

#### Home page
* Hero section with “See it in action” call to action with navigation to “See it in action” page
* Content: Explains product features

#### “See it in action” page
This page allows unauthenticated users to view the markdown editor and live preview, essentially the same content as the “Document page”:
* They are able to use the markdown editor with live preview.
* The “Save” button has the same authentication functionality as the “Sign in” button, upon successful authentication:
  1. The user is redirected to the protected “Document page” with the document open
  2. A model prompts the user to name the document and the markdown document is saved
  3. A toast displays “Saved”

#### Dashboard page  
User dashboard showing Markdown documents with fields: name, created (date), edited (date)
* User can toggle between List view or Card view (shows document preview).
* Clicking a list item or card item opens the document for editing
* Ability to delete a document
* Ability to share a document (link is copied and toast displays)

#### Document link sharing
User shares a document url, the recipient opens the url and sees the markdown rendered. He has the ability to:
1. “download” (as markdown file)
2. “Open in MD Pretty” (recipient has to sign-in, the document is copied into his dashboard.
3. Note: there is no collaborative editing.

#### Document page
Shows the markdown editor with live preview

On desktop: 
* side by side like a standard markdown editor with live preview.
* Sync scroll toggle

On mobile (ideally):
1. A split-screen layout with an editor at the top and preview at the bottom
2. The editor has a dark theme with light text and occupies roughly the upper half of the screen
3. The editor pane shows markdown content that can be scrolled independently
4. Below the editor is a "Preview" section with a light background that renders the formatted markdown
5. The preview section becomes visible when scrolling down the page
6. Both sections have their own scrollable areas but can be synchronized with the "Sync Scroll" feature

This design allows users to edit markdown in the fixed editor area while easily checking the rendered output by scrolling down to the preview section, with an option to synchronize scrolling between both views.​​​​​​​​​​​​​​​​

Markdown features:
* core syntax features including links, tables, code blocks
* sync scroll
* clean design (or configurable)
* Nice to have:
  * Edit/Preview buttons for mobile (like GitHub)
  * can be styled with Tailwind CSS
  * syntax highlighting
* Not required
  * Image embedding
  * Mathematical notation not required 

### Version Control
* Simple version control with the ability to compare versions. When in Markdown editor I can “save as version X” or “save” (current)

### AI Assistance
#### 1. Editing Assistance
* Assume Anthropic API and API key is securely stored and not exposed in the front end
* On the “Document page” user can click “Ask AI”, and prompt for any document enhancements (e.g., Fix my syntax; suggest a better structure; fix grammar and spelling mistakes; write it more directly and clearly). 
* I can compare my version against the AI edited version side-by-side, and click “save” or “save as version X”.

#### 2. bring your own API key
Bring your own Anthropic API key for AI assistance. Limited to predefined companies and models (e.g, Anthropic, API key, select model to use: Sonnet 3.5, Sonnet 3.7 etc.).