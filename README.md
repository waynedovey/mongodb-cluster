rs.reconfig(cfg)cfg = rs.conf()# mongodb-cluster

***MongoDB DB steps***

---

```oc project pacman-app

kubectl exec -it $(kubectl get po -o jsonpath='{.items[0].metadata.name}') -- mongo

rs.initiate()

var cfg = rs.conf();

cfg.members[0].host="mongo1.pacman-app.svc.clusterset.local:27017";

rs.reconfig(cfg);

rs.add("mongo2.pacman-app.svc.clusterset.local:27017");

rs.add("mongo3.pacman-app.svc.clusterset.local:27017");

rs.add("mongo4.pacman-app.svc.clusterset.local:27017");

rs.add("mongo5.pacman-app.svc.clusterset.local:27017");

cfg = rs.conf()

cfg.members[0].priority = 2

cfg.members[1].priority = 2

cfg.members[2].priority = 1

cfg.members[3].priority = 1

cfg.members[4].priority = 1

cfg.members[0].votes = 1

cfg.members[1].votes = 1

cfg.members[2].votes = 1

cfg.members[3].votes = 1

cfg.members[4].votes = 1

rs.reconfig(cfg)

rs.status()```

---
