# Terraform Workflow Example

Directories are structured by cloud providers and environments:

Directory structure example:
```
|-- terraform-stacks
    |-- cloud-provider
    |   |-- shared-services
    |   |   |-- modules
    |   |   |-- files.tf
    |   |   |-- shared-services.tfvars
    |   |-- production
    |   |   |-- modules
    |   |   |-- files.tf
    |   |   |-- production.tfvars   
    |   |-- staging
    |   |   |-- modules
    |   |   |-- files.tf
    |   |   |-- staging.tfvars
    |   |-- development
    |   |   |-- modules
    |   |   |-- files.tf
    |   |   |-- development.tfvars
```

Terraform Workflow:

```mermaid
  graph TD;
      A[Pull request workflow]-->B{Which cloud provider?};

     
      B--Google-->C1["Set gcp credentials"];
      B--Azure-->C2["Set azure credentials"];
      B--AWS-->C3["Set aws credentials"];
            
      C1--->W{Which environment?};
      C2-->W{Which environment?};
      C3-->W{Which environment?};
            
      W--Shared Services-->E1["Set shared-services.tfvars"];
      W--Production-->E2["Set production.tfvars"];
      W--Staging-->E3["Set staging.tfvars"];
      W--Development-->E4["Set dev.tfvars"];
      
      E1-->P[Terraform Plan];
      E2-->P[Terraform Plan];
      E3-->P[Terraform Plan];
      E4-->P[Terraform Plan];
         
      P--->V{"Validation Result"};
            
      V--Fail-->K["End Workflow"];
      V--Pass-->F{"Reviewer Approval"};
      F--Yes-->I["Merge Branch"];
      I-->H["Terraform Apply"];
      F--No-->K["End Workflow"];
```
