# pi-skill-implement-spec

[![Pi Package](https://img.shields.io/badge/pi--package-skill-blue)](https://github.com/IgorGuariroba/pi-skill-implement-spec)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**implement-spec** skill for the **[Pi coding agent](https://pi.dev)**, adapted from Matt Pocock's Engineering Skills.

> Implement a spec and its ticket graph on one integration branch using Pi workers.

---

## Installation

Install directly into Pi using `pi install`:

```bash
pi install git:github.com/IgorGuariroba/pi-skill-implement-spec
```

Or clone into your local/global skills directory:

```bash
# Global Pi skills directory:
git clone https://github.com/IgorGuariroba/pi-skill-implement-spec.git ~/.pi/agent/skills/implement-spec

# Or Agent Skills standard path:
git clone https://github.com/IgorGuariroba/pi-skill-implement-spec.git ~/.agents/skills/implement-spec
```

---

## Usage

Trigger it explicitly in your session:

```text
/skill:implement-spec
```

Or let Pi automatically route to it based on conversation context and need.

---

## Credits

- **Original concept & methodology**: [Matt Pocock](https://github.com/mattpocock)
- **Adapted for Pi Agent**: [Igor Guariroba](https://github.com/IgorGuariroba)

---

## License

[MIT](LICENSE)
