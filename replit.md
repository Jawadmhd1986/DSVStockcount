# Overview

This is a Flask-based DSV (logistics company) quotation system that provides an intelligent quotation generator for various logistics services. The application offers 3PL (storage/warehousing), 4PL (comprehensive logistics), transportation, and relocation services with an integrated approval workflow system. It features an AI-powered chatbot assistant using OpenAI's GPT models and RAG (Retrieval-Augmented Generation) for intelligent customer support. The system includes user authentication, quotation generation with PDF exports, approval workflows with version control, and real-time notifications.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture
- **Template Engine**: Jinja2 with server-side rendering
- **Styling**: Custom CSS with DSV corporate branding and responsive design
- **JavaScript**: Vanilla JavaScript for interactive components (chatbot, approval workflows)
- **Mobile Support**: Responsive design with mobile-first approach and viewport height fixes
- **Page Structure**: Single-page forms for each service type with modal previews

## Backend Architecture
- **Framework**: Flask web framework with Blueprint-style routing
- **Session Management**: Cookie-based authentication system
- **File Storage**: JSON-based persistence layer for simplicity and rapid development
- **Document Generation**: python-docx for Word document generation, PDF support via pypdf
- **Business Logic**: Modular calculation functions with Decimal precision for financial accuracy

## Data Storage Solutions
- **Primary Storage**: JSON files for all data persistence
  - `approvals.json`: Approval workflow records with version history
  - `notifications.json`: User notification system
  - `user_history.json`: Per-user quotation history tracking
- **RAG Index**: NumPy-based vector storage (`rag_index.npz`) with metadata (`rag_index_meta.json`)
- **Session Data**: Server-side session storage via Flask sessions

## Authentication and Authorization
- **Authentication**: Email-based login system with role-based access
- **Authorization**: Role-based permissions (approver vs requester roles)
- **Session Security**: Cookie-based session management with user context preservation

## AI Integration Architecture
- **Chatbot Engine**: OpenAI GPT-4o-mini with custom RAG implementation
- **Embedding Model**: OpenAI text-embedding-3-small for document vectorization
- **RAG System**: Custom implementation with chunked document processing and semantic search
- **Fallback Strategy**: Local knowledge base with ChatGPT fallback when strict mode disabled
- **Content Sources**: Automatic indexing of templates, documentation, and knowledge base files

## Approval Workflow System
- **Version Control**: Immutable version snapshots for each quotation edit
- **State Management**: PENDING → APPROVED/REVISED/CHANGES_REQUESTED workflow
- **Audit Trail**: Complete history of all approval actions and modifications
- **Real-time Updates**: In-app notification system for approval status changes

## Pricing and Calculation Engine
- **Decimal Precision**: All financial calculations use Python Decimal with ROUND_HALF_UP
- **Rate Management**: Centralized rate dictionaries for consistency across services
- **Auto-recalculation**: Dynamic total updates when approvers modify quotations
- **Multi-service Support**: Separate calculation logic for 3PL, 4PL, transport, and relocation services

# External Dependencies

## Core Framework Dependencies
- **Flask**: Web framework and routing
- **Jinja2**: Template rendering engine
- **Werkzeug**: WSGI utilities and development server

## Document Processing
- **python-docx**: Word document generation and manipulation
- **pypdf**: PDF document processing and generation
- **openpyxl**: Excel file handling for data imports/exports

## Data Processing
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing and vector operations for RAG
- **pytz**: Timezone handling for international operations

## AI and Machine Learning
- **OpenAI API**: GPT models for chatbot and text embeddings
- **Custom RAG Implementation**: Built on numpy for document retrieval and semantic search

## Utilities
- **requests**: HTTP client for external API calls
- **python-dotenv**: Environment variable management
- **lxml**: XML/HTML parsing for document processing

## Production Deployment
- **gunicorn**: WSGI HTTP server for production deployment
- **blinker**: Signal handling for Flask applications

## Development and Testing
- **logging**: Built-in Python logging for debugging and monitoring
- **functools**: Decorator utilities for authentication and caching
- **pathlib**: Modern path handling for file operations

Note: The application uses file-based JSON storage as the primary database solution, making it lightweight and suitable for rapid deployment without requiring external database setup.