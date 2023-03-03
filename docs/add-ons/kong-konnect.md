
## Kong Konnect

Kong Konnect is an API lifecycle management platform designed from the ground up for the cloud native era and delivered as a service. This platform lets you build modern applications better, faster, and more securely. The management plane is hosted in the cloud by Kong, while the runtime engine, Kong Gateway — Kong’s lightweight, fast, and flexible API gateway — is managed by you within your preferred network environment.

For more details, refer [Kong Konnect](https://docs.konghq.com/konnect/).



## Pre-Requisites

* Sign up for [Kong Konnect](https://cloud.konghq.com/register) if not already. 
* Download the shell script 

```
curl -o https://raw.githubusercontent.com/aws-samples/sample-kong-gateway/main/konnect-secrets-manager.sh
```

* Execute
* Run script from where you have aws cli and access to your aws account.

```
./konnect-secrets-manager.sh -v -api https://cloud.konghq.com -u '<KONNECT_USERNAME>' -p '<KONNECT_PASSWORD>' -c '<KONNECT_RUNTIME_SHA>'
```

After the script is executed ,cert and key secret will be created in AWS Secret Manager.

* Save the output to `terraform.auto.tfvars`
* Optionally fill in `kong_values.yaml` with any additional helm values that you may want for the kong's helm chart.

## Usage

Kong Konnect can be deployed by enabling the add-on along with the mandatory values in the kong helm config via the following 

```hcl
enable_external_secrets = true
enable_kong_konnect = true

kong_helm_config = {
   cluster_dns      = var.cluster_dns
   telemetry_dns    = var.telemetry_dns
   cert_secret_name = var.cert_secret_name 
   key_secret_name  = var.key_secret_name
   values = [templatefile("${path.module}/kong_values.yaml"] [Optionally include value if need any additional helm values that you may want for the kong's helm chart.]
}

```
Include the variables in `variables.tf` file.

