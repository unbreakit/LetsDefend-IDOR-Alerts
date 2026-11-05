# LetsDefend Alert: Possible IDOR Attacks

## IDOR Attacks (Indirect Object Reference) 

Indirect Object Reference attacks involve changing parameters inside a URL.  If the web server doesn't verify that the user is supposed to view the content associated with that changed parameter, an unauthorized user can get access to content they wouldn't normally get access too.

## Alert 1

<img width="1566" height="747" alt="Screenshot 2026-11-04 125659" src="https://github.com/user-attachments/assets/7273d827-1bcc-4b6d-a2a1-34b6354c31dc" />

We've got an alert for potential IDOR attacks but we're going to need to look at the HTTP logs for more information.  I'm using the "Source IP Address" value to filter for the specific logs that I want.  I got 5 results for that source address.  They also happen to be around the same time as the alert.

<img width="1427" height="505" alt="Screenshot 2026-11-04 125753" src="https://github.com/user-attachments/assets/976a43c2-3234-437b-a087-98078ff0b5fc" />

Looking at the logs, each entry is a HTTP post from that IP to the same site.  However, every time the "ID" parameter is being changed by the user.  This is definitely an IDOR attack.

<img width="695" height="282" alt="ID-Change-1" src="https://github.com/user-attachments/assets/2cd174b7-52bc-4535-985e-df78ed8aa123" />
<img width="667" height="273" alt="ID-Change-2" src="https://github.com/user-attachments/assets/b1a3bb50-ef4a-453d-9456-16f3729fb26e" />
<img width="682" height="283" alt="ID-Change-3" src="https://github.com/user-attachments/assets/345be321-204d-423f-9b3e-b1a00c9fa064" />

Where it gets a little complicated is whether or not the attack was successful.  On each entry, I'm seeing a "200" HTTP response and each response size is quite a bit different.  This is evidence that the attack was successful but it's not guaranteed.  I would have to escalate this to be sure.
