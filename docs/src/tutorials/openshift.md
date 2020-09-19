# OpenShift
---

* Database configuration (mysql)

```bash
oc get pods
oc port-forward [pod name] :3306
```

OR

```bash
oc rsh [pod name]
mysql -u [user] -p[password] [database]
```

* Environment Variables

```text
MYSQL_DATABASE
MYSQL_PASSWORD
MYSQL_USER
```
