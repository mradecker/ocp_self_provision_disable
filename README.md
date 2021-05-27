# ocp_self_provision_disable.yml

A basic authenticated user in OpenShift is part of the system:authenticated:oauth group and can perform basic tasks inside the cluster including creating new projects/namespaces.

An organization's policy may restrict the ability of basic users to create new projects and resources which they are permitted to do in OpenShift by default.  By removing the cluster role "self-provisioner" from the "system:authenticated:oauth" group, users that log into the cluster will not be able to create new projects and will have to request that permission from the cluster admin.  

This playbook removes the self-provisioner cluster role from the group, ensures that upgrades to the cluster won't reset the permissions, and adds a project request message stating that the user does not have permission to create a project and to contact their system administrator.

Run the playbook with:

ansible-playbook self_provision_disable.yml

Make sure your host reflects your host or run as localhost.  Also, if you want to change your project request message, edit that before running the playbook.  You can also edit the project with:

oc edit project.config.openshift.io/cluster

spec:
  projectRequestMessage: To request a project, contact your system administrator
