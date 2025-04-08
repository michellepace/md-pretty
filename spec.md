# MD Pretty - Technical Specification

## Table of Contents

- [Project Overview](#project-overview)
- [Technology Stack](#technology-stack)
- [UI & Experience](#ui--experience)
  - [1. Header/Footer](#1-headerfooter)
  - [2. Home Page](#2-home-page)
  - [3. Dashboard Page](#3-dashboard-page)
  - [4. Document Page](#4-document-page)
    - [Markdown Editor](#markdown-editor)
    - [Document Management](#document-management)
- [Core Functionality](#core-functionality)
  - [1. Markdown Editor/Preview](#1-markdown-editorpreview)
  - [2. Document Link Sharing](#2-document-link-sharing)
  - [3. Document Version Modal (version control)](#3-document-version-modal-version-control)
  - [4. AI Assistance](#4-ai-assistance)
- [Technical Implementation](#technical-implementation)
  - [Authentication](#authentication)
  - [Database Schema](#database-schema)
  - [Error Handling](#error-handling)
- [Implementation Priorities](#implementation-priorities)
- [Future Considerations](#future-considerations)

## Project Overview

MD Pretty is a web application that provides a clean, user-friendly markdown editor with live preview and AI editing assistance. The application is designed with a mobile-first responsive approach, prioritising simplicity and user experience. MD Pretty targets anyone who wants to create, manage, and share markdown documents in a beautiful interface.

## Technology Stack

- **Platform**: Web application
- **Frontend**: 
  - Next.js
  - TypeScript
  - Tailwind CSS 
  - shadcn/UI for components
  - react-markdown and @uiw/react-md-editor for the core markdown editing functionality
- **Backend & Storage**: 
  - Supabase for database
  - Authentication via Clerk integrated with Supabase
  - Supabase for document storage

## UI & Experience

### 1. Header/Footer
Simple, clean design shared across the application
- Header:
  - Navigation logo with "MD Pretty" text
  - "Sign in" (sign up) button for unauthenticated users
  - "Dashboard" button if user is authenticated AND on [Home Page](#2-home-page)
  - User profile icon if user is on a protected page (requires authentication)
- Footer
  - Minimalist design shared across the application
  - Contains only copyright information in a single line

### 2. Home Page
- Hero section with prominent "See it in action" call-to-action button
- Content explaining the product features in a clear, concise manner
- Clean, visually appealing layout

### 3. Dashboard Page
Requires user authentication, all children pages are also protected.
- Displays user's markdown documents with fields:
  - Document name
  - Created date
  - Last edited date
- Two view options:
  - List view (default): Shows document titles and metadata in rows
  - Card view: Shows document titles, metadata, and a text snippet from the beginning of each document
- Document actions:
  - Click on list item/card to open document for editing
  - Share: copies link to clipboard and shows toast notification
  - Delete: with confirmation dialog for permanent deletion (all versions)

### 4. Document Page
Requires user authentication, all children pages are also protected.

#### Markdown Editor
- Desktop Layout:
  - Side-by-side layout with markdown editor on left, preview on right
  - Toggle for sync scrolling (off by default)
- Mobile Layout:
  - Tab-based interface with "Edit" and "Preview" tabs
  - User can switch between tabs using buttons at the top of the screen
  - Simple implementation prioritised for initial release

#### Document Management
- Save button:
  - Enabled only when there are unsaved changes
  - New documents: prompts for document name (validation for prohibted values), saves as version 1
  - Existing documents: saves to current version, updates last edited date
- Share button: copies link to clipboard and shows toast notification
- Three-dot-button
  - "Save as new version": saves as version X+1
  - "See version history": opens the [Document Version Modal](#3-document-version-modal-version-control)
  - "Delete": with confirmation dialog for permanent deleltion (all versions)

## Core Functionality

### 1. Markdown Editor/Preview
- Based on react-markdown combined with @uiw/react-md-editor
- Supports core markdown syntax features (incl. links, tables, code blocks)
- Features:
  - Clean, minimal design
  - Sync scroll option (user-toggled)
  - Syntax highlighting for code blocks

### 2. Document Link Sharing
- User can generate and share document URL
- Recipients can:
  1. View the rendered markdown
  2. Download the document as a markdown file
  3. "Open in MD Pretty" (requires sign-in, creates a copy in recipient's dashboard)
- No collaborative editing functionality
- Basic sharing security with no additional measures

### 3. Document Version Modal (version control)
This temporarily replaces the editor/preview split on the [Document Page](#4-document-page), with a large modal for version comparison, then returns to normal editing mode.
1. In this model, show:
   - List of versions (left panel): latest version selected by default
   - Previous version (middle panel): raw markdown
   - Current text from the editor (right panel): raw markdown
2. Include buttons:
   - "Copy to clipboard" button on the left panel (previous version)
   - "Close" button to return to editing/preview view
3. After closing or restoring, return to the normal editor view

### 4. AI Assistance
- User-initiated assistance only (no real-time suggestions)
- Implementation:
  1. User clicks "Ask AI" button in [Document Page](#4-document-page)
  2. User enters a prompt for document enhancement (e.g., "Fix my syntax", "Improve structure")
  3. System sends the entire markdown content along with the user's prompt to the LLM
  4. LLM returns edited version
  5. System displays original and AI-edited versions side-by-side
  6. User can choose to save the AI-edited version as current or as a new named version
- API Key Management:
  - "Bring your own API key" for Anthropic API
  - Limited to predefined selection of models (e.g., Claude Sonnet 3.5, Claude Sonnet 3.7)
  - API keys saved for future sessions
  - User interface for managing saved API keys

## Technical Implementation

### Authentication
- Implementation via Clerk integrated with Supabase
- Standard authentication flows for sign-up and sign-in
- Protected routes for authenticated features (Dashboard, Document editing)
- No specific custom requirements beyond basic functionality

### Database Schema
Users Table
- `id` (primary key, UUID, from Clerk auth)
- `email` (text, from Clerk auth)
- `created_at` (timestamp)
- `updated_at` (timestamp)

Documents Table
- `id` (primary key, UUID)
- `user_id` (foreign key to users.id)
- `name` (text)
- `created_at` (timestamp)
- `updated_at` (timestamp)
- `is_public` (boolean, for shared documents)
- `share_id` (UUID, for generating unique sharing links)

Document_Versions Table
- `id` (primary key, UUID)
- `document_id` (foreign key to documents.id)
- `content` (text, the actual markdown content)
- `version_name` (text, optional, for named versions)
- `created_at` (timestamp)
- `is_current` (boolean, identifies the current active version)

Document_Shares Table
- `id` (primary key, UUID)
- `document_id` (foreign key to documents.id)
- `created_at` (timestamp)
- `created_by` (foreign key to users.id)

API_Keys Table
- `id` (primary key, UUID)
- `user_id` (foreign key to users.id)
- `service` (text, e.g., "Anthropic")
- `key` (text, encrypted)
- `model` (text, selected model)
- `created_at` (timestamp)
- `updated_at` (timestamp)

### Error Handling
Simple approach to error handling:
 - Toast notifications for errors
 - Clear, user-friendly error messages
 - Graceful handling of common errors (network issues, authentication failures)
 - No complex error recovery mechanisms in initial implementation

## Implementation Priorities
Features should be implemented in the following order:

1. Header and footer
1. Home page
1. Authentication integration
1. Dashboard page
1. Document page (desktop/mobile): *Markdown Editor/Preview*
1. Document management (save, delete)
1. Document link sharing
1. Document page (desktop/mobile): *Document Version Modal*
1. "See it in action" page
1. AI assistance
1. API key management


## Future Considerations
Items explicitly noted for future implementation:
1. Autosave functionality
1. Enhanced markdown editor mobile experience with optimised layout, follow [this tool's design](https://markdownlivepreview.dev)
1. In [Document Version Modal](#3-document-version-modal-version-control), make current version (right panel) editable. This is convenient for users to copy partial content from prior versions into the current version
1. Analytics and user activity tracking
1. Full rendered preview in card view on dashboard