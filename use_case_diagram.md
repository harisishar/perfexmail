# PERFEXMAIL Use Case Diagram

## System Use Case Overview

```mermaid
graph LR
    %% Left Side Actors
    Marketer[👤 Marketer<br/>Team Member]
    Designer[👤 Designer<br/>Team Member]
    TeamLead[👤 Team Lead]
    System[⚙️ System<br/>Automated]

    %% Right Side Actors
    Admin[👤 Administrator]
    ESP[🌐 Email Service<br/>Provider]

    subgraph PERFEXMAIL_System["🎯 PERFEXMAIL Email Marketing Platform"]
        %% Core Email Marketing Use Cases
        UC001[UC001: Manage Email<br/>Campaigns]
        UC002[UC002: Manage Subscriber<br/>Lists]
        UC003[UC003: Manage Email<br/>Templates]
        UC004[UC004: Automate Email<br/>Workflows]
        UC008[UC008: View Reports<br/>& Analytics]
        UC009[UC009: Manage Forms]

        %% Administrative Use Cases
        UC005[UC005: Manage Users &<br/>Team Accounts]
        UC006[UC006: System Administration<br/>& Configuration]
        UC007[UC007: Manage Usage Plans<br/>& Limits]
        UC010[UC010: Manage Sending<br/>Infrastructure]
        UC011[UC011: Manage Blacklists]
    end

    %% Marketer Relationships
    Marketer --> UC001
    Marketer --> UC002
    Marketer --> UC003
    Marketer --> UC004
    Marketer --> UC008
    Marketer --> UC009

    %% Designer Relationships
    Designer --> UC003
    Designer --> UC009

    %% Team Lead Relationships
    TeamLead --> UC001
    TeamLead --> UC002
    TeamLead --> UC003
    TeamLead --> UC004
    TeamLead --> UC008
    TeamLead --> UC007
    TeamLead --> UC005

    %% Administrator Relationships
    UC005 --> Admin
    UC006 --> Admin
    UC007 --> Admin
    UC010 --> Admin
    UC011 --> Admin
    UC001 --> Admin
    UC002 --> Admin
    UC003 --> Admin
    UC004 --> Admin
    UC008 --> Admin

    %% System/Automated Relationships
    System --> UC004
    System --> UC010
    System --> UC011

    %% ESP Relationships
    UC010 --> ESP

    %% Include Relationships
    UC001 -.->|includes| UC004
    UC002 -.->|includes| UC011
    UC004 -.->|includes| UC003
    UC010 -.->|includes| UC011

    %% Actor Inheritance
    TeamLead -.->|inherits| Marketer

    %% Styling
    classDef actor fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#000
    classDef usecase fill:#f3e5f5,stroke:#4a148c,stroke-width:2px,color:#000
    classDef system fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#000
    classDef admin fill:#ffebee,stroke:#b71c1c,stroke-width:2px,color:#000

    class Marketer,Designer,TeamLead actor
    class Admin admin
    class ESP,System system
    class UC001,UC002,UC003,UC004,UC008,UC009 usecase
    class UC005,UC006,UC007,UC010,UC011 admin
```

## Actor Descriptions

### **Primary Actors (Human Users)**

| Actor | Description | Access Level |
|-------|-------------|--------------|
| **Marketer (Team Member)** | Core user who creates and manages email marketing campaigns, subscriber lists, and views performance analytics | Standard User |
| **Designer (Team Member)** | Specializes in creating and customizing email templates and visual content for campaigns | Standard User |
| **Team Lead** | Senior team member with additional permissions to manage team resources and view team-wide analytics | Elevated User |
| **Administrator** | System administrator with full access to platform configuration, user management, and infrastructure settings | Admin User |

### **Secondary Actors (External Systems)**

| Actor | Description | Interaction Type |
|-------|-------------|------------------|
| **Email Service Provider (ESP)** | External email delivery services (SendGrid, SMTP servers) that handle email sending and provide delivery feedback | System Integration |
| **System (Automated)** | Automated system processes that handle background tasks, monitoring, and scheduled operations | Internal Automation |

## Use Case Categories

### **📧 Core Email Marketing Use Cases**
- **UC001: Manage Email Campaigns** - Create, edit, schedule, and send email campaigns
- **UC002: Manage Subscriber Lists** - Organize and maintain subscriber databases
- **UC003: Manage Email Templates** - Design and manage reusable email templates
- **UC004: Automate Email Workflows** - Create and manage automated email sequences
- **UC008: View Reports & Analytics** - Access performance metrics and campaign analytics
- **UC009: Manage Forms** - Create and manage subscription and lead capture forms

### **👥 User & Team Management Use Cases**
- **UC005: Manage Users & Team Accounts** - User registration, authentication, and profile management
- **UC007: Manage Usage Plans & Limits** - Monitor and control resource usage and limits

### **⚙️ System Administration Use Cases**
- **UC006: System Administration & Configuration** - Configure system settings and preferences
- **UC010: Manage Sending Infrastructure** - Configure email sending servers and domain authentication
- **UC011: Manage Blacklists** - Maintain global email blacklists for compliance

## Relationship Types

### **Association Relationships**
- **Solid arrows (→)**: Direct interaction between actor and use case
- **Dotted arrows (-.->)**: Include relationships showing use case dependencies

### **Inheritance Relationships**
- **Team Lead inherits from Marketer**: Team Lead has all Marketer permissions plus additional elevated access

### **Include Relationships**
- **UC001 includes UC004**: Campaign management includes automation capabilities
- **UC002 includes UC011**: List management includes blacklist checking
- **UC004 includes UC003**: Automation workflows include template management
- **UC010 includes UC011**: Infrastructure management includes blacklist handling

## Security and Access Control

### **Permission Levels**
1. **Standard User** (Marketer, Designer): Core email marketing functionality
2. **Elevated User** (Team Lead): Team resource management and oversight
3. **Admin User** (Administrator): Full system configuration and user management
4. **System Integration**: Automated processes and external service interactions

### **Multi-Tenant Isolation**
- All use cases respect team-based data isolation
- Users can only access data within their assigned team(s)
- Administrators have cross-team visibility for system management

This use case diagram provides a comprehensive overview of the PERFEXMAIL system's functionality, showing how different types of users interact with various features while maintaining appropriate access controls and security boundaries. 