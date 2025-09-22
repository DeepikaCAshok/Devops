# Devops
DEvops_assessment_1
1] CICD Stands for continues integration and continuous delivery (or continuous deployment)

Continuous integrations - is a software development process where the changes made to software are integrated into the main code as and when the application is ready so that software will be always ready to be build tested deployed and monitored continuously



Continuous integrations - after the integration the continues deliver process will take place where the where the continually integrated changes will tested and deployed into a specific environment, generally through a manual process after all the quality checks are successful

Continuous Deployment - Its a practice where the continuously integrated changes are deployed automatically into the target environment after passing all the quality checks



2] A Jenkinsfile is used to :
Define a pipeline as code(CICD process)
Automate build, test and deploy steps.
keep pipeline in version control for consistency
enable collaboration and repeatability across teams



3]Declarative Pipeline
Structured and easy to read syntax
best for simple/ standard CICD pipelines
Limited flexibility compared to scripted

Scripted Pipeline
Groovy based free-form coding style
suitable for complex/custom pipelines
more flexible but harder to maintain



4] GUI Based configuration (manual setup)
Limited flexibility - good for small/simple tasks
harder to reproduce/tract changes(not stored as code)

Define as code(jenkinsfile)
highly flexible - supports complex CICD workflows
stored in version control, easy to reuse and maintain

Freestyle - simple GUI Job
pipeline - CICD as code



5]using the credentials plugins which stores different types of credential like username with a password ssh username with the private key aws credentials Jenkins build tokens \& certificates

6]if a job fails i will analyse the reason for the

1. failure troubleshoot the issue by checking the console output
2. examining build logs
   3.investigating any error message



Section 3 : Debugging \& Scenarios

1] exit Code 137 in a jenkins pipeline usually means the process was killed by the system (SIGKILL)
Causes :

1. The out of memory(OOM)
   the build/test process consumed more memory than allocated.
   common with docker builds, java apps or heavy test suites
2. Container/agent resource limits:
   if running inside docker/kubernets, the container may have memory/CPU limits - exceeding them kills the process
3. manual/system kill:
   the process was forcefully stopped (less common)

Fixes :
increase memory allocates (eg -xmx for java or container memory limits)
optimize build/ test process

2] 1. Use a job queue - jenkins will schedule jobs on available agents automatically
2. add more agents (scale horizontally) - use kubernetes docker or cloud-based agents
3. parallelize within pipeline - split long jobs into smaller parallel stages if possible
4. Prioritize critical jobs - use job throttling or labels to control execution

3] 1. Restore from backup - keep regular backups of JENKINS\_HOME (config.jobs, plugins)
2. Bring up a standby master - if HA setup is in place (active-passive/active-active).
3. Re-deploy jenkins - on a new server/VM/Container , then restore JENKINS\_HOME.
4. For cloud setups - use infrastructure as code (terraform/ansible/docker/k8) to quickly recreates jenkins.

4] 1. Revoke the taken immediately in a github (security risk)
2. Audit logs to check if the token was with least privilege
3. rotate secrets  - generate a new token with least privilege
4. update jenkins credentials store with the new token
5. prevent future leaks - mask credentials in jenkins(withCredentials, secret masking plugins)

