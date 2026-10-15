
Version: NAFATH-V4

Track: AI

# Overview
A national service provider depends on software, AI models, mobile applications, and internet routing, so weaknesses in any part of its supply chain can threaten the whole service. The Twelve-Factor App approach keeps configuration separate from source code, reducing the risk of exposing credentials. Mobile security standards help teams test applications before release, while networking protections such as RPKI reduce certain types of false BGP route announcements. Vulnerability management is also essential, as demonstrated by the Log4Shell vulnerability in Apache Log4j. A Software Bill of Materials (SBOM) improves visibility by listing software components and their dependencies, helping teams identify potentially affected systems when new vulnerabilities emerge. These controls work together to strengthen security, improve incident response, and reduce supply chain risks. For the AI track, understanding adversarial machine learning attacks, especially evasion and poisoning, is essential to protecting models and the data used to train them.
# Software
The Twelve Factor App methodology says deployment-specific configuration should be stored in environment variables rather than hard-coded into source code. This includes service credentials, database connection details, and values that change between staging and production. Separating configuration from code lets teams change deployment settings without modifying the application and reduces the risk of committing credentials to version control. Secrets still need access controls and secure management; environment variables alone do not replace a secrets-management process.

Resource: The Twelve-Factor App — III. Config - https://12factor.net/config
# AI
Adversarial machine-learning attacks can target different stages and goals. Evasion attacks manipulate inputs at inference time to make a trained model produce an incorrect result. Poisoning attacks manipulate training data or model updates so the model learns undesirable behavior. Other categories include privacy attacks, which seek to infer sensitive information, and trojan or backdoor attacks, which cause specific behavior under chosen conditions. Because attacks differ, defenses should match the threat model and cover the AI lifecycle, not only live predictions.

Resource: NIST AI 100-2 E2023, Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://csrc.nist.gov/pubs/ai/100/2/e2023/final
# Mobile
The OWASP Mobile Application Security Verification Standard (MASVS) defines security requirements for mobile apps. It covers secure storage, cryptography, authentication, network communication, platform interaction, code quality, resilience, and privacy. Teams use MASVS requirements as a checklist and test apps using suitable methods, including the Mobile Application Security Testing Guide (MASTG). MASVS supports structured security verification but does not automatically certify an app as secure.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/
# Networking
BGP route hijacking occurs when a network announces a route that attracts traffic intended for another network, redirecting, intercepting, or blackholing it. Resource Public Key Infrastructure (RPKI) supports Route Origin Validation: networks check whether an IP prefix and originating autonomous system are authorized by a Route Origin Authorization. This helps reject invalid origin announcements. However, RPKI does not verify the full AS path, prevent every route leak, or encrypt traffic, so other routing safeguards are still needed.

Resource: RFC 6811 — BGP Prefix Origin Validation - https://www.rfc-editor.org/rfc/rfc6811
# Cybersecurity
Log4Shell (CVE-2021-44228) was a critical remote code execution flaw in Apache Log4j 2. In vulnerable configurations, attacker-controlled text logged by an application could trigger a JNDI lookup and potentially execute code remotely. It was severe because Log4j was widely used in Java applications and exploitation could expose systems to major compromise. The main fix was upgrading to a fixed Log4j release, then checking applications and bundled dependencies for vulnerable copies and investigating possible exploitation.

Resource: Apache Logging Services Security - https://logging.apache.org/security.html
# Data
A Software Bill of Materials (SBOM) is a machine readable inventory of a product’s software components and their relationships. It helps teams identify applications affected by a newly disclosed dependency vulnerability. Minimum useful fields include supplier, component name, version, other unique identifiers, dependency relationships, SBOM author, and timestamp. Teams should maintain an SBOM for each release. It improves visibility and response speed, but does not prove that components are safe or vulnerability free.

Resource: CycloneDX Specification Overview - https://cyclonedx.org/specification/overview/
# Misconception in My Track
A common misconception in AI security is that adversarial attacks only happen when someone changes an input to trick a model into making a wrong prediction. In reality, attacks can also happen before a model is deployed. For example, poisoning attacks involve changing training data so the model learns incorrect or harmful patterns. These attacks require different defenses from evasion attacks, which target a model while it is being used. Therefore, AI teams should check training data carefully and test models against manipulated inputs. NIST explains these attack types in sections “2.2. Evasion Attacks and Mitigations” and “2.3. Poisoning Attacks and Mitigations” of its AI 100-2 E2023 publication.
# Open Question
Which dataset-integrity, model-provenance, and adversarial-testing controls should be required before a national digital service accepts a third party AI model?
