# Azure Firewall Policy Optimizer

A web-based tool to analyze and optimize Azure Firewall Policy rules from ARM template JSON.  
Merge similar rules, reduce redundancy, and simplify your Azure Firewall configurations.

![Screenshot](https://github.com/nguyenviettung7691/azure-firewall-policy-optimizer/assets/39761347/b96fb65d-0ad1-4d1c-b655-250eb06ec660)

## Features

- **Paste or edit** your Azure Firewall Policy ARM template JSON.
- **Analyze** rules for optimization opportunities.
- **Preview** how rules can be merged.
- **One-click optimization**: Merge rules and update your JSON.
- Supports **NetworkRule**, **NatRule**, and **ApplicationRule** collections.
- Visual JSON rendering with [rainbowJSON](rainbowJSON/README.md).

## Usage

1. Open `index.html` in your browser.
2. Paste your Azure Firewall Policy ARM template JSON into the input box.
3. Select the optimize type (Subnet or FQDN) and direction (Target or Source).
4. Click **Analyze**.
5. Review the suggested optimizations and preview merged rules.
6. Click **Optimize** to merge rules and update your JSON.

## Requirements

- Modern web browser (no backend required).
- Internet connection (for CDN dependencies: jQuery, Bootstrap, Bootstrap Icons).

## How it works

- The tool groups rules by common source/destination addresses or FQDNs.
- Rules with matching properties (e.g., ports, protocols) are eligible for merging.
- Merged rules are added to the top of the rule collection.
- The tool uses [rainbowJSON](rainbowJSON/README.md) for pretty-printing and folding JSON.

## Development

- All logic is in [`index.html`](index.html).
- JSON rendering uses [`rainbowJSON`](rainbowJSON/).
- No build step required.

## License

MIT License. See [LICENSE](LICENSE).

---

Created by Nguyễn Việt Tùng (Harry)