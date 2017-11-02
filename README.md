# hosts-toggler
Simple little tool to easily group hosts file entries and enabling/disabling the entries in each group.

## README
```
$ ./hosts-toggler -h
Enable or disable entries in your hosts file, by named group.
This script will prompt for a sudo password.
Usage: hosts-toggler [-hqnlps] -[e|d] <group_name>
  -h    This helpful text.
  -p    Print entries in group and quit.
  -e|d <name> Enable or disable group
  -s <name> Get current status for the group (enabled/disabled)
  -l    List all known groups
  -n    Non-interactive (sudo)
  -q    Quiet - only print errors

Examples:
  hosts-toggler
  hosts-toggler -q -d newspapers
  hosts-toggler -p -e newspapers
  hosts-toggler -qs newspapers
  hosts-toggler -p newspapers
```


## Example usage

### Quick Toggler
[Quick Toggler](https://extensions.gnome.org/extension/1077/quick-toggler/) is a GNOME extension which is quite handy with regards to conveniently enable or disable host groups.

Example configuration (in `~/.entries.json`):
```json
{
  "deftype": {
      "host_group": {
          "base": "toggler",
          "vars": ["name"],
          "command_on": "pkexec hosts-toggler -qe ${name}",
          "command_off": "pkexec hosts-toggler -qd ${name}",
          "detector": "hosts-toggler -qs ${name} | grep enabled"
      }
  },
  "entries": [
    {
      "type": "submenu",
      "title": "Host groups",
      "entries": [
        {
          "title": "Newspapers",
          "type": "host_group",
          "name": "newspapers"
        },
        {
          "title": "Social media",
          "type": "host_group",
          "name": "social_media"
        }
      ]
    }
  ]
}
``` 