## traefik docker-compose.yml

### create username and password for auth

```bash
docker run --rm httpd:2.4-alpine htpasswd -nbB admin password | cut -d ":" -f 2
```

admin:$$2y$$05$Nf97SVPrrOpvu1MSSqyCu.ZnSkC.liqe5NRi/YBU7/anstf/94EN2

### self-signed wildcard certificate

```bash
openssl req -x509 -out coffee.example.com.crt -keyout coffee.example.com.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=example.com' -extensions EXT -config <( \
     printf "[dn]\nCN=example.com\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:*.example.com\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```
