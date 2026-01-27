# Phase 5 Final Audit（Read Only）

## Identity

whoami
id
groups

## Isolation

tree -L 3 environments/

## Immutable Lock

lsattr environments/prod/docker-compose.yml

## Service Health

sudo docker compose ps

## Automation Outputs

ls /var/log/inspections/
ls /data/backups/

## Sudoers Boundary

sudo -l
