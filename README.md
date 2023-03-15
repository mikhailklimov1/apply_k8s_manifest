Role Name
=========


Requirements
------------

A collection kubernetes.core should be installed. To accomplish this run the following command:

ansible-galaxy collection install kubernetes.core

See https://docs.ansible.com/ansible/latest/collections/kubernetes/core/docsite/kubernetes_scenarios/k8s_intro.html for more information

Role Variables
--------------

This role reads and stores data from ansible folder. Each cluster should have it's own folder within ansible folder with a required data. 'backup-cluster-name' should have backup manifests. And 'new-cluster-name' should store authentication data. Example:

cluster_name/
├── auth
│   ├── kubeadmin-password
│   └── kubeconfig
└── manifests_folder
        ├── manifest1.yaml
        ├── manifest2.yaml
        └── manifest3.yaml

cluster_name: A cluster hostname (eq new cluster folder name)
domain_name: A domain name of the new cluster
manifests_folder: A directory name where manifests to apply are stored
manifests: Names of the .yaml files in ./backup-cluster-name/backup folder

Dependencies
------------

-

Example Playbook
----------------

# A play with a loop:

- hosts: localhost
  vars:
    cluster_name: cluster_name
    domain_name: example.com
    manifests_folder: manifests_folder
    manifests:
    - manifest1.yaml
    - manifest2.yaml
    - manifest3.yaml

  tasks:
  - name: Apply manifest {{ item }}
    vars:
      manifest_name: "{{ item }}"
    include_role:
      name: apply_k8s_manifest
    loop: "{{ manifests }}"

License
-------

BSD

Author Information
------------------

Mikhail Klimov
