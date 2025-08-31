# Recruit A Speaker
**AI-Powered Speaker Discovery & Outreach Automation**

***

## Set up and run (steps)

### **Prerequisites**
- n8n Workflow Platform (Cloud or Self-hosted)
- API credentials for: OpenAI, Tavily Search, Unipile (LinkedIn), Slack

### **Step 1: Environment Setup**
```bash
# Required API Keys
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
UNIPILE_API_KEY=your_unipile_key  
SLACK_BOT_TOKEN=xoxb-your-slack-token
```

### **Step 2: Slack App Configuration**
1. Create Slack App at https://api.slack.com/apps
2. Enable Bot Token Scopes: `chat:write`, `chat:write.public`, `users:read`
3. Configure Interactive Components webhook: `https://your-n8n-domain/webhook/slack-interactions`
4. Install to workspace and obtain bot token

### **Step 3: Unipile LinkedIn Setup**
1. Create account at https://unipile.com
2. Connect your LinkedIn account
3. Configure webhook for message responses: `https://your-n8n-domain/webhook/linkedin-response`
4. Obtain API credentials (DSN + API Key)

### **Step 4: Import Workflows**
1. Import `Recruit_A_Speaker_Stage1.json` into n8n
2. Import `Recruit_A_Speaker_Stage2.json` into n8n
3. Configure API credentials in both workflows
4. Update Slack user IDs and webhook URLs
5. Test both stages with sample data

***

## Problem Statement

B2B SaaS Marketers (and marketers in general) spend a lot of time and effort to recruit speakers for their webinars and events (on average 10-20 hours per booking).

***

## Users and Context

These webinars are typically monthly or quarterly requiring 1 speaker on average per webinar and conferences are annual or semi-annual requiring up to 10 speakers per event. The manual process involves a lot of time in searching over LinkedIn, speaker bureaus, Google, ChatGPT, researching their profiles and finding past speaking experience plus reviewing posts to find authenticity, followed by a cold-outreach process in order to book them.

This is a current spend in Marketing budgets - people spend up to $900 for a webinar speaker. There is a willingness to pay a small fee in order to get an authentic booking.

***

## Solution Overview with Diagram

With Agentic AI, contextual research, finding relevant speakers with experience and getting to them to recruit them should become WAY MORE easier - we have done a bit of customer research and found that there is a willingness to pay upon a successful outcome - HENCE we feel the time is NOW!!

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Event Form    │───▶│   STAGE 1:      │───▶│   Slack         │
│   Submission    │    │   LinkedIn      │    │   Approval      │
└─────────────────┘    │   Discovery     │    │   Interface     │
                       └─────────────────┘    └─────────────────┘
                                                        │
                                                [User clicks "Approve"]
                                                        │
                                                        ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Final Slack   │◀───│   STAGE 2:      │◀───│   Button        │
│   Outcome       │    │   LinkedIn      │    │   Trigger       │
│   Report        │    │   Outreach &    │    │   + Data        │
└─────────────────┘    │   Conversation  │    │   Retrieval     │
                       └─────────────────┘    └─────────────────┘
```

**Stage 1**: LinkedIn profile discovery via Tavily Search → AI-powered qualification → Slack approval interface with speaker profiles and approve buttons (event data stored in button values)

**Stage 2**: Slack button click triggers workflow → Event data retrieved from button payload → AI-generated personalized LinkedIn outreach → Automated conversation management (max 3 exchanges) → Success/failure analysis → Final outcome report to Slack

***

## Models and Data

**AI Models:**
- **OpenAI GPT-4.1**: Complex conversation analysis, strategic message generation, outcome classification
- **OpenAI GPT-5 Mini**: Profile processing, quick response analysis, routine text operations

**Data Sources:**
- **Tavily Search**: LinkedIn profile discovery and data extraction
- **Slack API**: Interactive approval interface and notifications
- **Unipile LinkedIn API**: Automated messaging and conversation management
- **User Input**: Event details (type, topic, date, location, audience) via web forms

**Data Flow**: Event details → LinkedIn discovery → Slack approval → Automated outreach → Conversation analysis → Outcome reporting

***

## Evaluation and Guardrails

**Hallucination Mitigation:**
- Human approval required before any LinkedIn outreach
- All AI-generated messages logged and reviewable
- 3-exchange hard limit prevents extended AI-only conversations
- Real-time Slack notifications for all AI interactions

**Bias Prevention:**
- Rule-based qualification scoring alongside AI analysis
- Diverse LinkedIn search parameters to avoid demographic bias
- Human oversight in final speaker selection decisions
- Regular review of AI message appropriateness across different cultures/industries

**Testing Scenarios:**
- Various event types (webinars, conferences, workshops)
- Different industries (tech, finance, healthcare, education)
- Geographic diversity (US, EU, APAC markets)
- Speaker experience levels (C-suite, mid-management, thought leaders)

***

## Known Limitations and Risks

**Technical Limitations:**
- Lower accuracy could impact trust (risk)
- Reputational risk if AI messes up the conversation
- Has not been tested for a variety of topics
- Need to expose the explainability of the results to the user

**Platform Risks:**
- LinkedIn Terms of Service violations may result in account suspension
- Automated messaging may be flagged as spam
- API rate limiting can slow down discovery process
- Dependence on third-party services (Unipile, Tavily) for core functionality

**AI-Specific Risks:**
- Conversation quality varies across industries and cultural contexts
- Limited to 3-exchange conversations may miss conversion opportunities
- AI-generated messages may lack human nuance in sensitive situations
- False positive/negative rates in success outcome classification

***

## Team

**Sandeep PBK** - Technical Lead & AI Architecture  
Email: [p.krishnasandeep5@gmail.com](mailto:p.krishnasandeep5@gmail.com)  
Role: System design, AI model integration, workflow orchestration

**Shailesh Hegde** - Product Strategy & Integration  
Email: [hegde.shailesh@gmail.com](mailto:hegde.shailesh@gmail.com)  
Role: LinkedIn integration, conversation flow design, user experience optimization

***

**© 2024 Team Turbine | Recruit A Speaker - AI-Powered Event Speaker Automation**
