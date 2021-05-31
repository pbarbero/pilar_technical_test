# FALCO 0.28.1

A new Falco release is now being released! It includes feature improvements, bug fixes and rules updates

[Here](https://github.com/falcosecurity/falco/releases/tag/0.28.1) you have the details but below you can find the most interesting highlights. 

And our installation guide [https://falco.org/docs/installation/](https://falco.org/docs/installation/).

## Monitoring the unknown

When Falco receives a timeout, it appears with an event that is discarted in the majority of cases.
It can also happen that the timeout comes *without* an event. These cases should not be worrisome, but they are suspicious that something is not going well at a low level.
We would have to worry in the unlikely event that many non-event timeouts are received. 

In this cases we have configured that Falco outputs an alert with this problem.

You can configure the number of consecutive timeouts without event in the _syscall_event_timeouts.max_consecutive_ configuration field.
With this, Falco would be able to manage how many consecutive timeouts without event are allowed without sending the alert.

The alert will be sent with DEBUG priority and the message would be:

```
Debug Falco internal: timeouts notification. 1000 consecutive timeouts without event.
```

## Rules changes

The following new macros:

> rule(macro: allowed_aws_ecr_registry_root_for_eks) \
> rule(macro: aws_eks_core_images) \
> rule(macro: aws_eks_image_sensitive_mount)

allow AWS EKS images to be used in rule: Launch Privileged Container.

### Rules deprecation

These macros are deprecated and will be no longer supported:

> rule(list falco_privileged_images) \
> rule(list falco_sensitive_mount_images) \
> rule(macro k8s_containers) \
> rule(macro: python_running_sdchecks) \
> rule(Change thread namespace)

## Bug fixes

Our community is great! We appreciate your contributions [reporting issues](https://github.com/falcosecurity/falco/issues/new) or by reaching out the OSS team if #falco channel on our [Slack](https://slack.sysdig.com/).

In this release, [an issue reported](https://github.com/falcosecurity/falco/issues/1575) few weeks ago was fixed. Now, when some invalid data arrived to Falco, the webserver for Kubernetes doesn't stop.

## Support

And at last, but not least, another useful update. Flag _--support_ now prints also information about the falco engine version. 

```json
"engine_info": {
  "engine_version": 8
}
```
---------------------------------------

If you've liked our new features, remember to [subscribe to our newsletters](https://sysdig.com/newsletters/) and join or [Falco mailing list](https://lists.cncf.io/g/cncf-falco-dev).

As always, you can report any bugs found [by opening an issue](https://github.com/falcosecurity/falco/issues/new).