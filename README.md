
1 - Instalando Minishift:

$ wget https://github.com/minishift/minishift/releases/download/v1.13.1/minishift-1.13.1-linux-amd64.tgz
$ tar -xf minishift-1.13.1-linux-amd64.tgz
$ sudo mv minishift-1.13.1-linux-amd64/minishift /usr/local/bin/ -v
'minishift-1.13.1-linux-amd64/minishift' -> '/usr/local/bin/minishift'
$ rm -rf minishift-1.13.1-linux-amd64

2 - Iniciando o minishift com virtualbox:

$ minishift start --vm-driver virtualbox

-- Starting profile 'minishift'
-- Checking if requested hypervisor 'virtualbox' is supported on this platform ... OK
-- Checking if VirtualBox is installed ... OK
-- Checking the ISO URL ... OK
-- Starting local OpenShift cluster using 'virtualbox' hypervisor ...
-- Minishift VM will be configured with ...
   Memory:    2 GB
   vCPUs :    2
   Disk size: 20 GB

   Downloading ISO 'https://github.com/minishift/minishift-b2d-iso/releases/download/v1.2.0/minishift-b2d.iso'
 40.00 MiB / 40.00 MiB [============================================] 100.00% 0s
-- Starting Minishift VM ............................ OK
-- Checking for IP address ... OK
-- Checking if external host is reachable from the Minishift VM ... 
   Pinging 8.8.8.8 ... OK
-- Checking HTTP connectivity from the VM ... 
   Retrieving http://minishift.io/index.html ... OK
-- Checking if persistent storage volume is mounted ... OK
-- Checking available disk space ... 0% used OK
   Importing 'openshift/origin:v3.7.1'  CACHE MISS
   Importing 'openshift/origin-docker-registry:v3.7.1'  CACHE MISS
   Importing 'openshift/origin-haproxy-router:v3.7.1'  CACHE MISS
-- Downloading OpenShift binary 'oc' version 'v3.7.1'
 38.51 MiB / 38.51 MiB [============================================] 100.00% 0s-- Downloading OpenShift v3.7.1 checksums ... OK
-- OpenShift cluster will be configured with ...
   Version: v3.7.1
-- Checking 'oc' support for startup flags ... 
   host-config-dir ... OK
   host-data-dir ... OK
   host-pv-dir ... OK
   host-volumes-dir ... OK
   routing-suffix ... OK
Starting OpenShift using openshift/origin:v3.7.1 ...
Pulling image openshift/origin:v3.7.1
Pulled 1/4 layers, 26% complete
Pulled 1/4 layers, 29% complete
Pulled 1/4 layers, 32% complete
Pulled 1/4 layers, 35% complete
Pulled 1/4 layers, 39% complete
Pulled 1/4 layers, 43% complete
Pulled 1/4 layers, 42% complete
Pulled 1/4 layers, 45% complete
Pulled 1/4 layers, 47% complete
Pulled 1/4 layers, 49% complete
Pulled 1/4 layers, 52% complete
Pulled 1/4 layers, 54% complete
Pulled 1/4 layers, 57% complete
Pulled 1/4 layers, 59% complete
Pulled 1/4 layers, 62% complete
Pulled 1/4 layers, 66% complete
Pulled 1/4 layers, 69% complete
Pulled 1/4 layers, 72% complete
Pulled 1/4 layers, 75% complete
Pulled 2/4 layers, 79% complete
Pulled 3/4 layers, 85% complete
Pulled 3/4 layers, 87% complete
Pulled 3/4 layers, 89% complete
Pulled 3/4 layers, 91% complete
Pulled 3/4 layers, 92% complete
Pulled 3/4 layers, 94% complete
Pulled 3/4 layers, 97% complete
Pulled 3/4 layers, 100% complete
Pulled 4/4 layers, 100% complete
Extracting
Image pull complete
OpenShift server started.

The server is accessible via web console at:
    https://192.168.99.100:8443

You are logged in as:
    User:     developer
    Password: 

To login as administrator:
    oc login -u system:admin

-- Exporting of OpenShift images is occuring in background process with pid 11656.

3 - Acessando minishift via linha de comando:

$ eval $(minishift docker-env)

$ oc login -u developer

$ docker login -u `oc whoami` -p `oc whoami -t` 172.30.1.1:5000

4 - Obtendo Dockerfile do projeto:

$ git clone https://github.com/rafhol/questao_02.git

5 - Criando image-stream:

docker build --no-cache -t 172.30.1.1:5000/myproject/nginx-nexxera .

docker tag 5260daef4b25 172.30.1.1:5000/myproject/nginx-nexxera

docker push 172.30.1.1:5000/myproject/nginx-nexxera

oc new-app 172.30.1.1:5000/myproject/nginx-nexxera

6 - Testando container:

$ curl localhost:8081
{
   "service":{
      "oracle":"ok",
      "redis":"ok",
      "mongo":"down",
      "pgsql":"down",
      "mysql":"ok"
   }
}$



