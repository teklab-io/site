# Security Working Groups

Managing the relationship between teams and an organisations compliance and security functions can sometimes be inefficient and lead to re-work from late breaking review of application architectures. This can often lead to a tense environment and security being seen as the blocker at the last minute to products going live.

There is a better way. We want to move towards a more continuous cylce of review and design, as our ideas about product and application architecture evolve over the lifecycle of a software delivery project.

A security working group (SWG) is a ritual to provide a structured way for teams to communicate with their security stakeholders and maintain a conversation.

One of the issues in communications is that unless you are extremely lucky or working on something extremely security sensitive, your unlikely to have a security person permanently embedded in your team, attending every standup and involved in every story. Infact, this is a general pattern about managing stakeholders within teams.

## Terms of Reference

## Purpose

To review and guide a project from the perspective of security accreditation and assurance. The goal is to minimise "check points" and reviews before products become live by introducing a more continuous cycle of assurance.

## Attendees

**Mandatory**

i.e. meeting cannot proceed without these:

- Chair / Minute taker (Usually someone from PMO or who represents broader governance)
- Delivery Lead (Project Manager, Scrum Master or Delivery Manager)
- Technical Lead
- Risk officer (representing SIRO - Senior Information Risk Officer)
- Technical security expert

The important point about this composition is that it has a quorum of the people who can actually make decisions. If someone can't attend they can delegate. People may need to take decisions externally for validation.

It is vital that the rest of the organisation accepts the representation in this core group, to avoid re-visiting decisions in the future.

**Optional**

- Product owner
- Relevant SME's
- Group / Programme architects


## Agenda

- Action review
- Tabled topics for discussion
- Review of upcoming work - are there security significant changes
- Recording of decisions
- Closing, assigning actions, notification of next meeting

## Security significant change

If teams are building out new product, inevitably there will be an initial period in which many things are changing, as the team explores the shape of the system they are building. Often it is difficult to keep track of these changes.

One technique we can use is to present review upcoming changes at SWG to see if people believe they are significant enough to trigger further investigation.

Areas of change that could be triggers are:

- Changes to network topology
- Addition or removal of data entities / attributes
- Additional components
- New technologies or tools
- New personas interacting with the system
- Significant product updates
- Changes that result in new legal classifications / obligations
- Changes in scale of use (e.g. moving from 10 users to 1000 or 10 data records to 1M)

These changes can be represented by versioning diagrams as described in the artifacts section.

## Artifacts

- Product roadmap
  - What are the planned features upcoming
- List of significant planned changes to the architecture / deployment, assesed for wether they are important or not
- Technical diagrams:
  - Security context diagram (what is in or out of scope for this meeting), including for example illustrating that the security of underlying infra such as VMWare is out of scope / covered in another context.
  - Application context diagram (for a particular scope / project, what is a high level description of its function and who uses it)
  - Component interaction diagram (what are the high level component parts of the system, and what information is flowing between them
  - Network Topology diagram - detailed map of servers, port numbers, protocols. Can be annonymised for a particular environment (i.e. don't need actual IP addresses). Must include all network appliances from external boundary to storage.
  - Data domain model - what entities are represented in the scope for consideration

- Data confidentiality classification
  - For each Data entity, or attribute, classify sensitivity

- Attack tree analysis
  - What are the key threats, mitigations, if different from common corporate context, if not can refer to a general corporate threat model

- Output from any penetration tests or automated testing / audits
- Dependency information of software component libraries
- Lists of technology and wethere patching is current or not? perhaps list version in use, latest version and highlight differences.
- Output from OWASP dependency check (https://www.owasp.org/index.php/OWASP_Dependency_Check)
- OWASP checklist - for each OWASP item, have a RAG status as to wether the team feel they have this covered, or actions to green.

