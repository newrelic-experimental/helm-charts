# nri-kube-events

## Chart Details

This chart will deploy the New Relic Events Routers as a Deployment.

## Configuration

| Parameter                                                  | Description                                                                                                                                                                                                                                    | Default                         |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| `global.cluster` - `cluster`                               | The cluster name for the Kubernetes cluster.                                                                                                                                                                                                   |                                 |
| `global.licenseKey` - `licenseKey`                         | The [license key](https://docs.newrelic.com/docs/accounts/install-new-relic/account-setup/license-key) for your New Relic Account. This will be preferred configuration option if both `licenseKey` and `customSecret` are specified. |                                 |
| `global.customSecretName` - `customSecretName`             | Name of the Secret object where the license key is stored                                                                                                                                                                                      |                                 |
| `global.customSecretLicenseKey` - `customSecretLicenseKey` | Key in the Secret object where the license key is stored.                                                                                                                                                                                      |                                 |
| `agentHTTPTimeout`                                         | The timeout for the events-router to reach the infra-agent                                                                                                                                                                                     | `30s`                           |
| `sinks.stdout`                                             | When enabled all routed events are also logged.                                                                                                                                                                                                | `false`                         |
| `nameOverride`                                             | The name that should be used for the deployment.                                                                                                                                                                                               |                                 |
| `image.kubeEvents.repository`                              | The events-router image name.                                                                                                                                                                                                                  | `newrelic/nri-kube-events`      |
| `image.kubeEvents.tag`                                     | The events-router image tag.                                                                                                                                                                                                                   | `1.1.0`                         |
| `image.infraAgent.repository`                              | The infra-agent image name.                                                                                                                                                                                                                    | `newrelic/k8s-events-forwarder` |
| `image.infraAgent.tag`                                     | The infra-agent image tag.                                                                                                                                                                                                                     | `1.11.24`                        |
| `resources`                                                | A yaml defining the resources for the events-router container.                                                                                                                                                                                 | {}                              |
| `rbac.create`                                              | Enable Role-based authentication                                                                                                                                                                                                               | `true`                          |
| `serviveAccount.create`                                    | If true, a service account would be created and assigned to the deployment                                                                                                                                                                     | true                            |
| `serviveAccount.name`                                      | The service account to assign to the deployment. If `serviveAccount.create` is true then this name will be used when creating the service account                                                                                              |                                 |
| `nodeSelector`                                             | Node label to use for scheduling                                                                                                                                                                                                               | `{}`                            |
| `tolerations`                                              | List of node taints to tolerate (requires Kubernetes >= 1.6)                                                                                                                                                                                   | `[]`                            |
| `affinity`                                                 | Node affinity to use for scheduling                                                                                                                                                                                                            | `{}`                            |

## Example

Make sure you have [added the New Relic chart repository.](../../README.md#installing-charts)

Then, to install this chart, run the following command:

```sh
helm install newrelic/nri-kube-events \
--set licenseKey=<enter_new_relic_license_key> \
--set cluster=my-k8s-cluster
```
