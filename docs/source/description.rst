Description
------------------------------------------------------------------------------

Ansible role to add users to system groups.

This role performs the following actions:

- Ensure the requirements are installed.

- Ensure the current user can obtain administrative (root) permissions.

- If the **users** variable is defined and the **groups** variable is
  defined, add all users to the specified groups.

- If the **configuration** variable is defined, add all users listed on it to
  the specified groups.
