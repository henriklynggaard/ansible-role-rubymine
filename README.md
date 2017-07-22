RubyMine (https://www.jetbrains.com/ruby)
=========

This role installs RubyMine and configured plugins. It has been tested on Linux Mint 18 but should wokr on most 
distributions. By default it installs RubyMine 2017.2 and no additional plugins

By default RubyMine is installed under the user's home directory and _become_ is not needed.

Requirements
------------

None


Role Variables
--------------

    rubymine_version: 2017.2
    rubymine_download_mirror: https://download.jetbrains.com/ruby/
    rubymine_plugin_download_mirror: "https://plugins.jetbrains.com/plugin/download?updateId="
    rubymine_plugins: []
    rubymine_download_directory: /tmp
    rubymine_install_directory: "{{ ansible_env['HOME'] }}/Tools"

    # calculated
    rubymine_install_file: "RubyMine-{{ rubymine_version }}.tar.gz"
    rubymine_download_url: "{{ rubymine_download_mirror }}{{ rubymine_install_file }}"
    rubymine_location: "{{ rubymine_install_directory }}/RubyMine-{{ rubymine_version }}"
    rubymine_desktop_file_location: "{{ ansible_env['HOME'] }}/.local/share/applications/rubymine-{{ rubymine_version }}.desktop"


rubymine_plugins is a list of names which get appended to rubymine_plugin_download_mirror to form a full download  


Dependencies
------------

None

Example 
-------

__Example playbook__


    - hosts: localhost
      connection: local
    
    roles:
      - henriklyngaard.rubymine
      
__Exmaple inventory for plugins__

The below IDs have been found by going to https://plugins.jetbrains.com/ruby and searching for the plugin. 
Once found copy the link location for the desired version and use the _updateId=XXXXX_ part at the end        
      
    rubymine_plugins:
      # ignore 1.7.6
      - 32828
      # bash support 1.6.5.171
      - 31610
      # ansible 0.9.4
      - 27616
      # docker 2.5.3
      - 33621
      # markdown 2017.1.20170302
      - 33092      
      
 Alternatively upload the required plugins to a webserver and adjust _rubymine_plugin_download_mirror_ and 
 _rubymine_plugins_ accordingly
      
      
License
-------

MIT

Change log
----------

* 1.0: Initial version
