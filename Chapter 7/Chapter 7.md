```
tell application "Mail"
    set theMessages to (every message of inbox whose read status is false)
    repeat with aMessage in theMessages
        set senderAddress to extract address from sender of aMessage
        set subjectLine to subject of aMessage
        
        -- Create a new outgoing message
        set replyMessage to make new outgoing message with properties {subject:"Re: " & subjectLine, content:"Thank you for reaching out. I am currently unavailable but will get back to you soon.", visible:true}
        
        -- Set the recipient
        tell replyMessage
            make new to recipient at end of to recipients with properties {address:senderAddress}
            send
        end tell
        
        -- Mark the email as read after replying
        set read status of aMessage to true
    end repeat
end tell
```


```
set recipientList to "/Users/username/Documents/emails.txt" -- Path to the file containing email addresses
set emailSubject to "Important Update"
set emailBody to "Hello,\n\nThis is an automated email. Please find the latest update attached.\n\nBest regards."

-- Read email addresses from file
set recipientEmails to paragraphs of (do shell script "cat " & quoted form of recipientList)

tell application "Mail"
    repeat with recipient in recipientEmails
        set newMessage to make new outgoing message with properties {subject:emailSubject, content:emailBody, visible:true}
        tell newMessage
            make new to recipient at end of to recipients with properties {address:recipient}
            send
        end tell
    end repeat
end tell

```


```
tell application "Mail"
    set targetMailbox to mailbox "Reports" of account "iCloud"
    set theMessages to (every message of inbox whose sender contains "reports@example.com")
    
    repeat with aMessage in theMessages
        move aMessage to targetMailbox
    end repeat
end tell

```


```
tell application "Mail"
    set invoiceMailbox to mailbox "Invoices" of account "iCloud"
    set meetingMailbox to mailbox "Meetings" of account "iCloud"
    
    set invoiceMessages to (every message of inbox whose subject contains "Invoice")
    set meetingMessages to (every message of inbox whose subject contains "Meeting")
    
    repeat with aMessage in invoiceMessages
        move aMessage to invoiceMailbox
    end repeat
    
    repeat with aMessage in meetingMessages
        move aMessage to meetingMailbox
    end repeat
end tell

```

```
set outputFile to "/Users/username/Documents/orders.txt"

tell application "Mail"
    set orderMessages to (every message of inbox whose sender contains "orders@example.com")
    
    repeat with aMessage in orderMessages
        set orderSubject to subject of aMessage
        set orderNumber to extractWord(2, orderSubject) -- Assuming order number is the second word in subject
        
        do shell script "echo " & orderNumber & " >> " & quoted form of outputFile
    end repeat
end tell

-- Helper function to extract a specific word
on extractWord(n, text)
    set wordList to words of text
    if (count of wordList) ≥ n then
        return item n of wordList
    else
        return "N/A"
    end if
end extractWord

```


```
tell application "Reminders"
    set todayDate to (current date)
    set newReminder to make new reminder with properties {name:"Team Meeting", due date:todayDate + (9 * hours)}
end tell

```


```
set response to display dialog "Do you want to continue the process?" buttons {"Cancel", "Proceed"} default button "Proceed"

if response = "Proceed" then
    display notification "Process started!" with title "System Alert"
else
    display notification "Process canceled!" with title "System Alert"
end if

```

```
set slackWebhook to "https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
set message to "A new file has been uploaded to the server."

do shell script "curl -X POST -H 'Content-type: application/json' --data '{\"text\": \"" & message & "\"}' " & slackWebhook

```


```
set currentDate to do shell script "date"
set systemUptime to do shell script "uptime"
set diskSpace to do shell script "df -h / | tail -1 | awk '{print $4}'"

set reportData to "Report Date: " & currentDate & return & ¬
    "System Uptime: " & systemUptime & return & ¬
    "Available Disk Space: " & diskSpace & return & ¬
    "-------------------------------------------" & return

```


```
set reportHeader to "====== SYSTEM REPORT ======" & return
set reportFooter to return & "====== END OF REPORT ======" & return

set formattedReport to reportHeader & reportData & reportFooter

```


```
====== SYSTEM REPORT ======
Report Date: Mon Mar 25 10:30:15 2025
System Uptime: 10:30  up 3 days,  5:42, 2 users, load averages: 1.78 1.90 2.00
Available Disk Space: 250G
-------------------------------------------
====== END OF REPORT ======

```


```
set emailSubject to "Daily System Report"
set emailBody to formattedReport
set recipientEmail to "admin@example.com"

tell application "Mail"
    set newMessage to make new outgoing message with properties {subject:emailSubject, content:emailBody, visible:true}
    tell newMessage
        make new to recipient at end of to recipients with properties {address:recipientEmail}
        send
    end tell
end tell

```


```
set recipientNumber to "+1234567890"
set reportMessage to formattedReport

tell application "Messages"
    set targetBuddy to buddy recipientNumber of service "iMessage"
    send reportMessage to targetBuddy
end tell

```



