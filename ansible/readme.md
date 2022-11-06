```sh
vagrant up --provision


ansible-playbook ./playbooks/install.yaml

ansible-playbook \
  --ssh-common-args "ForwardAgent=yes" \
  ./playbooks/install.yaml

ansible-playbook \
  -i <production-domain-name> \
  --private-key ~/.ssh/id_scn \
  ./playbooks/setup.yaml
```