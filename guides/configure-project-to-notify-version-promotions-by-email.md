# Configure project to notify version promotions by email

Use this command to check any subsystem webhook at the project level

```bash
$ ced project:list-webhooks <projectId>
```

Create a subsystem webhook at the project level

```bash
$ ced project:set-webhook <projectId>
```

Use the following options

- Name: `"Version promotion emails"`
- Url: `https://us-central1-ced-notif-dispatcher.cloudfunctions.net/http-api/v1/dispatcher/version-promotion-email?auth=47dZL7iCdtQUDXrcy6Tk`
- Method: `POST`
- Webhook event: `[Build]`
- Webhook operation state: `[Started]`

Use this URL for notifications in CED Prod

```
https://us-central1-ced-notif-dispatcher.cloudfunctions.net/http-api/v1/dispatcher/version-promotion-email?auth=47dZL7iCdtQUDXrcy6Tk
```

Use this URL for notifications in CED Dev

```
https://us-central1-ced-notif-dispatcher-dev.cloudfunctions.net/http-api/v1/dispatcher/version-promotion-email?auth=47dZL7iCdtQUDXrcy6Tk
```
