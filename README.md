# MailMind - AI Email Generator System

A modern email generation and management system built with Spring Boot and React. This project provides both a REST API service for email generation and a browser extension for Gmail integration.

## Project Overview

This system consists of three main components:

1. **Spring Boot Backend API** - A Java-based REST API for email generation and management
2. **React Web Application** - A user interface for testing and generating email replies
3. **Mail Mind Browser Extension** - A Chrome extension that integrates with Gmail to provide AI-powered email replies

## Features

- Generate email responses based on input content and tone
- Store and retrieve generated emails
- REST API with validation and error handling
- Gmail integration through browser extension
- Modern React user interface for direct email generation

## Technical Stack

### Backend
- Java 24
- Spring Boot
- Jakarta EE
- Lombok
- Spring MVC for REST endpoints

### Frontend
- React 19.1.0
- Material UI 7.2.0
- Axios for API communication
- Vite 7.0.0 for build tooling

### Browser Extension
- Manifest V3 Chrome Extension
- JavaScript content scripts
- Gmail integration

## Project Structure

### Backend (Spring Boot)

```
src/main/java/com/email/email_writer_sb/
├── EmailGeneratorController.java   # REST API endpoints
├── EmailGeneratorService.java      # Business logic for email generation
├── EmailRequestDto.java            # Data transfer object for requests
├── EmailResponseDto.java           # Data transfer object for responses
├── EmailWriterSbApplication.java   # Spring Boot application entry point
└── GlobalExceptionHandler.java     # Centralized exception handling
```

### Frontend (React)

The React application provides a user-friendly interface for testing the email generation service.

### Browser Extension

The Mail Mind browser extension integrates with Gmail to provide AI-powered email reply generation directly in the Gmail interface.

## API Endpoints

### Generate Email
`POST /api/emails/generate`

Generates a new email based on the provided request.

**Request Body:**
```json
{
  "subject": "Meeting Request",
  "recipient": "example@example.com",
  "emailType": "reply",
  "senderName": "John Doe",
  "additionalContext": "Previous discussion about project timeline"
}
```

**Response:**
```json
{
  "id": 1,
  "subject": "Meeting Request",
  "recipient": "example@example.com",
  "content": "Dear example@example.com,\n\nThis is a generated email based on your request.\n\nBest regards,\nEmail Generator System",
  "createdAt": "2025-07-04T10:15:30"
}
```

### Get Email by ID
`GET /api/emails/{id}`

Retrieves an email by its ID.

### Get All Emails
`GET /api/emails`

Retrieves a list of all generated emails.

## Setup Instructions

### Backend Setup

1. Ensure you have Java 24 and Maven installed
2. Clone this repository
3. Navigate to the project root directory
4. Run `mvn clean install` to build the project
5. Run `mvn spring-boot:run` to start the backend server

The server will start on `http://localhost:8080`

### Frontend Setup

1. Navigate to the `mail-mind-react` directory
2. Run `npm install` to install dependencies
3. Run `npm run dev` to start the development server

The React application will be available at `http://localhost:5173`

### Browser Extension Setup

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable "Developer mode" in the top-right corner
3. Click "Load unpacked" and select the `mail-mind-extension` directory
4. The extension should now be installed and will work when you open Gmail

## Development

### Adding New Features

To add new features to the email generation system:

1. Create appropriate DTOs for new data structures
2. Add service methods in `EmailGeneratorService.java`
3. Expose new endpoints in `EmailGeneratorController.java`
4. Update the React UI in `App.jsx` to utilize new features
5. Modify the browser extension in `content.js` if needed

### Testing

The system can be tested using:

1. The React UI for visual testing
2. Postman or curl for API testing
3. The browser extension directly in Gmail

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

For questions or support, please open an issue in the project repository.
