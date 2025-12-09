---
title: "Blog 3"
date: 
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# How PropHero built an intelligent property investment advisor with continuous evaluation using Amazon Bedrock

PropHero is a leading property wealth management service that democratizes access to intelligent property investment advice through big data, AI, and machine learning (ML). For the Spanish and Australian consumer base, PropHero needed an AI-powered advisory system that could engage customers in accurate property investment discussions. The goal was to provide personalized investment insights and to guide and assist users at every stage of their investment journey: from understanding the process, gaining visibility into timelines, securely uploading documents, to tracking progress in real time.

PropHero collaborated with the AWS Generative AI Innovation Center to implement an intelligent property investment advisor using AWS generative AI services with continuous evaluation. The solution helps users engage in natural language conversations about property investment strategies and receive personalized recommendations based on PropHero’s comprehensive market knowledge.

In this post, we explore how we built a multi-agent conversational AI system using Amazon Bedrock that delivers knowledge-grounded property investment advice. We explore the agent architecture, model selection strategy, and comprehensive continuous evaluation system that facilitates quality conversations while facilitating rapid iteration and improvement.

## The challenge: Making property investment knowledge more accessible
The area of property investment presents numerous challenges for both novice and experienced investors. Information asymmetry creates barriers where comprehensive market data remains expensive or inaccessible. Traditional investment processes are manual, time-consuming, and require extensive market knowledge to navigate effectively. For the Spanish and Australian consumers specifically, we needed to build a solution that could provide accurate, contextually relevant property investment advice in Spanish while handling complex, multi-turn conversations about investment strategies. The system needed to maintain high accuracy while delivering responses at scale, continuously learning and improving from customer interactions. Most importantly, it needed to assist users across every phase of their journey, from initial onboarding through to final settlement, ensuring comprehensive support throughout the entire investment process.

## Solution overview
We built a complete end-to-end solution using AWS generative AI services, architected around a multi-agent AI advisor with integrated continuous evaluation. The system provides seamless data flow from ingestion through intelligent advisory conversations with real-time quality monitoring. The following diagram illustrates this architecture.

![System Architecture](/images/blog-3-1.jpeg)

The solution architecture consists of four virtual layers, each serving specific functions in the overall system design.

## Data foundation layer
The data foundation provides the storage and retrieval infrastructure for system components:

* Amazon DynamoDB – Fast storage for conversation history, evaluation metrics, and user interaction data
* Amazon Relational Database (Amazon RDS) for PostgreSQL – A PostgreSQL database storing LangFuse observability data, including large language model (LLM) traces and latency metrics
* Amazon Simple Storage Service (Amazon S3) – A central data lake storing Spanish FAQ documents, property investment guides, and conversation datasets
## Multi-agent AI layer
The AI processing layer encompasses the core intelligence components that power the conversational experience:

* Amazon Bedrock – Foundation models (FMs) such as LLMs and rerankers powering specialized agents
* Amazon Bedrock Knowledge Bases – Semantic search engine with semantic chunking for FAQ-style content
* LangGraph – Orchestration of multi-agent workflows and conversation state management
* AWS Lambda – Serverless functions executing multi-agent logic and retrival of user information for richer context
## Continuous evaluation layer
The evaluation infrastructure facilitates continuous quality monitoring and improvement through these components:

* Amazon CloudWatch – Real-time monitoring of quality metrics with automated alerting and threshold management
* Amazon EventBridge – Real-time event triggers for conversation completion and quality assessment
* AWS Lambda – Automated evaluation functions measuring context relevance, response groundedness, and goal accuracy
* Amazon QuickSight – Interactive dashboards and analytics for monitoring the respective metrics
## Application and integration layer
The integration layer provides secure interfaces for external communication:

* Amazon API Gateway – Secure API endpoints for conversational interface and evaluation webhooks
## Multi-agent AI advisor architecture
The intelligent advisor uses a multi-agent system orchestrated through LangGraph, which sits in a single Lambda function, where each agent is optimized for specific tasks. The following diagram shows the communication flow among the various agents within the Lambda function.

![System Architecture](/images/blog-3-2.png)

## Agent composition and model selection
Our model selection strategy involved extensive testing to match each component’s computational requirements with the most cost-effective Amazon Bedrock model. We evaluated factors including response quality, latency requirements, and cost per token to determine optimal model assignments for each agent type.Each component in the system uses the most appropriate model for its designated function, as outlined in the following table.

# End-to-end conversation flow
The conversation processing follows a structured workflow that facilitates accurate responses while maintaining quality standards:

1. User queries enter through API Gateway and are routed to the router agent.
2. The router agent determines the appropriate specialized agent based on query analysis.
3. User information is retrieved at the start for richer context and knowledge-intensive queries trigger the retriever to access the Amazon Bedrock knowledge base.
4. Specialized agents process queries with retrieved user information and relevant context from the knowledge base.
5. The response agent formats and generates the final user-facing response with the appropriate tone.
6. Parallel evaluation processes assess context relevance, response groundedness, and goal accuracy.
Conversation data is stored in DynamoDB for analysis and improvement.
## Amazon Bedrock Knowledge Bases configuration
The knowledge base uses several AWS services for optimal performance:

* Data source – S3 bucket
* Chunking strategy – Semantic chunking optimized for FAQ-style content
* Embedding model – Cohere Embed Multilingual v3 for Spanish understanding
* Reranker – Cohere Rerank 3.5 for reranking retrieved Spanish content
* Vector database – Amazon OpenSearch Serverless for scalable semantic search
## Sample conversation experience
The system handles natural Spanish conversations seamlessly. For example:

Usuario: “Hola, ¿qué es PropHero exactamente?”

Asistente: “¡Hola! PropHero es una plataforma que te permite crear, optimizar y crecer tu patrimonio inmobiliario delegando todo el proceso en nuestro equipo de profesionales…”

Usuario: “¿Y cómo funciona en la práctica?”

Asistente: “Es muy sencillo. Comenzamos con una sesión con tu Property Coach para definir tu estrategia de inversión personalizada…”

## Integrated continuous evaluation system
The continuous evaluation system is integrated into the architecture, operating as a core component. This approach supports quality monitoring in real-time alongside conversation processing.

### Evaluation metrics
We used the following metrics from the Ragas library for evaluation:

* Context Relevance (0–1) – Measures the relevance of retrieved context to user queries, evaluating RAG system effectiveness
* Response Groundedness (0–1) – Makes sure responses are factually accurate and derived from PropHero’s official information
* Agent Goal Accuracy (0–1) – Binary measure of whether responses successfully address user investment goals
### Real-time evaluation workflow
The evaluation system operates seamlessly within the conversation architecture:

* Amazon DynamoDB Streams triggers – Conversation data written to DynamoDB automatically triggers a Lambda function for evaluation through Amazon DynamoDB Streams
* Parallel processing – Lambda functions execute evaluation logic in parallel with response delivery
* Multi-dimensional assessment – Each conversation is evaluated across three key dimensions simultaneously
* Intelligent scoring with LLM-as-a-judge – Anthropic’s Claude 3.5 Haiku provides consistent evaluation as an LLM judge, offering standardized assessment criteria across conversations.
* Monitoring and analytics – CloudWatch captures metrics from the evaluation process, and QuickSight provides dashboards for trend analysis
The following diagram provides an overview of the Lambda function responsible for continuous evaluation.
![System Architecture](/images/blog-3-3.png)

## Implementation insights and best practices
Our development journey involved a 6-week iterative process with PropHero’s technical team. We conducted testing across different model combinations and evaluated chunking strategies using real customer FAQ data. This journey revealed several architectural optimizations that enhanced system performance, achieved significant cost reductions, and improved user experience.

### Model selection strategy
Our approach to model selection demonstrates the importance of matching model capabilities to specific tasks. By using Amazon Nova Lite for simpler tasks and Amazon Nova Pro for complex reasoning, the solution achieves optimal cost-performance balance while maintaining high accuracy standards.

### Chunking and retrieval optimization
Semantic chunking proved superior to hierarchical and fixed chunking approaches for FAQ-style content. The Cohere Rerank 3.5 model enabled the system to use fewer chunks (10 vs. 20) while maintaining accuracy, reducing latency and cost.

### Multilingual capabilities
The system effectively handles Spanish and English queries by using FMs that support Spanish language on Amazon Bedrock.

### Business impact
The PropHero AI advisor delivered measurable business value:

* Enhanced customer engagement – A 90% goal accuracy rate makes sure customers receive relevant, actionable property investment advice. Over 50% of our users (and over 70% of paid users) are actively using the AI advisor.
* Operational efficiency – Automated responses to common questions reduced customer service workload by 30%, freeing staff to focus on complex customer needs.
* Scalable growth – The serverless architecture automatically scales to handle increasing customer demand without manual intervention.
* Cost optimization – Strategic model selection achieved high performance while reducing AI costs by 60% compared to using premium models throughout.
* Consumer base expansion – Successful Spanish language support enabled PropHero’s expansion into the Spanish consumer base with localized expertise.
## Conclusion
The PropHero AI advisor demonstrates how AWS generative AI services can be used to create intelligent, context-aware conversational agents that deliver real business value. By combining a modular agent architecture with a robust evaluation system, PropHero has created a solution that enhances customer engagement while providing accurate and relevant responses.The comprehensive evaluation pipeline has been particularly valuable, providing clear metrics for measuring conversation quality and guiding ongoing improvements. This approach makes sure the AI advisor will continue to evolve and improve over time.For more information about building multi-agent AI advisors with continuous evaluation, refer to the following resources:

* Retrieve data and generate AI responses with Amazon Bedrock Knowledge Bases – With Amazon Bedrock Knowledge Bases, you can implement semantic search with chunking strategies
* LangGraph – LangGraph can help you build multi-agent workflows
* Ragas – Ragas offers comprehensive LLM evaluation metrics, including context relevance, groundedness, and goal accuracy used in this implementation

To learn more about the Generative AI Innovation Center, get in touch with your account team.