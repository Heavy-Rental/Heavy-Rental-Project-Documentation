# ADR 0003: Two NAT Gateways

- Status: accepted
- Date: 2026-08-21

## Decision
One NAT Gateway + EIP per public AZ. Same-AZ outbound for app and data guests. Not a NAT instance.

## Consequences
AZ failure keeps egress; NAT bills until `destroy`.
