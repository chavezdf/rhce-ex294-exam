As 2nd solumcion we can use templates:

1. Create a file called motd.j2:

``` 
    {% if inventory_hostname in groups['proxy'] %}
    Welcome to HAProxy server
    {% endif %}
    {% if inventory_hostname in groups['database'] %}
    Welcome to MySQL database
    {% endif %}
    {% if inventory_hostname in groups['webserver'] %}
    Welcome to Apache server
    {% endif %}
``` 

2. Create a playbook using template module:

``` yaml
  ---
  - name: Customize motd by Server Type
    hosts: all
    become: true
    gather_facts: false
    tasks:
    - name: Add motd using jinka Templates
      template:
        src: motd.j2
        dest: /etc/motd
        owner: root
        group: root
        mode: 644
``` 
3. To run it go to /home/automation/plays and call:
``` 
    ansible-playbook motd.yml
```     
