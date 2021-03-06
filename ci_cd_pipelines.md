# CI/CD Pipeline configurations

- CI/CD [pipelines](#Pipelines) for a git vendor (gitlab, perforce) is configured using a YAML file `.gitlab-ci.yml`
- is done at the project level
- `.gitlab-ci.yml` defines structure and order of the pipeline, also determines
  - what to execute using [Gitlab Runner](#runners)
  - decisions to make when certain conditions are encountered (upon success or failure)
- default three stages: build, test and deploy

## Annexure

### Pipelines

- top level components of CI/CD
- comprises
  - `jobs` defines what to run (code compilation or test runs)
  - `stages` defines when and how to run, oder of jobs (e.g. test run only after code compilation)
- `parallel` jobs of a stage can run if concurrent runners are available
- if all the jobs in a stage `succeed` then pipeline moves to next stage otherwise pipeline ends early (usually)
- in pipeline `stage` name is capitalized
- `only: merge_requests` in a job will run a job only for a merge request

#### Grouping jbs

- grouped under job named `test`
  - test 0 3
  - test 1 3
  - test 2 3
- grouped under `test ruby`
  - test 1:2 ruby
  - test 2:2 ruby
- grouped under `test ruby`
  - 1/3 test ruby
  - 2/3 test ruby
  - 3/3 test ruby

#### Badges

- <https://example.gitlab.com/namespace/project/badges/branch/pipeline.svg>
- <https://example.gitlab.com/namespace/project/badges/branch/coverage.svg?job=coverage_job_name>

#### Working with pipelines

- manually execution from pipeline section of the repository
- `when: manual` ensures job execution manual only (deploy to production)
- `when: delayed` ensures a delay between stages (e.g. partial rollout before a full rollout to production), `start_in: 30 minutes`
- can be triggered through pipeline api
- a branch can be tagged `protected` to allow specific users to merge or push, to run against runners marked as protected only
- variables marked as protected can be accessed only by protected branches

Reference: <https://docs.gitlab.com/ee/ci/pipelines.html>

### Runners

- runs the code defined in `.gitlab-ci.yml`
- are isolated vms that pick up jobs through the coordinator API of Git vendor CI.
- a runner can be a shared one, specific or a group one
- Registering a Runner: <https://docs.gitlab.com/ee/ci/runners/README.html#registering-a-shared-runner>

