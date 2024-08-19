# Scaleway Serverless Container Deploy

> _Part of [HTTP Toolkit](https://httptoolkit.com): powerful tools for building, testing & debugging HTTP(S)_

This GitHub Action lets you automatically deploy a container to a Scaleway Serverless Container directly from your GitHub actions. It takes the id of an existing container, updates it to a given image tag or id, redeploys it, and waits until that deploy completes.

It's based on two previous repos:

* https://github.com/thibaultchazal/scaleway-serverless-container-deploy-action
* https://github.com/yamatt/scaleway-serverless-container-deploy-action

and extends them by:

* Monitoring the deploy after it's started, and waiting until it's completed successfully
* Exposing a v1 tag to allow easy tracking & referencing of the latest version

## Usage

In your workflow use this action like so, filling in the arguments with your own values.

```yml
      - name: Deploy container
        uses: httptoolkit/scaleway-serverless-container-deploy-action@v1
        with:
          container_id: 762bd6f8-1551-4a9c-bd34-5fa11889677a
          secret_key: ${{ secrets.SCALEWAY_SECRET_KEY }}
          registry_image_url: rg.fr-par.scw.cloud/example-registry/example-image:latest
```

## Arguments

| Argument | Description | Required | Default |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------|
| `container_id` | The UUID of the container. This Action does not create containers, only update existing ones. You therefore need a container to be created initially, and take the ID from that. The ID can be found in the URL, or the API. | ✔️ | N/A |
| `secret_key` | The secret API key used to access Scaleway. This is generated from the Credentials page. This key must be for the right Organization. The key must have access to the Container Registry and the Serverless APIs. Note that Access Key is not used. | ✔️ | N/A |
| `registry_image_url` | The URL for the registry, image, and version to use in the container, e.g: `rg.fr-par.scw.cloud/example-registry/example-image:latest` | ✔️ | N/A |
| `region` | Scaleway region ID (one of `fr-par`, `nl-ams`, `pl-waw`) | ❌ | fr-par |
| `api_version` | The version of the API to compare against | ❌ | v1beta1 |

## License

MIT
