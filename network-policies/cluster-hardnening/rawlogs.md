
########manual api query



controlplane $ k config view --raw
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJTm41eDZ1dHFLdGd3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHpOREV5TURRd09URXpOREphTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUUNYM1ByKzcyZ1h0VmNDMzhRczF5VHppamR2cTF5UGs0WVdoMlF2UlFGS2o4TjV3LzdsditwaEpEREwKOXpMRXlUSjNOSGMvdW5vQTdud1d0dzFmK2d3OEFVa09vQkIwZmFqUnROdXNobSsxVDZvSVd2dzJRWGhSR09kZQpCdnB2RzBPQ29qTVVUQVdMVFovRi90aWpYa1BsdldkRGZwMkhBOUJRV3lxNkNTN25WZW9JSTlrdmhYdmNjVHcvCkNrK2QzbEVrVzlBMWZISkk4Y1phUzk5R29ySC96dXI2UWI4UFdkSUJVZVNHR2s4WU05SVcyMzhtdW1RSVdmTWwKa3Frd0Z0NWh5TjdDQkNkK0hsTmJZaUpwUFNrRW9uK0wzV2FQVkdXMXRuKzBYSStoazVPVllRNDcvbmEyTjkyRgpudEtRM3M1TUJvSkwyZVAwZmdIci9ob0pqMFVqQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJTMkpBOGVsNFZySWpOYkZRTzFvZ3JlMXBZcjlEQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQ09Ea1BheHdwVAphQWcvejRKdThUZVFBYXNJUTRpRnZHNzhCSmFOSDNxYUcyaFJubEo5dWl6c1VMZ1FUUTV0dko0UTV4NXI0U0VPCkgxRXBvcmhNTUFqK0VZa1JxdmEybXdxK1JyaWZQdzN4ekpyVUJnb2pxZTFiN1lwOUZjUENlY1VYK0NsVDFXN2oKc01pazFzWXVOenBMdSt4MHdxdTRSckNyWE1IeUVsblNFVHhQWHpqZit4azdaVGQwUkUvUmdnMk9qdzdHdUVLbAo1QmdBL2Riam45T0cza1BOdml5dlFJOFo3UkJ2Y3huQklxQ2dwOHVTdjNaRTVlM0FQSUVXVGdiTEVmcWVMSnhFCmNxR3pDNVczay9zd0ZaVEdqbWtyd1ZuTGlwemJtdndFNGRncWJpeVlPY2dPREFrcXlPK2ZpMElGT25LZkpBVWYKaFlQZGxTaXZEc3JSCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://172.30.1.2:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURLVENDQWhHZ0F3SUJBZ0lJYm1DU21LU3lDWXN3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHlOVEV5TURZd09URXpOREphTUR3eApIekFkQmdOVkJBb1RGbXQxWW1WaFpHMDZZMngxYzNSbGNpMWhaRzFwYm5NeEdUQVhCZ05WQkFNVEVHdDFZbVZ5CmJtVjBaWE10WVdSdGFXNHdnZ0VpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCRHdBd2dnRUtBb0lCQVFDekJxTHcKR0dQWmQzempaSkpucWJZd0xuRnE1WFYwYnFyaWRGckR4bGlaQUFudzRqMjJPYjh1TlhqN2JwVDdCN2srcEY2QgpGbXhLRzl0ZXVmaTd4REJFRTArMXZpLy9JZmJURjVhWURUa3MweFV3VUZ6a1kwaG9oS1R0U1AxTVpWNmlucXl6CmdqS3VtRGU5Y0RScWlYaWxoNGZ0RDZQUXZvQ1dOZ3puTVpqUklIVDBTRmlyempqKytIK1FRaE1mYWRkV0pJSVAKOWttekp2NXN6V2Z0cnRMZktDbkFGZ2VQcUwyRjQzc1VGK1V2UzBjQ3NNZWdMWGVxS3RuSFZVQ2lrUUQ5RDNrRwprYklIWmpMd2QwRkU3L1hMWnhUZzcvUWpHdWY0UElocUVmMFpwL1I5WEFFOTBwbitScHFRZk5rZ0htdEE2NlphCmFSM0hKcWRVQWRtZUk0eXBBZ01CQUFHalZqQlVNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUsKQmdnckJnRUZCUWNEQWpBTUJnTlZIUk1CQWY4RUFqQUFNQjhHQTFVZEl3UVlNQmFBRkxZa0R4NlhoV3NpTTFzVgpBN1dpQ3Q3V2xpdjBNQTBHQ1NxR1NJYjNEUUVCQ3dVQUE0SUJBUUNMZUQ2SWd5TEVXald1aHliNHVoeWsxRmxPCnp5WmZvcjVLREcxUTZkWWlicDBBQVBuYkprRzVSSStveFJNUkZVMWhRTmR5ZFl5V3ptUmxnRnZBeS9RSjR0VVAKb3dPUWg0RUNFTndYWFp4aUFjL1RnR3VkRHAya1JzYWNWMmg5Yis1RGxaWTZHamJOME9CdHRGS1kwZ0hSdlZJSgpKblZGYnRuUityQmRZTmJCa3dOSU1KOHNhcjBOcGJTc1lCbEVRSWc3bzlCRURwdjM0dlZYUnIrT24xU1RkUzl5CjUvVGVvK25TQnA3bmFobWhMNWFqbmVTNHNuODBPTlJicVRtTEhYUCt1K3llSzNGcENsUHJ0T1RJZ1A4UGJ4MXkKdTd5TGk4eGpNdUlmSkM0bUI2cEp6OWRXU0xOWURIUEt0N24wYmdtR1dPaGhObkR0MUpub0xOS3dVSCthCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcFFJQkFBS0NBUUVBc3dhaThCaGoyWGQ4NDJTU1o2bTJNQzV4YXVWMWRHNnE0blJhdzhaWW1RQUo4T0k5CnRqbS9MalY0KzI2VSt3ZTVQcVJlZ1Jac1NodmJYcm40dThRd1JCTlB0YjR2L3lIMjB4ZVdtQTA1TE5NVk1GQmMKNUdOSWFJU2s3VWo5VEdWZW9wNnNzNEl5cnBnM3ZYQTBhb2w0cFllSDdRK2owTDZBbGpZTTV6R1kwU0IwOUVoWQpxODQ0L3ZoL2tFSVRIMm5YVmlTQ0QvWkpzeWIrYk0xbjdhN1MzeWdwd0JZSGo2aTloZU43RkJmbEwwdEhBckRICm9DMTNxaXJaeDFWQW9wRUEvUTk1QnBHeUIyWXk4SGRCUk8vMXkyY1U0Ty8wSXhybitEeUlhaEg5R2FmMGZWd0IKUGRLWi9rYWFrSHpaSUI1clFPdW1XbWtkeHlhblZBSFpuaU9NcVFJREFRQUJBb0lCQVFDU0M5L3dyblVHZTR2TwpsY1U1L0NFOHZTYVpaZ2VqcklTTHFSQkNsaFRBL0Y4ZnUvRk1MMS9mZW8vdnpnNkxtNGxycVB2UG8xTkVRZVY4CktZclk0dnZkRFVRQnA5M1A3UTFHdC8rS20zOEJLbElteitoNENPYVJIV1RPanJUVkZmMVYvTXcyeFFoRGxyb2kKT044SjZvd1p2YThObmF5dUpqc1FUNWZISTViZlFwUkNaaStvY1JRK1BOOG00WFdKbHdXSUtPNjhXWjRvSEpERgo1TEZ6cjRjckRWcTNUSVJSaXI1Q3QvV2dRTWpRWTFkSFpMUGJUYTBlNkk0bDcyNTdqdnlQdDNHMHREbHordUYyCnF3TzY4S2NIeHpUQ1NtcjJDSWFEMDRVTk9QOVVEVkFpc09lWnVzOFF6dWlGbFV0R08rNEZ1QzduSzZhdVhrbEMKTmlBcEh4Z0JBb0dCQU1LT0ZuNW1jU3dORFhqRW1rR0ZubkxSek43Qi84dTZ4cHdxc1hNUHdSZGNhMHpkbFE1SgpIQ1N3WWR6aVNKMklYQ0hhK1hrZTB4Z1VDVGIzcVcwQ21nNTlkdjBDb0RIMmM5M2hIZWRVR1ZDTHVSMDN1dURaCjVzNGR1WCtpK0l5c1loUlpwcStXSjlyQUhBQ0N2ZHFiZVNQVUc4QWVwS3lZS3pjSUdUc1A3amFKQW9HQkFPdVIKQW1HbXhjSFVkSTdoR3FPeUJUMDRBV3FDY01xbW5qNTM4UVM1VGFNc2h2b05RZFB2dHJKSUROdnhiTGFLODJZUwpLejVxcXg3bldmK1lqMnV2bXd6YitJeW9vYVFJNGE1cnVOWksxa0RGQ0I1T0FSdG5taGFuUDV4N2tha090ZzNnCmc2bkk1N29FRU5DN3ZqbFc2WEdOeldNbkpYdGRBSnlkUmgwQitSMGhBb0dCQUl2R1lVcTJkcUJiVUU1dmtSTjUKMS9oTjJvNC9lbkwzNFREWlMxdUsrZ0s2bHl4R0ZZeUo0ZnBKN2tVdkhWUndYeUREblcvelFWMlBKMytpTnNybQpqNS9SYStjaU44MHRidGo5bnVwUGRWQjAwYTI0R0Q3cXpmTlBUN0h2ZC9vNDdzNElDc1VqYjhhdE5uRDNmVWJOClpCN2xpSHBpaVpTbVRvWGUvNkY3TkgxaEFvR0JBTkErMFN3aWtwQlhrUEwrYk41cGNkZzh1b085N0pnNTA0ckYKM1h1ZmxOSzdlbGR6Z000ckRBZHZTbTdsYm9XeE1KcjdWTjlJelIzMHg4cjh3MDBmWUtKdGs3eEZGeUE3K2NhSAoxRThjdVd0b3cxU0hBTk9KTXQ3ejIzZ3FoUW8reHhKZGVBZVFZOG85N2QrWkdRRDNwRWVPWkJOVGQvOG1xSFBMClZVQXZqbG9CQW9HQU5kODVFZG40MVF1b2pEeHYrTzc3SGZkS0x2N3BlbC9yUTgwNzRTenBSM2YzbE1mb2pxV0UKaVdOWTFwQzFZWXh4VEVGa3VDaURvMVhpOHUvQXVIZlQrc3VMSlAwUEIvU3NzWlN3ZDhsTXlnTjVrQ3h4WFRCSAowd2FOYWF5eW1Pc3JpZmR6c3d4N2tVcDBNVmtERGhxamlpUStJQ3RFVUFraVZkTnNVOHBVTndrPQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
controlplane $ echo "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJTm41eDZ1dHFLdGd3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHpOREV5TURRd09URXpOREphTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUUNYM1ByKzcyZ1h0VmNDMzhRczF5VHppamR2cTF5UGs0WVdoMlF2UlFGS2o4TjV3LzdsditwaEpEREwKOXpMRXlUSjNOSGMvdW5vQTdud1d0dzFmK2d3OEFVa09vQkIwZmFqUnROdXNobSsxVDZvSVd2dzJRWGhSR09kZQpCdnB2RzBPQ29qTVVUQVdMVFovRi90aWpYa1BsdldkRGZwMkhBOUJRV3lxNkNTN25WZW9JSTlrdmhYdmNjVHcvCkNrK2QzbEVrVzlBMWZISkk4Y1phUzk5R29ySC96dXI2UWI4UFdkSUJVZVNHR2s4WU05SVcyMzhtdW1RSVdmTWwKa3Frd0Z0NWh5TjdDQkNkK0hsTmJZaUpwUFNrRW9uK0wzV2FQVkdXMXRuKzBYSStoazVPVllRNDcvbmEyTjkyRgpudEtRM3M1TUJvSkwyZVAwZmdIci9ob0pqMFVqQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJTMkpBOGVsNFZySWpOYkZRTzFvZ3JlMXBZcjlEQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQ09Ea1BheHdwVAphQWcvejRKdThUZVFBYXNJUTRpRnZHNzhCSmFOSDNxYUcyaFJubEo5dWl6c1VMZ1FUUTV0dko0UTV4NXI0U0VPCkgxRXBvcmhNTUFqK0VZa1JxdmEybXdxK1JyaWZQdzN4ekpyVUJnb2pxZTFiN1lwOUZjUENlY1VYK0NsVDFXN2oKc01pazFzWXVOenBMdSt4MHdxdTRSckNyWE1IeUVsblNFVHhQWHpqZit4azdaVGQwUkUvUmdnMk9qdzdHdUVLbAo1QmdBL2Riam45T0cza1BOdml5dlFJOFo3UkJ2Y3huQklxQ2dwOHVTdjNaRTVlM0FQSUVXVGdiTEVmcWVMSnhFCmNxR3pDNVczay9zd0ZaVEdqbWtyd1ZuTGlwemJtdndFNGRncWJpeVlPY2dPREFrcXlPK2ZpMElGT25LZkpBVWYKaFlQZGxTaXZEc3JSCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K" | base64 --decode
-----BEGIN CERTIFICATE-----
MIIDBTCCAe2gAwIBAgIINn5x6utqKtgwDQYJKoZIhvcNAQELBQAwFTETMBEGA1UE
AxMKa3ViZXJuZXRlczAeFw0yNDEyMDYwOTA4NDJaFw0zNDEyMDQwOTEzNDJaMBUx
EzARBgNVBAMTCmt1YmVybmV0ZXMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK
AoIBAQCX3Pr+72gXtVcC38Qs1yTzijdvq1yPk4YWh2QvRQFKj8N5w/7lv+phJDDL
9zLEyTJ3NHc/unoA7nwWtw1f+gw8AUkOoBB0fajRtNushm+1T6oIWvw2QXhRGOde
BvpvG0OCojMUTAWLTZ/F/tijXkPlvWdDfp2HA9BQWyq6CS7nVeoII9kvhXvccTw/
Ck+d3lEkW9A1fHJI8cZaS99GorH/zur6Qb8PWdIBUeSGGk8YM9IW238mumQIWfMl
kqkwFt5hyN7CBCd+HlNbYiJpPSkEon+L3WaPVGW1tn+0XI+hk5OVYQ47/na2N92F
ntKQ3s5MBoJL2eP0fgHr/hoJj0UjAgMBAAGjWTBXMA4GA1UdDwEB/wQEAwICpDAP
BgNVHRMBAf8EBTADAQH/MB0GA1UdDgQWBBS2JA8el4VrIjNbFQO1ogre1pYr9DAV
BgNVHREEDjAMggprdWJlcm5ldGVzMA0GCSqGSIb3DQEBCwUAA4IBAQCODkPaxwpT
aAg/z4Ju8TeQAasIQ4iFvG78BJaNH3qaG2hRnlJ9uizsULgQTQ5tvJ4Q5x5r4SEO
H1EporhMMAj+EYkRqva2mwq+RrifPw3xzJrUBgojqe1b7Yp9FcPCecUX+ClT1W7j
sMik1sYuNzpLu+x0wqu4RrCrXMHyElnSETxPXzjf+xk7ZTd0RE/Rgg2Ojw7GuEKl
5BgA/dbjn9OG3kPNviyvQI8Z7RBvcxnBIqCgp8uSv3ZE5e3APIEWTgbLEfqeLJxE
cqGzC5W3k/swFZTGjmkrwVnLipzbmvwE4dgqbiyYOcgODAkqyO+fi0IFOnKfJAUf
hYPdlSivDsrR
-----END CERTIFICATE-----
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ echo "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJTm41eDZ1dHFLdGd3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHpOREV5TURRd09URXpOREphTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUUNYM1ByKzcyZ1h0VmNDMzhRczF5VHppamR2cTF5UGs0WVdoMlF2UlFGS2o4TjV3LzdsditwaEpEREwKOXpMRXlUSjNOSGMvdW5vQTdud1d0dzFmK2d3OEFVa09vQkIwZmFqUnROdXNobSsxVDZvSVd2dzJRWGhSR09kZQpCdnB2RzBPQ29qTVVUQVdMVFovRi90aWpYa1BsdldkRGZwMkhBOUJRV3lxNkNTN25WZW9JSTlrdmhYdmNjVHcvCkNrK2QzbEVrVzlBMWZISkk4Y1phUzk5R29ySC96dXI2UWI4UFdkSUJVZVNHR2s4WU05SVcyMzhtdW1RSVdmTWwKa3Frd0Z0NWh5TjdDQkNkK0hsTmJZaUpwUFNrRW9uK0wzV2FQVkdXMXRuKzBYSStoazVPVllRNDcvbmEyTjkyRgpudEtRM3M1TUJvSkwyZVAwZmdIci9ob0pqMFVqQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJTMkpBOGVsNFZySWpOYkZRTzFvZ3JlMXBZcjlEQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQ09Ea1BheHdwVAphQWcvejRKdThUZVFBYXNJUTRpRnZHNzhCSmFOSDNxYUcyaFJubEo5dWl6c1VMZ1FUUTV0dko0UTV4NXI0U0VPCkgxRXBvcmhNTUFqK0VZa1JxdmEybXdxK1JyaWZQdzN4ekpyVUJnb2pxZTFiN1lwOUZjUENlY1VYK0NsVDFXN2oKc01pazFzWXVOenBMdSt4MHdxdTRSckNyWE1IeUVsblNFVHhQWHpqZit4azdaVGQwUkUvUmdnMk9qdzdHdUVLbAo1QmdBL2Riam45T0cza1BOdml5dlFJOFo3UkJ2Y3huQklxQ2dwOHVTdjNaRTVlM0FQSUVXVGdiTEVmcWVMSnhFCmNxR3pDNVczay9zd0ZaVEdqbWtyd1ZuTGlwemJtdndFNGRncWJpeVlPY2dPREFrcXlPK2ZpMElGT25LZkpBVWYKaFlQZGxTaXZEc3JSCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K" | base64 --decode > ca
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ echo "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURLVENDQWhHZ0F3SUJBZ0lJYm1DU21LU3lDWXN3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHlOVEV5TURZd09URXpOREphTUR3eApIekFkQmdOVkJBb1RGbXQxWW1WaFpHMDZZMngxYzNSbGNpMWhaRzFwYm5NeEdUQVhCZ05WQkFNVEVHdDFZbVZ5CmJtVjBaWE10WVdSdGFXNHdnZ0VpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCRHdBd2dnRUtBb0lCQVFDekJxTHcKR0dQWmQzempaSkpucWJZd0xuRnE1WFYwYnFyaWRGckR4bGlaQUFudzRqMjJPYjh1TlhqN2JwVDdCN2srcEY2QgpGbXhLRzl0ZXVmaTd4REJFRTArMXZpLy9JZmJURjVhWURUa3MweFV3VUZ6a1kwaG9oS1R0U1AxTVpWNmlucXl6CmdqS3VtRGU5Y0RScWlYaWxoNGZ0RDZQUXZvQ1dOZ3puTVpqUklIVDBTRmlyempqKytIK1FRaE1mYWRkV0pJSVAKOWttekp2NXN6V2Z0cnRMZktDbkFGZ2VQcUwyRjQzc1VGK1V2UzBjQ3NNZWdMWGVxS3RuSFZVQ2lrUUQ5RDNrRwprYklIWmpMd2QwRkU3L1hMWnhUZzcvUWpHdWY0UElocUVmMFpwL1I5WEFFOTBwbitScHFRZk5rZ0htdEE2NlphCmFSM0hKcWRVQWRtZUk0eXBBZ01CQUFHalZqQlVNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUsKQmdnckJnRUZCUWNEQWpBTUJnTlZIUk1CQWY4RUFqQUFNQjhHQTFVZEl3UVlNQmFBRkxZa0R4NlhoV3NpTTFzVgpBN1dpQ3Q3V2xpdjBNQTBHQ1NxR1NJYjNEUUVCQ3dVQUE0SUJBUUNMZUQ2SWd5TEVXald1aHliNHVoeWsxRmxPCnp5WmZvcjVLREcxUTZkWWlicDBBQVBuYkprRzVSSStveFJNUkZVMWhRTmR5ZFl5V3ptUmxnRnZBeS9RSjR0VVAKb3dPUWg0RUNFTndYWFp4aUFjL1RnR3VkRHAya1JzYWNWMmg5Yis1RGxaWTZHamJOME9CdHRGS1kwZ0hSdlZJSgpKblZGYnRuUityQmRZTmJCa3dOSU1KOHNhcjBOcGJTc1lCbEVRSWc3bzlCRURwdjM0dlZYUnIrT24xU1RkUzl5CjUvVGVvK25TQnA3bmFobWhMNWFqbmVTNHNuODBPTlJicVRtTEhYUCt1K3llSzNGcENsUHJ0T1RJZ1A4UGJ4MXkKdTd5TGk4eGpNdUlmSkM0bUI2cEp6OWRXU0xOWURIUEt0N24wYmdtR1dPaGhObkR0MUpub0xOS3dVSCthCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K" | base64 --decode 
-----BEGIN CERTIFICATE-----
MIIDKTCCAhGgAwIBAgIIbmCSmKSyCYswDQYJKoZIhvcNAQELBQAwFTETMBEGA1UE
AxMKa3ViZXJuZXRlczAeFw0yNDEyMDYwOTA4NDJaFw0yNTEyMDYwOTEzNDJaMDwx
HzAdBgNVBAoTFmt1YmVhZG06Y2x1c3Rlci1hZG1pbnMxGTAXBgNVBAMTEGt1YmVy
bmV0ZXMtYWRtaW4wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCzBqLw
GGPZd3zjZJJnqbYwLnFq5XV0bqridFrDxliZAAnw4j22Ob8uNXj7bpT7B7k+pF6B
FmxKG9teufi7xDBEE0+1vi//IfbTF5aYDTks0xUwUFzkY0hohKTtSP1MZV6inqyz
gjKumDe9cDRqiXilh4ftD6PQvoCWNgznMZjRIHT0SFirzjj++H+QQhMfaddWJIIP
9kmzJv5szWftrtLfKCnAFgePqL2F43sUF+UvS0cCsMegLXeqKtnHVUCikQD9D3kG
kbIHZjLwd0FE7/XLZxTg7/QjGuf4PIhqEf0Zp/R9XAE90pn+RpqQfNkgHmtA66Za
aR3HJqdUAdmeI4ypAgMBAAGjVjBUMA4GA1UdDwEB/wQEAwIFoDATBgNVHSUEDDAK
BggrBgEFBQcDAjAMBgNVHRMBAf8EAjAAMB8GA1UdIwQYMBaAFLYkDx6XhWsiM1sV
A7WiCt7Wliv0MA0GCSqGSIb3DQEBCwUAA4IBAQCLeD6IgyLEWjWuhyb4uhyk1FlO
zyZfor5KDG1Q6dYibp0AAPnbJkG5RI+oxRMRFU1hQNdydYyWzmRlgFvAy/QJ4tUP
owOQh4ECENwXXZxiAc/TgGudDp2kRsacV2h9b+5DlZY6GjbN0OBttFKY0gHRvVIJ
JnVFbtnR+rBdYNbBkwNIMJ8sar0NpbSsYBlEQIg7o9BEDpv34vVXRr+On1STdS9y
5/Teo+nSBp7nahmhL5ajneS4sn80ONRbqTmLHXP+u+yeK3FpClPrtOTIgP8Pbx1y
u7yLi8xjMuIfJC4mB6pJz9dWSLNYDHPKt7n0bgmGWOhhNnDt1JnoLNKwUH+a
-----END CERTIFICATE-----
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ echo "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURLVENDQWhHZ0F3SUJBZ0lJYm1DU21LU3lDWXN3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeU1EWXdPVEE0TkRKYUZ3MHlOVEV5TURZd09URXpOREphTUR3eApIekFkQmdOVkJBb1RGbXQxWW1WaFpHMDZZMngxYzNSbGNpMWhaRzFwYm5NeEdUQVhCZ05WQkFNVEVHdDFZbVZ5CmJtVjBaWE10WVdSdGFXNHdnZ0VpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCRHdBd2dnRUtBb0lCQVFDekJxTHcKR0dQWmQzempaSkpucWJZd0xuRnE1WFYwYnFyaWRGckR4bGlaQUFudzRqMjJPYjh1TlhqN2JwVDdCN2srcEY2QgpGbXhLRzl0ZXVmaTd4REJFRTArMXZpLy9JZmJURjVhWURUa3MweFV3VUZ6a1kwaG9oS1R0U1AxTVpWNmlucXl6CmdqS3VtRGU5Y0RScWlYaWxoNGZ0RDZQUXZvQ1dOZ3puTVpqUklIVDBTRmlyempqKytIK1FRaE1mYWRkV0pJSVAKOWttekp2NXN6V2Z0cnRMZktDbkFGZ2VQcUwyRjQzc1VGK1V2UzBjQ3NNZWdMWGVxS3RuSFZVQ2lrUUQ5RDNrRwprYklIWmpMd2QwRkU3L1hMWnhUZzcvUWpHdWY0UElocUVmMFpwL1I5WEFFOTBwbitScHFRZk5rZ0htdEE2NlphCmFSM0hKcWRVQWRtZUk0eXBBZ01CQUFHalZqQlVNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUsKQmdnckJnRUZCUWNEQWpBTUJnTlZIUk1CQWY4RUFqQUFNQjhHQTFVZEl3UVlNQmFBRkxZa0R4NlhoV3NpTTFzVgpBN1dpQ3Q3V2xpdjBNQTBHQ1NxR1NJYjNEUUVCQ3dVQUE0SUJBUUNMZUQ2SWd5TEVXald1aHliNHVoeWsxRmxPCnp5WmZvcjVLREcxUTZkWWlicDBBQVBuYkprRzVSSStveFJNUkZVMWhRTmR5ZFl5V3ptUmxnRnZBeS9RSjR0VVAKb3dPUWg0RUNFTndYWFp4aUFjL1RnR3VkRHAya1JzYWNWMmg5Yis1RGxaWTZHamJOME9CdHRGS1kwZ0hSdlZJSgpKblZGYnRuUityQmRZTmJCa3dOSU1KOHNhcjBOcGJTc1lCbEVRSWc3bzlCRURwdjM0dlZYUnIrT24xU1RkUzl5CjUvVGVvK25TQnA3bmFobWhMNWFqbmVTNHNuODBPTlJicVRtTEhYUCt1K3llSzNGcENsUHJ0T1RJZ1A4UGJ4MXkKdTd5TGk4eGpNdUlmSkM0bUI2cEp6OWRXU0xOWURIUEt0N24wYmdtR1dPaGhObkR0MUpub0xOS3dVSCthCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K" | base64 --decode > crt
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ echo "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcFFJQkFBS0NBUUVBc3dhaThCaGoyWGQ4NDJTU1o2bTJNQzV4YXVWMWRHNnE0blJhdzhaWW1RQUo4T0k5CnRqbS9MalY0KzI2VSt3ZTVQcVJlZ1Jac1NodmJYcm40dThRd1JCTlB0YjR2L3lIMjB4ZVdtQTA1TE5NVk1GQmMKNUdOSWFJU2s3VWo5VEdWZW9wNnNzNEl5cnBnM3ZYQTBhb2w0cFllSDdRK2owTDZBbGpZTTV6R1kwU0IwOUVoWQpxODQ0L3ZoL2tFSVRIMm5YVmlTQ0QvWkpzeWIrYk0xbjdhN1MzeWdwd0JZSGo2aTloZU43RkJmbEwwdEhBckRICm9DMTNxaXJaeDFWQW9wRUEvUTk1QnBHeUIyWXk4SGRCUk8vMXkyY1U0Ty8wSXhybitEeUlhaEg5R2FmMGZWd0IKUGRLWi9rYWFrSHpaSUI1clFPdW1XbWtkeHlhblZBSFpuaU9NcVFJREFRQUJBb0lCQVFDU0M5L3dyblVHZTR2TwpsY1U1L0NFOHZTYVpaZ2VqcklTTHFSQkNsaFRBL0Y4ZnUvRk1MMS9mZW8vdnpnNkxtNGxycVB2UG8xTkVRZVY4CktZclk0dnZkRFVRQnA5M1A3UTFHdC8rS20zOEJLbElteitoNENPYVJIV1RPanJUVkZmMVYvTXcyeFFoRGxyb2kKT044SjZvd1p2YThObmF5dUpqc1FUNWZISTViZlFwUkNaaStvY1JRK1BOOG00WFdKbHdXSUtPNjhXWjRvSEpERgo1TEZ6cjRjckRWcTNUSVJSaXI1Q3QvV2dRTWpRWTFkSFpMUGJUYTBlNkk0bDcyNTdqdnlQdDNHMHREbHordUYyCnF3TzY4S2NIeHpUQ1NtcjJDSWFEMDRVTk9QOVVEVkFpc09lWnVzOFF6dWlGbFV0R08rNEZ1QzduSzZhdVhrbEMKTmlBcEh4Z0JBb0dCQU1LT0ZuNW1jU3dORFhqRW1rR0ZubkxSek43Qi84dTZ4cHdxc1hNUHdSZGNhMHpkbFE1SgpIQ1N3WWR6aVNKMklYQ0hhK1hrZTB4Z1VDVGIzcVcwQ21nNTlkdjBDb0RIMmM5M2hIZWRVR1ZDTHVSMDN1dURaCjVzNGR1WCtpK0l5c1loUlpwcStXSjlyQUhBQ0N2ZHFiZVNQVUc4QWVwS3lZS3pjSUdUc1A3amFKQW9HQkFPdVIKQW1HbXhjSFVkSTdoR3FPeUJUMDRBV3FDY01xbW5qNTM4UVM1VGFNc2h2b05RZFB2dHJKSUROdnhiTGFLODJZUwpLejVxcXg3bldmK1lqMnV2bXd6YitJeW9vYVFJNGE1cnVOWksxa0RGQ0I1T0FSdG5taGFuUDV4N2tha090ZzNnCmc2bkk1N29FRU5DN3ZqbFc2WEdOeldNbkpYdGRBSnlkUmgwQitSMGhBb0dCQUl2R1lVcTJkcUJiVUU1dmtSTjUKMS9oTjJvNC9lbkwzNFREWlMxdUsrZ0s2bHl4R0ZZeUo0ZnBKN2tVdkhWUndYeUREblcvelFWMlBKMytpTnNybQpqNS9SYStjaU44MHRidGo5bnVwUGRWQjAwYTI0R0Q3cXpmTlBUN0h2ZC9vNDdzNElDc1VqYjhhdE5uRDNmVWJOClpCN2xpSHBpaVpTbVRvWGUvNkY3TkgxaEFvR0JBTkErMFN3aWtwQlhrUEwrYk41cGNkZzh1b085N0pnNTA0ckYKM1h1ZmxOSzdlbGR6Z000ckRBZHZTbTdsYm9XeE1KcjdWTjlJelIzMHg4cjh3MDBmWUtKdGs3eEZGeUE3K2NhSAoxRThjdVd0b3cxU0hBTk9KTXQ3ejIzZ3FoUW8reHhKZGVBZVFZOG85N2QrWkdRRDNwRWVPWkJOVGQvOG1xSFBMClZVQXZqbG9CQW9HQU5kODVFZG40MVF1b2pEeHYrTzc3SGZkS0x2N3BlbC9yUTgwNzRTenBSM2YzbE1mb2pxV0UKaVdOWTFwQzFZWXh4VEVGa3VDaURvMVhpOHUvQXVIZlQrc3VMSlAwUEIvU3NzWlN3ZDhsTXlnTjVrQ3h4WFRCSAowd2FOYWF5eW1Pc3JpZmR6c3d4N2tVcDBNVmtERGhxamlpUStJQ3RFVUFraVZkTnNVOHBVTndrPQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=" | base64 --decode > key
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://172.30.1.2:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl  https://172.30.1.2:6443
curl: (60) SSL certificate problem: unable to get local issuer certificate
More details here: https://curl.haxx.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl  https://172.30.1.2:6443 --cacert ca   
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "forbidden: User \"system:anonymous\" cannot get path \"/\"",
  "reason": "Forbidden",
  "details": {},
  "code": 403
}controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl  https://172.30.1.2:6443 --cacert ca --cert crt
curl: (58) unable to set private key file: 'crt' type PEM
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl  https://172.30.1.2:6443 --cacert ca --cert crt --key key
{
  "paths": [
    "/.well-known/openid-configuration",
    "/api",
    "/api/v1",
    "/apis",
    "/apis/",
    "/apis/admissionregistration.k8s.io",
    "/apis/admissionregistration.k8s.io/v1",
    "/apis/apiextensions.k8s.io",
    "/apis/apiextensions.k8s.io/v1",
    "/apis/apiregistration.k8s.io",
    "/apis/apiregistration.k8s.io/v1",
    "/apis/apps",
    "/apis/apps/v1",
    "/apis/authentication.k8s.io",
    "/apis/authentication.k8s.io/v1",
    "/apis/authorization.k8s.io",
    "/apis/authorization.k8s.io/v1",
    "/apis/autoscaling",
    "/apis/autoscaling/v1",
    "/apis/autoscaling/v2",
    "/apis/batch",
    "/apis/batch/v1",
    "/apis/certificates.k8s.io",
    "/apis/certificates.k8s.io/v1",
    "/apis/coordination.k8s.io",
    "/apis/coordination.k8s.io/v1",
    "/apis/crd.projectcalico.org",
    "/apis/crd.projectcalico.org/v1",
    "/apis/discovery.k8s.io",
    "/apis/discovery.k8s.io/v1",
    "/apis/events.k8s.io",
    "/apis/events.k8s.io/v1",
    "/apis/flowcontrol.apiserver.k8s.io",
    "/apis/flowcontrol.apiserver.k8s.io/v1",
    "/apis/flowcontrol.apiserver.k8s.io/v1beta3",
    "/apis/networking.k8s.io",
    "/apis/networking.k8s.io/v1",
    "/apis/node.k8s.io",
    "/apis/node.k8s.io/v1",
    "/apis/policy",
    "/apis/policy/v1",
    "/apis/rbac.authorization.k8s.io",
    "/apis/rbac.authorization.k8s.io/v1",
    "/apis/scheduling.k8s.io",
    "/apis/scheduling.k8s.io/v1",
    "/apis/storage.k8s.io",
    "/apis/storage.k8s.io/v1",
    "/healthz",
    "/healthz/autoregister-completion",
    "/healthz/etcd",
    "/healthz/log",
    "/healthz/ping",
    "/healthz/poststarthook/aggregator-reload-proxy-client-cert",
    "/healthz/poststarthook/apiservice-discovery-controller",
    "/healthz/poststarthook/apiservice-openapi-controller",
    "/healthz/poststarthook/apiservice-openapiv3-controller",
    "/healthz/poststarthook/apiservice-registration-controller",
    "/healthz/poststarthook/apiservice-status-local-available-controller",
    "/healthz/poststarthook/apiservice-status-remote-available-controller",
    "/healthz/poststarthook/bootstrap-controller",
    "/healthz/poststarthook/crd-informer-synced",
    "/healthz/poststarthook/generic-apiserver-start-informers",
    "/healthz/poststarthook/kube-apiserver-autoregistration",
    "/healthz/poststarthook/priority-and-fairness-config-consumer",
    "/healthz/poststarthook/priority-and-fairness-config-producer",
    "/healthz/poststarthook/priority-and-fairness-filter",
    "/healthz/poststarthook/rbac/bootstrap-roles",
    "/healthz/poststarthook/scheduling/bootstrap-system-priority-classes",
    "/healthz/poststarthook/start-apiextensions-controllers",
    "/healthz/poststarthook/start-apiextensions-informers",
    "/healthz/poststarthook/start-apiserver-admission-initializer",
    "/healthz/poststarthook/start-cluster-authentication-info-controller",
    "/healthz/poststarthook/start-kube-aggregator-informers",
    "/healthz/poststarthook/start-kube-apiserver-identity-lease-controller",
    "/healthz/poststarthook/start-kube-apiserver-identity-lease-garbage-collector",
    "/healthz/poststarthook/start-legacy-token-tracking-controller",
    "/healthz/poststarthook/start-service-ip-repair-controllers",
    "/healthz/poststarthook/start-system-namespaces-controller",
    "/healthz/poststarthook/storage-object-count-tracker-hook",
    "/livez",
    "/livez/autoregister-completion",
    "/livez/etcd",
    "/livez/log",
    "/livez/ping",
    "/livez/poststarthook/aggregator-reload-proxy-client-cert",
    "/livez/poststarthook/apiservice-discovery-controller",
    "/livez/poststarthook/apiservice-openapi-controller",
    "/livez/poststarthook/apiservice-openapiv3-controller",
    "/livez/poststarthook/apiservice-registration-controller",
    "/livez/poststarthook/apiservice-status-local-available-controller",
    "/livez/poststarthook/apiservice-status-remote-available-controller",
    "/livez/poststarthook/bootstrap-controller",
    "/livez/poststarthook/crd-informer-synced",
    "/livez/poststarthook/generic-apiserver-start-informers",
    "/livez/poststarthook/kube-apiserver-autoregistration",
    "/livez/poststarthook/priority-and-fairness-config-consumer",
    "/livez/poststarthook/priority-and-fairness-config-producer",
    "/livez/poststarthook/priority-and-fairness-filter",
    "/livez/poststarthook/rbac/bootstrap-roles",
    "/livez/poststarthook/scheduling/bootstrap-system-priority-classes",
    "/livez/poststarthook/start-apiextensions-controllers",
    "/livez/poststarthook/start-apiextensions-informers",
    "/livez/poststarthook/start-apiserver-admission-initializer",
    "/livez/poststarthook/start-cluster-authentication-info-controller",
    "/livez/poststarthook/start-kube-aggregator-informers",
    "/livez/poststarthook/start-kube-apiserver-identity-lease-controller",
    "/livez/poststarthook/start-kube-apiserver-identity-lease-garbage-collector",
    "/livez/poststarthook/start-legacy-token-tracking-controller",
    "/livez/poststarthook/start-service-ip-repair-controllers",
    "/livez/poststarthook/start-system-namespaces-controller",
    "/livez/poststarthook/storage-object-count-tracker-hook",
    "/metrics",
    "/metrics/slis",
    "/openapi/v2",
    "/openapi/v3",
    "/openapi/v3/",
    "/openid/v1/jwks",
    "/readyz",
    "/readyz/autoregister-completion",
    "/readyz/etcd",
    "/readyz/etcd-readiness",
    "/readyz/informer-sync",
    "/readyz/log",
    "/readyz/ping",
    "/readyz/poststarthook/aggregator-reload-proxy-client-cert",
    "/readyz/poststarthook/apiservice-discovery-controller",
    "/readyz/poststarthook/apiservice-openapi-controller",
    "/readyz/poststarthook/apiservice-openapiv3-controller",
    "/readyz/poststarthook/apiservice-registration-controller",
    "/readyz/poststarthook/apiservice-status-local-available-controller",
    "/readyz/poststarthook/apiservice-status-remote-available-controller",
    "/readyz/poststarthook/bootstrap-controller",
    "/readyz/poststarthook/crd-informer-synced",
    "/readyz/poststarthook/generic-apiserver-start-informers",
    "/readyz/poststarthook/kube-apiserver-autoregistration",
    "/readyz/poststarthook/priority-and-fairness-config-consumer",
    "/readyz/poststarthook/priority-and-fairness-config-producer",
    "/readyz/poststarthook/priority-and-fairness-filter",
    "/readyz/poststarthook/rbac/bootstrap-roles",
    "/readyz/poststarthook/scheduling/bootstrap-system-priority-classes",
    "/readyz/poststarthook/start-apiextensions-controllers",
    "/readyz/poststarthook/start-apiextensions-informers",
    "/readyz/poststarthook/start-apiserver-admission-initializer",
    "/readyz/poststarthook/start-cluster-authentication-info-controller",
    "/readyz/poststarthook/start-kube-aggregator-informers",
    "/readyz/poststarthook/start-kube-apiserver-identity-lease-controller",
    "/readyz/poststarthook/start-kube-apiserver-identity-lease-garbage-collector",
    "/readyz/poststarthook/start-legacy-token-tracking-controller",
    "/readyz/poststarthook/start-service-ip-repair-controllers",
    "/readyz/poststarthook/start-system-namespaces-controller",
    "/readyz/poststarthook/storage-object-count-tracker-hook",
    "/readyz/shutdown",
    "/version"
  ]
}controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl  https://172.30.1.2:6443 --cacert ca --cert crt --key key