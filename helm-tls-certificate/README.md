# Helm Issuer Chart

This Helm chart deploys a Kubernetes Issuer and Certificate using `cert-manager`. It supports flexible configurations through values and questions.yaml for Rancher App UI.

## Prerequisites
- Kubernetes cluster
- cert-manager installed in the cluster
- Helm CLI (for CLI method)
- Rancher UI (for Rancher UI method)

## Installation

### 1. Using Helm CLI

#### Step 1: Add cert-manager repository
Ensure you have the `cert-manager` Helm repository added:

```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
```

#### Step 2: Install the Helm chart

Run the following command to install the chart:

```bash
helm install <release-name> ./helm-issuer-chart --set issuer.name=<your-issuer-name>,certificate.commonName=<your-domain>
```

Replace `<release-name>` with your desired Helm release name, and customize the values for your Issuer and Certificate by overriding values with `--set` flags.

You can also customize other values by editing the `values.yaml` or using the `--set` flags to override defaults:
```bash
helm install <release-name> ./helm-issuer-chart   --set issuer.name="custom-issuer"   --set certificate.commonName="example.com"   --set certificate.dnsNames={"example.com","www.example.com"}
```

#### Step 3: Verify Installation
Check that the Issuer and Certificate have been created:
```bash
kubectl get issuers,certificates -n <namespace>
```

### 2. Using Rancher UI

#### Step 1: Add the Chart to the Rancher App Catalog
1. Package the Helm chart into a `.tgz` file or use the provided one.
2. In Rancher, go to **Apps & Marketplace** > **Charts** > **Add a Catalog**.
3. Upload the `.tgz` file to Rancher as a new catalog.

#### Step 2: Install the Chart from Rancher UI
1. Go to **Apps & Marketplace** and find the Helm chart.
2. Click **Install** and fill in the fields as per your needs:
   - **Issuer Name**: Name of the Issuer.
   - **Issuer Kind**: Select either Issuer or ClusterIssuer.
   - **Certificate Name**: Name of the Certificate.
   - **Common Name**: Domain for which you want the certificate.
   - **DNS Names**: List of DNS names for the certificate.

3. Click **Install** to deploy the Issuer and Certificate.

#### Step 3: Verify Installation
Check the status of your resources in Rancher under **Workloads** or via CLI:
```bash
kubectl get issuers,certificates -n <namespace>
```

## Uninstallation

### Using Helm CLI:
To uninstall the Helm chart, run:
```bash
helm uninstall <release-name>
```

### Using Rancher UI:
To uninstall via Rancher, go to **Apps & Marketplace**, find your app, and click **Delete**.

## Configuration
The following parameters are configurable through `values.yaml` or via Rancher UI:
- `issuer.name`: Name of the Issuer.
- `issuer.kind`: Type of Issuer (Issuer or ClusterIssuer).
- `certificate.name`: Name of the Certificate.
- `certificate.commonName`: Common Name for the certificate.
- `certificate.dnsNames`: DNS names for the certificate.
- `certificate.duration`: Certificate validity duration.
- `certificate.renewBefore`: Time to renew before expiration.

For more information on configuration, please refer to the `values.yaml` file.

---

Enjoy using the Helm Issuer Chart!
