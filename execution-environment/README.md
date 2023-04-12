# Build and Create Execution Environment

1. Install ansible-builder

```shell
python3 -m pip install ansible-builder
```

2. Build execution environment image

```shell
ansible-builder build --container-runtime=docker -t quay.io/morvencao/snow-ansible-ee:latest
docker push quay.io/morvencao/snow-ansible-ee:latest
```

Note: Make sure the image in quay.io is public access.

3. Create `Execution Environments` from AAP UI using the image sha from last step

4. Create `Project` from AAP UI with the `Execution Environments` created in last step and `Git` with current github repository

5. From `Templates `Create `Job Template` named `snow-create-change-request` with `run` type with `Project` created in last step and check `Promote on launch` box for `Variables`, put the following values to `Variables`:

```yaml
---
sn_username: admin
sn_password: xxxxxx
sn_instance: xxxxxx
```

6. Launch a Job with the following variables and make sure no error found:

```yaml
---
sn_username: admin
sn_password: xxxxxx
sn_instance: xxxxxx
sn_severity: 3
sn_priority: 3
app_name: pacman_test
target_clusters:
- mycluster
```
