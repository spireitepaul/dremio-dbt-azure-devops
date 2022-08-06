FROM centos/python-38-centos7
ARG DEV_HOST
ENV DREMIO_HOST=${DEV_HOST}
ARG DEV_USER
ENV DREMIO_USER=${DEV_USER}
ARG DEV_PWD
ENV DREMIO_PWD=${DEV_PWD}
ARG BRANCH
ENV SOURCEBRANCH=${BRANCH}

USER root
#RUN yum -y update

RUN yum -y install unixODBC-devel
#RUN yum -y update
ADD ./build/dremio-odbc-1.5.4.1002-1.x86_64.rpm /tmp
RUN yum -y localinstall /tmp/dremio-odbc-1.5.4.1002-1.x86_64.rpm
RUN pip install dbt-dremio
COPY . /usr/app
COPY ./build/odbc.ini /etc
COPY ./build/odbcinst.ini /etc
ENV dbt_PROFILES_DIR=/usr/app/build/
WORKDIR "/usr/app/"
# vary ssh according to server - can i use an if in this
# better to not have this logic in here.   We should pass in the ubunto@xxx   from the calling pipeline
# also need to pass in the nranch (dev, uat, prod) ratherthan hardcoded.
# RUN --mount=type=ssh ssh -4 -fN -o StrictHostKeyChecking=no -L 31010:127.0.0.1:31010 ubuntu@backend.ukdev.dremio.dyedurham.dev -p 60022 -v -v -v
RUN dbt deps
RUN dbt compile --profiles-dir /usr/app/build --target deploy
# RUN dbt seed --profiles-dir /usr/app/build --target $(Build.SourceBranchName)
RUN dbt run --profiles-dir /usr/app/build  --target deploy
# RUN dbt test --profiles-dir /usr/app/build --target deploy
