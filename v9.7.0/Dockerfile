FROM alpine

# Install necessary packages
RUN apk --no-cache add wget libcap

# Install websocket tunneling
RUN wget https://github.com/erebe/wstunnel/releases/download/v9.7.0/wstunnel_9.7.0_linux_amd64.tar.gz \
    && mkdir src \
    && tar -xzf wstunnel_9.7.0_linux_amd64.tar.gz -C src \
    && mv src/wstunnel /usr/local/bin/wstunnel \
    && rm -rf src \
    && chmod uo+x /usr/local/bin/wstunnel \
    && setcap CAP_NET_BIND_SERVICE=+eip /usr/local/bin/wstunnel

# Create entrypoint script
RUN echo "#!/bin/sh" > /usr/local/bin/start_wstunnel.sh \
    && echo "exec \$COMMAND" >> /usr/local/bin/start_wstunnel.sh \
    && chmod +x /usr/local/bin/start_wstunnel.sh

# Set the entrypoint script as the default command
ENTRYPOINT ["/usr/local/bin/start_wstunnel.sh"]