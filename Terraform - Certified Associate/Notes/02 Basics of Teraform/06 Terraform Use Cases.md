**IaC for Various Providers :** 
- Terraform supports a variety of providers outside GCP, AWS, and Azure.
- tf is open-source and extendable any API could be used to create IaC tooling for any kind of cloud platform or technology. Eg: Heroku

**Multi-Tier Applications :**
- tf by default makes it easy to divide large and complex apps into isolated configuration scripts ( modules )
- It has complexity advantage over cloud-native IaC tools for its flexibility

**Disposable Environments :**
- This is not just for terraform, all IaC platforms should support this - Easily stand up and teardown environments for temporary or test deployments that very closely matches production

**Multi-Cloud Deploymnets**: 
- Terraform is a cloud-agnostic and allows a single configuration to be used to manage multiple providers, and to even handle cross-cloud dependencies!