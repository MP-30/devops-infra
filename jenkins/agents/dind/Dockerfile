FROM jenkins/inbound-agent:latest
USER root

# Install Docker daemon tools
RUN apt-get update && \
    apt-get install -y --no-install-recommends docker.io && \
    rm -rf /var/lib/apt/lists/*

# Create a robust, multi-line startup script
RUN printf '#!/bin/sh\n\
dockerd --data-root /var/lib/docker-dind &\n\
sleep 5\n\
exec /usr/local/bin/jenkins-agent "$@"\n' > /usr/local/bin/entrypoint.sh && \
chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
