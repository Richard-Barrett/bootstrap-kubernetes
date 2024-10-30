<img align="right" width="60" height="60" src="https://github.com/devicons/devicon/blob/master/icons/ansible/ansible-plain-wordmark.svg">

# Ansible Role: bootstrap-kubernetes

[![Ansible Lint](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/ansible-lint.yml)
[![CodeQL](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/codeql.yaml/badge.svg)](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/codeql.yaml)
[![Molecule Test](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/molecule.yml/badge.svg)](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/molecule.yml)
[![Trivy Scan](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/trivy.yaml/badge.svg)](https://github.com/Richard-Barrett/bootstrap-kubernetes/actions/workflows/trivy.yaml)

- `Description`: An Ansible Role to Bootstrap Kubernetes on BareMetal/Virtual Machines

- `Overview`: An Ansible role to install Kubernetes across various operating systems and CPU architectures in a controlled, versioned manner with configurable CNI plugins.

## Requirements

- Ansible 2.9+
- Supported OS:
  - Ubuntu (focal, bionic, jammy)
  - Debian (buster, bullseye)
  - CentOS/RHEL (7, 8, 9)
  - SUSE (openSUSE Leap 15.x, SLES 12-SP5, 15-SPx, Tumbleweed)
- Supported Architectures:
  - `x86_64`
  - `arm64`

## Role Variables

| Variable               | Default                | Description                                               |
|------------------------|------------------------|-----------------------------------------------------------|
| `kubernetes_version`   | `1.26.0`               | Kubernetes version to install                             |
| `cni_plugin`           | `calico`               | CNI plugin to use (`calico`, `flannel`, `weave`)         |
| `pod_network_cidr`     | `192.168.0.0/16`       | Pod network CIDR (adjust based on CNI requirements)       |
| `k8s_admin_user`       | `{{ ansible_user }}`   | User to configure kube config                             |
| `supported_architectures` | `["x86_64", "arm64"]` | List of supported CPU architectures                       |
| `arch_packages`        | See below              | Mapping of architectures to Kubernetes package names      |

### `arch_packages` Structure

```yaml
arch_packages:
  x86_64:
    kubelet: "kubelet-{{ kubernetes_version }}"
    kubeadm: "kubeadm-{{ kubernetes_version }}"
    kubectl: "kubectl-{{ kubernetes_version }}"
  arm64:
    kubelet: "kubelet-{{ kubernetes_version }}"
    kubeadm: "kubeadm-{{ kubernetes_version }}"
    kubectl: "kubectl-{{ kubernetes_version }}"
```
