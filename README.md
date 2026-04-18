# Azure Firewall Policy Optimizer

A web-based tool to analyze and optimize Azure Firewall Policy rules from ARM template JSON.  
Merge similar rules, reduce redundancy, and simplify your Azure Firewall configurations.

![Screenshot](https://github.com/nguyenviettung7691/azure-firewall-policy-optimizer/assets/39761347/b96fb65d-0ad1-4d1c-b655-250eb06ec660)

<img width="1628" height="1209" alt="image" src="https://github.com/user-attachments/assets/ec04ef19-1e1c-4a20-a36a-09a92b10866d" />

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

### Expected ARM template format:

```json
{
  "parameters": {
    "ruleCollectionGroups": {
      "value": [
        {
          "name": "rcg-prod-eastus",
          "properties": {
            "priority": 100,
            "ruleCollections": [
              {
                "name": "rc-net-allow-core",
                "ruleCollectionType": "FirewallPolicyFilterRuleCollection",
                "priority": 100,
                "action": {
                  "type": "Allow"
                },
                "rules": [
                  {
                    "name": "net-web-443-from-app1",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.10.1.0/24"
                    ],
                    "destinationAddresses": [
                      "20.30.40.10"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-web-443-from-app2",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.10.2.0/24"
                    ],
                    "destinationAddresses": [
                      "20.30.40.10"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-web-443-from-app3",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.10.3.0/24"
                    ],
                    "destinationAddresses": [
                      "20.30.40.10"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-db-multiport-same-source-a",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.20.1.0/24"
                    ],
                    "destinationAddresses": [
                      "172.16.10.5"
                    ],
                    "destinationPorts": [
                      "1433"
                    ]
                  },
                  {
                    "name": "net-db-multiport-same-source-b",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.20.1.0/24"
                    ],
                    "destinationAddresses": [
                      "172.16.10.5"
                    ],
                    "destinationPorts": [
                      "1434"
                    ]
                  },
                  {
                    "name": "net-backup-fqdn-a",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.30.1.0/24"
                    ],
                    "destinationFqdns": [
                      "backup.contoso.net"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-backup-fqdn-b",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.30.2.0/24"
                    ],
                    "destinationFqdns": [
                      "backup.contoso.net"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-no-merge-different-dest",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.10.4.0/24"
                    ],
                    "destinationAddresses": [
                      "20.30.40.11"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  }
                ]
              },
              {
                "name": "rc-nat-publish-core",
                "ruleCollectionType": "FirewallPolicyNatRuleCollection",
                "priority": 200,
                "action": {
                  "type": "Dnat"
                },
                "rules": [
                  {
                    "name": "nat-rdp-host1",
                    "ruleType": "NatRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      ""
                    ],
                    "destinationAddresses": [
                      "52.160.10.10"
                    ],
                    "destinationPorts": [
                      "50001"
                    ],
                    "translatedAddress": "10.0.10.4",
                    "translatedPort": "3389"
                  },
                  {
                    "name": "nat-rdp-host2",
                    "ruleType": "NatRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      ""
                    ],
                    "destinationAddresses": [
                      "52.160.10.10"
                    ],
                    "destinationPorts": [
                      "50002"
                    ],
                    "translatedAddress": "10.0.10.4",
                    "translatedPort": "3389"
                  },
                  {
                    "name": "nat-rdp-host3",
                    "ruleType": "NatRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      ""
                    ],
                    "destinationAddresses": [
                      "52.160.10.10"
                    ],
                    "destinationPorts": [
                      "50003"
                    ],
                    "translatedAddress": "10.0.10.4",
                    "translatedPort": "3389"
                  },
                  {
                    "name": "nat-no-merge-different-translated-port",
                    "ruleType": "NatRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      ""
                    ],
                    "destinationAddresses": [
                      "52.160.10.10"
                    ],
                    "destinationPorts": [
                      "50004"
                    ],
                    "translatedAddress": "10.0.10.4",
                    "translatedPort": "3390"
                  }
                ]
              },
              {
                "name": "rc-app-web-egress",
                "ruleCollectionType": "FirewallPolicyFilterRuleCollection",
                "priority": 300,
                "action": {
                  "type": "Allow"
                },
                "rules": [
                  {
                    "name": "app-msft-login-team-a",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.40.1.0/24"
                    ],
                    "targetFqdns": [
                      "login.microsoftonline.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  },
                  {
                    "name": "app-msft-login-team-b",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.40.2.0/24"
                    ],
                    "targetFqdns": [
                      "login.microsoftonline.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  },
                  {
                    "name": "app-msft-login-team-c",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.40.3.0/24"
                    ],
                    "targetFqdns": [
                      "login.microsoftonline.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  },
                  {
                    "name": "app-github-http-https-a",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.50.1.0/24"
                    ],
                    "targetFqdns": [
                      "api.github.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Http",
                        "port": 80
                      },
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  },
                  {
                    "name": "app-github-http-https-b",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.50.1.0/24"
                    ],
                    "targetFqdns": [
                      "api.github.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      },
                      {
                        "protocolType": "Http",
                        "port": 80
                      }
                    ]
                  },
                  {
                    "name": "app-no-merge-different-protocol",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.40.4.0/24"
                    ],
                    "targetFqdns": [
                      "login.microsoftonline.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Http",
                        "port": 80
                      }
                    ]
                  }
                ]
              }
            ]
          }
        },
        {
          "name": "rcg-prod-westus",
          "properties": {
            "priority": 110,
            "ruleCollections": [
              {
                "name": "rc-net-allow-secondary",
                "ruleCollectionType": "FirewallPolicyFilterRuleCollection",
                "priority": 100,
                "action": {
                  "type": "Allow"
                },
                "rules": [
                  {
                    "name": "net-cross-collection-part-1",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.60.1.0/24"
                    ],
                    "destinationAddresses": [
                      "203.0.113.50"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-cross-collection-part-2",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.60.2.0/24"
                    ],
                    "destinationAddresses": [
                      "203.0.113.50"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  }
                ]
              },
              {
                "name": "rc-net-allow-secondary-2",
                "ruleCollectionType": "FirewallPolicyFilterRuleCollection",
                "priority": 101,
                "action": {
                  "type": "Allow"
                },
                "rules": [
                  {
                    "name": "net-cross-collection-part-3",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.60.3.0/24"
                    ],
                    "destinationAddresses": [
                      "203.0.113.50"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  },
                  {
                    "name": "net-cross-collection-part-4",
                    "ruleType": "NetworkRule",
                    "ipProtocols": [
                      "TCP"
                    ],
                    "sourceAddresses": [
                      "10.60.4.0/24"
                    ],
                    "destinationAddresses": [
                      "203.0.113.50"
                    ],
                    "destinationPorts": [
                      "443"
                    ]
                  }
                ]
              },
              {
                "name": "rc-app-ops-egress",
                "ruleCollectionType": "FirewallPolicyFilterRuleCollection",
                "priority": 300,
                "action": {
                  "type": "Allow"
                },
                "rules": [
                  {
                    "name": "app-monitoring-a",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.70.1.0/24"
                    ],
                    "targetFqdns": [
                      "ingest.monitor.azure.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  },
                  {
                    "name": "app-monitoring-b",
                    "ruleType": "ApplicationRule",
                    "sourceAddresses": [
                      "10.70.2.0/24"
                    ],
                    "targetFqdns": [
                      "ingest.monitor.azure.com"
                    ],
                    "protocols": [
                      {
                        "protocolType": "Https",
                        "port": 443
                      }
                    ]
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }
}
```

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
