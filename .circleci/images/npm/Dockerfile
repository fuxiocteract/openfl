FROM openfl/openfl:develop

## install node/npm
ADD https://deb.nodesource.com/setup_8.x /opt/node8setup.sh
RUN chmod +x /opt/node8setup.sh && /opt/node8setup.sh
RUN apt-get install -y --no-install-recommends nodejs

# Install Chrome
RUN apt-get install -y --no-install-recommends wget
RUN wget --no-check-certificate -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get update
RUN apt-get install -y google-chrome-stable

# Disable sandboxing - it conflicts with unprivileged containers
RUN sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g' \
           "/opt/google/chrome/google-chrome"

## install hxgenjs
## re-install if repo changed and clear docker cache
ADD https://api.github.com/repos/jgranick/hxgenjs/compare/master...HEAD /dev/null
RUN haxelib git hxgenjs https://github.com/jgranick/hxgenjs

# more logs from npm
ENV NPM_CONFIG_LOGLEVEL info
