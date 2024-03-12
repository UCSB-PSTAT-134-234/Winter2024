# FROM ucsb/pstat234:v20240108
FROM ucsb/pstat234:v20240129

USER root

## ### Quarto
## # versions: https://quarto.org/docs/download/_download.json
## # neat setup: https://github.com/jeremiahpslewis/reproducibility-with-quarto
## # ENV QUARTO_VERSION 1.2.475
ENV QUARTO_VERSION 1.3.450
RUN curl --silent -L --fail \
        https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.deb > /tmp/quarto.deb && \
    apt-get update && \
    apt-get install -y --no-install-recommends /tmp/quarto.deb && \
    rm -rf /tmp/quarto.deb /var/lib/apt/lists/* /tmp/library-scripts

ENV GITHUB_CLI_VERSION 2.30.0
RUN wget https://github.com/cli/cli/releases/download/v${GITHUB_CLI_VERSION}/gh_${GITHUB_CLI_VERSION}_linux_amd64.tar.gz -O - | \
    tar xvzf - -C /usr/bin gh_${GITHUB_CLI_VERSION}_linux_amd64/bin/gh --strip-components=2

USER ${NB_USER}

### Prints Jupyter server token when terminal is opened
RUN echo "echo \"Jupyter server token: \$(jupyter server list 2>&1 | grep -oP '(?<=token=)[[:alnum:]]*')\"" > ${HOME}/.get-jupyter-url.sh && \
    echo "sh \${HOME}/.get-jupyter-url.sh" >> ${HOME}/.bashrc

RUN quarto install tool tinytex