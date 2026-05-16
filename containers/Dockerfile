FROM n8nio/n8n:latest

# Switch to root to install packages
USER root

# Install sqlite3 (Alpine Linux)
RUN apk add --no-cache sqlite

# Switch back to node user
USER node

# Default port
EXPOSE 5678

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=40s --retries=3 \
    CMD node -e "require('http').get('http://localhost:5678/healthz', (r) => {if (r.statusCode !== 200) throw new Error(r.statusCode)})"
