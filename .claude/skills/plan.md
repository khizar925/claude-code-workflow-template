---
name: plan
description: Create a detailed implementation plan for features without making any code changes. Use when user says "plan for", "plan to implement", "planning for", or similar planning requests.
---

# Code Change Planner Skill

Feature to plan: $ARGUMENTS

---

## Project Context

Read these files only when relevant to the feature being planned:

- `docs/MEMORY.md` — always read this first — decisions, patterns, and gotchas already established
- `docs/ARCHITECTURE.md` — read when feature touches DB queries, auth, middleware, or access control
- `docs/PROJECT.md` — read when you need to confirm tech stack, file structure, or existing conventions
- `tasks/lessons.md` — read if the feature is in an area where past mistakes were made

---

You are in **PLANNING MODE**. Your role is to create a comprehensive implementation plan WITHOUT making any code changes. Make sure to identify all edge cases and assume that this feature will be used by large number of users.

## When This Skill Is Invoked

This skill is automatically invoked when users request planning such as:
- "plan for login OAUTH implementation"
- "plan to implement dark mode"
- "planning for user authentication"
- "create a plan for adding payment integration"
- Any similar request asking for an implementation plan

## Your Responsibilities

### 1. **Explore the Codebase First**
Before creating the plan:
- Use Glob, Grep, and Read tools to understand existing patterns
- Identify the current architecture and tech stack
- Find similar existing features to maintain consistency
- Locate relevant configuration files, dependencies, and utilities

### 2. **Create a Comprehensive Implementation Plan**

Your plan MUST include the following sections:

#### **Overview & Architecture**
- Brief summary of what will be implemented
- High-level architecture diagram or description
- Key technical decisions and rationale
- Dependencies/libraries needed (with versions)
- Integration points with existing code

#### **File Structure & Changes**

For each file to create or modify, provide:

**File: `path/to/file.ext`**
- **Action**: [Create New | Update Existing]
- **Purpose**: What this file does
- **Key Changes**:
  - Specific functions/classes/components to add
  - Interfaces/types to define
  - Important implementation details
- **Dependencies**: What it imports/uses

Example:
```
**File: `backend/src/auth/oauth.controller.ts`**
- **Action**: Create New
- **Purpose**: Handle OAuth authentication flows
- **Key Changes**:
  - `initiateOAuth()` - Redirect to OAuth provider
  - `handleCallback()` - Process OAuth callback
  - `exchangeToken()` - Exchange auth code for tokens
- **Dependencies**: express, passport, oauth2 library
```

#### **Implementation Steps**

Numbered, sequential steps:
1. Step description with specific actions
2. Next step...

Example:
```
1. Install required packages: `npm install passport passport-google-oauth20`
2. Create OAuth configuration file at `backend/config/oauth.config.ts`
3. Implement OAuth controller at `backend/src/auth/oauth.controller.ts`
...
```

#### **Configuration Changes**

- Environment variables to add (with examples)
- Config files to update
- Database migrations/schema changes
- API routes to register

Example:
```
**Environment Variables (.env)**:
GOOGLE_CLIENT_ID=your_client_id_here
GOOGLE_CLIENT_SECRET=your_client_secret_here
OAUTH_CALLBACK_URL=http://localhost:3000/auth/callback
```

#### **Edge Cases & Error Handling**

List potential issues and how to handle them:
- Invalid OAuth tokens
- Network failures during OAuth flow
- User cancels authentication
- Expired sessions
- Race conditions
- Security considerations (CSRF, XSS, etc.)

#### **Testing Strategy**

**Manual Testing Checklist**:
- [ ] Step-by-step verification steps
- [ ] Expected outcomes
- [ ] How to verify success

Example:
```
**Manual Testing**:
1. Navigate to `/login`
2. Click "Sign in with Google"
3. Verify redirect to Google OAuth consent screen
4. After consent, verify redirect back with valid session
5. Check user data is stored in database
6. Verify JWT token is issued
```

#### **Security Considerations**

- Authentication/Authorization checks
- Data validation requirements
- Secure token storage
- HTTPS requirements
- CORS configuration
- Rate limiting needs

#### **Rollback Plan**

- How to revert changes if needed
- Database rollback steps
- Configuration rollback

### 3. **Format & Presentation**

- Use clear markdown formatting
- Include code examples where helpful (but NO actual implementation)
- Use bullet points and numbered lists
- Add comments to explain complex decisions
- Keep it organized and easy to follow

### 4. **Important Constraints**

**DO NOT**:
- Write actual implementation code
- Make any file changes (no Edit, Write, or NotebookEdit tools)
- Install packages or run commands
- Commit changes

**DO**:
- Use Read, Glob, Grep tools to explore
- Use Task tool with Explore agent for codebase understanding
- Ask clarifying questions using AskUserQuestion if needed
- Create detailed, actionable plans

### 5. **Output Format**

Present your plan in this structure:

```markdown
# Implementation Plan: [Feature Name]

## 1. Overview & Architecture
[Content]

## 2. Technical Stack & Dependencies
[Content]

## 3. File Structure & Changes
[Detailed file-by-file breakdown]

## 4. Implementation Steps
[Sequential steps]

## 5. Configuration Changes
[Environment variables, configs, etc.]

## 6. Edge Cases & Error Handling
[Potential issues and solutions]

## 7. Testing Strategy
[Unit, integration, manual tests]

## 8. Security Considerations
[Security checklist]

## 9. Rollback Plan
[How to undo changes]

## 10. Estimated Complexity
[Simple/Medium/Complex with brief justification]
```

## Example Usage

**User**: "plan for login OAUTH implementation"

**Your Response**:
1. First, explore the codebase to understand existing auth patterns
2. Identify the backend framework and current auth mechanism
3. Create a comprehensive plan covering all sections above
4. Present the plan in the specified format
5. Ask if user wants clarification on any part

Remember: Your goal is to provide a clear, detailed roadmap that a developer can follow to implement the feature. Be thorough, consider edge cases, and maintain consistency with the existing codebase patterns.

## Prerequisites & Requirements

Before finalizing the plan, identify and list everything needed that is outside the codebase:

**Credentials & Keys**
- API keys, client IDs, client secrets required
- Where to obtain them (e.g. Google Cloud Console, Stripe Dashboard)
- Which `.env` variables they map to

**Third-party Accounts / Services**
- Any external service accounts that need to be created or configured
- Paid plans or free tier limitations to be aware of

**External Configuration**
- Callback URLs, redirect URIs, or webhook endpoints to register
- CORS origins, IP whitelists, or DNS changes needed

**Internal Prerequisites**
- Features or models that must exist before this can be built
- Migrations or seed data required
- Other team members or approvals needed

List each item as a checklist so it can be verified before implementation starts:
- [ ] Prerequisite item

---

## Output & Saving

When the plan is complete, re-verify it:
- Every step is specific and unambiguous
- No step depends on something not covered in a prior step
- Files affected list is complete — nothing missing
- Security considerations are honest, not just filler
- Rollback plan is actionable

Then save:
- Full plan → `docs/PLANS/<FeatureName>.md` (PascalCase, no spaces — e.g. `GoogleOAuth.md`, `TaskReminders.md`)
- Checkable step summary → `tasks/todo.md`