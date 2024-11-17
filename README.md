# example-pants

A sample repository demonstrating the usage of the [Pants](https://www.pantsbuild.org/) build system.

## Repository structure

```sh
.
├── example-go-project
│   ├── app
│   │   ├── backend
│   │   └── frontend
│   └── docker
│       ├── backend
│       │   ├── api
│       │   │   ├── BUILD
│       │   │   ├── Dockerfile
│       │   │   └── extensions.json
│       │   └── batch
│       │       ├── BUILD
│       │       ├── Dockerfile
│       │       └── extensions.json
│       ├── common
│       │   ├── mise
│       │   │   ├── BUILD
│       │   │   └── Dockerfile
│       │   ├── rust
│       │   │   ├── BUILD
│       │   │   └── Dockerfile
│       │   └── ubuntu
│       │       ├── BUILD
│       │       ├── Dockerfile
│       │       └── Tiltfile
│       └── frontend
│           └── vite
│               ├── BUILD
│               ├── Dockerfile
│               └── extensions.json
├── example-svelte-project
│   ├── app
│   │   ├── backend
│   │   └── frontend
│   └── docker
│       ├── backend
│       │   ├── api
│       │   │   ├── BUILD
│       │   │   ├── Dockerfile
│       │   │   └── extensions.json
│       │   └── batch
│       │       ├── BUILD
│       │       ├── Dockerfile
│       │       └── extensions.json
│       ├── common
│       │   ├── mise
│       │   │   ├── BUILD
│       │   │   └── Dockerfile
│       │   └── ubuntu
│       │       ├── BUILD
│       │       └── Dockerfile
│       └── frontend
│           └── vite
│               ├── BUILD
│               ├── Dockerfile
│               └── extensions.json
├── pants
└── pants.toml
```

## Install

Install pants by running:

```bash
curl --proto '=https' --tlsv1.2 -fsSL https://static.pantsbuild.org/setup/get-pants.sh | bash
```
