---
layout: post
title: Utilizing App Role Tokens
tags: [blog]
---

Use http api to authenticate with hashi vault tokens.

```bash
sudo apt install -y curl jq

ROLE_ID="<some role id>"

SECRET_ID=$(curl \
    --silent \
    --show-error \
    --fail \
    --request POST \
    --header "X-Vault-Token: $SECRET_TOKEN" \
    $SECRET_ID_GENERATOR_URL | jq -r .data.secret_id)
# Add mask for github actions
# echo ::add-mask::$SECRET_ID

CLIENT_TOKEN=$(curl \
    --silent \
    --show-error \
    --fail \
    --request POST \
    --data "{\"role_id\": \"$ROLE_ID\", \"secret_id\": \"$SECRET_ID\"}" \
    https://$VAULT_URL/v1/auth/approle/login | jq -r .auth.client_token)

# echo ::add-mask::$CLIENT_TOKEN
# echo CLIENT_TOKEN="$CLIENT_TOKEN" >> $GITHUB_ENV
```
