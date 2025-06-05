```mermaid
classDiagram
    class User {
        +String id
        +String email
        +String password
        +String apiToken
        +String status
        +DateTime createdAt
        +authenticate()
        +generateApiToken()
        +updateProfile()
        +resetPassword()
    }
    
    class Admin {
        +String id
        +String userId
        +String firstName
        +String lastName
        +String timezone
        +String status
        +manageUsers()
        +configureSending()
        +viewSystemLogs()
        +managePlans()
    }
    
    class Team {
        +String id
        +String userId
        +String firstName
        +String lastName
        +String timezone
        +String status
        +JSON usageLimits
        +createCampaign()
        +manageSubscribers()
        +viewReports()
        +checkUsageLimits()
    }
    
    class Subscription {
        +String id
        +String teamId
        +String planId
        +String status
        +DateTime currentPeriodEndsAt
        +JSON usageCounts
        +updateUsage()
        +checkLimits()
        +renewSubscription()
    }
    
    class Plan {
        +String id
        +String name
        +JSON features
        +JSON limits
        +Decimal price
        +String status
        +validateUsage()
        +getFeatureAccess()
        +calculateCost()
    }
    
    class MailList {
        +String id
        +String teamId
        +String name
        +String fromEmail
        +String fromName
        +String description
        +Boolean sendWelcomeEmail
        +String status
        +addSubscriber()
        +removeSubscriber()
        +getSegments()
        +exportSubscribers()
    }
    
    class Subscriber {
        +String id
        +String mailListId
        +String email
        +String status
        +String source
        +String ipAddress
        +DateTime subscribedAt
        +updateStatus()
        +getEngagementScore()
        +getActivityHistory()
        +unsubscribe()
    }
    
    class Campaign {
        +String id
        +String teamId
        +String mailListId
        +String segmentId
        +String name
        +String subject
        +String htmlContent
        +String plainContent
        +String status
        +DateTime scheduledAt
        +DateTime sentAt
        +Boolean trackOpen
        +Boolean trackClick
        +send()
        +schedule()
        +getStatistics()
        +pause()
        +resume()
        +clone()
    }
    
    class Template {
        +String id
        +String teamId
        +String name
        +String content
        +String category
        +String image
        +Boolean shared
        +DateTime createdAt
        +preview()
        +duplicate()
        +share()
        +validateContent()
    }
    
    class Automation {
        +String id
        +String teamId
        +String mailListId
        +String name
        +String status
        +JSON workflowData
        +String timezone
        +activate()
        +pause()
        +getStatistics()
        +addEmail()
        +setTrigger()
        +validateWorkflow()
    }
    
    class AutomationEmail {
        +String id
        +String automationId
        +String subject
        +String content
        +Integer delayValue
        +String delayUnit
        +send()
        +getStatistics()
    }
    
    class TrackingLog {
        +String id
        +String campaignId
        +String subscriberId
        +String email
        +String status
        +DateTime sentAt
        +String messageId
        +recordDelivery()
        +recordBounce()
        +getDeliveryStatus()
    }
    
    class OpenLog {
        +String id
        +String trackingLogId
        +String userAgent
        +String ipAddress
        +DateTime openedAt
        +String location
        +recordOpen()
        +getOpenDetails()
    }
    
    class ClickLog {
        +String id
        +String trackingLogId
        +String url
        +String ipAddress
        +DateTime clickedAt
        +String userAgent
        +recordClick()
        +getClickDetails()
    }
    
    class BounceLog {
        +String id
        +String trackingLogId
        +String bounceType
        +String reason
        +DateTime bouncedAt
        +processBounce()
        +updateSubscriberStatus()
    }
    
    class SendingServer {
        +String id
        +String name
        +String type
        +String host
        +Integer port
        +String username
        +String password
        +String apiKey
        +Boolean isActive
        +JSON settings
        +testConnection()
        +sendEmail()
        +getQuota()
    }
    
    class Segment {
        +String id
        +String mailListId
        +String name
        +JSON conditions
        +Integer subscriberCount
        +DateTime updatedAt
        +getSubscribers()
        +updateCount()
        +validateConditions()
    }

    User "1" --> "*" Admin : can_be
    User "1" --> "*" Team : creates
    Team "1" --> "1" Subscription : has
    Subscription "*" --> "1" Plan : subscribes_to
    Team "1" --> "*" MailList : owns
    Team "1" --> "*" Campaign : creates
    Team "1" --> "*" Template : creates
    Team "1" --> "*" Automation : creates
    MailList "1" --> "*" Subscriber : contains
    MailList "1" --> "*" Segment : has
    Campaign "*" --> "1" MailList : targets
    Campaign "*" --> "0..1" Segment : targets
    Campaign "1" --> "*" TrackingLog : generates
    Automation "*" --> "1" MailList : targets
    Automation "1" --> "*" AutomationEmail : contains
    TrackingLog "1" --> "*" OpenLog : tracks_opens
    TrackingLog "1" --> "*" ClickLog : tracks_clicks
    TrackingLog "1" --> "*" BounceLog : tracks_bounces
    Subscriber "1" --> "*" TrackingLog : receives_emails

    ```