# k3s-hardening (public, no Cloudflare)


Harden Ubuntu 24.04 nodes for an HA k3s cluster (API private-only, RBAC, Pod Security Standards, default-deny NetworkPolicy, UFW, SSH hardening, fail2ban, optional mDNS).


## Quick start
```bash
# macOS: brew install ansible | Ubuntu: apt -y install ansible
cp inventory.example.ini inventory.ini
cp group_vars/all.example.yaml group_vars/all.yaml
# Update inventory.ini & group_vars/all.yaml
ansible -m ping all
ansible-playbook -i inventory.ini site.yaml --check
ansible-playbook -i inventory.ini site.yaml -K

ansible-playbook -i inventory.ini site.yaml -l masters --tags "ssh,ufw,fail2ban,mdns" -K
ansible-playbook -i inventory.ini site.yaml -l workers --tags "ssh,ufw,fail2ban,mdns" -K
ansible-playbook -i inventory.ini site.yaml -l masters --tags k3s -K