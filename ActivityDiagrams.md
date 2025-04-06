
# Activity Workflow Modeling with Activity Diagrams

Workflow 1: Database Backup Process
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> CheckBackupSchedule
    CheckBackupSchedule --> BackupRequired: Backup is scheduled
    BackupRequired --> BackupInProgress
    BackupInProgress --> BackupSuccessful: Backup completed
    BackupInProgress --> BackupFailed: Backup failed
    BackupSuccessful --> End
    BackupFailed --> RetryBackup: Retry backup
    RetryBackup --> BackupInProgress
    RetryBackup --> End: Max retries reached

Explanation:
Start/End Nodes:

Start: The backup process starts based on the scheduled time.
End: The backup process either ends successfully or after a defined number of retries.

Actions:
CheckBackupSchedule: The system checks whether a backup is required based on the schedule.
BackupRequired: If a backup is required, the system initiates the backup process.
BackupInProgress: The system starts performing the backup.
BackupSuccessful: If the backup completes successfully, the process ends.
BackupFailed: If the backup fails, a retry mechanism is triggered.
RetryBackup: The system retries the backup process a defined number of times before aborting.

Decisions:
Is backup required?: Determines whether to start the backup based on the schedule.
Backup failed?: Determines whether to retry the backup if it fails.

Swimlanes:
System: The system checks the backup schedule, performs the backup, and retries if necessary.

Stakeholder Concerns:
The backup process aligns with the system administrator's requirement to automate backups efficiently, reducing manual oversight and ensuring timely recovery (FR-004).

Workflow 2: Database Recovery Process
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> DetectFailure
    DetectFailure --> RecoveryInitiated: Database failure detected
    RecoveryInitiated --> CheckReplicaAvailable
    CheckReplicaAvailable --> ReplicaAvailable: Replica ready
    CheckReplicaAvailable --> NoReplicaAvailable: No replica found
    ReplicaAvailable --> FailoverToReplica
    NoReplicaAvailable --> NotifyAdmin: Notify administrator
    FailoverToReplica --> RecoveryInProgress
    RecoveryInProgress --> RecoverySuccessful: Recovery completed
    RecoveryInProgress --> RecoveryFailed: Recovery failed
    RecoverySuccessful --> End
    RecoveryFailed --> RetryRecovery: Retry recovery
    RetryRecovery --> RecoveryInProgress
    RetryRecovery --> End: Max retries reached

Explanation:
Start/End Nodes:
Start: Recovery process triggered by a database failure.
End: Recovery process ends, either with success or failure.

Actions:
DetectFailure: The system detects a database failure.
RecoveryInitiated: The system initiates the recovery process.
CheckReplicaAvailable: The system checks if a replica database is available.
FailoverToReplica: If a replica is available, the system switches to it.
RecoveryInProgress: The system starts recovering the database.
RecoverySuccessful: The system successfully recovers the database.
RecoveryFailed: If the recovery fails, the system retries recovery.
RetryRecovery: The system retries the recovery process a defined number of times.

Decisions:
Is replica available?: Decides whether to failover to a replica or notify the administrator.

Swimlanes:
System: The system handles detection of failures, recovery initiation, replica checks, and recovery attempts.
Administrator: Notified if recovery fails and no replica is available.

Stakeholder Concerns:
Ensures the hospital's IT team has a reliable process for database recovery (FR-002) with fallback options when replicas are unavailable. The retry mechanism also ensures high availability and reliability of the system.

Workflow 3: User Account Registration
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> CollectUserData
    CollectUserData --> ValidateData
    ValidateData --> ValidData: Data is valid
    ValidateData --> InvalidData: Data is invalid
    ValidData --> CreateAccount
    InvalidData --> NotifyUser: Notify user of invalid data
    CreateAccount --> SendConfirmationEmail
    SendConfirmationEmail --> End

Explanation:
Start/End Nodes:

Start: User registration process starts.
End: Registration is complete.

Actions:
CollectUserData: The system collects user information (e.g., name, email, password).
ValidateData: The system validates the collected data for correctness.
CreateAccount: The system creates the user account.
SendConfirmationEmail: The system sends a confirmation email to the user.
NotifyUser: The system informs the user if their data is invalid.
Decisions:
Is data valid?: Determines whether the collected user data is valid.

Swimlanes:
User: Provides data for registration.
System: Handles data validation, account creation, and sending the confirmation email.

Stakeholder Concerns:
The diagram supports the hospital’s goal of ensuring a smooth and secure user account creation process, addressing user concerns about account registration security and validation (FR-008).

Workflow 4: Payment Processing
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> CollectPaymentDetails
    CollectPaymentDetails --> ValidatePayment
    ValidatePayment --> PaymentValid: Payment is valid
    ValidatePayment --> PaymentInvalid: Payment is invalid
    PaymentValid --> ProcessPayment
    PaymentInvalid --> NotifyUser: Notify user of invalid payment
    ProcessPayment --> ConfirmPayment
    ConfirmPayment --> End

Explanation:
Start/End Nodes:
Start: Payment processing starts.
End: Payment is successfully processed or fails.

Actions:
CollectPaymentDetails: The system collects payment information.
ValidatePayment: The system validates the payment details.
ProcessPayment: If the payment is valid, the system processes it.
ConfirmPayment: After successful payment, a confirmation is generated.
NotifyUser: The system notifies the user if the payment is invalid.

Decisions:
Is payment valid?: Determines whether the payment details are correct.

Swimlanes:
User: Provides payment details.
System: Validates payment, processes it, and sends notifications.

Stakeholder Concerns:
The payment process supports ensuring accurate payment validation and user notifications (FR-007), addressing the finance team's concern for secure transactions.

Workflow 5: Transaction Rollback on Failure
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> DetectFailure
    DetectFailure --> CheckRollbackPossible
    CheckRollbackPossible --> RollbackPossible: Rollback can be done
    CheckRollbackPossible --> NoRollbackPossible: No rollback possible
    RollbackPossible --> PerformRollback
    NoRollbackPossible --> NotifyAdmin: Notify admin for manual intervention
    PerformRollback --> End

Explanation:
Start/End Nodes:

Start: Rollback process is initiated.
End: Rollback is completed or manual intervention is required.

Actions:
DetectFailure: The system detects a failure in a transaction.
CheckRollbackPossible: The system checks if the transaction can be rolled back.
PerformRollback: If rollback is possible, the system performs it.
NotifyAdmin: If rollback isn't possible, the admin is notified.

Decisions:
Can rollback be performed?: Checks whether the transaction can be reversed.

Swimlanes:
System: Detects failure, checks rollback conditions, and performs rollback or notifies the administrator.

Stakeholder Concerns:
This workflow ensures transaction integrity (FR-007) and the system’s resilience to errors, providing hospital IT staff with a clear process for handling transaction failures.

Workflow 6: Security Alert Handling
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> DetectThreat
    DetectThreat --> AnalyzeThreat
    AnalyzeThreat --> ThreatValid: Threat is valid
    ThreatValid --> EscalateAlert
    AnalyzeThreat --> FalseAlarm: False alarm
    FalseAlarm --> End
    EscalateAlert --> ResolveThreat
    ResolveThreat --> End

Explanation:
Start/End Nodes:

Start: Security threat detection starts.
End: The process terminates after resolving or dismissing the threat.

Actions:
DetectThreat: The system detects a potential security threat.
AnalyzeThreat: The system analyzes the detected threat.
EscalateAlert: If the threat is valid, the system escalates the alert.
ResolveThreat: The system resolves the security threat.
FalseAlarm: If the threat is not valid, the system ends the process.

Decisions:
Is the threat valid?: Determines whether the threat requires further action.

Swimlanes:
System: Detects and analyzes threats, resolves them, or identifies false alarms.
Administrator: May be involved if escalation or manual resolution is required.

Stakeholder Concerns:
This workflow addresses security concerns (FR-009), ensuring that potential threats are handled promptly and appropriately.

Workflow 7: Database Replica Synchronization
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> CheckReplicaStatus
    CheckReplicaStatus --> SyncRequired: Replica needs syncing
    SyncRequired --> SyncInProgress
    SyncInProgress --> SyncCompleted: Sync successful
    SyncInProgress --> SyncFailed: Sync failed
    SyncCompleted --> End
    SyncFailed --> RetrySync: Retry sync
    RetrySync --> SyncInProgress
    RetrySync --> End: Max retries reached

Explanation:
Start/End Nodes:

Start: Synchronization process starts.
End: Synchronization completes successfully or after max retries.

Actions:
CheckReplicaStatus: The system checks if the replica needs synchronization.
SyncInProgress: The system performs the synchronization process.
SyncCompleted: The synchronization is completed successfully.
SyncFailed: If synchronization fails, a retry mechanism is triggered.
RetrySync: The system retries synchronization.

Decisions:
Does the replica need syncing?: Determines if synchronization is required.

Swimlanes:
System: Manages synchronization and retry logic.

Stakeholder Concerns:
Ensures the system is always up-to-date with the primary database, which is vital for maintaining data integrity and availability (FR-003).

Workflow 8: Notification System for Critical Alerts
Activity Diagram (Mermaid syntax):

stateDiagram-v2
    [*] --> Start
    Start --> DetectCriticalAlert
    DetectCriticalAlert --> GenerateAlertMessage
    GenerateAlertMessage --> SendNotification
    SendNotification --> End

Explanation:
Start/End Nodes:

Start: Alert generation starts.
End: Alert process ends after notification is sent.

Actions:
DetectCriticalAlert: The system detects a critical alert.
GenerateAlertMessage: The system creates a message to notify users.
SendNotification: The system sends the notification to the appropriate parties.

Swimlanes:
System: Detects critical alerts, generates messages, and sends notifications.

Stakeholder Concerns:
This workflow ensures that critical alerts are promptly communicated to the appropriate stakeholders (FR-009), maintaining high security and operational continuity.