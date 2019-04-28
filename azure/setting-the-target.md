# Gathering information about existing enterprise architecture

- [1. Understanding Infrastructure](#1-understanding-infrastructure)

  - [Identifying constraints and dependencies](#identifying-constraints-and-dependencies)
  - [Identifying compliance requirements](#identifying-compliance-requirements)
  - [Understand Infrastructure](#understand-infrastructure)
  - [Identifying Network Infrastructure](#identifying-network-infrastructure)
  - [Identifying Enterprise application categories](#identifying-enterprise-application-categories)

- [2. Identifying service oriented architecture](#2-identifying-service-oriented-architecture)
  - [ETL](#etl)
  - [SSO](#sso)
  - [REST request and security](#rest-request-and-security)
  - [When to choose each](#when-to-choose-each)
  - [Service discoverability](#service-discoverability)
- [3. Identifying security architecture](#3-identifying-security-architecture)
- [4. Identifying data and data models infrastructure](#4-identifying-data-and-data-models-infrastructure)
  - [Data migration approaches](#data-migration-approaches)
  - [Data remanence](#data-remanence)
- [5. Design patterns](#5-design-patterns)
- [6. Anti patterns](#6-anti-patterns)
  - [Wolf tickets](#wolf-tickets)
- [Reference](#reference)

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

## 2. Identifying service oriented architecture

### ETL

- good choice when latency is not important
- user remanence
  - focus not only on data in but data out also
- 3 approaches to remove a person data on leaving a company
  - set comparison
    - db with unique user key (A) and a file with all user key (B)
    - create all users that do not exists in SET A but do exists in SET B
    - update all users that exists in both
    - delete all users that exists in SET A but not in SET B
    - responsibility of user remanence lies with the person creating the file Set B
    - user might drop off in one night and come back in next
  - rolling deletion
    - create a date-stamped record for all users in SET A that do not exists in SET B
    - delete all user records who have x datestamp records for the last X days
  - never delete anybody

### SSO

In sso there is no username/pwd being passed, since company B can cryptographically verify the trust set by company A. Who started the process

- service provider initiated
- identity provider initiated

### REST request and security

- REST requests should always be communicating over HTTPS
- `Protected` against interception : url path, queryString, headers and body of the request
- `Not protected` : host address and port
- server logs can have secure data in the form of plain text

### When to choose each

- `ETL`
  - Requires a highest level of trust
  - Providing a service with the data
  - Higher latency
- `SSO`
  - Facilitating authentication only
  - Can be highly reusable
  - Generally a more fractured user experience
- `REST`
  - Middle Ground between the two
  - Seamless integration
  - But you need programmer on both sides

### Service discoverability

Discover

- Existence
- Structure
- Availability

e.g. Sql server populates it's server dropdown like this, wrap the service with discoverability protocol.

## 3. Identifying security architecture

- Who needs to do which thing to what? _Authorization_
- How is that enforced?
- How is data protected while being transported? How is it protected at rest?
- How do we know when a breach has occurred? How can we know correct data is being logged so that we can investigate it?
- `Multi factor authentication` provides a more robust security measure

- Static security code analysis
  - Analyze the code for quality and patterns before building it into binaries
  - Virtuous build cycles
  - Early on, analysis catches a lot of problems
  - The correction work their way into your style
  - And the knowledge in the tool is installed in your brain
  - Tools : SonarQube, hp-fortify

## 4. Identifying data and data models infrastructure

### Data migration approaches

- `Read only push`
  - Transactional instance remains in service
  - Periodic, one-way sync
- `Replication`
  - Two peer copies
  - Maybe one on-premises, one in cloud
  - Consistency or latency - choose one
- `One-Time transfer`
  - Take the db offline, transfer it, bring it back up
  - Downside is downtime

### Data remanence

- When does data cease to remain and how?
- What does `deleted` mean exactly?
- Remanence solutions
  - Delete the data by `Overwriting` the sectors
  - `Degaussing`, destroy magnetic field of the media (media specific tool)
  - `Destruction`, phase transition (liquid, gas)
  - Fry the drive
  - Getting data out of cloud is like getting milk out of coffee

## 5. Design patterns

- Authentication broker, instead of each application separate identity management
- `REST` patterns and maturity
  - `Level 0` : POX (plain old XML)
  - `Level 1` : Resource
  - `Level 2` : HTTP verbs
  - `Level 3` : HATEOAS (application's state)
    - e.g. in response returning add miles api and other api details
    - Challenges, no strong standard on relationships
    - No strong consensus on operations
    - Small-scale standards are possible

## 6. Anti patterns

### Wolf tickets

- A promise or a threat in the app you won't keep
- A broad commitment that becomes narrow
  - Our product support standard X, but does it really?
- Vendor-specific implementations lock consumers in
- Proofs of implementations
  - An automated tool?
    - like Acid3 for CSS
  - Certification by an independent standards body
- Don't accept or hand out Wolf tickets
- If you commit to standard
  - you commit to the verification of the standard
  - Auditors can keep you honest

## Reference

- Chris Behrens, Pluralsight course
