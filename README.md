# Pilot Starting Balance for phpVMS 7

Pilot Starting Balance is a standalone, update-safe phpVMS 7 module for
administrators who want to credit newly verified pilots and make controlled
one-off credits to pilots whose current balance is zero.

The module does not modify phpVMS core files. It listens for the normal
Laravel email-verification event, records an idempotent application row, and
uses the phpVMS finance service to create an auditable journal credit.

## Features

- Admin-configured default balance for newly registered pilots.
- Credit is applied once, after the pilot confirms their email address.
- Blank or zero default values result in zero credit.
- Manual one-off credit for multiple selected pilots.
- The manual pilot list contains only pilots with a current zero balance.
- Each credit is written through the phpVMS finance journal.
- A memo can be recorded with manual credits.
- Repeated verification events cannot duplicate the registration credit.
- Administrator status page under **Admin -> Addons -> Pilot Starting Balance**.
- Cached GitHub release checker with a manual refresh button.
- Manual administrator-controlled updates; the module never self-updates.
- MIT licensed and free to use.

## Compatibility

- phpVMS 7 installations using the standard module manager.
- PHP 8.1.2 or newer.
- A phpVMS installation with the normal user verification and finance services.

The first release retains the setting and audit-table identifiers used by the
earlier AEV/Jumpseat implementation. This allows existing installations to
install the standalone module without losing the saved default or existing
registration-credit audit records.

## Installation through the phpVMS admin panel

1. Download `PilotStartingBalance.zip` from the GitHub release.
2. Keep the top-level folder inside the archive named `PilotStartingBalance`.
3. Sign in as a phpVMS administrator.
4. Open **Admin -> Modules -> Add New**.
5. Select and upload `PilotStartingBalance.zip`.
6. Activate the module if phpVMS places it under **Not Installed Modules**.
7. Run the module migration if the installer did not run it automatically.
8. Clear the Laravel/application caches.
9. Open **Admin -> Addons -> Pilot Starting Balance**.
10. Set the default balance and confirm the installed version and GitHub release status.

Expected installed path:

```text
modules/PilotStartingBalance/
```

## FTP or file-manager installation

1. Extract the archive.
2. Upload the `PilotStartingBalance` folder into the phpVMS `modules` directory.
3. Activate it from **Admin -> Modules**.
4. From the phpVMS installation root, run:

   ```bash
   php artisan module:enable PilotStartingBalance
   php artisan module:migrate PilotStartingBalance --force
   php artisan optimize:clear
   ```

## Updating phpVMS and the module

The module lives outside phpVMS core files, so normal phpVMS updates do not
replace its provider, event listener, controller, migration, or update page.
The setting and credit audit data are stored in the database and are not part
of the phpVMS core settings seed files.

The admin status page checks the canonical GitHub release every six hours, or
immediately when **Check GitHub now** is pressed. If a newer release is found,
it displays the release link. Updates are administrator-controlled: download
the new ZIP from GitHub and install it through the phpVMS module manager.
The module never replaces files automatically.

If a hosting deployment removes the module directory, upload and enable the
module again. Reinstalling does not reset the saved default or existing
credit audit rows.

## Links

- Repository: <https://github.com/parkho/PilotStartingBalance>
- Releases: <https://github.com/parkho/PilotStartingBalance/releases/latest>

## Notes

This is an independent community module and is not an official phpVMS
product. Back up the database and test in a staging VA before enabling credits
in production. Support requests and compatibility reports are welcome.

## License

Released under the MIT License. See [LICENSE](LICENSE).
