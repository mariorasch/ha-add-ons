# Copying existing Vaultwarden data from your local Mac to Home Assistant app

## Prerequisites

- Your Home Assistant instance is reachable at **homeassistant.local**.
- The SSH user is "root".
- Your Vaultwarden data is available locally on the your Mac at "~/vaultwarden".

## Steps

### 1. Install Advanced SSH & Web Terminal

Install the **[Advanced SSH & Web Terminal](https://github.com/hassio-addons/addon-ssh)** app in Home Assistant.

#### 1.1. Disable Safe Mode

In the "Information" tab, disable the **Safe Mode** option.

#### 1.2. SSH Configuration

In the configuration, use the **username** "**root**", add the **authorized_key** from your own Mac, and enable the options "**sftp**" (so that the "scp" command works) and "**zsh**".

### 2. Copy Vaultwarden Data

From your local Mac, using:

```bash
scp -rp ~/vaultwarden root@homeassistant.local:/data
```

copy the Vaultwarden data to the Home Assistant instance.

### 3. Stop the Vaultwarden app

### 4. Establish SSH Connection

In macOS Terminal, using:

```bash
ssh root@homeassistant.local
```

connect to your Home Assistant instance.

### 5. Check Docker Containers

Using:

```bash
docker ps
```

check the running Docker containers. There should be a container named **hassio_supervisor** running.

### 6. List Vaultwarden's app data folder

Using:

```bash
docker exec -it hassio_supervisor ls -al /data/addons/data
```

list the contents of the apps data folder. There should be a Vaultwarden data folder named **<id>_vaultwarden**.

### 7. Copy Vaultwarden data to app data folder

Copy the Vaultwarden data copied to the Home Assistant instance in step 2 using:

```bash
docker cp /data/vaultwarden/. hassio_supervisor:/data/addons/data/<id>_vaultwarden
```

to the above Vaultwarden app data folder.
