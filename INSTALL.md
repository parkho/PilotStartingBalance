# Pilot Starting Balance - Admin Installation

## Requirements

- phpVMS 7 with the standard module manager;
- PHP 8.1.2 or newer;
- administrator access to the phpVMS installation;
- the normal phpVMS user verification and finance services.

## Install from the admin panel

1. Upload `PilotStartingBalance.zip` at **Admin -> Modules -> Add New**.
2. If phpVMS shows the module under **Not Installed Modules**, select
   **Activate Module**.
3. The installer normally runs the module migration automatically.
4. If necessary, run this from the phpVMS root:

   ```bash
   php artisan module:migrate PilotStartingBalance --force
   ```

5. Clear caches:

   ```bash
   php artisan optimize:clear
   ```

6. Open **Admin -> Addons -> Pilot Starting Balance**.
7. Set the default amount. Blank or zero means no automatic credit.
8. Use the manual credit section to select one or more zero-balance pilots.

## Verify the installation

Confirm that the module appears under **Admin -> Addons** and that the status
page shows the installed version and GitHub release status. A newly registered
pilot receives the configured amount once, after confirming their email.

## Updating or removing

Install newer releases through the phpVMS module manager. The module's update
checker only reports releases; it never downloads or installs files itself.

Normal phpVMS core updates do not overwrite this module. If the module folder
is replaced, upload and enable it again. The migration is safe to run again.
Uninstalling does not remove the setting or audit table, preserving the
administrator's configuration and transaction history for a later reinstall.
