# Contoso Retail

## 1. Document Purpose

This document describes the business and technical context of Contoso Retail.

Its purpose is to provide a stable set of requirements and assumptions for designing an Azure Landing Zone. Architecture decisions should be based on the requirements defined in this document.

Detailed implementation decisions, including management group hierarchy, subscription topology, identity, networking, governance, security, monitoring, and automation, will be documented separately using Architecture Decision Records.

---

## 2. Company Overview

Contoso Retail is a medium-sized retail company operating in several European countries.

The company sells products through:

- Physical retail stores
- A customer-facing e-commerce platform
- Business-to-business sales channels

Contoso Retail employs approximately 500 people. Most employees work in retail operations, logistics, sales, customer support, and corporate functions.

The main company headquarters is located in Poland.

---

## 3. IT Organization

The internal IT department consists of approximately 40 employees.

The technology organization includes:

- Four application development teams
- One platform engineering team
- One security team
- One service desk and workplace technology team
- External technology partners supporting selected systems

### Application Development Teams

Application development teams are responsible for:

- Developing and maintaining business applications
- Deploying application workloads
- Monitoring application health
- Managing application-level configuration
- Resolving application incidents

### Platform Engineering Team

The platform engineering team is responsible for:

- Azure platform architecture
- Cloud governance
- Shared platform services
- Infrastructure as Code
- Deployment pipelines
- Subscription onboarding
- Platform monitoring
- Cost management enablement
- Providing reusable components for development teams

The platform team manages the Azure platform but should not become a deployment bottleneck for application teams.

### Security Team

The security team is responsible for:

- Defining security requirements
- Reviewing platform security controls
- Monitoring the cloud security posture
- Supporting incident response
- Reviewing privileged access
- Providing compliance guidance

Security controls should be automated wherever possible.

---

## 4. Application Portfolio

Contoso Retail operates a mixture of customer-facing and internal applications.

The initial Azure application portfolio contains three representative workloads.

### 4.1 E-Commerce Platform

The e-commerce platform is a customer-facing application used to browse products and place orders.

Characteristics:

- Publicly accessible
- Business-critical
- Handles customer information
- Requires high availability in production
- Integrates with the Order Management API
- Experiences variable traffic
- Requires independent development and production environments

### 4.2 Order Management API

The Order Management API processes customer orders and communicates with internal logistics and inventory systems.

Characteristics:

- Not intended for direct public access
- Business-critical
- Used by the e-commerce platform and internal systems
- Processes transactional business data
- Requires controlled network access
- Requires independent development and production environments

### 4.3 Employee Portal

The Employee Portal provides internal services and information to employees.

Characteristics:

- Available only to authenticated employees
- Integrates with Microsoft Entra ID
- Contains internal company information
- Has lower availability requirements than the e-commerce platform
- Requires independent development and production environments

---

## 5. Azure Adoption Strategy

Contoso Retail has adopted an Azure-first strategy for new applications and platform services.

Existing applications will be evaluated individually before migration. The company does not require every existing system to be immediately moved to Azure.

The Azure environment must support:

- New cloud-native applications
- Migration of selected existing applications
- Shared platform services
- Independent application teams
- Future organizational growth
- Additional Azure subscriptions without redesigning the complete platform

The initial Landing Zone implementation should remain simple while allowing the platform to evolve over time.

---

## 6. Environment Strategy

Application workloads require separation between production and non-production environments.

The initial environment model includes:

- Development
- Test
- Production

Development and test environments may share selected governance and connectivity characteristics.

Production workloads require stronger controls, including:

- More restrictive access
- More restrictive governance policies
- Higher monitoring requirements
- Stronger change control
- Clear separation from non-production resources

The final subscription model will be defined as a separate architecture decision.

---

## 7. Geographic Requirements

Contoso Retail operates primarily within the European Union.

Azure resources should be deployed in approved EU Azure regions unless a documented exception is accepted.

The initial preferred Azure regions are:

- West Europe
- North Europe

The Landing Zone should make it possible to control the locations in which resources can be deployed.

Regional resilience requirements will be determined separately for each workload based on its business criticality.

---

## 8. Identity and Access Requirements

Microsoft Entra ID is the primary identity provider for Azure.

Access to Azure resources must follow these principles:

- Least privilege
- Role-based access control
- Separation of duties
- Group-based role assignments
- Limited use of permanent privileged access
- Traceable administrative actions

Application teams should manage resources within their assigned scope without receiving unnecessary permissions to shared platform services or other application environments.

Production access must be more restrictive than non-production access.

Emergency administrative access must be available through a controlled process.

The detailed RBAC and privileged access models will be designed separately.

---

## 9. Security Requirements

The Azure platform must provide a consistent security baseline for all workloads.

The initial security requirements are:

- Public network access should be minimized.
- Internet exposure must be explicitly justified.
- Data must be encrypted in transit and at rest.
- Privileged access must be controlled and auditable.
- Security-relevant logs must be collected centrally.
- Production and non-production workloads must be separated.
- Workloads must follow an agreed resource configuration baseline.
- Azure security recommendations must be reviewed regularly.
- Security controls should be implemented through automated guardrails where practical.
- Exceptions must be documented and approved.

The company is not currently designing the platform for highly regulated or sovereign workloads.

Workload-specific security requirements may introduce additional controls.

---

## 10. Governance Requirements

Contoso Retail requires centralized Azure governance without preventing development teams from delivering applications.

The governance model must support:

- Consistent policy assignment
- Resource location restrictions
- Required resource metadata
- Resource naming standards
- Control of publicly accessible services
- Central visibility of subscriptions and resources
- Separation of production and non-production workloads
- Documented policy exceptions
- Auditable platform changes

Governance controls should be inherited from higher organizational scopes whenever practical.

The detailed management group and Azure Policy design will be documented separately.

---

## 11. Networking Requirements

The company requires controlled communication between:

- Customer-facing applications
- Internal application components
- Shared Azure services
- Corporate systems
- External services

The networking model should support:

- Centralized connectivity where justified
- Private communication between application components
- Controlled internet ingress and egress
- Private access to selected Azure platform services
- Central DNS capabilities
- Future connectivity to corporate locations
- Isolation between unrelated workloads

The detailed network topology has not yet been selected.

Hub-and-spoke networking and Azure Virtual WAN will be evaluated during the connectivity design stage.

---

## 12. Management and Monitoring Requirements

The platform team requires central visibility across the Azure environment.

The platform must support:

- Central collection of platform and security logs
- Monitoring of shared platform components
- Application monitoring owned by workload teams
- Alerting for critical platform conditions
- Auditability of administrative operations
- Defined log retention
- Integration with security monitoring processes
- Visibility of backup and recovery status

Responsibilities between the platform team and application teams must be clearly documented.

---

## 13. Business Continuity Requirements

Business continuity requirements depend on workload criticality.

The e-commerce platform and Order Management API are considered business-critical workloads.

The Employee Portal is considered an important but non-critical workload.

The platform must allow workload teams to implement:

- Backup
- Restore procedures
- Availability controls
- Regional recovery where justified
- Documented recovery objectives

Recovery Time Objectives and Recovery Point Objectives will be defined separately for each production workload.

The Landing Zone should provide the governance and platform capabilities required to support these workload-level decisions.

---

## 14. Cost Management Requirements

Azure costs must be visible and attributable to an application, environment, or shared platform capability.

The platform must support:

- Subscription-level cost visibility
- Workload ownership identification
- Environment identification
- Budget configuration
- Cost alerts
- Consistent cost-related metadata
- Separation of shared platform costs from application costs

Application teams are responsible for managing the cost efficiency of their workloads.

The platform team is responsible for providing central visibility, standards, and cost management capabilities.

---

## 15. Automation and DevOps Requirements

Azure infrastructure must be managed through Infrastructure as Code wherever practical.

Bicep is the preferred Infrastructure as Code language for this project.

The implementation must support:

- Version-controlled infrastructure
- Repeatable deployments
- Code review through pull requests
- Automated validation
- Deployment preview before changes are applied
- Separate deployment stages
- Traceable platform changes
- Reusable Bicep modules
- Controlled promotion of changes between environments

Manual changes in production should be minimized.

Azure DevOps is the initial CI/CD platform.

The repository should remain understandable for engineers who are learning Azure platform architecture and should avoid unnecessary abstraction.

---

## 16. Platform Engineering Principles

The Azure platform will follow these principles:

### Start Simple

The initial platform will implement only the capabilities required by current business needs.

### Design for Growth

The platform should support additional workloads and subscriptions without requiring a complete redesign.

### Governance Through Code

Management groups, policies, role assignments, and shared platform resources should be managed through version-controlled code wherever practical.

### Secure by Default

New workloads should inherit a defined security and governance baseline.

### Clear Ownership

Every subscription, workload, resource group, and critical resource should have an identifiable owner.

### Team Autonomy Within Guardrails

Application teams should be able to deliver and operate workloads independently within centrally defined boundaries.

### Separate Platform and Workload Responsibilities

The platform team owns the shared Azure foundation. Application teams own their workloads.

### Prefer Evidence-Based Architecture Decisions

Architecture decisions should reference a business, security, operational, or technical requirement.

### Document Exceptions

Exceptions to platform standards must have a documented reason, owner, approval, and review process.

---

## 17. Initial Platform Scope

The first version of the Landing Zone project will cover:

- Repository structure
- Management group hierarchy
- Subscription organization
- Azure Policy baseline
- Platform RBAC model
- Shared connectivity design
- Central management and monitoring design
- Infrastructure as Code deployment model
- CI/CD pipeline structure
- Application Landing Zone onboarding approach

Each area will be designed and implemented incrementally.

---

## 18. Out of Scope

The following items are outside the initial scope:

- Complete production deployment
- Migration of existing applications
- Full disaster recovery implementation
- Multi-cloud management
- Sovereign cloud requirements
- Highly regulated industry compliance
- Detailed application architecture
- Kubernetes platform implementation
- Complex multi-region active-active architecture
- Automated subscription vending in the first iteration
- Full enterprise-scale operating model

These items may be introduced later if justified by new requirements.

---

## 19. Success Criteria

The Landing Zone project will be considered successful when:

- The Azure resource hierarchy is clearly defined.
- Platform and application responsibilities are documented.
- New subscriptions can be placed within the governance hierarchy.
- Baseline policies can be assigned consistently.
- Production and non-production workloads can be separated.
- Platform changes can be deployed through Infrastructure as Code.
- Changes can be reviewed before deployment.
- Logging and cost visibility can be centrally enabled.
- Application teams can operate within defined platform guardrails.
- Architecture decisions are connected to documented requirements.

---

## 20. Assumptions

The initial design is based on the following assumptions:

- Contoso Retail uses a single Microsoft Entra ID tenant.
- Azure is the primary public cloud platform.
- The company operates primarily in the European Union.
- Bicep is used for platform Infrastructure as Code.
- Azure DevOps is used for CI/CD.
- The platform is managed by a central platform engineering team.
- Application teams own the resources deployed within their assigned workload scope.
- The number of Azure workloads and subscriptions will grow over time.
- The company does not currently require a sovereign Landing Zone.
- Architecture decisions may change when new business requirements are introduced.

---

## 21. Next Architecture Decision

The first architecture decision following this document will define the Azure management group hierarchy.

The decision should answer:

- What organizational scopes are required?
- How should platform and application workloads be separated?
- Where should production and non-production subscriptions be placed?
- At which scopes will Azure Policy be assigned?
- At which scopes will RBAC permissions be assigned?
- How will sandbox and decommissioned subscriptions be handled?
- How can the initial hierarchy remain simple while supporting future growth?