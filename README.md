***MongoDB DB steps***

---

```

oc project mongodb-cluster

kubectl exec -it $(kubectl get po -o jsonpath='{.items[0].metadata.name}') -- mongo

rs.initiate()

var cfg = rs.conf();

cfg.members[0].host="mongo1.mongodb-cluster.svc.clusterset.local:27017";

rs.reconfig(cfg);

rs.add("mongo2.mongodb-cluster.svc.clusterset.local:27017");
rs.add("mongo3.mongodb-cluster.svc.clusterset.local:27017");

cfg = rs.conf()

cfg.members[0].priority = 2
cfg.members[1].priority = 2
cfg.members[2].priority = 1

cfg.members[0].votes = 1
cfg.members[1].votes = 1
cfg.members[2].votes = 1

rs.reconfig(cfg)

rs.status()

use pacman-dev
db.createUser(
  {
    user: "pacman",
    pwd:  "pacman",
    roles: [ { role: "readWrite", db: "pacman-dev" }]
  }
);

use pacman-qa
db.createUser(
  {
    user: "pacman",
    pwd:  "pacman",
    roles: [ { role: "readWrite", db: "pacman-qa" }]
  }
);

use pacman-prod
db.createUser(
  {
    user: "pacman",
    pwd:  "pacman",
    roles: [ { role: "readWrite", db: "pacman-prod" }]
  }
);

show dbs;

