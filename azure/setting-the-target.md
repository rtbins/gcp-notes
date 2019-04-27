# Gathering information about existing enterprise architecture in Microsoft Azure

## Identifying constraints and dependencies

### Project constraints

- Toolset selections

  - tools are standards once selected at the beginning of a project
  - standards develop a maintenance and deployment ecosystem around them
  - get on the same page as shareholders
  - toolset selection is flexible most of the time, make sure to discuss it upfront

- People

  - enablers and roadblocks
  - identify the team (your customer, boss, yourself etc)
  - begin with: yourself and your boss
  - `team members:` anyone producing content for the team, to assess the productivity
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
  - involvement: daily or intermittent
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

### Proper settings

- the schedule: not too long and not too short
- the team: not too big or not too small
- smaller, smarter and experienced team outperforms bigger

### How to estimate

- expert judgement
- estimation by analogy (based on history)
- consensus estimation
- we can only estimate tasks, break down the project in tasks

## Identifying compliance requirements

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
- `COBIT`: Control Objectives for Information and Related Technologies
  - framework for achieving Sarbanes-Oxley
  - Access and Authentication
  - Network Security: proper set of infrastructure
  - Monitoring and auditing the relevant activities
  - segregation of duties: more than one set of eyes to take actions in the event of frauds
