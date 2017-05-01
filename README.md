# Caddy Ingress Controller

This is a Caddy ingress controller for Kubernetes.

Caddy is a simple http server written in Go. [Read more here.](https://github.com/mholt/caddy)

## Using the ingress controller

When creating an ingress, specify the annotation:

```
kubernetes.io/ingress.class: "caddy"
```

Example:

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: caddy-test
  annotations:
    kubernetes.io/ingress.class: "caddy"
spec:
  rules:
  - host: myhost.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: my-service
          servicePort: 9090
```

## Configuration

You can also add the following annotations for various settings.

| Name | type |
|------|------|
| [ingress.kubernetes.io/tls](#tls) | true or false |
| [ingress.kubernetes.io/jwt](#jwt) | true or false |
| [ingress.kubernetes.io/jwt-redirect](#jwt) | string |
| [ingress.kubernetes.io/jwt-allow](#jwt) | string |
| [ingress.kubernetes.io/jwt-deny](#jwt) | string |

# tls

Automatically generate a valid SSL certificate from Let's Encrypt.

*WARNING* If you're not using persistent storage, you will _probably_ run into the Let's Encrypt [rate limit](https://letsencrypt.org/docs/rate-limits/).

```
ingress.kubernetes.io/tls: true
```

# jwt

A JSON Web Token (JWT) is a secure authentication token that stores data.  Read more about jwt [here](https://jwt.io/).

*WARNING* When jwt is enabled, the private key must be deployed with the ingress controller via. setting the environment variable `JWT_SECRET` (HMAC) or `JWT_PUBLIC_KEY` (RSA).

Read more about the jwt plugin [here](https://github.com/BTBurke/caddy-jwt).

### ingress.kubernetes.io/jwt

To enable jwt, set

```
ingress.kubernetes.io/jwt: "true"
```

This will require all paths and hosts defined by the ingress to require a valid JWT.

## Disclaimer

This repository includes software with the following licenses:
* [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0.txt)