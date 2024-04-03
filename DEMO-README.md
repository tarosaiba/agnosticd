
# 初期セットアップ
* AWS Account 払い出し
* hosted zoneの設定

```diff
-sandbox_account_id: xxxxxxxxxxxx
+sandbox_account_id: 752270192105

-HostedZoneId: xxxxxxxxxxxxx
+HostedZoneId: Z1VSVV64202UX7

 subdomain_base_short: "{{ guid }}"
-subdomain_base_suffix: "sandbox2464.opentlc.com"
+subdomain_base_suffix: "sandbox666.opentlc.com"
 subdomain_base: "{{subdomain_base_short}}{{subdomain_base_suffix}}"
```

* rosa tokenの取得 (RH Consoleにて)
* secretの設定
```
$ cat base-rosa-secret.yml
rosa_token: "<TOKEN>"
aws_access_key_id: "<KEY_ID>"
aws_secret_access_key: "<KEY>"
```

# playbook実行

* 作成

```
ansible-playbook ansible/main.yml -e@ansible/configs/base-rosa/default_vars.yml -e@base-rosa-var.yml -e@base-rosa-var-custom.yml -e@base-rosa-secret.yml
```

* 削除

# Workload - OCP Plus
https://github.com/redhat-cop/agnosticd/tree/5db35ea2f7bcff0bfa778aeb3c4f828cbfffbb8c/ansible/roles_ocp_workloads/ocp4_workload_plus

```
TARGET_HOST="107.20.156.140"
ANSIBLE_USERNAME="ec2-user"
WORKLOAD="ocp4_workload_automation_demo"
GUID=saiba007
KEY_FILE="/tmp/output_dir/ssh_provision_saiba007"
ocp_username=cluster-admin
ocp_password="Uhzoo-s9xB5-x3esf-r7g2h"

ansible-playbook -i ${TARGET_HOST}, ./configs/ocp-workloads/ocp-workload.yml \
    -e"ansible_ssh_private_key_file=${KEY_FILE}" \
    -e"ansible_user=ec2-user" \
    -e"ocp_username=${OCP_USERNAME}" \
    -e"ocp_password=${ocp_password}" \
    -e"ocp_workload=${WORKLOAD}" \
    -e"silent=False" \
    -e"guid=${GUID}" \
    -e"ACTION=create"
```
