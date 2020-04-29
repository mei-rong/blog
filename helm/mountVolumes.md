#Mount volumes

##Mount volumes from path
```yaml
volumes:
    - name: empty-volume
    emptyDir: {}
```
##Mount volumes from secret
```yaml
volumes:
    - name: secret-volume
    secret:
        secretName: test-secretme
```
##Mount volumes from configmap 
```yaml
volumes:
    - name: cm-volume
    configMap:
        name: test-cm
        items:
        - key: a
            path: aa
```
### Attachment
```yaml
<!-- Source: test-dep.yaml -->
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
name: test-dep
labels:
  app: test-dep-app
annotations:
spec:
replicas: 1
selector:
  matchLabels:
    app: test-dep-app
template:
  metadata:
    labels:
      app: test-dep-app
    annotations:
    spec:
      containers:
      - name: test-dep
        image: test-dep:latest
        imagePullPolicy: IfNotPresent
        volumeMounts:
        - name: secret-volume
          mountPath: /etc/idm/jdbc/certificates
        - name: cm-volume
          mountPath: /etc/seeded
          readOnly: true
        - name: empty-volume
          mountPath: /var/run/secrets/boostport.com
      volumes:
      - name: secret-volume
        secret:
          secretName: test-secret
      - name: cm-volume
        configMap:
            name: test-cm
            items:
            - key: a
                path: aa
      - name: empty-volume
        emptyDir: {}
---
<!-- Source: test-secret.yaml -->
apiVersion: v1
kind: Secret
metadata:
  name: test-secret
data:
  <!-- base64 decoded -->
  a: ZGpzamZqY2pkamRzbGFrc25jd2VqZHNuZGtqamtqaiVeJSZeKCpeKiUmc2FqZGpzago=
  b: YXNkamtkamthczM0NzIwODE0N2hqc2RqCg==
---
<!-- Source: test-cm.yaml -->
apiVersion: v1
data:
  a: fdfdsalfj
  b: MTIzNDU2
kind: ConfigMap
metadata:
  name: test-cm
```

