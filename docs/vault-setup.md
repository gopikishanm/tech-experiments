root@vault:~# export VAULT_DATA=/opt/vault/data
root@vault:~# export VAULT_CONFIG=/etc/vault.d

mkdir -p ${VAULT_DATA} && mkdir -p {VAULT_CONFIG}

Install vault
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vault

setcap cap_ipc_lock=+ep $(readlink -f $(which vault))

root@vault:~# useradd --system --home ${VAULT_DATA} --shell /sbin/nologin vault
useradd: user 'vault' already exists
root@vault:~# useradd --system --home ${VAULT_DATA} --shell /sbin/nologin vault
useradd: user 'vault' already exists
root@vault:~# chown vault:vault ${VAULT_DATA}
root@vault:~# chmod -R 750 ${VAULT_DATA}

After modifying vault.hcl, change permissions on the file

chown vault:vault "${VAULT_CONFIG}/vault.hcl" && \
  sudo chmod 640 "${VAULT_CONFIG}/vault.hcl"

vault server -dev



Refernces
https://developer.hashicorp.com/vault/downloads#linux
https://developer.hashicorp.com/vault/tutorials/get-started/setup
https://developer.hashicorp.com/vault/docs/install/install-binary
https://asokolsky.github.io/proxmox/lxc-vault.html