# 1. CI/CD Pipeline configurations

- CI/CD [pipelines](#Pipelines) for a git vendor (gitlab, perforce) is configured using a YAML file `.gitlab-ci.yml`
- is done at the project level
- `.gitlab-ci.yml` defines structure and order of the pipeline, also determines
  - what to execute using `Gitlab Runner`
  - decisions to make when certain conditions are encountered (upon success or failure)

## 1.1. Annexure

### 1.1.1. Pipelines

- top level components of CI/CDD
- comprises
  - `jobs` defines what to run (code compilation or test runs)
  - `stages` defines when and how to run, oder of jobs (e.g. test run only after code compilation)
- `parallel` jobs of a stage can run if concurrent runners are available
- if all the jobs in a stage `succeed` then pipeline moves to next stage otherwise pipeline ends early (usually)
- in pipeline `stage` name is capitalized
- `only: merge_requests` in a job will run a job only for a merge request

#### 1.1.1.1. Grouping jbs

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

#### 1.1.1.2. Badges

- <https://example.gitlab.com/namespace/project/badges/branch/pipeline.svg>
- <https://example.gitlab.com/namespace/project/badges/branch/coverage.svg?job=coverage_job_name>

#### 1.1.1.3. Working with pipelines

- manually execution from pipeline section of the repository
- `when: manual` ensures job execution manual only (deploy to production)
- `when: delayed` ensures a delay between stages (e.g. partial rollout before a full rollout to production)
- can be triggered through pipeline api
- a branch can be tagged `protected` to allow specific users to merge or push, to run against runners marked as protected only
- variables marked as protected can be accessed only by protected branches

Reference: <https://docs.gitlab.com/ee/ci/pipelines.html>