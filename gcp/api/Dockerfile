# Copyright 2021 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.11-slim@sha256:ad5dadd957a398226996bc4846e522c39f2a77340b531b28aaab85b2d361210b

# Generation 1 of cloud run overrides the HOME environment variable, causing
# poetry to run in the incorrect environment, as it defaults to using $HOME/.cache/virtualenvs/...
# 
# This forces it to create the virtualenv in the same directory as the project, avoiding this issue.
ENV POETRY_VIRTUALENVS_IN_PROJECT=true

# TODO(ochang): Just copy the entire project (needs a clean checkout).
COPY setup.py pyproject.toml poetry.lock README.md /osv/
COPY osv /osv/osv
COPY gcp/api /osv/gcp/api

WORKDIR /osv/gcp/api
RUN pip3 install poetry==1.8.3 && poetry install

ENTRYPOINT ["poetry", "run", "python", "/osv/gcp/api/server.py"]
