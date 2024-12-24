The Vulnerability Scanner trivy is installed on your main terminal. Use it to scan the following images for known CVEs:

nginx:1.16.1-alpine
k8s.gcr.io/kube-apiserver:v1.18.0
k8s.gcr.io/kube-controller-manager:v1.18.0
docker.io/weaveworks/weave-kube:2.7.0
Write all images that don't contain the vulnerabilities CVE-2020-10878 or CVE-2020-1967 into /opt/course/21/good-images.