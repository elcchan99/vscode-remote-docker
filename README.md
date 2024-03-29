# Try Out Development Remote Containers: Python

This is a sample project that lets you try out the **[VS Code Remote - Containers](https://aka.ms/vscode-remote/containers)** extension in a few easy steps.

> **Note:** If you're following the quick start, you can jump to the [Things to try](#things-to-try) section. 

## Setting up the development container

Follow these steps to open this sample in a container:

1. If this is your first time using a development container, please follow the [getting started steps](https://aka.ms/vscode-remote/containers/getting-started).

2. **Linux users:** Update `USER_UID` and `USER_GID` in `.devcontainer/Dockerfile` with your user UID/GID if not 1000 to avoid creating files as root.

3. If you're not yet in a development container:
   - Clone this repository.
   - Press <kbd>F1</kbd> and select the **Remote-Containers: Open Folder in Container...** command.
   - Select the cloned copy of this folder, wait for the container to start, and try things out!
   
## Setting up the Virtual Box - VM

Follow these steps to setup Virtual Box - VM
Linux VM is expected

1. Install docker in VM
    - https://docs.docker.com/install/linux/docker-ce/ubuntu/
2. Turn dockerd to a systemd service and expose port
    - https://nickjanetakis.com/blog/docker-tip-73-connecting-to-a-remote-docker-daemon
3. Set VM network type to Bridge
4. Makesure your HOST can access VM's dockerd
    - `curl {vm-ip}:{dockerd-port}`
    - Can access if `{"message":"page not found"}`
    - Cannot access if `Connection refused`
    - Check whether your VM firewall blocks the port
5. Share source directory in Host to VM
    - https://askubuntu.com/questions/1073024/how-do-i-set-up-a-virtual-box-shared-folder-in-an-ubuntu-18-04-vm-on-a-windows-1?noredirect=1&lq=1
    - https://askubuntu.com/questions/1121705/how-to-share-a-directory-from-host-to-guest-machine-in-virtualbox
    - https://askubuntu.com/questions/22743/how-do-i-install-guest-additions-in-a-virtualbox-vm
    - expect /media/sf_{your-directory} is mounted to your HOST directory
6. Configure VSCode to use VM's dockerd
    - add settings.json in .vscode directory
    - `"docker.host"="tcp://{vm-ip}:{dockerd-port}"`
7. Configure devcontainer to use docker-compose
    - mount VM volumes to Containers
8. Reopen folder in Container

## Things to try

Once you have this sample opened in a container, you'll be able to work with it like you would locally. 

> **Note:** This container runs as a non-root user with sudo access by default. Comment out `"runArgs": ["-u", "vscode"]` in `.devcontainer/devcontainer.json` if you'd prefer to run as root.

Some things to try:

1. **Edit:**
   - Open `app.py`
   - Try adding some code and check out the language features.
2. **Terminal:** Press <kbd>ctrl</kbd>+<kbd>shift</kbd>+<kbd>\`</kbd> and type `uname` and or other Linux commands from the terminal window.
3. **Build, Run, and Debug:**
   - Open `app.py`
   - Add a breakpoint (e.g. on line 9).
   - Press <kbd>F5</kbd> to launch the app in the container.
   - Once the breakpoint is hit, try hovering over variables (e.g. the app variable on line 7), examining locals, and more.
   - Continue, then open a local browser and go to `http://localhost:9000` and note you can connect to the server in the container
4. **Forward another port:**
   - Stop debugging and remove the breakpoint.
   - Open `.vscode/launch.json`
   - Change the server port to 5000 on line 20. (`"--port","5000"`)
   - Press <kbd>F5</kbd> to launch the app in the container.
   - Press <kbd>F1</kbd> and run the **Remote-Containers: Forward Port from Container...** command.
   - Select port 5000.
   - Click "Open Browser" in the notification that appears to access the web app on this new port.

### More samples

- [Tweeter App - Python and Django](https://github.com/Microsoft/python-sample-tweeterapp)

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## License

Copyright © Microsoft Corporation All rights reserved.<br />
Licensed under the MIT License. See LICENSE in the project root for license information.
