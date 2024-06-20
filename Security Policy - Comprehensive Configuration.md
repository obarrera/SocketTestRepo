# Security Policy - Comprehensive Configuration

#### Block 🚫

| Alert                          | Alert Info                                                                                             | Category          | Severity |
|--------------------------------|-------------------------------------------------------------------------------------------------------|-------------------|----------|
| Known malware                  | This package is malware. We have asked the package registry to remove it.                              | Supply chain risk | Critical |
| Protestware or potentially unwanted behavior | This package is a joke, parody, or includes undocumented or hidden behavior unrelated to its primary function. | Supply chain risk | High     |
| AI detected potential malware  | AI has identified this package as malware. This is a strong signal that the package may be malicious.  | Supply chain risk | High     |
| Potential Typo Squat           | Package name is similar to other popular packages and may not be the package you want.                | Supply chain risk | Critical |
| Obfuscated code                | Obfuscated files are intentionally packed to hide their behavior. This could be a sign of malware.    | Supply chain risk | High     |
| Shell access                   | This module accesses the system shell. Accessing the system shell increases the risk of executing arbitrary code. | Supply chain risk | Critical |
| Network access                 | This module accesses the network.                                                                     | Supply chain risk | High     |
| Native code                    | Contains native code which could be a vector to obscure malicious code, and generally decrease the likelihood of reproducible or reliable installs. | Supply chain risk | High     |

#### Warn ⚠️

| Alert                        | Alert Info                                                                                                                                                                                                 | Category          | Severity |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------|
| Bin Script Shell Injection   | This package re-exports a well-known shell command via an npm bin script. This is possibly a supply chain risk.                                                                                            | Supply chain risk | High     |
| HTTP dependency              | Contains a dependency which resolves to a remote HTTP URL which could be used to inject untrusted code and reduce overall package reliability.                                                             | Supply chain risk | Critical |
| Git dependency               | Contains a dependency which resolves to a GitHub URL. Dependencies fetched from GitHub specifiers are not immutable and can be used to inject untrusted code or reduce the likelihood of a reproducible install. | Supply chain risk | Critical |
| Telemetry                    | This package contains telemetry which tracks how it is used.                                                                                                                                               | Supply chain risk | High     |
| AI detected security risk    | AI has determined that this package may contain potential security issues or vulnerabilities.                                                                                                              | Supply chain risk | High     |
| High entropy strings         | Contains high entropy strings. This could be a sign of encrypted data, leaked secrets, or obfuscated code.                                                                                                  | Supply chain risk | Medium   |
| New author                   | A new npm collaborator published a version of the package for the first time. New collaborators are usually benign additions to a project, but do indicate a change to the security surface area of a package. | Supply chain risk | Medium   |
| Unstable ownership           | A new collaborator has begun publishing package versions. Package stability and security risk may be elevated.                                                                                             | Supply chain risk | Medium   |

#### Monitor 👁️

| Alert                     | Alert Info                                                                                                           | Category      | Severity |
|---------------------------|---------------------------------------------------------------------------------------------------------------------|---------------|----------|
| Critical CVE              | Contains a Critical Common Vulnerability and Exposure (CVE).                                                         | Vulnerability | Critical |
| High CVE                  | Contains a high severity Common Vulnerability and Exposure (CVE).                                                    | Vulnerability | High     |
| Medium CVE                | Contains a medium severity Common Vulnerability and Exposure (CVE).                                                  | Vulnerability | Medium   |
| Low CVE                   | Contains a low severity Common Vulnerability and Exposure (CVE).                                                     | Vulnerability | Low      |
| Non-existent author       | The package was published by an npm account that no longer exists.                                                   | Supply chain risk | Medium   |
| Unresolved Require        | Package imports a file which does not exist and may not work as is. It could also be importing a file that will be created at runtime which could be a vector for running malicious code. | Quality       | Critical |
| Environment variable access | Package accesses environment variables, which may be a sign of credential stuffing or data theft.                   | Supply chain risk | High     |
| Dynamic require           | Dynamic require can indicate the package is performing dangerous or unsafe dynamic code execution.                   | Supply chain risk | High     |

#### Ignore ❌

| Alert                      | Alert Info                                                                                               | Category          | Severity |
|----------------------------|-----------------------------------------------------------------------------------------------------------|-------------------|----------|
| Install scripts            | Install scripts are run when the package is installed. The majority of malware in npm is hidden in install scripts. | Supply chain risk | High     |
| Deprecated license         | License is deprecated which may have legal implications regarding the package's use.                      | Legal risk        | Medium   |
| Unpopular package          | This package is not very popular.                                                                         | Supply chain risk | Low      |
| Trivial Package            | Packages less than 10 lines of code are easily copied into your own project.                              | Quality risk      | Low      |
| Minified code              | This package contains minified code. While sometimes harmless, it may hide malicious content.             | Quality risk      | Low      |
| Uses eval                  | Package uses eval() which is a dangerous function and increases the risk that the code may contain exploits or malicious behavior. | Supply chain risk | Medium   |
| Deprecated SPDX exception  | Contains a known deprecated SPDX license exception.                                                       | Legal risk        | Low      |
| Ambiguous License Classifier | An ambiguous license classifier was found.                                                              | Legal risk        | Low      |

#### Ignore (TBD)

| Alert                | Alert Info                                                                                       | Category          | Severity |
|----------------------|---------------------------------------------------------------------------------------------------|-------------------|----------|
| Floating dependency  | Package has a dependency with a floating version range. This can cause issues if the dependency publishes a new major version. | Quality risk | Medium   |
| Manifest confusion   | This package has inconsistent metadata. This could be malicious or caused by an error when publishing the package. | Quality risk | Medium   |

---

