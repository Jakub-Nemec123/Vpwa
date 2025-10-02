FROM node:24-trixie
ARG USERNAME=node
ARG NPM_GLOBAL=/usr/local/share/npm-global

# node permissions setup
# @src https://github.com/devcontainers/images/blob/777b69b9e3d5ee39c0de1e752f7a7445447d0de7/src/javascript-node/.devcontainer/Dockerfile
RUN \
	# configure npm install location
    if ! cat /etc/group | grep -e "^npm:" > /dev/null 2>&1; then groupadd -r npm; fi \
    && usermod -a -G npm ${USERNAME} \
    && umask 0002 \
    && mkdir -p ${NPM_GLOBAL} \
    && touch /usr/local/etc/npmrc \
    && chown ${USERNAME}:npm ${NPM_GLOBAL} /usr/local/etc/npmrc \
    && chmod g+s ${NPM_GLOBAL} \
    && npm config -g set prefix ${NPM_GLOBAL} \
    && su ${USERNAME} -c "npm config -g set prefix ${NPM_GLOBAL}" \
	# install eslint, typescript, tslint->eslint
    && su ${USERNAME} -c "umask 0002 && npm install -g eslint typescript tslint-to-eslint-config" \
    && npm cache clean --force > /dev/null 2>&1