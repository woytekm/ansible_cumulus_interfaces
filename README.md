# ansible_cumulus_interfaces
cumlus_interfaces Ansible custom fact for Cumulus Linux

Ansible custom fact for ethernet switches running Cumulus Linux. This fact will generate an array of information related to interface configuration, which is not gathered by standard Ansible facts.

How to use in playbook:

<pre>
- name: "Create custom fact directory"
  file:
   path: "/etc/ansible/facts.d"
   state: "directory"

- name: "Insert custom fact file"
  copy:
    src: cumulus_interfaces.fact
    dest: /etc/ansible/facts.d/cumulus_interfaces.fact
    mode: 0755
    
- name: reload ansible_local
  setup: filter=ansible_local
  
- name: "Display interface info from switch"
  debug:
   msg: "{{ item }}"
  with_items: "{{ ansible_local.cumulus_interfaces }}"

</pre>
