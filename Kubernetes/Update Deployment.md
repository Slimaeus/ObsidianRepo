# 1️⃣Commands
- kubectl set image deployment/NAME CURRENT_CONTAINER=NEW_IMAGE
- kubetcl rollout status deployment/NAME
# 2️⃣Steps
1. docker build -t NAME:TAG .
2. docker push USERNAME/NAME:TAG
3. kubectl set image deployment/NAME CURRENT_CONTAINER=NEW_IMAGE
4. kubetcl rollout status deployment/NAME