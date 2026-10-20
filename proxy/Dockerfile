FROM nginxinc/nginx-unprivileged:1-alpine
LABEL maintainer="amel.sellami@value.com.tn"

# 1. Set environment variables early
ENV LISTEN_PORT=8000
ENV APP_HOST=app 
ENV APP_PORT=9000

# 2. Switch to root to create directories and permissions
USER root

RUN mkdir -p /vol/static && \
    chmod 755 /vol/static && \
    touch /etc/nginx/conf.d/default.conf && \
    chown nginx:nginx /etc/nginx/conf.d/default.conf

# 3. Copy configuration and script files
COPY ./default.conf.tpl /etc/nginx/default.conf.tpl
COPY ./uwsgi_params /etc/nginx/uwsgi_params
COPY ./run.sh /run.sh

# 4. Make sure the run script is executable
RUN chmod +x /run.sh

# 5. Define volumes and drop back to non-root user
VOLUME /vol/static
USER nginx

# 6. Command to run on container startup
CMD ["/run.sh"]