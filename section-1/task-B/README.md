# Task B – Dockerize a Python Web App

## Building and running the application
Start the application by running:
```bash
docker compose up
```
The application will be available at http://localhost:5000.

## Dockerfile versions
`Dockerfile` - classic single-stage version  
`Dockerfile_multi-stage` - alternative multi-stage version

## Notes

### Single-stage version
Dockerfile was built using following rules according to best practices:
 - slim base image (reduced final image size)
 - specific versioning (instead of using latest tag)
 - separate app user to avoid running application as root (security best practice)
 - copying and installing dependencies before the app content (faster rebuilds)
 - `RUN python -m pip install` instead of `RUN pip install` (version alignment)
 - `--no-cache-dir` in pip install (cache is not stored inside the image)
 - CMD uses exec form (recommended over string form)

### Multi-stage version
Benefit of the multi-stage version is that build phase and runtime phase are separated, meaning that build tools, dependencies and artifacts are not included in the final runtime image.
This results in cleaner production images with reduced image size and improved security, containing only the necessary components to run the app.

