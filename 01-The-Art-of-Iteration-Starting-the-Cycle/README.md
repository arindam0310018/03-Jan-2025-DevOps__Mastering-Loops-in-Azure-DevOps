# The Art of Iteration: Starting the Cycle:-

Greetings my fellow Technology Advocates and Specialists.

This is the __Chapter #1__ of my __Mastering Loops in Azure DevOps__ Series.

In this Session, I will walk you through __The Art of Iteration: Starting the Cycle__.

This is a quick start guide to introduce the topic and how it is relevant to the real world.

| __REFERENCE LINKS:-__ |
| --------- |
| 1. [Microsoft Learn - Azure Devops - Expressions](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops#each-keyword). |

| __HOW DOES MY CODE PLACEHOLDER LOOKS LIKE:-:-__ |
| --------- |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/eevyehn1ktbcm8kldiqm.jpg) |

| __MILLION DOLLAR QUESTION:-__ |
| --------- |
| Question: __Can we use "Loop" in Azure Devops YAML Pipeline ?__ |
| Answer: __YES__ |

| __HOW ?__ |
| --------- |
| __Concise summary follows below:-__ |
| __1.)__ We can use __"Loop"__ in Azure Devops YAML Pipeline by using the __"each"__ keyword. |
| __2.)__ We can use the __"each"__ keyword to loop through a) __Parameters__ with the type as b) __Object__. |
| __3.)__ Additionally, you can iterate through __Nested elements within an Object__. |

| __EXAMPLE:-__ |
| --------- |

| __PIPELINE CODE SNIPPET:-__ |
| --------- |

| __AZURE DEVOPS YAML PIPELINE (azure-pipelines-Leverage-Loops-For-Automation-Initial-Test.yml):-__ |
| --------- |

```
trigger:
  none

######################
#DECLARE PARAMETERS:-
######################
parameters:
- name: RGNAME
  displayName: Please Provide the Resource Group Name:-
  type: object
  default: [AMRG001,AMRG002,AMRG003]

######################
#DECLARE VARIABLES:-
######################
variables:
  BuildAgent: windows-latest

#########################
# Declare Build Agents:-
#########################
pool:
  vmImage: $(BuildAgent)

###################
# Declare Stages:-
###################
stages:
  - ${{ each rg in parameters.RGNAME }}:
    - stage: CREATE_${{ rg }}
      jobs:
        - job: CreateResourceGroup
          steps:
            - script: echo "Creating "${{ rg }}""
    
```

| __EXPLANATION:-__ |
| --------- |

__I.)__ Declare __"Parameter"__ of type __"Object"__. In this example, I have declared 3 values (Resource Group Names) as an array.

```
######################
#DECLARE PARAMETERS:-
######################
parameters:
- name: RGNAME
  displayName: Please Provide the Resource Group Name:-
  type: object
  default: [AMRG001,AMRG002,AMRG003]
```

__II.)__ Declare __"Each"__ at beginning of the Pipeline stage. The __"rg"__ variable stores all the values that the __"each"__ keyword iterates over in the __parameter of type object__.

```
stages:
  - ${{ each rg in parameters.RGNAME }}:
```

__III.)__ As there are 3 values declared in __"Parameter"__ of type __"Object"__, there will be __3 STAGES CREATED__. 

__IV.)__ Name of each stage will be one of iterated value from the array declared in __"Parameter"__ of type __"Object"__.

```
- stage: CREATE_${{ rg }}
```

__V.)__ Finally, each stage displays the Value in the console. 

```
steps:
            - script: echo "Creating "${{ rg }}""
```

| __OUTPUT OF EXAMPLE:-__ |
| --------- |
| 1. As in the example, there were 3 values declared in __"Parameter"__ of type __"Object"__, hence __3 STAGES__ got created. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1nj7wnang21drggwug4x.png) |
| 2. Name of each stage is the iterated value from the array declared in __"Parameter"__ of type __"Object"__. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/32zqjih0qkycsa5dtxui.jpg) |
| 3. Each stage displays the Value in the console. |
| __STAGE #1:__ __CREATE_AMRG001__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mlylqge2n1gmrai34vqk.jpg) |
| __STAGE #2:__ __CREATE_AMRG002__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ijnrwvhqp9m1g9v89xxh.jpg) |
| __STAGE #3:__ __CREATE_AMRG003__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y9a647j2y0yubxf4jxz6.jpg) |
 
__Hope You Enjoyed the Session!!!__

__Stay Safe | Keep Learning | Spread Knowledge__
