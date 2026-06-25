# CKA 기본 명령어 모음

---

## 공통 명령어 (모든 객체에서 사용)

```bash
kubectl get all                                          # kubernetes의 현재 전체 객체 보기
kubectl get pods                                         # 생성되어 있는 Pod 보기
kubectl describe pod <pod이름>                           # 생성된 Pod 상세보기
kubectl delete pod <pod이름>                             # Pod 객체 삭제하기
kubectl create -f redis.yaml                             # yaml 파일로 객체 생성하기
kubectl apply -f redis.yaml                              # yaml 파일로 객체 생성/변경하기
```

---

## Pod

```bash
kubectl get pods -o wide                                 # 파드 정보 상세보기, 어떤 노드에 생성되었는지 확인 가능
kubectl run nginx --image=nginx                          # 파드 명령어로 간단하게 생성하기
kubectl run nginx --image=nginx --dry-run=client -o yaml > redis.yaml
                                                         # 실제 생성 안하고 yaml로만 만들기
```

---

## Deployment

```bash
kubectl create deployment nginx --image=nginx            # deployment 명령어로 생성하기
kubectl set image deployment nginx nginx=nginx:1.18      # 이미지 변경하기
kubectl scale deployment nginx --replicas=4              # 복제본 개수 수정하기

# 변경 이력 및 롤백
kubectl rollout history deployment my-deployment                  # 변경 이력 보기
kubectl rollout history deployment my-deployment --revision=3     # 특정 버전 이력 보기
kubectl rollout undo deployment my-deployment --to-revision=3     # 특정 버전으로 롤백
```

---

## Service

```bash
kubectl expose pod redis --port=6379 --name=redis-service
                                                         # 기존 pod, deploy에 대응하는 service 만들 때
```