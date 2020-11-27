# Instana Version Resource

This [Concourse](https://concourse-ci.org/) resource allows you to track the version of an Instana backend.

## Source Configuration

* `endpoint`: *Required.* The URL of your Instana backend, including the protocol (`https`) and, with self-managed (a.k.a. on-prem) units, the port; do not include the path. So, `https://my-unit.instana.io` or `https://my-unit.my-domain:1444` are good, `https://my-unit.instana.io/api` is not.

* `api_token`: A valid [API token](https://www.instana.com/docs/api/web/#tokens), no additional permissions required.

### Example

``` yaml
resource_types:

  - name: instana-version
    type: docker-image
    source:
      repository: instana/instana-version-resource
      tag: latest

resources:

  - name: backend-version
    type: instana-version
    source:
      endpoint: https://awesome-tenant.instana.io
      api_token: ((instana_api_token)) # Use secrets if you can!
```

## Behaviour

### In

The resource will create the following file:

* `release`, containing, e.g., `190`

## Support

To ensure we do not miss your requests, we disabled the Issues functionality for this repository.
If you have questions about how to use Concourse resource, please open a [support request](https://support.instana.com/hc/en-us/requests/new).

## Development

The actions of the resource are written in `bash`, `curl` and `jq`, with the goal of being easy to debug in local even from inside a Docker image (hello, [`fly intercept`](https://concourse-ci.org/builds.html#fly-intercept)!).
The test scripts assumes a local Docker daemon.

## Contributing

Ah, our kind of person!
Go ahead, open a Pull Request.

Please be aware that we will be able to accept only code contributed under the Apache 2.0 license.
