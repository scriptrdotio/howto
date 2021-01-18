# Security

Security is of paramount importance in software systems and applications. Scriptr.io deals with security at two levels: (1) identity and (2) permissions (authorizations)

# Identity

The owner of a scriptr.io account signs into the workspace (web IDE) using his account user name and password, which should never be shared with anyone. Since it is possible to create more than one application for a same account, the account owner has a specific account owner token that will identify him against the scriptr.io API (more on this in the next sections).
Those tokens should never be shared as well, and never be used within applications.

## User and device directory

Each application of a scriptr.io account has its own user and device directory. Directories are not shared across applications, which means that a user/device who is identified in an application is unknown to another application of the same scriptr.io account.
