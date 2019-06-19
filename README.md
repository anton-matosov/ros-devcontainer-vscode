ROS dev container for vscode
----------------------------
Packed with:
- Preconfigured docker image for ROS development.
- Browser accessible X11 server to display gazebo, rviz, rqt (runs on Windows/Mac).
- Tasks definition to run catkin_make, roscore, rviz commands.
- Preconfigured code completion for C++, Python, XML (package.xml, launchfiles, URDF, SDF).

![screenshot](https://user-images.githubusercontent.com/18067/58605055-8dc84980-82d1-11e9-8ee5-dc969fcb2ae1.png)

How to use this dev container
-----------------------------
First, you have to install VS Code and Docker for Windows/Mac:
- https://code.visualstudio.com/
- https://docs.docker.com/docker-for-mac/
- https://docs.docker.com/docker-for-windows/

After you installed required softwares:

1. Install ["Remote Development" extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) on your VS Code.
2. Clone this repository by using git command.
3. Click on the quick actions status bar item (green icon) in the lower left corner of the VS Code.
4. Select "Remote-Containers: Open Folder in Container..." from the command list that appears, and open the root folder of the project you just cloned.
5. You need to wait a while for container to come up (only required once).

For detailed instructions, see:
https://code.visualstudio.com/docs/remote/containers

If you are behind the proxy
-----------------------------

Please apply following two settings, if you are using your PC behind the proxy.

1. Proxy setting for the Docker server.

Click Docker Desktop task bar icon > Select `preference` menu item. You will see the following options:

![docker-proxy-settings](https://user-images.githubusercontent.com/18067/59744551-c4302d80-92ad-11e9-9b20-cc873a53a8bb.png)

In most cases, `System proxy` option will work. But if you have problem downloading the docker images, please try `Manual proxy configuration` option.

2. Proxy setting for the devcontainer.

This setting will enable you to use the `apt-get` or the other network commands inside the devcontainer.

First, open `.env.sample` file under the root folder of the cloned project.
Edit the settings according to your environment.
Save the file as name `.env`.

Next, open `docker-compose.yml` file under the root folder of the cloned project and uncomment the following lines:
```yaml
  workspace:
    env_file:
      - .env
```

How to reset or update the devcontainer
---------------------------------------

If you want to reset the devcontainer. Please close vscode and enter the following command under the folder of the cloned project:
```shell
$ docker-compose down
```

If you want to update the environment to the most recent version. Please enter the following command under the folder of the cloned project:
```shell
$ docker-compose pull
```

Please be noticed that the `docker-compose down` command will reset your enviromnent including installed `.deb` packages. However, if you write `package.xml` files correctly, you can reinstall all the depending packages by entering the following two commands:
```shell
$ rosdep update
$ rosdep install --from-paths src --ignore-src -r -y
```

How to open X11 server screen
-----------------------------

1. Wait for the container to start.
2. Open http://localhost:3000/ using your favorite browser.

If you are using Docker Toolbox, open the following URL instead:

http://192.168.99.100:3000/

If you want browser screen to be integrated with VS Code, use [Browser Preview for VS Code extension](https://marketplace.visualstudio.com/items?itemName=auchenberg.vscode-browser-preview).

Created by
----------
Yosuke Matsusaka (MID Academic Promotions, Inc.)