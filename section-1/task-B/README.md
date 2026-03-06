### Building and running the application

Start the application by running:
`docker compose -f docker-compose.yml up`.

The application will be available at http://localhost:5000.

### Notes
Dockerfile - classic single-stage version
Dockerfile_multi-stage - alternative multi-stage version

Benefit of the multi-stage version is that build phase and runtime phase are separated, meaning that build tools, dependencies and artifacts are not included in the final runtime image.
This results in cleaner production images with reduced image size and better security, containing only the necessary components to run the app.

