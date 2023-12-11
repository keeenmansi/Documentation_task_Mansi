# Superset

## 1 . Task Requirement

To run the **superset** with a **podman play kube** which is generated with the helm chart of the
superset.

### Definition of Superset 

Apache Superset is an open-source business intelligence platform with a web-based interface for exploring, analyzing, and visualizing data from various sources. Users can create interactive dashboards, charts, and graphs without extensive coding. Developed by the Apache Software Foundation, Superset supports integration with diverse databases, making it versatile for data exploration and reporting.

### Definition of Podman play kube 

Podman play kube will be read in a structured file of Kubernetes YAML. It will then recreate
the containers, pods or volumes described in the YAML.

## 2 . Environment Details

Name: Ubuntu

Version: 20.04.6 LTS (Focal Fossa)

ID: ubuntu

ID Like: debian

Pretty Name: Ubuntu 20.04.6 LTS

Version ID: 20.04

## My System Configuration

CPU:  Intel Core i5-8350U CPU @ 1.70GHz x 8

RAM:  8GB (4GB x 2 SODIMM DDR4)  

Storage:  512GB   


## 3 . List of Tools and Technologies

Podman version 3.4.2

Helm version 3.12.1 

Vim 

Bash

## 4 . Definition of Tools

Podman - It is an open-source tool for developing, managing, and running containers
on your Linux systems.

Helm - It is a tool that streamlines installing and managing Kubernetes applications.

Vim - It is a highly configurable text editor built to create and changing any
kind of text very efficient.

Bash - It is the command line shell that you encounter when you open the terminal on
most Unix operating systems, like MacOS and Linux.

## 5 . The command for the setup or configuration

**Step 1. Run the following command to install curl.**

```python
sudo apt install curl
```
- sudo: Provides administrative privileges to the command.
- apt: Refers to the APT package manager used for managing software.
- install: Specifies the action to be taken, which is to install a package.
- curl: The name of the package to be installed, a command-line tool for URL-related data transfer.


> curl is a command-line tool that allows you to fetch data from the internet. It's like a web browser for your terminal. You can use it to download files, make web requests, and interact with web services directly from the command line.

![Alt text](../../webpreview_htm_d3474f1010434ed3.png)


**Step 2: Adding Helm GPG key.**
```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
```

- `curl https://baltocdn.com/helm/signing.asc`: This uses the `curl` command-line tool to download the contents of the specified URL, which appears to be the GPG (GNU Privacy Guard) signing key for Helm, a package manager for Kubernetes.  
- `gpg --dearmor`: This uses the `gpg` command to dearmor the GPG key. In GPG, "dearmor" means to convert a GPG public or private key from the binary format to a text-based format. This is often done for distribution or storage purposes.  
- `sudo tee /usr/share/keyrings/helm.gpg > /dev/null`: This part of the command uses `tee` to write the output of the previous `gpg` command to the file `/usr/share/keyrings/helm.gpg`.  
- The `> /dev/null` part at the end redirects the standard output (stdout) to the "null" device .

  
>  this command sets up the security key needed for Helm to ensure the integrity of the software it installs.


![Alt text](image1.png)
  
**Step 3: Adding Helm Repository to Package Sources.**

```bash
 echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
```

- This line tells the apt package manager to download Helm packages from the `https://baltocdn.com/helm/stable/debian/` repository.
- The `arch=$(dpkg --print-architecture)` part tells the apt package manager to download the correct package for your system architecture.
- The `signed-by=/usr/share/keyrings/helm.gpg` part tells the apt package manager to verify the authenticity of the packages using the GPG key that is stored in the file `/usr/share/keyrings/helm.gpg`.
- Creates a new file called `helm-stable-debian.list` in the directory `/etc/apt/sources.list.d/`.
- It adds the following line to the file:
deb [arch=(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main


  > this command adds the Helm repository to your system's list of software sources, allowing you to install Helm and related software packages from that repository.


 ![Alt text](im2.png)


**Step 4: Update system repositories.**

```bash
sudo apt update
```
-  sudo: This part of the command is used to execute the following command with administrative or superuser privileges.

-  apt: Refers to the APT package manager, which is commonly used on Debian-based Linux distributions like Ubuntu.

-  update: This is the action you want APT to perform. When you run "sudo apt update," it instructs APT to update the package lists and information about available software packages from the configured repositories.

  
> Running "sudo apt update" ensures that your system is aware of the latest software packages and updates available in the repositories. This is an essential step before installing or upgrading software to make sure you're working with the most current package information.


![Alt text](image.png)  

**Step 5: Install helm.**

```bash
sudo apt install helm
```
or

```python
sudo snap install helm --classic
```

* `sudo`: This prefix is used to execute the command with superuser (administrator) privileges. It allows you to install software system-wide.
* `apt`: The package management tool used for managing software packages on Debian-based systems.
* `install`: A command to instruct apt to install a specified package.
* `helm`: The name of the package you want to install. In this case, "Helm" is a tool used for managing Kubernetes applications. Helm simplifies the process of deploying and managing complex applications on Kubernetes clusters.


>  This command is used to add Helm to your system, allowing you to manage and deploy applications on a Kubernetes cluster effectively.



![Alt text](im4.png)

**Step 6: Verifying the installation and
version.**

```bash
helm version
```
![Alt text](im5.png)

**Step 7: Create directory.**
```bash
mkdir superset-poc
```


* `mkdir`:  It's used to create a new directory (folder) in the file system.
* `superset-poc`: This is the name of the directory you want to create.   


**Step 8: Go in to directory.**

```bash
cd superset-poc
```
* `cd`: Stands for "change directory." It's a command used to navigate through the file system by changing your current working directory.

* `superset-poc`: This is the directory you want to move into. It's the name of the target directory you're switching to.

![Alt text](im6.png)

**Step 9: Run the command to install vim.**

```bash
sudo apt install vim
```
- `sudo`: This part of the command is used to execute it with administrative or superuser privileges, allowing you to install software system-wide.

- `apt`: Refers to the APT package manager, which is commonly used on Debian-based Linux distributions like Ubuntu to manage software packages.

- `install`: Specifies the action to be performed, which is to install a package.

- `vim`: This is the name of the package you want to install. "Vim" is a highly configurable, efficient, and powerful text editor, often used by programmers and system administrators for editing files in the terminal.


![ ](../../12.png) 



**Step 10: Create yaml file  and add details in it.** 

To check system IP, run the below command.
```
hostname -I
```

Now open host file, add domain and IP.
```bash
 sudo vim /etc/hosts
```


And add :   
`192.168.xxx.xxx` `sample.com` and save the file.  


![](hostimage.png)


**Create values-stage.yaml file**

```bash
vim values-stage.yaml
```

* `vim`: This is a command-line text editor that allows you to create, view, and edit text files directly within the terminal.
* `value-stage.yaml`: This is the name of the file you will open.




```yaml
global:
  hosts:
    domain: sample.com
postgresql:
  image:
    tag: 14.0
certmanager-issuer:
  email: mansi_01@sample.com

```  
**Note** :   
"In the values-stage.yaml file,  modify the domain and email according to your specific requirements.To save a file in Vim, press Esc and then type :wq! followed by Enter"

"When you copy and paste to another place, the indentation gets messed up, so pay attention to the indentation."
      


**Step 11: Generate Kubernetes manifests for deploying the Superset application.**

```bash
helm template --dry-run --debug superset/superset --generate-name --values values-stage.yaml > superset-kube.yaml
```

- `helm template`: This is the command that tells Helm to generate Kubernetes manifests based on a Helm chart.
- `--dry-run`: This  indicates  Helm will simulate the installation without actually deploying anything. This is useful for seeing what manifests would be generated without affecting the cluster.
- `--debug`: This enables debug output, providing more detailed information about the Helm template process.
- `superset/superset`: This specifies the Helm chart to use for generating the Kubernetes manifests. The chart name is in the format `repository/chart-name`.
- `--generate-name`: This generates a unique name for the release based on the chart's name. It's used when you want to create a new release without specifying a release name.
- `--values values-stage.yaml`: This  points to a values file (`values-stage.yaml`) that provides custom configuration values for the Helm chart.

- `superset-kube.yaml`: This part of the command uses the output redirection (`>`) to save the generated Kubernetes manifests to a file named `superset-kube.yaml`.

> In summary, this command generates Kubernetes manifests for deploying the Superset application using a specific Helm chart and custom configuration values from the `values-stage.yaml` file. The generated manifests are saved in the `superset-kube.yaml` file. The use of `--dry-run` and `--debug` ensures that we can preview the manifests before actually deploying the application, it helps to  verify that the configuration is correct.


![Alt text](im8.png)


Problem 1. There we got above error .

For solving this, run below commands.
```
helm repo add superset https://apache.github.io/superset

```
``` 
helm repo update
```

For this I follow this link: https://stackoverflow.com/questions/66706363/where-is-the-superset-helm-chart




```
helm template --dry-run --debug superset/superset --generate-name --values values-stage.yaml > superset-kube.yaml

```

![Alt text](im10.png)

**Step 12: Edit this  superset-kube.yaml and create a new final.yaml as per the requirement in podman play kube.**

Add the below data -

```bash
cat superset-kube.yaml   
```
- Copy the output and paste in to new file final.yaml.
```bash
vim final.yaml           
```

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubepostgresql
spec:
  replicas: 1
  template:
    metadata:
      name: kubepostgresql
    spec:
      serviceAccountName: default
      securityContext:
        fsGroup: 1001
      hostNetwork: true
      hostIPC: false
      initContainers: []
      containers:
        - name: postgresql
          image: docker.io/bitnami/postgresql:14.6.0-debian-11-r13
          imagePullPolicy: "IfNotPresent"
          securityContext:
            runAsUser: 1001
          env:
            - name: BITNAMI_DEBUG
              value: "false"
            - name: POSTGRESQL_PORT_NUMBER
              value: "5432"
            - name: POSTGRESQL_VOLUME_DIR
              value: "/bitnami/postgresql"
            - name: PGDATA
              value: "/bitnami/postgresql/data"
            - name: POSTGRES_USER
              value: "superset"
            - name: POSTGRES_POSTGRES_PASSWORD
              value: "superset"
            - name: POSTGRES_PASSWORD
              value: "superset"
            - name: POSTGRES_DB
              value: "superset"
            - name: POSTGRESQL_ENABLE_LDAP
              value: "no"
            - name: POSTGRESQL_ENABLE_TLS
              value: "no"
            - name: POSTGRESQL_LOG_HOSTNAME
              value: "false"
            - name: POSTGRESQL_LOG_CONNECTIONS
              value: "false"
            - name: POSTGRESQL_LOG_DISCONNECTIONS
              value: "false"
            - name: POSTGRESQL_PGAUDIT_LOG_CATALOG
              value: "off"
            # Others
            - name: POSTGRESQL_CLIENT_MIN_MESSAGES
              value: "error"
            - name: POSTGRESQL_SHARED_PRELOAD_LIBRARIES
              value: "pgaudit"
          ports:
            - name: tcp-postgresql
              containerPort: 5432
          resources:
            limits: {}
            requests:
              cpu: 250m
              memory: 256Mi
          volumeMounts:
            - name: data
              mountPath: /bitnami/postgresql
      volumes:
        - name: data
          hostPath:
            path: /home/maansi/superset-poc/postgres/

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: kuberedis-master
spec:
  replicas: 1
  template:
    spec:
      securityContext:
        fsGroup: 1001
      terminationGracePeriodSeconds: 30
      containers:
        - name: redis
          image: docker.io/bitnami/redis:7.0.10-debian-11-r4
          imagePullPolicy: "IfNotPresent"
          securityContext:
            runAsUser: 1001
          command:
            - /bin/bash
          args:
            - -c
            - /opt/bitnami/scripts/start-scripts/start-master.sh
          env:
            - name: BITNAMI_DEBUG
              value: "false"
            - name: REDIS_REPLICATION_MODE
              value: "master"
            - name: ALLOW_EMPTY_PASSWORD
              value: "yes"
            - name: REDIS_TLS_ENABLED
              value: "no"
            - name: REDIS_PORT
              value: "6379"
          ports:
            - name: redis
              containerPort: 6379
              hostPort: 6379
          resources:
            limits: {}
            requests: {}
          volumeMounts:
            - name: start-scripts
              mountPath: /opt/bitnami/scripts/start-scripts/start-master.sh
              subPath: start-master.sh
            - name: redis-data
              mountPath: /data
            - name: config
              mountPath: /opt/bitnami/redis/mounted-etc
      volumes:
        - name: start-scripts
          hostPath:
            path: /home/maansi/superset-poc/redis/start-master.sh
            type: FileOrCreate
            defaultMode: 0777
        - name: config
          hostPath:
            path: /home/maansi/superset-poc/redis/redis-conf
            type: Directory
        - name: redis-data
          hostPath:
            path: /home/maansi/superset-poc/redis/redis-data

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubesuperset-worker
spec:
  replicas: 1
  template:
    spec:
      securityContext:
        runAsUser: 0
      initContainers:
        - command:
            - /bin/sh
            - -c
            - dockerize -wait "tcp://192.168.xxx.xxx:5432" -wait "tcp://192.168.xxx.xxx:6379" -timeout 120s
          env:
            - name: REDIS_HOST
              value: 192.168.xxx.xxx
            - name: REDIS_PORT
              value: "6379"
            - name: DB_HOST
              value: 192.168.xxx.xxx
            - name: DB_PORT
              value: "5432"
            - name: DB_USER
              value: "superset"
            - name: DB_PASS
              value: "superset"
            - name: DB_NAME
              value: "superset"
          image: 'apache/superset:dockerize'
          imagePullPolicy: 'IfNotPresent'
          name: wait-for-postgres-redis
      containers:
        - name: superset
          image: "apachesuperset.docker.scarf.sh/apache/superset:2.1.0"
          imagePullPolicy: IfNotPresent
          command: ["/bin/sh","-c",". /app/pythonpath/superset_bootstrap.sh; celery --app=superset.tasks.celery_app:app worker"]
          env:
            - name: "SUPERSET_PORT"
              value: "8088"
            - name: REDIS_HOST
              value: 192.168.xxx.xxx
            - name: REDIS_PORT
              value: "6379"
            - name: DB_HOST
              value: 192.168.xxx.xxx
            - name: DB_PORT
              value: "5432"
            - name: DB_USER
              value: "superset"
            - name: DB_PASS
              value: "superset"
            - name: DB_NAME
              value: "superset"
          volumeMounts:
            - name: superset-config
              mountPath: "/app/pythonpath"
              readOnly: true
          livenessProbe:
            exec:
              command:
                - sh
                - -c
                - celery -A superset.tasks.celery_app:app inspect ping -d celery@$HOSTNAME
            failureThreshold: 3
            initialDelaySeconds: 120
            periodSeconds: 60
            successThreshold: 1
            timeoutSeconds: 60
          resources: {}
      volumes:
        - name: superset-config
          hostPath:
            path: /home/maansi/superset-poc/superset/

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubesuperset
spec:
  replicas: 1
  template:
    spec:
      securityContext:
        runAsUser: 0
      initContainers:
        - command:
            - /bin/sh
            - -c
            - dockerize -wait "tcp://192.168.xxx.xxx:5432" -timeout 120s
          env:
            - name: REDIS_HOST
              value: 192.168.xxx.xxx
            - name: REDIS_PORT
              value: "6379"
            - name: DB_HOST
              value: 192.168.xxx.xxx
            - name: DB_PORT
              value: "5432"
            - name: DB_USER
              value: "superset"
            - name: DB_PASS
              value: "superset"
            - name: DB_NAME
              value: "superset"
          image: 'apache/superset:dockerize'
          imagePullPolicy: 'IfNotPresent'
          name: wait-for-postgres
      containers:
        - name: superset
          image: "apachesuperset.docker.scarf.sh/apache/superset:2.1.0"
          imagePullPolicy: IfNotPresent
          command: ["/bin/sh","-c",". /app/pythonpath/superset_bootstrap.sh; /usr/bin/run-server.sh"]
          env:
            - name: "SUPERSET_PORT"
              value: "8088"
            - name: REDIS_HOST
              value: 192.168.xxx.xxx
            - name: REDIS_PORT
              value: "6379"
            - name: DB_HOST
              value: 192.168.xxx.xxx
            - name: DB_PORT
              value: "5432"
            - name: DB_USER
              value: "superset"
            - name: DB_PASS
              value: "superset"
            - name: DB_NAME
              value: "superset"
          volumeMounts:
            - name: superset-config
              mountPath: "/app/pythonpath"
              readOnly: true
          ports:
            - name: http
              containerPort: 8088
              hostPort: 8088
              protocol: TCP
          resources: {}
      volumes:
        - name: superset-config
          hostPath:
            path: /home/maansi/superset-poc/superset/


```


Note : There i replace the path .
Example:

* path: /home/harsh/superset/redis/start-master.sh  
To this
path: /home/mansi/superset-poc/redis/start-master.sh

* change the ip with  system ip.   
* Also correct indentation of this yaml file.

Then save the file. 



**Step 13: Check list of file in current directory.**

```bash
ls -lrth    
```        
* It will list all of the files in the current directory .

![Alt text](im11.png)


**Step 14:  Create a script file and add details in it.**

```bash
vim pre-install-task.sh    
```

> Bash Script: A Bash script is a file containing a sequence of commands written in the Bash scripting language. These commands can include system commands, variable assignments, conditionals, loops, and more. Bash scripts are used to automate tasks, perform system administration, and execute a series of actions.

```bash
#!/bin/bash

mkdir superset
mkdir redis
mkdir postgres

cat <<- END > superset/superset_bootstrap.sh
	#!/bin/bash
	if [ ! -f ~/bootstrap ]; then echo "Running Superset with uid 0" > ~/bootstrap; fi

END

cat <<- END > superset/superset_config.py
import os
from cachelib.redis import RedisCache
    
def env(key, default=None):
	return os.getenv(key, default)
    
MAPBOX_API_KEY = env('MAPBOX_API_KEY', '')
CACHE_CONFIG = {
    	'CACHE_TYPE': 'RedisCache',
    	'CACHE_DEFAULT_TIMEOUT': 300,
    	'CACHE_KEY_PREFIX': 'superset_',
    	'CACHE_REDIS_HOST': env('REDIS_HOST'),
    	'CACHE_REDIS_PORT': env('REDIS_PORT'),
    	'CACHE_REDIS_PASSWORD': env('REDIS_PASSWORD'),
    	'CACHE_REDIS_DB': env('REDIS_DB', 1),
}
DATA_CACHE_CONFIG = CACHE_CONFIG
    
SQLALCHEMY_DATABASE_URI = f"postgresql+psycopg2://{env('DB_USER')}:{env('DB_PASS')}@{env('DB_HOST')}:{env('DB_PORT')}/{env('DB_NAME')}"
SQLALCHEMY_TRACK_MODIFICATIONS = True
SECRET_KEY = env('SECRET_KEY', 'thisISaSECRET_1234')
    
class CeleryConfig(object):
	CELERY_IMPORTS = ('superset.sql_lab', )
	CELERY_ANNOTATIONS = {'tasks.add': {'rate_limit': '10/s'}}
	BROKER_URL = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"
	CELERY_RESULT_BACKEND = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"
    
CELERY_CONFIG = CeleryConfig
RESULTS_BACKEND = RedisCache(
    	host=env('REDIS_HOST'),
    	port=env('REDIS_PORT'),
    	key_prefix='superset_results'
)
END
cat <<- END > superset/superset_init.sh
#!/bin/sh
set -eu
echo "Upgrading DB schema..."
superset db upgrade
echo "Initializing roles..."
superset init
    
echo "Creating admin user..."
superset fab create-admin \
           	--username admin \
                	--firstname Superset \
                	--lastname Admin \
                	--email admin@superset.com \
                	--password admin \
                	|| true
    
if [ -f "/app/configs/import_datasources.yaml" ]; then
   echo "Importing database connections.... "
   superset import_datasources -p /app/configs/import_datasources.yaml
fi
END
mkdir redis/redis-conf
cat <<- END > redis/redis-conf/master.conf
	dir /data
	# User-supplied master configuration:
	rename-command FLUSHDB ""
	rename-command FLUSHALL ""
	# End of master configuration
END

cat <<- END > redis/redis-conf/redis.conf
	appendonly yes
	save ""
END

cat <<- END > redis/redis-conf/replica.conf
    	dir /data
	rename-command FLUSHDB ""
	rename-command FLUSHALL ""
END

mkdir -p redis/redis-data
cat <<- END > redis/master-redis.sh
	#!/bin/bash
	[[ -f \$REDIS_PASSWORD_FILE ]] && export REDIS_PASSWORD="\$(< "\${REDIS_PASSWORD_FILE}")"
	if [[ -f /opt/bitnami/redis/mounted-etc/master.conf ]];then
    	cp /opt/bitnami/redis/mounted-etc/master.conf /opt/bitnami/redis/etc/master.conf
	fi
	if [[ -f /opt/bitnami/redis/mounted-etc/redis.conf ]];then
    	cp /opt/bitnami/redis/mounted-etc/redis.conf /opt/bitnami/redis/etc/redis.conf
	fi
	ARGS=("--port" "\${REDIS_PORT}")
	ARGS+=("--protected-mode" "no")
	ARGS+=("--include" "/opt/bitnami/redis/etc/redis.conf")
	ARGS+=("--include" "/opt/bitnami/redis/etc/master.conf")
	exec redis-server "\${ARGS[@]}"
END
chmod +x superset/superset_init.sh
chmod +x superset/superset_config.py
chmod +x superset/superset_bootstrap.sh

```


**Step 15: Check list of file in current directory.**

```
 ls -lrth
```

![Alt text](im12.png)

**Step 16: Give permission.** 
```bash
chmod +x pre-install-task.sh
```

- chmod : change the permissions of a file or directory.
- +x  : to add the execute permission to the file or directory.

![Alt text](im13.png)

**step 17: Run the script.** 

```bash
sh pre-install-task.sh
```
* `sh`: Command to run a shell interpreter.
* `pre-install-task.sh`: Name of the shell script file to be executed.

**Step 18: Check list of file in current directory.**

![Alt text](webpreview_htm_6ddad949c2ad712f.png)



**Step 19: Install podman.** 

```bash
sudo apt install podman    
```
Output:

![Alt text](img13A.png)

Problem 3: If you encountered an error while attempting to install Podman.

For solving this problem run below commands.

```bash
sudo sh -c "echo 'deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_$(lsb_release -rs)/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"

```

```bash
wget https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_$(lsb_release -rs)/Release.key

```
```bash
sudo apt-key add - < Release.key
```
```
sudo apt update
```

```
sudo apt install -y podman
```
```
podman --version
```
"Note : Adding a repository is required for Ubuntu 20 version and is not needed for the latest version of Ubuntu."


**Step 20: Create the pods and containers.** 

```
podman play kube final.yaml
```

> This command will create the pods and containers described in the file `final.yaml`. The containers within the pod will then be started, and the ID of the new Pod will be output. 

![Alt text](im14.png)



**Step 21: To see running  containers.**
```
podman ps 
```

![Alt text](im15.png)



* List the currently running containers managed by the Podman tool.
* Provides information about container IDs, names, status, ports, and more.

Go to the browser and write : 
```
192.168.xxx.xxx:8088/login/

```

  
If you encounter error after this follow given below steps.


```python
ls -lrth
```

![Alt text](webpreview_htm_6ddad949c2ad712f.png)

```
cd superset
```
![Alt text](<TCP load balancer Raw_htm_fc3a93f992bfebdf.png>)

```python
ls -lrth
```

![Alt text](ls-lrtg.png)

```
vim superset_config.py
```
```
import os
from cachelib.redis import RedisCache

def env(key, default=None):
    return os.getenv(key, default)

MAPBOX_API_KEY = env('MAPBOX_API_KEY', '')
CACHE_CONFIG = {
    'CACHE_TYPE': 'RedisCache',
    'CACHE_DEFAULT_TIMEOUT': 300,
    'CACHE_KEY_PREFIX': 'superset_',
    'CACHE_REDIS_HOST': env('REDIS_HOST'),
    'CACHE_REDIS_PORT': env('REDIS_PORT'),
    'CACHE_REDIS_PASSWORD': env('REDIS_PASSWORD'),
    'CACHE_REDIS_DB': env('REDIS_DB', 1),
}
DATA_CACHE_CONFIG = CACHE_CONFIG

SQLALCHEMY_DATABASE_URI = f"postgresql+psycopg2://{env('DB_USER')}:{env('DB_PASS')}@{env('DB_HOST')}:{env('DB_PORT')}/{env('DB_NAME')}"
SQLALCHEMY_TRACK_MODIFICATIONS = True
SECRET_KEY = env('SECRET_KEY', 'thisISaSECRET_1234')

class CeleryConfig(object):
    CELERY_IMPORTS = ('superset.sql_lab', )
    CELERY_ANNOTATIONS = {'tasks.add': {'rate_limit': '10/s'}}
    BROKER_URL = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"
    CELERY_RESULT_BACKEND = f"redis://{env('REDIS_HOST')}:{env('REDIS_PORT')}/0"

CELERY_CONFIG = CeleryConfig
RESULTS_BACKEND = RedisCache(
    host=env('REDIS_HOST'),
    port=env('REDIS_PORT'),
    key_prefix='superset_results'
)

```
![Alt text](<TCP load balancer Raw_htm_2af13ae72afe963a.png>)

> "Note :- Correct its indentation and save it."


Now Go to the browser and write : 

```
192.168.xxx.xxx:8088/login/
```
![Alt text](im16.png)



Problem 4 . Go to the browser and give password and username.


![Alt text](im17.png)

For the credential error run the below commands.

1. 

```
podman exec -it kubesuperset-pod-0-superset superset fab create-admin
```
> The command podman exec -it kubesuperset-pod-0-superset superset fab create-admin is used to interactively create an administrative user for Superset within a specific container (kubesuperset-pod-0-superset). This user will have the necessary privileges to manage and configure the Superset instance.

**Add username:** xxxxx

**First Name:** xxxxx

**Last Name:** xxxxx

**Email Id:** Here,we should write the email address that we had used in values-stage.yaml. (For example:mansi_01@sample.com).

2. 
```
podman exec -it kubesuperset-pod-0-superset superset db upgrade
```
> This command executes the Superset command-line interface (superset) inside the specified container (kubesuperset-pod-0-superset). The db upgrade part instructs Superset to apply any pending database migrations or updates. This is crucial for keeping the database schema in sync with the current version of Superset.

3. 
```
podman exec -it kubesuperset-pod-0-superset superset load_examples
```
> This command loads example data and configurations into Superset. It's beneficial for new users who want to explore Superset's capabilities by providing them with pre-built dashboards, charts, and datasets.
```
4. 
podman exec -it kubesuperset-pod-0-superset superset init
```
> This command initializes Superset. It often involves setting up default roles, permissions, and configurations necessary for Superset to function correctly. It's typically used during the initial setup to prepare the environment for first-time use.


![Alt text](im18.png)




Reference link

https://helm.sh/docs/intro/install/

https://docs.podman.io/en/v4.2/markdown/podman-play-kube.1.html

