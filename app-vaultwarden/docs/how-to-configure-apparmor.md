# How to configure AppArmor for a Home Assistant app

## Documentation

https://gitlab.com/apparmor/apparmor/-/wikis/Documentation

## Monitor requested app resources

Using the "complain" flag for an AppArmor profile, you can monitor what resources a Home Assistant app is requesting during its execution.

Follow these steps:

1. Add the "complain" flag

   Have a look at the example below that shows where to add the "complain" for a configured profile:

   ```
   #include <tunables/global>
  
   profile <Home Assistant app slug> flags=(...) {
     # Start new profile for Vaultwarden service  
     /opt/vaultwarden cx -> vaultwarden_service,
    
     profile vaultwarden_service flags=(complain, ...)) {
       ...
     }
   }
   ```

2. SSH to Home Assistant OS

   ```
   ssh root@homeassistant.local -p 22222
   ```

   Have a look at [Debugging the Home Assistant Operating System](https://developers.home-assistant.io/docs/operating-system/debugging) to learn how to enable SSH to Home Assistant OS.

3. Check requested resources

   Inside Home Assistant OS, do the following to check for resources that were requested:

   ```
   cd /mnt/data/supervisor/apparmor/

   journalctl _TRANSPORT="audit" -g 'apparmor="ALLOWED"' --no-pager
   ```

4. Add requested resources

   Add the requested resources to the AppArmor profile and remove the "complain" flag once you have verified that the app is working correctly.

## Helpful links

- [vi cheat sheet](https://www.atmos.albany.edu/daes/atmclasses/atm350/vi_cheat_sheet.pdf)
