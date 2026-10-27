# Project 2 Rationale

## 1. Base Image Choice (nginx:alpine)
For the final stage, I chose `nginx:alpine` instead of a larger base image or continuing to use the full Node.js image. 

**Multi-stage build savings:**
By using a multi-stage build, the build tools (Node.js, npm, and dependencies) are left in the first stage. Only the compiled static `build/` output is copied to the final `nginx:alpine` image. 

*Measured sizes from T02:*
- Multi-stage image size: 93 MB
- Single-stage image size: 1.63 GB

The multi-stage image is significantly smaller, which means it pulls faster, consumes less storage, and presents a smaller attack surface since the Node.js toolchain is not present in production.

## 2. Service Split (Web and Cache)
I separated `cache` into its own service (using `redis:7-alpine`) rather than folding caching logic directly into the `web` service. 

**Week 3 Service Model framing:**
A container sits between IaaS and PaaS because it allows developers to decide exactly what they manage themselves and what they accept as a pre-built dependency. Writing a custom caching layer inside the web app increases complexity and operational burden. By composing a public `redis:7-alpine` image into the stack, I am treating caching as a pre-built dependency. The `depends_on: condition: service_healthy` ensures the web service does not start until the cache is fully ready, which makes the system reliable and the startup order explicit in code.

## References
- Docker Docs: Multi-stage builds (https://docs.docker.com/build/building/multi-stage/)
- Docker Docs: Control startup and shutdown order in Compose (https://docs.docker.com/compose/how-tos/startup-order/)
