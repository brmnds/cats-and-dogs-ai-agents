---
inclusion: manual
---

# Pet Image AI Application Requirements

_Specific requirements and constraints for the Pet Image AI project_

## Application Overview

The Pet Image AI application is a single-page web application that generates pet images and classifies them using AI, with user name tracking and database storage.

## Core Functionality Requirements

### Image Generation

- **Service**: Amazon Nova Canvas on Bedrock
- **Model**: amazon.nova-canvas-v1:0
- **Input**: Dropdown selection (Cat or Dog)
- **Output**: Base64 encoded image displayed on page
- **No Authentication**: Anyone can generate images

### Image Classification

- **Service**: Strands Agents Framework on Bedrock AgentCore Runtime
- **Input**: Generated image + user name (required)
- **Output**: Classification (cat/dog) + confidence score
- **Storage**: Results stored in Aurora PostgreSQL database
- **Validation**: User name required before classification

### Database Storage

- **Service**: Amazon Aurora PostgreSQL
- **Data**: User name, classification, confidence, timestamp, image metadata
- **Error Handling**: Classification works even if database fails
- **Schema**: See database-guidelines.md for table structure

## Technical Constraints

### No Authentication System

- No user registration or login required
- Simple name input for classification tracking
- No session management or user accounts
- Public access to all functionality

### AWS-Only Architecture

- **Hosting**: AWS Amplify (not Vercel)
- **Database**: Aurora PostgreSQL (not other databases)
- **AI Services**: Amazon Bedrock only (no OpenAI, etc.)
- **Deployment**: Native AWS service integration

### Error Handling Requirements

- **Graceful Degradation**: App works even if services fail
- **User-Friendly Messages**: No technical error details to users
- **Database Independence**: Classification works without database
- **Retry Logic**: Automatic retries for transient failures

## User Experience Requirements

### Interface Design

- **Framework**: Next.js + React + TypeScript + Tailwind CSS
- **Responsive**: Works on mobile and desktop
- **Accessibility**: WCAG 2.1 AA compliance
- **Loading States**: Clear indicators for all operations
- **Error States**: Helpful error messages and recovery options

### Workflow

1. User selects pet type (cat/dog) from dropdown
2. User clicks "Generate Image" button
3. Generated image appears on page
4. User enters their name in input field
5. User clicks "Classify Image" button
6. Classification result appears with confidence score
7. Result is stored in database (with error handling if database fails)

## Development Requirements

### Local Development

- **Environment**: localhost:3000 with hot reloading
- **AWS Credentials**: Required for local testing
- **Database**: Connect to Aurora instance for local development
- **Testing**: All AWS services must work locally

### Deployment

- **Platform**: AWS Amplify with automatic CI/CD
- **Environment Variables**: Managed through Amplify console
- **IAM Roles**: Amplify-managed roles for AWS service access
- **Monitoring**: CloudWatch for error tracking and performance

### Code Quality

- **TypeScript**: Strict mode enabled
- **Testing**: Optional unit tests (marked with \* in tasks)
- **Error Handling**: Comprehensive error boundaries and API error handling
- **Performance**: Optimized for 200-1K concurrent users

## Security Requirements

### Data Protection

- **No PII Storage**: Only user names (not sensitive data)
- **AWS IAM**: Least privilege access for all services
- **HTTPS**: All communications encrypted in transit
- **Input Validation**: Sanitize all user inputs

### AWS Security

- **Credentials**: No hardcoded credentials in code
- **Environment Variables**: Secure storage in Amplify
- **VPC**: Database in private subnet (if required)
- **Monitoring**: CloudWatch for security event tracking

## Performance Requirements

### Response Times

- **Image Generation**: < 30 seconds (Nova Canvas)
- **Image Classification**: < 15 seconds (Bedrock Agent)
- **Database Operations**: < 2 seconds
- **Page Load**: < 3 seconds initial load

### Scalability

- **Concurrent Users**: Support 200-1K users
- **Database**: Aurora auto-scaling enabled
- **API Routes**: Serverless scaling through Amplify
- **Error Recovery**: Graceful handling of service limits

## Compliance Requirements

### Accessibility

- **WCAG 2.1 AA**: Full compliance required
- **Keyboard Navigation**: All functionality accessible via keyboard
- **Screen Readers**: Proper ARIA labels and semantic HTML
- **Color Contrast**: Minimum 4.5:1 ratio for normal text

### Data Handling

- **User Consent**: Clear information about data storage
- **Data Retention**: Define retention policy for classification records
- **Privacy**: No tracking beyond classification storage
- **Transparency**: Clear explanation of AI usage

---

_Note: These requirements are specific to the Pet Image AI application and should be referenced during development to ensure compliance with project specifications._
