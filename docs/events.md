<!--
---
linkTitle: "Events"
weight: 700
---
-->
# Events in Tekton Triggers

Triggers event controller emits [Kubernetes events](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#event-v1-core)
when EventListener get request to process `Triggers`. This allows you to monitor and react to what's happening during execution by
retrieving those events using the `kubectl get events` command.

## Events in `EventListener`

`EventListener` emit events for the following `Reasons`:

- `Started`: emitted the first time when the `EventListener` received request.
- `Succeeded`: emitted when eventlistener received request and process all triggers request.
- `Failed`: emitted if triggers failed to process the request.

## Events format

Resource            |Event      |Event Type
:-------------------|:---------:|:----------------------------------------------------------
`EventListener`     | `Started` | `dev.tekton.event.triggers.started.v1`
`EventListener`     | `Succeed` | `dev.tekton.event.triggers.successful.v1`
`EventListener`     | `Failed`  | `dev.tekton.event.triggers.failed.v1`

##Note
By default Kubernetes events are disabled for EventListener.

To enable Kubernetes events for each EventListener need to add below annotation
```yaml
  annotations:
    enable-eventlistener-events: "true"
```

ex:
```yaml
apiVersion: triggers.tekton.dev/v1beta1
kind: EventListener
metadata:
  name: github-listener
  annotations:
    enable-eventlistener-events: "true"
spec:
---
```
To view the events execute below command

`kubectl get events`
