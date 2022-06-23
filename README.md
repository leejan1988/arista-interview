![Arista CloudVision Automation](https://img.shields.io/badge/Arista-CVP%20Automation-blue) ![Arista EOS Automation](https://img.shields.io/badge/Arista-EOS%20Automation-blue)

# AVD Arista Validated Design for Arista Test Drive

## About

This repository is configured to run [`arista.cvp`](https://github.com/aristanetworks/ansible-cvp) & [`arista.avd`](https://github.com/aristanetworks/ansible-avd) ansible collections against the Arista Test Drive (ATD) Topology.

<p align="center">
  <img src='docs/imgs/cv_ansible_logo.png' alt='Arista CloudVision and Ansible'/>
</p>

To access an Arista Test Drive topology, please contact your Arista representative.

## Lab Topology

The ATD Lab topology consists of 2 Spines, 4 Leafs and 2 Hosts, as shown below.

<p align="center">
  <img src="docs/imgs/atd-topo.png" alt="ATD Lab Topology" width="600"/>
</p>

## ATD Topology Device List

| Device | IP Address   |
| ------ | ------------ |
| spine1 |192.168.0.10 |
| spine2 |192.168.0.11 |
| leaf1  |192.168.0.12 |
| leaf2  |192.168.0.13 |
| leaf3  |192.168.0.14 |
| leaf4  |192.168.0.15 |
| host1  |192.168.0.16 |
| host2  |192.168.0.17 |

> Current repository is built with cEOS management interface (`Management0`). If you run a vEOS topology, please update `mgmt_interface` field to `Management1` in [inventory](./atd-inventory/group_vars/ATD_LAB.yml)

## Getting Started

Connect to your ATD Lab environment.
- If you need an ATD Lab instance, please contact your local account team.
- Once connected to the ATD Lab instance, select the Programmability IDE.
- This container is built with all the necessary requirements and Python modules to run AVD playbooks.

1. Setup Git user and email and the ATD lab environment.

    - Open a terminal window in VS Code View -> Terminal from the menu, and run the following commands:

    ```shell
    # Setup your git global config (optional)
    $ git config --global user.email "you@example.com"
    git config --global user.name "Your Name"

    # Run Script to setup environment
    $ curl -fsSL https://get.avd.sh/atd/install.sh | sh
    ```

2. Update Inventory with Lab Credentials

    - Open file in VS Code: atd-avd/atd-inventory/inventory.yml

    - Set credentials in the `inventory.yml` to the credentials provided on the Arista Test Drive landing page.


3. Run the Playbook to Prepare CloudVision for AVD

    - Execute the following commands:

    ```shell
    # Change to ATD-AVD directory
    $ cd labfiles/arista-ansible/atd-avd

    # Run Playbook to Prepare CloudVision for AVD
    $ ansible-playbook playbooks/atd-prepare-lab.yml
    ```

 - Verify that tasks in CloudVision have been executed automatically.

4. Run playbook to deploy AVD setup

    - Execute the following commands:

    ```shell
    # Run Playbook to Deploy AVD Setup
    $ ansible-playbook playbooks/atd-fabric-deploy.yml
    ```

    -  Execute pending tasks in CloudVision Portal manually.

5. Run validation and snapshot playbooks.

    - Execute the following commands:

    ```shell
    # Run audit playbook to validate Fabric states
    $ ansible-playbook playbooks/atd-validate-states.yml

    # Execute EOS_SNAPSHOT role to collect show commands
    $ ansible-playbook playbooks/atd-snapshot.yml
    ```

    - Review generated output.

## Step by Step walkthrough

A complete [step-by-step guide](./DEMO.md) is available

## Resources

- [Arista Ansible AVD Collection](https://github.com/aristanetworks/ansible-avd)
- [Arista Cloudvision Collection](https://github.com/aristanetworks/ansible-cvp)
- [Arista AVD public documentation](https://www.avd.sh)

## License

This Project is published under [Apache License]().
