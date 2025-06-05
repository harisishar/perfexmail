```mermaid
erDiagram
    USERS {
        uuid id PK
        string email UK
        string password
        string status
        timestamp created_at
        timestamp updated_at
    }
    
    TEAMS {
        uuid id PK
        uuid user_id FK
        string first_name
        string last_name
        string timezone
        json usage_limits
        string status
        timestamp created_at
    }
    
    SUBSCRIPTIONS {
        uuid id PK
        uuid team_id FK
        uuid plan_id FK
        string status
        json usage_counts
        timestamp current_period_ends_at
    }
    
    PLANS {
        uuid id PK
        string name
        json features
        json limits
        decimal price
        string status
    }
    
    MAIL_LISTS {
        uuid id PK
        uuid team_id FK
        string name
        string from_email
        string from_name
        text description
        boolean send_welcome_email
        string status
    }
    
    SUBSCRIBERS {
        uuid id PK
        uuid mail_list_id FK
        string email UK
        string status
        string from
        string ip
        timestamp subscribed_at
    }
    
    CAMPAIGNS {
        uuid id PK
        uuid team_id FK
        uuid mail_list_id FK
        uuid segment_id FK
        string name
        string subject
        text html_content
        text plain_content
        string status
        timestamp scheduled_at
        timestamp sent_at
    }
    
    TEMPLATES {
        uuid id PK
        uuid team_id FK
        string name
        text content
        string category
        boolean shared
        timestamp created_at
    }
    
    AUTOMATIONS {
        uuid id PK
        uuid team_id FK
        uuid mail_list_id FK
        string name
        string status
        json workflow_data
        string timezone
    }
    
    AUTOMATION_EMAILS {
        uuid id PK
        uuid automation_id FK
        string subject
        text content
        integer delay_value
        string delay_unit
    }
    
    TRACKING_LOGS {
        uuid id PK
        uuid campaign_id FK
        uuid subscriber_id FK
        string email
        string status
        timestamp sent_at
    }
    
    OPEN_LOGS {
        uuid id PK
        uuid tracking_log_id FK
        string user_agent
        string ip_address
        timestamp opened_at
    }
    
    CLICK_LOGS {
        uuid id PK
        uuid tracking_log_id FK
        string url
        string ip_address
        timestamp clicked_at
    }
    
    USERS ||--o{ TEAMS : "has"
    TEAMS ||--|| SUBSCRIPTIONS : "has"
    SUBSCRIPTIONS }o--|| PLANS : "uses"
    TEAMS ||--o{ MAIL_LISTS : "owns"
    MAIL_LISTS ||--o{ SUBSCRIBERS : "contains"
    TEAMS ||--o{ CAMPAIGNS : "creates"
    CAMPAIGNS }o--|| MAIL_LISTS : "targets"
    TEAMS ||--o{ TEMPLATES : "owns"
    TEAMS ||--o{ AUTOMATIONS : "creates"
    AUTOMATIONS ||--o{ AUTOMATION_EMAILS : "contains"
    CAMPAIGNS ||--o{ TRACKING_LOGS : "generates"
    TRACKING_LOGS ||--o{ OPEN_LOGS : "tracks"
    TRACKING_LOGS ||--o{ CLICK_LOGS : "tracks"
