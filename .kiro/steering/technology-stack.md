# Technology Stack

_Draft framework - to be defined based on project requirements_

## Current Stable Versions (October 2025)

### Runtime & Language

- **Node.js**: v22.20.0 (LTS)
- **TypeScript**: Latest stable
- **JavaScript**: ES2024 features

### Frontend Framework

- **Next.js**: v15.5.6 (Latest stable) ✅ **SELECTED**
- **React**: Latest compatible with Next.js ✅ **SELECTED**
- **CSS**: Tailwind CSS ✅ **SELECTED**

### Backend & API

- **API Framework**: Next.js API Routes ✅ **SELECTED**
- **Database**: Amazon Aurora PostgreSQL ✅ **SELECTED**
- **ORM/Query Builder**: Native AWS SDK with PostgreSQL client ✅ **SELECTED**

### AI & Machine Learning

- **Image Generation**: Amazon Nova Canvas on Bedrock ✅ **SELECTED**
- **AI Agent Framework**: Strands Agents Framework ✅ **SELECTED**
- **AI Agent Runtime**: Amazon Bedrock AgentCore Runtime ✅ **SELECTED**
- **Foundation Models**: Amazon Bedrock models ✅ **SELECTED**

### Development Tools

- **Package Manager**: npm ✅ **SELECTED**
- **Linting**: ESLint with TypeScript support ✅ **SELECTED**
- **Formatting**: Prettier ✅ **SELECTED**
- **Testing**: Vitest (with optional unit tests) ✅ **SELECTED**

### Infrastructure & Deployment

- **Cloud Provider**: AWS ✅ **SELECTED**
- **Hosting Platform**: AWS Amplify ✅ **SELECTED**
- **Database Hosting**: Amazon Aurora PostgreSQL ✅ **SELECTED**
- **Image Storage**: Base64 in-memory (no persistent storage) ✅ **SELECTED**

### Authentication & Security

- **Authentication**: None (no login required) ✅ **SELECTED**
- **Environment Management**: dotenv with validation ✅ **SELECTED**
- **Security**: AWS IAM roles, CORS configuration ✅ **SELECTED**
- **AWS Services**: Bedrock, Aurora, Amplify integration ✅ **SELECTED**

### Monitoring & Analytics

- **Error Tracking**: Sentry or similar (optional)
- **Analytics**: Simple analytics or Google Analytics (optional)
- **Performance Monitoring**: Built-in Next.js analytics or custom

## Technology Decision Criteria

### For 200-1K Users Scale

- Prioritize developer productivity over premature optimization
- Choose mature, well-documented technologies
- Prefer solutions with good TypeScript support
- Consider hosting costs and complexity

### Decision Framework

1. **Maturity**: Is the technology stable and well-maintained?
2. **Community**: Does it have good documentation and community support?
3. **TypeScript**: Does it have excellent TypeScript integration?
4. **Scale**: Is it appropriate for our user base and growth expectations?
5. **Team**: Does it match the team's expertise and preferences?

## Pet Image AI Application Stack

All technology decisions have been finalized for the Pet Image AI application:

### Core Architecture

- **Frontend**: Next.js 15.5.6 + React + TypeScript + Tailwind CSS
- **Backend**: Next.js API Routes with AWS SDK integration
- **Database**: Amazon Aurora PostgreSQL for classification data storage
- **Hosting**: AWS Amplify with native AWS service integration
- **AI Services**: Amazon Bedrock (Nova Canvas + AgentCore Runtime)

### Key Features

- **No Authentication**: Simple, accessible interface without login requirements
- **AI Image Generation**: Amazon Nova Canvas for cat/dog image generation
- **AI Classification**: Strands Agents Framework on Bedrock AgentCore
- **Data Persistence**: User names and classification results stored in Aurora
- **Error Handling**: Graceful degradation with user-friendly error messages

### Environment Variables Required

```bash
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_access_key (local dev only)
AWS_SECRET_ACCESS_KEY=your_secret_key (local dev only)
BEDROCK_AGENT_ID=your_agent_id
BEDROCK_AGENT_ALIAS_ID=your_alias_id
NOVA_CANVAS_MODEL_ID=amazon.nova-canvas-v1:0
DATABASE_HOST=your-aurora-cluster.cluster-xyz.us-east-1.rds.amazonaws.com
DATABASE_PORT=5432
DATABASE_NAME=pet_image_ai
DATABASE_USERNAME=your_db_user
DATABASE_PASSWORD=your_db_password
```

---

_Note: This stack is specifically configured for the Pet Image AI application requirements._
