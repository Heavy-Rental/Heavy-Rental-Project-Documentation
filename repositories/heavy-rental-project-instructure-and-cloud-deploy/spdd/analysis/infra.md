# Analysis — Academy infra

Vocareum caps EC2 (~9). Eight ASG instances + zero NAT EC2 fits. Neo4j is HA via NLB, not a causal cluster. NAT Gateways bill until destroy; `stop` does not pause them.
