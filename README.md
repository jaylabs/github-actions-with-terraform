# gcp-terraform-example
Testing github actions with terraform
    
```
|-- terraform-stacks
    |-- aws
    |   |-- project
    |   |   |-- modules
    |   |   |-- files.tf    
    |-- azure
    |   |-- project
    |   |   |-- modules
    |   |   |-- files.tf    
    |-- google
    |   |-- project
    |   |   |-- modules
    |   |   |-- files.tf    
```

```mermaid
  graph TD;;
      A[Pull request workflow]-->B{Which cloud provider?};

     
      B--Google-->C1["Set Provider Credentials"];
      B--Azure-->C2["Set Provider Credentials"];
      B--AWS-->C2["Set Provider Credentials"];
            
      C1--->W{Which environment?};
      C2-->W{Which environment?};
      C3-->W{Which environment?};
            
      W--Shared Services-->E1["Set Variables"];
      W--Production-->E2["Set Variables"];
      W--Staging-->E3["Set Variables"];
      W--Development-->E4["Set Variables"];
      
      E1--->P{Which Project?};
      E2--->P{Which Project?};
      E3--->P{Which Project?};      
      E4--->P{Which Project?};

      
      P--Project Name-->T["Terraform Plan"];
      
      T--->V{"Validation Result"};
            
      V--Fail-->K["End Workflow"];
      V--Pass-->F{"Reviewer Approval"};
      F--Yes-->I["Merge Branch"];
      I-->H["Terraform Apply"];
      F--No-->K["End Workflow"];
  

```
