# ust-k8s

**Crear certificados de cuarto nivel con cert-manager**

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
    name: mi-certificado-cuarto-nivel-wildcard
spec:
    secretName: mi-certificado-cuarto-nivel-tls
    issuerRef:
        name: letsencrypt-prod
        kind: ClusterIssuer
    dnsNames:
        - '*.infra.dominio.com'
        - '*.services.dominio.com'
```
