### Deploy Laravel Using Ansistrano

## Prepare

* Please install `python-simplejson, apt-transport-https, ca-certificates` on **Remote server**:

    ```
    sudo apt-get install -y python-simplejson apt-transport-https ca-certificates
    ```

## Usage

### Config

* Add **Drone's** project public key to github/bitbucket (scm) **Deploy keys** and Remote server file: `~/.ssh/authorized_keys`
* Copy `.ansistrano` folder and `.drone.yml` to your Laravel folder.
* You have to change some configurations in the following files:
    * Ansible’s inventory file: `.ansistrano/production` and `.ansistrano/staging`
        * We have 2 servers: [webservers] and [dbservers] server, please change both of them (it can be the same)
        * Change IP address host, ssh user (`ansible_ssh_user`), ssh port (`ansible_ssh_port`)
    * All variables need to change: `deploy.yml`
        * **server_name**: Server/Domain name
        * **nginx_config_name**: Nginx config file name
        * **php_version**: Server php version
        * **ansistrano_deploy_to**: Base path to deploy to server.
        * **ansistrano_shared_paths**: Shared paths to symlink to release dir
        * **ansistrano_shared_files**: Shared files to symlink to release dir
        * **ansistrano_git_repo**: Github/Bitbucket (scm)
        * **ansistrano_git_branch**: Git branch name for deployment

* Deployment strategy

```
-- /var/www/my-app.com
|-- current -> /var/www/my-app.com/releases/20100512131539
|-- releases
|   |-- 20100512131539
|   |-- 20100509150741
|   |-- 20100509145325
|-- shared
|   |-- .env
|   |-- node_modules
|   |-- storage
```

### Commands:

* For deployment

    ```
    ansible-playbook -i production deploy.yml --extra-vars='ansible_become_pass={become_password}'
    ```

* Modify commands in `.drone.yml` file.