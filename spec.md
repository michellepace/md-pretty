# MD Pretty - Technical Specification Document

## Project Overview
MD Pretty is a web-based markdown editor application designed primarily for technical writers who need a simple solution to create, edit, and manage markdown documents. The application provides a clean, user-friendly interface with mobile-first responsive design, live preview functionality, and AI-assisted editing capabilities.

## Target Audience
- Technical writers seeking a streamlined markdown editing experience
- Users who create Product Requirement Documents (PRDs) and similar technical documentation
- Individuals who want to manage all their markdown documents in one place

## Tech Stack
- **Frontend:** Next.js, TypeScript, Tailwind CSS, shadcn/UI, Lucide Icons
- **Backend & Storage:** Supabase for database, authentication, and storage
- **Authentication:** Google Sign-in only, handled via Clerk integrated with Supabase
- **AI Integration:** Anthropic API (Claude models)

## Feature Specifications

### 1. Authentication & User Management
- **Authentication Method:** Google Sign-in only (via Clerk through Supabase)
- **User Roles:** Single user role only; no team or role-based permissions
- **User Profile:** No custom profile information needed beyond what's provided by Google authentication

### 2. User Dashboard
- **Layout:** Simple list view of all user documents
- **Information Display:**
  - Document title
  - Creation date
  - Last edited date
- **Actions:**
  - Create new document
  - Open existing document
  - Delete document
- **Organization:** Flat list structure with no folders or tags
- **Future Enhancement (V2):** Grid of cards with document previews

### 3. Markdown Editor
- **Layout:**
  - Desktop: Side-by-side editor and live preview
  - Mobile: Responsive layout handled by the markdown editor library
- **Supported Markdown Features:**
  - Core markdown syntax (headings, lists, links, bold, italic, etc.)
  - Tables
  - Code blocks
  - Syntax highlighting (nice to have if easily implementable)
- **Save Functionality:**
  - Manual save only (no autosave)
  - When saving a new document, prompt user for document name
  - Options to "Save" or "Save as version X"
- **Notifications:** Toast messages for successful saves, errors, etc.

### 4. Version Control
- **Version History:** Unlimited version history per document
- **Version Management:**
  - Save current version
  - Save as new version
  - View version history
- **Version Comparison:** Side-by-side comparison of complete before and after versions (no diff highlighting required)

### 5. Document Sharing
- **Share Method:** Shareable URL
- **Recipient Options:**
  - View rendered markdown document in browser
  - Download as markdown file
  - "Open in MD Pretty" - creates a copy of the document in recipient's dashboard after sign-in
- **Access Control:** No additional access controls needed; all shared links are public

### 6. AI Assistance
- **Implementation Phases:**
  - **Version 1:** All users use application-provided API key (hidden from users)
  - **Version 2:** Selected users have access to application's AI; others must provide their own API key
- **API Key Management:** All API keys stored securely in backend
- **AI Integration:** Anthropic API (Claude models: Sonnet 3.5 or Sonnet 3.7 only)
- **Functionality:**
  - User clicks "Ask AI" button in editor view
  - User enters a prompt for document enhancement
  - System sends current document content and user prompt to AI
  - AI response displayed as a complete new version side-by-side with original
  - User can choose to save new version or continue with original

### 7. Import/Export
- **Import:** Allow users to upload existing .md files
- **Export:**
  - Download as markdown file
  - Shared documents automatically rendered as HTML when viewed via shared link

### 8. User Interface & Experience
- **Design Philosophy:** Mobile-first responsive design, clean and simple UI
- **UI Components:** Use shadcn/UI components for consistent design
- **Icons:** Lucide Icons library
- **Notifications:** Toast notifications for important actions/events

### 9. Technical Requirements
- **Internet Connectivity:** Always required; no offline functionality
- **Browser Support:** Modern browsers only (Chrome, Firefox, Safari, Edge)
- **Responsive Design:** All features must work on both desktop and mobile devices

## API & Data Structure

### Document Data Model
```typescript
interface Document {
  id: string;
  user_id: string;
  title: string;
  content: string;
  created_at: Date;
  updated_at: Date;
  current_version: number;
}

interface DocumentVersion {
  id: string;
  document_id: string;
  version_number: number;
  content: string;
  created_at: Date;
  created_by: string; // user_id or "AI" if AI-generated
}

interface SharedDocument {
  id: string;
  document_id: string;
  share_url: string;
  created_at: Date;
}

interface UserSettings {
  id: string;
  user_id: string;
  anthropic_api_key?: string; // Optional, for V2
  default_model?: string; // "claude-3.5-sonnet" or "claude-3.7-sonnet"
}
```

### Primary API Endpoints

```
POST /api/auth/google               # Google authentication
GET /api/documents                  # Get all user documents
POST /api/documents                 # Create new document
GET /api/documents/:id              # Get specific document
PUT /api/documents/:id              # Update document
DELETE /api/documents/:id           # Delete document
POST /api/documents/:id/versions    # Create new document version
GET /api/documents/:id/versions     # Get document version history
GET /api/documents/:id/versions/:vnum # Get specific document version
POST /api/documents/:id/share       # Create shared link
GET /api/shared/:shareId            # Get shared document (public)
POST /api/ai/enhance                # Send document to AI for enhancement
```

## User Flows

### Document Creation Flow
1. User signs in with Google account
2. User navigates to dashboard
3. User clicks "Create New"
4. User creates markdown content in editor
5. User clicks "Save"
6. System prompts for document title
7. System saves document and returns to dashboard

### AI Assistance Flow
1. User opens existing document
2. User clicks "Ask AI" button
3. User enters enhancement prompt
4. System sends document and prompt to Anthropic API
5. System displays AI response side-by-side with original
6. User decides to save AI version or continue with original

### Document Sharing Flow
1. User opens document
2. User clicks "Share" button
3. System generates shareable link
4. User shares link with recipient
5. Recipient opens link in browser
6. Recipient sees rendered markdown document
7. Recipient can:
   - Download as markdown file
   - Click "Open in MD Pretty"
   - If chosen, sign in with Google
   - Document is copied to recipient's dashboard

## Development Phases

### Version 1 (MVP)
- Authentication with Google Sign-in
- Document creation, editing, and deletion
- Basic version control
- Markdown editor with live preview
- Document sharing via URL
- AI assistance using application-provided API key

### Version 2
- Grid view for dashboard with document previews
- "Bring your own API key" functionality for AI assistance
- Selected users have access to application's AI
- Additional UI enhancements

## Non-Requirements
- Offline functionality
- Collaborative editing
- Folders or tags for organization
- Export to formats other than markdown
- Advanced markdown features (mathematical notation, diagrams)
- Team or role-based permissions
- Password-protected documents
- Analytics tracking