# Task A – Production went down

When an outage occurs, the primary goal should be to restore the app/service as quickly as possible, and investigate the root cause afterward. Since I'm only at the beginning of my DevOps learning path, this will be a high-level overview of recommended steps, without specific tools or commands mentioned.

## 1. Confirm the problem and check status
- **Verification:** I need to check the app myself and verify that it's actually down. I need to see what error message (and status code) I'm getting.
- **Notification:** I need to inform the relevant people in my company about the outage, using a dedicated Slack channel or other tools our company uses for such incidents.
- **Status Check:** I need to quickly check monitoring dashboards (if available). Depending on the infrastructure, I’ll need to verify whether our cloud provider or any critical third-party services used by the app are down.

## 2. Check for recent changes
In the next phase, I ask the following "What has changed?" questions:
- **Check CI/CD:** Has a new version of the app been deployed recently?
- **Check Infrastructure:** Have there been any recent changes to the infrastructure?
- **Check Configuration:** Have any recent changes been made to the configuration files or settings?
- **Check DB Migrations:** Has any recent database migration been performed?
- **Check Network:**  Have there been any recent changes to firewall rules or security policies? Are there any expired certificates? 
If a recent deployment is causing the crash, the first step should be rollback to the previous (stable) version.

## 3. Check the logs
Next, I would review logs to find errors:
- **Application:** Check all relevant logs related to our application.
- **Container logs:** Check the status and logs of containers running our application.
- **Cloud/Server logs:** Search for any errors or exceptions, connection timeouts...  

## 4. Check the system health
If monitoring tools are enabled and used in our application, I will check:
- **CPU/Memory:** Is the server under heavy load? Are its resources fully used?
- **Disk:** What is the current disk space usage? Is the disk full? Do we need to free up space?
- **Error Rates:** Are we experiencing a high number of errors recently? What types of errors?
- **Traffic:** Is the traffic too high? Should we scale up?

## 5. Check external dependencies
If our app depends on other services, I will verify that:
- **Database:** is reachable and communication between our app and database is working.
- **APIs:** or third-party services working.

## 6. Apply a fix
Based on my findings from the previous steps, I take one of these possible actions:
- Roll back the most recent deployment
- Restart the service or container
- Scale the application if it is overloaded
- Clean up unused resources and free up disk space

## 7. Post-Mortem Analysis
Once our app is up and running again:
- I analyze and document the exact time the issue started and its impact.
- I describe the root cause of the issue and the fix that was applied.
- I propose a solution to prevent this issue from occurring in the future.