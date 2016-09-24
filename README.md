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
    * `Pending`

### Commands:

* For deployment

    ```
    ansible-playbook -i production deploy.yml --extra-vars='ansible_become_pass={become_password}'
    ```

* Modify commands in `.drone.yml` file.