# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**ClaudeCodeWeb** is a User Service API for an LMS (Learning Management System) platform. The project currently contains an OpenAPI 3.1 specification defining the API contract. Implementation is pending.

## API Architecture

### Core Entities
- **User**: UUID-identified users with profiles (username, first_name, last_name, email, role)
- **Roles**: admin, instructor, student
- **Permissions**: Course-level access control (can_view, can_edit, can_delete)
- **Activity Logs**: User action tracking with timestamps

### Endpoints Structure

```
POST   /api/user                                          # Create user
GET    /api/user/{user_uuid}                             # Get user profile
PATCH  /api/user/{user_uuid}                             # Update user
DELETE /api/user/{user_uuid}                             # Delete user
GET    /api/user/{user_uuid}/permissions/{course_uuid}   # Get permissions
GET    /api/user/{user_uuid}/activity                    # Get activity log
```

### Key API Patterns

**API Versioning**
- All endpoints require `X-Api-Version` header (currently "0.1")
- Version header is mandatory for all requests

**Authentication**
- Write operations (POST, PATCH, DELETE) require Bearer token: `Authorization: Bearer <token>`
- Read operations (GET) currently don't enforce authentication in spec

**Response Headers**
- All responses include `X-User-Pseudo-ID` header with user UUID
- Used for tracking/telemetry purposes

**Field Filtering**
- User profile endpoint supports `filter` query parameter for field selection
- Example: `?filter=username,email` returns only specified fields
- Permissions endpoint supports filtering specific permissions (view, edit, delete)

**Pagination**
- Activity log endpoint uses limit/offset pagination
- Default limit: 10, max: 100
- Supports filtering by action type

**Error Handling**
- Standardized error schema with status, error, message, timestamp
- HTTP status codes: 200 (OK), 201 (Created), 204 (No Content), 400 (Bad Request), 404 (Not Found)

## Servers

- **Development**: http://localhost:3000
- **Production**: https://api.lms.example.com

## When Implementing

The OpenAPI specification (OpenAPI.yaml) is the source of truth for:
- Request/response schemas
- Required fields and validation rules
- Supported query parameters and filters
- HTTP status codes and error responses

Ensure any implementation adheres strictly to the defined contract, including:
- UUID format for all IDs
- Email format validation
- Enum constraints for roles and permissions
- Required headers (X-Api-Version, Authorization)
