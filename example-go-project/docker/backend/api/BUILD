docker_image(
    name="dev-backend-api",
    description="backend api server image for dev environment",
    tags=["example-go-project", "dev-image", "dev-backend-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="dev",
    dependencies=[
        "example-go-project/docker/common/go:dev-common-go",
        ":build",
        ":vscode-extensions",
    ],
    extra_build_args=[
        "TARGET=dev",
        "DOCKER_FILE_PATH=./example-go-project/docker/backend/api",
        "VSCODE_EXTENSIONS_JSON=extensions.json",
        "APP_DIR=app",
        "PORT=8081",
    ],
)

file(name="build", source="BUILD")
file(name="vscode-extensions", source="extensions.json")
