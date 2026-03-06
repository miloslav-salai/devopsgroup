# Task C – Docker Build Fails: (no space left on device)

## Error explanation

The CI machine ran out of disk space while building the Docker image.

## 1. Diagnose

First we should check what is actually full by running these two commands:

```bash
df -h              # shows overall disk usage
docker system df   # shows how much space Docker is using
```

## 2. Temporary Fix

Clean up unused Docker resources:

```bash
docker system prune  # removes stopped containers, unused images, and build cache
```

## 3. Permanent Fix

### Make improvements to the Dockerfile (reduce size of the image)

Provided Dockerfile uses `ubuntu:20.04` as a base image and installs node.js on top of that, which increases the image size. This is not necessary when we can simply use the `node` as a base image. If we use the slim or the alpine version, this one change can reduce the image size significantly.
We could also add a `.dockerignore` to further improve and reduce the size of the final build. This will exclude any unnecessary files from the image.

### Automated cleanup (scheduled or after every build)

We can turn the Temporary Fix (Step 2) into automated cleaning job by running the `docker system prune` command after every build (as a part of our CI pipeline).
Alternatively we can run this command as a part of scheduled maintenance, running it e.g. once a week using a cron job.

## 4. Monitoring

We can configure alerts or notifications to trigger when disk usage reaches a certain threshold (e.g. 80%), so the issue can be addressed in advance.