### [Linux users, processes and permissions](http://haifux.org/lectures/84-sil/users-processes-files-and-permissions/users-perms-lec.html)
1. File's permissions are specified for user, group and public.
2. Objects in the system (Processes, Files) are attached to Users. Process can access whatever the user can access. Process assumes user-owner permissions if setuid flag is set for the process executable file.
    1. Process contains PID, UID.
3. Multiple user processes can execute at the same time.
4. Groups allow for sharing of files/folders across users.
5. User can access a file only if the user has execute permissions on all the directories upto the file parent directory.
6. Passwords are stored in /etc/shadow file to not let other users see passwords. Encrypted password is stored.
7. Users list is present at /etc/passwd. All users can access this file.
8. All the groups are present at /etc/group.
9. User can belong to multiple groups.
10. User can assume the role of another user using [sudo](https://www.linode.com/docs/guides/linux-users-and-groups/).
    1. While sudo is used to give another user limited access to another user’s account for the purpose of performing tasks (in most cases the root user or the superuser), sudo may be best explained as a tool that allows users and groups to have access to commands they normally would not be able to use. sudo enables a user to have administration privileges without logging in directly as root.
