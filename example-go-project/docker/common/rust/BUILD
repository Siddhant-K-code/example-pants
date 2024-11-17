docker_image(
    name="dev-common-go",
    description="base go image for dev environment",
    tags=["example-go-project", "dev-image", "dev-common-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="dev",
    dependencies=["example-go-project/docker/common/ubuntu:dev-common-ubuntu", ":build"],
    extra_build_args=["TARGET=dev", "GO_VERSION=1.79.0"],
)

file(name="build", source="BUILD")
