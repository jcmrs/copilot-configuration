# Platform Protocols & Constraints for copilot-configuration

## Purpose

This document enumerates the platform, environmental, and infrastructure constraints that impact autonomous and human maintainers in the copilot-configuration repository. It is referenced by all roles and expertises, and must be reviewed and updated as project context evolves.

---

## 1. Platform Constraints

### 1.1. GitHub Actions & CI/CD

- **Firewall Rules:** Outbound DNS and packet connections (e.g., to telemetry.nextjs.org) may be blocked by default.  
  - Impact: Build, lint, and telemetry steps may stall or fail.
  - Mitigation:  
    - Disable unnecessary telemetry (e.g., `NEXT_TELEMETRY_DISABLED=1` for Next.js).
    - Escalate allowlist requests for critical domains.
    - Document all block events in workflow logs and artifacts.

- **Artifact Retention:** Logs and artifacts are purged after 90 days.
  - Impact: Long-term troubleshooting must use in-repo documentation.

- **Job Environment:** No persistent state between jobs except via artifacts or cache actions.
  - Impact: Onboarding and reliability steps must be self-contained.

### 1.2. Repository Permissions

- **Branch Protections:** Autonomous actions may be limited by protected branch rules.
  - Impact: Pull request workflows may require human review or approval.

- **Secrets & Security:** No direct access to repository secrets in workflows; must use approved Actions or escalation.

### 1.3. Network & Telemetry

- **Telemetry Blocking:** Domains not in allowlist (e.g., telemetry.nextjs.org) are blocked.
  - Impact: Next.js and other tools may attempt telemetry and fail.
  - Mitigation:  
    - Always disable telemetry for CI builds.
    - Document and escalate when necessary.

- **IP Restrictions:** Outbound packets to certain IPs (e.g., WALinuxAgent) are blocked or redirected.
  - Impact: System-level logging or reporting may fail.

---

## 2. Cross-Role Impact

All constraints above affect every autonomous role and expertise, including:

- **Project Owner:** Must ensure repo reliability and document platform boundaries.
- **Project Manager:** Coordinates mitigation, onboarding, and reporting protocols.
- **Lead Developer:** Designs workflows to function under platform constraints.
- **Prompt Designer:** Crafts onboarding prompts that reference platform context.
- **AI Specialist:** Sets operational boundaries and escalation paths aligned with platform rules.
- **DevOps, Systems Architect, GitHub Specialist, Next.js Specialist, etc.:** Must actively diagnose, document, and propose adaptations for platform conditions.

---

## 3. Adaptation Protocol

- **Document platform constraints in onboarding and lessons-learned files.**
- **Escalate platform-related failures or blocks in commit messages and session logs.**
- **Propose workflow changes or mitigation steps when encountering new platform conditions.**
- **Update this document as platform environment evolves.**

---

## 4. References

- [GitHub Actions Setup Steps](https://gh.io/copilot/actions-setup-steps)
- [Copilot Firewall Configuration](https://gh.io/copilot/firewall-config)
- [Next.js Telemetry Documentation](https://nextjs.org/telemetry)

---

_Last updated: 2025-09-02_