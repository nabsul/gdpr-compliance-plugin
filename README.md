# GDPR Compliance for WordPress

The goal of this plugin is to offer an easy way to make your site and all the plugins you might own GDPR complaint.

The main things this GDPR Compliance tool addresses are:

- Checking if a user has opted in to data collection
- Full discloser of data collected to the user
- Giving the user the ability to download their personal data
- Giving the user the ability to delete their personal data

This plugin does not actually perform any of the tasks above. It acts as a framework for other plugins to attach to.

## What this Plugin does

The plugin provides the following features:

- Creates a page that shows the GDPR notice for WordPress and all installed plugins
- Tracks which users have concented to having their data collected and which have not
- Automatically tracks changes GDPR notice and asks user for re-consent as needed
- Provides a place where a user can download their date
- Allows users to fully delete their personal data

## Full Disclosure

Full disclosure is the main notice that describes all of the data the site is collecting. 
The plugin presents this as a post and auto-fills the content via hooks from other plugins. 

If the disclosure agreement changes, then you will need your users to consent once again. 
This pluging achieves this by monitoring the disclosure agreement 
and incrementing a version number every time it changes. 
It will then make sure that all users have opted in as needed.

## Opting In and Out

This plugin tracks the user's opt-in and opt-out status via a `usermeta` entry called `gdpr_compliance`.
This entry is JSON data that tracks the following:

- Time, date and version of user opting-in to data collection
- Date and time of requests to download their personal data
- Date and time of opting out to personal data collection

Additionally, the plugin offers several static functions to check a user's current opt-in status:

```PHP
GDPR_Compliance::get_current_consent_version()
GDPR_Compliance::get_user_consent_version( $user_id = null )
GDPR_Compliance::is_user_opted_in( $user_id = null )
```

## Hooks for Plugin Compliance

The following hooks are used to add data to different hooks

`gdpr_compliance_notice`: Add your plugin's documentation to this hook so that it appears on the notice page.
`gdpr_compliance_remove_user`: Add a method to this hook to delete a user's plugin-specific custom data.
`gdpr_compliance_user_data_download`: Add data the JSON-encoded data that the user can download.
