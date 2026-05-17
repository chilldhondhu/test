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

