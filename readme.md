# PART 1 
  # VPC Creation
  The VPCs are designed using custom-mode networking with Global dynamic routing to support secure segmentation, future scalability, and enterprise-grade hybrid networking patterns. Standard best path selection was chosen for modern BGP-compliant route handling. IPv6 and DNS Armor were intentionally disabled to reduce unnecessary operational complexity for the current scope while maintaining a secure and production-aligned fintech architecture.
    app-subnet : 10.10.1.0/24
    shared-subnet: 10.100.1.0/24
  
  ## Create app-vpc and app-subnet
  
    gcloud compute networks create app-vpc --project=quiet-rigging-490521-d6 --subnet-mode=custom --bgp-routing-mode=global --bgp-best-path-selection-mode=standard --bgp-bps-inter-region-cost=default
    gcloud compute networks subnets create app-vpc --project=quiet-rigging-490521-d6 --range=10.10.1.0/24 --stack-type=IPV4_ONLY --network=app-vpc --region=us-central1 --enable-private-ip-google-access
  
  
  ## Create shared-vpc and shared-subnet
  
    gcloud compute networks create shared-vpc --project=quiet-rigging-490521-d6 --subnet-mode=custom --bgp-routing-mode=global --bgp-best-path-selection-mode=standard --bgp-bps-inter-region-cost=default
    gcloud compute networks subnets create shared-subnet --project=quiet-rigging-490521-d6 --range=10.100.1.0/24 --stack-type=IPV4_ONLY --network=shared-vpc --region=us-central1 --enable-private-ip-google-access

  ## VPC Peering
  VPC peering was configured using IPv4 single-stack networking with custom route exchange enabled to support scalable private communication between isolated application and shared services networks. Public private-route exchange was disabled because the architecture uses standard RFC1918 private addressing. Independent update strategy was selected for operational simplicity and flexible network administration
  app-vpc to shared-vpc
  <img width="1104" height="718" alt="Screenshot 2026-05-17 at 11 01 58 PM" src="https://github.com/user-attachments/assets/3e347c47-b66a-4e91-9608-9770a6202b35" />

  shared-vpc to app-vpc
  <img width="1104" height="736" alt="image" src="https://github.com/user-attachments/assets/3204bbff-bebd-4e37-83bf-e6f2f205a3d8" />

