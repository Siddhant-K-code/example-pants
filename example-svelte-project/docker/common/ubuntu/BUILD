docker_image(
    name="dev-common-ubuntu",
    description="base ubuntu image for dev environment",
    tags=["example-svelte-project", "dev-image", "dev-common-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="dev",
    dependencies=[":build"],
    extra_build_args=[
        "UBUNTU_VERSION=24.04",
        "USER_PASSWORD=devstage-sid",
    ],
)

docker_image(
    name="prod-common-ubuntu",
    description="base ubuntu image for prod environment",
    tags=["example-svelte-project", "prod-image", "prod-common-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="prod",
    dependencies=[":build"],
    extra_build_args=[
        "UBUNTU_VERSION=24.04",
        "USER_PASSWORD=devprod-sid",
    ],
)

file(name="build", source="BUILD")
