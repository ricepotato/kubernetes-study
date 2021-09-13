# Kubernetes

## 노드 보기

```bash
  kubectl get nodes
  kubectl get nodes --kubeconfig admin.conf # admin config 파일 지정해서 보기
```

## 설치 구성 요소 보기

```bash
  kubectl get pods --all-namespaces
```

## pod 보기
```bash
  kubectl get pods
  kubectl get pods -o wide # 상세 보기
  kubectl get pods -o=custom-columns=NAME:.metadata.name,IP:.status.podIP,STATUS:.status.phase,NODE:.spec.nodeName # 필요한 내용만 출력하기
```

## pod 생성하기

```bash
  kubectl create -f ~/path/to/file.yml
  kubectl run nginx-pod --image=nginx
```


## pod 삭제
```bash
  kubectl delete pod nginx-pod
```

## deployment 생성하기
```bash
  kubectl create deployment dpy-nginx --image=nginx
```



## deployment 삭제
```bash
  kubectl delete deployment dpy-nginx
```

## scale

pod 의 수를 확장 / 축소

```bash
  kubectl scale deployment dpy-nginx --replicas=3
```

## 파일로부터 오브젝트 생성하기
```bash
  kubctl create -f ./echo-hname.yml
```

## 변경내용 적용하기

- record: 배포 정보 히스토리 저장

```bash
  kubectl apply -f ./echo-hanme.yml
  kubectl apply -f ./echo-hanme.yml --record
```


## pod 정보를 yaml 파일로 출력
```bash
  kubectl get pod echo-hname-7894b67f-qcq6z -o yaml > pod.yaml
```


## kubectl conrdon 

node 에 pod 가 스케쥴링 되지 않는 상태로 변경 설정 / 해제

- node 의 기존 pods 는 삭제되지 않음

```bash
  kubectl conrdon w3-k8s # w3-k8s node 에 scheduling 되지 않게 변경
  kubectl unconrdon w3-k8s # 해제
```

## kubectl drain

node 를 scheduling 되지 않는 상태로 변경하고 모든 pod 를 다른 node 로 이동시킴 (데몬셋 무시)

- 원상 복구하려면 `kubectl unconrdon` 명령어 사용

```bash
  kubectl drain w3-k8s --ignore-daemonsets
```

## kubectl set 

rollout-nginx deployment 의 이미지를 1.16.0 을 업데이트

```bash
  kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record
```

## kubectl rollout status deployment

deployment 의 rollout 상태 확인

```bash
  kubectl rollout status deployment rollout-nginx
```


## kubectl rollout histiry deployment

deployment 의 rollout history 확인

```bash
  kubectl rollout history deployment rollout-nginx
```

## kubectl describe deployment

deployment 상태 확인

```bash
  kubectl describe deployment rollout-nginx
```

## kubectl rollout undo deployment rollout-nginx

rollout undo

```bash
  kubectl rollout undo deployment rollout-nginx
  kubectl rollout undo deployment rollout-nginx --to-revision=1 # revision=1 상태로 undo
```

## kubectl get services
kubernetes service 보기

```bash
  kubectl get services
```

## kubectl expose deployment

deployment 를 외부에 노출하기(node port service 생성하기)

```bash
kubectl expose deployment np-pods --type=NodePort --name=np-svc-v2 --port=80
```



