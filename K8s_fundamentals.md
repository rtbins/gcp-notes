# K8s Fundamentals

## Containerization

A container is a collection of software processes unified by <mark>one namespace</mark> with access to an os kernel that it shares with other containers and little to no access between containers.

A runtime instance of a docker image contains three things

1. A Docker image
2. An execution environment
3. A standard set of instructions

In context of OOPS containers are objects and images are classes.

Core pieces of Docker ecosystem

1. Docker engine

   - comprised of the runtime and packaging tool
   - must be installed on the host that runs docker

2. Docker Store/Hub

   - online repository for users to store and share the docker images

There are also other services provided by Docker.

| Virtual Machines                    | Containers                                                     |
| ----------------------------------- | -------------------------------------------------------------- |
| One or many applications            | Include the application and all of its dependency              |
| Te necessary binaries and libraries | Share the kernel with other containers                         |
|                                     | Not tied to OS, only needs Docker Engine installed on the host |
|                                     | Run as isolated process in user space on the host OS           |

Containers benefits for developers

1. Applications are portable and packaged in a standard way
2. Deployment is easy and repeatable
3. Automated testing, packaging and integrations
4. Support newer microservice architectures
5. Removes platform compatibility issues

Containers benefits for DevOps

1. Reliable deployments, improve speed and frequency of releases
2. Consistent application lifecycle, configure once and run multiple times
3. Consistent environments, no differences between dev and production environments
4. Simple scaling, based on the on-demand use cases, addition of extra workers is easier as deployment is fast

Containers are used to create microservice based architectures. It brings agility to your code, helps in building CI/CD pipelines.
