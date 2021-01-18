# Security

Security is of paramount importance in software systems and applications. Scriptr.io deals with security at three levels: 
- Authentication
- Authorizations
- Encryption

# Authentication

## Account owner

The owner of a scriptr.io account signs into the workspace (web IDE) using his account user name and password, which should never be shared with anyone. Since it is possible to create more than one application for a same account, the account owner has a specific **account owner authentication token** that will identify him against the application (more on this in the next sections). Those tokens should never be shared as well, and never be used within applications.

## User and device directory
Each application of a scriptr.io account has its own user and device directory. Directories are not shared across applications, which means that a device or a user who is identified in an application is unknown to other applications of the same scriptr.io account.

### Credentials
Adding a new a user or a device into the directory can be done from the workspace or using the corresponding APIs. It requires providing a user name (respectively a device name) and a password that will be used to generate an **authentication token**. If a token is lost or corrupted, a new token can be regenerated, which automatically invalidates the other one. It is also possible to modify the password, which leads to the automatic regeneration of an authentication token, and the invalidation of the former password and token respectively.

Users and devices access a scriptr.io application by issuing authenticated http requests to it's API. A request is authenticated by scriptr.io if it contains a valid authentication token pertaining to the directory of the targeted application. 

User interfaces served by a scriptr.io application can also leverage the [Login component](https://github.com/scriptrdotio/login), which allow the user to sign-in by entering their username and password in a login form. The login component will generate a session token, automatically redirecting users to the login form upon session expiration.
