# VM Prerequisites and Add-Ons

When setting up VMs (e.g., via GUI options), select these groups for Oracle compatibility:

- **Development Tools**: Includes compilers (gcc, g++), make, and other tools needed for building and installing Oracle software dependencies.
- **Security Tools**: For firewall and security management.
- **Performance Tools**: For system tuning and monitoring.
- **System Administration Tools**: Provides utilities like system-config-* for network, firewall, and user management, simplifying VM configuration.
- **Compatibility Libraries**: Ensures support for legacy libraries (e.g., compat-libcap1, libaio) required by Oracle 19c, addressing compatibility issues.

Install via: `yum groupinstall "Development Tools" "Security Tools" "Performance Tools" "System Administration Tools" "Compatibility Libraries"`.
