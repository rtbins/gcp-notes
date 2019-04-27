# Gathering information about existing enterprise architecture in Microsoft Azure

1. [Understanding Infrastructure](#understanding-infrastructure)

   - [Identifying constraints and dependencies](#identifying-constraints-and-dependencies)
   - [Identifying compliance requirements](#identifying-compliance-requirements)
   - [Understand Infrastructure](#understand-infrastructure)
   - [Identifying Network Infrastructure](#identifying-network-infrastructure)
   - [Identifying Enterprise application categories](#identifying-enterprise-application-categories)

## 1. Understanding Infrastructure

### Identifying constraints and dependencies

#### Project constraints

- Toolset selections

  - tools are standards once selected at the beginning of a project
  - standards develop a maintenance and deployment ecosystem around them
  - get on the same page as shareholders
  - toolset selection is flexible most of the time, make sure to discuss it upfront

- People

  - enablers and roadblocks
  - identify the team (your customer, boss, yourself etc)
  - begin with : yourself and your boss
  - `team members` : anyone producing content for the team, to assess the productivity
    - work availability (%age of weekly hour devoted to this project)
    - planned time-off during the scope of the project
    - level of comfort with the toolset, set aside time to get comfortable with the toolset

- Support Staff

  - security admin
  - database admin
  - deployment admin
  - estimate the different costs (like deployments) in the start

- Stakeholders

  - invested in the success of the project
  - can be product owner or customer
  - involvement : daily or intermittent
  - try and get sign-off and buy-in early on solid requirements

- Testers

  - involve them early in the project
  - give testers lead time and keep them happy

- Know availability windows

  - ask _how quickly do you feel comfortable responding to requests?_
  - give everyone lead time
  - know it for everyone and maintain an excel sheet

- Time

  - Epistemological humility
    - know that quality of our knowledge is not perfect
    - software must be partially completed before an accurate estimate can be composed

- Too little time

  - an arbitrary data was set
  - developers were overly optimistic (`Dunning-Kruger Effect`)
  - Scope change in between (wouldn't it be nice)

- Too much time
  - scope creep
  - expanding the work scope to fill in the time
  - gold-plating, adding unnecessary enhancements

#### Proper settings

- the schedule : not too long and not too short
- the team : not too big or not too small
- smaller, smarter and experienced team outperforms bigger

#### How to estimate

- expert judgement
- estimation by analogy (based on history)
- consensus estimation
- we can only estimate tasks, break down the project in tasks

### Identifying compliance requirements

- code we write, data we store and the information we present can all be impacted by governance policies
- software is impacted by governance policies
- requirements can be different at different levels (Federal, executive agency and state laws)
- conforming with one government policy doesn't imply conforming with other
- HIPAA - Health Insurance Portability and Accountability act
  - PII
  - PHI
  - first line of defence to avoid the accountability is to not store the data of PII and PHI
  - dump it ASAP
  - if can't dump it hash it
  - if can't hash it, encrypt it
- Sarbanes-Oxley act
  - passed in 2001 in response to accounting scandals
  - companies weren't creating representational faithfulness in their accounting
  - you can follow rules and still not achieve representational faithfulness
- `COBIT` : Control Objectives for Information and Related Technologies
  - framework for achieving Sarbanes-Oxley
  - Access and Authentication
  - Network Security : proper set of infrastructure
  - Monitoring and auditing the relevant activities
  - segregation of duties : more than one set of eyes to take actions in the event of frauds

### Understand Infrastructure

#### Identify identity and access management infrastructure

- authentication establishes a subject
- authorization establishes a verb
- missing part object of a verb
- e.g. Chris Behrens reads File X
  - `Chris Behrens` is `identity`
  - `reads` is a `permission`
  - `File X` is an `object`
- an identity system needs to store a user, a permissions and a file
- this structure is called a directory (AD in Microsoft)
- a hierarchical store of organizational objects
  - users, groups, computers
  - their relationships to each other

#### Three broad categories of identity management using AD

- independent identity management
  - completely separate identity store for authentication and authorization
  - can reduce the load on existing IT infra for onboarding new users
- partial integration
  - authentication through AD
  - but other aspects like authorization is stored separately in the application
  - saves the overhead of password related complexity
  - preserves the ability to have a separate staging environment for authorization
  - saves the complexity of heterogenous queries
- complete integration
  - all aspects of users management are stored in AD
  - connecting back to AD for group membership is trickier
  - maintaining application resources in the directory is even harder
  - heterogenous queries
    - joining AD queries to datastore queries
    - databases are better at being directories than directories are at being databases

Independent and partial are most common solutions. With partial integration as a user story further down the line. **Make your identity infrastructure pluggable and abstract**

#### Identity Federation

- responsibility for authentication is delegated
- to a trusted third party
- Real life example, Driver's license Federation chain (DMV office -> Birth certificate -> MOM)
- e.g. sign-in with facebook, with google
- Public key infrastructure (PKI)
  - a set of public keys
    - encrypt content, for a certain recipient
    - validates signature
  - a corresponding set of private keys
    - to decrypt the content
    - create signatures
- Azure as a service provider, SAML

  - your application or network is the service provider
  - azure cryptographically trusts the assertion your application sends
  - ideal when your directory is not AD
  - <https://bit.ly/2x7oD5j>

- Suggestions
  - identify federation parties as early as possible
  - find out whether your IT staff can manage the federation or whether it's up to you
  - your org may use access management tools
    - directories are security databases
    - access management tools manage and enforce policies within the directory
    - self service like, password reset
    - automated workflows
  - user remanence (different from data remanence)
    - whether or not and how users remain
    - termination (revoke complete access, and remove from system)
    - retirement (partial access might be required)
    - PTO
    - explore these questions with your directory manager

### Identifying Network Infrastructure

- continuously connected or occasionally connected
- no pre-determined checklists
- understand your company network and boundaries with other networks
- ask and explore following questions
  - [ ] what is the structure of oue company network?
  - [ ] how do we secure our network?
    - how is email secured?
    - how are file transfer secured
  - [ ] what happens when portions of network become unavailable?
  - [ ] what portions of the network are
    - on premise
    - in the cloud
    - why?
- choices faced while migrating to a cloud
  - `lift and shift`, bare minimum to migrate to a cloud, e.g. take all of the application and put it in a cloud's vm
  - `replatform`, some aspect of application to cloud feature, most of the architecture remains same, e.g. sql server to azure sql db
  - `cloud native`, rebuilt the system such that dead weights between on-premises and cloud architecture have been addressed if not fully resolved
- **Don't let the perfect be the enemy of the good**
- Azure AD connect
  - sync architecture
  - AD connect bypasses federated auth by syncing bytes bytes even at the password hash level

### Identifying Enterprise application categories

#### Broad categories

- CRM
  - organizes customer information and history
  - e.g. Microsoft dynamics
  - `Integration` : can we send message to this email from MS Dynamics
- CMS
  - content and document management system
  - e.g. SharePoint
  - `Integration` : can we embed a PDF of the contract from SharePoint
- Collaboration
  - tools for communicating and collaborating
  - e.g. MS Teams
  - `Integration`: could I get a teams notification whenever somebody fills out the form
- Version control system
  - git

#### Suggestions

- talk to your users
- how do they get their work done right now
- let your integration (or lack of integration) be informed by how people work
