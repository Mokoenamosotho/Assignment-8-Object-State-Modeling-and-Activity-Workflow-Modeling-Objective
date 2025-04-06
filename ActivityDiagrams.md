# Activity Workflow Modeling with Activity Diagrams

8 complex workflows from your system

1. User Registration and Verification, 
2. Submit Recovery Request, 
3. Review and Approve Recovery Request, 
4. Execute Recovery Operation, 
5. Predict System Failure, 
6. Incident Management, 
7. AI Model Training and Deployment, 
8. Automated Notification Dispatch

Workflow 1: User Registration
Mermaid Diagram

%%{init: {'theme': 'default'}}%%
flowchart TD
    subgraph User
        A1(Start) --> A2[Fill Registration Form]
        A2 --> A3[Submit Form]
    end

    subgraph System
        A3 --> B1[Validate Data]
        B1 --> B2{Is Data Valid?}
        B2 -- No --> B3[Show Error]
        B2 -- Yes --> B4[Create Account]
        B4 --> B5[Send Verification Email]
        B5 --> A4[End]
    end


Explanation
This workflow captures the registration process. It ensures data validity before creating an account. The system sends a verification email to complete the process. This ensures secure onboarding, aligning with the security stakeholder requirement.

Workflow 2: Submit Recovery Request
Mermaid Diagram

flowchart TD
    subgraph User
        A1(Start) --> A2[Enter Recovery Details]
        A2 --> A3[Submit Request]
    end

    subgraph System
        A3 --> B1[Check Dependencies]
        B1 --> B2{All Requirements Met?}
        B2 -- No --> B3[Show Missing Info]
        B2 -- Yes --> B4[Forward to Reviewer]
        B4 --> A4[End]
    end

Explanation
This diagram handles submitting database recovery requests. Stakeholders are concerned about incomplete inputs; this workflow ensures validation before processing, improving reliability.

Workflow 3: Review and Approve Request
Mermaid Diagram

flowchart TD
    subgraph Reviewer
        A1(Start) --> A2[Open Pending Request]
        A2 --> A3[Evaluate Details]
        A3 --> A4{Approve?}
        A4 -- Yes --> A5[Approve Request]
        A4 -- No --> A6[Reject Request]
        A5 --> A7[End]
        A6 --> A7
    end

Explanation
The approval process is critical for governance. It addresses concerns about unauthorized execution. This diagram supports traceability and accountability.

Workflow 4: Execute Recovery
Mermaid Diagram

flowchart TD
    subgraph System
        A1(Start) --> A2[Prepare Recovery Environment]
        A2 --> A3[Restore Data from Backup]
        A3 --> A4{Success?}
        A4 -- No --> A5[Trigger Alert]
        A4 -- Yes --> A6[Run Validation Checks]
        A6 --> A7[Log Completion]
        A5 --> A7
        A7 --> A8[End]
    end

Explanation
This workflow safeguards successful recovery. It checks system restoration and logs results, meeting the system admin’s need for transparency and error handling.

Workflow 5: Predict Failure
Mermaid Diagram

flowchart TD
    subgraph System
        A1(Start) --> A2[Collect Monitoring Data]
        A2 --> A3[Apply AI Model]
        A3 --> A4{Failure Likely?}
        A4 -- No --> A5[Continue Monitoring]
        A4 -- Yes --> A6[Trigger Alert]
        A5 --> A7[End]
        A6 --> A7
    end

Explanation
This supports predictive maintenance. AI forecasts potential failures early, helping system admins mitigate risks proactively.

Workflow 6: Incident Management
Mermaid Diagram

flowchart TD
    subgraph User
        A1(Start) --> A2[Report Incident]
    end

    subgraph IT Team
        A2 --> B1[Assign Technician]
        B1 --> B2[Investigate Issue]
        B2 --> B3{Resolved?}
        B3 -- No --> B2
        B3 -- Yes --> B4[Close Incident]
        B4 --> A3[End]
    end

Explanation
This looped workflow handles incident management with continuous assessment until resolution. Meets operational continuity goals.

Workflow 7: Model Training
Mermaid Diagram

flowchart TD
    subgraph Data Scientist
        A1(Start) --> A2[Prepare Training Data]
        A2 --> A3[Train AI Model]
        A3 --> A4[Evaluate Accuracy]
        A4 --> A5{Accuracy > 90%?}
        A5 -- Yes --> A6[Deploy Model]
        A5 -- No --> A7[Tune Parameters]
        A7 --> A3
        A6 --> A8[End]
    end

Explanation
This iteration-focused process ensures that AI models meet performance standards before deployment. Supports stakeholder concerns over false positives.

Workflow 8: Send Notifications
Mermaid Diagram

flowchart TD
    subgraph System
        A1(Start) --> A2[Check Triggers]
        A2 --> A3{Trigger Type?}
        A3 -- Backup Complete --> A4[Send Success Notification]
        A3 -- Recovery Failed --> A5[Send Alert]
        A4 --> A6[Log Notification]
        A5 --> A6
        A6 --> A7[End]
    end

Explanation
Ensures timely communication of backup and recovery statuses. Logs help for auditing. Meets stakeholder expectations for transparency and responsiveness.