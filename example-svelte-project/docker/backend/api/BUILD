docker_image(
    name="dev-backend-api",
    description="backend api server image for dev environment",
    tags=["example-svelte-project", "dev-image", "dev-backend-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="dev",
    dependencies=[
        "example-svelte-project/docker/common/mise:dev-common-mise",
        ":build",
        ":vscode-extensions",
    ],
    extra_build_args=[
        "TARGET=dev",
        "DOCKER_FILE_PATH=./example-svelte-project/docker/backend/api",
        "VSCODE_EXTENSIONS_JSON=extensions.json",
        "NODE_VERSION=20.14.0",
        "APP_DIR=app",
        "PORT=5173",
        "BACKEND_PROJECT_NAME=backend"
    ],
)

file(name="build", source="BUILD")
file(name="vscode-extensions", source="extensions.json")
