= imagebuilder on RHEL 8

Ansible playbooks to deploy imagebuilder VM on KVM/Libvirt

== Setup a secret for secured variables
```bash
vi .vault_secret
```

== Update secured variables in roles/<role-name>/default/main.yaml
```bash
ansible-vault encrypt_string --vault-password-file .vault_secret --encrypt-vault-id default --name 'password' 'somepassword'
```

= Build VM and setup imagebuilder
```bash
ansible-playbook build.yaml --vault-password-file .vault_secret 
ansible-playbook setup.yaml --vault-password-file .vault_secret 
```

= Destroy
```bash
ansible-playbook teardown.yaml
```

```bash
sudo systemctl restart libvirtd
```

Note2: You can use tags: server
