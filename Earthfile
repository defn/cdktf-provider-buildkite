VERSION --shell-out-anywhere --use-chmod --use-host-command --earthly-version-arg --use-copy-link 0.6

IMPORT github.com/defn/cloud/lib:master AS lib

FROM lib+platform

warm:
    COPY cdktf.json pyproject.toml poetry.lock .
    RUN ~/bin/e poetry install

update:
    COPY cdktf.json pyproject.toml poetry.lock .
    RUN ~/bin/e poetry update
    SAVE ARTIFACT poetry.lock AS LOCAL poetry.lock

imports:
    FROM +warm
    RUN ~/bin/e cdktf get
    SAVE ARTIFACT .gen AS LOCAL imports
