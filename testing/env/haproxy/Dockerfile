FROM test-env-base:centos7

RUN yum install --assumeyes epel-release
RUN rpm --import file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
RUN yum install --assumeyes openssl python-pip rsyslog
RUN pip --disable-pip-version-check install pyOpenSSL
RUN mkdir --parents /etc/haproxy/certs
RUN /etc/pki/tls/certs/make-dummy-cert /etc/haproxy/certs/dumb.pem

COPY haproxy/config/iptables /etc/sysconfig
