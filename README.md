# Create Jira Ticket for EventBridge Schema Discovery Updates

The solution will create a Jira ticket when an EventBridge rule is triggered (in this case, when an EventBridge Schema discovery update occurs, but this can easily be adjusted). To add useful information to the ticket, the event is enriched during the flow (see the inline Lambda code in the template).

## Architecture

```
+----------------+      +--------+      +-------------------------+      +----------------+      +-------------------------+
| EventBridge    | ---> | SQS    | ---> | EventBridge Pipe        | ---> | Step Function  | ---> | SSM Automation Document |
| Rule           |      |        |      | (Filtering & Enrichment)|      |                |      |                         |
+----------------+      +--------+      +-------------------------+      +----------------+      +-------------------------+
```

## Deploy

* Create encrypted SSM parameter with Jira API Token
* Update necessary parameters in `template.yml` or provide them in deploy command.


```
$  aws cloudformation deploy --template-file template.yml --stack-name <name> --capabilities CAPABILITY_IAM
```