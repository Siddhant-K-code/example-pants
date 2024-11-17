docker_image(
    name="dev-frontend-vite",
    description="frontend vite server image for dev environment",
    tags=["example-go-project", "dev-image", "dev-frontend-image"],
    source="Dockerfile",
    image_tags=["{build_args.GIT_CURRENT_BRANCH}"],
    target_stage="dev",
    dependencies=[
        "example-go-project/docker/common/mise:dev-common-mise",
        ":build",
        ":vscode-extensions",
    ],
    extra_build_args=[
        "TARGET=dev",
        "DOCKER_FILE_PATH=./example-go-project/docker/frontend/vite",
        "VSCODE_EXTENSIONS_JSON=extensions.json",
        "NODE_VERSION=20.14.0",
        "APP_DIR=app",
        "PORT=5173",
        "FRONTEND_PROJECT_NAME=client"
    ],
)

file(name="build", source="BUILD")
file(name="vscode-extensions", source="extensions.json")
