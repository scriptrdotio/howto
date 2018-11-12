# How to give remote clients anonymous access to my API?

It is very simple to grant unrestricted access to your API (scripts) to remote resources, i.e. without requiring the latter to provide an authentication token.
In order to do that, you need to just need to switch the ACL of the script to **Anonymous**

Click on the small red lock that appears on the right of the script editor in your [workspace](https://www.scriptr.io/workspace)

![Secure script](./images/acl_lock.png)

**Image 1**

Clicking on the lock opens an **Access Control List (ACL)** editor. As you can see, access to the script is granted by default only to the owners **authenticated** role, i.e. any user or device created from your account.

![Default ACL](./images/acl_view.png)

*Image 2*

Modify this ACL by searching for the **Anonymous** built-in role, then by clicking "Add". Acknowledge scriptr's message regarding switching to this role (cick "yes") and click on "Save Changes" to validate your choice.  

![Change ACL](./images/anonymous.png)


