
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
ansible-playbook ansible/main.yml -e@ansible/configs/base-rosa/default_vars.yml -e@base-rosa-var.yml -e@base-rosa-secret.yml
```

* 削除
