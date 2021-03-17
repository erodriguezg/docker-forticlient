# Forticlient for Docker

Connect to a FortiNet VPNs through docker container. 

## Usage

```bash
# Start the privileged docker container

# -d => detached mode (you can use -it to run it interactively)
# --name => specify a name of the container
# --label => labels are not necessary but can help to identify and filter the containers
# --privileged => this is vital to run VPN containers in a privileged mode (or use caps)
# -p => # use mapped ports to allow access to anyone in your network (using a port on the left side)

# -e "VPNADDR=vpn-gateway-ip:port" => specify VPN gateway and port (defined by your VPN provider)
# -e "VPNUSER=[user-id]" => VPN user ID (defined by your VPN provider)
# -e "VPNPASS=[pwd]" => VPN user password (defined by your VPN provider). You can use DOCKER SWARM secrets to make this more secure.
# -e "TUNNELIP=192.168.1.123" => IP of the remote connection throw VPN (target IP inside the VPN)
# -e "TUNNELPORT=3380" => PORT of the remote PC connection throw VPN (target PORT inside the VPN)

docker run \
  -d \
  --name vpn-test1 \
  --label container-type=vpnclient \
  --label vpn-type=forticlient \
  --label customer=customer-XYZ \
  --privileged \
  -p 51234:3380 \
  -e "VPNADDR=vpn-gateway-ip:port" \
  -e "VPNUSER=[user-id]" \
  -e "VPNPASS=[pwd]" \
  -e "TUNNELIP=192.168.1.123" \
  -e "TUNNELPORT=3380"
  erodriguezg/docker-forticlient
```