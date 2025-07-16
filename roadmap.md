# OpenNyx Project Roadmap
This roadmap outlines the key phases of development to realize our vision of a fully encrypted, portable, and self-destructing operating system. This roadmap is dynamic and will be adjusted as we make progress, identify new challenges, or receive valuable community feedback.
Our Vision: OpenNyx is your idea of a fully encrypted, portable, and self-destructing operating system. It is designed for ultimate privacy and digital freedom.
## Phase 0: Conception & Initialization (Current)
 * Goals:
   * Refine the core concepts and principles of OpenNyx.
   * Establish the foundational project infrastructure.
   * Recruit initial core members and build an early community.
 * Key Steps:
   * Detailed Specification: Elaborate a comprehensive document outlining OpenNyx's architecture, core functionalities, and security requirements.
   * Technology Stack Evaluation: Research and select suitable base technologies (e.g., Linux kernel derivative, bootloader, encryption libraries, programming languages).
   * Community Building: Launch the Discord server, establish social media presence (e.g., Reddit post) to attract contributors and interested parties.
   * Open-Source Infrastructure: Set up a Git repository (GitHub/GitLab), a basic build system, and a documentation platform.
   * Governance & Licensing: Define project governance and choose an appropriate open-source license.
## Phase 1: Proof of Concept (PoC) & Kernel Foundations
 * Goals:
   * Demonstrate the feasibility of core principles (RAM operation, basic encryption, rudimentary self-destruction).
   * Build a minimal, bootable kernel.
 * Key Steps:
   * Minimal Bootloader: Develop or adapt a bootloader that loads a highly stripped-down kernel into RAM.
   * Kernel Stub: Develop a basic kernel stub that loads into RAM and allows for simple console output.
   * RAM-Disk Implementation: Initial experiments with a RAM-disk as the filesystem for the live system (e.g., tmpfs or ramfs with overlayfs).
   * Basic Crypto Integration (PoC): Implement a very rudimentary, non-production-ready encryption of the RAM image and/or temporary data.
   * Self-Destruction (PoC): Implement a simple mechanism for overwriting RAM upon shutdown.
   * Basic Build System: Automate the compilation and creation process of the bootable image.
## Phase 2: Functional Prototype & Security Architecture
 * Goals:
   * Expand the kernel with fundamental system functionalities.
   * Implement a robust and secure encryption architecture.
   * Establish a reliable self-destruction mechanism.
 * Key Steps:
   * Kernel Expansion: Implement memory management, process scheduler, and device driver framework (for essential hardware).
   * Cryptographic Subsystem: Full implementation of FIPS-validated cryptographic libraries and secure key management.
     * Algorithm Choice: AES-256 (GCM mode) for symmetric data encryption, as it is strong, fast, and widely adopted, providing authenticated encryption. For key derivation, Argon2id or Scrypt. For hashing, SHA-3 (512).
     * Implementation: Utilize hardware acceleration (AES-NI) where available.
     * Key Management: Derive temporary session keys exclusively in RAM, based on a passphrase or hardware token.
   * On-the-fly Encryption: Ensure all data generated during runtime is encrypted. Integration into the filesystem and swap space (if present, ideally not).
   * Secure Boot Integration: Research and implement secure boot concepts to ensure the integrity of the loaded system (e.g., Verified Boot, Trusted Platform Module (TPM) integration for integrity measurements and key sealing).
   * Robust Self-Destruction ("Nuke" Function):
     * RAM-Wiping: Multiple passes of random data overwrites across all accessible RAM segments (e.g., following principles similar to DoD 5220.22-M or Gutmann method for maximum security, though fewer cycles may suffice for RAM). This will be initiated by the kernel.
     * Trigger Mechanisms:
       * Manual: Specific command or physical button (if hardware integration is possible).
       * Automatic Shutdown: During normal system shutdown.
       * Emergency Triggers: Removal of the USB stick, inactivity beyond a defined time, multiple incorrect passcode entries, geofencing (optional, complex).
       * Alarm Password: A special password that, instead of granting access, triggers the "Nuke" function.
     * No Persistent Storage: Systematic verification that no data is written to any permanent storage media.
   * Input/Output: Basic support for keyboard, mouse, and display/console.
   * Network Fundamentals: Implementation of a minimal network stack.
## Phase 3: Advanced Features & Stabilität
 * Goals:
   * Implement advanced features and improve user experience.
   * Focus on stability, performance, and comprehensive testing.
 * Key Steps:
   * Filesystem Enhancements: Optimize the RAM filesystem and integrate overlay filesystems for temporary, non-persistent changes (e.g., aufs or overlayfs).
   * Anonymization Integration: Optional integration of network anonymization services (e.g., Tor, I2P) at the system level.
   * Lightweight UI (Optional): Development or integration of a very lean graphical user interface (e.g., based on Wayland/Xorg with a minimalist window manager like i3wm, Openbox, or dwm).
     * Design Consideration:
       * Aesthetics: Functional, minimalist, dark-themed (privacy-oriented, eye-friendly). No flashy animations or unnecessary graphics.
       * Usability: Intuitive navigation with clear visual indicators for encryption status and active "Nuke" triggers.
       * Key Elements: Status bar with network and encryption status, quickly accessible "Nuke" option (visually subtle but easily reachable), simple application icons.
       * Color Scheme: Few, high-contrast colors. Primarily dark greys and blacks with high-contrast accents: Green (Secure/Active), Red (Warning/Nuke Trigger), Blue (Informational).
       * Fonts: Monospace fonts for clarity and code aesthetics.
   * Hardware Compatibility: Expand driver support for a wider range of hardware, especially USB controllers and network adapters.
   * Comprehensive Testing: Intensive unit, integration, and system tests. Launch a bug bounty program (if resources allow).
   * Dokumentation: Create comprehensive user and developer documentation.
## Phase 4: Initial Release & Community Growth
 * Goals:
   * Release the first stable version of OpenNyx.
   * Expand the user base and contributor network.
 * Key Steps:
   * Release 1.0: Official public release of the first stable version.
   * Bugfixing & Patches: Continuous maintenance and bug resolution.
   * Community Feedback: Actively solicit and integrate feedback from the community.
   * Marketing & Outreach: Intensified promotion of the project to attract more users and developers.
