FROM edxops/precise-common:latest
MAINTAINER edxops

USER docker
WORKDIR /edx/app/edx_ansible/edx_ansible
RUN sudo git fetch --all
RUN sudo git checkout e0d/docker-latest
RUN sudo git reset --hard origin/e0d/docker-latest
RUN sudo git pull
WORKDIR /edx/app/edx_ansible/edx_ansible/docker/plays
RUN sudo ansible-playbook nginx.yml -c local \
   -i '127.0.0.1,' \
   -e@roles/edxapp/defaults/main.yml \
   -e@roles/xqueue/defaults/main.yml \
   -e@roles/ora/defaults/main.yml \
   -e@roles/certs/defaults/main.yml

USER root
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
WORKDIR /etc/nginx
CMD ["/usr/sbin/nginx"]
EXPOSE 18000 48000 18010 48010 18020
