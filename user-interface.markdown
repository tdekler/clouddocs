---
layout: default
---
# User Interface

## Access the user interface

The UI (User Interface) is the web site that allows you to operate the HPC Cloud. Put it simply, it is your way to manage (create/destroy) your Virtual Machines (VM).

>**Note:**
>
>You can find the UI here: [https://ui.hpccloud.surfsara.nl](https://ui.hpccloud.surfsara.nl)


## Change your Password
> ⚠ **WARNING:**
>
>To protect your account, you are advised to change the password that we give you upon your first login.


This is how you change your password:

1. Look at the top-right corner of the screen on the UI. There is a _buddy_ icon that represents your user. Click on it.
2. Click on _Settings_, you will see the option to change or update your password. If you use a `user view` (see section below for OpenNebula views), click on the _edit_ icon on the right of the _view_ button.
3. On the new screen, type your new password twice and click the button to submit it.

## Logging out

Whenever you are ready to stop working for the day on the HPC Cloud, you are advised to log out of the UI.

> **NOTE**
>
> We kindly request you to free all resources whenever you are not using them. That way, other users may benefit from them in your absence. When you are about to log out, it is a good moment to reconsider what resources you need to release.

This is how you log out:

1. Look at the top-right corner of the screen on the UI. There is a _buddy_ icon that represents your user. Click on it.
2. Under the _buddy_, you will get an option to  _Sign Out_. Click there, and the welcome page will come up asking you to fill your username and password in again.

## Views
OpenNebula's `view`s are a way to present functionality on the screen. The simpler the `view`, the less functionality it offers, but the easier it is to understand and operate the HPC Cloud interface.

### What is a `view`

We have opted to assign `view`s to users depending on their role within projects. The HPC Cloud interface offers, therefore, different options to different types of users.

Each `view` shows different information, tabs and action buttons. Users can access one or multiple `view`s depending on their assigned role in their projects. In case of multiple `view`s, users can switch among them, as briefly explained further down in this document. The system remembers what `view` the user was using the last time she was logged in, and thus a new session will load the previous `view` the user was working at.

### User types
We have established 3 roles for users in projects:

1. basic user
2. advanced user
3. group administrator user

A group administrator sees the most functionality (including administering other users), the basic user the least, and the advanced user can operate a bit more than the basic user.

#### Basic user
* Available view: **cloud**
* Description: simplified view for accessing pre-defined objects (images, templates, VMs). These pre-defined objects are created by the other roles (advanced user and group administrator user).
* Possible Functions:
  * Manage VMs
  * Display own quota
  * Display own accounting

![cloud_view_img](images/cloud_view_52.png)

#### Advanced user   
* Available views: **cloud** (and **user**)
* Description: more functional view for creating and managing objects (images, templates, VMs)
* Possible Functions:
  * Create/Modify/Delete Images
  * Create/Modify/Delete Templates
  * Manage ACLs (Access Control Lists)
  * All functions available to **basic user**

![user_view_img](images/user_view_52.png)

#### Group Administrator user
* Standard View: **groupadmin** (and **cloud** and **user**)
* Description: full control the project quota and members
* Possible Functions:
  * Create/Modify/Delete users in the project
  * Define quotas for each user
  * Display accounting for each user
  * Display accounting for the whole project
  * All functions available to **advanced user**

![groupadmin_view_img](images/groupadmin_view_52.png)

### Switch views
Users with the **group administrator** and **advanced** roles have access to multiple views, and can switch between these anytime.

In the user interface, select the _buddy_ icon that represents your user at the top right (next to the Home icon). Then select the _Change view_ button, unfold the tab and switch the option to the wanted view. 

![switch_cloud_to_user_img](images/switch_view_52.png)


## Menu

There is a menu on the left side within the **user** `view`. The tabs displayed there are:

* Dashboard
* Instances
* Templates
* Storage
* Network
* Settings

A description of each of these items follows. 

> **NOTE**
>
> The menu displays different functionalities accordingly to the `view` mode. 

### Dashboard
The Dashboard is the page where you can see a summary of the status of your project. Information includes:

* daily graphs of CPU and memory usage
* list of VMs
* network and storage counters
* quotas

### Instances
The _Instances_ menu allows you to manage your created `VM`s. It offers 2 sub-options:

* _VMs_: to manage `VM`s (i.e.: create, start, stop, suspend, delete...)
* _Services_:  *new functionality; documentation to be updated*

### Templates

The _Templates_ menu allows you to manage your `Templates`s. It offers 2 sub-options:

* _VMs_: to manage `Template`s (i.e.: create, edit, delete)
* _Services_: *new functionality; documentation to be updated*

### Storage

The _Storage_ menu allows the user to see information about all storage related resources. It offers 4 sub-options:

* _Datastores_: to see where you can take storage from and how much you are using of each 
* _Images_: to manage `Image`s
* _Files & Kernels_: to manage _kernel_, _ramdisk_ and _context_ files that can be used from `Templates` and on `VM`s
* _Apps_: Access to the _Appliances_ 

_Appliances_ are ready-made `image`s (and, sometimes, `template`s as well), that you can import into your project so that you can instantiate `VM`s out of them. There are pre-made _appliances_ for CentOS and Ubuntu, for example. When you click on one of them, make sure you read the corresponding comments.


### Network

The _Network_ menu allows you mainly to see information about the network resources available in the HPC Cloud and your usage of them. It offers 3 sub-options:

* _Virtual Networks_: to see which networks you have available and which your `VM`s are using them
* _Network Topology_: *new functionality; documentation to be updated*

<!---
Not available in the user view!!!!
* _Security Groups_: *new functionality TODO*
-->

>**Note:**
>
>We expect to offer the possibility for users to contribute their own _appliances_ to the AppMarket in the future.
