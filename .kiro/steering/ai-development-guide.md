# AI Development Guide

_Amazon Bedrock & Strands Agents Framework - Pet Image AI Application_

## Core Principles

### Model Selection for Pet Image AI

**Selected AWS Bedrock Services:**

- **Image Generation**: Amazon Nova Canvas (amazon.nova-canvas-v1:0)
  - Optimized for high-quality image generation
  - Cost-effective for on-demand image creation
  - Supports cat and dog image generation with text prompts
- **Image Classification**: Strands Agents Framework on Bedrock AgentCore Runtime
  - Enterprise-grade agent deployment and scaling
  - Structured response format with confidence scores
  - Built-in error handling and retry mechanisms

**Cost Considerations:**

- Nova Canvas: Pay-per-image generation (suitable for demo/testing)
- Bedrock Agent: Pay-per-invocation with built-in optimization
- Monitor usage through AWS CloudWatch
- No caching needed for demo application (each generation is unique)

### Prompt Engineering for Pet Image AI

**Nova Canvas Image Generation Prompts:**

```typescript
// Template for cat images
const catPrompt =
  'A realistic, high-quality photograph of a cute domestic cat. The cat should be clearly visible, well-lit, and the main subject of the image. Professional photography style.';

// Template for dog images
const dogPrompt =
  'A realistic, high-quality photograph of a cute domestic dog. The dog should be clearly visible, well-lit, and the main subject of the image. Professional photography style.';
```

**Strands Agent Classification Instructions:**

```typescript
// Agent system prompt for classification
const classificationPrompt = `
You are an expert pet classifier. Analyze the provided image and determine if it contains a cat or a dog.

Response format:
{
  "classification": "cat" | "dog",
  "confidence": 0.0-1.0,
  "reasoning": "Brief explanation of key features that led to this classification"
}

Focus on key distinguishing features like facial structure, ears, body shape, and posture.
`;
```

**Best Practices:**

- Keep prompts simple and focused on the specific task
- Use consistent terminology across all AI interactions
- Test with edge cases (unclear images, multiple animals, etc.)
- Validate response format before processing

### Error Handling & Reliability for Pet Image AI

**AWS Bedrock Error Handling:**

```typescript
// Error categories for Pet Image AI
enum AIErrorType {
  NOVA_CANVAS_FAILED = 'NOVA_CANVAS_FAILED',
  CLASSIFICATION_FAILED = 'CLASSIFICATION_FAILED',
  AWS_CREDENTIALS_INVALID = 'AWS_CREDENTIALS_INVALID',
  SERVICE_UNAVAILABLE = 'SERVICE_UNAVAILABLE',
  TIMEOUT = 'TIMEOUT',
}

// User-friendly error messages
const errorMessages = {
  [AIErrorType.NOVA_CANVAS_FAILED]:
    'Unable to generate image. Please try again.',
  [AIErrorType.CLASSIFICATION_FAILED]:
    'Unable to classify image. Please check your connection.',
  [AIErrorType.AWS_CREDENTIALS_INVALID]:
    'Service configuration error. Please contact support.',
  [AIErrorType.SERVICE_UNAVAILABLE]:
    'AI services are temporarily unavailable. Please try again later.',
  [AIErrorType.TIMEOUT]: 'Request timed out. Please try again.',
};
```

**Retry Strategy:**

- Nova Canvas: 3 retries with exponential backoff (2s, 4s, 8s)
- Bedrock Agent: 2 retries with 3s, 6s delays
- Timeout limits: 30s for image generation, 15s for classification
- No retries for invalid credentials or malformed requests

### Context Management

**Conversation Context:**

- Keep context focused and relevant to the task
- Implement context window management
- Clear context when switching between different tasks
- Store important context in application state, not just AI memory

**Data Privacy:**

- Never send sensitive user data to AI models without explicit consent
- Implement data anonymization where appropriate
- Follow data retention policies for AI interactions
- Be transparent about AI usage with users

### Testing & Validation

**AI Output Validation:**

- Validate AI outputs against expected formats
- Test with edge cases and unexpected inputs
- Implement content filtering for inappropriate responses
- Monitor AI output quality over time

**Testing Strategies:**

- Unit tests for AI integration functions
- Integration tests for complete AI workflows
- Performance tests for response times and throughput
- User acceptance tests for AI-powered features

### Performance & Optimization

**Response Time Optimization:**

- Stream responses when possible for better user experience
- Implement caching for frequently requested AI operations
- Use appropriate model sizes for the task complexity
- Monitor and optimize prompt length

**Resource Management:**

- Implement request queuing for high-volume scenarios
- Set appropriate concurrency limits
- Monitor API usage and costs
- Optimize batch processing when applicable

## Pet Image AI Development Workflow

### Strands Agents Framework Development

1. **Agent Creation**: Implement classification agent using Strands framework
2. **Bedrock Deployment**: Package and deploy agent to Bedrock AgentCore Runtime
3. **Testing**: Validate agent responses with known cat/dog images
4. **Integration**: Connect Next.js API routes to deployed agent
5. **Monitoring**: Track classification accuracy and response times

### AWS Bedrock Integration

**Nova Canvas Integration:**

```typescript
// Example Nova Canvas API call
const generateImage = async (petType: 'cat' | 'dog') => {
  const prompt = petType === 'cat' ? catPrompt : dogPrompt;

  const request = {
    taskType: 'TEXT_IMAGE',
    textToImageParams: { text: prompt },
    imageGenerationConfig: {
      quality: 'standard',
      width: 512,
      height: 512,
      numberOfImages: 1,
    },
  };

  return await bedrockClient.invokeModel({
    modelId: 'amazon.nova-canvas-v1:0',
    body: JSON.stringify(request),
  });
};
```

**Bedrock Agent Integration:**

```typescript
// Example agent invocation
const classifyImage = async (imageData: string, userName: string) => {
  return await bedrockAgentClient.invokeAgent({
    agentId: process.env.BEDROCK_AGENT_ID,
    agentAliasId: process.env.BEDROCK_AGENT_ALIAS_ID,
    inputText: JSON.stringify({ imageData, task: 'classify_pet' }),
  });
};
```

### Monitoring & Quality Assurance

- **AWS CloudWatch**: Monitor API call success rates and latencies
- **Classification Accuracy**: Track confidence scores and user feedback
- **Cost Monitoring**: Monitor Bedrock usage and costs
- **Error Tracking**: Log and analyze AI service failures

### Documentation Requirements

- Document Strands Agent configuration and deployment steps
- Maintain AWS Bedrock model version compatibility
- Document error codes and user-facing messages
- Keep environment variable documentation updated

---

_Note: This guide is specifically configured for the Pet Image AI application using Amazon Bedrock services and Strands Agents Framework._
