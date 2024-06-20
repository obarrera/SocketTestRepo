# Security Policy - Suggested Configuration

#### Block 🚫

| Alert                          | Alert Info                                                                                             | Category          | Severity |
|--------------------------------|-------------------------------------------------------------------------------------------------------|-------------------|----------|
| Known malware                  | This package is malware. We have asked the package registry to remove it.                              | Supply chain risk | Critical |
| Protestware or potentially unwanted behavior | This package is a joke, parody, or includes undocumented or hidden behavior unrelated to its primary function. | Supply chain risk | High     |
| AI detected potential malware  | AI has identified this package as malware. This is a strong signal that the package may be malicious.  | Supply chain risk | High     |
| Potential Typo Squat           | Package name is similar to other popular packages and may not be the package you want.                | Supply chain risk | Critical |

#### Warn ⚠️

| Alert                        | Alert Info                                                                                                                                                                                                 | Category          | Severity |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------|
| Bin Script Shell Injection   | This package re-exports a well-known shell command via an npm bin script. This is possibly a supply chain risk.                                                                                            | Supply chain risk | High     |
| HTTP dependency              | Contains a dependency which resolves to a remote HTTP URL which could be used to inject untrusted code and reduce overall package reliability.                                                             | Supply chain risk | Critical |
| Git dependency               | Contains a dependency which resolves to a GitHub URL. Dependencies fetched from GitHub specifiers are not immutable and can be used to inject untrusted code or reduce the likelihood of a reproducible install. | Supply chain risk | Critical |
| Telemetry                    | This package contains telemetry which tracks how it is used.                                                                                                                                               | Supply chain risk | High     |

#### Monitor 👁️

| Alert              | Alert Info                                                                                             | Category      | Severity |
|--------------------|-------------------------------------------------------------------------------------------------------|---------------|----------|
| Critical CVE       | Contains a Critical Common Vulnerability and Exposure (CVE).                                          | Vulnerability | Critical |
| High CVE           | Contains a high severity Common Vulnerability and Exposure (CVE).                                     | Vulnerability | High     |
| Unresolved Require | Package imports a file which does not exist and may not work as is. It could also be importing a file that will be created at runtime which could be a vector for running malicious code. | Quality       | Critical |

#### Ignore ❌

| Alert             | Alert Info                                                                                               | Category          | Severity |
|-------------------|-----------------------------------------------------------------------------------------------------------|-------------------|----------|
| Install scripts   | Install scripts are run when the package is installed. The majority of malware in npm is hidden in install scripts. | Supply chain risk | High     |

---
