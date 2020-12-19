Zundoko Ansible Operator
=========================

Zundoko Ansible Operator is a [Kubernetes operator](https://github.com/operator-framework/awesome-operators) built with [Operator SDK (Ansible plugin)](https://sdk.operatorframework.io/docs/building-operators/ansible/), that plays ZundokoKiyoshi.

Deploy to Kubernetes cluster
----------------------------

[kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) is needed in your PATH.

1. `git clone https://github.com/kaitoy/zundoko-ansible-operator.git`
2. `cd zundoko-ansible-operator`
3. `export IMG=kaitoy/zundoko-ansible-operator:0.0.1`
4. `make deploy`

Usage
-----

### Start a ZundokoKiyoshi

1. Write a Hikawa manifest.

    e.g.)

    ```yaml
    apiVersion: zundokokiyoshi.kaitoy.github.com/v1beta2
    kind: Hikawa
    metadata:
      name: hikawa
    spec:
      intervalMillis: 500
    ```

2. Apply the manifest to start a ZundokoKiyoshi.
    * Zundoko Operator starts to create Zundokos one by one with their Say fields set to "Zun" or "Doko" randomly.
    * When 4 "Zun"s are created and then "Doko" is done, Zundoko Operator creates Kiyoshi.
3. See Zundokos by: `kubectl get zundoko`

    ```console
    [root@k8s-master ~]# kubectl get zundoko
    NAME                        SAY    AGE
    hikawa-zundoko-0001   Doko   10m
    hikawa-zundoko-0002   Doko   10m
    hikawa-zundoko-0003   Doko   9m
    hikawa-zundoko-0004   Zun    9m
    hikawa-zundoko-0005   Doko   9m
    hikawa-zundoko-0006   Doko   8m
    ```

4. See Kiyoshi by: `kubectl get kiyoshi`

    ```console
    [root@k8s-master ~]# kubectl get kiyoshi
    NAME                    SAY        AGE
    hikawa-sample-kiyoshi   Kiyoshi !   7m
    ```

5. Delete the manifest to clean a ZundokoKiyoshi.


Build Operator
--------------

You can build the operator yourself rather than pull it from Docker Hub.

[docker](https://docs.docker.com/engine/reference/commandline/cli/) is needed in your PATH.

1. `git clone https://github.com/kaitoy/zundoko-ansible-operator.git`
2. `cd zundoko-ansible-operator`
3. `docker build . -t kaitoy/zundoko-ansible-operator:0.0.1`
