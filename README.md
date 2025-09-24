# Blue/Green Helm Chart

This chart deploys two versions of the app (`blue`, `green`) and switches traffic using a single Service controlled by `activeColor`.

---

## Build & Push Images

```bash
docker build -t aruns14/appbluegreen:blue-1.0.0 --build-arg COLOR=blue .
docker push aruns14/appbluegreen:blue-1.0.0

docker build -t aruns14/appbluegreen:green-1.0.0 --build-arg COLOR=green .
docker push aruns14/appbluegreen:green-1.0.0
