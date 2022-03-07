# devworkspace-telemetry-example-plugin

This project shows the completed telemetry plug-in example from the Che documentation [here](TODO: add link when ready).

When running in the context of a DevWorkspace, this plug-in receives telemetry events from the `onEvent()` method, and sends a `POST` request to an `/event` endpoint from a baseUrl of `http://little-telemetry-back-end-che.apps-crc.testing`.

This project requires a dependency from the GitHub Packages Maven registry, namely `org.eclipse.che.incubator.workspace-telemetry:backend-base`. See [Authenticating to GitHub Packages](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-apache-maven-registry#authenticating-to-github-packages) in order to authenitcate with GitHub credentials, and retrieve the dependency.

## Creating a container image
### Creating a Java-based image
With `GITHUB_USERNAME` and `GITHUB_TOKEN` set in `settings.xml`, run:
```
./mvnw --settings=settings.xml package && \\
docker build -f src/main/docker/Dockerfile.jvm -t image:tag .
```

### Creating a Quarkus native image
With `GITHUB_USERNAME` and `GITHUB_TOKEN` set in `settings.xml`, run:
```
./mvnw --settings=settings.xml package -Pnative -Dquarkus.native.container-build=true && \\
docker build -f src/main/docker/Dockerfile.native-micro -t image:tag .
```