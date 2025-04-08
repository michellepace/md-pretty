# MD Pretty - Technical Specification

## Table of Contents
1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [User Interface & Experience](#user-interface--experience)
   - [Header](#header)
   - [Footer](#footer)
   - [Home Page](#home-page)
   - ["See it in Action" Page](#see-it-in-action-page)
   - [Dashboard Page](#dashboard-page)
   - [Document Page](#document-page)
4. [Core Functionality](#core-functionality)
   - [Markdown Editor](#markdown-editor)
   - [Document Management](#document-management)
   - [Document Link Sharing](#document-link-sharing)
   - [Version Control](#version-control)
   - [AI Assistance](#ai-assistance)
5. [Authentication & User Management](#authentication--user-management)
6. [Database Schema](#database-schema)
7. [Error Handling](#error-handling)
8. [Implementation Priorities](#implementation-priorities)
9. [Future Considerations](#future-considerations)

## Project Overview

MD Pretty is a web application that provides a clean, user-friendly markdown editor with live preview and AI editing assistance. The application is designed with a mobile-first responsive approach, prioritizing simplicity and user experience. MD Pretty targets anyone who wants to create, manage, and share markdown documents in a beautiful interface.

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

## User Interface & Experience

### Header
- Simple, clean design shared across the application
- Contains:
  - Navigation logo with "MD Pretty" text
  - "Sign in" (sign up) button for unauthenticated users
  - "Dashboard" button if user is authenticated AND on homepage
  - User profile icon if user is on a protected page (requires authentication)

### Footer
- Minimalist design shared across the application
- Contains only copyright information in a single line

### Home Page
- Hero section with prominent "See it in action" call-to-action button
- Content explaining the product features in a clear, concise manner
- Clean, visually appealing layout

### "See it in Action" Page
- Provides unauthenticated users access to a demo of the markdown editor with live preview
- Functionally similar to the Document page but with limited capabilities
- "Save" button triggers authentication flow:
  1. Upon successful authentication, user is redirected to protected Document page
  2. A modal prompts the user to name the document
  3. The markdown document is saved to the user's account
  4. A toast notification displays "Saved" confirmation

### Dashboard Page
- Displays user's markdown documents with fields:
  - Document name
  - Created date
  - Last edited date
- Two view options:
  - List view (default): Shows document titles and metadata in rows
  - Card view: Shows document titles, metadata, and a text snippet from the beginning of each document
- Document actions:
  - Click on list item/card to open document for editing
  - Delete button (with confirmation dialog for permanent deletion)
  - Share button (copies link to clipboard and shows toast notification)

### Document Page
#### Desktop Layout:
- Side-by-side layout with editor on left, preview on right
- Toggle for sync scrolling (off by default)

#### Mobile Layout:
- Tab-based interface with "Edit" and "Preview" tabs
- User can switch between tabs using buttons at the top of the screen
- Simple implementation prioritized for initial release

## Core Functionality

### Markdown Editor
- Based on react-markdown combined with @uiw/react-md-editor
- Supports core markdown syntax features:
  - Headings
  - Lists (ordered and unordered)
  - Links
  - Tables
  - Code blocks
  - Bold, italic, and other text formatting
- Features:
  - Clean, minimal design
  - Sync scroll option (user-toggled)
  - Syntax highlighting for code blocks

### Document Management
- Save functionality:
  - Explicit save only (no autosave in initial implementation)
  - Save button clearly visible in the editor interface
  - Toast notification confirms successful save
- Document naming:
  - Validation for prohibited characters only
  - No character limits or uniqueness requirements enforced
- Document deletion:
  - Confirmation dialog required
  - Permanent deletion (no trash/recovery feature)

### Document Link Sharing
- User can generate and share document URL
- Recipients can:
  1. View the rendered markdown
  2. Download the document as a markdown file
  3. "Open in MD Pretty" (requires sign-in, creates a copy in recipient's dashboard)
- No collaborative editing functionality
- Basic sharing security with no additional measures

### Version Control
- Simple implementation focused on comparison
- Features:
  - Save current version with optional version name
  - View list of previous versions with timestamps
  - Compare current version with any previous version in a simple side-by-side view
  - No detailed diff highlighting in initial implementation

### AI Assistance
- User-initiated assistance only (no real-time suggestions)
- Implementation:
  1. User clicks "Ask AI" button in Document page
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

## Authentication & User Management
- Implementation via Clerk integrated with Supabase
- Standard authentication flows for sign-up and sign-in
- Protected routes for authenticated features (Dashboard, Document editing)
- No specific custom requirements beyond basic functionality

## Database Schema

### Users Table
- `id` (primary key, UUID, from Clerk auth)
- `email` (text, from Clerk auth)
- `created_at` (timestamp)
- `updated_at` (timestamp)

### Documents Table
- `id` (primary key, UUID)
- `user_id` (foreign key to users.id)
- `name` (text)
- `created_at` (timestamp)
- `updated_at` (timestamp)
- `is_public` (boolean, for shared documents)
- `share_id` (UUID, for generating unique sharing links)

### Document_Versions Table
- `id` (primary key, UUID)
- `document_id` (foreign key to documents.id)
- `content` (text, the actual markdown content)
- `version_name` (text, optional, for named versions)
- `created_at` (timestamp)
- `is_current` (boolean, identifies the current active version)

### Document_Shares Table
- `id` (primary key, UUID)
- `document_id` (foreign key to documents.id)
- `created_at` (timestamp)
- `created_by` (foreign key to users.id)

### API_Keys Table
- `id` (primary key, UUID)
- `user_id` (foreign key to users.id)
- `service` (text, e.g., "Anthropic")
- `key` (text, encrypted)
- `model` (text, selected model)
- `created_at` (timestamp)
- `updated_at` (timestamp)

## Error Handling
- Simple approach to error handling:
  - Toast notifications for errors
  - Clear, user-friendly error messages
  - Graceful handling of common errors (network issues, authentication failures)
  - No complex error recovery mechanisms in initial implementation

## Implementation Priorities
Features should be implemented in the following order:

1. Core markdown editor functionality
2. Header and footer
3. Home page
4. "See it in action" page
5. Authentication integration
6. Dashboard page
7. Document page (desktop and mobile views)
8. Document management (save, delete)
9. Document link sharing
10. Version control
11. AI assistance
12. API key management

## Future Considerations
Items explicitly noted for future implementation:

- Analytics and user activity tracking
- Advanced accessibility features
- More sophisticated version control with detailed diff highlighting
- Autosave functionality
- Collaborative editing features
- Enhanced mobile experience with optimized layouts
- Full rendered preview in card view on dashboard