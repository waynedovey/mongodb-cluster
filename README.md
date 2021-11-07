# mongodb-cluster

** MongoDB DB steps **

---

kubectl exec -it $(kubectl get po -o jsonpath='{.items[0].metadata.name}') -- mongo

rs.initiate()

var cfg = rs.conf();
cfg.members[0].host="mongo1.pacman-app.svc.clusterset.local:27017";
rs.reconfig(cfg);

rs.add("mongo2.pacman-app.svc.clusterset.local:27017");
rs.add("mongo3.pacman-app.svc.clusterset.local:27017");
rs.add("mongo4.pacman-app.svc.clusterset.local:27017");

rs.status()

---
