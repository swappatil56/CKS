# Use Trivy to check some public images

and our kube api serever image

controlplane $ k get pod kube-apiserver-controlplane -n kube-system -o yaml | grep image
    image: registry.k8s.io/kube-apiserver:v1.31.0
    imagePullPolicy: IfNotPresent
    image: registry.k8s.io/kube-apiserver:v1.31.0
    imageID: registry.k8s.io/kube-apiserver@sha256:470179274deb9dc3a81df55cfc24823ce153147d4ebf2ed649a4f271f51eaddf
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker run ghcr.io/aquasecurity/trivy:latest image registry.k8s.io/kube-apiserver:v1.31.0
2024-12-16T10:08:40Z    INFO    [vulndb] Need to update DB
2024-12-16T10:08:40Z    INFO    [vulndb] Downloading vulnerability DB...
2024-12-16T10:08:40Z    INFO    [vulndb] Downloading artifact...        repo="mirror.gcr.io/aquasec/trivy-db:2"
223.25 KiB / 57.58 MiB [>____________________________________________________________] 0.38% ? p/s ?2.06 MiB / 57.58 MiB [-->____________________________________________________________] 3.58% ? p/s ?7.48 MiB / 57.58 MiB [-------->_____________________________________________________] 13.00% ? p/s ?15.40 MiB / 57.58 MiB [------------>___________________________________] 26.74% 25.28 MiB p/s ETA 1s21.33 MiB / 57.58 MiB [----------------->______________________________] 37.05% 25.28 MiB p/s ETA 1s30.54 MiB / 57.58 MiB [------------------------->______________________] 53.03% 25.28 MiB p/s ETA 1s39.10 MiB / 57.58 MiB [-------------------------------->_______________] 67.90% 26.20 MiB p/s ETA 0s43.57 MiB / 57.58 MiB [------------------------------------>___________] 75.66% 26.20 MiB p/s ETA 0s49.36 MiB / 57.58 MiB [----------------------------------------->______] 85.72% 26.20 MiB p/s ETA 0s53.93 MiB / 57.58 MiB [-------------------------------------------->___] 93.65% 26.10 MiB p/s ETA 0s56.86 MiB / 57.58 MiB [----------------------------------------------->] 98.75% 26.10 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 26.10 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 24.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 24.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 24.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 23.21 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 23.21 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 23.21 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 21.71 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 21.71 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 21.71 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 20.31 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 20.31 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [-------------------------------------------------] 100.00% 12.94 MiB p/s 4.6s2024-12-16T10:08:46Z        INFO       [vulndb] Artifact successfully downloaded       repo="mirror.gcr.io/aquasec/trivy-db:2"
2024-12-16T10:08:46Z    INFO    [vuln] Vulnerability scanning is enabled
2024-12-16T10:08:46Z    INFO    [secret] Secret scanning is enabled
2024-12-16T10:08:46Z    INFO    [secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2024-12-16T10:08:46Z    INFO    [secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2024-12-16T10:08:50Z    INFO    Detected OS     family="debian" version="12.5"
2024-12-16T10:08:50Z    INFO    [debian] Detecting vulnerabilities...   os_version="12" pkg_num=3
2024-12-16T10:08:50Z    INFO    Number of language-specific files       num=2
2024-12-16T10:08:50Z    INFO    [gobinary] Detecting vulnerabilities...
2024-12-16T10:08:50Z    WARN    Using severities from other vendors for some vulnerabilities. Read https://aquasecurity.github.io/trivy/v0.58/docs/scanner/vulnerability#severity-selection for details.

registry.k8s.io/kube-apiserver:v1.31.0 (debian 12.5)
====================================================
Total: 0 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 0)


go-runner (gobinary)
====================
Total: 3 (UNKNOWN: 0, LOW: 0, MEDIUM: 2, HIGH: 1, CRITICAL: 0)

┌─────────┬────────────────┬──────────┬────────┬───────────────────┬────────────────┬─────────────────────────────────────────────────────────────┐
│ Library │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version  │                            Title                            │
├─────────┼────────────────┼──────────┼────────┼───────────────────┼────────────────┼─────────────────────────────────────────────────────────────┤
│ stdlib  │ CVE-2024-34156 │ HIGH     │ fixed  │ v1.22.5           │ 1.22.7, 1.23.1 │ encoding/gob: golang: Calling Decoder.Decode on a message   │
│         │                │          │        │                   │                │ which contains deeply nested structures...                  │
│         │                │          │        │                   │                │ https://avd.aquasec.com/nvd/cve-2024-34156                  │
│         ├────────────────┼──────────┤        │                   │                ├─────────────────────────────────────────────────────────────┤
│         │ CVE-2024-34155 │ MEDIUM   │        │                   │                │ go/parser: golang: Calling any of the Parse functions       │
│         │                │          │        │                   │                │ containing deeply nested literals...                        │
│         │                │          │        │                   │                │ https://avd.aquasec.com/nvd/cve-2024-34155                  │
│         ├────────────────┤          │        │                   │                ├─────────────────────────────────────────────────────────────┤
│         │ CVE-2024-34158 │          │        │                   │                │ go/build/constraint: golang: Calling Parse on a "// +build" │
│         │                │          │        │                   │                │ build tag line with...                                      │
│         │                │          │        │                   │                │ https://avd.aquasec.com/nvd/cve-2024-34158                  │
└─────────┴────────────────┴──────────┴────────┴───────────────────┴────────────────┴─────────────────────────────────────────────────────────────┘

usr/local/bin/kube-apiserver (gobinary)
=======================================
Total: 6 (UNKNOWN: 0, LOW: 0, MEDIUM: 4, HIGH: 1, CRITICAL: 1)

┌────────────────────────────────┬────────────────┬──────────┬──────────┬───────────────────┬────────────────────┬─────────────────────────────────────────────────────────────┐
│            Library             │ Vulnerability  │ Severity │  Status  │ Installed Version │   Fixed Version    │                            Title                            │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼─────────────────────────────────────────────────────────────┤
│ github.com/opencontainers/runc │ CVE-2024-45310 │ MEDIUM   │ fixed    │ v1.1.13           │ 1.1.14, 1.2.0-rc.3 │ runc: runc can be tricked into creating empty               │
│                                │                │          │          │                   │                    │ files/directories on host                                   │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45310                  │
├────────────────────────────────┼────────────────┼──────────┤          ├───────────────────┼────────────────────┼─────────────────────────────────────────────────────────────┤
│ golang.org/x/crypto            │ CVE-2024-45337 │ CRITICAL │          │ v0.24.0           │ 0.31.0             │ golang.org/x/crypto/ssh: Misuse of                          │
│                                │                │          │          │                   │                    │ ServerConfig.PublicKeyCallback may cause authorization      │
│                                │                │          │          │                   │                    │ bypass in golang.org/x/crypto                               │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45337                  │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼─────────────────────────────────────────────────────────────┤
│ gopkg.in/square/go-jose.v2     │ CVE-2024-28180 │ MEDIUM   │ affected │ v2.6.0            │                    │ jose-go: improper handling of highly compressed data        │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-28180                  │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼─────────────────────────────────────────────────────────────┤
│ stdlib                         │ CVE-2024-34156 │ HIGH     │ fixed    │ v1.22.5           │ 1.22.7, 1.23.1     │ encoding/gob: golang: Calling Decoder.Decode on a message   │
│                                │                │          │          │                   │                    │ which contains deeply nested structures...                  │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-34156                  │
│                                ├────────────────┼──────────┤          │                   │                    ├─────────────────────────────────────────────────────────────┤
│                                │ CVE-2024-34155 │ MEDIUM   │          │                   │                    │ go/parser: golang: Calling any of the Parse functions       │
│                                │                │          │          │                   │                    │ containing deeply nested literals...                        │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-34155                  │
│                                ├────────────────┤          │          │                   │                    ├─────────────────────────────────────────────────────────────┤
│                                │ CVE-2024-34158 │          │          │                   │                    │ go/build/constraint: golang: Calling Parse on a "// +build" │
│                                │                │          │          │                   │                    │ build tag line with...                                      │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-34158                  │
└────────────────────────────────┴────────────────┴──────────┴──────────┴───────────────────┴────────────────────┴─────────────────────────────────────────────────────────────┘
controlplane $ docker run ghcr.io/aquasecurity/trivy:latest image registry.k8s.io/kube-apiserver:v1.31.3
2024-12-16T10:09:29Z    INFO    [vulndb] Need to update DB
2024-12-16T10:09:29Z    INFO    [vulndb] Downloading vulnerability DB...
2024-12-16T10:09:29Z    INFO    [vulndb] Downloading artifact...        repo="mirror.gcr.io/aquasec/trivy-db:2"
227.34 KiB / 57.58 MiB [>____________________________________________________________] 0.39% ? p/s ?2.05 MiB / 57.58 MiB [-->____________________________________________________________] 3.55% ? p/s ?10.62 MiB / 57.58 MiB [----------->_________________________________________________] 18.44% ? p/s ?20.06 MiB / 57.58 MiB [---------------->_______________________________] 34.83% 33.06 MiB p/s ETA 1s29.52 MiB / 57.58 MiB [------------------------>_______________________] 51.26% 33.06 MiB p/s ETA 0s38.82 MiB / 57.58 MiB [-------------------------------->_______________] 67.41% 33.06 MiB p/s ETA 0s47.56 MiB / 57.58 MiB [--------------------------------------->________] 82.59% 33.88 MiB p/s ETA 0s56.81 MiB / 57.58 MiB [----------------------------------------------->] 98.65% 33.88 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.88 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 32.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 32.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 32.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 30.65 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 30.65 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 30.65 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 28.67 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 28.67 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 28.67 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [-------------------------------------------------] 100.00% 16.30 MiB p/s 3.7s2024-12-16T10:09:34Z      INFO    [vulndb] Artifact successfully downloaded       repo="mirror.gcr.io/aquasec/trivy-db:2"
2024-12-16T10:09:34Z    INFO    [vuln] Vulnerability scanning is enabled
2024-12-16T10:09:34Z    INFO    [secret] Secret scanning is enabled
2024-12-16T10:09:34Z    INFO    [secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2024-12-16T10:09:34Z    INFO    [secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2024-12-16T10:09:37Z    INFO    Detected OS     family="debian" version="12.7"
2024-12-16T10:09:37Z    INFO    [debian] Detecting vulnerabilities...   os_version="12" pkg_num=3
2024-12-16T10:09:37Z    INFO    Number of language-specific files       num=2
2024-12-16T10:09:37Z    INFO    [gobinary] Detecting vulnerabilities...

registry.k8s.io/kube-apiserver:v1.31.3 (debian 12.7)
====================================================
Total: 0 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 0)


usr/local/bin/kube-apiserver (gobinary)
=======================================
Total: 3 (UNKNOWN: 0, LOW: 0, MEDIUM: 2, HIGH: 0, CRITICAL: 1)

┌────────────────────────────────┬────────────────┬──────────┬──────────┬───────────────────┬────────────────────┬────────────────────────────────────────────────────────┐
│            Library             │ Vulnerability  │ Severity │  Status  │ Installed Version │   Fixed Version    │                         Title                          │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ github.com/opencontainers/runc │ CVE-2024-45310 │ MEDIUM   │ fixed    │ v1.1.13           │ 1.1.14, 1.2.0-rc.3 │ runc: runc can be tricked into creating empty          │
│                                │                │          │          │                   │                    │ files/directories on host                              │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45310             │
├────────────────────────────────┼────────────────┼──────────┤          ├───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ golang.org/x/crypto            │ CVE-2024-45337 │ CRITICAL │          │ v0.24.0           │ 0.31.0             │ golang.org/x/crypto/ssh: Misuse of                     │
│                                │                │          │          │                   │                    │ ServerConfig.PublicKeyCallback may cause authorization │
│                                │                │          │          │                   │                    │ bypass in golang.org/x/crypto                          │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45337             │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ gopkg.in/square/go-jose.v2     │ CVE-2024-28180 │ MEDIUM   │ affected │ v2.6.0            │                    │ jose-go: improper handling of highly compressed data   │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-28180             │
└────────────────────────────────┴────────────────┴──────────┴──────────┴───────────────────┴────────────────────┴────────────────────────────────────────────────────────┘
controlplane $ docker run ghcr.io/aquasecurity/trivy:latest image registry.k8s.io/kube-apiserver:v1.31.11
2024-12-16T10:09:46Z    INFO    [vulndb] Need to update DB
2024-12-16T10:09:46Z    INFO    [vulndb] Downloading vulnerability DB...
2024-12-16T10:09:46Z    INFO    [vulndb] Downloading artifact...        repo="mirror.gcr.io/aquasec/trivy-db:2"
239.25 KiB / 57.58 MiB [>____________________________________________________________] 0.41% ? p/s ?2.30 MiB / 57.58 MiB [-->____________________________________________________________] 3.99% ? p/s ?11.19 MiB / 57.58 MiB [----------->_________________________________________________] 19.43% ? p/s ?20.61 MiB / 57.58 MiB [----------------->______________________________] 35.79% 33.97 MiB p/s ETA 1s30.08 MiB / 57.58 MiB [------------------------->______________________] 52.23% 33.97 MiB p/s ETA 0s39.42 MiB / 57.58 MiB [-------------------------------->_______________] 68.46% 33.97 MiB p/s ETA 0s48.77 MiB / 57.58 MiB [---------------------------------------->_______] 84.68% 34.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 34.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 34.81 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.49 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.49 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.49 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.33 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.33 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.33 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.31 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.31 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.31 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 27.42 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [-------------------------------------------------] 100.00% 15.31 MiB p/s 4.0s2024-12-16T10:09:51Z  INFO    [vulndb] Artifact successfully downloaded  repo="mirror.gcr.io/aquasec/trivy-db:2"
2024-12-16T10:09:51Z    INFO    [vuln] Vulnerability scanning is enabled
2024-12-16T10:09:51Z    INFO    [secret] Secret scanning is enabled
2024-12-16T10:09:51Z    INFO    [secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2024-12-16T10:09:51Z    INFO    [secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2024-12-16T10:09:52Z    FATAL   Fatal error     image scan error: scan error: unable to initialize a scanner: unable to initialize an image scanner: unable to find the specified image "registry.k8s.io/kube-apiserver:v1.31.11" in ["docker" "containerd" "podman" "remote"]: 4 errors occurred:
        * docker error: unable to inspect the image (registry.k8s.io/kube-apiserver:v1.31.11): Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
        * containerd error: containerd socket not found: /run/containerd/containerd.sock
        * podman error: unable to initialize Podman client: no podman socket found: stat podman/podman.sock: no such file or directory
        * remote error: GET https://asia-south1-docker.pkg.dev/v2/k8s-artifacts-prod/images/kube-apiserver/manifests/v1.31.11: MANIFEST_UNKNOWN: Failed to fetch "v1.31.11"


controlplane $ docker run ghcr.io/aquasecurity/trivy:latest image registry.k8s.io/kube-apiserver:v1.31.3 
2024-12-16T10:10:00Z    INFO    [vulndb] Need to update DB
2024-12-16T10:10:00Z    INFO    [vulndb] Downloading vulnerability DB...
2024-12-16T10:10:00Z    INFO    [vulndb] Downloading artifact...        repo="mirror.gcr.io/aquasec/trivy-db:2"
239.25 KiB / 57.58 MiB [>____________________________________________________________] 0.41% ? p/s ?2.30 MiB / 57.58 MiB [-->____________________________________________________________] 3.99% ? p/s ?11.23 MiB / 57.58 MiB [----------->_________________________________________________] 19.51% ? p/s ?20.77 MiB / 57.58 MiB [----------------->______________________________] 36.06% 34.23 MiB p/s ETA 1s29.14 MiB / 57.58 MiB [------------------------>_______________________] 50.61% 34.23 MiB p/s ETA 0s33.14 MiB / 57.58 MiB [--------------------------->____________________] 57.55% 34.23 MiB p/s ETA 0s41.64 MiB / 57.58 MiB [---------------------------------->_____________] 72.31% 34.27 MiB p/s ETA 0s50.55 MiB / 57.58 MiB [------------------------------------------>_____] 87.78% 34.27 MiB p/s ETA 0s55.64 MiB / 57.58 MiB [---------------------------------------------->_] 96.62% 34.27 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 33.76 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.58 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.58 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 31.58 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.54 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.54 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 29.54 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 27.63 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 27.63 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 27.63 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 25.85 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 25.85 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 25.85 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 24.18 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [---------------------------------------------->] 100.00% 24.18 MiB p/s ETA 0s57.58 MiB / 57.58 MiB [-------------------------------------------------] 100.00% 11.20 MiB p/s 5.3s2024-12-16T10:10:07Z  INFO    [vulndb] Artifact successfully downloaded       repo="mirror.gcr.io/aquasec/trivy-db:2"
2024-12-16T10:10:07Z    INFO    [vuln] Vulnerability scanning is enabled
2024-12-16T10:10:07Z    INFO    [secret] Secret scanning is enabled
2024-12-16T10:10:07Z    INFO    [secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2024-12-16T10:10:07Z    INFO    [secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2024-12-16T10:10:11Z    INFO    Detected OS     family="debian" version="12.7"
2024-12-16T10:10:11Z    INFO    [debian] Detecting vulnerabilities...   os_version="12" pkg_num=3
2024-12-16T10:10:11Z    INFO    Number of language-specific files       num=2
2024-12-16T10:10:11Z    INFO    [gobinary] Detecting vulnerabilities...

registry.k8s.io/kube-apiserver:v1.31.3 (debian 12.7)
====================================================
Total: 0 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 0)


usr/local/bin/kube-apiserver (gobinary)
=======================================
Total: 3 (UNKNOWN: 0, LOW: 0, MEDIUM: 2, HIGH: 0, CRITICAL: 1)

┌────────────────────────────────┬────────────────┬──────────┬──────────┬───────────────────┬────────────────────┬────────────────────────────────────────────────────────┐
│            Library             │ Vulnerability  │ Severity │  Status  │ Installed Version │   Fixed Version    │                         Title                          │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ github.com/opencontainers/runc │ CVE-2024-45310 │ MEDIUM   │ fixed    │ v1.1.13           │ 1.1.14, 1.2.0-rc.3 │ runc: runc can be tricked into creating empty          │
│                                │                │          │          │                   │                    │ files/directories on host                              │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45310             │
├────────────────────────────────┼────────────────┼──────────┤          ├───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ golang.org/x/crypto            │ CVE-2024-45337 │ CRITICAL │          │ v0.24.0           │ 0.31.0             │ golang.org/x/crypto/ssh: Misuse of                     │
│                                │                │          │          │                   │                    │ ServerConfig.PublicKeyCallback may cause authorization │
│                                │                │          │          │                   │                    │ bypass in golang.org/x/crypto                          │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-45337             │
├────────────────────────────────┼────────────────┼──────────┼──────────┼───────────────────┼────────────────────┼────────────────────────────────────────────────────────┤
│ gopkg.in/square/go-jose.v2     │ CVE-2024-28180 │ MEDIUM   │ affected │ v2.6.0            │                    │ jose-go: improper handling of highly compressed data   │
│                                │                │          │          │                   │                    │ https://avd.aquasec.com/nvd/cve-2024-28180             │
└────────────────────────────────┴────────────────┴──────────┴──────────┴───────────────────┴────────────────────┴────────────────────────────────────────────────────────┘
controlplane $ 