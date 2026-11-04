FROM clickhouse/clickhouse-server:26.3

# Bind IPv6 so langfuse-web and langfuse-worker can reach this service over
# Railway's private network.
COPY railway-listen.xml /etc/clickhouse-server/config.d/railway-listen.xml

EXPOSE 8123 9000
