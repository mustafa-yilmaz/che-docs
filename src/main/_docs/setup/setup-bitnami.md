---
tags: [ "eclipse" , "che" ]
title: Getting Started&#58 Private Cloud
excerpt: "Using Che with your cloud hosting account."
layout: docs
permalink: /:categories/bitnami/
---
{% include base.html %}

Bitnami provides a [one-click install](https://bitnami.com/stack/eclipse-che) solution for deploying Eclipse Che to your own cloud account.

# 1. Install Che  
Bitnami will automatically install Che to your cloud account, just select your provider and then choose "Add Account" from the menu:

![ScreenShot2016-06-23at9.40.42AM.png]({{ base }}/docs/assets/imgs/ScreenShot2016-06-23at9.40.42AM.png)

Once your account is connected select the instance size. You should ensure that Che has at least 4GB RAM and 10GB of storage (the Che server itself will need ~2GB RAM). If you plan on running larger or more workspaces, increase your RAM and storage.

#### Azure Ports
Che runs Docker which uses the ephemeral port range when starting containers and exposing services. On Azure instances, the ephemeral port range has been limited to 50 - if all ports are in use when you try and start a container you'll receive an error. Try stopping a container or increasing the ephemeral port range for your Azure machine.


# 2. Usage  
When your private Che cloud server is ready you will see a page like the following:

![ScreenShot2016-11-30at12.40.15PM.png]({{ base }}/docs/assets/imgs/ScreenShot2016-11-30at12.40.15PM.png)

In the Credentials section you'll find your username and password. Show the password and copy it to the clipboard.  When you click on the IP address for the Che server on this page you will be brought to a welcome page from Bitnami. When you select the login link you will be asked for a username and password. Type the username and paste the password into the form.

You should now have access to the Che user dashboard.

These are some other common URLs on your instance:

```text  
<url>/                   # Loads dashboard or last opened workspace
<url>/dashboard          # Loads dashboard
<url>/ide/<wsname>       # Loads specific workspace
<url>/ide/<ws-not-exist> # Opens IDE with a prompt to create a new workspace
<url>/ide                # Loads the IDE, bypassing the dashboard\
```

## Running, Stopping and Restarting Che
If you have SSH access to the Che instance you can start and stop Che from the command line.

```shell  
# to start Che
sudo su eclipseche -- /opt/bitnami/apps/eclipseche/che/bin/che.sh -p:8080 -s:uid start

# to stop Che
sudo su eclipseche -- /opt/bitnami/apps/eclipseche/che/bin/che.sh -p:8080 -s:uid stop
```

Controlling the instance hosting Che is done through your cloud provider's management console.

## Preserving Project Files
All of your configuration files, workspaces, and projects are stored on the instance file system.  These files won't be lost when you stop the machine normally from your cloud provider's console.

If you destroy the instance hosting Che, your workspace and preferences will be lost. If you want to migrate or preserve those settings you can SSH into the instance and copy everything in `opt/bitnami/apps/eclipseche`.

## Changing the Password
Passwords are stored in a file at `/opt/bitnami/apps/eclipseche/conf/.htpasswd` and the default user is `user`. The user and password can be updated using Apache's `htpasswd` command.

To change the password:

1. Access the server using an [SSH connection](https://docs.bitnami.com/azure/faq/#how-to-connect-to-the-server-through-ssh)
2. Change the contents of `/opt/bitnami/apps/eclipseche/conf/.htpasswd` to include the password you want to use.
3. Run the following command substituting `new_user` for your preferred user name:

```text  
sudo /opt/bitnami/apache2/bin/htpasswd /opt/bitnami/apps/eclipseche/conf/.htpasswd new_user\
```

#### Advanced Configuration
There are many aspects of Eclipse Che like port and hostname that can be configured by setting [Eclipse Che properties]({{ base }}/docs/setup/configuration/index.html).  

# 3. Develop with Che  

# Develop with Che  
Now that Che is running there are a lot of fun things to try:

- Become familiar with Che through [one of our tutorials]({{ base }}/docs/tutorials/multi-machine/index.html).
- [Import a project]({{ base }}/docs/ide/import-a-project/index.html) and setup [git authentication]({{ base }}/docs/ide/git-svn/index.html).
- Use [commands]({{ base }}/docs/ide/commands/index.html) to build and run a project.
- Create a [preview URL]({{ base }}/docs/ide/previews/index.html) to share your app.
- Setup a [debugger]( {{ base }}/docs/ide/debug/index.html).
- Create reproducible workspaces with [chedir]({{ base }}/docs/chedir/getting-started/index.html).
- Create a [custom runtime stack]({{ base }}/docs/workspace/stacks/index.html).
