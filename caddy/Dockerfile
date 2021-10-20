FROM caddy:2.3.0-builder-alpine AS builder

RUN xcaddy build \
    --with github.com/caddy-dns/cloudflare

FROM caddy:2.3.0-alpine

RUN apk add --no-cache ca-certificates curl bind-tools jq

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
COPY Caddyfile /etc/caddy/Caddyfile
COPY data /data/caddy
COPY configure_cloudflare.sh /configure_cloudflare.sh
RUN chmod +x /configure_cloudflare.sh

ENTRYPOINT [ "/configure_cloudflare.sh" ]
CMD [ "caddy", "run", "--config", "/etc/caddy/Caddyfile" ]