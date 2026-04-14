FROM quay.io/redhat-user-workloads/ose-osc-tenant/osc-podvm-payload-v1-11@sha256:49054c05d3a1aff308fcf9decaa6652bdf6d33eb7494de0af416c8355f454e46 as payload

FROM registry.redhat.io/ubi9/ubi-init@sha256:3f9cb52568d60cf44b1a0baf593707b0869b4a2c2e8b744bc805b936ba3ae2ef

RUN subscription-manager register --org "$(cat /activation-key/org)" --activationkey "$(cat /activation-key/activationkey)"

RUN dnf install -y \
cpio systemd-ukify jq openssl qemu-img libguestfs guestfs-tools libguestfs-tools virt-install qemu-kvm edk2-ovmf nc

COPY qemu.conf /etc/libvirt/qemu.conf

COPY --from=payload /podvm-binaries.tar.gz /payload/
COPY --from=payload /pause-bundle.tar.gz /payload/

# to make virt-customize work
ENV LIBGUESTFS_BACKEND=direct

