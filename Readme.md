# Weiterbildung ansible

## Vitual machines instantiation

- clone project
- change to the repository

'''sh

  cd ansible 
'''
- VMs instantiation

'''sh
 vagrant up
'''
## generate ssh key
-create an repository
  - mkdir -p ssh-
- generate keys
   - ssh-keygen -f ssh-keys/id_ed25519
- copy the private key to vm-
  - create first the repository
  - vagrant ssh vm-admin -c "sudo mkdir -p /opt/tools/ssh-keys"
# install vagrant plugin for scp
   - vagrant plugin install vagrant-scp

## copy repository to vm-admin
  -  vagrant scp ssh-keys/ vm-admin:/home/vagrant/
  -  vagrant ssh vm-admin -c "sudo mv /home/vagrant/ssh-keys/ /opt/tools/ssh-keys/"
  -vagrant ssh vm-admin -c "sudo chmod 600 /opt/tools/ssh-keys"

##  copy public keys to vm-applications
 - cat ssh-keys/id_ed25519.pub | vagrant ssh vm-applications -c "sudo cat >> ~/.ssh/authorized_keys"

##  copy public keys to vm-databases
 - cat ssh-keys/id_ed25519.pub | vagrant ssh vm-databases -c "sudo cat >> ~/.ssh/authorized_keys"
