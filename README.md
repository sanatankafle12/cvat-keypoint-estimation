CVAT Keypoint Estimation
Custom CVAT with Pose Estimation

This repository is a modified version of the CVAT tool, adapted to run a custom pose estimation model.
Modifications

This version includes:

    A custom pose estimation model integrated for specific annotation tasks.

License

The original CVAT code is licensed under the MIT License.
CVAT with Serverless Machine Learning Models

The steps to deploy CVAT using Nuclio and run a model in CVAT are detailed below:
1. Docker Compose to Set Up CVAT

docker compose -f docker-compose.yml -f components/serverless/docker-compose.serverless.yml up -d

    Purpose: Initializes the CVAT application along with its serverless components.
    Details:
        -f docker-compose.yml: Specifies the primary Docker Compose file for the base CVAT setup.
        -f components/serverless/docker-compose.serverless.yml: Adds additional configurations to enable serverless functionality in CVAT.
        up -d: Starts the defined services in detached mode, allowing them to run in the background.
    Outcome: Both CVAT and its serverless infrastructure are deployed and running as Docker containers.

2. Download the Nuclio CLI (nuctl)

wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-linux-amd64

    Purpose: Downloads the Nuclio command-line interface (CLI), used for managing serverless functions.
    Details:
        wget: Downloads files from the specified URL.
        The URL points to the 1.13.0 release of the Nuclio CLI binary for Linux systems.
    Outcome: The nuctl CLI binary is saved to the current directory.

3. Make the nuctl Executable

sudo chmod +x nuctl-1.13.0-linux-amd64

    Purpose: Adds executable permissions to the downloaded nuctl binary.
    Details:
        sudo: Runs the command with administrator privileges to modify file permissions.
        chmod +x: Adds the executable permission to the file.
    Outcome: The nuctl binary can now be executed from the command line.

4. Add nuctl to the System Path

sudo ln -sf $(pwd)/nuctl-1.13.0-linux-amd64 /usr/local/bin/nuctl

    Purpose: Creates a symbolic link to the nuctl binary, making it accessible from anywhere on the system.
    Details:
        ln -sf: Creates or updates a symbolic link (-s for symbolic and -f to force replacement).
        $(pwd): Expands to the current working directory where the nuctl binary is located.
        /usr/local/bin/nuctl: Adds the link to the system’s executable search path.
    Outcome: The nuctl CLI can now be run from any location in the terminal.

5. Create a Nuclio Project

nuctl create project cvat

    Purpose: Initializes a new Nuclio project named cvat.
    Details:
        Projects in Nuclio serve as logical containers for related serverless functions, making it easier to organize and manage them.
    Outcome: A project named cvat is created in Nuclio.
