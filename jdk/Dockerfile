FROM alpine:3.13.5
# 安装glibc
#ENV LANG=C.UTF-8
RUN apk update && apk add ca-certificates wget && \
wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-2.33-r0.apk&& \
apk add glibc-2.33-r0.apk && \
wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-bin-2.33-r0.apk && \
wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-i18n-2.33-r0.apk && \
apk add glibc-bin-2.33-r0.apk glibc-i18n-2.33-r0.apk && \
/usr/glibc-compat/bin/localedef -i zh_CN -f UTF-8 zh_CN.UTF-8 && \
rm -rf *.apk && \
rm -rf /var/cache/apk/* && \
# 设置时区
ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
echo Asia/Shanghai > /etc/timezone && \
# 安装jdk8
mkdir -p /usr/local/jdk8 && \
cd /usr/local/jdk8 && \
wget https://github.com/AdoptOpenJDK/openjdk8-upstream-binaries/releases/download/jdk8u292-b10/OpenJDK8U-jre_x64_linux_8u292b10.tar.gz && \
tar -xf OpenJDK8U-jre_x64_linux_8u292b10.tar.gz --strip-components 1 && \
rm -rf OpenJDK8U-jre_x64_linux_8u292b10.tar.gz && \
sed -i '/^jdk.tls.disabledAlgorithms/c\jdk.tls.disabledAlgorithms=SSLv3, RC4, DES, MD5withRSA, \\ ' /usr/local/jdk8/lib/security/java.security

#******************设置JAVA变量环境******************
ENV JAVA_HOME=/usr/local/jdk8
ENV LANG=zh_CN.UTF-8
ENV LANGUAGE=zh_CN:UTF-8
ENV LC_ALL=zh_CN.UTF-8
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=.:$JAVA_HOME/bin:$PATH
CMD ["java","-version"]

