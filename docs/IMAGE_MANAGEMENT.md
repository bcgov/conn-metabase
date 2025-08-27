The below steps must be done when a version change on Metabase is needed, so that test and prod can properly pull the new tag being used.

# Login to OpenShift registry

oc project b40eb8-tools
oc registry login

# Pull from Docker Hub (force x86_64 architecture)

podman pull --arch amd64 docker.io/metabase/metabase:v0.54.2

# Tag with the correct version

podman tag docker.io/metabase/metabase:v0.54.2 \
 image-registry.apps.silver.devops.gov.bc.ca/b40eb8-tools/metabase:v0.54.2

# Push to internal registry

podman push \
 image-registry.apps.silver.devops.gov.bc.ca/b40eb8-tools/metabase:v0.54.2

Alternatively, using Docker

# Login to OpenShift registry

oc project b40eb8-tools
oc registry login

# Pull from Docker Hub (force x86_64 architecture)

docker pull --platform linux/amd64 docker.io/metabase/metabase:v0.54.2

# Tag with the correct version for the internal registry

docker tag docker.io/metabase/metabase:v0.54.2 \
 image-registry.apps.silver.devops.gov.bc.ca/b40eb8-tools/metabase:v0.54.2

# Push to internal registry

docker push \
 image-registry.apps.silver.devops.gov.bc.ca/b40eb8-tools/metabase:v0.54.2
