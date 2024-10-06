# Helm Charts Repository

Welcome to the Helm Charts repository! This repository contains multiple Helm charts for deploying various Kubernetes resources.

## Repository Structure

```bash
helm-charts/
├── charts/
│   ├── helm-tls-certificate/
│   ├── other-chart/
│   └── ...
```

Each chart is stored under the `charts` directory, and each has its own `values.yaml`, templates, and metadata.

## Using this Repository as a Helm Chart Repository

To use this repository as a Helm repository directly, follow these steps:

### Step 1: Add the Helm Repository
Add the repository to your Helm client:

```bash
helm repo add thanhtunguet-charts https://github.com/thanhtunguet/helm-charts
```

Note: Make sure that Helm supports Git-based repositories. If it does not, you can use `helm-git` plugin for Git-based Helm repositories. To install the plugin:

```bash
helm plugin install https://github.com/databus23/helm-diff
```

Then you can add the Git repository:

```bash
helm repo add thanhtunguet-charts git+https://github.com/thanhtunguet/helm-charts
```

### Step 2: Update the Helm Repositories

```bash
helm repo update
```

### Step 3: Install a Chart from the Repository

Once the repository is added, you can install charts from it like any other Helm repository:

```bash
helm install <release-name> thanhtunguet-charts/helm-tls-certificate --set issuer.name=<your-issuer-name>,certificate.commonName=<your-domain>
```

### Example:
```bash
helm install my-issuer thanhtunguet-charts/helm-tls-certificate   --set issuer.name="my-issuer"   --set certificate.commonName="example.com"   --set certificate.dnsNames={"example.com","www.example.com"}
```

This will install the `helm-tls-certificate` from the GitHub repository.

## Contributing

Feel free to contribute by opening pull requests to add new charts or improve existing ones.

## License

This repository is licensed under the MIT License. See the `LICENSE` file for more information.
